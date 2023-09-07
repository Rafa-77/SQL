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

3. **Eliminar registros duplicados**

1:52:21
