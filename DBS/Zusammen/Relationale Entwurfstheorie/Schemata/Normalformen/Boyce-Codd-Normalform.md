#DBS 

**ACHTUNG:** mindestens eine Bedingung muss erfüllt sein!
![[Pasted image 20260324120649.png]]
Fuer die Unterschiede zwischen 
[[Dritte Normalform 3NF]] und [[Boyce-Codd-Normalform]]
Siehe [hier]([[DBS-5.pdf]]) Seite 46/60
#### Zerlegung
![[Pasted image 20260324121249.png]]
![[Pasted image 20260324121306.png]]
##### oder in besser
![[Pasted image 20260327154445.png]]
` „Solange du eine Regel (α→β) findest, die die BCNF verletzt, zerschneide die Tabelle in zwei neue Tabellen (Ri1​ und Ri2​).“ `

### Beispiel aus den Folien
![[Pasted image 20260329165057.png]]

(Achtung von Gemini) 
#### 1. Die erste neue Tabelle (Ri1​)

Die Formel lautet: Ri1​:=α∪β Das Symbol ∪ bedeutet „Vereinigung“ (wir werfen beides in einen Topf).

- Wir nehmen die linke Seite des Störenfrieds: `{zip}`
    
- Wir nehmen die rechte Seite des Störenfrieds: `{city, region}`
    
- **Ergebnis Ri1​:** `{zip, city, region}`
    
- _In deinem Beispiel-Bild ist das die Tabelle, die **`cities`** genannt wird._
    

Das ist der einfache Teil. Wir haben einfach die störende Abhängigkeit in eine eigene, isolierte Tabelle ausgelagert. Hier ist `{zip}` jetzt der Schlüssel, also ist alles in Ordnung.

#### 2. Die zweite neue Tabelle (Ri2​)

Die Formel lautet: Ri2​:=Ri​−β Das Symbol − bedeutet „Mengenabzug“ (wir werfen etwas aus der Ursprungstabelle raus).

- Wir nehmen alle Attribute der Ursprungstabelle Ri​: `{street, city, region, zip}`
    
- Wir ziehen die rechte Seite des Störenfrieds (β) ab: `{city, region}` verschwindet.
    
- Was bleibt übrig? `{street, zip}`
    
- **Ergebnis Ri2​:** `{street, zip}`
    
- _In deinem Beispiel-Bild ist das die Tabelle, die **`streets`** genannt wird._
### Beispiel
![[Pasted image 20260327154212.png]]
#### Links 
[Wikipedia](https://de.wikipedia.org/wiki/Normalisierung_(Datenbank)?useskin=vector)
