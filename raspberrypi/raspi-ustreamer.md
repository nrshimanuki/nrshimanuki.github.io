ラズパイ見守りカメラ（1号）
======================

## 用意したもの

* Raspberry Pi 4
* microSDカード 32GB
* Raspberry Pi Camera B01


## インストール

* Raspberry Pi OS Lite
* ustreamer


## カメラの撮影テスト

```
libcamera-hello
libcamera-jpeg -o test.jpg
```

### 他のターミナルからプロセスを強制終了する

* 実行中の libcamera-vid のPID（プロセスID）を探す

```
ps aux | grep libcamera
kill -9 12345
```


## ustreamer

### Install

```
// 依存 modules を install
$ sudo apt install libevent-dev libbsd-dev libcamera-v4l2
$ sudo apt install libcairo2-dev libjpeg62-turbo-dev libpango1.0-dev libgif-dev build-essential g++

$ git clone --depth=1 https://github.com/pikvm/ustreamer
$ cd ustreamer
$ make
```

###  Run
```
$ cd ustreamer
$ ./ustreamer --device=/dev/video0 --host=0.0.0.0 --port=8080
```

* IPアドレスか、ドメイン名でブラウザからアクセス
	* http://192.168.1.xxx:8080
	* http://raspberrypi.local:8080
* /stream をクリック


## 実際に使用したコマンド

```
sudo ssh pi@raspberrypi.local // (例)
```

```
cd ustreamer
./ustreamer --device=/dev/video0 --host=0.0.0.0 --port=8080 --resolution=640x480 --quality=40 --desired-fps=10
```

OR （ホームディレクトリから実行の場合）

```
ustreamer/ustreamer --device=/dev/video0 --host=0.0.0.0 --port=8080 --resolution=640x480 --quality=40
```

### 常時起動

* nohup は SSH 切断後もコマンドを実行し続けるツール

```
nohup ./ustreamer --device=/dev/video0 --host=0.0.0.0 --port=8080 --resolution=640x480 --quality=40 --desired-fps=10 > ustreamer.log 2>&1 &
```

### 稼働中のプロセス確認
```
ps aux | grep ustreamer
kill <ID>
```


## Raspberry Pi の電源を入れたときに自動的に ustreamer を起動させる方法

### systemdサービスとして登録する
* systemdは現代のLinuxで標準的な起動管理システムで、再起動や自動起動に強い。

#### 設定手順（例）
* サービスファイル作成

```
sudo nano /etc/systemd/system/ustreamer.service
```

* 以下の内容を貼り付け（パスやオプションは適宜変更）

```
[Unit]
Description=Ustreamer Service
After=network.target

[Service]
ExecStart=/home/pi/ustreamer/ustreamer --device=/dev/video0 --host=0.0.0.0 --port=8080 --resolution=640x480 --quality=70 --desired-fps=8
Restart=always
User=pi
WorkingDirectory=/home/pi/ustreamer

[Install]
WantedBy=multi-user.target
```

#### サービスの読み込みと有効化
```
sudo systemctl daemon-reload
sudo systemctl enable ustreamer.service
```

#### 手動で起動確認
```
sudo systemctl start ustreamer.service
sudo systemctl status ustreamer.service
```


## 補足: 他の選択肢

### Raspberry Pi OS + Motion
* 自由度高め
* 通常のRaspbian（Raspberry Pi OS）に motion というソフトを追加して動作させる方法
* Web配信、録画、モーション検知など可能
* Pythonスクリプトなどと組み合わせて拡張しやすい

* セットアップ手順概要（ターミナル）：
```
sudo apt update
sudo apt install motion
sudo nano /etc/motion/motion.conf
daemon on
stream_localhost off
```

framerate, width, height なども調整可能

* Motionを有効化して起動：
```
sudo systemctl enable motion
sudo systemctl start motion
→ http://<PiのIPアドレス>:8081 にアクセスで映像が見れる。
```

* 録画データの保存・外部連携
	* microSDに保存（注意：寿命短くなるため要バックアップ）
	* 外付けHDDやNASに保存
	* DropboxやGoogle Drive連携（rcloneなど）
	* メールやLINE通知も可能（モーション検出時）


## 補足: 拡張案

* 顔認識（OpenCV + Python）
* Webアプリ連携（Flask + HTML）


## 補足: 上手くいかなかったこと

* MotionEyeOS
	* Raspberry Pi 4 ではエラーになって起動してくれなかった

* MotionEye
	* Raspberry Pi OS での Python 環境が「外部管理」されている（PEP 668 の仕様に準拠）ために、sudo python3 get-pip.py のような システム全体への直接的な Python パッケージのインストールが制限されている。
	* Debian Bookworm や Ubuntu 23.04 以降に導入された PEP 668 により、Python のシステム領域は保護されており、pip による直接インストールを 明示的に拒否するようになっている。
	* 仮想環境を使う方法があるみたいだけど、今回はパス。


## 補足: Bullseye以降のOS

* 設定が変わっているもの多数
* 検索した情報が古いことが多いので注意
* (例)
	* Raspberry Pi OS（Bullseye以降）では raspi-config に「P1 Camera」の項目が表示されなくなった。これは、従来の raspistill / raspivid が廃止され、新しいカメラスタック（libcamera）が導入されたため。
	* vcgencmd get_camera は 古いカメラシステム（raspistill/raspivid）向けの診断コマンド。現在の Raspberry Pi OS（Bullseye以降）では 新しいカメラシステム（libcamera） が導入され、vcgencmd get_camera の結果は 信頼できなくなっている。
	つまり：supported=0 detected=0 と表示されても libcamera-hello が映像を表示できていれば、カメラは正常に認識・動作している。
