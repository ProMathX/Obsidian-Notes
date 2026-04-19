## Aufgabe 1

1) SQL tabelle zu season
```PostgreSQL
CREATE SEQUENCE serial START  1;

CREATE TABLE season(
	seasonID int PRIMARY KEY DEFAULT nextval('serial'),
	startdate DATE NOT NULL,
	enddate DATE NOT NULL,
	commonname VARCHAR(12) NOT NULL UNIQUE 
);
```

```PostgreSQL
CREATE SEQUENCE serial START  1;

CREATE TABLE league(
	leagueID int PRIMARY KEY DEFAULT nextval('serial'),
	name TEXT NOT NULL,
	hierarchylevel int NOT NULL
);
```

```PostgreSQL
CREATE SEQUENCE serial START  3;

CREATE TABLE team(
	teamID int PRIMARY KEY DEFAULT nextval('serial'),
	name TEXT NOT NULL,
	abbreviation varchar(3) NOT NULL UNIQUE,
	stadium varchar(110) NOT NULL
);
```

[longest city name ](https://en.wikipedia.org/wiki/Taumatawhakatangi%C2%ADhangakoauauotamatea%C2%ADturipukakapikimaunga%C2%ADhoronukupokaiwhen%C2%ADuakitanatahu?useskin=vector)

[longest stadium name](https://en.wikipedia.org/wiki/ACA%E2%80%93VDCA_Cricket_Stadium?useskin=vector)

```PostgreSQL
CREATE TABLE belongsTOLeague(
	teamID int REFERENCES team(teamID),
	seasonID int REFERENCES season(seasonID),
	leagueID int REFERENCES league(leagueID)
);
```

```PostgreSQL
CREATE SEQUENCE serial START  4;

CREATE TABLE player(
	playerID int PRIMARY KEY DEFAULT nextval('serial'),
	name TEXT NOT NULL,
	dateofbirth DATE NOT NULL,
	
	-- Länderkürzel nach ISO 3166-1 A-3
	nationality TEXT NOT NULL,
	
	-- Defense -> D
	-- Attack -> A
	-- Mildfield -> M
	-- GOAL -> G
	fieldposition char(1) NOT NULL,
	CHECK (fieldposition IN ('D', 'A', 'M', 'G')),
	height DECIMAL(5,2) NOT NULL, 
	CHECK (height BETWEEN 150 AND 270)
	
);
```

```PostgreSQL
CREATE TABLE  playsFor(
	player int REFERENCES player(playerID), 
	team int REFERENCES team(teamID),
	since DATE NOT NULL,
	until DATE,
	shirtNumber int NOT NULL,
	CHECK (shirtNumber BETWEEN 1 AND 99),
	PRIMARY KEY (player,team,since)	
);
```

```PostgreSQL
CREATE TABLE match(
	homeTeamID int REFERENCES team(teamID),
	awayTeamID int REFERENCES team(teamID),
	CHECK (homeTeamID <> awayTeamID)
	playdon DATE NOT NULL ,
	homegoals int NOT NULL DEFAULT 0,
	awaygoals int NOT NULL DEFAULT 0
);
```

---
# Aufgabe 2



```sql
select distinct caughtby, country

from fish

natural join fishery

where fish.caughtby = fishery.name

order by caughtby asc
```


```sql
select distinct name,country

from fishery

join fish

on fish.caughtby = fishery.name

group by name,country

having count(fish.id) > 40

order by name asc

```


```sql
select name, taxID, count(customer) as customer_count

from wholesalers left join sold

on wholesalers.name = sold.whname

and wholesalers.taxID = sold.whtaxid

  

group by name, taxID

order by customer_count desc
```

```sql
select name, taxID, count(customer) as customer_count

from wholesalers left join sold

on wholesalers.name = sold.whname

and wholesalers.taxID = sold.whtaxid

group by name, taxID

having sum(sold.quantity) > 20000

  

order by customer_count desc
```

```sql
select name

from customer

where customer.name

NOT IN

(

select distinct sold.customer

from sold

)

AND customer.name NOT IN

(

select distinct distributor.customer

from distributor

)
```

```sql
select distributor.customer,

round(avg(distributor.unitprice),2) as unit_avg_price,

(

select sum(sold.quantity)

from sold

where sold.customer = distributor.customer

) as sum_sold

from distributor

group by distributor.customer

having avg(distributor.unitprice) > (select avg(unitprice) from distributor)
```

```sql
select c.name , round(avg(d.unitprice),2)

from customer c

join distributor d

on c.name = d.customer

join wholesalers w

on d.customer = c.name and d.whname = w.name

  

-- WAY 1

-- group by c.name

-- having count(distinct d.whname) = (

-- select count(distinct wh.name)

-- from wholesalers wh

-- where wh.country = c.country

-- )

-- order by c.name desc

  

-- WAY 2

where w.country = c.country and not exists (

select *

from wholesalers w1

where w1.country = c.country and not exists (

select *

from distributor d1

where d1.customer = c.name

and d1.whname = w1.name

and d1.whtaxid = w1.taxid

)

)

group by c.name

order by c.name desc;

--https://gregorulm.com/relational-division-in-sql-the-easy-way/
```
