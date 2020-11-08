# はじめに

## 前提

- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Git](https://git-scm.com/)

※Windows/MacOSで確認しました。

## Kubernetes

Docker Desktopには、Kubernetesサーバーとクライアントが内包されています。
Dockerインスタンス内でローカルに実行され、単一ノードクラスターとなっています。

1. タスクバーにある![docker-icon](img/docker-desktop.png)を右クリックして、 `Settings` を選択してください。
2. メニューにある `Kubernetes` を選択してください。
    ![docker-desktop-kubernetes](img/docker-desktop-kubernetes.png)
3. `Enable Kubernetes` をチェックし、 `Apply&Restart` をクリックしてください。  
    しばらくすると③の箇所にKubernetes Runningと表示します。
    ![docker-desktop-kubernetes-enable](img/docker-desktop-kubernetes-enable.png)

## Kompose

### Windowsの場合

Windowsでは、Chocolateyでインストールできます。

※Chocolateryをインストールしていない方は[こちら](Chocolatery.md)

```PowerShell
choco install kubernetes-kompose
```

### MacOSの場合

MacOSでは、Homebrewでインストールできます。

※Homebrewをインストールしていない方は[こちら](Homebrew.md)

```Shell
brew install kompose
```
