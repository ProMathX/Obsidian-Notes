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




