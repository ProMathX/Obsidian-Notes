# ACHTUNG!
>[!important]
>Dieses Cheat Sheet wurde von Gemini-Pro erstellt:
>Prompt 1
>"
>erstelle mir ein komplettes SQL Cheat Sheet von dieser PDF, also iuch meine wirklich alles ovn der ganzen pdf, zu jedem Thema
NIMM DIR SO VIEL ZEIT WIE MÖGLICH, UM DAS DOKUMENT MEHRMALS ZU SCANNEN UND ES DURCHZUGEHEN UND DEINE ANTWORT ZU VERFEINERN, ich kann bist zu mehreren Mintuen warten 
>"
>
>Prompt 2 
>"
>passt jetzt in markdown format, für obsidian bitte pdf nocnmalö durchgehen und vorherige antowrt prüfen und dann antweorten
>"

>[!Anmerkung]
>Verwendete Dateien waren SQL 1 + 2 



SQL ist eine **deklarative** Anfragesprache ("Was", nicht "Wie").

- **DDL (Data Definition)**: `CREATE`, `ALTER`, `DROP` (Schema-Ebene).
    
- **DML (Data Manipulation)**: `INSERT`, `UPDATE`, `DELETE` (Datensatz-Ebene).
    
- **DQL (Data Query)**: `SELECT` (Anfragen).
    
- **TCL (Transaction Control)**: `BEGIN`, `COMMIT`, `ROLLBACK` (Steuerung).
    
- **DCL (Data Control)**: `GRANT`, `REVOKE` (Rechte).
    

---

## 2. DDL: Datendefinition

### Wichtige Datentypen

- `char(n)`: Feste Länge, belegt immer $n$ Bytes.
    
- `varchar(n)`: Variable Länge, belegt nur genutzten Platz.
    
- `numeric(p,s)`: Präzision ($p$ gesamt, $s$ nach Komma).
    
- `date`, `xml`, `blob`/`clob` (große Daten).
    

### Tabellenverwaltung

SQL

```
-- Erstellen
CREATE TABLE prof (
  id integer PRIMARY KEY,
  name varchar(30) NOT NULL,
  rank char(2) UNIQUE
);

-- Aus anderer Tabelle erstellen
CREATE TABLE prof2 AS (SELECT * FROM prof); -- [cite: 18]

-- Ändern [cite: 18, 19]
ALTER TABLE prof ADD COLUMN (office integer);
ALTER TABLE prof ALTER COLUMN name type varchar(50);
ALTER TABLE prof DROP COLUMN rank;

-- Löschen [cite: 20, 21]
DROP TABLE prof;
TRUNCATE TABLE prof; -- Leert Inhalt (schneller als DELETE)
```

### Constraints & Zahlengeneratoren

- `PRIMARY KEY`: Beinhaltet `NOT NULL` und `UNIQUE`.
    
- `FOREIGN KEY (col) REFERENCES tab(id)`: Referenzielle Integrität.
    
- **Sequenzen**:
    
    SQL
    
    ```
    CREATE SEQUENCE serial START 101; -- [cite: 15]
    CREATE TABLE wine (id integer DEFAULT nextval('serial')); -- [cite: 16]
    ```
    

---

## 3. DML: Datenmanipulation

SQL

```
-- Einfügen [cite: 559, 563]
INSERT INTO professor VALUES (2136, 'Curie', 'C4', 36);
INSERT INTO professor (empid, name) VALUES (2137, 'Kant'), (2138, 'Hegel');

-- Löschen & Ändern [cite: 575, 576]
DELETE FROM student WHERE semester > 13;
UPDATE student SET semester = semester + 1;
```

---

## 4. DQL: Anfragen (Grundlagen)

### SFW-Block (Select-From-Where)

- **SELECT**: Projektion ($\pi$). `DISTINCT` entfernt Duplikate.
    
- **FROM**: Kreuzprodukt ($\times$) oder Joins.
    
- **WHERE**: Selektion ($\sigma$).
    
- **ORDER BY**: `ASC` (Default), `DESC`.
    

Join-Varianten

- **Natural Join**: Verbindet über gleichnamige Spalten.
    
- **Inner Join**: `A JOIN B ON A.id = B.id` (Theta Join).
    
- **Outer Join**: Behält Tupel ohne Partner (`LEFT`, `RIGHT`, `FULL`). Fehlende Werte werden `NULL`.
    

### Mengenoperationen

Verlangt gleiche Spaltenanzahl/Typen.

- `UNION` / `UNION ALL` (Vereinigung).
    
- `INTERSECT` (Schnittmenge).
    
- `EXCEPT` (Differenz).
    

---

## 5. Komplexe Abfragen & Rekursion

### Subqueries (Schachtelung)

- **Mengen-Prädikate**: `IN`, `NOT IN`, `EXISTS`, `NOT EXISTS`.
    
- **Quantoren**: `ALL` (alle Bedingungen erfüllt), `ANY` (mind. eine).
    
- **Allquantifizierung**: "Welche A haben alle B?" wird über doppelte Negation mit `NOT EXISTS` gelöst.
    

### Rekursive Anfragen (WITH RECURSIVE)

Wichtig für Hierarchien oder Pfade (z.B. Voraussetzungen von Kursen).

SQL

```
WITH RECURSIVE transitiveCourse (pred, succ) AS (
    SELECT predecessor, successor FROM requires -- Basis-Teil
    UNION
    SELECT t.pred, r.successor 
    FROM transitiveCourse t, requires r 
    WHERE t.succ = r.predecessor -- Rekursiver Teil
) SELECT * FROM transitiveCourse; -- [cite: 176]
```

---

## 6. Aggregation & Gruppierung

### Funktionen

`COUNT(*)`, `SUM(col)`, `AVG(col)`, `MIN(col)`, `MAX(col)`.

### GROUP BY & HAVING

- `GROUP BY`: Bildet Gruppen basierend auf Attributwerten.
    
- `HAVING`: Filtert die **Gruppen** (WHERE filtert Zeilen vor der Gruppierung).
    

> [!IMPORTANT]
> 
> Jedes Attribut im `SELECT`, das nicht aggregiert wird, **muss** im `GROUP BY` stehen!

---

## 7. Fortgeschrittene Konzepte

### NULL-Werte (Dreiwertige Logik)

- Vergleiche mit NULL ergeben `unknown`.
    
- NULL wird propagiert: `null + 1 = null`.
    
- Prüfung immer mit `IS NULL` oder `IS NOT NULL`.
    
- `COALESCE(val, replacement)`: Ersetzt NULL durch Alternativwert.
    

### Window Funktionen

Erlauben Aggregation, ohne Zeilen zusammenzufassen.

- `RANK() OVER (PARTITION BY ... ORDER BY ...)`
    
- Führt Berechnungen über "Windows" (Frames) durch.
    

### Sichten (Views)

Virtuelle Tabellen für Abstraktion oder Sicherheit.

- `CREATE VIEW name AS SELECT ...`.
    
- **Materialized Views**: Speichern das Ergebnis physisch zur Performance-Steigerung.
    

Dynamische Integrität & Trigger

- `ON DELETE CASCADE`: Löscht abhängige Datensätze automatisch.
    
- `ON UPDATE SET NULL`: Setzt Fremdschlüssel bei Änderung auf NULL.
    
- **Trigger**: Automatische Aktionen nach dem ECA-Prinzip (Event, Condition, Action).
    
    - `BEFORE` / `AFTER` auf Zeilen- oder Statement-Ebene.

---
# DIVISON

Die relationale Division löst Fragen vom Typ: _"Finde X, die mit **allen** Y verknüpft sind."_

### 1. Der "Zähl-Ansatz" (Gruppierung & Vergleich)

Dies ist die modernste und lesbarste Variante. Sie vergleicht die Anzahl der vorhandenen Verknüpfungen mit der Soll-Anzahl.

SQL

```Postgresql
SELECT x_id
FROM VerknüpfungsTabelle
GROUP BY x_id
HAVING COUNT(DISTINCT y_id) = (SELECT COUNT(*) FROM Y_Tabelle);
```

- **Wann nutzen?** Fast immer. Sehr performant bei indizierten Spalten und leicht zu verstehen.
    
- **Voraussetzung:** Die Verknüpfungstabelle darf keine Duplikate enthalten (sonst `DISTINCT` im Count nutzen).
    

---

### 2. Der "Doppelte-Verneinung-Ansatz" (Universal-Quantor)

Logik: _"Finde X, für die es **kein** Y gibt, das **nicht** mit X verknüpft ist."_

SQL

```Postgresql
SELECT x.name
FROM X_Tabelle x
WHERE NOT EXISTS (
    SELECT * FROM Y_Tabelle y
    WHERE NOT EXISTS (
        SELECT * FROM VerknüpfungsTabelle v
        WHERE v.x_id = x.id AND v.y_id = y.id
    )
);
```

- **Wann nutzen?** Wenn du strikt nach relationaler Algebra arbeitest oder Aggregate (`COUNT`) aus Performancegründen vermeiden willst.
    
- **Vorteil:** Funktioniert auch, wenn die "Soll-Menge" (Y) leer ist (ergibt dann meist alle X).

### 1. Die "Except"-Variante (Mengenlehre)

Dieser Ansatz ist mathematisch am nächsten an der Definition: _"Die Menge aller Großhändler im Land minus der Menge der Großhändler, mit denen der Kunde einen Vertrag hat, muss leer sein."_

SQL

```Postgresql
SELECT c.name
FROM customer c
WHERE NOT EXISTS (
    -- Menge aller Großhändler im Land des Kunden
    SELECT w.name FROM wholesalers w WHERE w.country = c.country
    EXCEPT
    -- Menge der Großhändler, mit denen dieser Kunde einen Vertrag hat
    SELECT d.whname FROM distributor d WHERE d.customer = c.name
);
```

- **Vorteil:** Sehr logisch aufgebaut. `EXCEPT` entfernt alle Übereinstimmungen; bleibt nichts übrig, ist die Bedingung erfüllt.
    
- **Nachteil:** In der Performance oft etwas langsamer als `COUNT`, da Mengenoperationen teuer sein können.
    

---

### 2. Die Array-Variante (PostgreSQL-Spezifisch)

In Postgres kannst du alle IDs eines Kunden in ein Array packen und prüfen, ob dieses Array das Array aller Großhändler im Land "enthält" (`@>`).

SQL

```Postgresql
SELECT c.name
FROM customer c
WHERE (
    SELECT array_agg(DISTINCT name ORDER BY name) 
    FROM wholesalers w WHERE w.country = c.country
) <@ (
    SELECT array_agg(DISTINCT whname ORDER BY whname) 
    FROM distributor d WHERE d.customer = c.name
);
```

- **Vorteil:** Extrem kompakt, wenn man mit Postgres-spezifischen Operatoren arbeitet.
    
- **Nachteil:** Überhaupt nicht portierbar auf andere SQL-Dialekte (wie MySQL oder Oracle) und schwerer zu lesen für SQL-Neulinge.
    

---

### 3. Join mit String-Aggregation (Der "Dirty"-Hack)

Manchmal sieht man Lösungen, die alle Namen alphabetisch sortiert in einen langen Textstring verketten und diese Strings vergleichen.

SQL

```Postgresql
SELECT c.name
FROM customer c
JOIN (SELECT country, string_agg(name, ',' ORDER BY name) as all_wh FROM wholesalers GROUP BY country) w_list
  ON c.country = w_list.country
JOIN (SELECT customer, string_agg(DISTINCT whname, ',' ORDER BY whname) as my_wh FROM distributor GROUP BY customer) d_list
  ON c.name = d_list.customer
WHERE w_list.all_wh = d_list.my_wh;
```

- **Vorteil:** Funktioniert gut für Reports, bei denen man die Liste der Partner sowieso sehen will.
    
- **Nachteil:** **Ganz schlechter Stil** für reine Logik-Prüfungen. Es ist fehleranfällig (Sonderzeichen in Namen) und performancetechnisch eine Katastrophe, da Strings verglichen werden statt IDs.
    


