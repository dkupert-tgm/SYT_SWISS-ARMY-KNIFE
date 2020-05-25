# Flask in Python (REST API)

## Allgemein

Man kann sich Flask wie Springboot in Java vorstellen.

Flask ist ein leichtes WSGI-Webanwendungsframework. Es wurde entwickelt, um den Einstieg schnell und einfach zu gestalten und um auf komplexe Anwendungen skaliert zu werden. Es begann als einfacher Wrapper um Werkzeug und Jinja und hat sich zu einem der beliebtesten Python-Webanwendungs-Frameworks entwickelt. 

Flask bietet Vorschläge an, erzwingt jedoch keine Abhängigkeiten oder Projektlayouts. Es ist Sache des Entwicklers, die Tools und Bibliotheken auszuwählen, die er verwenden möchte. Es gibt viele Erweiterungen, die von der Community bereitgestellt werden und das Hinzufügen neuer Funktionen vereinfachen. [1,2]

## Import

```python
from flask import Flask
```

## Generelle Struktur

```python
from flask import Flask, escape, request

app = Flask(__name__)

# Hier wird die URL definiert
@app.route('/')
def hello():
    #Der Inhalt der Webseite wird hier returned
    return 'Hallo Welt'
```

## Flask ausführen

Es gibt Zwei Möglichkeit eine Flask anzuführen.

#### Möglichkeit 1

Damit man Flask ausführen kann muss man zuerst eine Variable mit dem name `FLASK_APP` definieren. [2]

```bash
# Variable definieren
env FLASK_APP=hello.py
# Flask app runnen
flask run
```

#### Möglichkeit 2

Man kann auch mit `if __name__ == '__main__'` arbeiten, und in dieser Unterscheidung definiert man die Attribute, welche man braucht. [3]

```python
if __name__=='__main__':
    app.run(debug=DEBUG, host=HOST, port=PORT)
```

## Quellen

[1] "Flask tutorial" [online](https://flask.palletsprojects.com/en/1.1.x/tutorial/#tutorial) |zuletzt besucht 26.05.2020

[2] "Flask setup" [online](https://palletsprojects.com/p/flask/) |zuletzt besucht 26.05.2020

[3] "Understandig FLask better" [online](https://teamtreehouse.com/community/can-someone-help-me-understand-flaskname-a-little-better) |zuletzt besucht 26.05.2020