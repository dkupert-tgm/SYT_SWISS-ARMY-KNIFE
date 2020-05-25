# InfluxDB Konfigurieren (Python)

## Allgemein

Damit wir die InfluxDB auch in unserem Beispiel benutzen können müssen wir Sie dementsprechend Konfigurieren. User hinzufügen, Rechte verteilen, usw.

## Konfiguration

Alle notwendigen Konfigurationsschritte [1]

```sql
-- DB erstellen, welche dann vom Python Programm benutzt wird
create database "sensor_data"
-- Der Admin mit seinen Rechten
create user admin with password 'influxadmin'
grant all privileges to admin

-- Der PI User
create user rpi3 with password 'rpi3'
grant all on "sensor_data" to 'rpi3'

-- Grafana User
create user "grafana" with password "grafana"
grant read on "sensor_data" to "grafana"
```

### Achtung

Bei dem Namen des User dürfen keine Sonderzeichen verwendet werden. [2]

## Quellen

[1] "MONITORING TEMPERATURE AND HUMIDITY WITH A RASPBERRY PI 3, DHT22 SENSOR, INFLUXDB AND GRAFANA "[online](https://www.definit.co.uk/2018/07/monitoring-temperature-and-humidity-with-a-raspberry-pi-3-dht22-sensr-influxdb-and-grafana/) |zuletzt besucht 26.05.2020

[2] "Name series with dash" [online](https://stackoverflow.com/questions/31286130/name-series-with-dash) |zuletzt besucht 26.05.2020

 