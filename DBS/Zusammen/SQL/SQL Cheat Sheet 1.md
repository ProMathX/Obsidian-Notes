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
>Verwendete Dateien waren SQL 1+2



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

