# InfluxDB in Python

## Dazu gehörige Dokumente

* [InfluxDB Allgemein](https://github.com/dkupert-tgm/SYT_SWISS-ARMY-KNIFE/blob/master/InfluxDB_Allgemein.md)
* [InfluxDB für Python konfigurieren](https://github.com/dkupert-tgm/SYT_SWISS-ARMY-KNIFE/blob/master/InfluxDB_Konfigurieren_Python.md)

## Imports

```python
from influxdb import InfluxDBClient
```

## Verbindung mit der Datenbank

Um mit der Datenbank zu kommunizieren und somit auch Daten senden zu können müssen wir erst eine Verbind herstellen.

```python
# Configure InfluxDB connection variables
host = "127.0.0.1" # Die IP-Adresse auf der die InfluxDB läuft
port = 8086 # Der 'default' Port von InfluxDB
user = "rpi3" # Der User, welchen wir bereits während der Konfiguration erstellt haben
password = "rpi3" # Das Passwort für den User
dbname = "sensor_data" # Der Name der Datenbank
interval = 1 # Die Zeitliche interval 

#Hier wird ein Client Objekt erzeugt
client = InfluxDBClient(host, port, user, password, dbname)
```

## Daten senden

Die Daten, welche gesendet währenden entsprechen der Form eines JSON Objektes, welches wie folgt aussehen soll.

```python
# Zeitstempel erstellen (-3600, damit UTC in CEST konvertiert wird)
iso = time.ctime(time.time() - 3600)
# JSON Struktur erstellen
data = [
    {
        # Der name der "Tabelle", obwohl es in InfluxDB keine wirklichen Tabellen gibt
        "measurement": measurement,
        # Die Tags können später bei der filterung verwendet werden
        "tags": {
            "location": location[i],
        },
        # Der Zeitstempel
        "time": iso,
        #Die Sensor Werte
        "fields": {
             "CO2ppm" : mq135_List[i].MQPercentage()
        }
    }
]
# JSON Objekt an InfluxDB schicken
client.write_points(data)
```

## Achtung

Ein häufiger Fehler ist es eine andere Zeitzone als UTC zu verwenden. In meinem Fall habe ich die aktuelle Zeit verwendet, wodurch in Grafana nichts angezeigt wurde, weil die Zeit in CEST umgesetzt wurde

## Quellen

[1] https://www.definit.co.uk/2018/07/monitoring-temperature-and-humidity-with-a-raspberry-pi-3-dht22-sensor-influxdb-and-grafana/

[2] https://www.influxdata.com/blog/tldr-influxdb-tech-tips-december-15-2016/