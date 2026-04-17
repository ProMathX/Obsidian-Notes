## Grundlegende Abfragen

```sql
SELECT col1, col2
FROM tabelle
WHERE bedingung
ORDER BY col1 DESC oder ASC 
LIMIT 10;
```

```sql
SELECT * FROM tabelle;                    -- Alle Spalten
SELECT DISTINCT col FROM tabelle;         -- Ohne Duplikate
SELECT col AS bezeichnung FROM tabelle;   -- Alias
```

---

## Filtern & Bedingungen

```sql
-- Vergleichsoperatoren
=  !=  <  >  <=  >=
AND  OR  NOT

-- BETWEEN
WHERE alter BETWEEN 18 AND 65

-- IN
WHERE land IN ('AT', 'DE', 'CH')

-- LIKE
WHERE name LIKE 'M%'    -- beginnt mit M
WHERE name LIKE '%er'   -- endet mit er
WHERE name LIKE '_at'   -- ein beliebiges Zeichen

-- NULL
WHERE spalte IS NULL
WHERE spalte IS NOT NULL
```

---

## JOINs

```sql
-- INNER JOIN (nur übereinstimmende Zeilen)
SELECT a.*, b.name
FROM tabelle_a a
INNER JOIN tabelle_b b ON a.id = b.a_id;

LEFT JOIN   -- alle Zeilen aus der linken Tabelle
RIGHT JOIN  -- alle Zeilen aus der rechten Tabelle
FULL JOIN   -- alle Zeilen aus beiden Tabellen
CROSS JOIN  -- kartesisches Produkt

-- Self Join
FROM mitarbeiter m1
JOIN mitarbeiter m2 ON m1.chef_id = m2.id
```

---

## Gruppieren & Aggregieren

```sql
COUNT(*)          -- Anzahl aller Zeilen
COUNT(col)        -- Anzahl Nicht-NULL-Werte
SUM(col)
AVG(col)
MIN(col)  MAX(col)

-- GROUP BY & HAVING
SELECT land, COUNT(*) AS anzahl
FROM kunden
GROUP BY land
HAVING COUNT(*) > 5
ORDER BY anzahl DESC;

-- ROLLUP
GROUP BY ROLLUP(jahr, monat)
```

---

## Daten manipulieren

```sql
-- INSERT
INSERT INTO tabelle (col1, col2)
VALUES ('wert1', 42);

-- UPDATE
UPDATE tabelle
SET col1 = 'neu', col2 = 0
WHERE id = 5;

-- DELETE
DELETE FROM tabelle
WHERE id = 5;

-- UPSERT (PostgreSQL)
INSERT INTO t (id, val)
VALUES (1, 'x')
ON CONFLICT (id)
DO UPDATE SET val = 'x';
```

---

## Tabellen & Schema

```sql
-- CREATE TABLE
CREATE TABLE nutzer (
  id   INT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  mail TEXT UNIQUE,
  age  INT DEFAULT 0
);

-- ALTER TABLE
ALTER TABLE t ADD col INT;
ALTER TABLE t DROP COLUMN col;
ALTER TABLE t RENAME TO neu;

-- DROP
DROP TABLE IF EXISTS tabelle;
TRUNCATE TABLE tabelle;   -- Inhalt leeren, Struktur bleibt
```

---

## Subqueries & CTEs

```sql
-- Subquery
SELECT * FROM aufträge
WHERE kunden_id IN (
  SELECT id FROM kunden
  WHERE land = 'AT'
);

-- CTE (WITH)
WITH top_kunden AS (
  SELECT id, SUM(betrag) AS umsatz
  FROM aufträge
  GROUP BY id
)
SELECT * FROM top_kunden
WHERE umsatz > 1000;

-- EXISTS
WHERE EXISTS (
  SELECT 1 FROM t WHERE ...
)
```

---

## Window Functions

```sql
-- Grundsyntax
FUNKTION() OVER (
  PARTITION BY col
  ORDER BY col
)

-- Rang & Reihe
ROW_NUMBER()    -- eindeutiger Rang
RANK()          -- Lücken bei Gleichstand
DENSE_RANK()    -- keine Lücken
NTILE(4)        -- Quartile

-- Verschiebung
LAG(col, 1)    -- vorherige Zeile
LEAD(col, 1)   -- nächste Zeile
FIRST_VALUE(col)
LAST_VALUE(col)

-- Laufende Summe
SUM(col) OVER (
  ORDER BY datum
  ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
)
```

---

## Indexes & Performance

```sql
-- Index erstellen
CREATE INDEX idx_name ON tabelle (spalte);
CREATE UNIQUE INDEX idx_u ON tabelle (spalte);

-- Index löschen
DROP INDEX idx_name;

-- Query-Plan analysieren
EXPLAIN SELECT * FROM tabelle;
EXPLAIN ANALYZE SELECT ...;
```

---

## Mengenoperationen

```sql
SELECT col FROM tabelle_a
UNION           -- ohne Duplikate
SELECT col FROM tabelle_b;

UNION ALL       -- mit Duplikaten
INTERSECT       -- nur gemeinsame Zeilen
EXCEPT          -- nur in der ersten Menge
```

---

## Nützliche Funktionen

```SQL
-- String
UPPER(s)  LOWER(s)  LENGTH(s)
TRIM(s)   LTRIM(s)  RTRIM(s)
CONCAT(a, ' ', b)
SUBSTRING(s, 1, 3)
REPLACE(s, 'alt', 'neu')

-- Datum & Zeit
NOW()   CURRENT_DATE   CURRENT_TIME
DATE_PART('year', datum)
DATE_TRUNC('month', datum)
DATE_ADD(datum, INTERVAL 7 DAY)

-- Bedingt
COALESCE(a, b, 'default')
NULLIF(a, b)
CASE WHEN x > 0 THEN 'positiv'
     WHEN x = 0 THEN 'null'
     ELSE 'negativ'
END

-- Casting
CAST(col AS INT)
col::TEXT      -- PostgreSQL
```

---

## Transaktionen

```sql
BEGIN;   -- oder: START TRANSACTION

  UPDATE konto SET betrag = betrag - 100 WHERE id = 1;
  UPDATE konto SET betrag = betrag + 100 WHERE id = 2;

COMMIT;   -- oder: ROLLBACK;

-- Savepoints
SAVEPOINT sp1;
ROLLBACK TO sp1;
RELEASE SAVEPOINT sp1;
```



# SQL Constraints – Cheat Sheet

---

## PRIMARY KEY

```sql
CREATE TABLE league (
  leagueID   INT          PRIMARY KEY,  -- reicht völlig aus
  leagueName VARCHAR(100) NOT NULL
);
```

| Constraint  | UNIQUE | NOT NULL | Hinweis                  |
|-------------|--------|----------|--------------------------|
| PRIMARY KEY | ✓ ja   | ✓ ja     | beides bereits enthalten |
| UNIQUE      | ✓ ja   | ✗ nein   | erlaubt NULL             |
| NOT NULL    | ✗ nein | ✓ ja     | Duplikate erlaubt        |

---

## FOREIGN KEY – Syntax

Falsch:
```sql
teamID INT FOREIGN KEY(team.teamID)
```

Richtig:
```sql
teamID INT,
FOREIGN KEY (teamID) REFERENCES team(teamID)
```

---

## FOREIGN KEY – vollständiges Beispiel

```sql
CREATE TABLE belongsToLeague (
  seasonID  INT,
  leagueID  INT,
  teamID    INT,

  PRIMARY KEY (seasonID, leagueID, teamID),  -- zusammengesetzter PK

  FOREIGN KEY (seasonID) REFERENCES season(seasonID),
  FOREIGN KEY (leagueID) REFERENCES league(leagueID),
  FOREIGN KEY (teamID)   REFERENCES team(teamID)
);
```

---

## Alle wichtigen Constraints

| Constraint     | Syntax                                  | Was es tut                          |
|----------------|-----------------------------------------|-------------------------------------|
| PRIMARY KEY    | `id INT PRIMARY KEY`                    | eindeutig + nicht null              |
| FOREIGN KEY    | `FOREIGN KEY (col) REFERENCES tbl(col)` | Verweis auf andere Tabelle          |
| NOT NULL       | `name VARCHAR(50) NOT NULL`             | kein leerer Wert erlaubt            |
| UNIQUE         | `email VARCHAR(100) UNIQUE`             | kein doppelter Wert                 |
| DEFAULT        | `status INT DEFAULT 1`                  | Standardwert wenn nichts angegeben  |
| CHECK          | `CHECK (age >= 18)`                     | Bedingung muss erfüllt sein         |
| AUTO_INCREMENT | `id INT AUTO_INCREMENT`                 | zählt automatisch hoch (MySQL)      |

---

## Häufige Fehler

| Fehler                          | Problem                                          |
|---------------------------------|--------------------------------------------------|
| `PRIMARY KEY UNIQUE NOT NULL`   | UNIQUE + NOT NULL sind redundant                 |
| `col INT FOREIGN KEY(tbl.col)`  | FOREIGN KEY muss separat stehen                  |
| `..., )`                        | Trailing Comma vor ) nicht erlaubt               |
| `REFERENCES tbl.col`            | Punkt-Notation ungültig → `REFERENCES tbl(col)`  |
