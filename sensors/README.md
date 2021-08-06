Sensoren
--------
***

> [⇧ **Home**](../README.md)

![](https://raw.githubusercontent.com/iotkitv3/intro/main/images/Messysteme.png)

Quelle: Prof. Dr.-Ing. Michael Weyrich, http://wiki.zimt.uni-siegen.de/fertigungsautomatisierung

- - -

Sensoren sind technische Bauteile, die Eigenschaften der Umgebung (z. B.: Wärmestrahlung, Temperatur, Feuchtigkeit, Druck, Schall, Helligkeit oder Beschleunigung) erfassen und in ein weiter verarbeitbares elektrisches Signal umformen.

### Hall Sensor 
***

![](https://static-cdn.m5stack.com/resource/docs/static/assets/img/product_pics/unit/hall/hall_unit.webp) 

Hall Sensor Unit

- - - 

Ein [Hall Sensor](http://de.wikipedia.org/wiki/Hall-Sensor) (auch Hall-Sonde oder Hall-Geber, nach Edwin Hall) nutzt den Hall-Effekt zur Messung von Magnetfeldern.

[Hall-Effekt-Unit](https://docs.m5stack.com/en/unit/hall) integriert mit drei A3144E Hall-Sensor-Schaltern, die von integrierten Gate-Schaltungen der Serie 74HC verarbeitet werden.

Ein Signal mit niedrigem Pegel kann erzeugt werden, wenn sich der S-Pol des Magneten nahe der Oberseite des Sensors oder der N-Pol nahe der Rückseite befindet und die interne LED-Anzeige aufleuchtet.

**Anwendungen**

*   Alarmanlagen, z.B. zum Sichern von Fenstern.
*   Im Auto zur Kontrolle ob der Sicherheitsgurt geschlossen ist, als Raddrehzahlsensoren, zur Erkennung des Zündzeitpunkts.
*   Zur Geschwindigkeitsmessung, z.B. für E-Bikes.
*   In der Kraftwerkstechnik zur Erfassung der Turbinendrehzahl.

**Beispiel mit Core2 und Hall Sensor an Port A**

![](images/hall-sensor.png)

- - -

    from m5stack import *
    from m5stack_ui import *
    from uiflow import *
    import unit
    
    screen = M5Screen()
    screen.clean_screen()
    screen.set_screen_bg_color(0xFFFFFF)
    hall_0 = unit.get(unit.HALL, unit.PORTA)
    
    label0 = M5Label('Text', x=129, y=48, color=0x000, font=FONT_MONT_14, parent=None)
    
    while True:
      label0.set_text(str(hall_0.value()))
      wait_ms(2)

### PIR Sensor 
***

![](https://static-cdn.m5stack.com/resource/docs/static/assets/img/product_pics/unit/pir/unit_pir_01.webp)

- - -

Ein Bewegungsmelder ist ein elektronischer Sensor, der Bewegungen in seiner näheren Umgebung erkennt und dadurch als elektrischer Schalter arbeiten kann. Ein Bewegungsmelder kann aktiv mit elektromagnetischen Wellen (HF oder Doppelradar), mit Ultraschall (Ultraschall-Bewegungsmelder) oder passiv anhand der Infrarotstrahlung der Umgebung arbeiten; es gibt auch Kombinationen davon.

Der [PIR Sensor (Bewegungsmelder)](http://de.wikipedia.org/wiki/Bewegungsmelder) (englisch passive infrared) ist der am häufigsten eingesetzte Typ von Bewegungsmeldern. Er reagiert optimal auf Winkeländerungen, wenn eine Person am Sensor vorbeigeht. 

Die [PIR Sensor Unit](https://docs.m5stack.com/en/unit/pir) liefert 1 wenn eine Person erkannt wurde und geht dann wieder auf 0.

**Anwendungen**

*   Einschalten einer Beleuchtung
*   Auslösen eines Alarms

**Beispiel mit Core2 und PIR Sensor an Port A**

![](images/pir-sensor.png)

- - -

    from m5stack import *
    from m5stack_ui import *
    from uiflow import *
    import unit
    
    screen = M5Screen()
    screen.clean_screen()
    screen.set_screen_bg_color(0xFFFFFF)
    pir_2 = unit.get(unit.PIR, unit.PORTA)
    
    label0 = M5Label('Text', x=120, y=44, color=0x000, font=FONT_MONT_14, parent=None)
    
    while True:
      if pir_2.state:
        label0.set_text('Person erkannt')
      else:
        label0.set_text('Keine Person erkannt')
      wait_ms(2)

