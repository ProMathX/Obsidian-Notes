---
topic: SQL
date: 2026-03-16
course: DBS
tags:
  - studies
  - DBS
---
## Key Concepts
Bisher mit Relationen (Mengen)
Jetzt SQL betrachten wir Tabellen (Bags, Mutlimengen)
##### Datenbeschreibungssprache
- Datentypen
	- varchar(n) für variable länge von dem character eigentlich String? 
	- blob binary large object / raw
	- xml
>[!Abfrage in SQL]
>BSP
```mySQL
INSERT INTO takes
	SELECT studid, courseid
	FROM student, course
	WHERE title = ’Logics’;
```

- Revoke ausführen, um zu sichern ob, sodass nutzer nichts macht 

##### Transaktionssprache
- kennzeichnet beginn einer Transaktion (Banküberweisung)
- COMMIT, schließt eine Transaktion ab
- ROLLBACK, setzt eine Transaktion zurück

##### Anfragesprache SQL-Grundlagen
- Der SFW Blcok 
- Einfache Anfragen 
- Mengenoperation 
- Schachtelung von Anfragen 
- Allquantifizierende Anfragen

Grundgerüst einer Abfrage
```mySQL 
SELECT <Liste von Attributen>

FROM <Liste von Tabllen>

WHER

```


## Important Details
Muss geübt werden

## Examples
[[SQL]]

## Questions
- Was sind die Edge Cases, also ab wann reicht SQL nicht mehr aus um Daten zu repräsentieren? 
- 

## Summary


## Related Topics
- [[DBS-6.pdf]]
- 
