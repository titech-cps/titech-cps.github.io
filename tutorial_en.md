# M5Stack How-to

M5Stack is an open-source modular toolkit for IoT devices.
This tutorial explains how to set up a development environment for M5Stack on your PC.

## About M5Stack

An M5Stack module is an enclosed device that consists of an ESP32 SoC and several peripheral components, including three buttons, an LCD, and a speaker. 

* Models
  - M5Stack Core Basic
  - M5Stack Core Gray (used in this tutorial)
  - M5Stack Fire
* Processor: ESP32 SoC (see below)
  - CPU: Dual 240MHz LX6
  - Memory: 512KB
* Flash: 4MB
* Peripheral Components
  - ILI9341 320x240 Color TFT LCD
  - Speaker
  - 3 x button
  - MPU9250 9-Axis Motion Sensor (M5Stack Core Gray, M5Stack Fire)
  - CP2104 USB-UART Adapter
  - Li-Po Battery
* Ports
  - USB-C
  - MBUS (GPIO etc.)
  - Grove (I2C)
  - micro-SD
* Size: 54 x 54 x 17 mm
* Weight: 120g
* Web
  - http://www.m5stack.com
  - https://github.com/m5stack/M5Stack

## About ESP32

ESP32 is a series of low-cost, low-power SoC microcontrollers with integrated WiFi and Bluetooth capabilities, created and developed by Espressif.  Apart from M5Stack, many ESP32-based modules and development boards are available.

* Processors
  - Dual 160/240MHz Xtensa LX6 (Tensilica)
  - ULP (Ultra Low Power) Co-Processor
* Memory: 520KB SRAM
* Wireless
  - WiFi 802.11 b/g/n (2.4GHz)
  - Bluetooth v4.2 BR/EDR & BLE
* Peripheral I/F
  - 18 x 12bit ADC
  - 2 x 8bit DAC
  - 10 x capacitive touch sensors
  - temperature sensor
  - 4 x SPI
  - 2 x I2S
  - 2 x I2C
  - 3 x UART
  - SD/SDIO/CE-ATA/MMC/eMMC host controller
  - SDIO/SPI slave controller
  - Ethernet MAC I/F
  - CAN bus 2.0
  - 8 x Infrared TX/RX
  - Motor PWM
  - 16 x LED PWM
  - Hall Effect Sensor
  - Ultra low power analog pre-amplifier
* Security
  - IEEE 802.11 WFA, WPA/WPA2 and WAPI
  - Secure boot
  - Flash encryption
  - 1024bit OTP
  - Cryptographic H/W acceleration: AES, SHA-2, RSA, ESS, RNG
* Web
  - https://www.espressif.com
    + https://www.espressif.com/en/products/hardware/esp32/overview
  - https://github.com/espressif
    + https://github.com/espressif/esp-idf
    + https://github.com/espressif/arduino-esp32


-----
## Development Environment

### Toolchain & Library for ESP32

* ESP32(LX6)用のgcc： Espressif 社が無償で提供
* 基本ランタイムライブラリ：FreeRTOSベース

-----
### 統合開発環境

* ESP-IDF
  - Official Development Environment for ESP32 by Expressif
    + https://docs.espressif.com/projects/esp-idf/en/latest/
    + https://github.com/espressif/esp-idf
  - CUI
  - M5Stackの開発にはArduinoライブラリとM5Stackライブラリが必要
    + https://github.com/m5stack/M5Stack
* Arduino IDE
  - ArduinoというマイコンボードのためのGUIベースの開発環境
    + https://www.arduino.cc
  - ESP32は公式にサポートされている(Arduino ESP32)
    + https://github.com/espressif/arduino-esp32
  - M5Stackの開発にはM5Stackライブラリが追加で必要
    + https://github.com/m5stack/M5Stack
* PlatformIO
  - 各種マイコンボード（およびデスクトップ）のための統合開発環境
    + https://platformio.org
  - コマンドラインおよびVSCode, Atom用プラグイン
    + VSCodeプラグインがおすすめ
  - ESP32は公式にサポートされている
  - M5Stackライブラリもサポートされている

その他，MicroPythonやUIFlow等．

-----
## 開発環境のセットアップ

必要なもの

* 開発用PC
  - Mac, Linux, Windowsのどれか
  - TODO: 必要なスペック等
* M5Stack Core Gray
* USB-Cケーブル（M5Stack Coreに付属）

M5Stack上で動作するプログラムの開発方法はいくつかあるが，ここでは，開発用PC上でビルドしたプログラムを，USBケーブルでM5Stackにアップロードする（クロス開発）方法について説明する．
他にも，PCあるいはクラウドベースの開発環境で作成したプログラムをWiFi経由でアップロードする方法もある．

セットアップの概要

* USB-UARTドライバのインストール（必須）
* IDEのセットアップ：以下のいずれか
  - Arduino IDE
  - ESP-IDF
  - PlatformIO

-----
### USB-UARTドライバのインストール

M5StackはSilicon Labs社のCP2104 USB-UARTインターフェースを内蔵しており，開発用PCとの通信に用いている．これを用いるためのドライバを開発用PCにインストールする．
以下から使用するOSに対応したドライバをダウンロードしてインストールする．

* https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers

ドライバ問題なくインストールされると，M5Stackを接続したときに以下のようなシリアルポートが現れる．

* Mac: `/dev/cu.SLAB_USBtoUART`
* Linux: `/dev/tty??`
* Windows: ?

**重要**：M5Stackを接続してもシリアルポートが現れない場合，M5Stack側のUSB-Cコネクタを180度回して挿し直してみること．

-----
### Arduino IDEのセットアップ

#### インストール

Arduino IDEを以下からダウンロードしてインストールする．

* https://www.arduino.cc/en/Main/Software

Macの場合は，ダウンロードしたzipファイルを展開し，出てきたアプリケーションを/Applicationsフォルダに移せばよい．

#### M5Stackの開発ができるようにする

##### 方法1

Arduino IDE のボードマネージャ，ライブラリマネージャを用いてお手軽にセットアップする．

* Arduino IDEの設定(Preference)で，"Additional Boards Manager URLs"に以下を追加する．
  - `https://dl.espressif.com/dl/package_esp32_index.json`
* Arduino IDEのメニュー Tools/Board: "..."/Boards Manager... を選択してボードマネージャを起動する．"Filter your search..." とある欄に ESP32 と入れて，esp32 by Espressif Systems をインストールする．Arduino ESP32だけでなく，コンパイラや基本ライブラリもこれで一緒にインストールされる．
* Arduino IDEのメニュー Tools/Manage Libraries... でライブラリマネージャを起動する．
"Filter your search..." とある欄に M5Stack と入れて，M5Stack by M5Stack をインストールする．

##### 方法2

方法1だとライブラリのアップデートへの対応が（とても）遅いので，GitHub上のライブラリをクローンして用いる．

* 以下の "Installing the ESP32 Arduino Core" にしたがって Arduino ESP32 および M5Stack 用ライブラリをそれぞれインストールする．
  - https://github.com/m5stack/m5stack

#### テスト

1. M5StackをUSBケーブルで接続する．
2. Tools/Board: "..." で "M5Stack-Core-ESP32" を選ぶ
3. Tools/Port をM5Stackのポートに設定する．
   - Mac: `/dev/cu.SLAB_USBtoUART`
4. File/Examples/M5Stack/Basics/HelloWorld を選ぶ
5. Sketch/Verify/Compile でコンパイルする
6. Sketch/Upload でM5Stackにアップロードする
7. M5StackのLCDに "Hello World" と表示されればOK

-----
### ESP-IDFのセットアップ

* https://docs.espressif.com/projects/esp-idf/en/latest/get-started/

#### インストール

##### ツールチェインのセットアップ

以下のツールチェインをダウンロード

* https://dl.espressif.com/dl/xtensa-esp32-elf-osx-1.22.0-80-g6c4433a-5.2.0.tar.gz

ホームディレクトリに`esp`ディレクトリを作成して，ツールチェインをインストール

```Bash
$ cd
$ mkdir esp
$ cd esp
$ tar -xvf ~/Download/xtensa-esp32-elf-osx-1.22.0-80-g6c4433a-5.2.0.tar.gz
```

##### ESP-IDFをインストール

```bash
$ git clone --recursive https://github.com/espressif/esp-idf.git
```

##### 環境変数のセットアップ

* `IDF_PATH` の値を `$HOME/esp/esp-idf` とする
* `PATH` に `$HOME/esp/xtensa-esp32-elf/bin` を追加する

##### ライブラリのインストール

ここまでで，ESP32のための基本的な開発環境がインストールされている．
M5Stackの開発には，以上に加えて Arduino ESP32 ライブラリと，M5Stack ライブラリが必要になる．
Arduino ESP32 ライブラリは esp-idf というブランチを指定すること．

```bash
$ cd ~/esp
$ mkdir components
$ cd components
$ git clone -b idf-update --recursive https://github.com/espressif/arduino-esp32
$ git clone https://github.com/m5stack/M5Stack
```

##### テスト

 M5StackをUSBケーブルで開発用PCに接続する

プロジェクトディレクトリを作成
```bash
$ cd ~/esp
$ mkdir -p HelloWorld/main
$ cd HelloWorld
```

`Makefile` を作成
```Makefile
PROJECT_NAME := HelloWorld
EXTRA_COMPONENT_DIRS := $(HOME)/esp/components
include $(IDF_PATH)/make/project.mk
```

mainディレクトリ下にソースファイル等を作成
```bash
$ cd main
$ touch component.mk
```

`main.cpp` を作成
```C++
#include <M5Stack.h>

void setup(){
  M5.begin();
  M5.Lcd.print("Hello World");
}
void loop() {}
```

プロジェクトの構成

```bash
$ cd ~/esp/HelloWorld
$ tree
.
|-- Makefile
`-- main
    |-- component.mk
    `-- main.cpp
```

ビルド

Mac の場合，OS付属のmakeだと途中でエラーになることがある．

```bash
$ gmake menuconfig
$ gmake
$ gmake flash
```

`gmake menuconfig` の設定

-----
### PlatformIOのセットアップ

Visual Studio Code のExtensionsで，PlatformIO IDE をインストールする．


