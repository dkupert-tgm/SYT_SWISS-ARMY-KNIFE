## Pullup / Pulldown[1]

* Pullup

  * > Um dies zu vermeiden wird, während nichts am Eingang passiert, dieser auf High gezogen (pullup). Will man also einen Taster haben, der Low schaltet, so will man für den Rest der Zeit High am Eingang liegen haben. Dies kann man erreichen, indem man den Eingang fest mit VCC verbindet. Vom Eingang geht nun eine Leitung nach VCC und eine über den Taster nach GND. Leider würde dies zu einem Kurzschluss führen sobald man den Taster drückt und die Schaltung könnte (und würde höchstwahrscheinlich) Schaden nehmen. Deshalb wird nun zwischen VCC und dem Eingang ein hochohmiger Widerstand eingesetzt, der Pullup-Widerstand. Bei geschlossenem Taster wird nun der Strom über den Pullup-Widerstand nach GND fließen und der Input liegt auf GND (0V).

* Pulldown

  * > Der Pulldown-Widerstand funktioniert analog zum Pullup-Widerstand, nur dass nun VCC  geschaltet werden soll und somit der Eingang auf GND gezogen werden muss. Dies geschieht in gleicher Weise wie beim Pullup, nur dass der Pulldown-Widerstand nun zwischen GND und dem Eingang platziert wird. Schließt man nun wieder den Taster, liegt am Eingang VCC an --> High.

## Quellen

[1] : "Pullup / Pulldown" Dokumentation [online](https://rn-wissen.de/wiki/index.php/Pullup_Pulldown_Widerstand) | zuletzt besucht 19.01.2020