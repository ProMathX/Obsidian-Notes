## Aufgabe 1

1) SQL tabelle zu season


```SQL 
CREATE TABLE season(
	seasonID int PRIMARY KEY,
	startdate DATE_PART('month','year', datum),
	enddate DATE_PART('month','year', datum),
	commonname NOT NULL VARCHAR(12) UNIQUE 
);
```

```SQL 
CREATE TABLE league(
	leagueID int PRIMARY KEY,
	name varchar(12),
	hierarchylevel NOT NULL int
);
```

```SQL 
CREATE TABLE team(
	teamID int PRIMARY KEY,
	name varchar(24),
	abbreviation NOT NULL varchar(85) UNIQUE,
	stadium NOT NULL varchar(110),
);
```

[longest city name ](https://en.wikipedia.org/wiki/Taumatawhakatangi%C2%ADhangakoauauotamatea%C2%ADturipukakapikimaunga%C2%ADhoronukupokaiwhen%C2%ADuakitanatahu?useskin=vector)

[longest stadium name](https://en.wikipedia.org/wiki/ACA%E2%80%93VDCA_Cricket_Stadium?useskin=vector)

```SQL 
CREATE TABLE belongsTOLeague(
	teamID int,
	seasonID int,
	leagueID int,
	
	FOREIGN KEY (teamID) REFERENCES team(teamID),
	FOREIGN KEY(seasonID) REFERENCES season(seasonID),
	FOREIGN KEY (leagueID) REFERENCES league(leagueID)
);
```



```SQL
CREATE TABLE player(
	playerID int PRIMARY KEY,
	name NOT NULL varchar(100),
	dateofbirth NOT NULL
	
	-- Länderkürzel
	nationality NOT NULL 
	fieldposition NOT NULL
	height NOT NULL int
);
```






