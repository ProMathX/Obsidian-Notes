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
7.10 
kurze WH
Was ist ein Problem? 
Ein Problem ist eine abzählbar unendliche INstanzen und eine Frage

Mathematik lässt sich nie im echten Leben anwenden! 

Modell für Algorithmen:
Eine einfache imperative Programmiersprache SIMPLE

13:19 das mit dem Entscheidungsproblem die Defintionition hinschreiben

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
	- *false* falss das PRogramm $\Pi$ auf Input I 

![[Pasted image 20261008110058.png]]



---
### Semi-Entscheidbarkeit

## Offene Fragen 
- [x] Totale Partielle Funktion anschauen
 - [ ] ⏫ ➕ 2026-10-06 Beweisführung Tuwel





#### Links
- [[Learn Lean]]
