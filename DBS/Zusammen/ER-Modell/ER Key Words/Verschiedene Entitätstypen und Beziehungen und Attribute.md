#DBS 

### Schwache Entitytypen

- Die Existenz eines **schwachen Entitys** hängt von der Existenz eines 
**starken Entitys** ab
- Schwache Entities sind nur mit dem [Schlüssel]([[Schlüssel Hierarchie Canvas.canvas]]) eindeutig identifizierbar
	- Die Schlüsselattribute des Schwachen Entitytyps werden 
	  gestrichelt (*Teilschlüssel*)

![[Pasted image 20260318201409.png]]


Merke bei schwache Entitytypen und deren identifizierende Beziehungstypen können *immer* zusammengeführt werden
wine: {[color, <u>name</u> ]}
vintage:{[<u>name → wine, year</u>, residualSweetness]}
#### Beispiel 
![[Pasted image 20260318210428.png]]


### Der ISA-Beziehungstyp
Spezialisierung und Generalisierung wird durch den isa-Beziehungstyp
ausgedrückt (Vererbung)

![[Pasted image 20260318201607.png]]


##### Bei [totaler]([[Participation Constraints]]) Generalisation/Spezialisierung
- Jeder weniger spezialisierte Entitytyp muss zu einem spezialisiertem Entitytyp gehören. 
- Notation: doppelte Linie

##### Bei [partielle]([[Participation Constraints]]) Generalisation/Spezialsierung (default!)
Jeder weniger spezialisierte Entitytyp kann (aber muss nicht) zu einem superspezialisierterem Entitytyp gehören.

#### Relationale Modellierung der Generalisierung
Das relationale Modell unterstützt keine Generalisierung und kann daher keine Vererbung ausdrücken
Deshalb wird die Generalisierung *simuliert*
**Beispiel:**
![[Pasted image 20260318211512.png]]

##### Möglichkeit 1: Hauptklassen
Ein bestimmtes Entity wird abgebildet als ein Tupel in einer einzigen R.
- employee: {[<u>empID</u>,name]}
- professor: {[<u>empID</u>,name,rank,office]}
- assistant: {[<u>empID</u>,name,department]}

![[Pasted image 20260320185939.png]]
##### Möglichkeit 2: Partitionierung
![[Pasted image 20260318211844.png]]

*Tabellarisch:*
![[Pasted image 20260318211907.png]]

##### Möglichkeit 3: Vollständige Redundanz
Ein bestimmtes Entity wird redundant in mehreren Relationen 
gespeichert inklusive aller geerbten Attribute.

![[Pasted image 20260318211945.png]]

##### Möglichkeit 4: Eine einzige Relation
Alle Entitys werden in einer einzigen Relation gespeichert und ein
besonderes Attribut hinzugefügt, welches die Zugehörigkeit zu einem
bestimmten Entitytyp angibt.

Daraus folgt:
- employee: {[<u>empID</u>, name, <mark style="background: #FF5582A6;">type,</mark> rank, office, department]}

![[Pasted image 20260318212035.png]]
### Rekursive Beziehungstypen
**Allgemein**
![[Pasted image 20260318210506.png]]

*Ein Beispiel*
![[Pasted image 20260318210518.png]]

### N-äre Beziehungstypen

#### N:M:P
![[Pasted image 20260318210828.png]]
#### N:M:1 
![[Pasted image 20260318210841.png]]
##### ACHTUNG! 
![[Pasted image 20260318211103.png]]

### Attribute

#### Zusammengesetzte Attribute
![[Pasted image 20260318210855.png]]

#### Abgeleitete Attribute
![[Pasted image 20260318210903.png]]

