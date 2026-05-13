Zusammenfassung der Folien 8


## Datenorganisation
- Primärspeicher (Volatile Storage)
- sekundärspeicher (Non-Volatile Storage)
	- Festplatte
- Tertiärspeicher (Non-Volatile Storage)
	- Magnetbäder
- -> Je höher die Hierarchie umso schneller ist der Speicher

Bei mechanischen Festplatten kann man eine Zugriffsoptimierung machen. Jede *Spur (Track)* ist unterteilt in Sektoren 
Eine *Seite (Block/Page)* ist eine kontinuierliche *Sequenz von Sektoren*

Opitmierung des Festplattenzugriffs
- Blöcke i.d Reihenfolge anordnen in der sie auch benötigt werden
- Verwandte Information aneinander legen

>[!Merke]
>Grundsätzlich werden relationale Daten als Sequenzen von Bits auf der Festplatte gespeichert

Funktionale Anforderungen 
- Records sequenziell abarbeiten
- Effiziente Key-Value-Suche
- Löschen von Tupeln (Records)

Performanceanforderungen
- Speicherplatz optimiert
- Schnelle Antowrtzeiten
- Hoher Durchsatz von Transaktionen


Wie werden aber Daten auf einer Festplatte abgespeichert? 
- Eine Datenbank wird als Menge von *Dateien (Files)* gespeichert (nona)
- Jede Datei einthält *Tupeln(Records)*
- Ein Tupel enthält eine bestimmte Anzahl an *Feldern(Fields)*

>[!Merke]
>Mehrere Records werden in Seiten/Blöcken (pages/blocks) zusammengefasst





## Indexstrukturen 






## Design Tuning




