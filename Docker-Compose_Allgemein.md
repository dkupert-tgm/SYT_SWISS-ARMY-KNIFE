# Docker-Compose Allgemein

## Beschreibung

Docker Compose wird verwendet, um mehrere Container als einen einzigen Dienst auszuführen. Angenommen, Sie hätten eine Anwendung, für die NGNIX und MySQL erforderlich sind, und Sie könnten eine Datei erstellen, mit der beide Container als Dienst gestartet werden, ohne dass jeder einzeln gestartet werden muss. [1]

## docker-compose.xml

Definieren Sie die Dienste, aus denen Ihre App besteht, in docker-compose.yml, damit sie zusammen in einer isolierten Umgebung ausgeführt werden können.

Beispiel einer docker-compose.xml Datei: [2]

```xml
version: '2.0'
services:
  web:
    build: .
    ports:
    - "5000:5000"
    volumes:
    - .:/code
    - logvolume01:/var/log
    links:
    - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

## Befehle

Um Docker-Compose zu starten muss man im selben Verzeichnis wie das docker-compose.xml File den Befehl `docker-compose up` schreiben. [2]

## Quellen

[1] "Docker-Compose definition" [online](https://www.tutorialspoint.com/docker/docker_compose.htm) | zuletzt besucht 25.05.2020

[2] "Overview of Docker Compose" [online](https://docs.docker.com/compose/) | zuletzt besucht 25.05.2020 

