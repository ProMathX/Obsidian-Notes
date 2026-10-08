---
topic: "Teil 1: Einführung in Berechenbarkeit und Entscheidbarkeit"
date: 2026-03-16
course: ThIf
tags:
  - studies
  - "#Berechenbarkeit"
  - "#ThIf"
---
## VO
Anmerkung, 
Teil 1: 26.10 
Teil 2/3: 22.11
Teil 4: 13.12
Teil 5 6.1
	Abgabe für die Übungen

### Probleme, Programme,Algorithmen

#### Probleme
Defintion von einem Problem, begriffe müssen exakt definiert werden. Ein Problem definiert druch eine (abzählbare) unendliche Menge von möglichen Instanzen (Inputs) zusammen mit einer Frage.

#### Entscheidungsproblem 
Ein Problem mit Ja/Nein als antwort

Bsp.
![[Pasted image 20261005124357.png]]
Ein Entscheidungsproblem

- Funktionsproblem (Was ist der Funktionswert an der Stell e)
- Optimierungproblem berechne den optimalen Wert von den Lösungen (minimum oder maximum als Optimum) (Was ist der kürzest mögliche Distanz im Grpahen bspw)

- Suchproblem: gib mir eine mögliche Lösung (gib mir einen Pfad nach u nach v)
- Aufzählpoblem: berechne alle Lösgunen (gib mir alle zylklenfreien pfade nach u nach v )
- Zählprobleme: Wie viele unterschiedliche Lösungen gibt es für die Probleme 

Bereich Komplexität-> Entscheidungsprobleme

Ein Lösungsverfahren muss auf beliebige Instaanzen anwendbar für das Problem sein

#### Algorithmen
Lösen für ein Problem:
![[Pasted image 20261005125122.png]]

Jede einzelne Instanz ist endlich! Man hat keine Beschränkung aber! Ein Algorithmus muss eine enldiche Instanz in endlich vielen Schritten ja oder nein wiedergeben

#### Berechenbarkeitstheorie
Welche Probleme kann man ein Programm(Algorithmus) schreiben? 

Vor allem: Was ist wenn wir kein Problem schreiben können? Bin ich zu blöd dafür, oder ist das Problem nicht algorithmisch lösbar? 

Unsere Aufgaben: Mathematisch beweisen,dass ich nicht blöd dafür bin ein Algo zu finden

#### Programme
![[Pasted image 20261005125730.png]]

Zweiter Teil: Beweis mit Turin-Maschinen

![[Pasted image 20261005130050.png]]

### Berechenbarkeit, Entscheidbarkeit

![[Pasted image 20261005130447.png]]
$\Sigma^*$ endliche Strings über diesem Alphabet
##### Entscheidbarkeit
Wann ist ein Entscheidungsproblem entscheidbar? 
![[Pasted image 20261005131233.png]]

##### Partielle vs. Totale Funktionen
![[Pasted image 20261005131432.png]]

Wenn man ein Lösungsverfahren ein Algo suchen, dann eine 

totale Funktion es gibt immer lösung, bei partieller funktion bei bestimmten input lösung, sonst keine Lösung 

##### Existenz von unenstscheibaren Problemen
![[Pasted image 20261006120958.png]]

Entscheidungprobleme entsprechen $\Sigma^* \to \{0,1\}$

![[Pasted image 20261005132317.png]]

-  ==Es gibt nur abzählbar unendlich viele Strings über unserem Alphabet, es gibt abzählbar viele Programme die wir schreiben können==
- ==Es gibt überabzählbar viele Funktionen für die wir Programme schreiben wollen -> es gibt funktionen für die es keine Programme gibt==

	Anmerkung: es hat gottlos lange gedauert es zu checken, bist du behindert, Menge der Funktionen $\Sigma^* \to \{0,1\}$ ist die Menge der Entscheidungsprobleme. Jedes Element dieser Menge ist eine Funktion und somit ein Entscheidungsproblenm. 


Ab hier beweist man die Existenz von unentscheidbaren Problemen

Das heißt es gilt zu zeigen:
 - $g: \Sigma^* \to \mathbb{N}$  Also $\Sigma^*$ ist abzählbar unendlich, somit kann ich jedem aus unserem Alphabet unendlich viele Wörter schreiben
 - $\mathbb{N} \to \{0,1\}$ wir haben unabzählbar viele funktionen für die wir ein Programm schreiben wollen

![[Pasted image 20261005132542.png]]

Beweis der Abzählbarkeit:
- [[ThInf-Teil1.pdf#page=18&selection=0,0,2,1|ThInf-Teil1, page 18]]
Wichtig ist injektivität, surjektivit ist zweitrangig
Und für die Überabzählbarkeit Cantors drittes Diagonalargument
Man kann es durch eine rekursive Funktion definieren

die problemstellung ist halt so (Ergänzung 13:39)
Ergänzung

![[Pasted image 20261006120153.png]]

![[Pasted image 20261006120159.png]]

---
<br>

7.10 
kurze WH
Was ist ein Problem? 
Ein Problem ist eine abzählbar unendliche INstanzen und eine Frage

Mathematik lässt sich nie im echten Leben anwenden! 

Modell für Algorithmen:
Eine einfache imperative Programmiersprache SIMPLE

13:19 das mit dem Entscheidungsproblem die Defintionition hinschreiben

- Was ist ein Problem
	- Für eine abzählbar unendliche Menge an Instanzen und eine Frage 
		- Wenn eine Frage ein ja nein als Antwort erwartet *Entscheidungsproblem*

Warum unendliche Menge von Instanzen? 
- Wenn man ein Lösungsverfahren sucht, sollte dieses Lösungsverfahren gründstzlich für beliebige Instnazen anwendbar sein

Wann ist ein Entscheidungsproblem entscheidbar? 

Ein Problem ist entscheidbar wenn es einen Algorithmus gibt, mit bestimmten Eigenschaften gibt
Dieser Algo kann beliebige Instanzen nehmen, terminiert garantiert und liefert ein Ergebnis.

Abstraktes Argument war, das man nur abzähöbar viele Programme schrieben, aber dafür gibt es überabzähöbar viele Probleme

Einwurf:
Weil $\{0,1\}^{\mathbb{N}} \equiv f: \mathbb{N} \to \{0,1\}$ die Menge unserer Entscheidungen, somit Probleme, somit Algorithmen sind. Wenn diese Menge überabzähöbar ist, somit überabzählbar viele Probleme und somit überabzähöbar viele Algorithmen!


Einem Studierenden ist aufgefallen, dass was einem bringt eine Funktion aus den natürlichen Zahlen nach {0,1} die ich nicht beschreiben kann
Wenn ich aber eine funktion beschreiben muss, dann brauche ich ja ein alphabet, welches ja endlich ist

Entscheidungsproblem ist eine Funktion $\Sigma^* \to \{0,1\}$ dann gibt es überabzählbar viele dasvon, wenn man es  komunizieren kann , dann überabzählbar viele


<br>

---
### Probleme über Programme
##### Goldbachsche Vermutung 
>[!Vermutung]
>Jede gerade Zahl größer als 2 ist die Summe von 2 Primzahlen

```SIMPLE
Boolean test(Integer n)
	for all i <= n, j <= n do
	{
		if(isPrime(i) and isPrime(j) and i + j = n)
			then return true;
	}
	return false;
	
Void testConjecture()
		n:= 4;
		while test(n) = true 
			do 
			{
				n := n+2;
			}
```

>[!Theorem]
>Die Goldbache Vermutung ist wahr <=> testConjecture() terminiert nicht.

Das hier ist eine Aufarbeitung der Folien von 19-40

----
Es gibt viele natürliche Probleme, für die ein Algorithmus nicht offensichtlich ist

Um dies zu veranschaulichen sagen wir ein Programm $\Pi$ und ein Input $I$, die konkrete Frage ist:
- tritt das Programm $\Pi$ in eine Endlosschleife? 
- Und terminiert es auf allen Inputs? 

Würde nman es verallgemeinern können, können wir damit die Korrektheit von Programmen sicherstellen

Man könnte auch die Mathematische Probleme Algorithmisch beweisen, siehe oben, die [[#Goldbachsche Vermutung]]

---
##### Versuch eines computergestützten Beweises
- Angenommen wir haben ein Programm $\Pi_{h}$ was über die Termination entscheidet, welches als Signatur, $\Pi_{h}(\Pi,String I)$ hat.
- Dann kann man auf $\Pi_{h}$ das Programm testConjecture also $\Pi$ überprüfen lassen.
- Falls $\Pi_h$ 
	- Ja ausgibt, Vermutung bewiesen
	- Nein, Vermutung widerlegt

---
##### Unentscheidbarkeit des Halteproblems

Das Halteproblem ist das Problem der Informatik, die Fragestellung ist recht banal

>[!Halteproblem]
>Instanz: (Quellcode) Program $\Pi$, Input Stirng $I$
>
>Frage: Terminiert das Programm $\Pi$ auf Input String $I$?

Wie kann man aber beweisen, dass keinen Algorithmus $\Pi_{h}$ gibt? ($\Pi_{h}$ entscheidet ja über das Halteproblem)

Der Beweis ist indirekt, dh:
- Annahme dass es ein Programm $\Pi_{h}$ gibt, welches Entscheidbar ist und man muss zeigen, dass es zu einem Widerspruch führt
- Die Annahme ist, dass das Programm $\Pi$ als String gegeben ist und somit als Input gelesen werden kann
- Der Beweis ist erneut ein *Diagnoalargument*:
	  Also es ist ein "rekursiver" Ansatz, d.h $\Pi(\Pi)$

###### Schritt 1

- $\Pi_{h}$ nimmt 2 Strings als Input:
	- $\Pi$  Quellcode eines Simple Programms
	- $I$ (Input  für Programm $\Pi$)

- Return value von $\Pi_{h}$
	- *true* falls das Programm $\Pi$ auf Input $I$ _terminiert_
	- *false* falss das PRogramm $\Pi$ auf Input I _nicht terminiert_

![[Pasted image 20261008110058.png]]

###### Schritt 2
Mit Hilfe von $\Pi_{h}$ erzeugen wir nun ein Programm $\Pi_h'$
- $\Pi_h'$ nimmt als Input einen String und dupliziert diesen und ruft damit $\Pi_h$ auf

$\Pi_h'$ überprüft, ob ein Progframm $\Pi$ terminiert, wenn es seinen eigenen Quellcode als Input nimmt!
![[Pasted image 20261008111009.png]]

###### Schritt 3
$\Pi_h'$  erzeugen wir $\Pi_h''$ 
$\Pi_h''$  geht in in eine Endlosschleife, wenn das Programm $\Pi$ auf sich selber hält $\Pi_h'$liefert *true* 

![[Pasted image 20261008111415.png]]

###### Schritt 4
Daraus folgt folgende Beobachtung:
1. Falls $\Pi$ auf seinen eigenen Input $\Pi$ hält, dann hält $\Pi_{h}''$ auf dem Input $\Pi$ nicht
2. Falls $\Pi$ auf seinen eigenen Input $\Pi$ nicht hält, dann hält $\Pi_{h}''$ auf dem Input $\Pi$

Was passiert wenn $\Pi_{h}''$ als input $\Pi_{h}''$ nimmt? 
Daraus folgen nun 2 Widersprüche!
1. $\Pi_{h}''$ hält, dann folgt aus der ersten beobachtung, $\Pi_{h}''$ nicht auf $\Pi_{h}''$ hält (*Widerspruch*)
2. $\Pi_{h}''$ hält nicht, dann folgt aus der zweiten beobachtung, $\Pi_{h}''$ hält auf dem Input $\Pi_{h}''$

Somit ist das Halteproblem unentscheidbar!


##### Weitere Beispiele für unentscheidbaren Problemen

>[!Korrektheit]
>Instanz: (Quellecode) $\Pi$ und 2 Strings $I_{1} , I_{2}$
>
>Frage: Terminiert $\Pi$ auf dem Input $I_{1}$ und liefert $I_{2}$?

Die *Korrektheit* ist unentscheidbar, weil die Beantwortung dieser Frage implizit die Fragen beantworten müsse, ob $\Pi$ auf $I_{1}$ hält. 

###### Code erreichbarkeit

>[! Erreichbarer-Code]
>Instanz: (Quellcode) von $\Pi$ ein Label (= String) $L$
>
>Frage: Gibt es einen Input $I$, sodass $\Pi$ bei Ausführung mit Input $I$ den Code auf der Programmzele mit dem Label $L$ ausführt? 

Das ist im Folgenden wichtig, Optimierungspotenzial, nie erreichbarer Code, kann gelöscht werden

Intuition: *Erreichbarer Code* ist unentscheidbar, weil es zu einem ähnlichen Problem wie das Halteproblem wird, wenn die letzte Zeile in $\Pi$ das Label $L$ bekommt

Beweis mittels **Reduktion**

---
### Semi-Entscheidbarkeit

Was ist ein Semi-Entscheibares Problem? Ein Semi-Entscheidbares Problem ist quasi die lockerung der Definition der Entscheidbarkeit

Also aus [[#Entscheidbarkeit]] wird 
![[Pasted image 20261008120556.png]]

- $\Pi$ arbeitet für alle Instanzen von $P$ korrekt 
- $\Pi$ darf auf negativen Instanzen von $P$ endlos laufen
- wenn $\Pi$ auf einer Instanz terminiert, dann muss $\Pi$ das korretkte Ergebnis (*false*) liefern
---
Anhand dieser neuen Defintion kann man Schlussfolgern, dass das Halteproblem 
*semi-entscheidbar* ist

Wie kann es aber bewiesen werden? 

Wir bauen einen Interpreter Programm $\Pi_{i}$ 
- $\Pi_{i}$  nimmt beliebige Instanzen des *Halteproblems*
- $\Pi_{i}$  analysiert $\Pi$ und simuliert $\Pi$ mit der Instanz $I$ 
- Wenn die Simulation von $\Pi$ *terminiert*, liefert $\Pi_{i}$ *true* und terminiert
- Wenn die Simulation von $\Pi$ auf $I$ *nicht terminert*, ist $\Pi_{i}$ in einer Endlosschleife

![[Pasted image 20261008121246.png]]


###### Weitere Semi entscheidbare Probleme 

Anhand dieser Erkenntniss, ist:

>[!Theorem]
>Das *Korrektheit*-Problem ist semi-entscheidbar!

Die Beweisidee ist ident zu dem mit dem Halteproblem.

Wir bauen erneut einen Interpreter $\Pi_{i}$ 
- $\Pi_{i}$  nimmt als Input $I$ eine beliebige Instanz (Quellcode von $\Pi$ und $I_{1} ,I_{2}$)
- $\Pi_{i}$ analysiert $\Pi$  und simuliert die Ausführung von $\Pi$ mit $I_1$ als Input
	- Falls es mit *Output O* terminiert, dann überprüft $\Pi_{i}$ ob $I_2$ = *O* gilt
		- Falls es gilt *true*
		- Sonst *false*
- Wenn $\Pi$  auf $I_1$ nicht terminiert , dann läuft logischerweise $\Pi_{i}$  auf dem Input $(\Pi,I)$ endlos 

Das gleiche gilt auch für *Erreichbarkeit von Code*
![[Pasted image 20261008122333.png]]

---
###### Aufzählung, Abzählbarkeit
Wenn man gemerkt haben, dass beim Interpreter $\Pi_{i}$, dass man alle Paare $(I,i)$ aufzählen können? 

Geschachtelte funktionen gehen nicht
![[Pasted image 20261008123101.png]]
Man kommt aus der 2ten schleife nie raus

Wie kann man aber das Problem verallgemeinern? 
- Wie kann man zwei Mengen $M_{1} \times M_{2}$ aufzählen? 
- Äquivalente Frage: Ist $M_{1} \times M_{2}$  abzähöbar, wenn die zwei Mengen $M_{1} M_{2}$  abzählbar unendlich sind? 

###### Abzählbarkeit
Eine Menge M heißt abzählbar falls es eine bijektive abbildung auf $\mathbb{N}$ gibt

But....how? 
- definiere bijektive Abbildung $g: \mathbb{N} \to M$ als Aufzählung
- Alternative, injektive Abbildung, $f: M \to \mathbb{N}$ 
- Aber warum geht das? 
	- Wenn es eine injektive Abbildung f gibt, dann gilt dass die Mächtigkeit von M kleiner der Natürlichen Zahlen ist ($|M| \leq |\mathbb{N}$)

Das heißt, wenn man eine Funktion f injektiv ist, definieren wir eine Abbildung
von $M \to \mathbb{N}$  names $g$

> $g: M \to \mathbb{N} mit g(a)=|\{m \in M | f(m)< f(a)\}| \forall a \in M$

---

Kurze Erinnerung was injektiv, surjektiv und bijektiv ist
_Injektiv_: Jedes Element der Zielmenge wird höchstens  einmal getroffen
- $f(a)=f(b )\implies a=b$
Man beweist es mittels Kontraposition, also indirekt:
wenn $f(b)< f(a)$ dann gilt $f(a)\not=f(b )\implies a \not= b$ 
Denn wenn eine Funktion streng monoton fallend oder steigend ist:
- $a<b \implies f(a) > f(b)$ str monoton fallend
- $a<b \implies f(a) < f(b)$ str monotn steigend

_Surjektiv_: Jedes Elemt der Zielmenge wird mindestens einmal getroffen
Seien X und Y mengen
$f: X \to Y$ eine Abbildung, dann ist f surjektiv wenn es zu jedem $y \in Y$ ein $x\in X$ gibt, mit $f(x) =y$ 
also formaler:
$$
\forall y \in Y \exists x\in X: f(x) =y
$$

Man kann es einfach mit einer $f^{-1}:Y\to X$ zeigen und die surjektivität gewährleisten 


(Wikipedia)
Für eine [endliche Menge](https://de.wikipedia.org/wiki/Endliche_Menge) $A$ ist die Mächtigkeit $|A|$ einfach die Anzahl der Elemente von $A$. Ist nun $f : A \to B$ eine surjektive Funktion zwischen endlichen Mengen, dann kann $B$ höchstens so viele Elemente wie $A$ haben, es gilt also $|B| \leq |A|$.

Für [unendliche Mengen](https://de.wikipedia.org/wiki/Unendliche_Menge) wird der Größenvergleich von Mächtigkeiten zwar mit Hilfe des Begriffs Injektion definiert, aber auch hier gilt: Ist $f : A \to B$ surjektiv, dann ist die Mächtigkeit von $B$ nicht größer als die Mächtigkeit von $A$, auch hier schreibt man dafür $|B| \leq |A|$.

---
###### Einige abzählbar unendliche Mengen
![[Pasted image 20261008130823.png]]

###### Cantor'sches Abzählprinzip  
Aufzählung von $M_{1} \times M_{2}$ mit $M_{1} = \{a_{1},a_{2},\dots\}$ und $M_{2} = \{b_{1},b_{2},\dots\}$
Durch dieses Kreuzprodukt entstehen neue Relationen
[[cantor_diagonal.gif]]

Daraus folgt![[Pasted image 20261008131142.png]]

###### Weitere semi-entscheidbare Probleme
>[!Das "Entscheidunsproblem"]
>Instanz: eine formel $\phi$ Prädikatenlogik erster Stufe
>
>Frage: Ist $\phi$ gültig? 

Prädikatenlogische Formeln erster Stude sind so definiert, dass man zuerst induktiv Terme definiert und damit dann ebenfalls induktiv Formeln: 

Terme können sein: 
- Konstantensymbole (üblicherweise a,b,c,...)
- Variablen (üblicherweise x,y,z)
- zusammengesetzte Terme $f(t_{1},\dots,t_{\alpha})$ 

![[Pasted image 20261008132732.png]]

![[Pasted image 20261008132927.png]]




---

## Offene Fragen 
- [x] Totale Partielle Funktion anschauen
 - [ ] ⏫ ➕ 2026-10-06 Beweisführung Tuwel
#### Links
- [[Learn Lean]]
