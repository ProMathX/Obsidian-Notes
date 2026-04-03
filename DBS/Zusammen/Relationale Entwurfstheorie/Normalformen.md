#DBS 
##### Quote of the day
><font color="#2DC26B">The data must depend on the key, the whole key, and nothing but the key (so help me Codd</font>

Es gibt folgende Normalformen 
- [Erste Normalform](obsidian://open?vault=Notes&file=DBS%2FZusammen%2FMitschrift%20und%20Notizen%2FRelationale%20Entwurfstheorie%2FSchemata%2FNormalformen%2FErste%20Normalform%201NF)
- [Zweite Normalform](obsidian://open?vault=notes&file=DBS%2FZusammen%2FMitschrift%20und%20Notizen%2FRelationale%20Entwurfstheorie%2FSchemata%2FNormalformen%2FZweite%20Normalform%202NF)
- [Dritte Normalform](obsidian://open?vault=Notes&file=DBS%2FZusammen%2FMitschrift%20und%20Notizen%2FRelationale%20Entwurfstheorie%2FSchemata%2FNormalformen%2FDritte%20Normalform%203NF)
- [Boyce-Codd-Normalform](obsidian://open?vault=Notes&file=DBS%2FZusammen%2FMitschrift%20und%20Notizen%2FRelationale%20Entwurfstheorie%2FSchemata%2FNormalformen%2FBoyce-Codd-Normalform)
## Motivation
Normalformen
- legen Eigenschaften von Relationschema fest
- verbieten bestimmte Kombinatioenn von funktionalen Abhängigkeiten in Relationen
- sollen Redundanz und Anomalien vermeiden
- Richtlinie um gute Zerlegung zu erhalten
### Uebersicht
![[Pasted image 20260324121607.png]]

![[Pasted image 20260324121619.png]]

### Zusammenfassung
##### Eigenschaften eines guten. Entwurfs
- Vermeidung von Redundanz
- Informationen koennen dargestellt werden
##### FDs
- Armstrong-Axiome um die Huelle zu bestimmen
- Kanonische/minimale Ueberdeckung
- FDs sind ein Werkzeug um guten Entwurf zu garantieren
##### Zerlegung
- Zum Verbessern
- funktionale Abh. Schluesselabhaegigkeit verwandeln
- Gutes ER Modell und Abbildungen von Rel. fuehrt zu 3NF (oder hoeher)
##### 3NF
- Verlustfrei abhaengigkeitsbewahrnd
- Immer erreichbar
![[Pasted image 20260327153326.png]]
![[Pasted image 20260327153348.png]]

##### BCNF
- Verlustfrei nicht abhaengigkeitsbewahrend
#### Denormalisierung
```
Prozess bei dem die Normalisierung "zurueckgenommen" wird, um Anfragen schneller bearbeiten zu koennen
```

#### Materialien
[Video](https://tuwel.tuwien.ac.at/mod/opencast/view.php?id=2865945)