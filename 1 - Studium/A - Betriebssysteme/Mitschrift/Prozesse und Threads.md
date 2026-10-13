---
topic: Prozesse und Threads
date: 2026-03-16
course: OSVO
tags:
  - studies
  - Betriebssysteme
  - Prozesse
  - Threads
---
# VO
Wir gehen davon aus, wir haben nur eine CPU und einen Core


Unser Ziel: 
	"Gleichzeitiges", kontrolliertes Ausführen von Programmen auf einem Rechner

- welche mechanismen sind nötig
- welche Datenstrukturen brauchen wir? 

## Prozess
- Ausführbares Progrmam 
- zugehörige Daten (Variable, Stack, Puffer, etc)
- Kontex
	- aktueller Zusatn des Prozesses
	- Daten zu Prozessverwaltung

![[Pasted image 20261013141906.png]]


### Trace
- Charakterisiert das Verhalten eines Prozesses
- Sequenz der Instruktionen, die für einen Prozess ausgeführt werden
- Überlappung von Traces verschiedener Prozesse charakterisieren das Prozessorverhalten

![[Pasted image 20261013141920.png]]

![[Pasted image 20261013142029.png]]

### BS und Prozesse
- BS kontrolliert die Ausführung der Prozesse
- Repräsentation von Prozessen muss Aufgaben des BS unterstützen
	- Zustand des Prozesses 
	- vom Prozess belegter Speicherbereich
		- Verwaltung von Prozessen in Datenstrukturen (Queues) entsprechend ihren Zuständen

### Erzeugung von Prozessen
BS baut Datenstrukturen uaf und allokiert notwendigen Speicher

Wann wird ein Prozess erzeugt?
- Login
- BS Ausführun eines Services
- Erzeugnung durch eine Bentutzerprocess (Parent bzw Child)
- Absetzen eines neuen jobs

### Beendigung von Prozessen
Prozess zeigt Beedniugn an 
- Logout 
- Service request an das BS
- Auftreten eines Fehler bei der Abarbeitung eines Prozesses 
- Halt-Instruktion eines JObs
- 

### Prozesszustände
![[Pasted image 20261013143507.png]]


### Wesentliche Prozesszustände
![[Pasted image 20261013143529.png]]




### 5 Zustands Prozessmodell

![[Pasted image 20261013143553.png]]


#### Queueing modell 
![[Pasted image 20261013143611.png]]

- New zustand
	- BS hat den Prozess kreiert:
		- Prozessnummer (PID)
		- tabellen und Tabelleneinträge zur Prozessverwaltung
	- der Prozess ist jedoch noch nicht bereit zur Ausführung
		- Ressourcenschonung


- Exit
	- Zustand wird durch Terminierung erreicht
	- Prozess wird nicht mher weiter ausgeführt 
	- Prozessinformationen werden  von Hilfsprogrammen verwendet 
	- Prozessinformationen, -tablenne werden gelöscht wenn sie nicht mehr benötigt werden


### Process Switch

![[Pasted image 20261013143914.png]]

- supervisor eher systemcall 
### Swapping
![[Pasted image 20261013144226.png]]

### Prozesszustände mit Suspend

![[Pasted image 20261013144252.png]]

### Ursachen für Suspend


## Kontrollstrukturen für die Prozessverwaltung



#### Links
- [[Learn Lean]]
