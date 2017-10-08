__1)__ List each country name where the population is larger than that of 'Russia'.

SELECT name FROM world  
  WHERE population >  
     (SELECT population FROM world  
      WHERE name='Russia')  

__2)__ Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

SELECT name  
FROM world  
WHERE continent = 'Europe' and GDP/population >   
(SELECT GDP/population FROM world where name = 'United Kingdom')  

__3)__ List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

SELECT name, continent  
FROM world  
WHERE continent in (SELECT continent from world   
  where name = 'Argentina' or name = 'Australia')  
ORDER BY name;  

__4)__ Which country has a population that is more than Canada but less than Poland? Show the name and the population.

SELECT name, population  
FROM world  
WHERE population >   
(SELECT population FROM world Where name = 'Canada') and  
population < (SELECT population FROM world Where name = 'Poland')  

__5)__ Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.

SELECT w.name, CONCAT(ROUND((w.population/w1.population*100)), '%')  
FROM world w, (SELECT population  from world where name = 'Germany') w1  
WHERE w.continent = 'Europe'  

__6)__ Which countries have a GDP greater than every country in Europe? [Give the name only.] (Some countries may have NULL gdp values)

SELECT w.name  
FROM world w  
WHERE w.GDP > ALL(SELECT GDP  from world WHERE continent ='Europe'and GDP >0)  

__7)__ Find the largest country (by area) in each continent, show the continent, the name and the area:

SELECT continent, name, area FROM world x  
  WHERE area >= ALL  
    (SELECT area FROM world y  
        WHERE y.continent=x.continent  
          AND area>0)  

__8)__ List each continent and the name of the country that comes first alphabetically.

SELECT continent, name  
FROM world w1  
WHERE w1.name <= ALL(SELECT name FROM world w WHERE w.continent = w1.continent)  

__9)__ Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.

SELECT name, continent, population  
FROM world  
WHERE continent not in (SELECT continent  
FROM world  
WHERE name = ANY(SELECT name FROM world WHERE population > 25000000));  

__10)__ Some countries have populations more than three times that of any of their neighbours (in the same continent). Give the countries and continents.

SELECT w1.name, w1.continent  
FROM world w1  
Where w1.population > ALL(SELECT 3* w2.population FROM world w2 where    w1.continent = w2.continent and w1.name <>w2.name )  
