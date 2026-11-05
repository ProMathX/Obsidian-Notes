---
topic:
date: 2026-03-16
course:
tags:
  - studies
---
## VO
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

























# Links und Tools
- https://lambdacalc.dev/


# TODO

- [x] Registermaschinen durchgehen und checken, grunpirnzip sitzt, aber die Rechnung mit der Hand durchgehen wie bei den Turingmaschinen  [completion:: 2026-10-25]
- [x] Redex machen lamda kalkulation  [completion:: 2026-10-25]
- [x] Das Rechnen mit dem lambda kalkül abschließen ✅ 2026-11-04
#### Links
- [[Learn Lean]]
