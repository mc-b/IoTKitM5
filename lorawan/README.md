LoraWAN
-------
***

![](images/lorawan.png)

Quelle: mbed 
- - - 

Sie können sich ein LoRaWAN als Netzwerk mit virtualisierter Netzwerkschicht vorstellen. Die Geräte kommunizieren mit dem Netzwerkserver unter Verwendung des LoRaWAN-Protokolls und bilden ein LoRaWAN-Netzwerk. Wenn mehrere Basisstationen Ihr Gerät abhören, leiten alle Ihr Paket an den Netzwerkserver weiter. Dies bedeutet, dass ein LoRaWAN-Gerät nicht in einer bestimmten Zelle lokalisiert ist.


Ein LoRaWAN-Netzwerk besteht aus drei grundlegenden Netzwerkelementen:
* Gerät.
* Basisstation.
* Network Server.

Die Basisstation hat die Aufgabe, über LoRa mit den Geräten in ihrem Empfangsbereich zu kommunizieren. Die eigentliche Netzwerksteuerung liegt in der Cloud, also im Netzwerkserver.

### The Things Network
***

![](images/the-things-network.png)

Quelle The Things Network
- - -

Das The Things Network (TTN) ist eine offene communitybasierte Initiative zur Errichtung eines energiesparenden Weitbereichs-Netzwerks für das Internet der Dinge.

Im öffentlichen Community-Netzwerk von The Things Network gilt eine [Fair Use Policy](https://www.thethingsnetwork.org/forum/t/fair-use-policy-explained/1300), die die **Uplink-Sendezeit auf 30 Sekunden pro Tag** und die Downlink-Nachrichten auf **10 Nachrichten pro Tag** pro Knoten begrenzt.

**Links**

* [The Things Network Console](https://eu1.cloud.thethings.network/console/applications)

### Unit LoRaWAN868
***

![](https://static-cdn.m5stack.com/resource/docs/static/assets/img/product_pics/unit/lorawan868/lorawan868_01.webp)

Quelle: M5Stack
- - -

Unit LoRaWAN868 ist ein LoRaWAN-Kommunikationsmodul, das für die 868-MHz-Frequenz geeignet ist und von M5Stack eingeführt wurde. 

Das Modul verwendet den [ASR6501](https://m5stack.oss-cn-shenzhen.aliyuncs.com/resource/docs/datasheet/unit/lorawan/ASR650X%20AT%20Command%20Introduction-20190605.pdf), das die Fernkommunikation unterstützt und sowohl einen extrem geringen Stromverbrauch als auch eine hohe Empfindlichkeit aufweist.

**AT Commands ASR6501**

**Hardware/Firmware Info**

* `AT+CGMI?` - Read Manufacturer Identification
* `AT+CGMM?` - Read Model Identification 
* `AT+CGMR?` - Read Version Identification

**Link Informationen**

* `AT+CJOINMODE=?` - Read Join Mode (0：OTAA, 1：ABP)      
* `AT+CDEVEUI=?` - Read DevEUI
* `AT+CAPPEUI?` -  Read AppEUI 
* `AT+CAPPKEY?` - Read AppKey
* `AT+CFREQBANDMASK?` - Read Frequency Band Mask (0001 = 0-7 channel, 0002 = ：8-15 channel)
* `AT+CCLASS?` - Read Class (0 = A, 1 = B, 2 = C)
* `AT+CNWKSKEY?` - Read NwkSKey
* `AT+ILOGLVL=5` - Set/Read Log Level
* `AT+DTRX?` - Send/Receive Data

### The Things Network und M5Stack
***

Verwendetes Material:
* [LPS8 Indoor Multichannel LoRaWAN Gateway](https://www.bastelgarage.ch/lps8-indoor-multichannel-lorawan-gateway) mit neuster Firmware! - Base Station
* [M5Stack BASIC](https://docs.m5stack.com/en/core/basic) oder [M5Stack Core2](https://docs.m5stack.com/en/core/core2). - End Device
* [Unit LoRaWAN868](https://docs.m5stack.com/en/unit/lorawan868) - LoRaWAN Modem

**Konfiguration Base Station**

![](images/base-station.png)

- - -

Die Daten vom der Base Station sind in The Things Network zu übertragen. Dazu ist ein [Gateway](https://eu1.cloud.thethings.network/console/gateways) anzulegen und die Daten (Dev EUI etc.) der Base Station zu übertragen.

**Konfiguration End Device in The Things Network**

![](images/end-device.png)

- - -

Im The Things Network ist zuerst eine Application und dann eine [End Device](https://eu1.cloud.thethings.network/console/applications) anzulegen.

* **DevEUI** kann generiert werden oder via obigen AT Befehlen aus dem Modem ausgelegen werden.
* **AppEUI** ist immer `0000000000000001`
* **AppKey** kann generiert werden oder via obigen AT Befehlen aus dem Modem ausgelegen werden.

Die restlichen Felder müssen nicht gesetzt werden, bzw. können auf den Standardwerten verbleiben.

**Programm**

Die Kommunikation klappte nur mit dem [Arduino Beispiel](LoRaWAN868/LoRaWAN868.ino). Dazu ist zuerst die [Arduino IDE](https://docs.m5stack.com/en/arduino/arduino_core2_development) für M5Stack einzurichten.

Nach erfolgter Einrichtung kann der entsprechende Arduino Sketch importiert werden.

In diesem sind die obigen Informationen vom The Things Network zu übertragen:

        sendATCMDAndRevice("AT+CDEVEUI=00BB9DA5B97XXXX\r");
        sendATCMDAndRevice("AT+CAPPEUI=0000000000000001\r");
        sendATCMDAndRevice("AT+CAPPKEY=27DFE264CA33AC1957C005EB48BXXXX\r");

Programm compilieren und der M5Stack sendet Daten via Base Station an The Things Network.
