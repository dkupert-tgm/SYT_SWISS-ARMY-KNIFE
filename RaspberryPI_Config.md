### Raspberry PI Konfigurieren

#### Raspberry PI OS

Ein Raspberry Pi an sich ist zwar schön und gut aber ohne Betriebssystem können wir auf dessen Funktionalität nicht zugreifen, deshalb muss man ein Betriebssystem aufspielen.

Es gibt viele verschiedene Betriebssysteme, welche für den Raspberry Pi geeignet sind. Ich habe mich für unsere Zwecke für "Rasbian Buster Lite" (basiert auf Debian Buster Lite 10) entschieden. Rasbian Buster Lite ist deshalb so gut geeignet, da die ISO Datei sehr klein ist und wir keine grafische Oberfläche brauchen. [1]

Nachdem wir die ISO auf der offiziellen Webseite gedownloadet haben müssen wir die ISO-Datei nur noch auf eine MicroSD-Karte flashen und dazu benutzen wir ein Programm namens "Etcher", welches von der offiziellen Raspberry PI Webseite empfohlen wird. [2]

Die Installation ist relativ simpel, falls man trotzdem Schwierigkeiten hat bietet Raspberry einen Installation-Guide an. [3]

#### Raspberry PI SSH-Verbindung

Da wir nur über eine Internetverbindung mit dem Raspberry Pi kommunizieren wollen brauchen wir eine SSH Verbindung, diese ist Standardmäßig deaktiviert. Um diese zu aktivieren muss man auf der Boot Partition eine Datei mit den Namen "ssh" (ohne Extension) erstellen. Dies sollte die SSH Verbindung beim einschalten des Gerätes aktivieren. [4]

|              | Default-Wert |
| ------------ | ------------ |
| Benutzername | pi           |
| Passwort     | raspberry    |

## Quellen

[1] : "Raspbian Buster Lite" Download [online](https://www.raspberrypi.org/downloads/raspbian/) | zuletzt besucht 19.12.2019

[2] : "Etcher" Download [online](https://www.balena.io/etcher/) | zuletzt besucht 19.12.2019

[3] : "Installing Images Raspberry Pi" [online](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) | zuletzt besucht 31.12.2019

[4] : "Enabel SSH on your Raspberry Pi" [online](https://peppe8o.com/2019/07/install-raspbian-buster-lite-in-your-raspberry-pi/) | zuletzt besucht 11.01.2019