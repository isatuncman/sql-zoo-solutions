__1)__ How many stops are in the database.

SELECT COUNT(id)
FROM stops

__2)__ Find the id value for the stop 'Craiglockhart'

SELECT ID
FROM stops
WHERE name = 'Craiglockhart'

__3)__ Give the id and the name for the stops on the '4' 'LRT' service.

SELECT ID, name
FROM stops, route
WHERE stops.id = route.stop and route.company = 'LRT' and route.num = 4

__4)__ The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.

SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*) =2;

__5)__ Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.

SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num), stops s1, stops s2
WHERE s1.id = a.stop and s1.name = 'Craiglockhart' and s2.id = b.stop and s2.name = 'London Road';

__6)__ The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'

SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' and stopb.name = 'London Road';

__7)__ Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith')

SELECT DISTINCT a.company, a.num
FROM route a JOIN route b
ON a.company = b.company and a.num = b.num
WHERE a.stop = 115 and b.stop = 137

__8)__ Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'

SELECT a.company, a.num
FROM route a, route b, stops s1, stops s2
WHERE a.company = b.company and a.num = b.num and s1.id = a.stop and s2.id = b.stop and s1.name ='Craiglockhart'  and s2.name =  'Tollcross';

__9)__ Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.

SELECT s2.name, a.company, a.num
FROM route a, route b, stops s1, stops s2
WHERE a.company = b.company and a.num = b.num and b.stop = s1.id and s1.name = 'Craiglockhart' and a.stop = s2.id

__10)__ Find the routes involving two buses that can go from Craiglockhart to Sighthill.
Show the bus no. and company for the first bus, the name of the stop for the transfer,
and the bus no. and company for the second bus.

SELECT DISTINCT a.num, a.company, s3.name, d.num, d.company
FROM route a, route b, route c, route d, stops s1, stops s2, stops s3, stops s4
WHERE a.stop = s1.id and d.stop = s4.id  and
s1.name = 'Craiglockhart' and s4.name = 'Sighthill' and
a.company = b.company and a.num = b.num and
c.company = d.company and c.num = d.num and
b.stop = c.stop and c.stop = s3.id and b.stop = s2.id
__ORDER BY LENGTH(a.num), b.num, s3.name, LENGTH(d.num), c.num__
