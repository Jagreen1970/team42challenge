# Ein Tic-Tac-Toe Spiel

## Das Projekt
Am Ende des Tages sollen zwei Spieler über eine Weboberfläche Tic-Tac-Toe spielen können. 
Das Projekt kann in zwei Teile geschnitten werden: Den Client- und den Serveranteil. Dabei soll ein Team ganz im Sinne der 
Agilen Methoden natürlich alle benötigten Skills abdecken, d.h. *beide Teile implementieren*. 
Die Ergebnisse werden am Abend bei einem Bierchen vorgestellt und mit angemessenem Applaus gefeiert!

### Der Server
* Der Tic-Tac-Toe Server besteht aus einem Executable.
* Als Protokoll ist REST/json über HTTP zu implementieren
* Der HTTP-Port, auf dem der Server horcht, soll konfigurierbar sein.
* Der Server soll folgende REST-Api bereitstellen:
  * `POST /ttt/`:Erzeugt ein neues Spiel und gibt dessen eindeutige ID zurück
  * `GET /ttt/`: Gibt eine Liste der aktiven Spiele zurück
  * `GET /ttt/:id`: Gibt den aktuellen Zustand des Spieles zurück
    * Spielbrett als String mit einer Länge von 9 Zeichen.
      * Erlaubte Zeichen: "X"(Spielstein X), "O"(Spielstein O) und "-"(leeres Feld)
      * Die Felder des Spielbrettes sind von links nach rechts in den bekannten 3 Zeilen numeriert:
      ```
         0 | 1 | 2
        ---|---|---
         3 | 4 | 5
        ---|---|---
         6 | 7 | 8
      ```
      * **Beispiel**: **`"-O--XOX--"`**
    * Spieler, der an der Reihe ist als String: ("X" oder "O")
    * Aktueller Zustand: "X/-"(Spieler X hat gewonnen) oder "-/O"(Spieler O hat gewonnen) oder "-/-"(Unentschieden)
* *Optional* kann das Executable den Kommandozeilenparameter `--cli` bereitstellen, um interaktiv auf der Shell testen zu können. 
  In diesem Fall muss natürlich ein zusätzliches ASCII-Interface via stdin/stdout implementiert werden. 

### Der Client
