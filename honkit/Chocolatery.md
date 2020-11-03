# Chocolateryインストール手順

## Chocolateryとは

![chocolatery](img/chocolatery.png)

OSや言語毎にパケージマネージャとよばれるツールが提供され、ソフトウエアや拡張機能のインストールはパッケージマネージャを利用して行うことができます。

ChocolateryはWindows用のパッケージマネージャーとなります。

## インストール手順

1. Power Shellを起動する
2. Windowsのスタートボタンを押します。
3. メニューにある「Windows PowerShell」から「Windows PowerShell」を選択します。
4. Chocolatery公式サイトにある[インストールページ](https://chocolatey.org/install)にアクセスし、インストールコマンドを確認します。
5. Power Shellにインストールコマンドを入力し、実行します。

```PowerShell
PS C:\> Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

### 動作確認

- chocoコマンドが実行できればインストール完了です。

```PowerShell
PS C:\> choco list -l
Chocolatey v0.10.15
chocolatey 0.10.15
1 packages installed.
```

以上でインストールは完了です。
