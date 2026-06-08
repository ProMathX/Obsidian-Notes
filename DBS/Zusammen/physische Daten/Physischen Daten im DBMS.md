Zusammenfassung der Folien 8
#DBS 

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

# Indexstrukturen
![[Pasted image 20260513131931.png]]

Merke: 
Primary vs secondary:
- = Clustering vs non-clustering
	- Ist die Datei nach dem Search-Key sortiert? 
		- Ja -> Clustering
		- Nein -> Non-Clustering


![[Pasted image 20260513131639.png]]

![[Pasted image 20260513131650.png]]

Dense vs sparse
- Gibt es einen separaten Eintrag für jedes Tupel bzw. jeden vorkommenden Wer des Search-Keys? 
- Ja -> dense
- Nein -> sparse


### $B^+ -Bäume$

- balancierte Suchbäume Anzahl von Lookups/Levels ist $\forall$ Einträge gleich
- Etwas Platz auf jeder Seite/Block lassen


![[Pasted image 20260513132534.png]]

![[Pasted image 20260513132913.png]]

![[Pasted image 20260513132925.png]]


 Warum in im DBMS? 

- Jeder Knoten hat die größe eines I/O Blocks
- Ein Knoten ist min. 50% gefüllt
- B+ Baum i.d.R sehr flach, wenige wahlfreie Zugriffe
- 1-2 ebenen im Hauptspeicher gecached
- Logisch nahe bedeutet nicht phsisch nahe
	- Lesen erfordert I/O-Zugriff
- Innere Knoten entsprechen einer Hierarcie von sparse Indexes

>[!important]
>Uniqueness-Constraints auf Attributen in einer Datenbank werden durch
B+ -Bäume realisiert → Primärschlüssel


![[Pasted image 20260513133312.png]]


Einfügen in dem B+ Baum

Einfügen den Schlüssel k
- Suche: Finde das Blatt b, das k enthalten müsste
- b genug Platz, füge k ein 
- sonst: spalte knoten b, teile schlüssen under den zwei knoten, ändere den Eintrag im Elternknoten

Merke:
Spalten von Knoten muss rekursiv nach oben folgen
- Wenn wurzel gespalten wird, erhöht sich die Tiefe des Baumes um eine Ebene

![[Pasted image 20260513133714.png]]


Beispiel, n = 3, Einfügen von 35
![[Pasted image 20260513133754.png]]


#### B+- Baum Löschen

Löschen von Schlüsselwert k
- Suche: Finde das Blatt b, das den Schlüsselwert k enthält
	-  Falls b genügend gefüllt bleibt min. ⌈ n ⌉, lösche k 2 Innere Knoten können dann Schlüssel enthalten, die nicht mehr in  den Blättern existieren.
	
- Sonst verschmelze Knoten 
	- Falls Verschmelzen mit Nachbarknoten möglich, verschmelzen und Pointer im Elternknoten anpassen. Falls Verschmelzen nicht möglich, Neuverteilung der Pointer über Elternknoten.

- Verschmelzen muss unter Umständen auch in höheren 
	- Ebenen erfolgen.Die Tiefe des Baumes kann sich um eine Ebene verringern
### Hashing

Erstellen eines Indexes auf Basis einer Hashfunktion anstatt auf Basis eines Search-Keys

- *Hashfunktion* $h$
- Seach-Key-Wert k -> $h(k)$
- Reserviere *Bucket* für jeden Wert von $h(k)$


![[Pasted image 20260513134324.png]]

![[Pasted image 20260513134341.png]]

## Design Tuning
![[Pasted image 20260513134455.png]]

![[Pasted image 20260513134408.png]]

