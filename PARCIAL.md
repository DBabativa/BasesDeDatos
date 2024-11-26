# Base De Datos

# Parcial consultas Mysql en HackerRank

### 1. Consulta "1.Weather Observation Station 9"

  ```sql
select distinct CITY from STATION 
WHERE CITY not like 'A%'
AND CITY  not like 'E%'
AND CITY not like 'I%'
AND CITY not like 'O%'
AND CITY not like 'U%';
  ```

![image](https://github.com/user-attachments/assets/b1d669d2-f303-475c-9eba-382add65040e)

### 2. Consulta "2.Weather Observation Station 15" 

  ```sql
SELECT ROUND(LONG_W, 4) AS Longitud_Occidental
FROM STATION WHERE LAT_N < 137.2345
ORDER BY LAT_N DESC LIMIT 1;
  ```

![image](https://github.com/user-attachments/assets/e8bd5bf4-4349-475b-85b0-a93424141457)


### 3. Consulta "3.Weather Observation Station 8"

```sql
SELECT DISTINCT City FROM STATION
WHERE (City LIKE 'A%' OR City LIKE 'E%' OR City LIKE 'I%' OR City LIKE 'O%' OR City LIKE 'U%')
  AND (City LIKE '%A' OR City LIKE '%E' OR City LIKE '%I' OR City LIKE '%O' OR City LIKE '%U');
```
![image](https://github.com/user-attachments/assets/e53553bb-0df1-40cc-a251-584578e21750)

# Consultas Básicas Parcial

### 1. Encuentra los departamentos que tienen más de 2300 empleados. Organizalos de mayor a menor en cantidad de empleados 
   ```sql
   SELECT d.dept_name AS Departamento,
COUNT(de.emp_no) AS Cantidad_Empleados
FROM  departments d JOIN dept_emp de ON d.dept_no = de.dept_no
GROUP BY d.dept_name HAVING  COUNT(de.emp_no) > 2300
ORDER BY Cantidad_Empleados DESC;
   ```

![image](https://github.com/user-attachments/assets/1af03715-f03e-49b0-af42-1a3caceeb310)

### 2. Calcula el salario promedio por cada título. Organizalos en orden alfabético.  
   ```sql
   SELECT t.title AS Titulo, ROUND(AVG(s.salary), 2) AS Salario_Promedio
FROM titles t JOIN salaries s ON t.emp_no = s.emp_no
GROUP BY t.title ORDER BY Titulo ASC;
   ```

![image](https://github.com/user-attachments/assets/805b425c-2711-44a7-9914-3b527aecdf03)

###  3. Cuenta cuántos empleados hay en total en la base de datos cuyo nombre empiece por 'A' y el apellido por 'R'.  
   ```sql
   SELECT COUNT(*) AS Total_Empleados FROM employees
WHERE first_name LIKE 'A%' AND last_name LIKE 'R%';
   ```

![image](https://github.com/user-attachments/assets/cccf48ab-02bd-4bb5-b10d-0e783128e78d)

### 4. Lista los 10 empleados con los salarios más altos.  
   ```sql
   SELECT e.emp_no AS Numero_Empleado,
    e.first_name AS Nombre,
    e.last_name AS Apellido,
    s.salary AS Salario
FROM employees e
JOIN  salaries s ON e.emp_no = s.emp_no
ORDER BY s.salary DESC LIMIT 10;
   ```

![image](https://github.com/user-attachments/assets/5f1c0bc6-760b-4092-8b3e-415f2dda94ef)

### 5. Encuentra a todos los empleados cuyo apellido tiene la silaba con "ata" y fueron contratados antes del '1986-09-08'
   ```sql
   SELECT emp_no AS Numero_Empleado,
    first_name AS Nombre,
    last_name AS Apellido
    FROM employees WHERE last_name LIKE '%ata' and hire_date < '1986-09-08';
   ```
![image](https://github.com/user-attachments/assets/9b5dbcf3-ffb2-4b42-9f17-d97cf9b451dd)


### 6. Encuentra todos los títulos únicos en la base de datos que tengan una fecha de inicio mayor a '1994-08-29'. Ordenalos alfabéticamente en orden descendente.
   ```sql
   SELECT distinct title FROM titles WHERE from_date > '1994-08-29' ORDER BY title DESC;
   ```

![image](https://github.com/user-attachments/assets/c4359ea5-404b-42d4-8524-f3bb1ff3f774)

### 7. Encuentra a todos los empleados cuyos salarios son mayores a 65.000 y su fecha de entrada es mayor a '1999-09-27'
   ```sql
  SELECT e.emp_no AS Numero_Empleado, e.first_name AS Nombre, e.last_name AS Apellido,
  s.salary AS Salario, e.hire_date AS Fecha_Contratacion
  FROM employees e JOIN salaries s ON e.emp_no = s.emp_no
  WHERE s.salary > 65000 AND e.hire_date > '1999-09-27';
   ```
![image](https://github.com/user-attachments/assets/2a0726a3-13e0-4c93-879c-1cc1bbefe983)

## Consultas Nivel Medio (Usando JOIN)

### 8. Encuentra el nombre y apellido de los empleados y sus títulos actuales, organizalos alfabeticamente por el apellido. Utilicen la fecha más grande.
   ```sql
   SELECT 
    e.first_name AS Nombre,
    e.last_name AS Apellido,
    t.title AS Titulo
FROM employees e
JOIN titles t ON e.emp_no = t.emp_no
WHERE t.to_date = (
SELECT MAX(to_date) FROM titles t2 
WHERE t2.emp_no = t.emp_no
    )
ORDER BY 
    e.last_name ASC;
   ```
![image](https://github.com/user-attachments/assets/91a26d6a-f474-4a79-ac17-e44a85edb756)

### 9. Lista a todos los empleados y, si están asignados a un departamento, muestra el número del departamento.  
   ```sql
   SELECT 
    e.emp_no AS Numero_Empleado,
    e.first_name AS Nombre,
    e.last_name AS Apellido,
    de.dept_no AS Numero_Departamento
FROM employees e
LEFT JOIN dept_emp de ON e.emp_no = de.emp_no
ORDER BY e.emp_no;
   ```

![image](https://github.com/user-attachments/assets/e0d0e751-2d50-4b4c-b8f1-c0be0ec5a6a6)



### 10. Listar los títulos de los empleados con sus nombres completos, fecha de nacimiento, título, número de empleado y genero
```sql

```


### 11. Lista todos los departamentos, incluso si no tienen empleados asignados actualmente.  
   ```sql
   
   ```

### 12. Listar los nombres de departamentos junto con el número de empleados que tienen un salario mayor a 70.000 
   ```sql
   
   ```

