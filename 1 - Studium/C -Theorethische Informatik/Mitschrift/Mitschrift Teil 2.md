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
(q,X,p,Y,D)\in \delta
$$
M liest im Zustand q auf dem Band Sybmbol X
- wechselt nun davon abhängig in den Zustand p
- überschriebt Symbol X durch Symbol Y
- bewegt den Lese/Schreibkopf nach Links(L) oder Rechts (R), je nachdem was in D steht oder S gar nicht

Beispiel für eine determinitsitsche TM
>[!Deterministische Turinmaschine]
>Eine Turingmaschien M heißt deterministisch, wenn für alle $(q,X) \in Q \times \Gamma$  höchstens ein Element $(q,X,p,Y,D)\in \delta$ exisitiert,sodass gilt $D \in {L,R,S};$ schreibt man auch $\delta(q,X) = (p,Y,D)$

Man hält/terminiert im Zustand q wenn $q \in F$, $\delta(q,X)$ bleibt undefiniert


Übetragung und Berechnung:
![[Pasted image 20261019132230.png]]

Somit, macht die obrige Erklärung, weitaus mehr Sinn als zuvor


#### Akzeptierte Sprache
![[Pasted image 20261019132421.png]]






![[Pasted image 20261019132802.png]]


YA MENYEK WAS WAR DAS FÜR EINE VORLESUNG AMK ehrlich bruder was war das.

### $\lambda \text{-Kalkül}$


#### Links
- [[Learn Lean]]
