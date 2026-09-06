#DBS 
Bestimmung funktionaler Abhaengigkeiten

![[Pasted image 20260323161556.png]]

#### Wie kann man sie herleiten
- Aus einer Menge von FDs $F$ sind weitere FDs herleitbar
- $F^{+}$ (*Huelle* von F) beinhaltet alle FDs die aus $F$ abgeleitet werden koenne, die also logisch impliziert werden 
- Inferenzregeln (Amstrong-Axiome)

#### Armstrong-Axiome
Man verwendet die Armstrong Axiome um die Huelle F+ zu 
bestimmen.

![[Pasted image 20260323162451.png]]

## Warum macht man das?

Die Ableitung mit diesen Axiomen ist die theoretische Basis für wichtige Schritte im Datenbankdesign:

- **Bestimmung von Superschlüsseln:** Du prüfst, ob ein Attribut (oder eine Gruppe) über die Axiome alle anderen Attribute der Relation ableiten kann.
    
- **Normalisierung:** Um Redundanzen zu finden und eine Tabelle in die 2. oder 3. Normalform (oder BCNF) zu bringen, musst du genau wissen, welche versteckten Abhängigkeiten existieren.
    
- **Kanonische Überdeckung:** Man nutzt die Regeln (oft ergänzt durch abgeleitete Regeln wie Vereinigung oder Zerlegung), um die Menge der FDs so klein und effizient wie möglich zu halte


![[Pasted image 20260323162509.png]]




![[Pasted image 20260331182416.png]]