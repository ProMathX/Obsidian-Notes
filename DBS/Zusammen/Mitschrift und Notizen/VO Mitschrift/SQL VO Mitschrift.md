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

SQL ist eine deklarative Sprache
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
---
##### Transaktionssprache
- kennzeichnet beginn einer Transaktion (Banküberweisung)
- COMMIT, schließt eine Transaktion ab
- ROLLBACK, setzt eine Transaktion zurück
---

##### Anfragesprache SQL-Grundlagen
- Der SFW Blcok 
- Einfache Anfragen 
- Mengenoperation 
- Schachtelung von Anfragen 
- Allquantifizierende Anfragen

Grundgerüst einer Abfrage
```mySQL 
SELECT <Liste von Attributen>  (Projektion)

FROM <Liste von Tabllen> (Kreuzprodukt)

WHERE <Bedingung>;  (Selektion)

```
- Man macht zuerst das FROM also das Kreuzprodukt, dann WHERE, dann SELECT

Auswahl von Tabellen 
```mySQL
SELECT *
FROM wine AS W;
	
	
SELECT *
FROM wine w1, wine w2; 
```

Natural Join (alt)
```mySQL
SELECT*
FROM wine,producer
WHERE wine.vineyard = producer.vineyard
```

(neu)
```mySQL
SELECT*
FROM wine,producer
WHERE wine NATURAL JOIN producer;
```

Es gibt auch das Kreuzprodukt als expliziter Operator
Man kann ein neues Tupel erstellen für Zwischenergebnisse
```mySQL
SELECT result.vineyard
FROM (wine NATURAL JOIN producer AS W)
```

Sortierung 
```mySQL
SELECT empid, name, rank 
FROM  professort
ORDER BY rank DESC, name ASC
```
- DESC... descending
- ASC ... ascending 
 
 <> .... != 
 
```mySQL
IS NULL
```
Testet ob null Wert

Bei Mengenoperation ist Duplikateneliminierung (disting) defualt


Durchschnitt (INTERSECT) und Mengendifferenz (EXCEPT) werden auch unterstützt

Existenzquantoren mit 
- ALL  $\forall$
- ANY $\exists$

Unkorrelierte Unteranfragen
attribut IN (SFW Block)

```mySQL
SELECT name
FROM professor
WHERE empid IN(SELECT taughtby
				FROM course);
```

NOT IN :<= > ist ähnlich wie ein Differenzenoperators in der relationalen Algebra

---
### Fortsetzung 20.4 

Es wurde einfach subqueries und group by gemacht



##### Rekursion und SQL 
Berechnung der Vorgänger 


```sql

with recursive mytable(number) as 
(
	values(1)
union 
	select number+1
	from mytable
	where number < 100
)
select sum(number)
from mytable;

```

es wird immer das letzte ergebnis der rekursion genommen

```postgresql

with recursive transitiveCourse(pred,succ)
as(
	select predecessor, successor
	from requires
union
	select distinct t.pred, r.successor
	from transitiveCourse t, requires r 
	where t.succ = r.predecessor
)
select *
from transitiveCourse
order by (pred,succ) asc;

```




## Important Details
Muss geübt werden

## Examples
[[SQL]]

## Questions
- Was sind die Edge Cases, also ab wann reicht SQL nicht mehr aus um Daten zu repräsentieren? 
- 

## Summary
Ausarbeiten der Folien I guess? So die wichtigsten Keywords, es ist nicht schwer, aber halt neu.
Dementsprechend ein Keyword list oder canvas eigentlich erstellen und mit diesem, dann arbeiten.

Also je nach Operatorfunktion, es so zurechtschreiben, sodass es passt.



## Related Topics
- [[DBS-6.pdf]]
- [TUW Tool](https://gordon.dbai.tuwien.ac.at/eSQL-tutorial/coursesList.action)
- [Internet Übungstool](https://sqlbolt.com/)
