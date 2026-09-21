# Formalización de Consultas
El álgebra relacional permite definir preguntas sobre relaciones en una base de datos **de forma general y sin ambigüedad**. Esto provee las bases teóricas de los lenguajes de consulta modernos como SQL, además de permitir la optimización de consultas mediante operaciones entre los operadores.
En el modelo de la relacional, tanto las entradas como los resultados de las consultas **son relaciones**, lo que permite anidar expresiones y construir consultas sobre los mismos resultados de consultas previas.

**Relación**: $R$ es una *relación*, esto es **una referencia a una tabla**, o sea que devuelve las filas de la tabla.

# Operaciones

Las operaciones sobre una sola relación son la selección y la proyección. 

## Selección
La operación de selección se denota por $\sigma$ y esta **devuelve una relación** conteniendo únicamente las tuplas que satisfacen una condición específica, dada por la operación.
Por ejemplo, para una Pokédex, la operación $\sigma_{HP>60}(\text{Pokedex})$ evalúa la tabla *Pokédex* de entrada y se extraen filas tal que se descartan aquellas cuyo valor en el campo HP sea 60 o menor.

Las condiciones pueden utilizar =, >, $\neq$, etc. y se pueden combinar condiciones con $\land, \lor$.

---
De forma general, el operador de selección $\sigma$:
$$
\sigma_{\text{Condicion}}(R)
$$
evalúa una combinación booleana de términos para determinar la filtración de cada tupla de $R$.

## Proyección

La operación de proyección se denota con $\pi$ y esta **extrae columnas** específicas de una relación.
Ejemplo: En la relación *Pokédex*, hacer la operación $\pi_{\text{Tipo}}(\text{Pokedex})$ reduce la tabla a una única columna con los valores Eléctrico, Pasto, Roca, Normal y Fantasma. 

El resultado de una proyección **es un conjunto**, esto implica que los valores duplicados desaparecen en la relación resultante.

---
De forma general, para una relación $R$, la operación:
$$
\pi_{A_{1},A_{2},\dots,A_{n}}(R)
$$
devuelve una nueva relación que deje solo los atributos $A_{1},A_{2},\dots,A_{n}$ de $R$.

## Orden de Operadores

El orden de aplicación de los operadores **altera la viabilidad** de la consulta, pudiendo tenerse errores en la aplicación de las operaciones. Por ejemplo, hacer $\sigma_{01-01-19\leq\text{capturado}}(\pi_{\text{Tipo}}(Pokedex))$ resulta en un error pues primero se hace una proyección para obtener solamente el *Tipo*, borrando la columna de la *Fecha*. Entonces es imposible que la selección posterior evalúe su condición sobre la tabla resultado.

# Combinación de Relaciones
El álgebra relacional define operaciones de conjuntos para combinar múltiples relaciones. Para aplicar las operaciones de unión, intersección y diferencia, las relaciones **deben ser comptabiles** para la unión. Esto es, tener el mismo número de campos y los campos correspondientes deben poseer los mismos dominios.
