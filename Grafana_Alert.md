# Alerts in Grafana

Grafana bietet uns die Möglichkeit bei überschreiten bestimmter Werte in einer Datenbank uns zu "alamieren", diese Funktion wird Alerts genannt man kann auf verschiedene weisen Alerts setzen. Ich habe mich für Discord entschieden, da ich Discord alltäglich benutze.

Aber bevor wir zu Alerts kommen, müssen wir einen Notification Channel hinzufügen. [1,2]

![image-20200525230612538](Grafana_Alert/image-20200525230612538.png)

Es gibt viele verschiedene Möglichkeiten

![image-20200525230720231](Grafana_Alert/image-20200525230720231.png)

Danach müssen wir nur den Content der Message angeben und die Webhook. Zu der Webhook kommen wir später noch.

![image-20200525230823845](Grafana_Alert/image-20200525230823845.png)

## Alert bei einen Graphen hinzufügen

Unter dem Punkt Alert kann man die Threshhold einstellen wann ein Alert getriggert werden soll.

![image-20200525230955940](Grafana_Alert/image-20200525230955940.png)

## Discord Output

![image-20200525231018478](Grafana_Alert/image-20200525231018478.png)

## Quellen:

[1] https://grafana.com/docs/grafana/latest/alerting/notifications/

[2] https://grafana.com/docs/grafana/latest/alerting/rules/