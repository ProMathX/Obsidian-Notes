#DBS
Die Attributhülle $\alpha^{+}$ bezüglich einer Menge von FDs $F$ und einer 
Menge von Attributen $\alpha$ ist 
$$
\alpha^{+} = \{A | \alpha \to A \in F^{+}\}
$$
Somit gilt dann $\alpha \to \beta \in F^{+} \implies \beta \in \alpha^{+}$
### Algo für die Attributhülle
Man kann sich die Attributhülle algorithmisch ausrechnen
Input:
- Menge von FDs F
- eine Mengen von Attributen $\alpha \subseteq R$

##### Info zum Algo
Er berechnet $\alpha$ korrekt
- Bei der Termination: alle Teile der Attributhuelle von $\alpha$ sind in result
- Der Algorithmus terminiert 

![[Pasted image 20260323210731.png]]

Wenn ich den Ausführe:
![[Pasted image 20260323210831.png]]

#### Wozu?
1. **Schlüssel finden:** Wenn die Hülle einer Attributmenge **alle** Attribute der Relation enthält, dann ist diese Menge ein **Superschlüssel**.
    
2. **FDs prüfen:** Willst du wissen, ob A→C gilt, obwohl es nicht direkt in deiner Liste steht? Berechne A+. Wenn C darin vorkommt, ist die Abhängigkeit gültig.
    
3. **Äquivalenz:** Du kannst prüfen, ob zwei Mengen von FDs das Gleiche aussagen.


#### Beispiel 1 
- **Relation R:** {A,B,C,D}
    
- **Startmenge α:** {A,D}
    
- **Menge der FDs (F):**
    
    1. A→B
        
    2. A→C
        
    3. CD→A
        

---

### Der Ablauf des Algorithmus

#### Schritt 1: Initialisierung

`result = α` Wir starten also mit dem, was wir sicher wissen: **`result` = {A, D}**

#### Schritt 2: Erster Durchlauf der `repeat`-Schleife

Wir gehen alle FDs in F nacheinander durch:

1. **Prüfe A→B:** Ist β (hier {A}) in `result`? **Ja**, A ist in {A,D}.
    
    - _Aktion:_ Füge γ (hier {B}) hinzu.
        
    - **`result` = {A, D, B}**
        
2. **Prüfe A→C:** Ist β (hier {A}) in `result`? **Ja**, A ist vorhanden.
    
    - _Aktion:_ Füge γ (hier {C}) hinzu.
        
    - **`result` = {A, D, B, C}**
        
3. **Prüfe CD→A:** Ist β (hier {C,D}) in `result`? **Ja**, sowohl C als auch D sind jetzt in `{A, D, B, C}` enthalten.
    
    - _Aktion:_ Füge γ (hier {A}) hinzu.
        
    - **`result` = {A, D, B, C}** (Keine Änderung, da A schon drin war).
        

#### Schritt 3: Abbruchbedingung prüfen

Hat sich `result` im letzten Durchlauf geändert? **Ja** (B und C kamen dazu). Also müssen wir die Schleife laut Algorithmus eigentlich noch einmal wiederholen.

#### Schritt 4: Zweiter Durchlauf

Wir prüfen die FDs erneut, aber da bereits alle Attribute der Relation (A,B,C,D) im `result` enthalten sind, kann offensichtlich nichts Neues mehr hinzukommen.

**Der Algorithmus terminiert (endet).**

---

### Das Endergebnis

Die Attributhülle von {A,D} ist die Menge aller Attribute der Relation:

α+={A,B,C,D}


