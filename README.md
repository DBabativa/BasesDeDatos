# Base De Datos

# Taller Consultas basicas MYSQL

## Consultas Básicas

**1. Selección de países en el continente 'Asia'**

**Álgebra relacional**:

$$
\sigma_{\text{Continent} = 'Asia'}(\text{Country})
$$

**SQL equivalente**:

```sql
SELECT * from country WHERE Continent = 'ASIA';
```

![image](https://github.com/user-attachments/assets/cbf8aa53-326d-4f7e-84fe-1862e720de5c)


**2. Contar el número total de ciudades**

**Álgebra relacional**:  

$$
\text{COUNT}(\text{City})
$$

**SQL equivalente**:  
```sql
SELECT distinct COUNT(Name) FROM CITY; 
```

![image](https://github.com/user-attachments/assets/e00e986d-a6c6-4464-b93e-f82ef8de895b)

**3. Listar todos los idiomas únicos en la tabla CountryLanguage**

**Álgebra relacional**:  

$$
\pi_{\text{Language}}(\text{CountryLanguage})
$$

**SQL equivalente**:  
```sql
SELECT Language FROM countrylanguage;
```

![image](https://github.com/user-attachments/assets/2101dcea-5c52-40b2-8461-58fdf6c3fd1d)

**4. Selección de países con población mayor a 100 millones**

**Álgebra relacional**:  

$$
\sigma_{\text{Population} > 100000000}(\text{Country})
$$

**SQL equivalente**:  
```sql
select * from country where Population>100000000;
```

![image](https://github.com/user-attachments/assets/e948257e-264e-4a90-b211-717bcc95934e)

**5. Listar nombres de países y continentes ordenados alfabéticamente por nombre de país**

**Álgebra relacional**:  

$$
\pi_{\text{Name}, \text{Continent}}(\text{Country}) \text{ ORDER BY Name}
$$

**SQL equivalente**:  
```sql
Select Name, continent From Country order by Name; 
```

![image](https://github.com/user-attachments/assets/38aaae18-d183-4f53-a6f8-666f7fe44612)

**6. Obtener la ciudad con mayor población**

**Álgebra relacional**:  

$$
\text{MAX}(\pi_{\text{Population}}(\text{City}))
$$

**SQL equivalente**:  
```sql
Select Name, Population From city order by Population desc limit 1;
```
![image](https://github.com/user-attachments/assets/634b3771-2355-456d-8449-99edc523b359)


**7. Selección de países que tienen 'Republic' en su nombre**

**Álgebra relacional**:  

$$
\sigma_{\text{Name LIKE '%Republic%'}}(\text{Country})
$$

**SQL equivalente**:  
```sql
SELECT Name FROM country where Name LIKE '%Republic%';
```

![image](https://github.com/user-attachments/assets/9cedcd6b-2ac7-4d1e-8f09-2e110fea1cc9)


**8. Listar los 5 países más poblados**

**Álgebra relacional**:  

$$
\pi_{\text{Name, Population}}(\text{Country}) \text{ ORDER BY Population DESC LIMIT 5}
$$

**SQL equivalente**:  
```sql
Select Name, Population From country order by Population desc limit 5;
```

![image](https://github.com/user-attachments/assets/a24f965c-f6c8-4715-81e6-1c3e463d9e39)


**9. Calcular la población promedio de los países en el continente 'Europe'**

**Álgebra relacional**:  

$$
\text{AVG}(\pi_{\text{Population}}(\sigma_{\text{Continent} = 'Europe'}(\text{Country})))
$$

**SQL equivalente**:  
```sql
Select AVG (Population) From country Where continent = 'Europe';
```
![image](https://github.com/user-attachments/assets/aa7c73c9-d412-48e0-8e9e-d066643e284e)


**10. Selección de idiomas con más del 10% de la población mundial que los habla**

**Álgebra relacional**:  

$$
\sigma_{\text{Percentage} > 10}(\text{CountryLanguage})
$$

**SQL equivalente**:  
```sql
SELECT * FROM countrylanguage WHERE Percentage > 10;
```

![image](https://github.com/user-attachments/assets/c21df7ab-d191-4925-ba4a-e89a1af36ef5)

## Consultas de Nivel Medio

**1. Encontrar los 5 países más poblados por continente**

**Álgebra relacional**:  

$$
\pi_{\text{Name, Population}}(\text{Country}) \text{ GROUP BY Continent ORDER BY Population DESC LIMIT 5}
$$

**SQL equivalente**:  
```sql
SELECT Continent, Name, Population FROM country AS c
WHERE Population = (SELECT MAX(Population)
    FROM country
    WHERE Continent = c.Continent)
ORDER BY Population DESC LIMIT 5;
```

![image](https://github.com/user-attachments/assets/a41e3377-b826-4674-b9dd-6c467028a509)

**2. Listar países que usan más de un idioma**

**Álgebra relacional**:  

$$
\sigma_{\text{count(Language)} > 1}(\text{CountryLanguage GROUP BY CountryCode})
$$

**SQL equivalente**:  
```sql
SELECT c.Name AS CountryName FROM countrylanguage cl
JOIN country c ON cl.CountryCode = c.Code
GROUP BY c.Name
HAVING COUNT(cl.Language) > 1;

```

![image](https://github.com/user-attachments/assets/16e56b88-b297-4eba-8c8a-f748d711f927)

**3. Calcular el total de población de cada continente**

**Álgebra relacional**:  

$$
\pi_{\text{Continent}, \text{SUM(Population)}}(\text{Country}) \text{ GROUP BY Continent}
$$

**SQL equivalente**:  
```sql
SELECT Continent, SUM(Population) AS TotalPopulation
FROM country
GROUP BY Continent;
```

![image](https://github.com/user-attachments/assets/450c38e9-3ce9-4bd8-b128-f730ce6b61c4)

**4. Contar el número de ciudades en cada país**

**Álgebra relacional**:  

$$
\pi_{\text{CountryCode}, \text{COUNT(*)}}(\text{City}) \text{ GROUP BY CountryCode}
$$

**SQL equivalente**:  
```sql
SELECT CountryCode, COUNT(*) AS NumberOfCities
FROM city
GROUP BY CountryCode;
```

![image](https://github.com/user-attachments/assets/98f6a73d-0bd9-48a2-9dda-dfea976e37f1)

**5. Listar los países y su promedio de vida ordenados por el promedio de vida en orden descendente**

**Álgebra relacional**:  

$$
\pi_{\text{Name}, \text{LifeExpectancy}}(\text{Country}) \text{ ORDER BY LifeExpectancy DESC}
$$

**SQL equivalente**:  
```sql
SELECT Name AS CountryName, LifeExpectancy
FROM country
ORDER BY LifeExpectancy DESC;
```

![image](https://github.com/user-attachments/assets/972a95b3-bb26-461b-9ca1-a1b89fcc2601)

**6. Selección de ciudades cuya población está entre 500,000 y 1,000,000**

**Álgebra relacional**:  

$$
\sigma_{500000 \leq \text{Population} \leq 1000000}(\text{City})
$$

**SQL equivalente**:  
```sql
SELECT Name, Population FROM city
WHERE Population BETWEEN 500000 AND 1000000;
```

![image](https://github.com/user-attachments/assets/3cb60d2c-8007-4d56-9b87-2333aec25943)

**7. Listar los idiomas hablados en países donde la población es mayor a 50 millones**

**Álgebra relacional**:  

$$
\pi_{\text{Language}}(\sigma_{\text{Population} > 50000000}(\text{Country}) \bowtie \text{CountryLanguage})
$$

**SQL equivalente**:  
```sql
SELECT cl.Language, cl.CountryCode
FROM country c
JOIN countrylanguage cl ON c.Code = cl.CountryCode
WHERE c.Population > 50000000;
```

![image](https://github.com/user-attachments/assets/6f140a4d-0f5c-4f66-9891-3f4f0c686408)

**8. Calcular el promedio de población por ciudad en cada país**

**Álgebra relacional**:  

$$
\pi_{\text{CountryCode}, \text{AVG(Population)}}(\text{City}) \text{ GROUP BY CountryCode}
$$

**SQL equivalente**:  
```sql
SELECT Name, AVG(population) AS promedio
FROM city
GROUP BY Name;
```

![image](https://github.com/user-attachments/assets/465e2a1e-c0fe-4af4-b880-63a6e5a49df9)

**9. Seleccionar los países cuya calificación de vida está por encima del promedio mundial**

**Álgebra relacional**:  

$$
\sigma_{\text{LifeExpectancy} > \text{AVG(LifeExpectancy)}}(\text{Country})
$$

**SQL equivalente**:  
```sql
SELECT Name, LifeExpectancy
FROM country
WHERE lifeexpectancy > (SELECT AVG(lifeexpectancy) FROM country);
```

![image](https://github.com/user-attachments/assets/739c36d6-87ad-4314-a735-43ee93d6d9a9)

**10. Encontrar los paises con una calificación de vida superior al promedio de su continente**

**Álgebra relacional**:  

$$
\pi_{\text{Continent, AVG(LifeExpectancy)}}(\text{Country}) \text{ GROUP BY Continent}
$$

**SQL equivalente**:  
```sql
SELECT p1.Name, p1.Continent, p1.LifeExpectancy
FROM country p1
WHERE p1.LifeExpectancy > (
    SELECT AVG(p2.LifeExpectancy)
    FROM country p2
    WHERE p2.Continent = p1.Continent
);
```
![image](https://github.com/user-attachments/assets/aebe5386-aa03-4fff-8669-f05deee5e2bb)

# Más consultas

## 1. ¿Cuáles son las 5 ciudades más pobladas?

**Álgebra relacional**:  

$$
\pi \text{Nombre, Población} \left( \sigma \text{Población} \text{ ordenado por } \text{Población DESC} (\text{Ciudad}) \right) \text{ LIMIT } 5
$$

**SQL equivalente**:  
```sql
Select Name, Population From city order by Population desc limit 5;
```

![image](https://github.com/user-attachments/assets/fb6f64ce-6071-4adb-97fa-7c3fd37c07d2)

## 2. ¿Qué países tienen una esperanza de vida superior a 80 años?

**Álgebra relacional**:  

$$
\sigma \text{Esperanza de vida} > 80 (\text{País})
$$

**SQL equivalente**:  
```sql
SELECT Name, LifeExpectancy FROM country WHERE LifeExpectancy > 80;
```

![image](https://github.com/user-attachments/assets/d47bf964-6a8a-4bd0-9a9b-5bfa27ee02b1)

## 3. ¿Cuántas ciudades hay en cada país?

**Álgebra relacional**:  

$$
\pi \text{Código de país, COUNT(*)} (\text{Ciudad}) \text{ GROUP BY Código de país}
$$

**SQL equivalente**:  
```sql
SELECT Countrycode, COUNT(*) AS num_ciudades FROM City GROUP BY Countrycode;
```

![image](https://github.com/user-attachments/assets/5dffabc9-3b32-4258-8b86-19c1592b817c)

## 4. ¿Cuáles son los idiomas hablados en países con población mayor a 50 millones?

**Álgebra relacional**:  

$$
\pi \text{Idioma} \left( \sigma \text{Población} > 50000000 (\text{País}) \bowtie \text{PaísIdioma} \right)
$$

**SQL equivalente**:  
```sql
SELECT cl.Language, c.Name, c.PopulationbFROM country c
JOIN countrylanguage cl ON c.Code = cl.CountryCode WHERE c.Population > 50000000;

```

![image](https://github.com/user-attachments/assets/7da15262-9f31-4165-a5b8-6bb0fdce94b1)

## 5. ¿Qué continentes tienen una esperanza de vida promedio superior a 75 años?

**Álgebra relacional**:  

$$
\pi \text{Continente, AVG(Esp. de vida)} (\text{País}) \text{ GROUP BY Continente HAVING AVG(Esp. de vida) > 75}
$$

**SQL equivalente**:  
```sql
SELECT Continent, AVG(LifeExpectancy) AS promedio
FROM country GROUP BY Continent
HAVING AVG(LifeExpectancy) > 75;
```

![image](https://github.com/user-attachments/assets/0e3c1ccc-a8a8-4af4-8280-321549d4a023)

## 6. ¿Cuáles son los países de Europa?

**Álgebra relacional**:  

$$
\sigma \text{Continente = 'Europe'} (\text{País})
$$

**SQL equivalente**:  
```sql
SELECT Name FROM country WHERE Continent = 'Europe';
```

![image](https://github.com/user-attachments/assets/091aac3b-f938-4c55-bd24-c8b335f7a42f)

## 7. ¿Cuál es la población total de cada continente?

**Álgebra relacional**:  

$$
\pi \text{Continente, SUM(Población)} (\text{País}) \text{ GROUP BY Continente}
$$

**SQL equivalente**:  
```sql
SELECT Continent, SUM(Population) AS total FROM country GROUP BY Continent;
```

![image](https://github.com/user-attachments/assets/d79e937c-feaa-4b00-a3a5-e4d05eadc87d)

## 8. ¿Qué países tienen una población menor a 1 millón?

**Álgebra relacional**:  

$$
\sigma \text{Población} < 1000000 (\text{País})
$$

**SQL equivalente**:  
```sql
SELECT Name, Population FROM country WHERE Population < 1000000;
```

![image](https://github.com/user-attachments/assets/5a4d9469-8627-405c-ac8d-298fa9f28337)

## 9.¿Cuáles son los países cuyo nombre comienza con la letra 'A'?

**Álgebra relacional**:  

$$
\sigma \text{Name LIKE 'A%'} (\text{País})
$$

**SQL equivalente**:  
```sql
SELECT Name FROM country WHERE Name LIKE 'A%';
```

![image](https://github.com/user-attachments/assets/86aa7879-2035-4a5e-a5dd-1ac8a434e83b)

## 10. ¿Cuáles son los nombres de los países y su región, ordenados alfabéticamente por región?

**Álgebra relacional**:  

$$
\pi \text{Name, Region} (\text{country}) \text{ ordenado por Region ASC}
$$

**SQL equivalente**:  
```sql
SELECT Name, Region FROM country ORDER BY Region ASC;
```

![image](https://github.com/user-attachments/assets/8e23c555-2af6-48da-9095-06bdfae07fb7)

