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
##### Vocabulario

- **Estado Mutable**: Se refiere a una variable o alguna estructura de datos cuyo contenido puede cambiar a lo largo del programa.

- **Cliente**: El cliente (o código cliente) es la parte del programa que utiliza, consume o interactúa con un servicio o componente provisto por otro objeto.
  Es el elemento que **coordina** las acciones generales sin tener la necesidad de conocer los detalles internos de **cómo** el proveedor realiza las acciones (como solicitar una lista de elementos o pedirle a figuras que se muestren en pantalla).
- **Interfaz**:
  1. Como *contrato* observable: Corresponde al conjunto de operaciones y servicios que un objeto expone a sus clientes. Describe **qué se le puede pedir a un objeto** (como los servicios disponibles), ocultando el *cómo* se realizan las operaciones.
  2. Como *lista de promesas*: (Implementado en código en Scala como `trait`) Premisa de *"si se usa este 'trait', se deben implementar estos miembros".* Permite que el cliente y las implementaciones concretas se desarrollen por separado, dejando que sea necesario ponerse de acuerdo en el contrato compartido.

## Programación Estructurada
Una metodología de programación estructurada es utilizar secuenciación, selección e iteración para organizar el flujo de trabajo, evitando así saltos arbitrarios en el programa.
\* La metodología suele complementarse con *descomposición procedural en funciones*. Esto es la técnica de dividir un problema complejo en subproblemas manejables **mediante la creación de funciones**. 
Por ejemplo, para tener el promedio de una secuencia
```Scala
def sumUpTo(n: Int): Int =
	var sum = 0
	for i <- 1 to n do sum += i
	sum

def average(n: Int):Double =
	sumUpTo(n).toDouble / n
```
en donde se divide el problema en dos funciones `sumUpTo`, donde`for` repite una acción; y la función `average`.

Pero expresar el flujo de control no dice *cómo repartir responsabilidades cuando el sistema crece*.

## Diseñar Programa

Además de estructurar el flujo de control de un programa, se debe considerar la problemática cuando se aumenten los requerimientos, usualmente van a surgir dos problemas fundamentales:
1. **Baja cohesión**: Una función o módulo toma múltiples responsabilidades no necesariamente relacionadas entre sí, o que tienen un distinto nivel de abstracción.
2. **Alto acoplamiento**: Los módulos dependen profundamente de cómo está implementado el código en otros módulos. Luego, un cambio en uno desencadena en fallos en múltiples puntos.
---
Como caso de estudio, se tiene una aplicación gráfica que recibe una colección de figuras y luego se muestran en pantalla.
Para mostrar las figuras se podría crear una función central que se encargue de revisar el tipo de figura para decidir qué función llamar
```Scala
def displayShape(s: Map[String, String]): Unit =
	if s("type") == "square" then
		drawSquare(s)
	else if s("type") == "circle" then
		drawCircle(s)
	else println("Unknown shape type")
```
luego, en el caso de que **el sistema crezca** y se requiera agregar más figuras, sería necesario incluir cada caso, volviendo el código más largo:
```Scala
def displayShape(s: Map[String, String]): Unit =
	if s("type") == "square" then
		drawSquare(s)
	else if s("type") == "circle" then
		drawCircle(s)
	else if s("type") == "triangle" then
		drawTriangle(s)
	else if s("type") == "rectangle" then
		drawRectangl(s)
	...
	
	else println("Unknown shape type")
```

La función `displayShape` tiene **baja cohesión y alto acoplamiento** pues tiene que *saber* demasiado: conocer los nombres de los tipos, las llaves de los diccionarios ("radius", "side") y los detalles internos de representación de las figuras.

\* Además usar un mapeo genérico `Map[String, String]` no garantiza que la llave `"radius"` exista, que esté bien escrita o que su valor sea un número entero válido. Entonces es propenso a errores tipográficos. 

Se realiza entonces un cambio de perspectiva a una orientada a objetos
- **Antes**: El cliente pregunta *'Qué tipo de figura eres'* para decidir qué hacer.
- **Después**: El cliente pide a la figura mostrarse y **cada objeto resuelve cómo hacerlo** por sí mismo.
La tarea del programa no cambia, solamente se redistribuyeron las responsabilidades.

En lugar de esconder los datos en mapeos genéricos y evaluar según el caso que se reciba, se define una interfaz clara y se deja que cada figura implemente su propio comportamiento:
- Cliente **coordina**: Recorre la colección y llama a una operación.
- Figura **encapsula**: Esta sabe cuáles son sus atributos y cómo dibujarse.

```Scala
//Se define una interfaz o 'contrato' conceptual
trait Shape:
	def displayOn(screen: Screen): Unit

//Cada figura encapsula sus propios datos y su forma de dibujarse
class Square(val side: Int, val position: Point) extends Shape:
	//lógica interna del cuadrado para dibujarse a si mismo
	println(s"dibujando cuadrado de lado $side")

class Circle(val radius: Int, val position: Point) extends Shape:
	override def displayOn(screen: Screen): Unit =
	//logica interna del circulo para dibujars a si mismo
	println(s"dibujando un circulo de radio $radius")

```

## Paradigma Orientado a Objetos
El enfoque del paradigma orientado a objetos es en quién toma las decisiones en el código. En lugar de que el cliente inspeccione el tipo de dato para decidir qué hacer, el cliente **delega** la acción al objeto.
> Principio: "Dime, no me preguntes": El cliente **invoca un servicio** y el objeto receptor resuelve internamente la ejecución.

**Las tres perspectivas de Martin Fowler**:
Para analizar un objeto correctamente, **evitando confundir el diseño con el código** se tienen las perspectivas:
1. **Conceptual**: "¿Qué representa en el dominio?", esto modela los conceptos y responsabilidades en el problema.
2. **De Especificación**: "Qué servicios promete ofrecer", lo que define la *interfaz pública* y contratos observables sin revelar detalles.
3. **De Implementación**: "Cómo cumple sus tareas", que define los campos de estado y el código de sus métodos.
Un ejemplo para el caso de estudio de cómo trabajan juntas las perspectivas es:
- Conceptual: Una figura sabe cómo mostrarse
- Especificación:
  ~~~Scala
  def displayOn(screen: Screen): Unit
  ~~~
- Implementación: `Square` utilizasu lado y posición para dibujarse.






### Interfaz de Objeto
La interfaz de un objeto es el **conjunto de operaciones que expone a sus clientes**. Estas describen qué servicios están disponibles y ocultan los detalles de cómo son implementados, permitiendo así que clientes dependan de un **contrato estable**.
\* Conceptualmente, puede ser implementado diferente a `interface` o `trait`.

Por ejemplo, para una especificación de una cuenta de banco, en Scala se puede expresar una interfaz con `trait`:
~~~Scala
trait Account:
	def getBalance: Int
	def withdraw(amount: Int): Boolean
	def deposit(amount: Int): Boolean
~~~
en donde los métodos definidos con `def` definen las operaciones que promete ofrecer la especificación de la cuenta de banco.
**Se definió qué mensajes responde la cuenta, no el cómo lo hace.**

---
Para representar las interfaces, se utiliza UML
![[Pasted image 20260829150309.png]]
https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-class-diagram-tutorial/

En el ejemplo de la cuenta:
![[Pasted image 20260829152939.png]]
que se traduce
~~~Scala
class SimpleAccount(
	var balance: Int,
	var currency : String
) extends Account:
	def getBalance: Int = balance
	def withdraw(amount: Int): Boolean =
		if balance >= amount then
			balance -= amount
			true
		else false
	def deposit(amount: Int): Boolean =
		balance += amount
		true

~~~

### Objeto
Cada objeto encapsula la información y el comportamiento necesarios para cumplir responsabilidades concretas. Una buena distribución intenta mantener relacionadas la información necesaria y las decisiones que dependen de sea información. Por ejemplo:

| Objeto  | Responsabilidades                                     |
| ------- | ----------------------------------------------------- |
| Cliente | - Pide lista de figuras<br>- Pide a figuras mostrarse |
| Figura  | Define cómo mostrarse                                 |
| BDD     | Define cómo obtener lista de figuras                  |

> ¿Cómo descomponer orientado a objetos?
> Los **sustantivos** pueden sugerir **objetos**
> Los **verbos** pueden sugerir **responsabilidades**

y estas se validan según la cohesión, el acoplamiento y cambios esperables.

Un objeto se compone de tres dimensiones esenciales:
1. **Identidad**: Esto distingue de forma única a un objeto de cualquier otro en la memoria, aunque estos compartan datos.
2. **Estado**: Información interna almacenada por el objeto, representado por **campos o variables de instancia** (mutables `var` o inmutable `val`).
3. **Comportamiento**: Operaciones expuestas mediante métodos públicos que conforman su interfaz, implentado mediante **métodos**.

Un ejemplo del nivel de implementación de una cuenta bancaria, se crea un objeto con `object`, y se puede implementar una interfaz de tal objeto con la palabra `extends`.
~~~Scala
object AccountOfBigby extends Account:
	// Estado: Campos
	var balance: Int = 50_000
	val currency : String = "CLP"

// Comportamiento: Métodos
	def getBalance: Int = balance
	def withdraw(amount: Int): Boolean =
		if balance >= amount then
			balance -= amount
			true
		else
			false
	def deposit(amount: Int): Boolean =
		balance += amount
		true
~~~
`extends` requiere que se implementen todos los métodos definidos en el trait `Account`.
\***Nota**: `account` es de tipo `AccountOfBigby` y `Account`

#### Crear Objetos en Scala
1. Se pueden crear objetos de forma *nominal*:
~~~Scala
object Alexander:
	val name: String = "Alexander"
	def talk(): Unit =
		println(name + ": Ed...ward")

@main def run(): Unit =
	val alexander = Alexander
	alexander.talk()
~~~
en donde no se tiene `trait`, luego la interfaz del objeto lo forman `name` `talk`.
\* Alternativamente a la concatenación con `+` de strings, se puede usar la interpolación de cadenas, de la forma `s"..."` en donde se usa `$v` para ingresar una variable en el lugar y `${expr}` para expresiones, como `s"{x.foo}"`.

2. De forma *anónima*
~~~Scala
trait Animal:
	val name: String
	def talk(): Unit

@main def run(): Unit =
	val alexander = new Animal:
		val name: String = "Alexander"
		def talk(): Unit =
			println(s"$name: Ed...ward")
	alexander.talk()

~~~

## Clases como fábricas de Objetos
Una clase es una especie de 'fábrica' de objetos, como una plantilla para instanciarlos. En donde se describe qué valores se necesitan para crear un objeto, su estado y comportamiento.

Por ejemplo, instanciar un perro como animal:
~~~Scala
class Dog(val name: String) extends Animal:
	def talk(): Unit =
		println(s"$name: Woof!")
~~~
en donde **una clase puede tomar argumentos** y se pueden usar esos argumentos en su cuerpo.

#### Ejemplo
~~~Scala
class Dog(val name: String) extends Animal:
	def talk(): Unit =
		println(s"$name: Woof!")

@main def dogMain(): Unit =
	val dog1: Animal = new Dog("Alexander")
	dog1.talk()
	val dog2: Animal = new Dog("Bond")
	dog2.talk()
~~~
![[Pasted image 20260829152730.png]]
en donde `dog1` y `dog2` tienen la misma implementación. Y visualizando en diagrama UML:
![[Pasted image 20260829152830.png]]
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




