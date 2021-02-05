# dbfileorga

### Starten der MitgliederDB
Um die jeweilige Mitglieder DB zu starten müssen folgende Java Dateien ausgeführt werden.  
Sortierte DB: [StartMitgliederDBOrdered.java](src/dbfileorga/StartMitgliederDBOrdered.java)  
Unsortierte DB: [StartMitgliederDB.java](src/dbfileorga/StartMitgliederDB.java)

### Beachtete Spezialfälle
- Es entsteht keine Lücke beim Löschen
- Bei einer Modifikation die Länger/kürzer ist werden die Records nach vorne/hinten verschoben
- Standart ErrorHandling um Exceptions zu vermeiden

### Nicht beachtete Spezialfälle
- Modifizierung des Sortierbegriffes ordnet modifizirten Record an richtiger Stelle ein (Hierzu wird die Insert Funktion bei einer sortierten DB benötigt)

### Implementierungen
#### Read
Um den gewünschten Record aus der Datenbank zu holen, wird die bereits implementierte Methode **getRecord(recNum)**
von der [DBBlock.java](src/dbfileorga/DBBlock.java) verwendet. Um diese zu verwenden musste der jeweilige Block
sowie die Position des Records im jeweiligen Block ermittelt werden.

#### FindPos
Für die Suche wurde die lineare Suche implementiert. 
Hierbei wurde das erste Attribut aller Records mit dem Suchbegriff verglichen. Hierzu wurde die Funktion read(recNum) verwendet 
um den Record und die Funktion getAttribut(1) um das erste Attribut des Records zu holen.
Danach konnte das Attribut mit dem Suchbegriff mit equals verglichen werden.

#### Insert
Da insert nur für die unsortierte Liste implementiert werden musste,
konnte der jeweilige Record am Ende der Datenbank einfach angehängt werden.
Hierzu wurde die bereits implementierte Funktion appendRecord(Record) verwendet. 
Um die jeweilige Record Nummer zurückzugeben wurde die Funktion getNumberOfRecords() verwendet,
da sich der Record an letzter Stelle befindet und somit die Record Nummer gleichzeitig der Gesamtzahl der Records, entspricht.

#### Delete
Um ein Record Objekt zu löschen müsste die Referenz auf das Objekt gelöscht werden.
Dies ist jedoch nicht so einfach möglich, da die Records mehr oder weniger über das CharArray block im Objekt DBBlock referenziert werden.
Daher haben wir es als einfacher erachtet, den gesamten Block zu überschreiben.
Hierzu wurden die Records vom jeweiligen Block, sowie alle nachfolgenden, ausgenommen dem zu löschenden Record in einem Array gespeichert.
Anschließend wurden alle Blöcke, ab dem zu löschenden Record, neu erzeugt um diese zu leeren. Mittels der appendRecord(Record) Funktion
konnten nun alle Records aus dem Array wieder in die Datenbank eingefügt werden.

#### Modify
Funktioniert ähnlich wie Delete, nur anstatt den zu löschenden Record beim speichern wegzulassen, wurde dieser durch den übergebenen ersetzt.


