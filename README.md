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

# Consultas Nivel medio


### 1. Encuentra los países que tienen un idioma oficial.
**Objetivo:** Identificar los países con al menos un idioma oficial registrado en la tabla `countrylanguage`.
- **Álgebra Relacional:** 
  $$\pi_{\text{CountryCode}}(\sigma_{\text{IsOfficial} = 'T'} (\text{CountryLanguage}))$$
- **Consulta en SQL:**
  ```sql
   SELECT DISTINCT CountryCode FROM countrylanguage WHERE IsOfficial = 'T';
  ```

  ![image](https://github.com/user-attachments/assets/4102c75b-8f4d-42b2-9c74-11b1717884da)

### 2. Lista los países que tienen más de un idioma oficial.
**Objetivo:** Identificar los países con varios idiomas oficiales.
- **Álgebra Relacional:**
  $$\pi_{\text{CountryCode}} (\sigma_{\text{IsOfficial} = 'T'} (\text{CountryLanguage}))\ \ \text{GROUP BY CountryCode HAVING COUNT(*) > 1}$$
- **Consulta en SQL:**
  ```sql
  SELECT CountryCode FROM countrylanguage WHERE IsOfficial ='T' group by CountryCode HAVING COUNT(*) >1;
  ```

![image](https://github.com/user-attachments/assets/2bd4eab5-cda2-4b29-8bf7-d42975d0c0fd)

### 3. Encuentra los países que tienen el mismo continente que Japón.
**Objetivo:** Listar los países que comparten el mismo continente que Japón.
- **Álgebra Relacional:**
  $$\pi_{\text{Name}} (\text{Country} \bowtie_{\text{Continent} = 'Asia'} \text{Country})$$
- **Consulta en SQL:**
  ```sql
  SELECT Name FROM country WHERE Continent = 'Asia';
  ```

![image](https://github.com/user-attachments/assets/e02948ff-c13e-4c1d-ac06-faa923046eac)

### 4. Encuentra las ciudades que tienen población mayor a 5 millones y están en América del Sur.
**Objetivo:** Filtrar ciudades por población y continente.
- **Álgebra Relacional:**
  $$\pi_{\text{City.Name}} (\sigma_{\text{City.Population} > 5000000 \land \text{Country.Continent} = 'South America'}(\text{City} \bowtie \text{Country}))$$
- **Consulta en SQL:**
  ```sql
  SELECT city.Name FROM City JOIN country ON city.CountryCode = country.Code
   WHERE city.Population > 5000000 AND country.Continent='South America';
  ```

![image](https://github.com/user-attachments/assets/1ec6de55-41f4-4325-977e-bb52233703b9)

### 5. Encuentra los países que no tienen ningún idioma oficial.
**Objetivo:** Listar los países sin idioma oficial.
- **Álgebra Relacional:**
  $$\pi_{\text{Country.Code}}(\text{Country}) - \pi_{\text{CountryCode}}(\sigma_{\text{IsOfficial} = 'T'}(\text{CountryLanguage}))$$
- **Consulta en SQL:**
  ```sql
   SELECT Code
   FROM Country WHERE Code NOT IN (
   SELECT CountryCode
   FROM CountryLanguage
   WHERE IsOfficial = 'T'
   );
  ```

![image](https://github.com/user-attachments/assets/722b99df-3f47-40bd-b771-2a0ae2ed9591)

### 6. Encuentra los idiomas que son oficiales en al menos dos países.
**Objetivo:** Identificar idiomas que sean oficiales en varios países.
- **Álgebra Relacional:**
  $$\pi_{\text{Language}} (\sigma_{\text{IsOfficial} = 'T'} (\text{CountryLanguage}) \ \text{GROUP BY Language HAVING COUNT(DISTINCT CountryCode) >= 2})$$
- **Consulta en SQL:**
  ```sql
  SELECT Language FROM countrylanguage WHERE Isofficial ='T' 
   GROUP BY Language HAVING COUNT(DISTINCT CountryCode) >= 2; 
  ```

![image](https://github.com/user-attachments/assets/86dbb3a4-b007-4719-bedd-cd2c8f9ebdd7)

### 7. Lista los países y su capital.
**Objetivo:** Obtener la relación entre los países y sus capitales.
- **Álgebra Relacional:**
  $$\pi_{\text{Country.Name}, \text{City.Name}} (\text{Country} \bowtie_{\text{Country.Capital} = \text{City.ID}} \text{City})$$
- **Consulta en SQL:**
  ```sql
   SELECT Country.Name AS CountryName, City.Name AS CapitalName
   FROM Country JOIN City ON Country.Capital = City.ID;
  ```
  
![image](https://github.com/user-attachments/assets/74cb06e7-2714-4250-b737-7df34b3a6a65)

### 8. Encuentra los países que tienen una población mayor que Alemania.
**Objetivo:** Comparar población con un país específico.
- **Álgebra Relacional:**
  $$\pi_{\text{Name}}(\sigma_{\text{Population} > ( \text{SELECT Population FROM Country WHERE Name = 'Germany'} ) }(\text{Country}))$$
- **Consulta en SQL:**
  ```sql
  SELECT Name FROM country WHERE Population > (SELECT population FROM country WHERE Name = 'Germany');
  ```

![image](https://github.com/user-attachments/assets/1d10d0f3-34e0-42f6-bd11-4f2af4ebbd9d)

### 9. Encuentra los idiomas oficiales de Europa.
**Objetivo:** Listar los idiomas oficiales de países europeos.
- **Álgebra Relacional:**
  $$\pi_{\text{Language}} (\sigma_{\text{Country.Continent} = 'Europe'} (\text{Country} \bowtie \text{CountryLanguage}))$$
- **Consulta en SQL:**
  ```sql
  SELECT DISTINCT CountryLanguage.Language
   FROM Country JOIN CountryLanguage ON Country.Code = CountryLanguage.CountryCode
   WHERE Country.Continent = 'Europe' AND CountryLanguage.IsOfficial = 'T';
  ```

![image](https://github.com/user-attachments/assets/5af570f6-de9e-4d5d-bac1-30eb25839b65)

### 10. Encuentra los países sin ciudades registradas en la tabla `City`.
**Objetivo:** Detectar países sin representación en la tabla de ciudades.
- **Álgebra Relacional:**
  $$\pi_{\text{Country.Code}}(\text{Country}) - \pi_{\text{CountryCode}}(\text{City})$$
- **Consulta en SQL:**
  ```sql
  SELECT Name FROM Country
   WHERE Code NOT IN (
    SELECT CountryCode
    FROM City	
   );
  ```
  
![image](https://github.com/user-attachments/assets/3992dc2a-8a26-4243-af30-d1a40559be66)

### 11. Muestra la población total de cada continente.
**Objetivo:** Calcular la población por continente.
- **Álgebra Relacional:**
  $$\pi_{\text{Continent}, \text{SUM(Population)}} (\text{Country} \ \text{GROUP BY Continent})$$
- **Consulta en SQL:**
  ```sql
   SELECT Continent, SUM(Population) AS total FROM Country
   GROUP BY Continent;
  ```

![image](https://github.com/user-attachments/assets/4d598beb-ca44-4525-902f-75cf38870a5d)

### 12. Encuentra los países en los que la esperanza de vida es menor al promedio global.
**Objetivo:** Filtrar países con esperanza de vida baja en comparación con el promedio.
- **Álgebra Relacional:** $$\pi_{\text{Name}}(\sigma_{\text{LifeExpectancy} < \text{AVG(LifeExpectancy)}}(\text{Country}))$$
- **Consulta en SQL:**
  ```sql
  SELECT Name FROM Country
  WHERE LifeExpectancy < (SELECT AVG(LifeExpectancy) FROM Country);
  ```
![image](https://github.com/user-attachments/assets/926db7f0-d942-4d23-ba41-f3247fdd9c85)


### 13. Encuentra los países en Asia sin idioma oficial registrado.
**Objetivo:** Listar países asiáticos sin idiomas oficiales.
- **Álgebra Relacional:**
  $$\pi_{\text{Country.Code}}(\sigma_{\text{Continent} = 'Asia'} (\text{Country})) - \pi_{\text{CountryCode}}(\sigma_{\text{IsOfficial} = 'T'}(\text{CountryLanguage}))$$
- **Consulta en SQL:**
  ```sql
  SELECT Code FROM Country  WHERE Continent = 'Asia'
  AND Code NOT IN (
      SELECT CountryCode
      FROM CountryLanguage
      WHERE IsOfficial = 'T'
  );
  ```
  
![image](https://github.com/user-attachments/assets/adf2516a-f5cb-4fc6-83e8-9d6101e4206a)

### 14. Lista los idiomas que son oficiales en países con esperanza de vida mayor a 80.
**Objetivo:** Identificar idiomas en países con alta esperanza de vida.
- **Álgebra Relacional:**
  $$\pi_{\text{Language}} (\sigma_{\text{Country.LifeExpectancy} > 80} (\text{Country} \bowtie \text{CountryLanguage}))$$
- **Consulta en SQL:**
  ```sql
  SELECT DISTINCT Language FROM Country JOIN CountryLanguage
  ON Country.Code = CountryLanguage.CountryCode WHERE Country.LifeExpectancy > 80
  AND CountryLanguage.IsOfficial = 'T';
  ```

![image](https://github.com/user-attachments/assets/10c54068-4091-4603-afb6-f7e3c67beaaf)

### 15. Encuentra los países con más de 10 ciudades en la tabla `City`.
**Objetivo:** Identificar países con una gran cantidad de ciudades registradas.
- **Álgebra Relacional:**

$$ \pi_{\text{CountryCode}} (\text{City} \ \text{GROUP BY CountryCode HAVING COUNT(*) > 10}) $$

- **Consulta en SQL:**
  ```sql
  SELECT CountryCode FROM City GROUP BY CountryCode HAVING COUNT(*) > 10;
  ```

![image](https://github.com/user-attachments/assets/94d53b20-e35e-466b-b8a7-b95797220f3a)

# Consultas propuestas

### 1. Encuentra los países con un PIB (GNP) mayor al promedio mundial.

**Álgebra relacional:**

$$
\pi_{Name}(\sigma_{GNP > AVG(GNP)}(Country))
$$

**SQL equivalente:**

```sql
SELECT Name FROM Country WHERE GNP > (SELECT AVG(GNP) FROM Country);
```

![image](https://github.com/user-attachments/assets/0e7800f0-f4e9-4a24-a180-f1bb93204462)

### 2. Lista las ciudades con más de un millón de habitantes en países de América del Sur.

**Álgebra relacional:**

$$ 
\pi_{City.Name}(\sigma_{Population > 1000000 \land Continent = 'South America'}(City \bowtie Country)) 
$$

**SQL equivalente:**
```sql
SELECT City.Name FROM City
JOIN Country ON City.CountryCode = Country.Code
WHERE City.Population > 1000000 AND Country.Continent = 'South America';
```

![image](https://github.com/user-attachments/assets/307946a6-60b1-47a5-bd4a-8700ce74094a)

### 3. Encuentra los continentes con más de 10 países registrados.

**Álgebra relacional:**

$$ 
\pi_{Continent}(Country \text{ GROUP BY } Continent \text{ HAVING COUNT(*) > 10}) 
$$

**SQL equivalente:**
```sql
SELECT Continent FROM Country GROUP BY Continent HAVING COUNT(*) > 10;
```

![image](https://github.com/user-attachments/assets/3aa003ae-d21c-4da4-b4ef-8aa73b3924d6)

### 4. ¿Cuáles son las capitales de los países en América del Sur?

**Álgebra relacional:**

$$ 
\pi_{City.Name}(\sigma_{Continent = 'South America'}(Country) \bowtie City) 
$$

**SQL equivalente:**
```sql
SELECT City.Name FROM Country
JOIN City ON Country.Capital = City.ID
WHERE Country.Continent = 'South America';
```

![image](https://github.com/user-attachments/assets/dffe3a33-b504-4943-972b-236971ec274f)

### 5. ¿Qué países tienen una población total menor que la de Alemania?

**Álgebra relacional:**

$$ 
\pi_{Name}(\sigma_{Population < (SELECT Population FROM Country WHERE Name = 'Germany')}(Country)) 
$$

**SQL equivalente:**
```sql
  SELECT Name FROM Country WHERE Population > (SELECT Population FROM Country WHERE Name = 'Germany');
```

![image](https://github.com/user-attachments/assets/caa71843-8de7-406f-9cc4-7b6c9b9dd6ed)

### 6. Lista los países donde no se habla inglés como idioma oficial.

**Álgebra relacional:**

$$
\pi_{Name}(Country - \pi_{Country.Name}(\sigma_{Language = 'English' \land IsOfficial = 'T'}(Country \bowtie CountryLanguage))) 
$$ 

**SQL equivalente:**

```sql
 SELECT Name FROM Country  
WHERE Code NOT IN (  
  SELECT CountryCode  
  FROM CountryLanguage  
  WHERE Language = 'English'  
    AND IsOfficial = 'T'  
);  
```

![image](https://github.com/user-attachments/assets/39b30f33-37b9-4483-a781-975ee27c1955)

### 7. Encuentra los países con mayor densidad de población que Japón.

**Álgebra relacional:**

$$
\pi_{Name}(\sigma_{LifeExpectancy < \text{AVG}(LifeExpectancy)}(Country))
$$

**SQL equivalente:**

```sql
SELECT Name, Population / SurfaceArea AS Density FROM Country
WHERE Population / SurfaceArea > (
    SELECT Population / SurfaceArea FROM Country WHERE Name = 'Japan'
)
ORDER BY Density DESC;
```

![image](https://github.com/user-attachments/assets/c068cff3-b45b-4d2a-a809-9034466974a7)

### 8. Lista las ciudades con nombre que comience con la letra 'Z'.

**Álgebra relacional:**

$$
\pi_{Name}(\sigma_{Name \, \text{LIKE} \, 'Z\text{}'}(City))
$$

**SQL equivalente:**

```sql
 SELECT Name FROM City WHERE Name LIKE 'Z%';
```

![image](https://github.com/user-attachments/assets/fd68054b-05ca-49ac-a1ac-2a255d78b866)

### 9. Lista las ciudades capitales junto con su población.

**Álgebra relacional

$$
\pi_{City.Name, City.Population}(City \bowtie_{City.ID = Country.Capital}(Country))
$$

**SQL equivalente:**

```sql
 SELECT City.Name, City.Population FROM City JOIN Country ON City.ID = Country.Capital;
```

![image](https://github.com/user-attachments/assets/b46c5eed-6387-4c3d-853b-5558ecd0700c)

### 10. Encuentra los países con más de 5 idiomas oficiales.

**Álgebra relacional:**

$$
\pi_{Name}(Country \bowtie (\sigma_{COUNT(IsOfficial) > 5}(CountryLanguage))) 
$$

**SQL equivalente:**

```sql
 SELECT Country.Name FROM Country
JOIN CountryLanguage ON Country.Code = CountryLanguage.CountryCode
GROUP BY Country.Name HAVING COUNT(CountryLanguage.CountryCode) > 5;
```

![image](https://github.com/user-attachments/assets/be4f9a5a-b721-4c01-bb7a-9b2a09c3e786)

