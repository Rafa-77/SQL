### PREGUNTA 1

```SQL
SELECT
	Fraude.reporteRegulatorio,
    SeccionBanxicoMapeo.seccionOrigen,
    SeccionBanxico.nombreCorto,
    ClaveBanxicoMapeo.claveOrigen,
    SubclaveBanxicoMapeo.subclaveOrigen,
	SUM(Fraude.monto) as sumaMonto,
	AVG(Fraude.monto) as promedioMonto,
    MAX(Fraude.monto) as maxMonto
FROM Fraude
-- Seccion
LEFT JOIN SeccionBanxico ON Fraude.seccion = SeccionBanxico.seccion
LEFT JOIN SeccionBanxicoMapeo ON SeccionBanxico.seccion = SeccionBanxicoMapeo.seccion
-- Clave
LEFT JOIN ClaveBanxico ON Fraude.clave = ClaveBanxico.clave
LEFT JOIN ClaveBanxicoMapeo ON ClaveBanxico.clave = ClaveBanxicoMapeo.clave
-- Subclave
LEFT JOIN SubclaveBanxico ON Fraude.subclave = SubclaveBanxico.subclave
LEFT JOIN SubclaveBanxicoMapeo ON SubclaveBanxico.subclave = SubclaveBanxicoMapeo.subclave
-- Condicion
WHERE Fraude.institucion = 'A' AND Fraude.fecha >= '2011-07-17'
-- Agrupacion
GROUP BY
    Fraude.reporteRegulatorio,
    SeccionBanxicoMapeo.seccionOrigen,
    SeccionBanxico.nombreCorto,
    ClaveBanxicoMapeo.claveOrigen,
    SubclaveBanxicoMapeo.subclaveOrigen;
```

### PREGUNTA 2

```SQL
SELECT
    idOperacion,
    divisa,
	fecha,
	fechaUltimaTransaccion,
    fecha - fechaUltimaTransaccion as diasDesdeUltimaTransaccion,
    saldo + saldoIntereses as saldoTotal,
    CASE
        WHEN divisa IN ('MXN', 'MXP', 'USD') AND fecha - fechaUltimaTransaccion >= 90 AND saldo + saldoIntereses < 1000 THEN 'NO ACTIVA'
        WHEN divisa IN ('MXN', 'MXP', 'USD') AND fecha - fechaUltimaTransaccion >= 90 AND saldo + saldoIntereses >= 1000 THEN 'SIN MOVIMIENTOS'
  		-- TIPO DE CAMBIO OBTENIDO DE INVESTING.COM EUR/MXN AL 31/03/2023: https://mx.investing.com/currencies/eur-mxn-historical-data
		WHEN divisa NOT IN ('MXN', 'MXP', 'USD') AND fecha - fechaUltimaTransaccion >= 90 AND (saldo + saldoIntereses)*19.52 < 1000 THEN 'NO ACTIVA'
		WHEN divisa NOT IN ('MXN', 'MXP', 'USD') AND fecha - fechaUltimaTransaccion >= 90 AND (saldo + saldoIntereses)*19.52 >= 1000 THEN 'SIN MOVIMIENTOS'
		ELSE 'ACTIVA'
    END AS Estatus
FROM
    CreditoLgr;
```

### PREGUNTA 3

Observando la tabla de datos de diciembre 2022, nos damos cuenta claramente que es erronea desde los puntos básicos.

Primero nos tenemos que asegurar que cumplan con los mismos formatos SQL que los datos historicos, es decir, la definicion de las claves en especial la PRIMARY KEY, el formato de los campos de la tabla ya sean TEXT, INTEGER, FLOAT, DATE; el numero de caracteres; la permision de valores NULL, etc.

Tras asegurarse que el formato sea el correcto, se aplican las reglas de NORMALIZACION:
Estas son 5 normas:

- Primero, debemos garantizar que cada atributo contenga un valor unico atomico, es decir, los valores de una columna no deben de ser una estructura de datos compleja (lista, conjuntos). Tampoco debe haber repeticiones en una misma fila para una clave primaria.
- Segunda, asegurarnos que no haya dependencias parciales, es decir que cada atributo que no sea una clave dependa completamente de la clave primaria.
- Tercero, asegurarnos que no haya dependencias transitivas, es decir, que cada atributo debe depender directamente de la clave primaria y no de atributos que no son claves.
- Cuarto, cada tabla debe tener una clave primaria compuesta que consta de multiples columnas en lugar de 1 sola.
- Quinta, asegurarse que no haya dependencias de union entre atributos.

### PREGUNTA 4

Ver Excel Adjunto.
