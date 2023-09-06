# 1. Conceptos Base de SQL

1. ### Entidad:

   Representacion de algo, ej: Casa (representada por un _cuadrado_)

2. ### Atributos:
   Caracteristicas/Atributos de la entidad (Representados por _ovalos_).

- Atributos Simples: Precio, tamaño (representados por **1 ovalo**)
- Atributos compuestos: Ambiente
- Atributos multivalor: Puerta, ventana (representados por **2 ovalos**)
- Atributos derivados: antiguedad, ubicacion, se pueden obtener de otra informacion (representados por un **ovalo con borde punteado**)
- Atributo Key: Un identificador Unico, ID Vivienda (identificado con un ovalo y **texto subrayado**)

#### Ejemplo 1: Entidad Persona y sus atributos

<p align="center">
    <img src="./Images/Atributo Persona.png" width="350" height="250">
</p>

#### Ejemplo 2: Entidad Empleado y sus atributos

<p align="center">
    <img src="./Images/Atributo Empleado.png" width="450" height="250">
</p>

3. ### Tabla:

   Es una estructura de datos en filas y columnas. Almacena informacion de una entidad especifica.

4. ### Campo/Field:

   Nombre de la informacion almacenada en una columna de la tabla.

5. ### Registro/Record:

   Es el nombre/numero de una fila de la tabla.

6. ### Valor de campo/Field Value:
   Es el valor correspondiente a una combinacion de campo y registro.

| Tabla      | Campo 1       | Campo 2       |
| ---------- | ------------- | ------------- |
| Registro 1 | Field Value 1 | Field Value 2 |
| Registro 2 | Field Value 3 | Field Value 4 |

---

---

### Codigo para crear una tabla en SQL

- Crear la base de datos

CREATE DATABASE "RAFA_DB"

- Crear una tabla para la base de datos

```SQL
CREATE TABLE "usuarios" (
	"nombre"	TEXT,
	"apellido"	TEXT,
	"edad"	INTEGER
);
```

- Insertar valores a la tabla creada

```SQL
INSERT INTO usuarios (nombre, apellido, edad)
VALUES ("Rafa", "Martinez", 23),
       ("Ale", "Martinez", 10),
       ("Gab", "Martinez", 100),
       ("Edu", "Martinez", 01)
```

- Crear una consulta para seleccionar datos de la base de datos

```SQL
SELECT * FROM usuarios
SELECT nombre, edad FROM usuarios
```

- Eliminar registros de una tabla

```SQL
DELETE FROM usuarios
```

---

---

7. ### Identifiers:

   - **PRIMARY KEYS (PK)**

Un campo utilizado para identificar registros dentro de una tabla.

Se utiliza la propiedad **"AUTOINCREMENT"** y **"PRIMARY KEY"** para lograr realizar el identificador.

```SQL
CREATE TABLE "usuarios" (
	"id_usuarios"	INTEGER,
	"nombre"	TEXT,
	"apellido"	TEXT,
	"edad"	INTEGER,
	PRIMARY KEY("id_usuarios" AUTOINCREMENT)
)
```

Se puede agregar registros sin necesidad de ingresar el **"id_usuario"**. Este se agregará automaticamente de manera que incremente en una unidad el valor previo registrado, en caso de ser el primero, sera el numero **1**.

```SQL
INSERT INTO usuarios (nombre, apellido, edad)
VALUES ("rafa", "mtz", 23)
```

- **FOREIGN KEY (FK)**

Campo que hace referencia a una **PRIMARY KEY** de otra tabla.

Se utiliza el mismo nombre que la PK a referenciar.

<p align="center">
    <img src="./Images/PK y FK.png" width="350" height=350">
</p>
