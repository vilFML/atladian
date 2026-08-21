Materia: Metodologías
	Fecha cátedra: 05/08/26
	Fecha digitalización: 05/08/26
	*tags:* 

# Python y Scala
Tienen estructura (semántica básica) similar, con distinta sintaxis. Scala tiene tipos.

## Compilador
Un compilador traduce un código escrito en un lenguaje de origen a un lenguaje de destino, como código máquina o *bytecode*.
El proceso de compilación es un buen lugar para el chequeo de tipos.

### Tipos
Un tipo define qué valores pertencen a él y qué operaciones son válidas sobre esos valores.

¿Por qué tener tipos? Una corrección posible cuando se compila el programa es la verificación de tipos. Cuando un programa esta en *bytecode*, es más eficiente que la parte de compilación 'ordene' el programa para que el computador tenga la versión del programa lo más 'expedita' posible.

También es bueno que la mayor cantidad de errores posible 'surjan' cuando se está escribiendo el programa y no luego ya de ser desarrollado o lanzado.

### Chequeo Estático vs Dinámico
* **Chequeo estático**: Correponde a encontrar el error automáticamente antes de que el programa se ejecute.
Es más *conservador*, pueden haber programas que no permita, pero que pueden ser válidos.
* **Chequeo dinámico**: El error se encuentra automáticamente cuando el código se está ejecutando.
* También hay lenguajes que no tienen chequeo, en los cuales se deben detectar manualmente los errores o que haya un riesgo a tener resultados incorrectos sin previo aviso.

## Scala
Acrónimo de *scalable language* pues la intención es poder implementar pequeños scripts hasta grandes sistemas.
Scala combina:
- Programación Orientada a Objetos:
- Programación Funcional:


### Tipos en Scala
Scala es leguaje tipado, o sea que se debe indicar el tipo de dato que se almacena en una variable. De la forma:
```Scala
nombre_variable: tipo
```

esto lo hace pues verifica la compatibilidad de datos antes de ejecutar el programa. Entonces si hay un error de tipos, en Scala no es necesario ejecutar el programa para saber que hay error de tipo.
\* La idea es 'fallar rápido', o sea encontrar los errores lo antes posible para que un programa no escale en tamaño.

Es posible no declarar un tipo, en donde se asigna el tipo indicado según el dato almacenado. Pero en la variable no se podrá almacenar un dato que no sea del mismo tipo.


- `Int`: Entero con signo, de 32 bits. (ej: `5`,`-200`). Tiene rangos $-2^{31},2^{31}-1$, es de cardinalidad
  $|\text{Int}|=2^{32}$
- `Long`: Entero con signo, de 64 bits. Tiene rangos
- `Boolean`
- `Double`
- `Char`
- `String`
- `Unit`: Ausencia de un valor significativo. Tiene cardinalidad $|\text{Unit}|={()}=1$
  > Si es que algo retorna un valor, no se va a usar. Es similar a `void`

### Errores comunes
```Scala
val sum: Int = 0
val n: Int = 0
val avrg: Int = sum/n
```
se tendría un error en tiempo de ejecución pues en Scala no se puede dividir por `0`.


#### Casos Borde
1. Dividir un número por cero entrega infinito
$$
\frac{x}{0,0}=+\infty
$$
2. Para un número negativo, se tiene infinito negativo
$$
-\frac{x}{0,0}=-\infty
$$

3. Dividir 0 en 0 entrega `NaN` (Not a Number)
$$
\frac{0,0}{0,0}=\text{NaN}
$$
### Funciones
Se pueden anotar los tipos de los argumentos y el tipo de retorno de una función.
En python se usa usualmente la notación *'snake_case'*
```python
def are_equal(
	a: int,
	b: int
) -> bool:
	print('equals called')
	return a == b
```

en Scala se usa la notación *camelCase*:
```Scala
def areEqual(
	a: Int,
	b: Int
): Boolean
	println('equals called')
	a == b
```

- 
- Scala no usa `return`, es implícito y siempre **se retorna la última línea**

