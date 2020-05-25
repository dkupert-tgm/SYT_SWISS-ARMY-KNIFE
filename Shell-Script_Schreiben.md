# Shell Script selber schreiben

## Allgemein

Um Prozesse zu automatisieren ist es praktische, wenn man ein eigenes Shell-Script schreibt. Erstellen wir zu erst eine Datei `test.sh`.  Im Script kann man alle Befehle, welche in der normalen Linux-Konsole benutzt auch ausführen. Des Weiteren kann man auch IF-Unterscheidungen und Schleifen mit einbinden. [1] 

## Ausgabe

Um Ausgaben im Script zu bekommen kann man den Befehl `echo` benutzen. [1]

## Pakete überprüfen

Um zu überprüfen, ob ein Paket bereits vorhanden ist benötigt man folgendes Code-Snippet.[2]

```bash
if ! [ -x "$(command -v git)" ]; then
  echo 'Error: git is not installed.' >&2
  exit 1
fi
```

## Ordner überprüfen

Um zu überprüfen, ob ein Verzeichnis bereits vorhanden ist benötigt man folgendes Code-Snippet. [3]

```bash
if [ -d "/path/to/dir" ] 
then
    echo "Directory /path/to/dir exists." 
else
    echo "Error: Directory /path/to/dir does not exists."
fi
```

## Ausführen

Um das Script auszuführen muss man die Datei ausführbar machen. [1]

```bash
chmod a+rx test.sh
# Ausfürhen
./test.sh
```

## Quellen

[1] "Shell Scripting Tutorial"  [online](https://www.shellscript.sh/) | zuletzt besucht 25.05.2020

[2] "How can I check if a program exists from a Bash script?" [online](https://stackoverflow.com/questions/592620/how-can-i-check-if-a-program-exists-from-a-bash-script) | zuletzt besucht 25.05.2020

[3] "HowTo: Check If a Directory Exists In a Shell Script" [online](https://www.cyberciti.biz/faq/howto-check-if-a-directory-exists-in-a-bash-shellscript/) | zuletzt besucht 25.05.2020