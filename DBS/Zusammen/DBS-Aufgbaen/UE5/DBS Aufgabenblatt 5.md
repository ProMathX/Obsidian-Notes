## Aufgabe 1

1) SQL tabelle zu season

```SQL 
CREATE TABLE season(
	seasonID SERIAL PRIMARY KEY,
	startdate DATE,
	enddate DATE,
	commonname VARCHAR(12) NOT NULL UNIQUE 
);
```

```SQL 
CREATE TABLE league(
	leagueID SERIAL PRIMARY KEY,
	name varchar(12),
	hierarchylevel int NOT NULL
);
```

```SQL 
CREATE TABLE team(
	teamID SERIAL PRIMARY KEY,
	name TEXT NOT NULL,
	abbreviation varchar(3) NOT NULL UNIQUE,
	stadium varchar(110) NOT NULL
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

```SQL 
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

```SQL
CREATE TABLE match(
	homeTeamID int REFERENCES team(teamID),
	awayTeamID int REFERENCES team(teamID),
	CHECK (homeTeamID <> awayTeamID)
	playdon DATE NOT NULL ,
	homegoals int NOT NULL DEFAULT 0,
	awaygoals int NOT NULL DEFAULT 0
);
```



