#DBS 

**ACHTUNG** : mindestens eine der Bedingungen muss erfüllt werden

![[Pasted image 20260324120153.png]]
### Anmerkungen
Transitive Abhängigkeit:
- Ein Nicht-Schlüssel-Attribut hängt von einem anderen Nicht-Schlüssel-Attribut ab
- B ist prim heißt:
> **Das Attribut B gehört selbst zu (mindestens) einem Kandidatenschlüssel** (setzt einen Schlüssel zusammen)

- **Nicht-triviale Abhängigkeit:** Ich erfahre etwas Neues. (z. B. `studID -> Name`)
    
- **Triviale Abhängigkeit:** Ich sage nur das Gleiche nochmal. (z. B. `{studID, Name} -> Name`)

![[Pasted image 20260324120433.png]]

### Beispiel aus den Folien 
![[Pasted image 20260329162626.png]]

(Achtung Erklärung von Gemini)
**1. Ist die Abhängigkeit trivial? (B∈α)**

- _Frage:_ Ist der `name` schon in der `studID` enthalten?
    
- _Antwort:_ Nein. Wenn ich dir eine Nummer (28106) gebe, ist der Name (Carnap) eine neue Information.
    
- _Urteil:_ **Durchgefallen.**
    

**2. Ist α ein Superschlüssel?**

- _Frage:_ Ist die `studID` allein der Schlüssel der gesamten Tabelle?
    
- _Antwort:_ Nein! Der Kandidatenschlüssel lautet `{studID, courseID}`. Die `studID` allein reicht nicht aus, um eine ganze Zeile (z.B. auch das belegte Fach) eindeutig zu identifizieren.
    
- _Urteil:_ **Durchgefallen.**
    

**3. Ist B prim?**

- _Frage:_ Gehört der `name` zu einem Kandidatenschlüssel?
    
- _Antwort:_ Nein. Die Schlüssel-Attribute sind nur `studID` und `courseID`. Der `name` ist nur eine schnöde Zusatzinfo (nicht-prim).
    
- _Urteil:_ **Durchgefallen.**

### Beispiel 1
![[Pasted image 20260327145454.png]]

![[Pasted image 20260327145605.png]]

#### Probleme 
![[Pasted image 20260327154004.png]]

Nein, deshalb [[Boyce-Codd-Normalform]]

#### Links 
[Wikipedia](https://de.wikipedia.org/wiki/Normalisierung_(Datenbank)?useskin=vector)

[Tool](https://normalizer.db.in.tum.de/index.py)
