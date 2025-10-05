# SQL Zoo

## Tutorials: Learn SQL step by step

### SELECT basics

#### 1. Introducing the world table of countries

Modify it to show the population of Germany

```SQL
SELECT population FROM world
  WHERE name = 'Germany'
```

#### 2. Scandinavia

Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.

```SQL
SELECT name, population FROM world
  WHERE name IN ('Sweden','Norway','Denmark');
```

#### 3. Just the right size

```SQL
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
```

### SELECT Quiz

### SELECT from WORLD Tutorial

#### 1.

```SQL
SELECT name, continent, population FROM world;
```

#### 2.

```SQL
SELECT name FROM world
WHERE population >= 200000000;
```

#### 3.

```SQL
SELECT name, gdp/population AS per_capita_GDP FROM world
WHERE population >= 200000000;
```

#### 4.

```SQL
SELECT name, population/1000000 AS people
FROM world
WHERE continent = 'South America';
```

#### 5.

```SQL
SELECT name, population FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

#### 6.

```SQL
SELECT name FROM world
WHERE name LIKE '%United%';
```

#### 7.

Show the countries that are big by area or big by population. Show name, population and area.

```SQL
SELECT name, population, area FROM world
WHERE population > 250000000 OR area > 3000000;
```

#### 8.

Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both. Show name, population and area.

```SQL
SELECT name, population, area FROM world
WHERE population > 250000000 XOR area > 3000000;
```

#### 9.

For Americas show population in millions and GDP in billions both to 2 decimal places.

```SQL
SELECT name, ROUND(population/1000000,2), ROUND(gdp/1000000000,2)
FROM world
WHERE continent = 'South America';
```

#### 10.

Show per-capita GDP for the trillion dollar countries to the nearest $1000.

```SQL
SELECT name, ROUND((gdp/population),-3) AS per_capita_GDP FROM world
WHERE gdp >= 1000000000000;
```

#### 11.

Show the name and capital where the name and the capital have the same number of characters.

```SQL
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

#### 12.

Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.

```SQL
SELECT name, capital
FROM world
WHERE LEFT(name,1) = LEFT(capital,1) AND name != capital;
```

#### 13.

Find the country that has all the vowels and no spaces in its name.

```SQL
SELECT name
   FROM world
WHERE name LIKE '%a%'
  AND name LIKE '%e%'
  AND name LIKE '%i%'
  AND name LIKE '%o%'
  AND name LIKE '%u%'
  AND name NOT LIKE '% %';
```

### SELECT from WORLD Tutorial

#### 1.

```SQL
SELECT name, continent, population FROM world;
```

#### 2.

```SQL
SELECT name FROM world
WHERE population >= 200000000
```

#### 3.

```SQL
SELECT name, gdp/population AS per_capita_GDP FROM world
WHERE population >= 200000000
```

#### 4.

```SQL
SELECT name, population/1000000 AS people
FROM world
WHERE continent = 'South America';
```

#### 5.

```SQL
SELECT name, population FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

#### 6.

```SQL
SELECT name FROM world
WHERE name LIKE '%United%';
```

#### 7.

```SQL
SELECT name, population, area FROM world
WHERE population > 250000000 OR area > 3000000;
```

#### 8.

```SQL
SELECT name, population, area FROM world
WHERE population > 250000000 XOR area > 3000000;
```

#### 9.

```SQL
SELECT name, ROUND(population/1000000,2), ROUND(gdp/1000000000,2)
FROM world
WHERE continent = 'South America';
```

#### 10.

```SQL
SELECT name, ROUND((gdp/population),-3) AS per_capita_GDP FROM world
WHERE gdp >= 1000000000000;
```

#### 11.

```SQL
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

#### 12.

```SQL
SELECT name, capital
FROM world
WHERE LEFT(name,1) = LEFT(capital,1) AND name != capital;
```

#### 13.

```SQL
SELECT name
   FROM world
WHERE name LIKE '%a%'
  AND name LIKE '%e%'
  AND name LIKE '%i%'
  AND name LIKE '%o%'
  AND name LIKE '%u%'
  AND name NOT LIKE '% %';
```

### SELECT from noble

#### 1.

```SQL
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```

#### 2.

```SQL
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'literature'
```

#### 3.

```SQL
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```

#### 4.

```SQL
SELECT winner
FROM nobel
WHERE yr >= 2000
AND subject = 'peace';
```

#### 5.

```SQL
SELECT *
FROM nobel
WHERE subject = 'literature'
AND yr >= 1980 AND yr <= 1989;
```

#### 6.

```SQL
SELECT * FROM nobel
WHERE winner IN ('Theodore Roosevelt','Thomas Woodrow Wilson','Jimmy Carter','Barack Obama')
```

#### 7.

```SQL
SELECT winner FROM nobel
WHERE winner LIKE "John %";
```

#### 8.

```SQL
SELECT yr, subject, winner FROM nobel
WHERE (subject = 'physics' AND yr = 1980) OR (subject = 'chemistry' AND yr = 1984);
```

#### 9.

```SQL
SELECT * FROM nobel
WHERE yr = 1980 AND subject NOT IN ('chemistry','medicine');
```

#### 10.

```SQL
SELECT * FROM nobel
WHERE (subject = 'medicine' AND yr < 1910) OR (subject = 'literature' AND yr >= 2004);
```

#### 11.

```SQL
SELECT * FROM nobel
WHERE winner = 'PETER GRÜNBERG';
```

#### 12.

```SQL
SELECT * FROM nobel
WHERE winner = "EUGENE O'NEILL";
```

#### 13.

```SQL
SELECT winner, yr, subject FROM nobel
WHERE winner LIKE 'Sir %'
ORDER BY yr DESC, winner;
```

#### 14.

```SQL
SELECT winner, subject
  FROM nobel
 WHERE yr=1984
 ORDER BY subject IN ('physics','chemistry'),subject,winner
```

### SELECT in SELECT

#### 1.

```SQL
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```

#### 2.

```SQL
SELECT name FROM world
WHERE continent = 'Europe' AND (gdp/population) >
(SELECT (gdp/population) FROM world WHERE name = 'United Kingdom');
```

#### 3.

```SQL
SELECT name, continent FROM world
WHERE continent IN (SELECT continent FROM world
WHERE name IN ('Argentina','Australia')) ORDER BY name;
```

#### 4.

```SQL
SELECT name, population FROM world
WHERE population > (SELECT population FROM world WHERE name = 'United Kingdom')
AND population < (SELECT population FROM world WHERE name = 'Germany');
```

#### 5.

```SQL
SELECT name, CONCAT(CAST(ROUND(population / (SELECT population/100 FROM world WHERE name = 'Germany'),0) AS VARCHAR(10)),'%')  AS percentage
FROM world
WHERE continent = 'Europe';
```

#### 6.

```SQL
SELECT name FROM world WHERE gdp > (SELECT MAX(gdp) FROM world WHERE continent = 'Europe');
```

#### 7.

```SQL
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent)
```

#### 8.

```SQL
SELECT continent, name FROM world x
WHERE name <= ALL(SELECT name FROM world y WHERE y.continent=x.continent);
```

#### 9.

```SQL
SELECT name, continent, population FROM world
WHERE continent IN
(SELECT continent FROM world x
WHERE population >= ALL(SELECT population FROM world y
WHERE x.continent = y.continent) AND population <= 25000000);
```

#### 10.

```SQL
SELECT name, continent FROM world z
WHERE population/3 >
(SELECT MAX(population) FROM world x
WHERE population < (SELECT MAX(population) FROM world y WHERE x.continent=y.continent AND y.continent =z.continent)
GROUP BY continent);
```

### SUM and COUNT

#### 1.

```SQL
SELECT SUM(population)
FROM world
```

#### 2.

```SQL
SELECT continent FROM world
GROUP BY continent
```

#### 3.

```SQL
SELECT SUM(gdp) FROM world WHERE continent = 'Africa';
```

#### 4.

```SQL
SELECT COUNT(name) FROM world WHERE area>1000000;
```

#### 5.

```SQL
SELECT SUM(population) FROM world WHERE name IN ('Estonia', 'Latvia', 'Lithuania');
```

#### 6.

```SQL
SELECT continent, COUNT(name)
FROM world
GROUP BY continent;
```

#### 7.

```SQL
SELECT continent, COUNT(name)
FROM world
WHERE population >= 10000000
GROUP BY continent;
```

#### 8.

```SQL
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) > 100000000;
```

### SUM and COUNT on nobel table

#### 1.

```SQL
SELECT COUNT(winner) FROM nobel
```

#### 2.

```SQL
SELECT DISTINCT subject FROM nobel;
```

#### 3.

```SQL
SELECT COUNT(winner) FROM nobel WHERE subject = 'Physics';
```

#### 4.

```SQL
SELECT subject, COUNT(winner) FROM nobel
GROUP BY subject;
```

#### 5.

```SQL
SELECT subject, MIN(yr) FROM nobel
GROUP BY subject;
```

#### 6.

```SQL
SELECT subject, COUNT(winner) FROM nobel
WHERE yr = 2000
GROUP BY subject;
```

#### 7.

```SQL
SELECT subject, COUNT(DISTINCT winner) FROM nobel
GROUP BY subject;
```

#### 8.

```SQL
SELECT subject, COUNT(DISTINCT yr) FROM nobel
GROUP BY subject;
```

#### 9.

```SQL
SELECT yr FROM nobel
WHERE subject = 'Physics'
GROUP BY yr
HAVING count(winner) = 3;
```

#### 10.

```SQL
SELECT winner FROM nobel
GROUP BY winner
HAVING COUNT(winner) > 1;
```

#### 11.

```SQL
SELECT winner FROM nobel
GROUP BY winner
HAVING COUNT(DISTINCT subject) > 1;
```

#### 12.

```SQL
SELECT yr, subject FROM nobel
WHERE yr >= 2000
GROUP BY yr, subject
HAVING COUNT(winner) = 3;
```

#### 1.

```SQL

```

#### 1.

```SQL

```

### The JOIN operation

#### 1.

```SQL
SELECT matchid, player FROM goal
WHERE teamid = 'GER';
```

#### 2.

```SQL
SELECT id,stadium,team1,team2
FROM game
WHERE id = 1012;
```

#### 3.

```SQL
SELECT player,teamid,stadium,mdate
FROM game JOIN goal ON (id=matchid)
WHERE teamid = 'GER';
```

#### 4.

```SQL
SELECT team1, team2, player FROM game
JOIN goal ON id=matchid
WHERE player LIKE 'Mario%';
```

#### 5.

```SQL
SELECT player, teamid, coach, gtime
FROM goal JOIN eteam ON teamid = id
WHERE gtime<=10
```

#### 6.

```SQL
SELECT mdate, teamname
FROM eteam JOIN game ON team1=eteam.id
WHERE eteam.coach = 'Fernando Santos';
```

#### 7.

```SQL
SELECT player FROM goal JOIN game ON matchid = id
WHERE stadium = 'National Stadium, Warsaw';
```

#### 8.

```SQL
SELECT DISTINCT player FROM goal
WHERE matchid in (SELECT DISTINCT matchid FROM goal WHERE teamid = 'GER')
AND teamid != 'GER';
```

Denne gir riktig svar, men den under som gir akkurat samme svar kommer opp
som feil.

```SQL
SELECT player
  FROM game JOIN goal ON matchid = id
 WHERE (team1 = "GER" OR team2 = "GER")
   AND teamid != 'GER'
GROUP BY player
```

#### 9.

```SQL
SELECT teamname, COUNT(player)
FROM eteam JOIN goal ON id=teamid
GROUP BY teamname
```

#### 10.

```SQL
SELECT stadium, COUNT(player)
FROM game JOIN goal ON matchid = id
GROUP BY stadium;
```

#### 11.

```SQL
SELECT matchid, mdate, COUNT(player)
FROM game JOIN goal ON matchid = id
WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid, mdate;
```

#### 12.

```SQL
SELECT matchid, mdate, COUNT(player)
FROM game JOIN goal ON id=matchid
WHERE teamid = 'GER'
GROUP BY matchid, mdate;
```

#### 13.

Her må vi bruke en LEFT JOIN fordi kamper der det ikke var scoret noen mål
blir ikke med. Så vi får ikke 0-0 kampene.

```SQL
SELECT mdate, team1,
SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) score1,
team2,
SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) score2
FROM game LEFT JOIN goal ON matchid = id
GROUP BY matchid,mdate,team1,team2
ORDER BY mdate,matchid,team1,team2
```
