
Base de datos: Una colección de datos organizada de cierta forma que facilite realizar consultas en ella.
Sistema de bases de datos: Es un **software** para representar, cargar, organizar, definir, actualizar, consultar datos.

Con respecto a las consultas, se usará la eficiencia no como el orden (o belleza) sino como la rapidez en la consulta.

Pueden haber múltiples usuarios actualizando la base de datos al mismo tiempo. Se pueden utilizar 'semáforos' para marcar que se está modificando el archivo (Transacciones)

El curso se va a centrar en bases de datos *relacionales*. 

##### Ejemplos
Datos en Excel: Los datos en sí son una base de datos, la plantilla no.
ORACLE: Es un sistema de base de datos.
IMDB: La aplicación no es una base de datos, pero los datos (las películas) sí.

---


# Modelo Relacional

Un modelo de datos es un conjunto de estructuras descriptivas de alto nivel que oculta los detalles de almacenamiento de bajo nivel. Permitiendo así organizar la información en términos de entidades y las relaciones que existen entre ellos.
En un modelo se pierden detalles de la implementación, esta información debiese ser la que no es relevante para el propósito del uso del modelo.

*Caso de estudio*: Clasificación del dominio de cervezas chilenas, organizando la información sobre marcas y variedades:
- Una primera aproximación es el modelo de árbol (o de jerarquía). Se estrcuturan los datos con una raíz *Cervezas*, que se ramifica por origen geográfico desde la cual surgen los tipos *Lager* y *Ale*, situando a *Austral Lager* con 4.6° de alcohol bajo *Lager* y *Austral Yagan* con 5.0° bajo *Ale*.
  El modelo jerárquico es fácil de entender, pero se genera redundancia. Por ejemplo, el nodo de tipo *Ale* debe duplicarse por distintos orígenes geográficos y se tienen dificultades de operaciones en caso de querer ser modificado.
  ![[Pasted image 20260901124509.png]]
- Otra opción es el modelo de grafos, en donde los nodos almacenan la información y se conectan mediante aristas direccionales a los nodos de cervezas específicas.
  EL modelo de grafos es muy flexible pero resumir los datos es una tarea difícil pues no es claro observar un esquema.
  ![[Pasted image 20260901124617.png]]
- La tercera opción es un modelo de tabla, llamado **Modelo Relacional**, que corresponde a un estándar en la industria. Con él se define una estructura con columnas: *Nombre*, *Tipo*, *Grados*, *Origen*; representando una cerveza específica por una fila, indicando sus valores en cada columna.
  ![[Pasted image 20260901124920.png]]

## Definiciones

- En el modelo relacional, a **cada tabla** se le denomina una **relación**. En el ejemplo anterior, la tabla completa se llama *relación **Cervezas***.
- A cada **columna** de la tabla se le denomina un **atributo o campo**.
  En el ejemplo, se tienen los atributos *nombre*, *tipo*, *grado* y *ciudad-origen*.
- A cada **fila** se le llama una **tupla** o registro.
  En el ejemplo, la fila compuesta por "Kuntsmann Torobayo", "Ale", "5.1", "Valdivia" constituye una tupla.

- Se utiliza el concepto de **esquema** para definir la estructura de las relaciones. Un esquema especifica el nombre de la relación y el nombre de cada atributo con su dominio (tipo) permitido, de la forma:
```SQL
Cervezas(nombre: string, tipo:string, grados:float, ciudad-origen:string)
```

- Luego, un **esquema de bases de datos** es **un conjunto de esquemas** de relaciones.
```SQL
Cervezas(nombre:string, tipo:string, grados:float, ciudad-origen:string)
Vinos(nombre:string, año:int, tipo:string, grados:float, ciudad-origen:string)
En-Stock(nombre:string, cantidad:int, precio-unitario:int)
```
Se pueden repetir el nombre de atributos en diferentes relaciones (como *nombre* para las relaciones Cervezas y Vinos) pues se pueden especificar usando el nombre de la relación como prefijo.
Por ejemplo `Cervezas_nombre` o `Vinos_nombre`.
\* Pero no se permiten atributos repetidos dentro de una misma relación.


- Una **instancia** de un esquema es un **conjunto de tuplas** para cada relación del esquema.
  En el ejemplo, las instancias son las tuplas que llenan la tabla. Como en vinos contiene las tuplas:
```SQL
(Tarapacá, Carménère, 2014, 13.5, Maipo)
(Gato, Merlot, 2016, 14.0, Maule)
```
el conjunto de tuplas es una instancia puede estar vacío, como por ejemplo que no se tenga nada en stock se verá una tabla sin tuplas.

---

* Agregar más relaciones es mejor: Si atributos comienzas a ser 'atómicos' (o esenciales) entonces se puede tener una relación.
* Los datos que se obtienen a partir de los atributos no se consideran atributos por sí mismos.

## Restricciones de Integridad
Definir una instancia como un conjunto de tuplas implica que no existe un orden predeterminado en las filas, entonces **no se pueden tener filas duplicadas**, en la práctica SQL lo permite si no hay restricción.
Las restricciones de integridad son condiciones formales que deben cumplir las instancias de un esquema para ser considerada 'legal', esto es para verificar la integridad de la información que contiene una base de datos.

### Restricción de Llave

#### Super Llave

**Super Llave**: Es un conjunto de atributos de una relación para el cual no se permiten que existan dos o más tuplas con los mismos valores en tales atributos.
Por ejemplo,
- El conjunto {nombre,tipo} es una super llave pues no existen dos cervezas con exactamente el mismo nombre y tipo
- El conjunto {nombre, tipo, grados, ciudad-origen} es una super llave en la relación Cervezas porque la totalidad de los atributos siempre identifica de manera única a una fila.
- El conjunto {tipo, grados, ciudad-origen} **no** es super llave pues pueden haber dos cervezas distintas que sean del mismo tipo, igual cantidad de grados y que vengan de la misma ciudad.

#### Llave candidata, llave primaria
En bases de datos se busca minimalidad, entonces se define una **llave candidata** como una super llave tal que **no hay un subconjunto propio de sus atributos que sea también super llave**.
> Una llave candidata es la super llave más pequeña posible.

> Puede haber más de una llave candidata, el diseñador escoge una para que sea **llave primaria** que es la cual se utiliza para identificar a las tuplas de la relación.

Por ejemplo, en la relación *Cervezas*, la llave candidata más natural sería {nombre} (asumiendo que cada cerveza tiene nombre único) que además es super llave y esta dentro de la super llave {nombre, tipo, grados, ciudad-origen}.

Una llave es una restricción definida sobre un el esquema, no es una descripción de los datos actuales presentes en una instancia temporal; las restricciones se basan en la semántica y las reglas del negocio, no en una observación empírica de una tabla en un momento dado.
Por ejemplo, en una relación *Vinos* se puede tener:
- Tarapacá (Carmenere)
- Tarapacá (Merlot)
- Gato (Merlot)
y se podría pensar que {nombre} no es llave candidata pero si se ingresa otro Tarapacá Merlot pero de año diferente, {nombre, tipo} dejaría de ser único.

### Dependencia Funcional

Dada una relación y dos conjuntos de atributos X e Y, se dice que:
X determina funcionalmente a Y si y solo si cada valor de C en la relación tiene asociado un solo valor de Y.
Luego, una llave (super o candidata) determina funcionalmente a todos los atributos de la relación.

Por ejemplo:
- Si se tiene el nombre de la cerveza, se puede tener inequívocamente su tipo y ciudad de origen: `nombre -> tipo, ciudad-origen`
- Si se tiene el nombre de una cerveza, se puede saber sus grados sin ambigüedad: `nombre -> grados`

## Modelo Entidad-Relación (ER)

Para mostrar la dificultad de elegir llaves y el diseño de esquemas, se presenta un caso de estudio de Vinos.
Se tiene la tabla *En-Stock*(nombre, cantidad, precio-unitario). Si se usa {nombre} como llave primaria, se tiene ambigüedad si una cerveza y un vino comparten un nombre. Para solucionar:
1. Usar un nombre más específico (ej. "Tarapacá Carménère 2014"). Esto es poco práctico.
2. Crear una súper llave añadiendo el tipo: En-Stock(nombre, tipo, cantidad, precio-unitario).
3. Introducir una llave artificial o "surrogate key", como un identificador único "id". Se tendrían *Cervezas*(id, nombre, tipo...), *Vinos*(id, nombre, tipo...) y *En-Stock*(id, cantidad, precio-unitario).
   Una llave natural tiene significado fuera de la base de datos (como un RUT), mientras que una llave artificial es inventada exclusivamente para el propósito de la base de datos.
4. Combinar las tablas, llevando cantidad y precio-unitario directamente a las relaciones Cervezas y Vinos.

Entonces para diseñar bases de datos relacionales se deben comprender conceptualmente qué se está describiendo. Para ello, se utiliza el diseño conceptual con el modelo Entidad-Relación (ER) que permite **abstraer** el problema.
1. Primero se identifican **Entidades**: Objetos del mundo real distinguibles unos de otros.
   Las entidades se representan mediante un rectángulo.
2. Las entidades se *describen mediante **Atributos***, representados por óvalos. Todo conjunto de entidades debe tener una llave obligatoria, la cual se indica subrayando el atributo correspondiente.
   Por ejemplo, para la entidad *Producto* se tienen los atributos *nombre*, *categoría* y *precio*.
3. Luego, se identifican las **Relaciones**: Asociaciones entre dos o más entidades, se representa mediante un rombo que conecta las entidades.
   Las relacione también pueden tener atributos propios, por ejemplo, para dos entidades *Persona* y *Acciones* se tiene la relación *Compra* y como atributo puede ser *desde*.

![[Pasted image 20260901182730.png]]

### Multiplicidad de Relaciones
Un aspecto esencial es definir la multiplicidad de las relaciones, lo que determina **cuántas instancias de una entidad pueden asociarse con otra**. Si $n$ es desde 0 en adelante:
1. $n$ a $n$: Muchas entidades a muchas entidades.
   Por ejemplo un producto puede ser fabricado por muchas compañías y una compañía puede fabricar muchos productos.
   ![[Pasted image 20260901183146.png]]
2. $n$ a 0 o 1: Para especificar una relación mas estricta tal que significa 'como máximo uno'.
   Un producto es fabricado por cero o una compañía y una compañía puede fabricar muchos productos.
   ![[Pasted image 20260901183414.png]]
   La dirección de la flecha indica que **un** producto se fabrica por como máximo una compañía. 
3. 0 o 1 a $n$:
   Un producto puede ser fabricado por muchas compañías y una compañía puede fabricar cero o un producto.
   ![[Pasted image 20260901183558.png]]
4. 0 o 1 a 0 o 1:
   Un producto puede ser fabricado por cero o una compañía y una compañía puede fabricar cero o un producto.
   ![[Pasted image 20260901183613.png]]

--- 
Restricciones Avanzadas: Restricciones de Participación
Un profesor puede trabajar en 'como máximo' una Universidad, pero se puede ser más restrictivo:
1. Se representa la participación total mediante una línea gruesa que conecta a Profesor con la relación *Trabaja*. Así, no existen entidades *Profesor* flotantes sin asociación.
   ![[Pasted image 20260901184525.png]]
   Luego, cada profesor trabaja en **al menos una** Universidad.
2. Para representar una participación total con restricción de un valor **único**, se señala con una línea gruesa terminada en flecha.
   ![[Pasted image 20260901184635.png]]
   Un profesor trabaja en exactamente una (y solo una) Universidad.

### Relaciones N-arias
Para las situaciones en donde una relación binaria es insuficiente, se pueden conectar más de dos entidades mediante una relación.
Por ejemplo, para el caso de modelar un alquiler de películas que tiene las entidades *Personas*, *Película*, *Local*:
- Se podría solamente relacionar las personas con película, dejando a local como un atributo. Pero este no es un valor simple que se pueda anexar como atributo, pues tiene características propias y el diseño ER dicta que **solamente se deben relacionar entidades**, no atributos de forma aislada.

Las relaciones ternarias son obligatorias cuando la asociación entre los datos asocia obligatoriamente a más de dos entidades y la información no puede ser dividida.

También se puede tener que una entidad participe más de una vez, pero con propósitos distintos en la relación. Esto se indica con la etiqueta de arcos (o "Papeles"). 
Por ejemplo: un escenario en donde una persona podría participar simultáneamente como el `cliente` que arrienda y como el `cajero` que procesa la transacción.
![[Pasted image 20260901202724.png]]

### Jerarquías de Clases
A partir de una entidad con sus atributos, se pueden derivar entidades a partir de ella tal que sea una *especialización* de la instancia mayor.
Por ejemplo, una `Bebida` actúa como una superclase y de ella se derivan las subclases `Vino` y `Cerveza`. Estas heredan los atributos de la superclase tales como origen, nombre y tipo pero **pueden añadir atributos específicos propios** como el año de cosecha para `Vino`.
La instanciación se denota con un triángulo invertido en el sentido de la instanciación con `isA` en su interior.
Se tienen dos restricciones para las jerarquías:
1. Restricciones de Solapamiento: Establecen si una entidad de la superclase puede pertenecer a más de una subclase simultáneamente.
2. Restricciones de Cobertura: Establecen si las entidades de las subclases incluyen de manera colectiva a la totalidad de las entidades de la superclase.

### Entidades Débiles
El enfoque que incluye las jerarquías de clases simplifica el diagrama, pero genera una gran cantidad de valores nulos, como por ejemplo un `idcontrato` en empleados temporales.

Hay entidades **Fuertes**: Aquella que existe por sí misma, denotada con **rectángulo simple**; y **Débil**: la que existe por la existencia de otra entidad, denotada con **rectángulo doble**.
Por ejemplo, del curso CC3201 existe la sección 2. Luego, el curso existe por sí mismo (es una entidad Fuerte) y la sección existe solo porque existe el curso (es una entidad Débil).

Las entidades débiles requieren de una *propiedad identificadora*, estas tienen su propia llave primaria, llamada llave **parcial** que es señalada con un subrayado de línea punteada.
Un ejemplo es un caso de `Beneficiarios` de un empleado. El beneficiario tiene una clave "parcial" llamada `nombreP` como el nombre del dependiente. Luego, para identificar de manera unívoca al beneficiario en *toda* la base de datos se debe combinar su clave parcial con su clave principal de la entidad propietaria. En este caso, el `dni` del `Empleado`.
Toda entidad débil requiere de:
1. Dependencia de llave respecto a la llave primaria de su entidad fuerte.
2. Una relación de tipo "una a varias" desde la entidad Fuerte a la débil.
3. Participación total de la entidad débil en la relación identificadora.

Por ejemplo
![[Pasted image 20260901205452.png]]
y una cadena de entidades débiles:
![[Pasted image 20260901205526.png]]

### Agregación, Entidad Virtual

Si se tiene, por ejemplo, un modelo donde una `Película` tiene un `Local` y una `Persona` alquila **a partir de esa existencia *conjunta***, el modelo clásico no permite trazar una relación conectando una entidad (`Perosona`) directamente con una relación.

La agregación permite **encapsular un conjunto de relaciones**, permitiendo que el sistema lo trate como si fuera una gran entidad; esto se denota con un cuadro de línea discontinua que encierra todos los elementos que se quieran encapsular.
> Se aplica agregación, en vez de una relación $n$aria grande cuando la relación interna **tiene sentido y restricciones *por si misma***, y se relaciona con una tercera entidad, generando atributos propios del nuevo vínculo.

![[Pasted image 20260901210057.png]]

## Modelo ER a Relacional (Lógico)

Se tiene un modelo Entidad-Relación válido, pero los sistemas de gestión operan con tablas, entonces se debe aplicar una transformación.

### Entidad a Tabla
A partir del modelo ER construido:
- La entidad se transforma directamente a una tabla, tal que el nombre de la entidad pasa a ser el nombre de la tabla (en plural).
- Los atributos de la entidad corresponden a las columnas de la tabla
- El atributo subrayado se convierte en la llave primaria, llamada **Primary Key PK** en la tabla relacional. Esta se indica añadiendo una fila debajo de los atributos, señalando PK en el atributo que sea la llave primaria de la entidad.
![[Pasted image 20260901210844.png]]

### Relación a Tabla
Para traducir una relación de tipo $n$ a $n$ se **crea una tabla nueva** tal que su llave primaria se forma **concatenando las llaves primarias** de las entidades que participan en la relación, constituyendo una *superllave* para la nueva tabla.
Por ejemplo para la relación $n$ a $n$ `fabrica` entre las entidades `Producto` y `Compañía`, al considerar la concatenación entre `p_nombre` y `c_nombre`, se tiene una super llave de la relación.
![[Pasted image 20260901211204.png]]

#### Relación con Restricciones (1 a $n$)
Se puede optimizar el diseño combinando tablas cuando un producto es fabricado por una sola compañía. No se necesita una tabla intermedia pues basta con llevar la clave de la compañía como clave foránea (**Foreign Key FK**) hacia la tabla de la entidad que tiene la restricción (o sea `Producto)`.
![[Pasted image 20260901212344.png]]

### Jerarquía de Clases a Tabla

Para traducir una jerarquía que se especializa en dos entidades, se tienen dos alternativas:
1. Si hay cobertura *estricta* y los accesos requieren atributos específicos rápidamente: Crear tablas únicamente para las subclases derivadas, repitiendo los atributos genéricos en ambas.
   \* Asumir que una consulta global requerirá un mayor coste al examinar todas las tablas.
2. Si existe alto solapamiento: Crear una tabla general para la superclase y tablas separadas para las subclases, enlazadas por llaves foráneas.
   Esto pues evita la redundancia de datos.

### Entidades Débiles a Tabla
Ambas relaciones se convierten en tabla y para la entidad débil, además de su clave parcial, esta **hereda** la clave primaria de la entidad fuerte, marcándola como llave foránea.

### Agregación a Tabla
La tabla que mapea el conjunto de relaciones externo incorpora las claves primarias completas de **todos los conjuntos participantes**, incluyendo el bloque agregado en su totalidad.
![[Pasted image 20260901213928.png]]
![[Pasted image 20260901213939.png]]

## Formas Normales
Tener todos los datos en una sola tabla es un mal diseño que mezcla hechos independientes en una misma estructura. Es necesario separar los conceptos y para ello es necesario un lenguaje formal.
> La **dependencia funcional** se denota como $X\to Y$, y dice que:
> Si dos tuplas coinciden en los valores del conjunto de atributos X, entonces obligatoriamente coinciden en los valores del conjunto de atributos Y

Normalizar significa refinar progresivamente el esquema para **reducir redundancia** y proteger la integridad de los datos frente a modificaciones.

Por ejemplo: el ejemplo de la tabla `Inscripción`, observamos las siguientes dependencias funcionales: el RUT determina el nombre del Alumno ($RUT \rightarrow Alumno$); el Curso determina el Nombre del curso y el Profesor ($Curso \rightarrow Nombre curso, Profesor$); y la combinación de RUT y Curso determina la Nota (${RUT, Curso} \rightarrow Nota$).

### 1FN
> Atomicidad:
> Una relación está en 1FN si todos sus atributos son **atómicos**, conteniendo **un solo valor por celda**, sin listas ni grupos repetidos.

Esto pues una celda con una lista no se puede consultas, indexar ni restringir eficientemente.

Por ejemplo, una tabla con los atributos `RUT` y `Cursos` donde la celda de cursos contiene la lista "CC3201, CC4102" viola la 1FN. La solución es transformarla para que contenga un hecho por fila, resultando en **dos filas para ese RUT**, cada una con un curso distinto

### 2FN
La segunda forma normal 2FN requiere que la tabla esté en 1FN y que ningún atributo fuera de la llave depende de una parte propia de una llave candidata
> Prohibe dependencias parciales.

La solución es la descomposición, **extrayendo la dependencia problemática a una nueva tabla** donde su determinante sea la llave completa.
La consecuencia de una dependencia parcial es redundancia.
Por ejemplo, en el esquema `Inscripción (RUT, Curso, Nota, Alumno)` con llave candidata {RUT, Curso}, el atributo Alumno depende exclusivamente del RUT, que es solo media llave y se tiene redundancia: el nombre del alumno se repetirá por cada curso que inscriba. Solución: se extrae la dependencia problemática a una nueva tabla donde su determinante sea la llave completa. Así, descomponemos en `Inscripción (RUT, Curso, Nota)` y `Alumno (RUT, Alumno)`

> Si una relación tiene una llave compuesta por **un solo atributo**, la 2FN se cumple automáticamente.

### 3FN
La tercera forma normal exige que para toda dependencia funcional no trivial $X\to A$, se cumpla alguna de las dos condiciones:
1. $X$ es una superllave
2. $A$ forma parte de alguna llave.

La 3FN elimina las depenedencias transitivas, evitando asi que si hay un cambio en algún atributo se deban actualizar todas las demás que dependen de ella.
- Las dependencias triviales (donde $Y$ es subconjunto de $X$) siempre se cumplen por definición.

Para ilustrarlo, observemos el esquema `Curso (Código, Profesor, Oficina)` con la dependencia Código $\rightarrow$ Profesor $\rightarrow$ Oficina. El atributo Oficina depende del Código, pero de manera indirecta, pasando por el Profesor. Dado que Profesor no es superllave y Oficina no es atributo de la llave, se viola la 3FN. Si el profesor cambia de oficina, deberíamos actualizar todas las filas de los cursos que dicta. La generalización indica que cada hecho debe guardarse una sola vez, por lo que descomponemos en `Curso (Código, Profesor)` y `Profesor (Profesor, Oficina)`.

### FNBC
La tercera forma normal no garantiza la eliminación de absolutamente toda la redundancia por la excepción de que $A$ sea parte de una llave, entonces se introduce la forma normal de Boyce-Codd FNBC.

FNBC establece que para toda dependencia funcional no trivial $X \to A$: $X$ **debe ser obligatoriamente una superllave**. Esta elimina la segunda condición de 3FN. Luego, **toda relación en FNBC está en 3FN**, pero no a la inversa.

Contraejemplo clásico que separa ambas formas: Supongamos la tabla `Dicta(Alumno, Curso, Profesor)` con las dependencias {Alumno, Curso} $\rightarrow$ Profesor, y Profesor $\rightarrow$ Curso (indicando que un profesor dicta un solo curso). Las llaves candidatas son {Alumno, Curso} y {Alumno, Profesor}. La tabla sí está en 3FN porque en la dependencia Profesor $\rightarrow$ Curso, aunque Profesor no es superllave, el atributo Curso se salva por ser parte de una llave candidata. Sin embargo, la redundancia persiste: el hecho "este profesor dicta este curso" se repite por cada alumno inscrito. Esta tabla viola la FNBC porque en Profesor $\rightarrow$ Curso, Profesor no es superllave. Si descomponemos para alcanzar FNBC obtenemos `R1(Profesor, Curso)` y `R2(Alumno, Profesor)`.

> La descomposición hacia FNBC siempre **preserva** la información, o sea que no hay pérdida de datos al reconstruir mediante *join* pues la intersección de las tablas resultantes es llave de una de ellas.
> Pero no siempre preserva las dependencias

Luego, hasta 3FN se debe decidir si se mantiene hasta 3FN aceptando redundancias para garantizar que se preserven las dependiencias, o avanzar hasta FNBC eliminando la redundancia pero posiblemente perdiendo la dependencia, pudiendo exigir validaciones externas complejas.

### Receta para ejercicio de normalización
1. Escribir el esquema y las dependencias funcionales.
    
2. Calcular los cierres, encontrar todas las llaves candidatas y marcar los atributos de las llaves.
    
3. Revisar cada dependencia $X \rightarrow A$: si X no es superllave, hay violación de FNBC.
    
4. Si además A no forma parte de ninguna llave, rompe la 3FN (o 2FN si X es parte de una llave).
    
5. Descomponer la relación problemática R en $R1(X^+)$ y $R2(X \cup (R - X^+))$, repitiendo hasta eliminar violaciones.
    
6. Documentar la decisión verificando si se preservan la información y las dependencias.


# Álgebra y Cálculo Relacional



## Álgebra Relacional

Lenguaje procedimental: Las consultas de componen mediante un conjunto de operadores, y cada consulta describe un procedimiento **paso a paso** para obtener la respuesta.
Se indica qué operadores aplicar y en qué orden

Un operador de álgebra relacional toma uno o dos ejemplares de relación como entrada y devuelve un nuevo ejemplar de relación como resultado.

Operadores:
1. **Selección** $\sigma_{\text{condicion}}$: Permite **filtrar** tuplas de una relación según una condición.
   Esta entrega las tuplas que cumplan la condición.
   - La condición de selección se puede complejizar mediante el uso de operadores lógicos $\land,\lor$
   - El esquema de la relación resultante es idéntico al de entrada.

Por ejemplo, para una relación `Pokédex` y se aplica la operación:
$$
\sigma_{\text{tipo}\text{=}\text{pasto}}(\text{Pokedex})
$$
el resultado es una *nueva relación* con las tuplas de los pokémon cuyos tipos sean "Pasto", o sea, se obtiene una nueva relación que el mismo esquema tal que solamente incluya las tuplas que tienen "Pasto" en la columna Tipo.
Otra operación es aplicar dos condiciones en simultáneo
$$
\sigma_{ATK\leq 100 \land \text{tipo}=\text{pasto}}
$$
en donde se filtra considerando las condiciones en las dos campos.

2. **Proyección** $\pi_{\text{atributo1},\text{atributo2},\dots}$: La proyección extrae **columnas**, se *devuelve una nueva relación* que contiene exclusivamente la columna del atributo indicado.
   - Para extraer más de un atributo, se indican los separandolos por coma (,).
   - El resultado es un conjunto de tuplas, luego, como los conjuntos no tienen elementos duplicados, si varias tuplas tienen el mismo valor para un atributo, éste aparecerá solo una vez. Por ejemplo, si varios Pokémon tienen Tipo *Pasto*, el valor *Pasto* aparecerá una sola vez en el resultado final.

Por ejemplo
$$
\pi_{\text{Tipo}}(\text{Pokedex})
$$
devuelve una nueva relación que contiene solamente la columna `Tipo`, incluyendo los valores *Eléctrico*, *Pasto*, *Roca*, *Normal*, etc.
Si se hace 
$$
\pi_{\text{Nombre},\text{Tipo}}(Pokedex)
$$
se va a tener una relación con las columnas `Nombre` y `Region`, con el nombre con su tipo respectivo para cada pokemon.


Se debe notar que el orden en que se aplican los operadores sí importa, pues si se extrae cierto atributo de una relación aplicando $\pi$ y luego se quiere filtrar por un atributo que no está en la nueva relación con $\sigma$, la operación falla pues la proyección eliminó la columna.

### Operadores de Conjuntos

Son operadores que provienen de teoría de conjuntos: Unión $\cup$, Intersección $\cap$ y diferencia \.
Para que dos relaciones puedan ser sometidas a operaciones de conjuntos, deben cumplir la condición esctricta de ser compatibles para la unión
1. :**Ambas relaciones deben tener el mismo número de campos**
2. Los campos correspondientes, de izquierda a derecha, **deben tener los mismos dominios**.

