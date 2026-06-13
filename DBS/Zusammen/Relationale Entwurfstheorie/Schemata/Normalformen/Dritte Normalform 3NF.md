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


Anmerkung am 13.6.2026
Bringe die FD's in die Form von $\alpha \rightarrow Attribut$
1) Trivial also $\alpha \rightarrow B \equiv B \rightarrow \alpha$
2) Ist die Linke Seite in unserem Superschlüssel enthalten? 
3) Ist die rechte Seite in einem Schlüssel enthalten? 


### Beispiel 1
![[Pasted image 20260327145454.png]]

![[Pasted image 20260327145605.png]]

#### Probleme 
![[Pasted image 20260327154004.png]]

Nein, deshalb [[Boyce-Codd-Normalform]]



## 3 NF Algorithmus


>[!Schritt 1]
>Bestimme die kanonische Überdeckung 

>[!Schritt 2]
>Aus jeder FD der kanonischen Überdeckung entsteht eine neue Relation

>[!Schritt 3]
>Füge ein neues Relationsschema mit einem Kandidatenschlüssel hinzu, falls keiner der Kandidatenschlüssel vollständig in einem Schema enthalten ist

>[!Schritt 4]
>Eliminiere Ra, wenn Ra ⊆ Ra'

### Beispiel 

R = {[A,B,C,D,E]}

FD's = {
		CD->AEB
		 BCE -> AD
		 E -> AD
	}
Mit der [minimalen Überdeckung]([[Kanoische Ueberdeckung (minimale Ueberdeckung)]])
Hat man CD->EB E -> AD und K = {C,D,E}

1. Schritt done
2. $R_{1} := \{C,D,E,B\}$ $R_{2} := \{E,A,D\}$
3. Es gilt $K \subseteq R_{1}$
4.  Eliminiere Triviale Abhängigkeiten
###### Final 
$R_{1} := \{C,D,E,B\}$ $R_{2} := \{E,A,D\}$
$\square$
---

#### Links 
[Wikipedia](https://de.wikipedia.org/wiki/Normalisierung_(Datenbank)?useskin=vector)

[Tool](https://normalizer.db.in.tum.de/index.py)
