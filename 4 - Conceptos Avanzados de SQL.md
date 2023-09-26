## 1. **BLOQUEOS Y TRANSACCIONES**

LOCKS: Mecanismos para manejar accesos concurrentes a una base de datos.

- SHARED LOCKS: Bloqueo compartido, prohibe que puedan modificar la base de datos pero permite leerla, esta siempre activa.
- RESERVED LOCKS: Bloqueo que se aplica cuando alguien esta escribiendo en la base de datos y permite a los demas leer pero no escribir.
- EXCLUSIVE LOCKS: Bloqueo que se aplica cuando alguien esta escribiendo en la base de datos y NO permite a los demas leer NI escribir.

TRANSACCIONES:

```SQL
-- Iniciar la transaccion
BEGIN TRANSACTION
-- Escribir las modificaciones a realizar
UPDATE Product SET ProductName = "Rafa" WHERE ProductName = "Chais";
-- COMMIT sirve para realizar los cambios
-- ROLLBACK sirve para deshacer los cambios
COMMIT()
```

Generalmente no se utilizan las transacciones de SQL sino que se utiliza un lenguaje de programacion utilizado en el BackEnd, como Python.

## 2. **PROCEDIMIENTOS ALMACENADOS**

Conjunto de comandos que se guardan en la base de datos que se pueden ejecutar en cualquier momento. Se ejecuta como su fuera una biblioteca.

## 3. **USER DEFINED FUNCTIONS**

Conj

6:35:54

<p align="center">
    <img src="./Images/.png" width="550" height="200">
</p>
```
