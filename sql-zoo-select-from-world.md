__2)__ Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

SELECT name FROM world  
WHERE population >=200000000;  

__3)__ Give the name and the per capita GDP for those countries with a population of at least 200 million.

SELECT name, GDP/population as per_capita_GDP  
FROM world  
WHERE population >= 200000000;  

__4)__ Show the name and population in millions for the countries of the continent 'South America'. Divide the population by 1000000 to get population in millions.

SELECT name, population/1000000  
FROM world w  
WHERE w.continent = 'South America';  

__5)__ Show the name and population for France, Germany, Italy

SELECT name, population  
FROM world  
WHERE name IN ('France', 'Germany', 'Italy');  

__6)__ Show the countries which have a name that includes the word 'United'

SELECT name  
FROM world  
WHERE name LIKE '%United%';  

__7)__ Two ways to be big: A country is big if it has an area of more than 3 million sq km or it has a population of more than 250 million.
Show the countries that are big by area or big by population. Show name, population and area.

SELECT name, population, area  
FROM world  
WHERE area >3000000 or population > 250000000;  

__8)__ Exclusive OR (XOR). Show the countries that are big by area or big by population but not both. Show name, population and area.

SELECT name, population, area  
FROM world  
WHERE area >3000000 XOR population > 250000000;  

__9)__ Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. Use the ROUND function to show the values to two decimal places.
For South America show population in millions and GDP in billions both to 2 decimal places.

SELECT name, round(population/1000000,2),   round(GDP/1000000000,2)  
FROM world  
WHERE continent = 'South America';  

__10)__ Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

Show per-capita GDP for the trillion dollar countries to the nearest $1000

SELECT name, ROUND(GDP/population, -3)  
FROM world  
WHERE GDP >=1000000000000;  

__11)__ Show the name and capital where the name and the capital have the same number of characters.

SELECT name, capital  
  FROM world  
 WHERE LENGTH(name) = LENGTH(capital)  

__12)__ Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.

SELECT name, capital  
FROM world  
WHERE LEFT(name, 1) = LEFT(capital, 1) AND name <> capital  

__13)__ Find the country that has all the vowels and no spaces in its name.

SELECT name  
   FROM world  
WHERE name LIKE '%a%' and name LIKE '%e%' and   
name LIKE '%i%' and name LIKE '%o%' and name LIKE '%u%'  
  AND name NOT LIKE '% %' ;  
