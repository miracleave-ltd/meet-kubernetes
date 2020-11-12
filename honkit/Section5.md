# Section5

今回のハンズオンで汚してしまった環境を片づけます。

1. kubernetesからdeploymentsの情報を取得して、現在存在するdeploymentsの情報をKubernetesから削除します。

    ```shell
    kubectl get deploy
    # NAME       READY   UP-TO-DATE   AVAILABLE   AGE
    # nginx      1/1     1            1           97m
    # postgres   1/1     1            1           97m
    # server     1/1     1            1           97m
    kubectl delete deploy nginx postgres server
    ```

2. kubernetesからservicesの情報を取得して、現在存在するservicesの情報をKubernetesから削除します。

    ```shell
    kubectl get svc
    # NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE  
    # kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP          6d21h
    # nginx        NodePort    10.106.171.137   <none>        8000:30445/TCP   100m 
    # postgres     ClusterIP   10.109.66.138    <none>        5432/TCP         100m 
    # server       ClusterIP   10.96.82.23      <none>        3001/TCP         100m
    kubectl delete svc nginx postgres server
    ```

3. kubernetesから各情報が削除されたことを確認します。
    ※service/kubernetesは標準で起動されるものとなります。

    ```shell
    kubectl get pod,svc,deploy
    # NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
    # service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   6d21h
    ```
