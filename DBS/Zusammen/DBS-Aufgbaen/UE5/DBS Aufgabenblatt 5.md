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
	nationality char(3) NOT NULL,
	
	-- Defense -> D
	-- Attack -> A
	-- Mildfield -> M
	fieldposition char(1) NOT NULL,
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
	nationality TEXT NOT NULL,
	shirtNumber int NOT NULL UNIQUE,
	CHECK (shirtNumber BETWEEN 1 AND 99)	
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



