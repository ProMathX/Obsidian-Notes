---
topic: Transaktionen in SQL
date: 2026-03-16
course: DBS
tags:
  - studies
  - "#DBS"
---
## Key Concepts
- Transaktion verstehen 
- ACID Eigenschaften 
- Serialisierbarkeit
- Konzept von Schedules
- Recoverable Schedules und Cascadeless Schedules

Beim Abbrechen von Transaktion (in der Mitte) stellt ein Problem dar
Alle Schriite müssen Alles oder nichts- Prinzip
Änderungen müssen permantent gespeichert werden

>[!Def]
>Eine Transaktion ist eine Bündelung einer Datenbankoperation

### Eigenschaften von Transaktionen ACID
- *A*tomicity (Atomarität)
	- Alles oder nichts Prinzip
	
- *C*onsistency (Konsizenz)
	- Ausführung einer Transaktion in Isolation enhätl den konsitenten ZUstand der Datenbank
	
- *I*solation
	- Jede Transaktion hat die DB "für sich alleins"
		- mittels Lock implementiert
		- Zwischenreuslatte (bei Transaktion) nicht einsehbar
		
- *D*urability 
	- Änderungen dürfen nich verloren gehen
		- Mit Log Einträgen implementiert


#### Operationen

- SQL Begin of transaction -> Anfang der Transaktion
```SQL
BEGIN;
```
- commit  -> Ende der Transaktion
```SQL
COMMIT;
```
- roolback oder abort (rollback der Transaktion)
```SQL
ROLLBACK;
```

- autocommit Modus, jeder Befehl wird ein einer egenen transaktion ausgeführt 

Beispiele für Checks
```SQL 
CREATE TABLE emp (
eid INT PRIMARY KEY ,
ename VARCHAR (30) NOT NULL , 
salary INT NOT NULL CHECK ( salary > 0) 
) ; 
-- primary key violation 
insert into emp values (11 , ’ Kim ’ , 200) ;
 -- Not null constraint violation 
insert into emp values (44 , NULL , 200) ; 
 -- Check statement violation
insert into emp values (44 , ’ Kim ’ , -200) ;
```

Savepoints  savepoint_name; -> teilweise rückgängig gemacht werden(Transaktionen)

- erfolgreicher Abschluss -> *Commit*
- erfolglose Ab -> *Abort*
- erfolglos Abschluss durch Fehler

- Realisation durch Mehrbenutzersynchronisation (isolation)
	- Semantische Korrektheit bei Nebenlöufigkeit
		- Nebenläufikeit paralles ablaufen des DBMS bei mehreren pro Nutzern (?)
	- Serialisierbarketi
	- Schächerre Isolation

- Recovery(Atomicity und Durability)
	- Zurücksetzen teilweise ausgeführter Transaktion
	- Wiederausführung von Transaktionen nach einem Fehler
	- Sicherstellen der Persiszenz von Änderungen

![[Pasted image 20260427144425.png]]

### Schedules und Serialisierbarkeit

![[Pasted image 20260427144700.png]]


Es gibt Probleme bei nebenläufiger Ausführung
- Es kann sein, dass die Werte gelöscht werden (*Lost Updates*)
- *Dirty Read* (Abhängigkeit von nicht freigegeben Änderungen)
- *Non-Repeatable Read* (Abhängigkeit von anderen Updates) bricht isolation
- *Phantomproblem* (Abhängigkeit von neuen/gelöschtren Tupeln)

#### Nebenläufigkeit und Korrektheit
![[Pasted image 20260427145603.png]]


>[!Defintion]
>Ein Schedule ist eine Sequenz von Operatioen von einer oder mehreren Transaktionen. Bei nebenläufigen Transaktionen können operatoren verzahnt sein

- Serieller Schedule
	- Operatioenen werden seqenziell ohn ezeitlich überlappung
- Nebenläufig
	- zeitlich überlappend 
-  Ein Schedule ist gültig (*valid*), wenn das Resultat der Ausführung “korrekt” ist
![[Pasted image 20260427150412.png]]


#### Korrektheit

>[!Def 1]
>Eine nebenläufige Ausführung von Transaktionen muss die Datenbank in
einem konsistentem Zustand hinterlassen.

>[!Def 2]
>Eine nebenläufige Ausführung von Transaktionen muss ergebnisäquivalent zu einer seriellen Ausführung der Transaktionen sein.

![[Pasted image 20260427150758.png]]


- Korrektheit von Schedules werden *nur die reads und writes* verwendet um die Korrekheit zu überprüfen

>[!Def4]
>Ein Schedule ist conflict serializable (konfliktserialisierbar) wenn er
konfliktäquivalent zu einem seriellen Schedule ist.



## Important Details

## Examples


## Questions
- Probleme bei Nebeläufiger Ausführung anschauen

## Summary


## Related Topics
- [[DBS-7_Part1.pdf]]
