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

```

