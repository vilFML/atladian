Materia: Metodologías
	Fecha cátedra: 05/08/26
	Fecha digitalización: 05/08/26
	*tags:* 

# Introducción a Scala
## Compilador
Un compilador traduce un código escrito en un lenguaje de origen a un lenguaje de destino, como código máquina o *bytecode*.
El proceso de compilación es un buen lugar para el chequeo de tipos.

## Chequeo Estático vs Dinámico
* **Chequeo estático**: Correponde a encontrar el error automáticamente antes de que el programa se ejecute.
Es más *conservador*, pueden haber programas que no permita, pero que pueden ser válidos.
* **Chequeo dinámico**: El error se encuentra automáticamente cuando el código se está ejecutando.
* También hay lenguajes que no tienen chequeo, en los cuales se deben detectar manualmente los errores o que haya un riesgo a tener resultados incorrectos sin previo aviso.

## Tipos
Un tipo define qué valores pertencen a él y qué operaciones son válidas sobre esos valores.

¿Por qué tener tipos? Una corrección posible cuando se compila el programa es la verificación de tipos. Cuando un programa esta en *bytecode*, es más eficiente que la parte de compilación 'ordene' el programa para que el computador tenga la versión del programa lo más 'expedita' posible.

También es bueno que la mayor cantidad de errores posible 'surjan' cuando se está escribiendo el programa y no luego ya de ser desarrollado o lanzado.

## Scala
Scala es acrónimo de *scalable language* pues la intención es poder implementar pequeños scripts hasta grandes sistemas con el mismo lenguaje. Scala combina la programción funcional con la programación orientada a objetos.

### Tipos en Scala
Scala es leguaje tipado estático, en estos, los tipos de datos de las variables se verifican en tiempo de compilación. Esto pues se verifica la compatibilidad de datos antes de ejecutar el programa, verificando que se tienen operaciones válidas para los tipos usados.
\* La idea es 'fallar rápido', o sea encontrar los errores lo antes posible para que un programa no escale en tamaño estando defectuoso.

Para definir una variable en Scala, se hace de la forma:
```Scala
nombre_variable: tipo
```

Y tiene de tipos:
- `Int`: Entero con signo, de 32 bits. (ej: `5`,`-200`). Tiene rangos $-2^{31},2^{31}-1$, es de cardinalidad
  $|\text{Int}|=2^{32}$
- `Long`: Entero con signo, de 64 bits. Tiene racdcngos
- `Boolean`
- `Double`
- `Char`
- `String`
- `Unit`: Ausencia de un valor significativo. Tiene cardinalidad $|\text{Unit}|={()}=1$
  > Si es que algo retorna un valor, no se va a usar. Es similar a `void`

---
Errores comunes:
```Scala
val sum: Int = 0
val n: Int = 0
val avrg: Int = sum/n
```
se tendría un error en tiempo de ejecución pues en Scala no se puede dividir por `0`.


#### Inferencia de Tipos
En lenguajes de tipado estático se tiene poca flexibilidad pero se es más explícito con respecto al propósito de variables (fuera de su identificador), provocando una mayor verbosidad.
Para evitar mucha verbosidad, en Scala es posible no declarar un tipo con la **inferencia de tipos** en donde el compilador asigna el tipo indicado según el dato que se almacenará en la variable, siendo no necesario expicitar el tipo de la variable.

Por ejemplo:
```Scala
val band = "System of a Down"
val favoriteAlbum = "Toxicity"
val listeningSessions = 3
val currentlyPlaying = true
```
aunque no se indica explícitamente el tipo de cada variable, Scala infiere los tipos de la forma:
```Scala
val band: String = "System of a Down"
val favoriteAlbum: String = "Toxicity"
val listeningSessions: Int = 3
val currentlyPlaying: Boolean = true
```



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

#### Diferencia entre `val` y `var`
En Scala se distingue entre **referencias** que pueden reasignarse con:
1. Referencia reasignable: `var`
2. No reasignable: `val`

Entonces por ejemplo:
```Scala
val band = "System of a Down"
var currentAlbum = "Toxicity"

currentAlbum = "Mezmerize"   //reasignacion
```
la reasignación de `currentAlbum` es válida pues fue declarada con `var`. En cambio hacer:
```Scala
band = "Scars on Broadway"
```
no compilará pues `band` fue declarada con `val`, indicando que la referencia no puede reasignarse.
#### Ejemplo: Estado mutable y recursión
Este archivo contiene dos implementaciones de una secuencia de Hailstone.

A partir de un entero positivo `n`, se aplican repetidamente estas reglas:

- si `n` es par, el siguiente valor es `n / 2`;
- si `n` es impar, el siguiente valor es `3 * n + 1`.

Por ejemplo, comenzando en `3`:

```
3 → 10 → 5 → 16 → 8 → 4 → 2 → 1
```

Esta transformación está asociada a la **conjetura de Collatz**, que afirma que este proceso alcanza `1` para cualquier entero positivo. Esta propiedad no ha sido demostrada en general (Lagarias, 1985).

En este módulo no intentaremos estudiar la conjetura: solo utilizaremos la secuencia como un ejemplo pequeño que permite comparar dos formas de organizar un cálculo.

##### `itHailstone`: mantener el estado con `var`
La primera implementación comienza con:

```scala
var r: Int = n
```

Durante la ejecución, `r` representa el término actual de la secuencia.

Por ejemplo:

```
r = 3
r = 10
r = 5
r = 16
...
```

En cada iteración del `while`, el programa:

1. observa el valor actual;
2. calcula el siguiente;
3. reemplaza `r` por ese nuevo valor.

Podemos pensar en `r` como el **estado actual del cálculo**.

Esta implementación necesita `var` porque la referencia `r` se reasigna repetidamente.

##### `recHailstone`: pasar el estado como argumento
La segunda implementación no mantiene el término actual en una variable mutable.

En cambio, cada llamada:

```scala
recHailstone(n)
```

recibe como argumento el término que debe procesar.

Cuando necesitamos continuar, hacemos una nueva llamada con el término siguiente:

```scala
recHailstone(n / 2)
```

o:

```scala
recHailstone(3 * n + 1)
```

La condición:

```scala
n == 1
```

es el **caso base**: cuando se cumple, la función deja de llamarse recursivamente.

Podemos resumir la diferencia así:

```
itHailstone
    ↓
el término actual vive en una variable mutable

recHailstone
    ↓
el término actual se pasa como argumento
```

Ambas implementaciones describen esencialmente el mismo proceso, pero organizan de manera distinta la información necesaria para continuar el cálculo.

Por ahora no buscamos concluir que una forma sea siempre mejor que la otra. El objetivo es reconocer ambas estrategias y poder razonar sobre sus diferencias.
#### Unit

El entry point del ejemplo termina con:

```scala
recHailstone(3): Unit
```

Esto puede resultar extraño al principio porque `recHailstone` retorna un `Int`:

```scala
def recHailstone(n: Int): Int
```

Sin embargo, en `hailstones` no nos interesa utilizar ese resultado. Solo queremos ejecutar la función y observar los valores que imprime.

El entry point está declarado como:

```scala
@main def hailstones(): Unit =
```

`Unit` representa que esta función no entrega un resultado significativo a quien la invoca.

La expresión:

```scala
recHailstone(3): Unit
```

hace explícito que **queremos descartar el `Int` producido por `recHailstone`**.

No modifica la ejecución de `recHailstone` ni transforma el entero mediante una operación como `toDouble`. Simplemente indica que su resultado no será utilizado.

Sin `: Unit`, el compilador puede advertir:

```
discarded non-Unit value of type Int.
Add `: Unit` to discard silently.
```

El mensaje nos está indicando que calculamos un valor y luego lo ignoramos. Agregar `: Unit` hace explícito que ese descarte es intencional.

Este es un pequeño ejemplo de cómo los tipos también pueden ayudarnos a hacer visibles ciertas decisiones del programa.

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
 
- Scala no usa `return`. Este es implícito y siempre **se retorna la última línea**



# Programación Orientada a Objetos
## Clases y Objetos
En una orientación a objetos, cada valor es un objeto y las definiciones de su comportamiento se definenn en clases o *traits*. 
Una **clase** define una plantilla, o sea **un tipo de dato estructurado**, que combina:
- Estado mediante los atributos o campos de la clase.
- Comportamiento por métodos.

Para definir una clase, es de la forma:
```Scala
class nombreClase (var idVar1: tipo, var idVar2: tipo, ...){
	def idMetodo1(atributo1: tipo1, atributo2: tipo2,...): Unit={
		...
	}
}
```

La clase actúa como un *molde* para nuevas variables que vayan a utilizar esta forma y comportamiento. Para utilizar la clase se crean *instancias* que son **objetos concretos** con la forma de la clase. Para crear una neuva instancia, se utiliza la palabra clave `new` como:
```Scala
val idVariable1 = new Clase(atributo1, atributo2, ...)
```


Por ejemplo, para definir una clase `Punto` que tenga dos campos mutables `x` e `y`, con un método `mover` que ajusta las coordenadas del punto:
```Scala
class Punto(var x: Int, var y: Int){
	def mover(dx: Int, dy: Int): Unit = {
		x = x + dx
		y = y + dy
	}
}
```

## Programación Estructurada
Una metodología de programación estructurada utiliza la secuenciación, selección e iteración para organizar el flujo, evitando así saltos arbitrarios.
\* Suele complementarse con descomposición procedural en funciones.

