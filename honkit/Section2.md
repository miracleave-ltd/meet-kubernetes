# Section2

## Komposeを利用して、Kubernetes用yamlを作成しよう

React+Go(Gin)+PostgresSQLのテンプレートを利用させてもらおうと思います。

1. 今回利用するテンプレートの[GitHub](https://github.com/el10savio/TODO-Fullstack-App-Go-Gin-Postgres-React)よりプログラムをダウンロードします。

    ![github-source-dl](img/github-source-dl.png)

2. Komposeコマンドでdocker-compose.ymlを変換します。  
    ※ダウンロードしたファイルを解凍したフォルダで実行してください。

    ```Shell
    kompose convert
    ```

    (WindowsPowerShell)
    ![kompose-convert-powershell](img/kompose-convert-powershell.png)

3. 変換後の確認を行います。  
    次のファイルが生成されていることを確認してください。

    - go-api-service.yaml
    - postgres-service.yaml
    - react-app-service.yaml
    - go-api-deployment.yaml
    - postgres-deployment.yaml
    - react-app-deployment.yaml

4. ダウンロードしたプログラムに誤りがあるため、修正を行います。

    対象ファイル：(TODO-Fullstack-App-Go-Gin-Postgres-React-master)/database/Dockerfile

    ```Shell
    - 7 COPY init /docker-entrypoint-initdb.d/
    + 7 COPY *.sql /docker-entrypoint-initdb.d/
    ```

5. ローカル環境にDockerイメージを作成します。
    ※ダウンロードしたファイルを解凍したフォルダで実行してください。

    ```Shell
    docker-compose build
    ```

6. Kubernetesに変換したファイルを反映します。

    ```Shell
    kubectl apply -f go-api-service.yaml -f postgres-service.yaml -f react-app-service.yaml -f go-api-deployment.yaml -f postgres-deployment.yaml -f react-app-deployment.yaml
    ```

    (WindowsPowerShell)
    ![kubectl-apply-kompose-file](img/kubectl-apply-kompose-file.png)

7. Kubernetesの状態確認を行います。

    ```Shell
    kubectl get pods
    kubectl get deployments
    kubectl get services
    ```

    (WindowsPowerShell)
    ![kubectl-get-pod-service](img/kubectl-get-pod-service.png)

8. 前述の赤枠部分について、*ImagePullBackOff*となり、正常にPodが起動していないため、起動するように修正します。  
    原因としては、DockerイメージをPullしようとしてきたが存在しないため、エラーとなっています。  
    ローカルのDockerイメージを取得するように修正します。  
    また、goのプログラムが単純にバグがあるので合わせて修正します。

    対象ファイル(1)：(TODO-Fullstack-App-Go-Gin-Postgres-React-master)/react-app-deployment.yaml

    ```yaml
    - 29 - image: react-app
    + 29 - image: todo-fullstack-app-go-gin-postgres-react-master_react-app
    - 30 imagePullPolicy: ""
    + 30 imagePullPolicy: Never
    ```

    対象ファイル(2)：(TODO-Fullstack-App-Go-Gin-Postgres-React-master)/go-api-deployment.yaml

    ```yaml
    - 29 - image: todo-fullstack-app-go-gin-postgres-react-master_go-api
    + 29 - image: go-api
    - 30 imagePullPolicy: ""
    + 30 imagePullPolicy: Never
    ```

    対象ファイル(3)：(TODO-Fullstack-App-Go-Gin-Postgres-React-master)/react-app-service.yaml

    ```yaml
    + 15 nodePort: 30000
    + 20 type: NodePort
    ```

    対象ファイル(4)：(TODO-Fullstack-App-Go-Gin-Postgres-React-master)/backend/api/api.go

    ```go
    - 24 // db, err = sql.Open("postgres", "postgres://postgres:password@postgres/todo?sslmode=disable")
    + 24 db, err = sql.Open("postgres", "postgres://postgres:password@postgres/todo?sslmode=disable")
    - 27 db, err = sql.Open("postgres", "postgres://postgres:password@localhost/todo?sslmode=disable")
    ```

    対象ファイル(5)：(TODO-Fullstack-App-Go-Gin-Postgres-React-master)/backend/main.go

    ```go
    - 6 api "./api"
    + 6 api "build/api"
    ```

9. Kubernetesに修正したファイルを反映します。

    ```Shell
    kubectl apply -f go-api-deployment.yaml -f react-app-deployment.yaml
    ```

    (WindowsPowerShell)
    ![kubectl-apply-deployment](img/kubectl-apply-deployment.png)

10. Kubernetesに反映したプロジェクトを確認します。  
    次のURLにアクセスしてください。  
    http://localhost:30000

    ![todo](img/todo.png)
