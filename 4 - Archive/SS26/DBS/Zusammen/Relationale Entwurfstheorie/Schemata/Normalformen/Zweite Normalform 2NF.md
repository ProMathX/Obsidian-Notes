#DBS 

Ist aufwendiger 
#### Definition 
>Ein Relationschema R mit FDs $F$
 ist ein 2NF, falls jedes Nicht-Primattribut
 $A \in R$ voll funktional abhaengig von jedem 
 Kandidatenschluessel der Relation ist.
>$$
(k_{j} \to A) \in F^{+}
$$
 und $k_{j}$ ist linksreduziert (voll funktional abh.)
---

Das heißt
---

> Ein Nicht-Primattribut A darf nicht von einer **echten Teilmenge** eines Kandidatenschlüssels κ abhängen
   Du kannst von der linken Seite (κ) nichts wegstreichen, ohne dass die Abhängigkeit kaputtgeht.
---

### Eläuterung von Definition
Eine Relation ist genau dann in der zweiten Normalform, wenn die erste Normalform vorliegt und kein Nichtprimärattribut (Attribut, das nicht Teil eines [Schlüsselkandidaten](https://de.wikipedia.org/wiki/Schl%C3%BCsselkandidat "Schlüsselkandidat") ist) funktional von einer echten Teilmenge eines Schlüsselkandidaten abhängt.

##### Es gelten folgende Eigenschaften:
![[Pasted image 20260324114836.png]]
#### Eliminierung partieller Abhaengigkeiten
![[Pasted image 20260324115130.png]]
![[Pasted image 20260324115326.png]]


### Wichtig
![[Pasted image 20260329154432.png]]

Erklärung von Gemini:

1. **Der volle Schlüssel:** `{studID, courseID}`. (Du brauchst beide, um eine Zeile eindeutig zu identifizieren).
    
2. **Die Abhängigkeit:** `{studID}` → `{name}`
    
3. **Das Problem:** Um den Namen (`name`) zu bestimmen, reicht die `studID` alleine aus. Die `courseID` wird überhaupt nicht benötigt.
    

**Warum nennt man das „partiell“?** Weil `{studID}` nur eine **Teilmenge** (ein Teil) des zusammengesetzten Schlüssels `{studID, courseID}` ist. Das Attribut `name` ist also nur von einem _Teil_ des Schlüssels abhängig – eben **partiell**.

#### Merksatz 
**2NF:** Wenn dein Schlüssel aus mehreren Spalten besteht (A + B), darf keine Info in der Tabelle stehen, die nur von A oder nur von B abhängt. **Alles muss von (A + B) abhängen.**

Also 1NF + Datenfelder von Schlüssel funktional abhängig

Oftmals um die 2NF zu retten verwendet man die [dekomposition](obsidian://open?vault=notes&file=DBS%2FZusammen%2FMitschrift%20und%20Notizen%2FRelationale%20Entwurfstheorie%2FSchemata%2FFunktionale%20Abhaenglkeiten%2FAbleitung%20funktionaler%20Abhaengigkeiten)

#### Links
[Wikipedia](https://de.wikipedia.org/wiki/Normalisierung_(Datenbank)#Zweite_Normalform_(2NF))
[DeineRöhre](https://www.youtube.com/watch?v=caMVrHP-SIs)




