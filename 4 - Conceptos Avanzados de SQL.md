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

Funcion creada para recibir informacion, procesarlos y dar una salida.

En el siguiente codigo de Python vemos como se realiza un sistema que:

1. Abre una coneccion
2. Realiza una consulta
3. Guarda los datos con un commit()
4. Cerro el cursor
5. Cerro la coneccion
6. Libero los recursos

```Python
import sqlite3
import pandas as pd

square = lambda n:n*n

conn = sqlite3.connect("Northwind.db")
# Nombre de la funcion a crear, numero de atributos, funcion
conn.create_function("square", 1, square)

cursor = conn.cursor()
# execute va a ejecutar la consulta y almacenarla en "cursor"
cursor.execute('''
    SELECT * FROM Products
    ''')

# fetchall muestra la informaicon almacenada en "cursor"
results = cursor.fetchall()
results_df = pd.DataFrame(results)

# Guarda los cambios
conn.commit()

# Libera el recurso y conexion
cursor.close()
conn.close()

results_df
```

Otra forma de realizar esto es:

```Python

```

<p align="center">
    <img src="./Images/.png" width="550" height="200">
</p>
```
