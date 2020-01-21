### Raspberry PI Konfigurieren

#### Raspberry PI OS

Ein Raspberry Pi an sich ist zwar schön und gut aber ohne Betriebssystem können wir auf dessen Funktionalität nicht zugreifen, deshalb muss man ein Betriebssystem aufspielen.

Es gibt viele verschiedene Betriebssysteme, welche für den Raspberry Pi geeignet sind. Ich habe mich für unsere Zwecke für "Rasbian Buster Lite" (basiert auf Debian Buster Lite 10) entschieden. Rasbian Buster Lite ist deshalb so gut geeignet, da die ISO Datei sehr klein ist und wir keine grafische Oberfläche brauchen. [3]

Nachdem wir die ISO auf der offiziellen Webseite gedownloadet haben müssen wir die ISO-Datei nur noch auf eine MicroSD-Karte flashen und dazu benutzen wir ein Programm namens "Etcher", welches von der offiziellen Raspberry PI Webseite empfohlen wird. [4]

Die Installation ist relativ simpel, falls man trotzdem Schwierigkeiten hat bietet Raspberry einen Installation-Guide an. [5]

#### Raspberry PI SSH-Verbindung

Da wir nur über eine Internetverbindung mit dem Raspberry Pi kommunizieren wollen brauchen wir eine SSH Verbindung, diese ist Standardmäßig deaktiviert. Um diese zu aktivieren muss man auf der Boot Partition eine Datei mit den Namen "ssh" (ohne Extension) erstellen. Dies sollte die SSH Verbindung beim einschalten des Gerätes aktivieren. [6]

|              | Default-Wert |
| ------------ | ------------ |
| Benutzername | pi           |
| Passwort     | raspberry    |

## Quellen

