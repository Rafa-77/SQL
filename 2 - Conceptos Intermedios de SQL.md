# Conceptos Intermedios de SQL

Para lo siguiente se utilizará la DB Northwind.

1. **Columnas y Alias**

Para cambiar el nombre de una columna de manera temporal se utiliza "**AS**".

```SQL
SELECT LastName AS Apellido FROM Employees
SELECT LastName AS Apellido, FirstName As Nombre FROM Employees
```

Al realizar operaciones simples el titulo se modifica automaticamente:

```SQL
SELECT Price, Price*2, Price*2 AS Precio_doble FROM Products
SELECT SUM(Price), SUM(Price*2), SUM(Price*2) AS Suma_Precio_Doble FROM Products
```

2. **Ordenamientos**

Para realizar ordenamientos se utiliza la clausula "**ORDER BY**".

---

Escala de valores ASCENDENTE:

- NULL
- Numeros
- Caracteres especiales
- Letras

---

Ordenamiento Ascendente y Descendente

```SQL
-- Ordenamiento Ascendente, puede no escribirse el ASC pues es el establecido por DEFAULT
SELECT * FROM Products
ORDER BY Price ASC
-- Ordenamiento Descendente, debe escribirse a fuerza el DESC
SELECT * FROM Products
ORDER BY Price DESC
```

Posicionamiento de NULLS

```SQL
-- Los NULLS van primero por jerarquia, puede no ponerse
SELECT * FROM Products
ORDER BY ProductName ASC NULLS FIRST
-- En caso de querer poner los NULLS al final se utiliza "LAST"
SELECT * FROM Products
ORDER BY ProductName ASC NULLS LAST
```

Posicionamiento aleatorio

```SQL
-- RANDOM() es una funcion
SELECT * FROM Products
ORDER BY RANDOM()
```

Posicionamiento multiple

```SQL
-- El ordenamiento por dos campos respeta el orden en que se esta pidiendo.
SELECT * FROM Products
ORDER BY ProductName ASC, SupplierID DESC
```

3. **Seleccionar registros unicos**

La clausula DISTINCT selecciona los valores unicos del campo a tratar.

```SQL
SELECT DISTINCT ProductName FROM Products
ORDER BY ProductName ASC
```

4. **Realizar condiciones**

Condicion de Igualdad

```SQL
-- Devuelve el registro completo
SELECT * FROM Products
WHERE ProductID = 14
-- Devuelve el Valor del Campo solicitado
SELECT ProductID FROM Products
WHERE ProductName = "Tofu"
```

Condicion matemática

```SQL
SELECT * FROM Products
WHERE Price <= 40
ORDER BY Price DESC
```

Eliminar Registros

```SQL
DELETE FROM turnos_medicos
WHERE id_turno = 3
```

Modificar el valor de un campo en especifico

```SQL
UPDATE turnos_medicos
SET horario = "10:30", motivo = "Dolor de muelas"
WHERE id_turno = 2
```

And/Or/Not

- Tener cuidado con la diferencia entre:
  - Operadores Logicos (AND/OR/NOT): Trabajan con valores booleanos
  - Operadores de Comparacion (=, !=, <=, >): Trabajan con 2 valores y devuelven un valor booleano

```SQL
-- AND
SELECT * FROM Customers
WHERE CustomerID >= 50 AND CustomerID < 55
-- OR
SELECT * FROM Employees
WHERE FirstName = "Nancy" OR FirstName = "Anne"
-- AND/OR
SELECT * FROM Products
WHERE (Price < 20 OR CategoryID = 6) AND SupplierID = 7
-- NOT
SELECT * FROM Products
WHERE NOT SupplierID = 7
-- !=
SELECT * FROM Customers
WHERE Country != "USA"
--
SELECT * FROM Customers WHERE NOT FALSE
SELECT * FROM Customers WHERE TRUE AND TRUE
SELECT * FROM Customers WHERE TRUE OR FALSE
SELECT * FROM Customers WHERE TRUE
SELECT * FROM Customers WHERE 1
```

5. **Clausula LIMIT**

```SQL
-- Limita el numero de resultados segun el orden especificado
SELECT * FROM Customers
WHERE CustomerID >= 50
AND NOT Country = "Germany"
AND NOT Country = "UK"
ORDER BY RANDOM()
LIMIT 5
```

6. **Operador BETWEEN**

- Este operador incluye los limites tambien
- El primer valor del operador no puede ser mayor al segundo

```SQL
SELECT * FROM Products
WHERE Price NOT BETWEEN 10 AND 20
--
SELECT * FROM Employees
WHERE BirthDate BETWEEN "1950-0-0" AND "1960-0-0"
```

7. **Operador LIKE**

- Funciona de la misma manera que un "="
- Pero utiliza comodines, caracteres especiales:
  - %: Se coloca antes/despues de la expresion, significa que puede haber cualquier cosa antes/despues de esta.
  - \_: Sirve para rellenar caracteres

```SQL
-- Inicia con una "r"
SELECT * FROM Employees WHERE LastName LIKE "r%"
-- Termina con una "r"
SELECT * FROM Employees WHERE LastName LIKE "%r"
-- Contiene una "r"
SELECT * FROM Employees WHERE LastName LIKE "%r%"
--
-- Tiene 5 caracteres antes de la "r"
SELECT * FROM Employees WHERE LastName LIKE "_____r"
-- Tiene 2 caracteres despues de la "full"
SELECT * FROM Employees WHERE LastName LIKE "ful__"
--
-- Tiene 1 Caracter antes de la u, y n caracteres despues
SELECT * FROM Employees WHERE LastName LIKE "_u%"
-- Tiene 1 Caracter antes de la u, y al menos 2 caracteres despues
SELECT * FROM Employees WHERE LastName LIKE "_u__%"
```

8. **Operador IS NULL/IS NOT NULL**

3:08:35
