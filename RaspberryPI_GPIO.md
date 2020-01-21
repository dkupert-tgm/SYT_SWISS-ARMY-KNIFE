### Raspberry Pi (Python)

#### GPIO-Pins

Fangen wir erstmal mit den Code-Snippets an, welche für die GPIO-Pins zuständig sind an. Erstmal müssen wir die RPi.GPIO library importieren. (weiteres dazu im Kapitel Requirments.txt) um den Code lesbarer zu gestalten habe ich das Modul zu GPIO umbenannt mit dem Befehl `as`.

```python
import RPi.GPIO as GPIO
```

Bevor wir zur Konfiguration der einzelnen Pins kommen sollten wir einige Vorkehrungen treffen. Zuerst sollten wir alle Warnungen Ignorieren und den Modus der Pin Nummerierung festlegen. Hierfür gibt es zwei Optionen `GPIO.BOARD` und `GPIO.BCM`.[1]

| BOARD                                                    | BCM                                                          |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| Referenziert sich auf die Nummerierung der Pins am Board | Referenziert die Bezeichnung, welche von der "Broadcom SOC channel" festgelegt wurde. |

##### BCM[3]

![GPIO-Pinout-Diagram-2](RaspberryPI_GPIO/GPIO-Pinout-Diagram-2.png)

##### BOARD

![a-and-b-physical-pin-numbers](img/a-and-b-physical-pin-numbers.png)

```python
GPIO.setwarnings(False) # Ignore warnings
GPIO.setmode(GPIO.BOARD) # Use physical pin numbering
```

Zu guter Letzt kommt, dass Konfigurieren der einzelnen Pins. Es gibt generell 2 unterschiedliche Modi output und input. Des Weiteren gibt es beim Input die Möglichkeit einen Pullup oder Pulldown Widerstand zu setzen. [3,4,5]

```python
# Pin auf Input setzen (Pulldown)
GPIO.setup(Pin_Nummer, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)
# Pin auf Input setzen (Pullup)
GPIO.setup(Pin_Nummer, GPIO.IN, pull_up_down=GPIO.PUD_UP)
#Pin auf Output setzen
GPIO.setup(Pin_Nummer, GPIO.OUT)
```

Da wir jetzt die Pins Konfiguriert haben können die jetzt Entscheiden ob der Pin Strom oder keinen Strom hat (High oder Low). Mit der Methode .output kann man den Modus des Pins ändern

```python
# Strom / High für den GPIO 3
GPIO.output(3, GPIO.HIGH)
# kein Strom / Low für den GPIO 3
GPIO.output(3, GPIO.LOW)

```

#### Interrupts

Da wir einen Button benutzen, brauchen wir Interrupts aber bevor wir zu den Interrupts kommen sollte man das Prinzip von Rissing und Falling verstehen. [Falling und Rising](SYT_Falling_Rising.md)

Nachdem man einen Pin auf Input gesetzt hat kann man weitere Events hinzufügen die Getriggert werden wenn ein `GPIO.RISING`oder `GPIO.FALLING` erkannt wird.

```python
# Config
GPIO.add_event_detect(Pin_Numer, GPIO.RISING / GPIO.FALLING, callback=methoden_name)
```

## Quellen

[1] : "What is the difference between BOARD and BCM for GPIO pin numbering?" [online](https://raspberrypi.stackexchange.com/questions/12966/what-is-the-difference-between-board-and-bcm-for-gpio-pin-numbering) | zuletzt besucht 18.01.2020

[2] : "GPIO-Pins Raspberry PI" [online](https://www.ics.com/blog/control-raspberry-pi-gpio-pins-python) | zuletzt besucht 19.01.2020

[3] : "Image RaspberryPi BCM" [onlien](![Image result for raspberry pi 3b+ pin board](https://www.raspberrypi.org/documentation/usage/gpio/images/GPIO-Pinout-Diagram-2.png))  | zuletzt besucht 19.01.2020

[4] : "Offizielle GPIO Raspberry Dokumentation" [online](https://www.raspberrypi.org/documentation/usage/gpio/)  | zuletzt besucht 19.01.2020

[5] : "Push Button with Raspberry PI GPIO" [online](https://raspberrypihq.com/use-a-push-button-with-raspberry-pi-gpio/) | zuletzt besucht 16.01.2020

