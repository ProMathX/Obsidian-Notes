---
topic: Mutual Exclusion & Condition Synchronisation
date: 2026-03-16
course: OSVO
tags:
  - studies
  - Betriebssysteme
  - "#Mutex"
  - "#ConditionSynchronisation"
---
## VO
Beispiele siehe die Folien:
- [[bs03_mutex-sync.pdf#page=2&selection=58,0,59,1|bs03_mutex-sync, page 2]]

### Gemeinsame Ressourcen
BS und Prozesse sind parallel laufende Prozesse
- verwenden dieselben Daten bzw. Ressourcen (Puffer, Shared Memory, Files, Geräte)
- tauschen Daten aus und/oder interagieren

Um Prozess-Konflikte zu vermeiden, braucht man einen *disziplinierten Zugriff*, auf gemeinsame Daten und oder Ressourcen _und_ **geordnete Abarbeitung** verteilter Aktionsfolgen. 

Falls man dies misachtet:
1. Inkonsistente Daten
2. Indeterministisches Verhalten (Ereignisfolge, Werte)

### Race   Condition

Ergebnis einer Operation hängt ab vom
- zetiliche Verhalten oder
- der Reihenfolge von Operattionen oder Ereignissen

außerhalb der Kontrolle eines Prozesses 

Fehler: ein oder mehrere der möglichen Ergebnisse sind falsch, bzw führen zu falschem Verhalten. 

<br>

### Interaktion von Prozessen

Mutual Exclusion

Konsistente Datne bleiben, Bedingungsyncronisation

 - Wettstreit um Ressourcen (Competition)
 - Mutual Exclusion (Verhindern des gleichzeitigen ressourcenzugriffs und Atomizität) 
- Condition Synchronisation (Erreicher einer definierten Abfolge von Operationen, vermeiden von race conditions)


#### Mutual Excl. und Cond. Sync.
![[Pasted image 20261104112019.png]]


#### BS-Kontrollaufgaben
Was muss ein Betriebssystem gewährleisten in diesem Kontext? 

- Mutual exclusion - Datenkonsistenz
- Regelung der abfolge der Ressorucenvergabe
- Verhinderung von Deadlocks
![[Pasted image 20261104112121.png]]
- Verhinderung von Starvation
![[Pasted image 20261104112126.png]]


#### Kritischer Abschnitt
Der Kritische abschnitt (kA) ist der Moment wo zwei Prozesse in ihrem code auf einer geteilte/gemeinsame Ressource/Datenbereich zugreifen, durch lesen oder durch schrieben, je nachdem.

![[Pasted image 20261104112235.png]]



#### Mutual Exclusion

Anhand dieses Szenarios

- Ein Prozess befindet sich im kritischen Abschnitt (kA) wenn er auf eine gemeinsame Daten bzw Ressourcen zugreift
- Wechselseitiger Ausschluss (mutual exclusion): zu jedem zeitpunkt darf sich höchstens ein Prozess in seinem kritischen abschnitt befinden
- eintritt in kA muss geregelt folgen

#### Prozessstrukturen für kA
![[Pasted image 20261104112431.png]]


#### Anforderungen für kA Lösungen

Wie soll eine Lösung ausschauen? 

- Mutual Exclusion
- Progess (Entscheidung über den nächsten Prozess, kein Lifelock kein After You )
- Bounded Waiting (Nachdem ein Prozess einen Request für den kA gegeben hat, Anzahl der Eintritte in den kA durch andere Prozesse abgeschrankt, keine Starvation)

#### Arten von Lösungen

- Softwarelösungen (Annahme: atomizität von lese- schreiboperationen auf speicher)
- Hardwareunterstützte Lösungen (atomare Maschineninstruktion)
- Höhere Synchronisationskonstrukte (vom API des BS verfügung gestellt)

<br>

### Mutual Exclusion in Software

#### Softwarelösungen

Preface: 
- P0 und P1 für zwei Prozesse
- dann Generalisierung mit n Prozesse Pi mit Pi != Pj für i !=  j
- HW Unterstützung atomares Lesen Schreiben eines Wertes vom/im Speicher
- Synchronisation über globale Variable
- Warteschleifen: Warten auf das eintreten einer Bedingung durch ständiges Testen
  
```sh
while Bedingung != true do nothing
```


#### Dekker algorithmus
![[Pasted image 20261104113329.png]]


#### Peterson-Algorithmus
![[Pasted image 20261104113350.png]]

- Mutual Exclusion
	- P0 setzt flag flag[0] auf true -> P1 blockiert
	- P1 im kA -> flag[1] = true -> P0 blockiert

- keine endloses gegenseitig Blockieren (Annahme P0 blockiert in while-Schleife dh. flag[1] = true und turn = 1)
-  P1 will nicht in kA >< flag[1] = true
-  P1 wartet auf kA >< turn = 1
- P1 monopolisert kA >< P1 muss turn von neuerlichem Eintritt in kA auf 0 setzen



#### Bakery Algorithm

wir haben bis jetzt immer nur 2 Prozesse angeschaut, was macht man mit n Prozessen? 

- NUmmernvergabe für kritische Abschnitt; Prozess mit niedrigster Nummer (>0) tritt als erstes in kA ein
- Nummer 0 keine Anforderung für kA Eintritt
- Pi und Pj mit gleichen Nummern: Pi kommt vor Pj in kA wenn i < j 
- es gilt: neu vergebene Nummer >= vorher vergebene Nummern

```
var choosing: array[0...n-1] of boolean;
	number: array[0...n-1] of integer;
```
![[Pasted image 20261104114148.png]]

<br>

### Hardwareunterstütze Lösungen

- Interrupt Disabling während kA
	- für Uniprozessorsystem geeignet (aber: Einschränkung des BS beim Dispatiching von Tasks)
	- Schutz von Intruktionssequenzen im BS

- Mächtigere atomare Maschineninstruktionen
	- test and set
	- Swap (Exchange)


#### Test and Set
![[Pasted image 20261104114437.png]]



#### Test and Set für kA
![[Pasted image 20261104114457.png]]


#### Sicherung des kA mit exchange
![[Pasted image 20261104114552.png]]

#### Busy Waiting
- Bisherige Lösungen verwenden Busy Waiting: Schleife zum wiederholten Testen der Wartebedingung
- Prozess verschwendet CPU-Zeit mit Warten
- kein geeigneter Mechanismus zur Synchronisation für Benutzer Code
- Blockieren der wartenden Prozesse in Blocked Queues 

<br>

### Semaphore

- Synchornisationskonstrukt ohne Busy Waiting 
- Semaphor S: Integer-Variable, auf de nach der Initialisierung nur mit zwei atomaren Funktionen wait und signal, zugegriffen werden kann

![[Pasted image 20261104114924.png]]

#### Semaphore Datenstruktur
![[Pasted image 20261104114952.png]]

#### Semaphore Operationen 
![[Pasted image 20261104115015.png]]

#### Wechselseitiger Ausschluss
![[Pasted image 20261104115104.png]]


#### Semaphore Implementierung

- wait und signal müssen als atomare Operationen (=kA) ausgeführt wreden
- Sichern der Semaphoroperationen mit Test und Set
	- flag in der Semaphordatenstruktur
	- vor kA: Bus Waiting mit test von flag
	- da wait und signal sehr kurz sind, kommt es kaum zum Busy waiting; daher ist der Overhead vertretbar

<br>

#### Semaphore Bemerkungen
![[Pasted image 20261104115255.png]]
![[Pasted image 20261104115304.png]]



#### Bedingungssynchronisation
Prozesse P1 und P2 müssen untereindaner kommunizieren, sodass ein Code C1 in P1 vor C2 in P2 ausgeführt. Deshalb Semaphoren für Bedingungssynchronisation (Condition Synchronisation)

![[Pasted image 20261111122203.png]]

#### Abwechselnder Zugriff
Wiederholter Datentransfer von P1 an P2, bspw schreibt P1 und P2 liest in ein SHM Objekt. 
Die eingelesenen/eingeschriebenen Daten dürfen nicht dupliziert oder verloren werden
![[Pasted image 20261111122602.png]]
![[Pasted image 20261111122648.png]]


#### Aufgabe
![[Pasted image 20261111122713.png]]
![[Pasted image 20261111122722.png]]
13:29 1:1 wie in den Prüfungen gut anschauen

57 man kann schon lesen bevor, irgendwas hiniengeschrieben worden ist

### Semaphoren Beispiele 

#### Producer-Consumer Problem
![[Pasted image 20261111122911.png]]

Was wäre wenn der Puffer unbegrenzt wäre? 

Produzent kann jederzeit ein Datenelement schreiben, der Konsument muss auf die daten warten, "in" zeigt auf nächstes freies Puffer-Element wo hingegen "out" zeigt auf nächstes  zu lesendes Element.
![[Pasted image 20261111123157.png]]

Was wäre wenn man Semaphoren einführt? 

- Mutual Exclusion: zu jedem Zeitpunkt darf nur ien Prozess auf den Pufferzugreifen (Semaphore "S")
- Bedingungssynchronisation: ein Konsument darf nur dann lesen, wenn mindestens ein ungelesenes Datenelement im Puffer steht. (Counting Semaphore "N" spiegel tAnzahl der Elemente im Puffer wieder)

![[Pasted image 20261111123330.png]]

Das wäre die Implementierung mit einem unbegrenztem Speicher, aber idR schauen die Sachen oftmals anders aus. 
Ein Ringpuffer mit K Elementen, also begrenzt;
- Lesen: mindestens ein "neuer" Wert notwendig
- Schreiben: mindestens ein Pufferelement muss frei sein

![[Pasted image 20261111123455.png]]

Wie können die Semaphoren für dieses Layout implementiert werden? 

- Semaphoren wie bei unbegrenztem Puffer (Bedingunen und Semaphoren wie bei unbegrenztem)
-  Bedingungssynchronisation: ein Produzuent darf nur dann schreiben, wenn mindestens ein leerer Speicherbereich vorhanden ist (E)
![[Pasted image 20261111123644.png]]

Die Reihen abfolge von V-Operationen "beliebig"
==Abfolge von P-Operationen== ist relevant!!!

![[Pasted image 20261111123751.png]]

#### Reader-Writer Problem

- Es gibt Lese- und Schreibprozesse, die auf eine gemeinsame Ressource zugreifen
- Beliebig viele Leser dürfen parallel lesen
- Schreiber benötigen exklusiven Zugriff
![[Pasted image 20261111124009.png]]

Fix: was wenn wir noch einen Semaphore Z hinzufügen? 
![[Pasted image 20261111124034.png]]

Was, wenn wir nochmal einen Semaphore hinzufügen, im loop?  
![[Pasted image 20261111124125.png]]


#### Dining Philosophers Problem
![[Pasted image 20261111124234.png]]

Jeder braucht zum Essen zwei Gabeln, es gibt aber nicht genug Gabeln für alle, wir suchen eine Lösung ohne Deadlock und Starvation

![[Pasted image 20261111124324.png]]

Eine Potenzielle Lösung, die ich sogar gesagt habe in der VO, was wenn wir einen Semaphore hinzufügen, der maximal 4 Philosophen gleichzeitig das Aufnehmen der Gabeln erlaubt, mindestenes ein Prozess nimmt die Gabeln in umgekehrter Reihenfolge auf, atomare P-Operationen für mehrere Semaphoren
![[Pasted image 20261111124447.png]]


#### P und V für mehrere Semaphoren
![[Pasted image 20261111124605.png]]


Für die Aufgabe, siehe Vorlesung, 10.11.2026


#### Probleme mit Semaphoren

Semaphoreoperationen sind über Prozesse verteilt, daher unübersichtilich. Operationen müssen in allen Prozessen korrekt verwendet werden . Ein fehlerhafter Prozess bewirkt Fehlverhalten aller Porzesse, die zusammenarbeiten 

Lösunng? Monitore

<br>

---

### Monitor, Nachrichten und andere Synchronisationsmechanismen

#### Monitor

Ist ein Softwaremodul, besteht aus:
- Prozeduren
- Lokalen Daten
- Initialisierungscode

Eigenschaften:
- Zugriff auf lokale Variable: Monitorprozeduren
- Eintritt von Prozessen in den Monitor über Monitorprozeduren 
- max ein Prozess zu jedem Zeitpunkt im Monitor

Ein Monitor erzwingt Mutual Exclusion, kein explizites Programmieren nötig. Gemeinsamer Speicher ist im Monitorbereich anzulegen. 

Bedingungssynchronisation über Monitorvariable
- Programmierung von Wartebedingungen für Bedingungsvariable (Condition Variables)
- Monitoreintritt, wenn Wartebedingung der Bedingungsvariablen erfüllt sind

![[Pasted image 20261111125405.png]]

#### Condition Variables

![[Pasted image 20261111125449.png]]

#### Monitor: Producer-Consumer
![[Pasted image 20261111125505.png]]

#### Message Passing
![[Pasted image 20261111125550.png]]



## Anmerkung
VO 3.11 ist ziemlich gut, und relevant für Prüfung! Seine Skizze!
