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
  * `GET /ttt/:id`: Gibt den aktuellen Zustand des Spieles zurück. Parameter im JSON-Body:
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
    * Aktueller Zustand als String: "X/-"(Spieler X hat gewonnen) oder "-/O"(Spieler O hat gewonnen) oder "-/-"(Unentschieden)
  * `POST /ttt/:id/player`: Ordnet dem Spiel mit der angegebenen ID einen neuen Spieler zu und gibt die ID des Spielers als 
  String, sowie die (zufällig) gewählte Seite zurück. ** X fängt an! **
  Das ist zwar nur eine minimale Absicherung gegen Trolle, aber besser als gar nichts... ;-)
  **Die Zuordnung zu einem Symbol ist Zufällig (X oder O) und der Server merkt sie sich intern!**
  * `POST /ttt/:id/move`: Postet einen neuen Zug, den der Server durchführt, sofern er gültig ist. Parameter im JSON-Body:
    * `player_id`: ID des Spielers als String (Zuordnung zum Spielstein erfolgt intern!)
    * `field`: Nummer des Feldes (0-8)
  * `GET /ttt/:id/move`: Gibt die Liste (History) der getätigten Züge in ihrer Reihenfolge als JSON-Objekt zurück. 
  Die Spieler-IDs bleiben privat und werden durch den jeweils gesetzten Spielstein (X oder O) ersetzt.
* **Optional** kann das Executable den Kommandozeilenparameter `--cli` bereitstellen, um interaktiv auf der Shell testen zu können. 
  In diesem Fall muss natürlich ein zusätzliches ASCII-Interface via stdin/stdout implementiert werden. 
* **Optional** kann das `POST /ttt/`-Interface um einen Body-Parameter `engine_mode` eweitert werden. Wenn dieser auf `true` gesetzt wird, kann nur ein Spieler (immer "X") teilnehmen und der Server spielt als "O".

### Der Client
Der Client soll in einem Browser laufen und das oben beschriebene REST-Interface benutzen, um:
1. den Spielern ein möglichst immersives und packendes Spielerlebnis zu bereiten und
2. es Zuschauern ermöglchen, dem Kampf der Gladiatoren in quasi-Echtzeit beizuwohnen

### Zeitrahmen
Ein Tag. Nur kein Streß! 

Viel Spaß! :-)
