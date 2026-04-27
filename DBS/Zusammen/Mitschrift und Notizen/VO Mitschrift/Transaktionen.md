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

## Important Details

## Examples


## Questions
- 

## Summary


## Related Topics
- [[]]
