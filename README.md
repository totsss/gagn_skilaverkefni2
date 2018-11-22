# gagn_skilaverkefni2

use 1608003640_northwind;


#1
SELECT ProductName, QuantityPerUnit FROM Products;



#2
SELECT ProductID, ProductName FROM Products
WHERE Discontinued = "False"
ORDER BY ProductName;



#3
SELECT ProductID, ProductName FROM Products
WHERE Discontinued = 1 
ORDER BY ProductName;



#4
SELECT ProductName, UnitPrice  FROM Products 
ORDER BY UnitPrice DESC;



#5
SELECT ProductID, ProductName, UnitPrice FROM Products
WHERE (((UnitPrice)<20) AND ((Discontinued)=False))
ORDER BY UnitPrice DESC;



#6
SELECT ProductName, UnitPrice FROM Products
WHERE (((UnitPrice)>=15 And (UnitPrice)<=25) 
AND ((Products.Discontinued)=False))
ORDER BY Products.UnitPrice DESC;



#7
SELECT DISTINCT ProductName, UnitPrice FROM Products
WHERE UnitPrice > (SELECT avg(UnitPrice) FROM Products)
ORDER BY UnitPrice;



#8
SELECT DISTINCT ProductName as Twenty_Most_Expensive_Products, UnitPrice FROM Products AS a
WHERE 20 >= (SELECT COUNT(DISTINCT UnitPrice)
                    FROM Products AS b
                    WHERE b.UnitPrice >= a.UnitPrice)
ORDER BY UnitPrice desc;



#9
SELECT Count(ProductName) FROM Products
GROUP BY Discontinued;



#10
SELECT ProductName,  UnitsOnOrder , UnitsInStock
FROM Products
WHERE (((Discontinued)=False) AND ((UnitsInStock)<UnitsOnOrder));



/*Naesta database.*/
use 1608003640_humanresources;



#1
SELECT FIRST_NAME, LAST_NAME, SALARY FROM employees 
WHERE SALARY > 
(SELECT salary FROM employees WHERE last_name = 'Bull');



#2
SELECT first_name, last_name FROM employees 
WHERE department_id 
IN (SELECT department_id FROM departments WHERE department_name='IT');



#3
SELECT first_name, last_name FROM employees 
WHERE manager_id in (select employee_id 
FROM employees WHERE department_id 
IN (SELECT department_id FROM departments WHERE location_id 
IN (select location_id from locations where country_id='US')));



#4
SELECT first_name, last_name FROM employees 
WHERE (employee_id IN (SELECT manager_id FROM employees));



#5
SELECT first_name, last_name, salary FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);






#6
SELECT location_id, street_address, city, state_province, country_name FROM locations
NATURAL JOIN countries;


#7
SELECT first_name, last_name, department_id, department_name FROM employees 
JOIN departments USING (department_id);


#8
SELECT e.first_name, e.last_name, e.job_id, e.department_id, d.department_name FROM employees e 
JOIN departments d 
ON (e.department_id = d.department_id) 
JOIN locations l ON 
(d.location_id = l.location_id) 
WHERE LOWER(l.city) = 'London';


#9
SELECT e.employee_id 'Emp_Id', e.last_name 'Employee', m.employee_id 'Mgr_Id', m.last_name 'Manager' 
FROM employees e 
join employees m 
ON (e.manager_id = m.employee_id);



#10
SELECT e.first_name, e.last_name, e.hire_date FROM employees e 
JOIN employees davies 
ON (davies.last_name = 'Jones') 
WHERE davies.hire_date < e.hire_date;


#6
SELECT department_name AS 'Department Name', 
COUNT(*) AS 'No of Employees' 
FROM departments 
INNER JOIN employees 
ON employees.department_id = departments.department_id 
GROUP BY departments.department_id, department_name 
ORDER BY department_name;
