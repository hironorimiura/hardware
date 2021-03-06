
# Degu Baseboard / Degu ベースボード

<a href="https://open-degu.com"><img src="images/degu_logo.png" alt="Degu logo" width="400"></a>

This repository contain the Degu baseboard circuit, BOM and reference of parts number on PCB.  
このリポジトリにはDeguベースボードの回路図、部品表、基板上の部品配置図が含まれます。


# Hardware Overview / 概要

![](images/Degu_Baseboard_pinout.png)

- Analog Port: include 3 anlog ports, AIN1, AIN2 and AIN3.
- Digital Port: include 3 digital ports, DIO1, DIO2 and DIO3.
- UART Port: 1 UART port.
- I2C Port: 1 I2C port.
- USB Port: 1 micro USB port.
- SWD Port: 1 SWD port.
- Switch: include 4 switchs, SW1 for resets, SW4 for DFU with bootloader , SW2 and SW3 are generic use.
- LED: include 4 LEDs(GREEN), LED1 and LED2 are lead type round top molded, LED3 and LED4 are surface mounted.
- UART Port: 1 UART Port.

------

- アナログポート: アナログ ポート * 3, AIN1、AIN2、AIN3
- デジタルポート: デジタルポート * 3, DIO1、DIO2、DIO3
- UARTポート: UART ポート * 1
- I2C ポート: I2C ポート * 1
- USB ポート: micro USB ポート * 1
- SWD ポート: SWD ポート * 1
- スイッチ: SW1はリセットボタンです。SW4はブートローダーをDFUモードにするために使います。 SW2とSW3は汎用スイッチです。
- LED: 緑色 * 4, LED1とLED2は砲丸型です。 LED3とLED4は表面実装型です。

## Pin Headers / ピンヘッダー

![](images/pin_header_pinout.png)

- Pin Headers: include 2 Pin headers, same lines to connected with AIN,DIO,UART,I2C Ports and extra 5 gpios.

-----

- ピンヘッダー: AIN,DIO,UART,I2C ポートと同じ信号が接続されています。それ以外に追加の5本のGPIO接続されています。

# Power Supply / 電源投入方法

-   ①USB microBコネクタ経由での5V給電
-   ②JST 2pin PHコネクタ経由での3.3V～5.5V給電
-   ③ JST 2pin PHコネクタ経由での3V給電(コイン電池等)

## JST 2pin PHコネクタ経由で給電する祭の注意

初回出荷品に関して、CON12 PHコネクタに接続されているケーブルの極性が
逆向きになっている可能性があり、逆向きの状態で給電した場合、故障する可能性があります。
接続されているケーブルの色が、基板のシルク印字に対して、赤：VIN，黒：GNDとなっていることを確認してください。
極性が逆向きになっている場合には交換対応いたしますので、購入店までお問い合わせください。

<a href="https://open-degu.com"><img src="images/con12_ok.png" alt="con12 ok image" width="300"></a>
<a href="https://open-degu.com"><img src="images/con12_ng.png" alt="con12 ng image" width="300"></a>

### ① USB microBコネクタ経由での5V給電時

|リファレンス番号|状態|
--|--
|JP1|1-2pinをショート|
|JP2|1-2pinをショート|
|JP3|1-2pinをショート|

![](images/JP-USB.svg)

### ② JST 2pin PHコネクタ経由での3.3V～5.5V給電

|リファレンス番号|状態|
--|--
|JP1|1-2pinをショート|
|JP2|1-2pinをショート|
|JP3|1-2pinをオープン|

![](images/JP_PH.svg)

### ③ JST 2pin PHコネクタ経由での3V給電(コイン電池を想定)

<span style="color: red;">この設定の場合はPHコネクタからの入力電圧が3.6Vを超えることの無いようにしてください。</span>\

|リファレンス番号|状態|
--|--
|JP1|JP1の1pin-JP2の1pinをショート|
|JP2|JP1の2pin-JP2の2pinをショート|
|JP3|1-2pinをオープン|

![](images/JP-COIN.svg)


# Antenna directivity and installation / アンテナの指向性と設置方法

## アンテナの指向性

Deguベースユニット、DeguゲートウェイG3に内蔵されているThread通信用のアンテナには指向性があります。
以下の図のように天面方向へ強く電波が飛びます。※製品面の定義については下記を参照してください。

#### Deguベースユニット　　　　　　　　　　　　　　DeguゲートウェイG3
![](images/degu_base_unit_ant_directivity.svg) ![](images/degu_gw_g3_ant_directivity.svg)

### Deguベースユニット製品面の定義

<img src="images/degu_base_unit_surface.svg" width="600" />

### DegeゲートウェイG3製品面の定義

![](images/degu_gw_g3_surface.svg)

## 設置方法

Deguベースユニット、DeguゲートウェイG3を設置する際には、アンテナの指向性を考慮し
以下の図のように、それぞれの天面方向が向かいあわせになるように設置することを推奨します。
また、通信経路上の障害物ができるたけ少なくなるような高さに設置することも重要になります。

![](images/degu_installation.svg)

## フレネルゾーンの確保

安定した無線通信を行うためには、DeguベースユニットとDeguゲートウェイG3間、またはDeguベースユニットとDeguベースユニット間
の通信経路においてフレネルゾーンを確保する必要があります。
フレネルゾーンとは、アンテナ間を結ぶ直線を中心に広がる回転楕円体の空間で、この空間内に障害物があると無線通信に影響します。
フレネルゾーンの中で、中心部分の半径をフレネルゾーン半径と呼び、一般的にフレネルゾーン半径の60％以上を確保すれば自由空間と同じ特性を得られると言われています。
フレネルゾーン半径r[m]は、アンテナ間距離から以下のように算出することができます。

![](images/fresnel_zone.svg)

2.4GHzの波長 λ=0.125[m]、アンテナから中心部までの距離 d1[m],d2[m]

<img src="https://latex.codecogs.com/gif.latex?r=\sqrt{\frac{\lambda&space;\times&space;d1\times&space;d2}{d1&plus;d2}}" />

アンテナ間距離が100mの場合、フレネルゾーン半径r[m]は以下の計算式から約1.8mとなります。
したがって、安定した通信を行うためにはDeguベースユニットおよびDeguゲートウェイG3を約1.8m以上(60%だと1.08m以上)の高さに設置することが望ましいと言えます。

<img src="https://latex.codecogs.com/gif.latex?r=\sqrt{\frac{0.125\times&space;50\times&space;50}{50&plus;50}}\fallingdotseq&space;1.8" />


