## SPI (Serial Peripheral Interface)
***

> [⇧ **Home**](../README.md)

![](images/SPI.png)

SPI Sternverbindung [Quelle Wikipedia](http://de.wikipedia.org/wiki/Serial_Peripheral_Interface)

- - -

![](images/SPI2.png) 

SPI-Verbindung durch Kaskadierung der Slaves [Quelle Wikipedia](http://de.wikipedia.org/wiki/Serial_Peripheral_Interface) 

- - -

Das Serial Peripheral Interface (kurz SPI) ist ein von Motorola entwickeltes Bus-System mit einem **„lockeren“ Standard** für einen synchronen seriellen Datenbus (Synchronous Serial Port), mit dem digitale Schaltungen nach dem Master-Slave-Prinzip miteinander verbunden werden können.

Es gibt drei gemeinsame Leitungen, an denen jeder Teilnehmer angeschlossen ist:

*   **SCLK** (englisch Serial Clock) auch SCK, wird vom Master zur Synchronisation ausgegeben
*   **MOSI** (englisch Master Output, Slave Input) oder SIMO (englisch Slave Input, Master Output)
*   **MISO** (englisch Master Input, Slave Output) oder SOMI (englisch Slave Output, Master Input)

Die Datenleitungen werden manchmal auch SDO (englisch Serial Data Out) und SDI (englisch Serial Data In) genannt. Wobei die Benennung meistens aus der Sicht des jeweiligen Busteilnehmers erfolgt und entsprechend zu verbinden sind, Bsp: Master MOSI (Master Output) mit Slave MOSI (Slave Input).

Je nach Anordnung der Slaves wird eine (bei Kaskadierung) oder mehrere (bei Stern) Chip-Select-Leitungen, welche alle vom Master gesteuert werden, benötigt. Diese Leitungen werden unterschiedlich mit Bezeichnungen wie SS, CS oder STE für Slave Select, Chip Select oder Slave Transmit Enable bezeichnet.

**Anwendungen** 

*   Zugriff auf [SD Karten](http://de.wikipedia.org/wiki/SD-Karte), [RFID Reader](http://de.wikipedia.org/wiki/RFID)
*   Ansteuerung von [LED Strips](https://os.mbed.com/components/Pololu-Addressable-RGB-LED-Strip/), [LCD Displays](http://developer.mbed.org/users/dreschpe/code/SPI_TFT_ILI9341/)

**M5Stack Funktionen**

* M5Stack stellt keine SPI Funktionen in UIFlow zur Verfügung.
* [Micropython](https://docs.micropython.org/en/latest/library/machine.SPI.html) kennt SPI Funktionen.

**M5Stack Produkte**

* Produkte die direkt via SPI angesprochen werden, scheinen keine vorhanden zu sein.
* Ausnahme bildet u.a. LCD und die [SD-Card](https://docs.m5stack.com/en/uiflow/advanced/sdcard), welche in den **Stack** Controllern verbaut ist. Siehe auch [Wikipedia SD-Karte](https://de.wikipedia.org/wiki/SD-Karte). 
* [RGB LED](https://docs.m5stack.com/en/unit/neopixel), sogenannte [Neopixel](https://learn.adafruit.com/adafruit-neopixel-uberguide), wurden früher via SPI (kaskadiert) angesprochen. Bei der neusten Generation kann jedes RGB LED einzeln angesprochen werden. 