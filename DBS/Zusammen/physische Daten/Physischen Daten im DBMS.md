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

Die Größe eines Records ist festgelegt
- Fixed Size -> Alle Tupel *gleiche* Größe
- Variable Size -> Tupen *unterschiedliche* Größe

Dateien auf Massenspeichern abglegt


>[! Markieren der Lücken]
>Markiere die Lücke als gelöscht und fülle sie später mit neuen Tupeln auf. * 
>>Free- List: Eine Möglichkeit, die freien Lücken zu verwalten: Markiere die erste Lücke im File-Header, um den Beginn der Liste freier Blöcke zu kennzeichnen. 
>>>Benutze die Lücken selbst, um auf weitere Lücken zu verweisen (verkettete Liste freier Speicherbereiche).

Datenstrukturen Heap, Sequenziell, Hash

### Indexstrukturen
![[Pasted image 20260513131931.png]]


![[Pasted image 20260513131639.png]]

![[Pasted image 20260513131650.png]]



## Indexstrukturen 






## Design Tuning




