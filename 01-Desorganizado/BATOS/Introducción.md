
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


[[Modelo Relacional]]
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

