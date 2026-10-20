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

Befehlszähler, die anzahl der Instruktionen die man hier durchgeht


### Trace
- Charakterisiert das Verhalten eines Prozesses
- Sequenz der Instruktionen, die für einen Prozess ausgeführt werden
- Überlappung von Traces verschiedener Prozesse charakterisieren das Prozessorverhalten

![[Pasted image 20261013141920.png]]

![[Pasted image 20261013142029.png]]


Kurze Begriffserklärung [Dispatcher](https://de.wikipedia.org/wiki/Dispatcher_(Informatik)?useskin=vector)
Kurz: Ein Dispatcher gibt der CPU die Anweisung zu welchem Prozess zu wechseln

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

### Wesentliche Prozesszustände
![[Pasted image 20261013143529.png]]

### 5 Zustands Prozessmodell

![[Pasted image 20261013143553.png]]

#### Queueing modell 
![[Pasted image 20261013143611.png]]

- **New zustand**
	- BS hat den Prozess kreiert:
		- Prozessnummer (PID oder process identifier)
		- tabellen und Tabelleneinträge zur Prozessverwaltung
	- der Prozess ist jedoch noch nicht bereit zur Ausführung
		- Ressourcenschonung


- **Exit**
	- Zustand wird durch Terminierung erreicht
	- Prozess wird nicht mher weiter ausgeführt 
	- Prozessinformationen werden  von Hilfsprogrammen verwendet 
	- Prozessinformationen, -tablenne werden gelöscht wenn sie nicht mehr benötigt werden


### Process Switch
![[Pasted image 20261013143914.png]]

- supervisor macht eher systemcall 
### Swapping
![[Pasted image 20261013144226.png]]

### Prozesszustände mit Suspend

![[Pasted image 20261013144252.png]]

### Ursachen für Suspend
- swapping
-  BS lagert Hintergrundporzess, Utility oder problembehafteten Prozess aus
- INterkativer Request (zB für Debugging)
- Timing: periodischer Prozess kann zwischen Aktivierung ausgelagert werden
- Parent Request: Untersuchung, Modifikation, koordinatoin von Kindprozessen

## Kontrollstrukturen für die Prozessverwaltung

### Kontrollstrukturen des BS

- Memory Tables 
- I/O Tables (Geräte und Kanäle)
- File Tables 
- Process Tables


### Process Image

- User Program
- User Data 
- System Stack 
- Process Control Block 
![[Pasted image 20261020132545.png]]


### PCB Process Identification
- PID (Process identifier) index  im Primary Process Table
- UID (User identfier) (besitmmt die Rechte des Prozesses)
- PPI (Parent Process Identifier)


### PCB Processor (CPU) State Information
- Registerinhalte
-  Kontroll und Statsusregister
- Stack Pointers

### Process Control Information
- Scheduling und Zustandsinformation
- Querverweise auf andere Prozesse
- Interprozesskommunikation (IPC)
- Privileges
- Memory Management
- Ressourcen


### Prozesslisten
![[Pasted image 20261020133510.png]]


### Execiton Modes
- Um die Datenstrukture (zb PCB) des BS zu schützen gibt es mindestes zwei execution mode
	- Privileged Mode (root)
	- User Mode
- Mode Switch in BS-Routinen
- Exection Modes werden durch Mode-Bits der CPU unterstützt
Also die Hardware muss das auch unterstützten!

### Mode Switch vs Process Switch
![[Pasted image 20261020133945.png]]


Process switch -> CPU kommt zu dem Prozess eines anderen Prozesses

Nicht jeder Process Switch .. 13:42 vervollständigen!!!


### Example Interrupt Handling
![[Pasted image 20261020134625.png]]

## Prozesse im Betriebssystem

### Nonprocess Kernel

![[Pasted image 20261020135237.png]]
- Prozessbegriff nur für Benutzerprogramme (in dem Moment ein Service des BS aufrufe, verlasse ich den Prozesskontext, kehrt dann wieder in ein Prozesskontext ein (Mode Switch nach Vollendung))
- Verlassen des Prozesskontexts bei BS-Aktivität
- BS arbeitet von Prozessen getrennt im Privilged Mode (eigener Speicherbereich , eigener Stack für BS)
### BS-Ausführung in User-Prozessen
![[Pasted image 20261020135346.png]]

Prozess kontext, so wenig wie mlöglich aufrufen.
Ich bleibe im aktuellen Prozesskontext, kaum, ich verlasse den Kontextwechsel bei Prozess Switch oder einen neuen Prozess aktivieren will. 

- BS ist eine Sammlung 


### BS Ausführung in User-Processes

![[Pasted image 20261020135700.png]]


### Prozessbasiertes BS
![[Pasted image 20261020135731.png]]

- BS sit eine Sammlung von Systemprozessne
- Nur Basisservices sind nicht als Prozesse realisiert

### Kernel Architekturen
![[Pasted image 20261020135857.png]]


### Microkernel Architektur
Prozessbasierte Architektur
![[Pasted image 20261020140351.png]]
![[Pasted image 20261020140448.png]]

## Threads

### Prozesse und Threads

### Singlethreaded Process Model

### Multithreaded Process Model

### Vorteile von Threads vs Prozess

### Einsatzbereich von Threads

### User Level Threads (ULT)

### Kernel Level Threads (KLT)




# TODO
Im Buch weiter lesen, weil das erklärt es ziemlich besser

#### Links
- [[Learn Lean]]
