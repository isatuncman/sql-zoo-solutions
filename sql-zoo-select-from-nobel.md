__1)__ Change the query shown so that it displays Nobel prizes for 1950.

SELECT yr, subject, winner  
FROM nobel  
WHERE yr = 1950;  

 __2)__ Show who won the 1962 prize for Literature.

SELECT winner  
FROM nobel  
WHERE yr = 1962  
AND subject = 'Literature';  

__3)__ Show the year and subject that won 'Albert Einstein' his prize.

SELECT yr, subject  
FROM nobel  
WHERE winner = 'Albert Einstein' ;  

__4)__ Give the name of the 'Peace' winners since the year 2000, including 2000.

SELECT winner  
FROM nobel  
WHERE subject = 'Peace' and yr >=2000  

__5)__ Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive.

SELECT *  
FROM nobel  
WHERE subject = 'Literature' and yr >=1980 and yr <=1989  

__6)__ Show all details of the presidential winners:

Theodore Roosevelt,
Woodrow Wilson,
Jimmy Carter,
Barack Obama

SELECT * FROM nobel  
 WHERE winner in ('Theodore Roosevelt',  
'Woodrow Wilson',  
'Jimmy Carter',  
'Barack Obama')  

__7)__ Show the winners with first name John

SELECT winner  
FROM nobel  
WHERE winner LIKE 'John%'  

__8)__ Show the year, subject, and name of Physics winners for 1980 together with the Chemistry winners for 1984.

SELECT *  
FROM nobel  
WHERE (subject = 'Physics' and yr =1980) OR (subject = 'Chemistry' and yr = 1984);  

__9)__ Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine

SELECT * FROM nobel  
WHERE yr = 1980 and subject not in ('Chemistry', 'Medicine');  

__10)__ Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004)

SELECT *  
FROM nobel  
WHERE (yr <1910 and subject = 'Medicine') OR (yr >=2004 and subject = 'Literature');  

__11)__ Find all details of the prize won by PETER GRÜNBERG

SELECT *  
FROM nobel  
WHERE winner LIKE 'PETER GR_NBERG';  

__12)__ Find all details of the prize won by EUGENE O'NEILL

SELECT *  
FROM nobel  
WHERE winner = 'EUGENE O''NEILL';  

__13)__ List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.

SELECT winner, yr, subject  
FROM nobel  
WHERE winner LIKE 'Sir%'  
ORDER BY yr DESC, winner ;  

__14)__ Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.

SELECT winner, subject  
  FROM nobel  
 WHERE yr=1984  
 ORDER BY subject IN ('Chemistry','Physics') , subject, winner;  
