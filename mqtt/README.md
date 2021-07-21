## MQTT (Message Queue Telemetry Transport)
***

> [⇧ **Home**](../README.md)

![](images/mqtt.png)

Quelle: Publish/Subscribe-Architektur von MQTT. © HiveMQ.com
- - -

[Message Queue Telemetry Transport (MQTT)](http://de.wikipedia.org/wiki/MQ_Telemetry_Transport) ist ein offenes Nachrichten-Protokoll für Machine-to-Machine-Kommunikation (M2M), das die Übertragung von Messdaten-Daten in Form von Nachrichten zwischen Geräten ermöglicht, trotz hoher Verzögerungen oder beschränkten Netzwerken. Entsprechende Geräte reichen von Sensoren und Aktoren, Mobiltelefonen, Eingebetteten Systemen in Fahrzeugen oder Laptops bis zu voll entwickelten Rechnern. **MQTT basiert auf TCP-Sockets.**

MQTT implementiert das [**Publish/Subscribe-Pattern**](http://de.wikipedia.org/wiki/Beobachter_(Entwurfsmuster)). Es ersetzt die Punkt-zu-Punkt-Verbindungen durch einen zentralen Server (Broker), zu dem sich Datenproduzenten und -nutzer gleichermaßen verbinden können. Das Senden (publish) und Empfangen (subscribe) von Nachrichten funktioniert über sogenannte Topics. Ein **Topic** ist ein String, der eine Art Betreff der Nachricht darstellt, aber ähnlich einer Web Adresse aufgebaut ist.

Im obigen Beispiel funktioniert die komplette Kommunikation rein über Topics, und der Sensor (links) und die Endgeräte (rechts) wissen nichts über die Existenz des jeweils anderen.

### Beispiel Topics

	Zuhause/Wohnzimmer/Temperatur
	Zuhause/Wohnzimmer/Luftfeuchtigkeit
	Zuhause/Schlafzimmer/Temperatur
	Zuhause/Schlafzimmer/Luftfeuchtigkeit						

Topics haben noch ein weiteres wichtiges Konzept - Wildcards. In oben stehenden Codebeispiel sind vier Topics aufgelistet, und je ein Sensor sendet eine neue Nachricht auf den jeweiligen Topic, sobald sich ein Wert geändert hat. Man kann nun je nach Anwendungsfall Wildcards benutzen, um mehrere Topics zu abonnieren.

### Beispiel Wildcards 

	Zuhause/+/Temperatur
	Zuhause/Wohnzimmer/#
	#

Oben sind alle möglichen Wildcard-Operatoren aufgelistet. Im ersten Fall bekommt die mobile Anwendung nur alle Nachrichten über neue Temperaturwerte, im zweiten Fall nur alle Werte aus dem Wohnzimmer und im dritten Fall alle Werte. Dabei lässt sich der +-Operator immer nur für eine Hierarchiestufe einsetzen und der #-Operator für beliebig viele Hierarchiestufen mit der Bedingung, dass dieser am Ende stehen muss.

### Mechanismen zur Qualitätskontrolle 

Ein weiteres wichtiges Konzept sind die drei Servicequalitäten bei der Datenübertragung 0, 1 und 2. Die Zusicherung variiert von keiner Garantie (Level 0) über die, dass die Nachricht mindestens einmal ankommt (Level 1), bis hin zur Garantie, dass die Nachricht genau einmal ankommt (Level 2).

## MQTT Publish Beispiel
***

Mittels Publish (unten) kann eine Meldung zum MQTT Broker bzw. Topic gesendet werden.

Ein anderes Board oder der Mosquitto Client mosquitto_sub kann dieses Topic Abonnieren (subscribe).

### Client

Mittels der Client Utilities von [Mosquitto](https://projects.eclipse.org/projects/technology.mosquitto) können Werte abgefragt oder gesendet werden.

Beispiel: Abfragen ob der Button A gedrückt wurde.

    mosquitto_sub -h cloud.tbz.ch -t 'm5stack/#'
    Button A was pressed
    Button A was pressed
    Button A was pressed

Beispiel: RGB Led 

    mosquitto_pub -h cloud.tbz.ch -t "m5stack/rgb" -m "12"
    mosquitto_pub -h cloud.tbz.ch -t "m5stack/rgb" -m "255"

Eine Liste von Öffentlichen MQTT gibt es [hier](https://github.com/mqtt/mqtt.github.io/wiki/public_brokers).

### Beispiel

![](images/pub-sub.png)

- - -

Sendet eine Meldung an den MQTT Broker wenn der Button A gedrückt wird.

Abonniert das Topic `m5stack/rgb` und setzt die Farbe des mittleren Leds.

    from m5stack import *
    from m5ui import *
    from uiflow import *
    from m5mqtt import M5mqtt
    
    def fun_m5stack_rgb_(topic_data):
      # global params
      rgb.setColor(1,(0 << 16) | (int(topic_data) << 8) | 0)
      pass
    
    def buttonA_wasPressed():
      # global params
      m5mqtt.publish(str('m5stack/button'),str('Button A was Pressed'))
      pass
    btnA.wasPressed(buttonA_wasPressed)
    
    m5mqtt = M5mqtt('ich', 'cloud.tbz.ch', 1883, 'test', 'test', 300)
    m5mqtt.subscribe(str('m5stack/rgb'), fun_m5stack_rgb_)
    m5mqtt.start() 

### Links 

*   [Ausführlicher Artikel auf heise.de](http://www.heise.de/developer/artikel/MQTT-Protokoll-fuer-das-Internet-der-Dinge-2168152.html)
*   [MQTT Client Library Encyclopedia - Paho Embedded](https://www.hivemq.com/blog/mqtt-client-library-encyclopedia-paho-embedded/) - gute Einführung in mbed Library
*   [MQTT Team auf mbed.org](https://os.mbed.com/teams/mqtt/)
*   [MQTT JavaScript Client Library für node.js und Browser](https://github.com/mqttjs/MQTT.js)
*   [Eclipse Paho, Client Libraries für Verschiedene Sprachen](http://www.eclipse.org/paho/)
*   [Practical MQTT with Paho](http://www.infoq.com/articles/practical-mqtt-with-paho)
*   [Paho UI Utilities für MQTT](https://wiki.eclipse.org/Paho/GUI_Utility)
*   [MQTT Toolbox - MQTT Client Chrome App](https://www.hivemq.com/blog/mqtt-toolbox-mqtt-client-chrome-app/) - einfacher MQTT Client um Meldungen zu abonnieren (subsribe).

