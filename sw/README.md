Software
--------

Die M5Stack Main Controller können mittels:

* [UIFlow](https://docs.m5stack.com/en/quick_start/core2/m5stack_core2_get_started_MicroPython) - empfohlen
* [Visual Studio Code mit Micropython](https://marketplace.visualstudio.com/items?itemName=curdeveryday.vscode-m5stack-mpy)
* [Arduino IDE](https://docs.m5stack.com/en/arduino/arduino_core2_development)

programmiert werden.

Dazu ist, zuerst der richtige Hardware Driver zu installieren und anschliessend ein Firmware Update durchzuführen. 

Die nötigen Schritte sind im **Quick Start** jedes Controllers beschrieben.

* [M5Stack BASIC](https://docs.m5stack.com/en/quick_start/m5core/m5stack_core_get_started_MicroPython)
* [M5Stack Core2](https://docs.m5stack.com/en/quick_start/core2/m5stack_core2_get_started_MicroPython) - empfohlen.
* [M5StickC Plus](https://docs.m5stack.com/en/quick_start/m5stickc_plus/m5stickc_plus_quick_start_with_uiflow)
* [Atom Lite und Matrix](https://docs.m5stack.com/en/quick_start/atom/atom_quick_start_uiflow)

Die nachfolgenden Anleitungen gehen auf Besonderheiten ein, welche in den **Quick Start** Tutorials fehlen.

### Hardware Driver

Der Hardware Driver stellt einen USB Seriellen Port (Windows COMx, Linux/Mac /dev/ttyUSB) zur Verfügung.

Über diesen wird der Controller programmiert, Firmwware Updates durchgeführt, die Konfigurations (z.B. WLAN) geändert.

* **M5Stack Controller** brauchen den [cp210x driver](https://docs.m5stack.com/en/quick_start/core2/m5stack_core2_get_started_MicroPython).
* **M5Stick** und **Atom** brauchen den [FTDI USB Driver](https://docs.m5stack.com/en/quick_start/atom/atom_quick_start_uiflow). Der von Windows installierte Driver funktioniert nicht sauber.

### Burning tool

![](images/burningtool.png)

- - -

Dient zum Updaten der Firmware und Einstellen von Konfigurationen wie z.B. WLAN SSID und Password.

* **Configuration** - setzt WLAN SSID, Start Mode etc.
* **Download** oder **Burn** - Downladen und Firmware auf Controller updaten.

**Tip**: beim Updaten der Firmware, WLAN SSID und Password frei lassen. Tests haben ergeben, dass diese Werte mittels **Configuration** sauberer gesetzt werden.

**Dieses Tools sollte immer Installiert werden, um die Controller in den Urzustand zurück setzen zu können.**

### Configuration / Start Mode

![](images/configuration.png)

- - -

Den API Keys braucht es für die Programmierung des Controllers via Web.

Die verschiedenen Start Mode haben folgende Bedeutung:
* **Internet Mode** - Programmierung erfolgt mittels Web IDE - [https://flow.m5stack.com](https://flow.m5stack.com)
* **USB Mode** - Programmierung erfolgt via Offline UIFlow IDE
* **APP Mode** - das letzte Programm wird ausgeführt. I.d.R. gespeichert als `main.py`. Eine Programmierung ist diesem Mode ist nicht möglich.

Die Modi können via Burning Tool oder nach einem `Reset/Power` umgestellt werden. 

![](images/startmode.png)

Eine Anleitung findet sich am Ende jeden **Quick Start** Tutorials.

Ansonsten sind nur WLAN SSID und Password zu setzen. Die anderen Werte sollten auf den Standardeinstellungen belassen werden.




