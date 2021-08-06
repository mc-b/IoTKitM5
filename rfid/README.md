NFC / RFID
---------- 
***

> [⇧ **Home**](../README.md)

[![](https://www.st.com/content/ccc/fragment/multimedia/video/product_video_thumbnail/group0/e1/e2/a9/18/f0/44/46/f1/What%20is%20NFC%20-%20Thumbnail/files/What%20is%20NFC%20Thumbnail.jpg/_jcr_content/translations/en.What%20is%20NFC%20Thumbnail.jpg)](https://st-videos.s3.amazonaws.com/2017-NFC-forum-what-is-nfc.mp4)

- - -

Die Nahfeld Kommunikation (Near Field Communication, Abkürzung NFC) ist ein internationaler Übertragungsstandard zum kontaktlosen Austausch von Daten per Funktechnik über kurze Strecken von wenigen Zentimetern und einer Datenübertragungsrate von maximal 424 kBit/s. Bisher kommt diese Technik vor allem in Lösungen für Micropayment – bargeldlose Zahlungen kleiner Beträge – zum Einsatz.

Die Übertragung erfolgt entweder verbindungslos (mit passiven HF-RFID-Tags nach ISO 14443 oder ISO 15693) oder Verbindungsbehaftet (zwischen gleichwertigen aktiven Transmittern). Die verbindungslose Nutzung ist nach üblicher Definition (beispielsweise in ISO 15408, den „Common Criteria“) nicht sicher gegen Angriffe von Dritten.

Die Technik hinter NFC basiert auf der englisch [radio-frequency identification (RFID).](http://de.wikipedia.org/wiki/RFID)

M5Stack stellt u.a. eine [RFID Unit](https://docs.m5stack.com/en/unit/rfid) zur Verfügung.

**Anwendungen**

*   Bargeldloser Zahlungsverkehr (girogo, Paypass, Visa payWave, Google Wallet, Apple Pay etc.)
*   papierlose Eintrittskarten
*   Abrechnung von Beförderungsdienstleistungen (zum Beispiel Touch and Travel)
*   Zugangskontrolle
*   Wächterkontrollsysteme zum Nachweis der Anwesenheit eines NFC-Lesegerätes an einem bestimmten Kontrollpunkt mit montierten oder geklebtes NFC-Tag. Steuerung des Smartphones durch im Handel verfügbare NFC-Tags (z. B. SmartTags von Sony, TecTiles von Samsung, oder universell einsetzbare BluewaveTags)

**Beispiel mit Core2 und RFID Unit an Port A** - ([rfid-unit.m5f](rfid-unit.m5f))

![](images/rfid-reader.png)

- - -
    
    from m5stack import *
    from m5stack_ui import *
    from uiflow import *
    import time
    import unit
    
    screen = M5Screen()
    screen.clean_screen()
    screen.set_screen_bg_color(0xFFFFFF)
    rfid_0 = unit.get(unit.RFID, unit.PORTA)
    
    label0 = M5Label('Text', x=100, y=68, color=0x000, font=FONT_MONT_14, parent=None)
    label1 = M5Label('Text', x=100, y=96, color=0x000, font=FONT_MONT_14, parent=None)
    label2 = M5Label('Text', x=100, y=135, color=0x000, font=FONT_MONT_14, parent=None)
    
    label0.set_text('RFID Test')
    while True:
      label1.set_text(str(rfid_0.isCardOn()))
      label2.set_text(str(rfid_0.readUid()))
      wait(0.5)
      wait_ms(2)