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

<br>

---

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


#### Turingmaschinen: Eingeschränkte Varianten - Endlicher Automat (EA) 

**Endlicher Automat:** Turingmaschine, die das Arbeitsband gar nicht benötigt. Übergänge besitzen einfache Form $(q,a;p,D_{E})$ erlaubt man nur $D_{E}\in\{R, S\}$ kann die Übergangsfunktion $\delta$ durch Tripel der Gestalt $(q,a;p)$ beschrieben werden $(a \in T \cup \{\varepsilon\})$ 

![[Pasted image 20261109164219.png]]

Also er akzeptiert es wenn $Z_{2}$ erreicht wird im Eingabeband

#### Akzeptierte Sprachen
![[Pasted image 20261109164435.png]]

<br>

---

### Reguläre Sprachen

Reguläre Sprachen sind allgegenwärtig.
- Gebildet durch Vereinigung, Konkatenation und Stern
- Äquivalent: endliche Automaten, reguläre Grammatiken
- Compilerbau, Token bilden reguläre Sprache, verabeitet durch Scanner (Lexer)

---

![[Pasted image 20261109165115.png]]


Es gilt außderdem bei Regulären Sprachen
$\{\}^*=\{\varepsilon\}$

Q: Ist jede endliche Menge regulär? 
A: Ich kann eine endliche Menge immer durch vereinigen von einelementigen Mengen kriegen, deshalb ja

- Einzelne Buchstaben sind nach Definition regulär $\{a\} \in \mathcal{L}_{\mathrm{reg}}(\Sigma)$.
- **Jedes Wort** $w = a_1 a_2 \cdots a_n$ ist regulär, weil $\{w\} = \{a_1\} \cdot \{a_2\} \cdots \{a_n\}$ ein Produkt/Konkatanation regulärer Mengen ist.
-  **Das leere Wort:** $\{\varepsilon\}$ steht nicht direkt in der Definition, ist aber regulär, denn $\{\}^* = \{\varepsilon\}$.
-  **Endliche Vereinigung:** $L = \{w_1\} \cup \dots \cup \{w_k\}$ ist eine endliche Vereinigung regulärer Mengen, also regulär. Für $k=0$ ist $L=\{\}$, und die ist direkt in der Definition enthalten.

---


Q: Jede reguläre Menge endlich? 
A: Der Kleene Stern bringt die unendlichkeit, deshalb nein 

$$A^* = \bigcup_{k \ge 0} A^k$$


Jede endliche Sprache ist regulär, denn jedes Wort ist ein Produkt einzelner Buchstaben, und endlich viele Wörter lassen sich vereinigen. Nicht jede reguläre Sprache ist endlich, denn $A^*$ ist für jedes $A$ mit einem nichtleeren Wort unendlich, z. B. $\{a\}^*$.


#### Endliche Automaten

Modell für Systeme mit Ein/Ausgaben aus endlichem Wertebereich und mit endlichem Speicher

![[Pasted image 20261109171320.png]]


#### DEA: Beispiel
![[Pasted image 20261109171344.png]]

Eingabe: Wort; Ausgehend vom Startzustand liest der Automat $\mathcal{A}$ von links nach rechts Symbol für Symbol.

Nach dem Lesen eines Symbols geht $\mathcal{A}$ in den nächsten Zustand über indem er entlang der mit diesem Symbol markierten Kante geht. Nach dem Lesen des letzten Symbols wird der Output erzeugt:
	Befindet sich $\mathcal{A}$ in einem Endzustand, wird das Wort akzeptiert; ansonsten wird das Wort nicht akzeptiert


#### Deterministische endliche Automaten
![[Pasted image 20261109171413.png]]
Hat ein fixes eingabealphabet

##### Falle
![[Pasted image 20261109171434.png]]

#### Deterministischer endlicher Automat
![[Pasted image 20261109171623.png]]
![[Pasted image 20261109171630.png]]


#### Nichtdeterminsitsche endliche Automaten (NEA)
![[Pasted image 20261109172001.png]]

![[Pasted image 20261109172012.png]]


>[!kurze wh, im Anfang der VO niederschreiben]

startzustand = endzustand -> akzeotiert das leerwort

Rgeuläre sprachen sind auch in ihrem Komplement abgeschlossen
13:50 sehr wichtig in der Vo nachahsuchen foliensatz zu 43, sehr viel wertvolle info

|xy|<= m ersten m symbole !!!! du pumpst das erster occurance von einem m

m ist di eanzahl der minimalzustände im Minimalautomaten

i = 0 für den Widerspruch 

Also, fuck that, es gibt keine Aufzeichnung, fuck that dude


Aufarbeitung ab hier:

----
#### Determinisierung $NEA \to DEA$

Zu jedem NEA gibt es einen äquivalenten DEA. Man kkan aber keinen DEA zu einem NEA transformieren, weil jeder DEA auch ein NEA schon ist.

Die Transformation geht über Teilmengenkonstruktion oder auch besser gesagt Potenzkonstruktion.

![[Pasted image 20261112113423.png]]

**Tipp:** Berechne die Übergangsfunktion ausgehend von $\hat{q}_{0}$ nur für tatsächlich erreichbare Zustände.

![[Pasted image 20261112113606.png]]

https://de.wikipedia.org/wiki/Potenzmengenkonstruktion?useskin=vector



#### Reguläre Menge $\to \varepsilon-NEA$

>[!Merke]
>Zu jeder regulären Sprache L gibt einen endlichen Automaten $\mathcal{A}$, sodass $L = \mathcal{L}(\mathcal{A})$

![[Pasted image 20261112114545.png]]

![[Pasted image 20261112120231.png]]

https://en.wikipedia.org/wiki/Thompson%27s_construction?useskin=vector

Es wurde in der Vorlesung aucht so sehr darauf eingegangen.


#### DEA $\to$ reguläre Menge

>[!Theorem]
>
Jede von ienem DEA akzeptierte Sprache ist regulär.

![[Pasted image 20261112120330.png]]

**Idee für $k > 0$.** Ein Weg von $q_i$ nach $q_j$ benutzt $q_k$ entweder gar nicht (erster Term) oder mindestens einmal. Dann zerfällt er in drei Teile:
1. $q_i \to q_k$ bis zum ersten Besuch von $q_k$ ($R^{k-1}_{ik}$),
2. beliebig viele Schleifen $q_k \to q_k$ ($(R^{k-1}_{kk})^*$),
3. $q_k \to q_j$ nach dem letzten Besuch von $q_k$ ($R^{k-1}_{kj}$).

**Beweis.** Induktion über $k$:
- $k = 0$: $R^0_{ij}$ ist endlich, also regulär.
- $k-1 \to k$: $R^k_{ij}$ entsteht aus $R^{k-1}_{\cdot\cdot}$ nur durch $\cup$, $\cdot$ und $^*$, und reguläre Sprachen sind darunter abgeschlossen.
- $k = n$: Alle Zwischenzustände sind erlaubt, also ist $L(\mathcal{A})$ eine endliche Vereinigung regulärer Sprachen. 

**Merke.** Das Verfahren ist Floyd-Warshall mit $(\cup, \cdot)$ statt $(\min, +)$. Die Ausdrücke können exponentiell groß werden.

- https://en.wikipedia.org/wiki/Kleene%27s_algorithm?useskin=vector


![[Pasted image 20261112121611.png]]

Hier gilt k = n
###### Schritt 0: Automat und Rekursion

$$
\begin{array}{c|cc}
 & 0 & 1 \\ \hline
q_1\ (\text{Start}) & q_2 & q_3 \\
q_2\ (\text{Ende}) & q_1 & q_3 \\
q_3\ (\text{Ende}) & q_2 & q_2
\end{array}
$$

$$
R^k_{ij} = R^{k-1}_{ij} \,\cup\, R^{k-1}_{ik}\,\bigl(R^{k-1}_{kk}\bigr)^*\,R^{k-1}_{kj}
$$

###### Schritt 1: $k=0$ (nur direkte Kanten, bei $i=j$ zusätzlich $\varepsilon$)

$$
\begin{aligned}
R^0_{11} = R^0_{22} = R^0_{33} &= \{\varepsilon\} \\
R^0_{12} = R^0_{21} &= \{0\} \\
R^0_{13} = R^0_{23} &= \{1\} \\
R^0_{32} &= \{0,1\} \\
R^0_{31} &= \{\}
\end{aligned}
$$

###### Schritt 2: $k=1$ ($q_1$ darf Zwischenstation sein)

$(R^0_{11})^* = \{\varepsilon\}^* = \{\varepsilon\}$

- Zeile 1: Umweg $q_1 \to q_1 \to q_j$ bringt nichts Neues, alles bleibt gleich.
- Zeile 3: $R^0_{31} = \{\}$, also kein Weg über $q_1$, alles bleibt gleich.
- Zeile 2 ($R^0_{21} = \{0\}$):

$$
\begin{aligned}
R^1_{21} &= \{0\} \cup \{0\}\{\varepsilon\}\{\varepsilon\} = \{0\} \\
R^1_{22} &= \{\varepsilon\} \cup \{0\}\{\varepsilon\}\{0\} = \{\varepsilon, 00\} \\
R^1_{23} &= \{1\} \cup \{0\}\{\varepsilon\}\{1\} = \{1, 01\}
\end{aligned}
$$

###### Schritt 3: $k=2$ ($q_2$ darf Zwischenstation sein)

Hilfsfakten:

$$
(R^1_{22})^* = \{\varepsilon,00\}^* = \{00\}^*, \qquad \{00\}^*\cdot\{\varepsilon,00\} = \{00\}^*, \qquad \{00\}^*\{1,01\} = \{0\}^*\{1\}
$$

$$
\begin{aligned}
R^2_{11} &= \{\varepsilon\} \cup \{0\}\{00\}^*\{0\} = \{00\}^* \\
R^2_{12} &= \{0\} \cup \{0\}\{00\}^*\{\varepsilon,00\} = \{0\}\{00\}^* \\
R^2_{13} &= \{1\} \cup \{0\}\{00\}^*\{1,01\} = \{0\}^*\{1\} \\[4pt]
R^2_{21} &= \{0\} \cup \{\varepsilon,00\}\{00\}^*\{0\} = \{0\}\{00\}^* \\
R^2_{22} &= \{\varepsilon,00\} \cup \{\varepsilon,00\}\{00\}^*\{\varepsilon,00\} = \{00\}^* \\
R^2_{23} &= \{1,01\} \cup \{\varepsilon,00\}\{00\}^*\{1,01\} = \{0\}^*\{1\} \\[4pt]
R^2_{31} &= \{\} \cup \{0,1\}\{00\}^*\{0\} = \{0,1\}\{00\}^*\{0\} \\
R^2_{32} &= \{0,1\} \cup \{0,1\}\{00\}^*\{\varepsilon,00\} = \{0,1\}\{00\}^* \\
R^2_{33} &= \{\varepsilon\} \cup \{0,1\}\{00\}^*\{1,01\} = \{\varepsilon\} \cup \{0,1\}\{0\}^*\{1\}
\end{aligned}
$$


#### Minimalautomat
![[Pasted image 20261112125616.png]]

#### Minimierungsalgorithmus von Brzozowski

![[Pasted image 20261112125641.png]]


#### Abschlusseigenschaften regulärer Sprachen
![[Pasted image 20261112125701.png]]

#### Homomorphismus

Seien $\Sigma$ und $\Gamma$ zwei Alphabete. 

Homomorphismus: $h: \Sigma\to\Gamma^*$
Induktive Erweiterung auf Wörter über $\Sigma$

1. $h(\varepsilon) = \varepsilon$
2. $h(wa) = h(w)h(a)$ $\forall w\in\Sigma^*    \text{und } a\in\Sigma$

Anwendung von h auf jedes Wort der Sprache L:

$$
h(L) = \{h(w) | w \in L\}
$$

![[Pasted image 20261112130244.png]]



#### Entscheidungsprobleme

![[Pasted image 20261112130315.png]]



#### Grenzen der Regularität
![[Pasted image 20261112130336.png]]


#### Schubfachprinzip

kennt man aus ADM
![[Pasted image 20261112130403.png]]



#### Pumping Lemma

(Unendliche) Reguläre Sprachen haben eine spzeielle Eigenschaft. 
Jedes Wort aber iener bestimmten Länge kann "aufgepumpt" werden, dh jedes solche Wort enthält ein Teilstück, das beliebig oft wiederholt werden kann wobei die resultierenden Wörter noch immer in derselben Sprache liegen.

>[!Pumping Lemma für reguläre Sprachen]
>Sei L eine unendliche reguläre Sprache. Dann **gibt es** eine (nur von L abhängige) Schranke m > 0 so, dass **jedes** Wort $w \in L$ mit  $|w| \geq m$ Wörter x,y,z so **exisitieren**, dass:
> 
> $w = xyz \text{ mit } |xy|\leq m \text{ und } |y|>0$
> 
> sowie
> 
> $w_{i} = xy^iz \in L$          $\forall i \geq 0$


##### Beispiel

![[Pasted image 20261112130954.png]]



---

### Grammatiken

### Kontextfreie Grammatiken und Sprachen

### Jenseits der Kontextfreiheit 

### Chomsky Hierarchie


# TODO 
- [x] Turingmaschinen hier machen und verstehen ✅ 2026-11-09
- [x] 📅 2026-11-09 VO schöner nacharbeiten, statt stumpf abzuschreiben ✅ 2026-11-09




