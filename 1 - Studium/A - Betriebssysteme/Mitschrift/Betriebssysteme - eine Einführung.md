---
topic: Betriebssysteme
date: 2026-03-16
course: OSVO
tags:
  - studies
  - Betriebssysteme
---
## VO
Warum ist Puschner so cool? 


### Historie
#### Serial Processing (1950)

- kein OS
- direkte Programmierung der Hardware
- I/O: Schalter, lampen; Kartenleser, Drucker

Problem: Fehleranfälligkeit
Lösung: unterprogrammbibliothek für I/O

Problem: Setup benötigt viel Zeit
Lösung 1: Spezialist für Setup
Lösung 2: Monitor

JCL- Job Control language
bspw übersetze in ein Pascal compiler

#### Monitor (1960)

![[Pasted image 20261013133250.png]]

Was muss implementier werden für den Monitor?:
- Speicherschutz
- Timer
- Privilegierte Instruktion (Privilegien des OS schützen)
- Interrupts

Problem: entweder CPU oder I/O akitv, der Rest der Maschine ist untätig

Lösung: parallele CPU und I/O Aktivität 
	Pufferung und I/O interrupts


#### Multiprogramming (1965)

Problem: Kaum ien Programm nützt CPU und perihphäre Hardware gelichmäßig aus 
- CPU Intesive Programme (CPU bound)
- I/O inteisve Programme (I/O bound)

Lösung: Multiprogramming bzw Multitasking


![[Pasted image 20261013133724.png]]

Stichwort CPU cycling (intruction cycling)


#### Multiprogrammed Batch Systems

Die parallele Ausführung von Programmen macht neue Mechanismen notwendig z.B.
- Speicherverwaltung
- Verwaltung der CPU und Ressourcen (Scheduling)

#### Time-Sharing Systems
Problem: Mehrere benutzer teilen einen Computer;Warten auf Fertigstellung von (Batch) Jobs
Lösung: Preemtive Scheduling, Prioritäten

Problem: Daten und Programme sollen für Benutzer leicht verfügbar sein

Lösung: Filesystem am Rechner



#### Was ist ein Betriebssystem? 

- Interface
- Virtuelle Machine
- Dienstleister
- Ressourcenmanager

.... Passt sich den anforderungen des Benutzers an

![[Pasted image 20261013135354.png]]



#### Abstraktionen

- "ungestörte" Programmabarbeitung
	- Prozess
	
- "unendlich" große Speicher, files
	- Speicherverwaltung
	
- "Private" Maschine
	- Zugriffsschutz, Datensicherheit



## Offene Fragen 







#### Links
- [[Learn Lean]]
