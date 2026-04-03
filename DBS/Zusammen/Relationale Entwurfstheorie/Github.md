### Abhängigkeitstreue
Menge der FDs ist äquivalent zur Menge der Schlüsselabhängigkeiten. (i.e. wir
verlieren keine FD)

### Verbundtreue
Alle Anwendungsdaten können aus den Basisrelationen durch natural joins
hergeleitet werden.

**Ein Kriterium:**
X zerlegt in X_1 / X_2 ist verbundtreu, falls  
X_1 ∩ X_2 Schlüssel für X_1 oder  
X_1 ∩ X_2 Schlüssel für X_2

z.B. R = (A B C), A -> B, B -> C  
X_1 = (AB), X_2 = (BC) ist verbundtreu, da X_1 ∩ X_2 = B  
und B -> (BC) = X_2 gilt (B ist Schlüssel für X_2).

**Anderes Kriterium:**
Eine Relation muss einen Universalschlüssel enthalten, d.h. eine Zerlegung X_i
-> X.

### Primattribut
Attribut, das Teil eines Schlüsselkandidaten ist

### Nicht-Primattribut
Attribut, das nicht Teil eines Schlüsselkandidaten ist

## Determinate
Attributmenge von der andere Attribute funktional abhängen.

### 1 NF
Alle Attribute sind atomar (also keine Listen oder so).

Nicht in 1 NF:
| Name  | Tiere              |
|-------|--------------------|
| Peter | Goldi, Rotlöckchen |


### 2 NF
Kein Nicht-Primattribut hängt funktional von einer *echten* Teilmenge eines
Schlüsselkandidaten ab.  
I.e. eliminiert *partielle* Abhängigkeiten von einem Nicht-Prim zu Primattribut.

Triviale Erfüllung:
1. Keine Nicht-Primattribute
2. Schlüsselkandidaten sind nur ein Attribut

### 3 NF
Kein Nicht-Primattribut hängt *transitiv* von einem Schlüsselkandidaten ab. Ein
Nicht-Primattribut darf also nur *direkt* von einem Schlüsselkandidaten
abhängen.

Warum? Transitive Abhängigkeiten offenlegen, thematische Durchmischung
vermeiden.

Triviale Erfüllung:
1. Keine Nicht-Primattribute


### BCNF
Jede Determinate (Menge, von der andere Attribute funktional abhängen) ist Schlüsselkandidat.
I.e. wenn X -> Y gilt, ist X ein Schlüsselkandidat

Überführung nicht immer abhängigkeitstreu möglich

### 4 NF
Nur triviale mehrwertige Abhängigkeiten (Alle mehrwertigen Abhängigkeiten sind nicht unabhängig):

| Personnummer | Haustier | Fahrzeug |
|--------------|----------|----------|

ist nicht in 4 NF, da Personnummer -> Haustier, Personnummer -> Fahrzeug MWA,
aber Haustier -> Fahrzeug nicht existiert
==> Unabhängig

| Person | Partner | Kind |
|--------|---------|------|

ist in 4NF. Person -> Partner, Person -> Kind, aber auch Partner -> Kind.


### Multi valued dependency

Triviale (X ->> Y): Y folgt bereits aus X (durch FD)

Erkennen A:
1. Aufspalten der Relation an FD
2. Natural joinen
3. Schauen, ob alle Tupel drinnen sind

Erkennen B (A ->> B):
1. Für jeden Wert von A:
   2. Halte A fest
   3. Sammle alle Tupel mit A=der Wert
   4. Sammle alle B Werte, die in diesen Tupeln vorkommen
   5. Tausche die B Werte in den Tupel aus 2 rum, bilde alle Kombinationen
   6. Wenn einer nicht drinnen ist, ist das kaputt


## Synthesealgorithmus

1. Einführung neuer FD (Alles) -> δ
2. Rechtsreduktion (Nur ein Attribut rechts, also aufspalten)
3. Linksreduktion  (Keine überflüssugen Attribute links, die sich durch andere
   Abhängigkeiten ergeben)

   z.B. A -> B und AB -> C zu A -> B, A -> C

4. Reduktion von redundanten FD (Membership test)
   5. Eine löschen
   6. Hülle bilden
   7. Go to i.
8. Äquivalenzklasen bilden (Zusammenfassen von FD mit gleicher oder
   äquivalenter (Es gibt A -> B und B -> A, sie sind also gleich mächtig)
   linker Seite)
