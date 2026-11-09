---
topic: Sprachen, Kontextfreie Grammatiken
date: 2026-03-16
course:
tags:
  - studies
  - ThIf
  - "#Sprachen"
  - "#Automaten"
---
## VO

- [[#Grundlagen]]
- [[#Turingmaschinen]]
- [[#Reguläre Sprachen]]
- [[#Grammatiken]]
- [[#Kontextfreie Grammatiken und Sprachen]]
- [[#Jenseits der Kontextfreiheit]]
- [[#Chomsky Hierarchie]]

Marion Oswald die Goat
<br>
### Grundlagen

#### Wörter
![[Pasted image 20261109121930.png]]

im englischen ist das empty word ein lambda fun fact, tinf trivia

konketenation ist nicht kommutativ
#### (Formale) Sprachen
![[Pasted image 20261109123003.png]]

wenn n >= 0, fällt logischerweise das leerwort auch weg
w = {$\epsilon$} = $w^r$ = {$\epsilon$}
genau wie {0} etc pp


#### Operationen auf Sprachen
![[Pasted image 20261109123642.png]]

#### Rechenrecgeln für Sprachoperatioren
![[Pasted image 20261109123702.png]]

#### Mengenoperation auf Sprachen
![[Pasted image 20261109124355.png]]


#### Abgeschlossenheit
![[Pasted image 20261109124421.png]]

### Turingmaschinen

![[Pasted image 20261109124818.png]]


Eine Turingmaschine M besteht aus folgenden Komponenten:
- Ein Eingabeband kann von links nach rechts gelesen werden. Es beinhaltet eine endliche Folge von Zeichen (Eingabewort), Eingabewort vom Anfangssysbol $Z_{1}$ und vom Endsymbol $Z_{2}$ begrenzt ist.
- Das Arbeitsband kann beliebig gelesen und beschrieben werden
- Die endliche Kontrolle kann einen Zusatnd aus einer endlichen Menge von Zuständen annehmen und steuert den Lesekopf auf dem Eingabeband und Lese-/Schreibkopf auf dem Arbeitsband; die Kopfbewegung sind LRS (left right stay)


#### Formale Beschreibung einer Turingmaschine

Eine turingmaschine ist ein Achttupel

$$
M = (Q,T,\Gamma,\delta,q_{0}, \{Z_{0},Z_{1},Z_{2}\},B,F)
$$
- $Q$ endliche Menge von Zuständen
- $T$ Alphabet des Eingabebandes
- $\Gamma$ Alphabet des Arbeitsbandes
- $\delta$ Übergangsfunktion
- $q_{0}\in Q$ Startzustand
- $Z_{0}\in\Gamma$ linkes Begrenzungssysmbol auf Arbeitsband, $Z_{1} Z_{2}$ Begrenzungssymbole des Eingabewortes
- $B \in \Gamma$ Blanksymbol
- $F \subseteq Q$ von Endzuständen

#### Übergänge
![[Pasted image 20261109143947.png]]

M liest im Zustand q auf dem Eingabeband Symbol a und auf dem Arbeitsband Symbol X
- wechselt nun davon abhängig in den Zustand p
- überschreibt auf dem Arbeitsband Symbol X durch Symbol Y
- bewegt auf dem Eingabeband den Lesekopf in die durch $D_{E}$ beschreibene Richtung und auf dem Arbeitsband den Lese-/Schreibkopf in die durch $D_{A}$ beschriebene Richtung ($D_{E},D_{A}\in\{L,R,S\}$)

#### (Deterministische TM) akzeptierte Sprache

>[!Akzeptierte Sprache]
>Die von der TM M akzeptierte Sprache L(M) besteht aus genau all jenen Wörtern, bei deren Analyse M einen Endzustand erreicht.

>[!Deterministische Turingmaschine]
>Eine Turingmaschine M heißt deterministisch, wenn für alle $(q,a,X;p,Y,D_{E},D_{A})\in \delta$ existiert; man schriebt auch $\delta(q,a,X)=(p,Y,D_{E},D_{A})$

#### Beispiel
![[Pasted image 20261109144704.png]]


$$\delta(q,\, b,\, A) = (q,\, C,\, R,\, L)$$
Allgemein gilt:

$$\delta(\underbrace{q}_{\text{Zustand}},\, \underbrace{b}_{\text{Eingabe}},\, \underbrace{A}_{\text{Arbeitsband}}) = (\underbrace{q}_{\text{neuer Zustand}},\, \underbrace{C}_{\text{schreibe}},\, \underbrace{R}_{\text{Eingabekopf}},\, \underbrace{L}_{\text{Arbeitskopf}})$$

| Teil          | Wert                                      | Bedeutung                                                     |
| ------------- | ----------------------------------------- | ------------------------------------------------------------- |
| Bedingung     | Zustand $q$, Eingabe $b$, Arbeitsband $A$ | Die Regel greift nur, wenn alle drei zutreffen                |
| Neuer Zustand | $q$                                       | Zustand bleibt gleich, die Regel läuft also in einer Schleife |
| Schreiben     | $C$                                       | Das $A$ unter dem Arbeitskopf wird durch $C$ ersetzt          |
| Eingabekopf   | $R$                                       | Weiter zum nächsten Eingabezeichen                            |
| Arbeitskopf   | $L$                                       | Ein Feld nach links, zum nächsten $A$                         |

Dabei passiert Folgendes:

1. Für jedes eingelesenes Symbol a  wird ein A aufs Arbeitsband geschrieben
2. Wenn das erte Symbol b eingelesen wird, geht M einen Schritt nach links, dieses erste Symbol b wird bei der ersten Anwendung von Übergang 3 nochmal gelesen
3. für ein eingelesen Symbol b wird ein A auf dem Arbeitsband mit C überschrieben
4. wird das erste Symbol c gelesen muss M genau $Z_{0}$ erreicht haben
5. für jedes eingelesene Symbol c wird nun ein C auf dem Arbeitsband gelöscht (durch das Blanksymbol B ersetzt)
6. wird mit dem Ende der Eingabe (dh dem Erreichen von $Z_{2}$) gleichzeitig das Ende der Symbole C auf dem Arbeitsband erreicht, so hält die Turingmaschine M im Endzustand s und hat damit die Eingabe akzeptiert

| Folie | Regel                         | Aussage                                                                                                                                                                          |
| ----- | ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1     | $\delta(p,a,B)=(p,A,R,R)$     | Für jedes $a$ wird ein $A$ aufs Arbeitsband geschrieben.                                                                                                                         |
| 2     | $\delta(p,b,B)=(q,B,S,L)$     | Beim ersten $b$ bleibt der Eingabekopf stehen ($S$), der Arbeitskopf geht einen Schritt nach links ($L$), auf das letzte $A$. Das $b$ wird deshalb bei Regel 3 nochmals gelesen. |
| 3     | $\delta(q,b,A)=(q,C,R,L)$     | Für jedes $b$ wird ein $A$ mit $C$ überschrieben.                                                                                                                                |
| 4     | $\delta(q,c,Z_0)=(r,Z_0,S,R)$ | Beim ersten $c$ muss der Arbeitskopf genau auf $Z_0$ stehen, also gleich viele $a$ und $b$.                                                                                      |
| 5     | $\delta(r,c,C)=(r,B,R,R)$     | Für jedes $c$ wird ein $C$ durch das Blank $B$ gelöscht.                                                                                                                         |
| 6     | $\delta(r,Z_2,B)=(s,B,S,L)$   | Ende der Eingabe ($Z_2$) und Ende der $C$'s fallen zusammen, also Endzustand $s$.                                                                                                |

Kompletter Durchgang mit `aaabbbccc` ($n=3$)
Startkonfiguration
- Zustand: $p$
- Eingabekopf: auf dem ersten $a$
- Arbeitsband: $Z_0\ B\ B\ B\ B\ B$, Kopf auf dem ersten Blank rechts von $Z_0$

Der Kopf steht in eckigen Klammern. Jede Zeile zeigt die Konfiguration **nach** Anwendung der angegebenen Regel. Die Markierung $Z_2$ rechts hinter der Eingabe ist nur dort eingezeichnet, wo sie relevant wird.

| Schritt | Regel | Zustand | Eingabeband | Arbeitsband |
|---|---|---|---|---|
| 0 | Start | $p$ | `[a]aabbbccc` | `Z₀ [B] B B B B` |
| 1 | 1 | $p$ | `a[a]abbbccc` | `Z₀ A [B] B B B` |
| 2 | 1 | $p$ | `aa[a]bbbccc` | `Z₀ A A [B] B B` |
| 3 | 1 | $p$ | `aaa[b]bbccc` | `Z₀ A A A [B] B` |
| 4 | 2 | $q$ | `aaa[b]bbccc` | `Z₀ A A [A] B B` |
| 5 | 3 | $q$ | `aaab[b]bccc` | `Z₀ A [A] C B B` |
| 6 | 3 | $q$ | `aaabb[b]ccc` | `Z₀ [A] C C B B` |
| 7 | 3 | $q$ | `aaabbb[c]cc` | `[Z₀] C C C B B` |
| 8 | 4 | $r$ | `aaabbb[c]cc` | `Z₀ [C] C C B B` |
| 9 | 5 | $r$ | `aaabbbc[c]c` | `Z₀ B [C] C B B` |
| 10 | 5 | $r$ | `aaabbbcc[c]` | `Z₀ B B [C] B B` |
| 11 | 5 | $r$ | `aaabbbccc[Z₂]` | `Z₀ B B B [B] B` |
| 12 | 6 | $s$ | `aaabbbccc[Z₂]` | `Z₀ B B [B] B B` |

Insgesamt sind es $3n+3 = 12$ Schritte, also linear in $n$.

#### Normalform
Eine DTM ist in Normalform, wenn 
- sie nur einen Endzustnad bestitzt
- das Arbeitsband am Ende eines akzeptierenden Laufes der Turingmaschine leer ist
- der letzte Übergang von Gestalt $\delta(s,Z_{2},Z_{0}) = f(f,Z_{0},S,R)$ ist, wobei f dieser einzige Endzustnad und s ein beliebiger anderer Zustand ist

![[Pasted image 20261109153856.png]]


| Schritt | Regel | Zustand | Eingabeband     | Arbeitsband      |
| ------- | ----- | ------- | --------------- | ---------------- |
| 0       | Start | $p$     | `[a]aabbbccc`   | `Z₀ [B] B B B B` |
| 1       | 1     | $p$     | `a[a]abbbccc`   | `Z₀ A [B] B B B` |
| 2       | 1     | $p$     | `aa[a]bbbccc`   | `Z₀ A A [B] B B` |
| 3       | 1     | $p$     | `aaa[b]bbccc`   | `Z₀ A A A [B] B` |
| 4       | 2     | $q$     | `aaa[b]bbccc`   | `Z₀ A A [A] B B` |
| 5       | 3     | $q$     | `aaab[b]bccc`   | `Z₀ A [A] C B B` |
| 6       | 3     | $q$     | `aaabb[b]ccc`   | `Z₀ [A] C C B B` |
| 7       | 3     | $q$     | `aaabbb[c]cc`   | `[Z₀] C C C B B` |
| 8       | 4     | $r$     | `aaabbb[c]cc`   | `Z₀ [C] C C B B` |
| 9       | 5     | $r$     | `aaabbbc[c]c`   | `Z₀ B [C] C B B` |
| 10      | 5     | $r$     | `aaabbbcc[c]`   | `Z₀ B B [C] B B` |
| 11      | 5     | $r$     | `aaabbbccc[Z₂]` | `Z₀ B B B [B] B` |
| 12      | 6     | $s$     | `aaabbbccc[Z₂]` | `Z₀ B B [B] B B` |
| 13      | 7     | $s$     | `aaabbbccc[Z₂]` | `Z₀ B [B] B B B` |
| 14      | 7     | $s$     | `aaabbbccc[Z₂]` | `Z₀ [B] B B B B` |
| 15      | 7     | $s$     | `aaabbbccc[Z₂]` | `[Z₀] B B B B B` |
| 16      | 8     | $f$     | `aaabbbccc[Z₂]` | `Z₀ [B] B B B B` |

Insgesamt sind es $4n+4 = 16$ Schritte, also immer noch linear in $n$. Der Rücklauf kostet $n+1$ Schritte mehr als bei $M$.

#### TM: eingeschränkte Variante - LBA

Ein linear bschränkter Automat (LBA) ist eine Turingmaschine, die auf dem Arbeitsband nur höchstens soviel Platz verwendet wie das Eingabewort lang ist (der darf sogar eine lineare Funktion der Länge des Eingabewortes sein)

>[!LBA]
>Eine TM M heißt linear beschränkter Automat, wenn es eine lineare Funktion cn+d so gibt, dass die Turingmaschine M für jedes Eingabewort w der Länge n während der Analyse höchstens cn+d Felder auf dem Arbeitsband benötigt

#### TM: Eingeschränkte Variante - Kellerautomaten 

Turingmaschine erfüllt Kellerautomatenbedingung, wenn:
- auf dem Eingabeband nie nach links gehen kann
- für den Lese-/Schreibkopf auf dem Arbeitsband in jeder Konfiguration gilt, dass
	- links davon nur Nicht-Blanksymbole
	- recht davon nur Blanksymbole stehen können

Im Wesentlichen ist also ein Kellerautomat eine Turingmaschine, die das Arbeitsband als sogenanneten Keller vewendet. 

Der Kellerautomat, darf per Definition nur das oberste Symbol lesen und diese dann löschen

Ein Kellerautomat ähnelt einem Stack - nach dem LIFO Prinzip 

#### Akzeptierte Sprache eines Kellerautomaten

1. Kellerautomat befindet sich im Sinne einer Turingmaschine nach dem Einlesen des gesamte Eingabewortes in einem akzeptierenden Zustand
2. Kellerautomaten akzeptiert durch leeren Keller (Arbeitsband)

**Normalform:** Eingabewort wird durch Endzustand und leeren Keller (Arbeitsband) akzeptiert, beim Übergang in den (einzigen) Endzustand wird das rechte Begrenzungssymbol $Z_{2}$ des Eingabebandes und im Keller (Arbeitsband) gleichzeitig das Kellergrundsymbol($Z_{0}$) gelesen. (Entspricht der NF für TM)


#### Beispiel eines Kellerautomaten

![[Pasted image 20261109160502.png]]

$$\delta(\underbrace{q}_{\text{Zustand}},\, \underbrace{x}_{\text{Eingabe}},\, \underbrace{Y}_{\text{Keller (Arbeitsband)}}) = \{(\underbrace{q'}_{\text{neuer Zustand}},\, \underbrace{W}_{\text{schreibe}},\, \underbrace{E}_{\text{Eingabekopf}},\, \underbrace{K}_{\text{Kellerkopf}})\}$$

| Schritt | Regel | Zustand | Eingabeband   | Arbeitsband      |     |
| ------- | ----- | ------- | ------------- | ---------------- | --- |
| 0       | Start | $q_0$   | `[0]011111`   | `Z₀ [B] B B B B` |     |
| 1       | 1     | $q_1$   | `[0]011111`   | `Z₀ A [B] B B B` |     |
| 2       | 2     | $q_0$   | `0[0]11111`   | `Z₀ A A [B] B B` |     |
| 3       | 1     | $q_1$   | `0[0]11111`   | `Z₀ A A A [B] B` |     |
| 4       | 2     | $q_0$   | `00[1]1111`   | `Z₀ A A A A [B]` |     |
| 5       | 3     | $q_2$   | `001[1]111`   | `Z₀ A A A [A] B` |     |
| 6       | 4     | $q_2$   | `0011[1]11`   | `Z₀ A A [A] B B` |     |
| 7       | 4     | $q_2$   | `00111[1]1`   | `Z₀ A [A] B B B` |     |
| 8       | 4     | $q_2$   | `001111[1]`   | `Z₀ [A] B B B B` |     |
| 9       | 4     | $q_2$   | `0011111[Z₂]` | `[Z₀] B B B B B` |     |
| 10      | 5     | $q_f$   | `0011111[Z₂]` | `Z₀ [B] B B B B` |     |
|         |       |         |               |                  |     |
Oder in Worten 
![[Pasted image 20261109163712.png]]


#### Turingmaschinen: Eingeschränkte Varianten -EA 

**Endlicher Automat:** Turingmaschine, die das Arbeitsband gar nicht benötigt. Übergänge besitzen einfache Form $(q,a;p,D_{E})$ erlaubt man nur $D_{E}\in\{R, S\}$ kann die Übergangsfunktion $\de$ 





### Reguläre Sprachen

{}^* = {e} durch vereinigen, habe ich nur  jede endlich emenge ist regulär, (siehe vereinigung) 13:23 aufschreiben
aber nicht jede reguläre menge ist endlich, siehe kleene stern. Weil der Kleenestern, nach definition quasi, bis ins unendliche geht. Es gibt unendliche Mengen die keine 

---

### Grammatiken

### Kontextfreie Grammatiken und Sprachen

### Jenseits der Kontextfreiheit 

### Chomsky Hierarchie


# TODO 
- [ ] Turingmaschinen hier machen und verstehen
- [ ] 📅 2026-11-09 VO schöner nacharbeiten, statt stumpf abzuschreiben




