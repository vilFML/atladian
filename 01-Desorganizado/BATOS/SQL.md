# SQL

SQL es un lenguage para gestionar datos en una base de datos relacional. Significa *Lenguaje de Consultas Estructurado*.

- DDL: *Data definition language* para ver cómo construir tablas. 
- DML: *Data manipultaion language* para ver cómo construir tablas.
### Extraer
Para **extraer atributos** de una columna se usa `select` que es equivalente a $\Pi$, de la forma:
```SQL
select atributo1, atributo2 from tabla
```
que es equivalente a hacer
$$
\Pi_{\text{atrib1},\text{atrib2}}(\text{Tabla})
$$

`select` entrega conjuntos, entonces el orden en que se entrgan los datos puede cambiar. Esto pues el sistema optimiza la consulta según si los datos se encuentran en RAM o en almacenamiento.

### Filtrar

Para **filtrar** datos se utiliza `where`, que es equivalente a $\sigma$ de álgebra relacional:
```SQL
select * from tabla where condicion1, condicion2
```
que es equivalente a 
$$
\sigma_{\text{cond1, cond2}}
$$





##### Ejemplo
Obtener los nadadores de la región del Maule:
```SQL
select * from nadador where region='Maule'
```
se extraen los `id` que nos sirven: 9, 19, 29.

Y para tener nadadores de género femenino:
```SQL
select nombre ||' '|| apellido as nombre_completo from nadador where genero='F'
```

```SQL
select nombre ||' '|| apellido as nombre_completo from nadador where genero='F' OR id_club=9 OR id_club=19 OR id_club=29
```
en donde se indican los id que sirven:

```SQL
select nombre ||' '|| apellido as nombre_completo from nadador where genero='F' OR id_club=9 OR id_club in (select id_club from club where region='Maule')
```

(select anidado)

### Extra
- Se puede **renombrar una columna** extraida con `atributo as alias`

- **Limitar la cantidad de filas extraidas** con `LIMIT n;`.
  Uso práctico: extraer cierto dato según un orden. Ejemplo: El nadador de mayor edad, si se ordena por edad y se realiza `LIMIT 1`

- Se pueden **mezclar columnas** con `||`.
  Por ejemplo para juntar 2 `select nombre ||' '|| apellido`. Y se puede renombrar tabla extraída con `as`, como `as nombre_completo`

- Extraer datos de 2 tablas o más es **hacer producto cruz**: Se mezclan las tablas con `select * from tabla1, tabla2`.
  Si `tabla1` tiene 10 filas y `tabla2` tiene 3: `tabla1, tabla2` tiene $10\times3 = 30$ filas, pues por cada fila de una tabla se recorre toda fila de la otra tabla.
  \* Si no se indica orden, SQL optimiza.
  En este caso se pueden tener PK y FK en la tabla de resultado.

- Se usa `like` para *refinar* la condición de $\sigma$ para filtrar por texto que **contenga un substring**, de la forma: 
  `like '%substring%`, donde `%` es equivalente a `*`.
  \*Esto es en vez de hacer una consulta de texto exacta como `atributo='Texto'`

- Si no se agrega el `;` final en cada línea, el lenguaje considera que se sigue dentro de la misma instrucción. Así, se puede realizar una consulta más larga en distintas líneas (y entrar y salir en paréntesis).