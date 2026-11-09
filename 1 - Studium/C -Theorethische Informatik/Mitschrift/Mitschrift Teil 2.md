---
topic:
date: 2026-03-16
course:
tags:
  - studies
---
# VO
Was ist das für ein süßer Vortragender?  Chris Fermüller der Goat nach Puschner? 

#### Was sollte man schon wissen? 

Was sollte man aus dem [[Mitschrift Teil 1]] schon kennen? 

- Es konkrete unentscheidbare (Entscheidungs-) Probleme (zB Halteproblem)
- Unentscheidbare Probleme sind oft semi-entscheidbar 
- Vie wichtitige Probleme sind nicht einmal semi-entscheidbar zB Programmäquivalnz, universelles Halteprobelm Korrektheit 
- Ähnliches gilt für Funktionen: Die meisten Funktionen sind unberechenbar ($\to$ Diagonalverfahren)

### Church Turing These

#### Wie robust ist unser Berechenbarkeitsmodell? 
![[Pasted image 20261019122357.png]]

Funktionen hier  bei der Variante 1 sind gemeint von diskreten Funktionen zB $f:\mathbb{N} \to \mathbb{N}$


#### Fragen zur Church-Turing-These
- Wie kommt es zu dieser These? 
![[Pasted image 20261019123139.png]]

Ab hier ist es historie, nice fun facts und side-notes stehen dann hier


### Imperative Paradigma: Turingmaschinen und mehr

#### Die Turing Maschine
*Turing Frage:* Welche reele Zahlen sind berechenbar? 

![[Pasted image 20261019130221.png]]


Resultate der Analyse: Turingmaschinen

![[Pasted image 20261019130242.png]]

- Das Band enthält die Eingabe. Alle anderen Zellen enthalten ein *Blank-Symbol B* (Nur endlich viele Zellen sind nicht B-gefüllt)
- Lese/Schreib-Kopf ist immer über eine Bandzelle positioniert
- Rechenschritt: Ersetze das gelesene Symbol; schiebe den Lese/Schreib-Kopf eine Zelle nach links oder rechts; endet in einem neune Zustand. 
- Anfang: Kopf ist über der am weitesten links stehenden Eingabezelle.


#### Formale beschreibung von Turingmaschinen 
Eine *Turingmaschine* besteht aus 7 Komponenten:
$$M = (Q,\Sigma,\Gamma,\delta,q_{0},B,F)$$
![[Pasted image 20261019131359.png]]

#### Übergänge
Sei M hier definiert als
$$
(q,X;p,Y,D)\in \delta
$$
M liest im Zustand q auf dem Band Sybmbol X
- wechselt nun davon abhängig in den Zustand p
- überschriebt Symbol X durch Symbol Y
- bewegt den Lese/Schreibkopf nach Links(L) oder Rechts (R), je nachdem was in D steht oder S gar nicht

Beispiel für eine determinitsitsche TM
>[!Deterministische Turinmaschine]
>Eine Turingmaschien M heißt deterministisch, wenn für alle $(q,X) \in Q \times \Gamma$  höchstens ein Element $(q,X;p,Y,D)\in \delta$ exisitiert,sodass gilt $D \in {L,R,S};$ schreibt man auch $\delta(q,X) = (p,Y,D)$

Man hält/terminiert im Zustand q wenn $q \in F$, $\delta(q,X)$ bleibt undefiniert


Übetragung und Berechnung:
![[Pasted image 20261019132230.png]]

Somit, macht die obrige Erklärung, weitaus mehr Sinn als zuvor

#### Akzeptierte Sprache
![[Pasted image 20261019132421.png]]


![[Pasted image 20261019132802.png]]


Folgendes beispiel erklärt es recht gut

![[Pasted image 20261019153432.png]]

Wenn man sich an das vorherige Bild errinert, q0 ist der lese schreibkopf, er hovert über der 110B 
- (q0,1) = (q0,1,R)
- (q0,1) = (q0,1,R)
- (q0,0) = (q0,0,R)
- (q0,B) = (q1,0,S) an der Stelle B kommt eine 0, dann wechselt man zu q1
- (q1,0) = (q1,0,L)
- (q1,0) = (q1,0,L)
- (q1,1) = (q1,1,L)
- (q1,1) = (q1,1,L)
- (q1,B) = (q2,B,L)


#### Universelle Turingmaschinen
Eine TM enspricht *nicht* einem Computer, sondern einem Programm.
Um ein Modell eines Rechners/Computers zu erhaltne, benötigen wir eine Maschine, die beliebige Programme (TM) simulieren kann.

TM als Input: $<M>$ bezeichnet den Zahlencode einer Turingmaschine M

![[Pasted image 20261019153823.png]]

Darauf folgt:
>[!Achtung]
>Jede Universelle TM entspricht einem *Interpreter*

### Varianten von Turingmaschinen
![[Pasted image 20261021131041.png]]


### Registermaschinen
Ist näher an heutigen Computern. Fokus auf arithmetische Funktionen ($\mathbb{N}^k \to \mathbb{N}$)
- [Arithmetische Funktionen](https://de.wikipedia.org/wiki/Zahlentheoretische_Funktion?useskin=vector)

![[Pasted image 20261021131855.png]]

_Wichtig:_ Anders als bei TMs werden bei RM Maschine und Programme getrennt. Erst mit einem RM-Programm kann man rechnen!



#### Programme für Registermaschinen
![[Pasted image 20261021132036.png]]

^ If else strukturen

R(i)... Inhalt des i-ten registers ($R(i) \in \mathbb{N}$)
Semantik der Befehle
![[Pasted image 20261021132312.png]]
A  eines rauf
S eins runter, aber bleibt bei Null 
t ist entsprechended eine Testanweisung, test ist positiv wenn R(i) = 0

Wir betrachten nur deterministsiche Programme: Jede Kennamrke kommt nur ienmal als solche vor.


#### Berechnen mit RM-Programmen
![[Pasted image 20261021132601.png]]
13:26 prüfungsfehler leak
Sie muessen nicht unbedingt k viele genau k viele register haben wenn sie eine K stellige funktion berechnen. Im allegemeinen werden sie auch Hilfsregister brauchen oder vorsehen wollen. Sie muessen bei diesem Anfangszustand natuerlich fuer jede Zahl, die sie eingeben wollen, im Doppel, also fuer jede der K Zahlen auch ein entsprechendes Register vorsehen. Das sind eben die ersten K register, die reihenfolge ist wichtig R1 bis Rk. Das M fuer die Registermaschine, die ist so eine Funktion, kann natuerlich groesser sein. Es weiterhin fesgeleegt,dass die weiteren Register auf 0 gestzt sind, dementsprechend muss man weitere register nicht auf 0 setzen, da die Definition einer RM dies schon handhabt.





Konfigurationen:
![[Pasted image 20261021132810.png]]


Ein Additions-Programm:
![[Pasted image 20261021132827.png]]
TODO Algorithmus durchgehen



Substraktions-Programm
![[Pasted image 20261021132853.png]]

#### Partielle Funktionen / Codierung
![[Pasted image 20261021133822.png]]


#### Wichitge Fakten zu Registermaschinen
![[Pasted image 20261021134258.png]]

F ist eine berechenbare Funktion, ein Programm für alle berechenbaren Funktionen -> universellen Registermaschine

[Wikipedia zu Registermaschinen](https://de.wikipedia.org/wiki/Registermaschine?useskin=vector)
### $\lambda \text{-Kalk\"ul}$


![[Pasted image 20261021135925.png]]

Sexy gleich gecheckt

Wie rechne ich mit $\lambda - \text{Termen}$
![[Pasted image 20261021140124.png]]
![[Pasted image 20261021140135.png]]

### Currying 
![[Pasted image 20261021141815.png]]


### Auswerten durch Einsetzen: $\beta - \text{Reduktionen}$
![[Pasted image 20261021142054.png]]
![[Pasted image 20261021142110.png]]
![[Pasted image 20261021143959.png]]


Kleiner Hinweis, es gibt verschiedne arten ein und oder ode rnegation als lambda term, gibt es verschiedene Formen. Wie man es dementsprechend findet etc

Für das Programmieren siehe Folien.
> Programmieren im $\lambda - \text{{Kalkül}}$
[[Teil_2_WS2026.pdf#page=36&selection=0,0,0,13|Teil_2_WS2026, page 36]]


#### Y-Kombinator

![[Pasted image 20261028134536.png]]

![[Pasted image 20261028135123.png]]


### Rekursive Funktionen

![[Pasted image 20261028135838.png]]


Die Funkitonen können auch zusammengestzt werden, k und m können unterschiedlich voneinander sein 

Eine einfache zusammensetzung der Funktionen h und g 
![[Pasted image 20261028140744.png]]

![[Pasted image 20261028141805.png]]

![[Pasted image 20261028141815.png]]

---

![[Pasted image 20261028142428.png]]

Das genauer anschauen, dass muss man genauer schauen, vor allem die Vertauschungsoperation. Somit kann man die Defintion dementsprechend ändern. Wichtig für Prüfungen und Übungsbeispiele.

![[Pasted image 20261028142745.png]]

![[Pasted image 20261028142813.png]]

Nah es ist nicht so schlimm, mit der Hand mal rechnen und es geht


---

<br>
### Der Satz von Rice und seine Anwendung

#### Sprachen

![[Pasted image 20261104152622.png]]

##### Eigenschaften von Sprachen 
![[Pasted image 20261104152659.png]]

##### Beispiele von Sprach-Eigenschaften
![[Pasted image 20261104152724.png]]


#### Der Satz von Rice

>[!Theorem]
>Jede nicht-triviale Sprach-Eigenschaft ist unentscheidbar

Achtung, Sprachen können (un)entscheidbar sein. Eigenschaften sind aber Mengen von Sprachen. Diese können indirekt, über ihre jeweilige Darstellung als Turingmaschine, als Sprachen repräsentiert werden. 


>[!Definition]
>Für jede Eigenschaft $\varepsilon$ rekursiv aufzählbarer Sprachen sei $L_{\varepsilon} = \{\langle M\rangle| \mathfrak{L}(M) \in \varepsilon \}$, also die Menge aller Codes von jenen TMs, die eine Sprache $L \in \varepsilon akzeptieren$

Somit folgt, die (Un-)Entscheidbarkeit von $\varepsilon$ mien (Un- )Entscheidbarkeit von $L_{\varepsilon}$

![[Pasted image 20261104155233.png]]


#### Anwendung vom Satz

![[Pasted image 20261104155342.png]]

#### Intensional versus Extensional
![[Pasted image 20261104160213.png]]


#### Für Funktionen

Nicht nur Spracheigenschaften sind relevant, sondern auch die Eigenschaften berechenbarer Funktionen sind relevant.

>[!Extensionale]
>Eine (extensionale) Funktionseigenschaft ist iene Teilmenge $\mathfrak{F}$ der Turing-berechenbaren Funktionen (eines bestimmten Types). $\mathfrak{F}$ heißt trivial, wenn sie entweder leer ist oder aus allen Turing-berechenbaren Funktionen (des entsprechenden Types) besteht 

>[!Definition]
>Für jede Funktions-Eigenschaft  $\mathfrak{F}$ sei  $L_{\mathfrak{F}} = \{\langle M\rangle| \mathfrak{F}(M) \in \mathfrak{F} \}$, also die Menge aller Codes von Turing Maschinen, die iene Funktion $f  \in \mathfrak{F}$ berechnen.

>[!Theorem]
>Für jede nicht-triviale Eigenschaft $\mathfrak{F}$ von Turing-berechenbaren Funktionen ist die Sprache $L_{\mathfrak{F}}$ unentscheidbar (kurz $\mathfrak{F}$ ist unentscheidbar)


#### Anwendung auf Funktionen
![[Pasted image 20261104161620.png]]


#### Weiteres zur Anwendbarkeit des Satzes von Rice

*Beobachtung:*
Die Unentscheidbarkeit des Korrektheitprobles aus Teil 1, angewendet auf arithmetische Funktionen, folgt unmittelbar aus dem Satz von Rice. Das gilt auch für die meisten verwandten Probleme: zB das universelle Halteproblem oder das Äquivalenzproblem.

*Anmerkung*
Die Beschränkung auf Turinmaschinen als Darstellungsmittel für Spracen bzw Funktionen ist unwesentlich. Analoge Sätze gelten auch für übliche Programmiersprachen, Typ-0-Grammatiken, $\lambda$- Terme ...


>[!Achtung]
>Es ist nicht immer einfach festzustellen, ob eine Funktions- oder Sprach-Eigenschaft trivial ist. ZB ist es trivial entscheidbar, ob eine von einer TM berechnete Funktion, vom Typ $\mathbb{N}^k \to \mathbb{N}$ $\lambda$ definierbar ist. 

Die Antwort darauf ist immer ja: Jede Turing-berechenbare Funktion ist $\lambda$ definierbar. 





### Weitere unentscheidbare Probleme

Ist mehr Trivia als Stoff 
[[Teil_2_WS2026.pdf#page=71&selection=0,0,0,24|Teil_2_WS2026, page 71]]
### Unkonventionelle Berechenbarkeitmodelle

Ist mehr trivia als Stoff 
[[Teil_2_WS2026.pdf#page=76&selection=0,0,0,18|Teil_2_WS2026, page 76]]


# Teil 2: Berechenbarkeit – Kernbegriffe erklärt

---

## 2.1 Church-Turing-These

### Berechenbarkeitsmodell, Robustheit

Ein **Berechenbarkeitsmodell** legt formal fest, was ein "Rechenverfahren" ist (TM, RM, λ-Kalkül, μ-rekursive Funktionen, ...). **Robustheit** heißt: Alle vernünftigen Modelle liefern _dieselbe_ Klasse berechenbarer Funktionen bzw. entscheidbarer Probleme. Der Begriff "berechenbar" hängt also nicht vom gewählten Modell ab.

### Church-Turing-These (Varianten)

Die These ist **nicht beweisbar**, weil "informell berechenbar" kein formaler Begriff ist. Sie wird durch die Äquivalenz aller bekannten Modelle gestützt.

|Variante|Aussage|
|---|---|
|1 (Turing)|Was in irgendeinem konkreten Sinn berechenbar ist, ist auch auf einer **TM** berechenbar.|
|2 (Turing)|Gibt es ein endlich beschreibbares Verfahren zur Spezifikation einer Sprache $L$, dann gibt es eine **TM**, die $L$ akzeptiert. (Begründet die Begriffe _semi-entscheidbar_ und _entscheidbar_.)|
|3 (Shepherdson & Sturgis)|Informell berechenbare arithmetische Funktionen sind auf einer **Registermaschine** berechenbar.|
|4 (Church)|Informell berechenbare arithmetische Funktionen sind **λ-definierbar**.|
|5 (Gödel/Kleene/Church/Péter)|Informell berechenbar = **partiell rekursiv**.|

### Charakteristische Funktion

Für eine Sprache $L \subseteq \Sigma$ ist 
$$\chi_L : \Sigma^* \to \{0,1\}, \qquad \chi_L(w) = \begin{cases} 1 & w \in L \\ 0 & w \notin L \end{cases}$$`
Damit lassen sich Sprachen in Funktionen übersetzen. Umgekehrt sind Funktionen $\mathbb{N}^k \to \mathbb{N}^m$ Mengen von Tupelpaaren, also als Sprachen darstellbar. **$L$ entscheidbar $\iff$ $\chi_L$ total berechenbar.**

### Paradigmen

- **Imperativ:** TM $\to$ SIMPLE $\to$ Java, C, ...
- **Funktional/deklarativ:** λ-Kalkül $\to$ ML, Haskell, ...

---

## 2.2 Turingmaschinen und Registermaschinen

### Turingmaschine (TM)

$$M = (Q, \Sigma, \Gamma, \delta, q_0, B, F)$$

- $Q$: endliche Menge von **Zuständen**
- $\Sigma$: **Eingabealphabet**
- $\Gamma$: **Bandalphabet**, $\Sigma \subsetneq \Gamma$
- $\delta : Q \times \Gamma \to Q \times \Gamma \times {L,R,S}$: **Übergangsfunktion**
- $q_0 \in Q$: **Startzustand**
- $B \in \Gamma \setminus \Sigma$: **Blank-Symbol**
- $F \subseteq Q$: **Endzustände**

Das Band ist beidseitig unendlich, nur endlich viele Zellen sind nicht $B$. Der Kopf steht anfangs auf dem linken Ende der Eingabe.

### Deterministische TM

Für jedes $(q,X) \in Q \times \Gamma$ gibt es **höchstens einen** Übergang $(q,X;p,Y,D) \in \delta$. Man schreibt $\delta(q,X) = (p,Y,D)$.

Bedeutung von $(q,X;p,Y,D)$: Im Zustand $q$ wird $X$ gelesen, dann wird in Zustand $p$ gewechselt, $X$ durch $Y$ überschrieben und der Kopf bewegt sich nach links ($L$), rechts ($R$) oder bleibt ($S$).

### Konfiguration, Übergang

Eine **Konfiguration** ist eine Momentaufnahme der Rechnung: $$X_1 X_2 \dots X_{i-1}, q, X_i X_{i+1} \dots X_n$$ Die TM ist im Zustand $q$, der Kopf steht über $X_i$, links von $X_1$ und rechts von $X_n$ stehen nur Blanks.

- $\Rightarrow$: **ein** Rechenschritt
- $\Rightarrow^*$: beliebig viele (auch null) Schritte

Beispiele für $\delta(q,X_i) = (p,Y,D)$:

- $D = L$: $\dots X_{i-1}, q, X_i \dots \Rightarrow \dots p, X_{i-1}, Y \dots$
- $D = R$: $\dots X_{i-1}, q, X_i \dots \Rightarrow \dots X_{i-1}, Y, p \dots$
- $D = S$: $\dots X_{i-1}, q, X_i \dots \Rightarrow \dots X_{i-1}, p, Y \dots$

(Merkregel: Der Zustand steht immer _links_ von dem Symbol, auf das der Kopf zeigt.)

### Haltende / terminierende TM

$M$ **hält**, wenn sie in einen Zustand $q \in F$ gelangt (dort ist $\delta$ undefiniert). Eine TM kann auch **nie** halten (Endlosschleife) oder in einem Nicht-Endzustand ohne passenden Übergang stehen bleiben.

### Akzeptierte Sprache

$$\mathcal{L}(M) = { w \in \Sigma^* \mid q_0 w \Rightarrow^* \alpha, p, \beta,\ p \in F,\ \alpha,\beta \in \Gamma^* }$$ Das sind genau die Wörter, bei deren Eingabe $M$ **terminiert**.

### Rekursiv aufzählbar (= semi-entscheidbar)

$L$ ist **rekursiv aufzählbar (r.e.)**, wenn eine TM $M$ mit $\mathcal{L}(M) = L$ existiert.

- Bei $w \in L$ hält $M$.
- Bei $w \notin L$ darf $M$ **ewig laufen**.

Beispiel: Halteproblem.

### Rekursiv (= entscheidbar)

$L$ ist **rekursiv**, wenn eine TM existiert, die **immer hält** und für jedes $w$ angibt, ob $w \in L$ oder $w \notin L$ (z.B. durch zwei verschiedene Endzustände).

Zusammenhang: $$\text{rekursiv} \subsetneq \text{rekursiv aufzählbar}$$ $L$ ist rekursiv $\iff$ $L$ und $\overline{L}$ sind r.e.

### Turing-Berechenbarkeit

Für arithmetische Funktionen $f : \mathbb{N}^k \to \mathbb{N}$ ($[n]_2$ = Binärdarstellung von $n$):

- **Anfangskonfiguration** für $(n_1,\dots,n_k)$: $; q_0,[n_1]_2, B \dots B, [n_k]_2$
- **Endkonfiguration**: $; x, p, [n]_2, B, y$ mit $p \in F$ ("$M$ gibt $n$ aus")

$M$ **berechnet** $f$, geschrieben $F(M) = f$, wenn $M$ bei Eingabe $(n_1,\dots,n_k)$ den Wert $f(n_1,\dots,n_k)$ ausgibt. Ist $f(n_1,\dots,n_k)$ **undefiniert**, hält $M$ **nicht**.

$f$ heißt **Turing-berechenbar**, wenn es eine TM $M$ mit $F(M) = f$ gibt.

> Dieselbe TM kann je nach Stelligkeit der Eingabe verschiedene Funktionen berechnen (Folie 18: $f_1(n) = 2n$ auf einer Zahl, eine andere Funktion auf zwei Zahlen).

### Code $\langle M \rangle$, universelle TM

$\langle M \rangle$ ist der **Zahlencode** einer TM $M$. Eine TM $U$ heißt **universell**, wenn für jede TM $M$ und alle Eingaben gilt: $$F(U)(\langle M\rangle, n_1,\dots,n_k) = F(M)(n_1,\dots,n_k)$$ Eine TM entspricht einem **Programm**, eine universelle TM einem **Interpreter** (bzw. dem Computer, der Programme ausführen kann). Turing hat 1936 gezeigt, dass es universelle TMs gibt.

### Berechnungsäquivalenz, Simulation/Reduktion

Zwei Modelle sind **berechnungsäquivalent**, wenn sie dieselben Funktionen berechnen bzw. dieselben Sprachen akzeptieren. Bewiesen wird das jeweils durch **Simulation** (Reduktion): Modell A kann Modell B nachbauen und umgekehrt.

TM-Varianten, die alle äquivalent zur Standard-TM sind: Mehrband-TM, Mehrkopf-TM, separates Eingabeband, binäres/unäres Eingabealphabet, nichtdeterministische TM (lässt sich determinisieren).

### Registermaschine (RM)

Eine $m$-RM ist $R = (S, \mathbf{O}, \mathbf{T})$:

- $S = \mathbb{N}^m$: **Speicherzustände** (Inhalt der $m$ Register)
- $\mathbf{O} = {A_i} \cup {S_i}$: **Speicherbefehle**
- $\mathbf{T} = {t_i}$: **Testbefehle**

Semantik ($R(i)$ = Inhalt von Register $i$):

- $A_i$: $R(i) := R(i) + 1$
- $S_i$: $R(i) := R(i) \mathbin{\dot-} 1$ (bleibt bei 0 stehen)
- $t_i$: Test, ob $R(i) = 0$

**Wichtig:** Bei RMs sind Maschine und **Programm getrennt**.

### RM-Programm

Startmarke $a \in \mathbb{N}$ plus endliche Menge von Anweisungen:

- **Funktionsanweisung** $(r, f, p)$: "`r`: do $f$ then goto $p$"
- **Testanweisung** $(r, t, p, q)$: "`r`: if $t$ then goto $p$ else goto $q$"

$r$ = **Kennmarke**, $p,q$ = **Sprungmarken**, Sprungmarken ohne zugehörige Kennmarke = **Endmarken** (hier hält das Programm). Deterministisch: jede Kennmarke kommt nur einmal vor.

**Berechnung von $f : \mathbb{N}^k \to \mathbb{N}$:** Anfangs $R(i) = n_i$ für $1 \le i \le k$, alle übrigen Register $0$. Ergebnis: $R(1)$ bei Erreichen einer Endmarke. Konfiguration: $p:(n_1,\dots,n_m)$.

Beispiel Addition: $$\mathrm{ADD} = (0, {(0,t_2,5,1),\ (1,S_2,2),\ (2,A_1,0)})$$ Solange $R(2) \ne 0$: $R(2)$ um 1 senken, $R(1)$ um 1 erhöhen. Ende bei Endmarke 5.

### Universelles RM-Programm

Es gibt ein RM-Programm $P_U$ mit $u(\langle F\rangle, n_1,\dots,n_k) = f(n_1,\dots,n_k)$ für jedes RM-Programm $F$, das $f$ berechnet. RMs und TMs sind berechnungsäquivalent. Schon **2-RMs** sind (mit geeigneter Codierung) universell. Codierung von Tupeln über Primfaktorzerlegung: $\langle n_1,\dots,n_m\rangle \mapsto 2^{n_1} \cdot 3^{n_2} \cdots p_m^{n_m}$.

---

## 2.3 λ-Kalkül

### λ-Term

Induktiv definiert:

1. Jede **Variable** $x$ ist ein λ-Term.
2. **Anwendung (Applikation):** Sind $M, N$ λ-Terme, dann ist $(MN)$ einer.
3. **Abstraktion:** Ist $x$ Variable und $M$ ein λ-Term, dann ist $(\lambda x.M)$ einer. $M$ ist der **Body**.

BNF: `<lterm> ::= <var> | (<lterm><lterm>) | (λ <var>.<lterm>)`

Schreibkonventionen:

- Äußere Klammern weglassen
- **Linksassoziativ:** $MNL = (MN)L$
- Der Body reicht so weit nach rechts wie möglich: $\lambda x.MN = \lambda x.(MN)$
- $\lambda xyz.M$ statt $\lambda x.\lambda y.\lambda z.M$

Idee: $\lambda x., x + 1$ ist die Funktion $x \mapsto x+1$ selbst (nicht ihr Ergebnis).

### Freie vs. gebundene Variablen, Kombinator

$$\begin{aligned} FV(x) &= {x} & GV(x) &= {} \ FV(MN) &= FV(M) \cup FV(N) & GV(MN) &= GV(M) \cup GV(N) \ FV(\lambda x.M) &= FV(M) \setminus {x} & GV(\lambda x.M) &= GV(M) \cup {x} \end{aligned}$$ Ein **Kombinator** ist ein λ-Term **ohne freie Variablen**.

### Currying

Eine mehrstellige Funktion wird als Kette einstelliger Funktionen dargestellt: $$f : A_1 \times \dots \times A_n \to B \quad\leadsto\quad f_{curried} : A_1 \to (A_2 \to (\dots (A_n \to B)))$$ Beispiel: $\lambda mn., m+n$ ist $\lambda m.(\lambda n., m+n)$; $\lambda n., m+n$ ist die Funktion "$+m$". Teilweise Anwendung ist damit möglich.

### α-Reduktion

Umbenennung **gebundener** Variablen: $\lambda x.x =_\alpha \lambda y.y$. Dabei dürfen keine freien Variablen gebunden werden.

### Substitution

$M[N/x]$ = ersetze alle **freien** Vorkommen von $x$ in $M$ durch $N$. Vorsicht bei Namenskollisionen: Ist $y \in FV(N)$ und steht $\lambda y$ im Weg, muss vorher mit $\alpha$ umbenannt werden.

### β-Reduktion, Redex, Normalform

- **Redex:** ein Teilterm der Form $(\lambda x.M)N$
- **β-Reduktion:** $(\lambda x.M)N \to_\beta M[N/x]$
- **Normalform:** ein Term **ohne Redex**. Sie entspricht dem Rechenergebnis.

Beobachtungen: Reduktion kann neue Redexe erzeugen oder Redexe verschwinden lassen. Die Anzahl der Schritte hängt von der Reduktionsstrategie (Redex-Wahl) ab.

Nicht jeder Term hat eine Normalform: $$(\lambda x.xx)(\lambda x.xx) \to_\beta (\lambda x.xx)(\lambda x.xx) \to_\beta \dots$$

### Church-Rosser-Theorem (Konfluenz)

Hat ein Term eine Normalform, ist sie **eindeutig** (bis auf α-Umbenennung): Jede terminierende Reduktionsreihenfolge führt zum selben Ergebnis.

### Church-Numerale

Zahl $n$ = $n$-fache Anwendung von $f$: $$0 = \lambda fx.x, \quad 1 = \lambda fx.fx, \quad 2 = \lambda fx.f(fx), \quad 3 = \lambda fx.f(f(fx)), \dots$$ $$\mathbf{succ} = \lambda nfx.f(nfx), \quad \mathbf{add} = \lambda mnfx.mf(nfx), \quad \mathbf{mult} = \lambda mnf.m(nf)$$ Grundlage von $\mathbf{add}$: $f^{(m)} \circ f^{(n)} = f^{(m+n)}$.

Booleans: $\mathbf{T} = \lambda xy.x$, $\mathbf{F} = \lambda xy.y$, $\mathbf{if\_then\_else} = \lambda pxy.pxy$.

### β-Äquivalenz

$M =_\beta M'$, wenn $M$ durch endlich viele β-Reduktionen, **auch inverse** (Rückwärtsschritte), in $M'$ überführt werden kann.

### Fixpunkt, Fixpunkt-Satz

$N$ ist **Fixpunkt** von $F$, wenn $$F N =_\beta N$$

> **Fixpunkt-Satz:** Jeder λ-Term hat einen Fixpunkt.

### Y-Kombinator (Fixpunkt-Generator)

$$\mathbf{Y} = \lambda f.,(\lambda x., f(xx))(\lambda x., f(xx))$$ Für jeden Term $N$ gilt $\mathbf{Y}N =_\beta N(\mathbf{Y}N)$, also ist $\mathbf{Y}N$ ein Fixpunkt von $N$. Das beweist den Fixpunkt-Satz.

Nachrechnen: $$\mathbf{Y}N \to_\beta (\lambda x.N(xx))(\lambda x.N(xx)) \to_\beta N\big((\lambda x.N(xx))(\lambda x.N(xx))\big) =_\beta N(\mathbf{Y}N)$$

**Bedeutung:** Damit lassen sich beliebige **Rekursionen** im λ-Kalkül darstellen, obwohl λ-Terme keine Namen für Funktionen haben. Man schreibt die rekursive Funktion als Term, der sich selbst als Parameter $f$ bekommt, und $\mathbf{Y}$ liefert den Selbstbezug.

### λ-definierbar

Eine arithmetische Funktion ist **λ-definierbar**, wenn sie sich (über Church-Numerale) als λ-Term darstellen und im λ-Kalkül berechnen lässt.

> **Theorem (Turing 1936):** $f$ ist λ-definierbar $\iff$ $f$ ist Turing-berechenbar.

Das zeigt, dass zwei völlig verschiedene Paradigmen gleich ausdrucksstark sind.

---

## 2.4 Rekursive Funktionen

Idee: Man startet mit offensichtlich berechenbaren **Grundfunktionen** und baut mit wenigen **Operatoren** neue Funktionen. Funktionsausdrücke sind **variablenfrei**.

### Grundfunktionen

- **Konstante:** $C^k_n(x_1,\dots,x_k) = n$
- **Nachfolger:** $S(x) = x+1$
- **Projektion:** $P^k_i(x_1,\dots,x_k) = x_i$, $1 \le i \le k$

### Komposition ($\circ$)

Für $h : \mathbb{N}^m \to \mathbb{N}$ und $g_i : \mathbb{N}^k \to \mathbb{N}$: $$f = h \circ (g_1,\dots,g_m), \qquad f(\vec x) = h(g_1(\vec x),\dots,g_m(\vec x))$$ Beispiel: $S \circ P^2_2\ (f(x,y) = y+1)$. Links-assoziativ.

### Primitive Rekursion ($\mathbf{Pr}$)

Für $g : \mathbb{N}^k \to \mathbb{N}$ und $h : \mathbb{N}^{k+2} \to \mathbb{N}$ ist $f = \mathbf{Pr}(g,h) : \mathbb{N}^{k+1} \to \mathbb{N}$ definiert durch $$\begin{aligned} f(0, \vec x) &= g(\vec x) \ f(m+1, \vec x) &= h(m,\ f(m,\vec x),\ \vec x) \end{aligned}$$ $g$ = **Anfang**, $h$ = **Übergang** (kennt Rekursionstiefe $m$, den bisherigen Wert und die Parameter).

Beispiel Addition: $\mathrm{Add} = \mathbf{Pr}(P^1_1,\ S \circ P^3_2)$ $$\mathrm{Add}(0,5) = P^1_1(5) = 5, \quad \mathrm{Add}(1,5) = S \circ P^3_2(0,5,5) = S(5) = 6, \dots$$ (Hier greift $P^3_2$ auf das _zweite_ Argument zu, den bisherigen Funktionswert.)

### Primitiv-rekursive Funktionen

Alle Funktionen, die man aus Grundfunktionen mit $\circ$ und $\mathbf{Pr}$ definieren kann. Beispiele: Add, Mult, Fact, APred (abgeschnittener Vorgänger), Signum, ASub (abgeschnittene Subtraktion). Sie sind alle **total**.

### Minimierung ($\mu_0$, $\bar\mu$)

Für eine **totale** Funktion $g : \mathbb{N}^{k+1} \to \mathbb{N}$: $$(\mu_0 g)(x_1,\dots,x_k) = \min_{y \ge 0},[, g(y,x_1,\dots,x_k) = 0,]$$ $$(\bar\mu g)(x_1,\dots,x_{k+1}) = \min_{y \ge 0},[, g(y,x_2,\dots,x_{k+1}) = x_1,]$$ Das ist die **unbeschränkte Suche** (wie eine `while`-Schleife). Existiert kein solches $y$, ist das Ergebnis **undefiniert** (die Suche terminiert nicht).

Beispiele: $\mu \mathrm{Add} =$ echte Subtraktion (undefiniert für $m<n$), $\mu\mathrm{Mult} =$ echte Division (undefiniert, wenn nicht teilbar).

### μ-rekursiv = partiell rekursiv

Funktionen, die aus Grundfunktionen mit $\circ$, $\mathbf{Pr}$ und $\mu_0$ (äquivalent $\bar\mu$) definierbar sind.

### Partielle vs. totale Funktion

- **Total:** für jede Eingabe definiert.
- **Partiell:** darf für manche Eingaben **undefiniert** sein. (Bei TMs: die TM hält dort nicht.)

Jede totale Funktion ist insbesondere auch partiell. Der Begriff "partiell" steht für "möglicherweise nicht überall definiert".

### Total rekursive Funktionen

Partiell rekursive Funktionen, die **überall definiert** sind. Sie entsprechen genau den Funktionen, die von einer **immer haltenden** TM berechnet werden.

Hierarchie: $$\text{primitiv rekursiv} \subsetneq \text{total rekursiv} \subsetneq \text{partiell rekursiv} = \text{Turing-berechenbar}$$

### Theorem von Turing, Kleene, Péter

> Jede auf einer TM berechenbare Funktion ist partiell rekursiv.

Die Gegenrichtung (jede partiell rekursive Funktion ist berechenbar) ist klar, da $\mu$ nur auf totale berechenbare Funktionen angewendet wird. Zusammen: **partiell rekursiv = Turing-berechenbar**, und das ist Church-Turing-These Variante 5.

### Cantor'sches Diagonalverfahren

Warum gibt es total berechenbare, aber nicht primitiv rekursive Funktionen?

1. Primitiv-rekursive Funktionsausdrücke lassen sich **systematisch aufzählen**: $F_0, F_1, F_2, \dots$
2. Jeder Tabelleneintrag $F_i(n)$ ist berechenbar.
3. Definiere die **Diagonale** $D(n) = F_n(n) + 1$.
4. $D$ ist **total und berechenbar**, aber $D \ne F_i$ für jedes $i$ (sie unterscheiden sich an der Stelle $i$).
5. Also ist $D$ **nicht primitiv rekursiv**.

### Ackermann-Funktion

$$\begin{aligned} \mathrm{Ack}(0,n) &= n+1 \ \mathrm{Ack}(m+1,0) &= \mathrm{Ack}(m,1) \ \mathrm{Ack}(m+1,n+1) &= \mathrm{Ack}(m,\ \mathrm{Ack}(m+1,n)) \end{aligned}$$ **Total und berechenbar, aber nicht primitiv rekursiv**, weil sie schneller wächst als jede primitiv-rekursive Funktion. Werte: $\mathrm{Ack}(1,n) = n+2$, $\mathrm{Ack}(2,n) = 2n+3$, $\mathrm{Ack}(3,n) = 2^{n+3} - 3$, $\mathrm{Ack}(4,n)$ = Zweierturm minus 3.

### Garantierte Termination erzwingt Unvollständigkeit

> Es kann keine Programmiersprache geben, in der **alle Programme terminieren** und in der **alle total berechenbaren Funktionen** ausdrückbar sind.

Begründung: Programme einer Sprache sind aufzählbar (sonst gäbe es keinen Parser/Compiler). Gäbe es so eine Sprache, würde die Diagonalisierung eine total berechenbare Funktion liefern, die in ihr nicht vorkommt. Wer Terminierung garantiert, bezahlt mit Ausdrucksstärke ($\mathbf{Pr}$ = `for`, fehlt $\mu$ = `while`).

---

## 2.5 Satz von Rice

### Ebene 1 vs. Ebene 2

- **Ebene 1 (dargestellte Objekte):** Sprachen, Funktionen, Relationen
- **Ebene 2 (Darstellungsmittel):** Grammatiken, Programme, TMs, λ-Terme

Entscheidungsprobleme beziehen sich auf Ebene 1, gefragt wird, ob es einen Entscheidungsmechanismus auf Ebene 2 gibt. Beide Ebenen strikt trennen!

### (Sprach-)Eigenschaft

Eine **Sprach-Eigenschaft** $\mathcal{E}$ ist eine Menge rekursiv aufzählbarer Sprachen. "$L$ hat die Eigenschaft" heißt $L \in \mathcal{E}$.

Beispiele: $\mathcal{E}_3 = {L \mid L \text{ endlich}}$, $\mathcal{E}_7 = {{}}$, $\mathcal{E}_{>5} = {L \mid \lvert L\rvert > 5}$.

### Trivial vs. nicht-trivial

$\mathcal{E}$ ist **trivial**, wenn $\mathcal{E} = \emptyset$ (keine r.e. Sprache hat sie) **oder** $\mathcal{E}$ = alle r.e. Sprachen (jede hat sie). Sonst **nicht-trivial**.

Nachweis der Nicht-Trivialität: Gib eine r.e. Sprache **mit** der Eigenschaft und eine **ohne** an. Beispiel $\lvert L\rvert > 5$: $L_1 = {a,a^2,\dots,a^6} \in \mathcal{E}$, $L_2 = {} \notin \mathcal{E}$.

Achtung: "trivial" heißt nicht "einfach", sondern "alle oder keine". Beispiel: "$\lambda$-definierbar zu sein" ist trivial (jede berechenbare Funktion ist es), aber das beruht auf tiefen Sätzen von Turing und Kleene.

### Extensional vs. intensional

- **Extensional:** Eigenschaft des **Dargestellten** (Sprache bzw. Funktion). Zwei TMs mit derselben Sprache/Funktion haben die Eigenschaft beide oder beide nicht.
- **Intensional:** Eigenschaft der **Darstellung** (der TM selbst, z.B. Anzahl Zustände, Bandverhalten, Laufzeitablauf).

Sprach-Eigenschaften sind per Definition extensional. Der Satz von Rice gilt **nur für extensionale** Eigenschaften.

**Test:** Nimm zwei TMs mit derselben Sprache/Funktion. Kann eine die Eigenschaft haben und die andere nicht? Dann ist sie intensional.

### Sprach-Code $L_{\mathcal{E}}$ bzw. $L_{\mathcal{F}}$

Genau genommen können nur _Sprachen_ entscheidbar sein, Eigenschaften sind aber _Mengen von Sprachen_. Deshalb betrachtet man den Sprach-Code: $$L_{\mathcal{E}} = {\langle M\rangle \mid \mathcal{L}(M) \in \mathcal{E}}, \qquad L_{\mathcal{F}} = {\langle M\rangle \mid F(M) \in \mathcal{F}}$$ Das sind alle Codes der TMs, deren Sprache bzw. berechnete Funktion die Eigenschaft hat. "$\mathcal{E}$ ist (un)entscheidbar" heißt "$L_{\mathcal{E}}$ ist (un)entscheidbar".

### Satz von Rice für Sprachen

> Für jede **nicht-triviale** Eigenschaft $\mathcal{E}$ rekursiv aufzählbarer Sprachen ist $L_{\mathcal{E}}$ **unentscheidbar**.

Kurz: _Jede nicht-triviale Sprach-Eigenschaft ist unentscheidbar._ Beispiele: "akzeptiert mehr als 5 Wörter", "akzeptiert nur endlich viele Wörter", "akzeptiert überhaupt etwas".

### Satz von Rice für Funktionen

Eine **Funktions-Eigenschaft** $\mathcal{F}$ ist eine Teilmenge der Turing-berechenbaren Funktionen (eines Typs); trivial, wenn leer oder alle.

> Für jede **nicht-triviale** Eigenschaft $\mathcal{F}$ Turing-berechenbarer Funktionen ist $L_{\mathcal{F}}$ **unentscheidbar**.

Beispiele: "berechnet die Nachfolgerfunktion", "berechnet nur totale Funktionen", "$F(M)(1) = 111$ oder $F(M)(1) = 000$". Folgerung: Korrektheitsproblem, universelles Halteproblem und Äquivalenzproblem sind (für arithmetische Funktionen) unentscheidbar.

### Nicht-Anwendbarkeit des Satzes

Rice ist **nicht anwendbar**, wenn

1. die Eigenschaft **intensional** ist (hängt von der TM, nicht von Sprache/Funktion ab), oder
2. die Eigenschaft **trivial** ist (dann ist das Problem **trivial entscheidbar**: Antwort immer "ja" bzw. immer "nein").

> **Wichtig:** "Rice nicht anwendbar" heißt **nicht** "entscheidbar". Intensionale Eigenschaften können unentscheidbar sein (z.B. "akzeptiert die TM ihren eigenen Code?"); dann braucht man einen anderen Beweis, meist eine **Reduktion vom Halteproblem**. Entscheidbar sind z.B. "hat die TM mindestens 5 Zustände?".

### Rezept für Aufgaben

1. Geht es um **Sprache/Funktion** (extensional) oder um die **TM selbst** (intensional)? Intensional $\Rightarrow$ Rice nicht anwendbar.
2. **Nicht-trivial?** Beispiel mit und ohne die Eigenschaft nennen. Trivial $\Rightarrow$ Rice nicht anwendbar, trivial entscheidbar.
3. Variante wählen: berechnete **Funktion** $\Rightarrow$ Rice für Funktionen; akzeptierte **Sprache** $\Rightarrow$ Rice für Sprachen.
4. Extensional und nicht-trivial $\Rightarrow$ **unentscheidbar**.









# Links und Tools
- https://lambdacalc.dev/


# TODO

- [x] Registermaschinen durchgehen und checken, grunpirnzip sitzt, aber die Rechnung mit der Hand durchgehen wie bei den Turingmaschinen  [completion:: 2026-10-25]
- [x] Redex machen lamda kalkulation  [completion:: 2026-10-25]
- [x] Das Rechnen mit dem lambda kalkül abschließen ✅ 2026-11-04
#### Links
- [[Learn Lean]]
