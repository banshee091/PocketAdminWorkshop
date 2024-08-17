# PocketAdmin Workshop


## Einleitung

Dieses Repo enthält die Bauanleitung für das [PocketAdmin](https://github.com/krakrukra/PocketAdmin) Projekt von Karakura. **Ich habe weder die Hardware, noch die Software hergestellt, Credits gehen vollständig an die Entwickler*Innen des Originalprojekts!**  
Ziel dieser Anleitung ist, als Anleitung für einen Workshop auf dem WAMP24, oder als Hilfestellung für Hacker*Innen zu dienen die das Projekt selbst nachbauen wollen und die Teile selbst gesourced haben.
Wenn du bereits Erfahrungen mit dem bauen von Hardware hast, benötigst du diese Anleitung vermutlich nicht.

**Der Workshop ist als Fortbildung geplant. Bitte sei vorsichtig mit dem Umgang des gebauten Gerätes und verwende es ausschließlich als Awareness- oder Administrationsgerät**

## Hardware

### Vorbereitung

Platziere als erstes alle Teile vor dir um sicherzustellen, dass alles vorhanden ist. Du solltest folgende Teile haben:

1x STM32F072C8T6 
![](/doc/Images/Picture_STM.png)

1x W25N01GVZEIG flash Speicher
![](/doc/Images/Picture_Flash.png)

1x IP4220CZ6 Spannungsschutzdiode
![](/doc/Images/Picture_Diode.png)

1x MCP1700-3302E/TT Linearregler
![](/doc/Images/Picture_linear_regulator.png)

3x 10µF Kondensatoren
![](/doc/Images/Picture_capacitors_10uF.png)

2x 18pF Kondensatoren
![](/doc/Images/Picture_capacitors_18pF.png)

7x 100nF Kondensatoren
![](/doc/Images/Pciture_capacitors_100nF.png)

2x 33 Ohm Widerstände 
![](/doc/Images/Picture_resistor_33.png)

2x 4.7k Ohm Widerstände 
![](/doc/Images/Picture_resistor_4k7.png)

1x Grüne LED 
![](/doc/Images/Picture_led.png)

1x NX5032GA 8MHz quartz crystal
![](/doc/Images/Picture_quartz.png) 

1x TL3342 Taster 
![](/doc/Images/Picture_switch.png)

1x USB Typ A Stecker
![](/doc/Images/Picture_usb.png)

Insgesammt solltest du 12 Packages mit Bauteilen, eine PCB und ein USB-Stick Case haben.


### Zusammenbau

Lade zuerst die [IBOM HTML Datei](/doc/BOM/ibom.html) herunter und öffne sie in einem Browser. Wähle nun die Rückseite der PCB (rechte obere Ecke, das große B).
Platziere die Platine im Rakel-Halter, platziere den Stencil und trage mit dem Rakel Lötpaste auf.
Wenn du das noch nie gemacht hast, frage bitte eine\*n Trainer\*in nach Hilfe.

Nimm nun eine Pinzette und platziere die einzelnen Teile. Achte darauf, dass die Teile korrekt orientiert (STM, IP4220CZ6) und gerade platziert sind.
![](/doc/Images/Picture_back.png)

Wenn du mit der ersten seite fertig bist, nimm die PCB und platziere sie im Reflow-Ofen.  
Warte bis die Platine fertig gebacken ist, nimm sie heraus und  warte noch etwas mehr bis sie abgekühlt ist.  

Trage dann das Lötzinn auf die Vorderseite auf und platziere auch hier die Teile mit einer Pinzette. 

**ACHTUNG: Lasse den USB Stecker vorerst weg! Der wird im Anschluss von Hand gelötet. Die Stecker halten die Hitz im reflow Ofen nicht aus und schmelzen!**

![](/doc/Images/Picture_front-png)

Wenn die Vorderseite fertig gebacken ist, stecke den USB Stecker auf und verlöte ihn von Hand.
![](/doc/Images/Picture_done.png)

Mache eine Sichtprüfung auf Kurzschlüsse oder Lötbrücken. Wenn du Hilfe beim reparieren brauchst, sag bescheid.

Du bist nun fertig mit dem Zusammenbau. Weiter gehts mit der Programmierung

## Programmierung

Klone als erstes das PocketAdmin Repository:
https://github.com/krakrukra/PocketAdmin

Installiere das **dfu-utils** Paket für dein Betriebssystem.

Nimm nun eine Pinzette und überbrücke den boot0 und den 3.3V Pin. Du findest sie am unteren Ende der Platine, es sind die beiden Löcher auf der gegenüberliegenden Seite des viereckigen Lochs:
(x) (x) () () []

![](/doc/Images/Picture_dfu.png)

Mit der Pinzette in den Löchern, stecke den PocketAdmin in deine USB-Buchse. Danach kannst du die Pinzette herausnehmen. Öffne ein Terminal und vergeissere dich, dass alles funktioniert mit  
**dfu-util -l**

Wenn du den Controller in der terminalsausgabe findest, navigiere in das /firmware Verzeichnis des PocketAdmin Repos.
Flashe nun die .dfu Datei mit   
**dfu-util -a 0 -D firmware_13006.dfu**  
(Der Dateiname kann abweichen, je nach Version.)

Im Terminal sollte ein Fortschrittsbalken zu sehen sein. Wenn der Upload abgeschlossen, entferne den PocketAdmin und stecke ihn wieder ein.
Dein Betriebssystem sollte nun ein unformatiertes Speichergerät erkennen. Erstelle eine Partitionstabelle und formatiere den USB Stick im FAT32 Format. Ich empfehle hierfür GParted.

## Und Jetzt?

Nachdem der PocketAdmin geflasht ist und du eine Partition erstellt hast solltest du in der Lage sein deinen PocketAdmin zu benutzen.
Für eine ausführliche Liste was das Gerät alles kann, schau ins [Wiki](https://github.com/krakrukra/PocketAdmin/wiki) des Projekts. 

Als kleiner test kannst du erstmal folgendes testen:
- Entferne den PocketAdmin
- Halte den knopf des PocketAdmin gedrückt und stecke ihn wieder ein. Warte ca. 1-2 Sekunden und lasse den Knopf los. 
- Dein Betriebssystem sollten den PocketAdmin als USB-Speicher erkennen.
- Kopiere die Datei "payload.txt" aus dem Repo auf den PocketAdmin.
- Öffne einen beliebigen Texteditor. Stecke den PocketAdmin jetzt einmal ab und wieder an. in dem Texteditor sollte jetzt "ABCDEFGH.." usw. erscheinen.

Glückwunsch, du solltest jetzt dein eigens PocketAdmin Tool haben. Bitte verwende das Gerät verantwortungsvoll!