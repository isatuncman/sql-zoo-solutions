__1)__ List the teachers who have NULL for their department.

SELECT t.name
FROM teacher t
WHERE t.dept IS NULL ;

__2)__ Note the INNER JOIN misses the teachers with no department and the departments with no teacher.

SELECT teacher.name, dept.name
 FROM teacher INNER JOIN dept
           ON (teacher.dept=dept.id)

__3)__ Use a different JOIN so that all teachers are listed.

SELECT t.name, dept.name
FROM teacher t LEFT JOIN dept ON dept.id = t.dept;

__4)__ Use a different JOIN so that all departments are listed.

SELECT t.name, d.name
FROM teacher t RIGHT JOIN dept d ON d.id =t.dept;

__5)__ Use COALESCE to print the mobile number. Use the number '07986 444 2266' if there is no number given. Show teacher name and mobile number or '07986 444 2266'

SELECT t.name, COALESCE(t.mobile,  '07986 444 2266')
FROM teacher t;

__6)__ Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.

SELECT t.name, COALESCE(d.name, 'None')
FROM teacher t LEFT JOIN dept d ON d.id = t.dept;

__7)__ Use COUNT to show the number of teachers and the number of mobile phones.

SELECT COUNT(t.name), COUNT(t.mobile)
FROM teacher t;

__8)__ Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.

SELECT dept.name, COUNT(t.name)
FROM teacher t RIGHT JOIN dept ON dept.id = t.dept
GROUP BY dept.name

__9)__ Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.

SELECT name,
CASE
WHEN t.dept = 1 or t.dept =2 THEN 'Sci' ELSE 'Art'
END as type
FROM teacher t;

__10)__ Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise.

SELECT name,
CASE
WHEN t.dept = 1 OR t.dept =2 THEN 'Sci'
WHEN t.dept = 3 THEN 'Art'
ELSE 'None'
END as type
FROM teacher t;
