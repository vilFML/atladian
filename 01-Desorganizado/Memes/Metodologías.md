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




[[01-Desorganizado/Memes/Testing]]
# Abstracciones
## Creación de Objetos (Constructor)

En programación orientada a objetos, la decisión del diseño del objeto es algo fundamental. Las **clases** definen tanto los tipos de los objetos como la forma en la que se inicializan.
En este punto es importante el **constructor**, el cual es el *método* responsable de crear el objeto en memoria e inicializar su estado interno.
Por ejemplo, para definiciones de clases
```Scala
class Person(var name: String, var age: Int)
class Musician(var name: String, var role: String)
class Book(var title: String, var author: Person, var year: Int)
class Movie(var name: String, var director: Person, var year: Int)
```
al hacer
```Scala
new Musician("Masahi Hamauzu", "Composer"):
//...
```
se está **instanciando** un objeto, en donde el constructor:
1. **Crea el objeto**: solicita al sistema reservar el espacio de memoria necesario.
2. **Inicialización**: Se define el estado y sus comportamientos.

\* En lenguajes anteriores era necesario asignar la memoria explícitamente (como `malloc()` en C) y luego inicializar es un proceso separado. En lenguajes orientados a objetos modernos, la asignación de memoria es manejado por la máquina virtual y el programador es el que define la lógica de inicialización.

---

Ejemplo de inicialización completa
```Scala
import java.awt.Color
class ColorPoint(
	var x: Double,
	var y: Double
):
	//color parte como None
	var color: Option[Color] = None
	
	//metodo asigna color
	def setColor(c: Color): Unit =
	color = Some(c)
```
el problema de este diseño es que si no se invoca el método `setColor` inmediatamente al instanciar un objeto `ColorPoint`, se tendrá un objeto incompleto o inconsistente.
Un buen diseño del constructor previene estados inválidos.

## Campos de Objeto
> Los campos del objeto representan **su estado**.


Una vez instanciada una clase, se pueden acceder a los campos del objeto. Estos campos siguen la regla de mutabilidad según si está definido con `val` o `var`, respectivamente.



Por ejemplo,
```Scala
val m = new Musician("Kai Hansen", "Guitarist")
println(m.name) // > Kai Hansen
println(m.role) // guitarrista
```

## Constructores Auxiliares
Toda clase tiene su constructor primario, pero estas pueden requerir *múltiples formas de inicialización* entonces se pueden añadir inicializaciones alternativas con constructores **secundarios** o auxiliares.
En Scala los constructores auxiliares se definen de la forma
```Scala
def this(..)
```

En Scala los constructores auxiliares **deben delegar** la operación de inicialización al constructor primario, ya sea directa o indirectamente invocando `this(...)` **como primera instrucción**.
\* La instrucción `this` hace referencia a la misma entidad en donde se está escribiendo. En este caso, `this()` se refiere al constructor principal de la clase en donde se está implementando el constructor auxiliar, entregando los respectivos parámetros como si estuviese instanciando fuera de él.

Por ejemplo, para una clase `Student` que permite la creación de objetos con tres niveles de especificidad: Entregando todos los datos, omitiendo la fecha (asumiendo la actual) u omitiendo la decha y el ID, generando uno a partir del nombre.
```Scala
class Student(val name: String, val id: String, val enrollmentDate: LocalDate):
  
  def this(name: String, id: String) =
    this(name, id, LocalDate.now())
    
  def this(name: String) =
    this(name, name.take(3).toUpperCase + "-000")
```
en donde en cada método definido con `this()`, se agrega la instrucción `this()` que hace referencia al constructor de la clase `Student`, entregando los valores de los parámetros que se deseen. Luego, la instanciación de un estudiante se adaptará según lo que se ingrese en el flujo principal.

## Parámetros por Defecto
Una alternativa a tener múltiples constructores secundarios son los parámetros por defecto, que permiten crear constructores más flexibles, evitando la duplicación de definiciones.
Para crear un objeto, el compilador sigue el orden de prioridad según:
1. Argumentos nombrados **explícitamente**.
2. Argumentos posicionales.
3. Parámetro ausente: asignación al valor por defecto.

Por ejemplo,
```Scala
class Socket(val timeout: Int = 5000, val linger: Int = 5000)
@main def socketExample(): Unit =
val s1 = Socket() // timeout = 5000, linger = 5000
val s2 = Socket(1000) // timeout = 1000, linger = 5000
val s3 = Socket(1000, 2000) // timeout = 1000, linger = 2000
val s4 = Socket(linger = 3000) // timeout = 5000, linger = 3000
val s5 = Socket(timeout = 1000, linger = 3000) // timeout = 1000, linger = 3000
val s6 = Socket(linger = 3000, timeout = 1000) // timeout = 1000, linger = 3000
```

---

El cuerpo entero de una clase actúa como parte del constructor principal. Por ejemplo, el flujo de inicialización
```Scala
class A(val x: Int):
  print("a")
  
  def this(x: String) =
    this(x.toInt)
    print("b")
    
  def this() =
    this("0")
    print("c")
    
  print("d")
```
Si el cliente invoca `new A()`, el flujo de ejecución es:
1. Se invoca el constructor auxiliar sin parámetros `def this()`.
    
2. Su primera instrucción es `this("0")`, que delega al segundo constructor auxiliar pues es el constructor que se utiliza cuando se ingresa 1 argumento de tipo `string`.
    
3. El segundo constructor invoca `this(x.toInt)`, que delega al constructor primario, pasando el entero `0`.
    
4. El constructor primario evalúa el cuerpo de la clase secuencialmente. Imprime `"a"` y luego imprime `"d"`.
    
5. El control retorna al constructor que lo invocó (el segundo auxiliar), el cual ejecuta su siguiente instrucción e imprime `"b"`.
    
6. Finalmente, el control retorna al primer constructor auxiliar, que imprime `"c"`.
    

La salida estándar será, en consecuencia, `adbc`.

## Diseño Estructural

### Traits
Un `trait` define un **contrato**: Este especifica el comportamiento de un objeto (el *qué* hace), pero no se entrega la implementación de tal comportamiento, delegando la implementación a cada clase.
- Regla práctica: Si múltiples clases deben acatar las mismas reglas pero implementarlas de formas distinta, se debe **extraer el comportamiento a un `trait`**.
\* Scala permite implementación por defecto dentro de un `trait`, pero se van a limitar solo a interfaces puras.

![[Pasted image 20260830203640.png]]

De esta manera el código cliente y las implementaciones pueden probarse por separado y solo necesitan ponerse de acuerdo en la interfaz mediante el `trait`.

> Implementar un trait permite que una clase sea más formal respecto del
comportamiento que promete proporcionar: el compilador se asegura de
que la clase realmente cumpla todas las promesas de cada trait.

---

Por ejemplo
```Scala
trait Legged:
  val numLegs: Int
  def walk(): Unit

class AkitaInu(val name: String) extends Legged:
  override val numLegs: Int = 4
  override def walk(): Unit = println(s"$name is walking on its $numLegs legs.")
```
la clase `AkitaInu` firma el contrato al utilizar la palabra clave `extends`. Si se omite la implementación de `numLegs` o `walk()` el compilador entrega un error pues la clase **falla en cumplir las promesas establecidas en la abstraccioń** `Legged`.
El uso de `override` es para **explicitar** que se está entregando la implementación de un miembro abstraído.

---

Los `trait` pueden extender a otros para apilar capacidades, por ejemplo:
```Scala
trait Camera:
	def takePhoto(): Unit

trait Phone:
	def makeCall(number: String): Unit
	// A Smartphone extends both capabilities
trait Smartphone extends Camera, Phone
```

### Polimorfismo de Tipos
> Programa sobre abstracciones, no sobre implementaciones.

Si se diseña una función `def putShoes(d: AkitaInu)`, la función está rígidamente acoplada a una clase concreta. Si se utiliza el contrato: `def putShoes(d: Legged)`, la función operará correctamente con cualquier clase actual o futura que implementa `Legged` lo que aumenta la reutilización del código.

Lo último funciona gracias al polimorfismo de subtipos, que se define como:
El tipo B es un subtipo del tipo A si cualquier contxto que espera una expresión del tipo A puede aceptar una expresión de tipo B sin erorres.
El subtipado corresponde a una relación "es un" entre tipos, notando que no necesariamente se tiene la relación inversa (Todo perro es un animal pero no todo animal es un perro).

> El polimorfismo de subtipos permite escribir código una vez y reutilizarlo para muchos subtipos.

Por ejemplo, si `Dog` es un `Animal`, se puede usar un `Dog` en cualquier lugar en donde se espera un `Animal`. Luego `Dog` es un subtipo de `Animal`.

\* En lenguajes de tipado dinámico (como Python), el subtipado es implícito: Si el objeto tiene los métodos correctos, simplemente funciona. En lenguajes de tipado estático, se debe explicitar el subtipado para evitar un error de compilación.

##### Caso de estudio: Árbol Binario
Implementando un árbol binario, que permita calcular la suma de sus nodos y enconrtar los valores mínimos y máximos.
Una aproximación procimental incrustada en objetos, podría ser:
```Scala
class Tree(var value: Int, var left: Option[Tree], var right: Option[Tree]):
	def sum: Int =
	    val rightSum = if right.isDefined then right.get.sum else 0
	    val leftSum = if left.isDefined then left.get.sum else 0
	    value + rightSum + leftSum
```
el defecto metodológico de este enfoque se puede observar en una cita de William Cook: "Un modelo de programación que permita inspeccionar la representación de más de una abstracción al mismo tiempo no es orientado a objetos." O sea que utilizar estructuras de control como `if left.isEmpty` para verificar el estado de la representanción (en este caso, un `Option` o ver si es nulo) acopla la lógica de control estructural dentro de un solo bloque centralizado.
Una solución orientada a objetos utiliza polimorfismo para distribuir responsabilidades:
```Scala
trait Tree:
  def sum: Int
  def min: Int
  def max: Int

class Leaf(val value: Int) extends Tree:
  override def sum: Int = value
  override def min: Int = value
  override def max: Int = value

class InternalNode(val value: Int, val left: Tree, val right: Tree) extends Tree:
  override def sum: Int = value + left.sum + right.sum
  override def min: Int = math.min(value, math.min(left.min, right.min))
  override def max: Int = math.max(value, math.max(left.max, right.max))
```
En este modelo, la abstracción es `Tree`. Se tienen dos implementaciones concretas, en los cuales:
`InternalNode` no inspecciona si `left` o `right` están vacíos, este deleha la responsabilidad invocando `left.sum` y el mecanismo de despacho dinámico dle polimorfismo de subtipos determina si se ejecuta la lógica de `Leaf` o de `InternalNode`. 
El código es **modular** y no tiene estructuras de control condicional para manejar los tipos lógicos.

# Clases Abstractas

Caso de estudio: Implementación de listas.
Una lista es una colección o secuencia ordenada que soporta operaciones: Inserción, acceso por posición y búsqueda de elementos.

Para la implementación de listas, surge el diseño de ellas: Debería ser una clase o un `trait`?

Las intefraces (`trait`) definen el contrato: Qué puede hacer una lista sin entregar el cómo lo hace. Luego, se define `SimpleList` como una interfaz y a partir de ella se extiende una segunda interfaz `MutableList` que hereda la primera y además añade la operación de mutación `add(...)`:
```Scala
trait SimpleList:
	def get(index: Int): Option[Any]
	def contains(value: Any): Boolean
	def indexOf(value: Any): Int

trait MutableList extends List:
	def add(index: Int, value: Any): Unit
```
en UML:
![[Pasted image 20260831163821.png]]
en donde la flecha denota una relación de generalización, apuntando desde la interfaz más específica a la más general.

> Las interfaces definen **qué** puede hacer una lista. Para crear una lista, se necesita una clase.

Para crear una lista, se pueden implementar de distintas formas que ofrezcan la misma interfaz, pero tienen comportamiento distinto en su interior: Lista basada en arreglo (bloques de memoria contiguos), lista enlazada (nodos conectados por referencias), etc.

##### Ejemplo: Lista basada en Arreglo

Viendo la implementación de lista basada en arreglos:
```Scala
class ArrayList(capacity: Int = 10) extends MutableList:
var size: Int = 0
var data: Array[Any] = new Array[Any](capacity)
override def add(index: Int, value: Any): Unit =
if index < 0 || index > size then println("Index out of bounds")
else
if size == data.length then
val newData = new Array[Any](data.length * 2)
for i <- 0 until size do newData(i) = data(i)
data = newData
for i <- size - 1 to index by -1 do data(i + 1) = data(i)
data(index) = value
size += 1
override def get(index: Int): Option[Any] = ???
override def contains(value: Any): Boolean = ???
override def indexOf(value: Any): Int = ???
```
La clase se define estableciendo una capacidad inicial: `class ArrayList(capacity: Int = 10) extends MutableList`. Internamente, requiere mantener el tamaño actual `var size: Int = 0` y el arreglo subyacente `var data: Array[Any] = new Array[Any](capacity)`. El método `add` presenta una complejidad particular que debemos analizar línea por línea:

1. Se valida que el índice esté dentro de los límites: `if index < 0 || index > size then println("Index out of bounds")`.
    
2. Si el índice es válido, se verifica si el arreglo subyacente está lleno: `if size == data.length`.
    
3. De estar lleno, se debe redimensionar. Se crea un nuevo arreglo con el doble de capacidad: `val newData = new Array[Any](data.length * 2)`.
    
4. Se copian los elementos del arreglo antiguo al nuevo mediante una iteración: `for i <- 0 until size do newData(i) = data(i)`.
    
5. Se actualiza la referencia del arreglo interno: `data = newData`.
    
6. A continuación, para insertar el nuevo valor, se deben desplazar los elementos existentes hacia la derecha para hacer espacio: `for i <- size - 1 to index by -1 do data(i + 1) = data(i)`.
    
7. Finalmente, se inserta el valor en la posición solicitada `data(index) = value` y se incrementa el tamaño `size += 1`.
    

Por su parte, el método `get` en el `ArrayList` es de acceso directo: verifica si el índice es válido y retorna `Some(data(index))`, o `None` en caso contrario.

##### Ejemplo: Lista Enlazada
```Scala
class LinkedList extends MutableList:
	var size: Int = 0
	var first: Option[Node] = None
	var last: Option[Node] = None
	
	override def add(index: Int, value: Any): Unit =
		if index < 0 || index > size then println("Index out of bounds")
		else
			val newNode = new Node(value)
			val after = getNode(index)
			if after.isDefined then ???
			else ???

	override def get(index: Int): Option[Any] = ???
	override def contains(value: Any): Boolean = ???
	override def indexOf(value: Any): Int = ???
	def getNode(index: Int): Option[Node] = ???
```

A diferencia del arreglo, esta clase no utiliza memoria contigua, sino referencias a un objeto `Node`. La clase `Node` almacena un valor `val value: Any` y dos referencias opcionales: `var next: Option[Node] = None` y `var prev: Option[Node] = None`. La clase `LinkedList` mantiene referencias al primer y último nodo: `var first: Option[Node] = None` y `var last: Option[Node] = None`. Analicemos la lógica de inserción `add`:

1. Se instancia el nuevo nodo: `val newNode = new Node(value)`.
    
2. Se busca el nodo en la posición actual mediante un método auxiliar: `val after = getNode(index)`.
    
3. Si el nodo destino existe (`after.isDefined`), procedemos a ajustar los punteros:
    
4. El siguiente del nuevo nodo apunta al nodo encontrado: `newNode.next = after`.
    
5. El previo del nuevo nodo apunta al previo del nodo encontrado: `newNode.prev = after.get.prev`.
    
6. Se actualiza la referencia del nodo anterior para que apunte al nuevo nodo. Si el previo era vacío, el nuevo nodo pasa a ser el primero: `if after.get.prev.isEmpty then first = Some(newNode)`. Si no era vacío, se actualiza el puntero `next` de dicho nodo previo: `else after.get.prev.get.next = Some(newNode)`.
    
7. Finalmente, el nodo desplazado ahora tiene como previo al nuevo nodo: `after.get.prev = Some(newNode)` y se incrementa el tamaño `size += 1`.

## Asociación y Composición
Se define la **asociación** como una relación general donde un objeto usa a otro, pero ambos pueden existir independientemente.

Por ejemplo, una clase `Library` contiene una lista de libros `var books: List[Book] = Nil`.
```Scala
package cl.uchile.dcc
package library

class Library:
  var books: List[Book] = Nil
```
```Scala
package cl.uchile.dcc
package library

class Book
```
los libros existen de forma independiente a la biblioteca.

La **Composición** es una forma estructa de asociación que implica *propiedad y dependencia*: **Las partes no pueden existir sin el todo**. Por ejemplo,
un `Engine` es parte intrínseca de un `Car`. Si el auto es destruido en memoria, el motor deja de existir en ese contexto.
```Scala
package car
class Car:
	val engine = new Engine
	
		@return
	def start(): String =
		engine.start()
```
```Scala
package car
class Engine:
		@return
	def start(): String =
		"Engine started"
```


Finalmente, la relación entre una lista enlazada `LinkedList` y los nodos `Node` es de composición pues los nodos carecen de sentido (u operabilidad) fuera de la lista que los contiene.

## Clases Abstractas

Si se quiere expandir el requerimiento de las listas tal que se agreguen nuevos métodos para una lista mutable `MutableList` como para agregar un elemento al final de la lista y para agregar múltiples elementos, se tienen un problema de diseño metodológico: El código en ambos métodos es **exactamente idéntico** en ambas clases:
- para `add(value: Any)`, ambas clases llaman a `add(getSize, value)`
- para `addAll`, ambas clases iteran sobre la colección en reversa llamando al método `add` posicional.
es posible no duplicar el código en cada implementación utilizando clases abstractas.

Dado que los `trait` en este contexto definen exclusivamente contratos, se requiere una abstracción intermedia que comparta la implementación en común.

### Clase Abstracta
Una clase abstracta se puede definir como una **clase incompleta**, y se declara usando la palabra reservada `abstract`, de la forma:
```Scala
abstract class AbstractMutableList extends MutableList
```

- Las clases abstractas no pueden ser instanciadas, o sea no se puede hacer `new AbstractMutableList()`, ya que existe solamente para ser extendida. Además puede contener métodos abstractos (o sea no implementados) que deben ser proporcionadas por las subclases.
- Las clases abstractas no deberían usarse como tipos; en su lugar, se deben usar interfaces (o `trait` en Scala).

### Clase Concreta
Una clase concreta **debe implementar** o heredar las implementaciones de:
1. Métodos de interfaces implementadas directamente.
2. Métodos de todas las interfaces "padre" transitivamente.
   Si C extiende B, y B extiende A, entonces C también debe imple,entar los métodos de A.
3. Todos los métodos abstractos que hereda.

Por ejemplo, 
```Scala
abstract class AbstractMutableList extends MutableList:
  override def add(index: Int, value: Any): Unit // Método abstracto
  override def get(index: Int): Option[Any]      // Método abstracto
  
  override def add(value: Any): Unit =
    add(getSize, value)                          // Método concreto reutilizable
    
  override def addAll(index: Int, values: List[Any]): Unit =
    for value <- values.reverse do add(index, value) // Método concreto reutilizable
```
luego `ArrayList` y `LinkedList` extienden de `AbstractMutableList` en lugar de extender directamente la interfaz, heredando la implementación de `add` y `addAll`, quedando necesaria la implementación `add(index, value)`

```Scala
class ArrayList(capacity: Int = 10) extends AbstractMutableList:

	override def get(index: Int): Option[Any] =
		if index < 0 || index >= size then None
		else Some(data(index))
```
```Scala
class LinkedList extends AbstractMutableList:

	override def get(index: Int): Option[Any] =
	val node = getNode(index)
	if node.isDefined then Some(node.get.value)
	else None
```
se sobrescribe **solo lo que cambia**, no es necesario sobrescribir `add(Any)` ni `addAll(Int, List[Any])`
En UML:
![[Pasted image 20260831172352.png]]
en donde:
- *cursiva indica "abstracto"*
- Flecha continua: Herencia entre clases o entre traits
- Flecha discontinua: Implementación de interfaz por una clase.

---

Se establecen tres roles claros en la jerarquía:
1. `trait` define un contrato.
2. Clase Abstracta: Comparte implementación común y deja partes por completar.
3. Clase concreta: Proporciona una implementación completa e *instanciable*.

### Herencia
Una clase define una familia de objetos: Define su estado y comportamiento; Sus instancias comparten esa definición.

La herencia **expresa especialización**, en donde una subclase representa una versión más específica de su superclase y puede heredar y refinar estados y comportamientos de su clase.
\*La superclase puede concentrar una implementación común, pero compartir código no basta para justificar una relación de herencia.

Cuando una clase A extiende una clase B:
- A hereda implementación de B
- A es **subtipo** de B, denotado $A<:B$
Luego, la superclsae puede concentrar estado y comportamientos comunes que sus subclases reutilizarán.
\* En lenguajes modernos de OOP, todas las clases derivan de una única clase raíz `Any`. Con herencia simple de clases, la jerarquía es un árbol.
![[Pasted image 20260831170953.png]]

## Clase Abstracta vs Interfaz
Una clase puramente abstracta (sin campos ni la implementación de los metodos) es similar a una interfaz, pero *no son equivlaentes*.

Las interfaces soportan estructuras no jerárquicas y permiten añadir comportamiento opcional mediante *mixins* (o sea comportamiento adicional o opcional) y es fácil adaptar una clase para que implemente una nueva interfaz.

> Usar interfaz para definir un tipo y una clase abstracta para compartir comportamiento

Una ventaja de las clases abstractas es que pueden agrgar métodos concretos nuevos sin romper las subclases existentes y evolucionar una interfaz es más difícil ya que las implementaciones que ya existen se deben actualizar.

##### Ejemplo: Implementar `Comparable` en una jerarquía
El objetivo es hacer comparable una jerarquía `Tree` basando el orden en la suma de sus nodos: un árbol es menor que otro si la suma de los valores en sus nodos es menor. 
Se define un _trait_ base:
```Scala
trait Comparable:
  def compareTo(other: Comparable): Int
```

Luego, la clase abstracta `AbstractTree` define la jerarquía base. En el código implementado, se calculará el peso o suma del árbol recursivamente entre sus nodos internos (`InternalNode`) y sus hojas (`Leaf`), para finalmente implementar `compareTo` delegando la comparación aritmética de estos resultados.

Avanzando en la extensión de clases, la herencia permite extender y refinar clases concretas, no solo abstractas. Tenemos una clase base `Point`:
```Scala
class Point(val x: Int, val y: Int):
  def getPosition: (Int, Int) = (x, y)
  def moveBy(dx: Int, dy: Int): Point = new Point(x + dx, y + dy)
  def display(screen: Screen): Unit = screen.drawPoint(x, y)
```

La subclase `ColorPoint` extiende `Point` y refina su comportamiento añadiendo un color
```Scala
class ColorPoint(x: Int, y: Int, val color: Color) extends Point(x, y)
```
Aquí observamos un aspecto crítico del mecanismo de herencia: el flujo de construcción. Al instanciar `ColorPoint`, se debe proveer argumentos al constructor de su superclase `Point(x, y)`.

### Orden Constructores de Superclases
El orden de ejecución de los constructores es siempre de **superclase a subclase**, o sea "de arriba hacia abajo". Por ejemplo,
```Scala
abstract class AbstractPerson(val name: String,
								val age: Int,
								val email: String):
	println("Creating a person...")
	
class Student(name: String,
					age: Int,
					val studentId: String) extends AbstractPerson(name, age, s"$studentId@university.edu"):
	println("Creating a Student...")

class PhDStudent(name: String,
				age: Int,
				studentId: String,
				val researchArea: String)
	extends Student(name, age, studentId):
	println("Creating a PhD Student...")
```
haciendo `new PhDStudent("Grace", 25, "ghop", "Entomology")`:
Primero, se invoca el constructor de `PhDStudent`. Sin embargo, antes de ejecutar su propio cuerpo de inicialización, este identifica que depende del constructor de su superclase `Student` y delega la ejecución pasándole los parámetros correspondientes. A su vez, el constructor de `Student` no puede ejecutarse inmediatamente, pues depende del constructor de su superclase `AbstractPerson`, delegándole el control. Dado que `AbstractPerson` es la raíz de esta jerarquía, ejecuta su bloque de inicialización primario (por ejemplo, ejecutando `println("Creating a person...")`). Una vez que `AbstractPerson` finaliza, el control regresa a `Student`, el cual ejecuta su propio cuerpo (`println("Creating a Student...")`). Finalmente, el control regresa a `PhDStudent`, el cual concluye el proceso instanciando sus variables específicas y ejecutando su cuerpo (`println("Creating a PhD Student...")`).
![[Pasted image 20260831174458.png]]

Este comportamiento se mantiene idéntico si se invocan constructores auxiliares mediante `def this(...)`. El flujo siempre resuelve **hasta el constructor primario de la clase más alta** en la jerarquía antes de ejecutar el código concreto hacia abajo.

Finalmente, se debe notar que **los constructores no se heredan**. Si una superclase define los constructores `Point()` y `Point(int x, int y)`, la subclase `ColorPoint` no hereda el constructor `new ColorPoint(1,2)` si no lo define explícitamente. Si la superclase carece de un constructor por defecto (no tiene parámetros), la subclase está obligada a invocar el constructor parametrizado explícitamente en su declaración de herencia.

Por ejemplo,
![[Pasted image 20260831174747.png]]
- `new Point()` y `new Point(1, 2)` está bien pues ambos constructores están definidos.
- `new ColorPoint()` también pues está el constructor por defecto.
- `new ColorPoint(1, 2)` no compila pues el constructor no se hereda.
Luego, para
![[Pasted image 20260831175007.png]]
- `new Point()` y `new Point(1, 2)` está bien pues ambos constructores están definidos.
- `new ColorPoint()` no compila pues no hay constructor por defecto
- `new ColorPoint(1, 2)` ahora si compila.
Finalmente, se debe explicitar el constructor por defecto:
![[Pasted image 20260831175138.png]]



[[Sobrescritura, Sobrecarga y Búsqueda de Métodos]]

[[Encapsulamiento]]