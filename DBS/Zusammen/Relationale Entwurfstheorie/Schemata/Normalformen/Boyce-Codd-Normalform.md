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

#### BCNF Algorithmus 
>[! Schritt 1]
>Starte mit Z={R}

>[!Solange es noch eine FD in einem Schema Ri ∈ Z gibt, die die BCNF verletzt]

```
Zerlege Ri in
    - Ri1 = α ∪ β
    - Ri2 = Ri - β
Entferne Ri aus Z und füge Ri1 und Ri2 ein

```

#### Beispiel 
Gleiches Beispiel wie bei [3NF](obsidian://open?vault=Obsidian-Notes&file=DBS%2FZusammen%2FRelationale%20Entwurfstheorie%2FSchemata%2FNormalformen%2FDritte%20Normalform%203NF)

Die Relation E->AD Vereltzt die BCNF

Weil:
1. Nicht trivial
2. E ist kein Superschlüssel (Kandidat für superschlüsse: {C,D})

Deshalb:
1. Initialisierung
$$
Z = \{A,B,C,D,E\}
$$
2. $R_{i}$ definieren
$$
R_{i}:= \{A,B,C,D,E\}
$$
$$
E \to AD
$$
Verletzt die BCNF, da E kein Superschlüssel ist

$$
\alpha := \{E\} 
$$
$$
\beta := \{A,D\}
$$

$R_{i1} := \alpha \cup \beta \leftrightarrow \{E,A,D\}$

$R_{i2} := R_{i} :\Leftrightarrow Z : Z-\beta := \{A,B,C,D,E\} - \{A,D\} = \{B,C,E\}$

$Z$ neu definieren := $\{R_{i1}, R_{i_2}\} = \{[E,A,D],[B,C,E]\}$
$\square$

#### Links 
[Wikipedia](https://de.wikipedia.org/wiki/Normalisierung_(Datenbank)?useskin=vector)
