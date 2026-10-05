Materia: 
	Fecha cátedra: 28/09/26
	Fecha digitalización: 28/09/26
	*tags:* 

Ya se vio que se pueden optimizar las bases de datos con índices, pero la inserción a gran escala es costoso por modificar constantemente el índice.

# Data Warehouse y Data Mart
Los distintos datos están separados en distintas áreas. Los **data warehouse** son repositorios generales de datos de todas las áreas, para analizar los datos y tomar decisiones basadas en un estudio de ellos.

Un **Data Mart** concentra información de una cierta área, dirigida a cierto departamento o unidad de negocio.

# ETL: Extract, Transform and Load
Son tres etapas con cada una de diferente responsabilidad al procesamiento de los datos.

- Extraer: Traer los datos como vienen de la fuente
- Transformar: 

---
Caso particular,
- se van a extraer de un .csv



## ELT
Extraer -> Cargar -> Transformar

Al obtener datos y visualizarlos, estos estarán *sucios*, lo que requiere una transformación para *limpiar* los datos que se usarán.

---
Ejemplo:

1. Extraer: CSV Puede venir con campos desordenados, o que no siguen la misma convención. O sea, para `nombre_raw` se tienen: 
   - `  CAMILA`
   - `Camila`
   - `   camila`
Se crea una tabla:
```SQL

```

Se copian los datos del csv a la tabla creada con `\copy` y luego visualizar los datos reflejará la tabla con los mismos campos, sin procesar.

Procesamiento de datos con funciones:
- Función `TRIM` elimina los espacios en blanco del inicio y fin del campo
- Función `INITCAP` deja solamente la primera letra en mayúscula
- Función `ILIKE` para comparar un campo con uno de referencia, para hacer:
```SQL
CASE
WHEN genero_raw ILIKE 'm%' THEN 'M'
WHEN genero_raw ILIKE 'f%' THEN 'F'
```

Para las fechas usar expresión regular tal que busque un patrón en los datos. Se usa la función `REGEXP_REPLACE`, de la forma:
```SQL
RE
```

El proceso entero se denomina **staging**.

### Transformar
Se hace el procesamiento y limpieza de datos, tal que se llevan los campos al **mismo formato**, usando una convención.


# Notas
- Data Science: Es la interpretación de la información contenida en los datos, debe ser adecuada según el **negocio** que se está analizando.
  No se pueden extrapolar interpretaciones de negocio de retail a quimica farmacéutica.