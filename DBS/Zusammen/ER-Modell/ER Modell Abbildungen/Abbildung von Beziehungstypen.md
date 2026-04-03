Sprich die Notation von Relationsschemata #DBS 

## Abbildungen von N:M Beziehungen
![[Pasted image 20260318202935.png]]

![[Pasted image 20260318203007.png]]

## Abbildungen von 1:N Beziehungen
![[Pasted image 20260318203058.png]]

Jedoch kann das verbessert werden indem man zusammenlegt.
![[Pasted image 20260318204242.png]]

Merke: *Relationen mit denselben Schlüssen sollten kombiniert werden (ausschließlich!)*

## 1:1 Beziehungen

![[Pasted image 20260318204713.png]]

Kann auch wieder verbessert werden indem man es zusammenlegt

![[Pasted image 20260318204739.png]]

So wie man sieht, kann eine [totale Partizipation]([[Participation Constraints]]) in eine einzige Relation gepackt werden.

### Zusammenfassung

##### M:N-Beziehung
- Neue Relation mit Attributen des Beziehungstyps
- Attribute hinzufügen die eine Referenz auf Primärschlüssel bilden (Fremdschlüssel)
- Primärschlüssel: Menge aller Fremdschlüssel
##### 1:N-Beziehung
- Attribute zur Relation des Entitytyps aud der N Seite hinzufügen
	- Fremschlüssel, der den Primärschlüssel des auf der 1 Seite referenzieren 
	- Attribute des Beziehungstyps hinzufügen
##### 1:1-Beziehung
- Aatribute eines der involvierten Entitytypen hinzufügen
	- Fremdschlüssel, der den Primärschlüssel des auf der 1 Seite referenzieren
	- Attribute des Beziehunstyps hinzufügen