# SQL Zoo

## Tutorials: Learn SQL step by step

### 0 SELECT basics

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