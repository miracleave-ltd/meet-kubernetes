# はじめに

## 前提

- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Git](https://git-scm.com/)

※Windows/MacOSで確認しました。

## Kubernetes

Docker Desktopには、Kubernetesサーバーとクライアントが内包されています。
Dockerインスタンス内でローカルに実行され、単一ノードクラスターとなっています。

1. タスクバーにある![docker-icon](img/docker-desktop.png)を右クリックして、 `Settings` を選択してください。
    Macの方：Dashboard,もしくはpreferenceをクリックしてください。
2. メニューにある `Kubernetes` を選択してください。
    ![docker-desktop-kubernetes](img/docker-desktop-kubernetes.png)
3. `Enable Kubernetes` をチェックし、 `Apply&Restart` をクリックしてください。  
    しばらくすると③の箇所にKubernetes Runningと表示します。
    ![docker-desktop-kubernetes-enable](img/docker-desktop-kubernetes-enable.png)

## Kompose

### Windowsの場合

Windowsでは、Chocolateyでインストールできます。

※Chocolateryをインストールしていない方は[こちら](Chocolatery.md)

1. Power Shellを起動する
2. Windowsのスタートボタンを押します。
3. メニューにある「Windows PowerShell」を右クリックして、 `管理者として実行` を選択します。
4. Power Shellにインストールコマンドを入力し、実行します。

    ```PowerShell
    choco install kubernetes-kompose
    ```

5. `choco list -l` を実行して、 `kubernetes-kompose` が表示されるとインストール完了です。

    ```PowerShell
    PS C:\> choco list -l
    Chocolatey v0.10.15
    chocolatey 0.10.15
    kubernetes-kompose 1.22.0
    2 packages installed.
    ```

### MacOSの場合

MacOSでは、Homebrewでインストールできます。

※Homebrewをインストールしていない方は[こちら](Homebrew.md)

1. ターミナルを起動する。
2. ターミナルにインストールコマンドを入力し、実行します。

    ```Shell
    brew install kompose
    ```

3. `brew list` を実行して、 `kompose` が表示されるとインストール完了です。

    ```Shell
    pc:go-react-todo-master pc$ brew list
    kompose
    ```
