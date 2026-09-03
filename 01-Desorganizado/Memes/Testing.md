# Testing

Se van a analizar las metodologías formales y empíricas de verificación de software, con énfasos en el diseño sistemático de pruebas unitarias.

Existen múltiples formas de verificar software. El análisis estático y los métodos formales permiten evaluar propiedades sin observar la ejecución, mientras que el testing requiere la ejecución de casos concretos para comparar el comportamiento observado.
*"El testing de programas puede usarse para demostrar la presencia de errores, pero nunca para demostrar su ausencia."* (Dijkstra, 1970)

El enfoque tradicional es realizar pruebas manuales, o *ad-hoc*, no estructurado. Este presenta limitaciones como que cada modificación en el código fuente exige repetir las pruebas, llegando a ser costosas, inconsistentes y difícles de reproducir.

## Test-Driven Development TDD
El enfoque Test-Driven Development es una forma de desarrollo de software en la cual **las pruebas se escriben antes del código de producción**, en vez de "implementar y luego probar".
El proceso opera bajo tres fases:
1. **Red**: Esta fase define la *especificación*, en donde se escribe una prueba **falla por la ausencia del comportamiento**.
2. **Green**: Esta exige una implementación mínima del código para satisfacer la aserción.
3. **Refactor**: Finalmente, esta autoriza la modificación de la estructura interna del código, garantizando que el comportamiento observable, protegido por las pruebas previas, se mantenga inalterado.

---

TDD también ayuda a corregir errores de la forma:
1. Escribir una prueba para reproducir el bug.
2. Corregir el código hasta que la prueba pase.
3. El test queda como protección para evitar futuras regresiones al error.
### Fases
El proceso opera bajo tres fases estrictas: Red, Green y Refactor.
#### Red
> Empezar con un test que falle.

Escribir primero una prueba que exprese el **comportamiento esperado** y ejecutarlo antes de implementar y este debiese fallar porque el comportamiento no está presente.
Se debe comprobar que la prueba falle **por la razón esperada**, si ya pasa, se debe revisar qué está comprobando realmente la prueba.
Así, la fase RED no significa cualquier fallo.

> RED: Con la prueba, primero se define **qué debe hacer el sistema**.

#### Green
> Hacer que el test pase.

En esta fase se debe implementar lo mínimo necesario para satisfacer la prueba diseñada en Red.
Se debe avanzar de a pasos pequeños, volviendo a ejecutar las pruebas después de cada modificación.
- No anticipar un requisito; Agregar comportamiento cuando exista una necesidad concreta.

#### Refactor
> Mejorar el diseño con confianza.

Finalmente, se reestrucura de a poco, mejorando la estructura, los nombres y responsabilidades del código.
Se debe **mantener el comportamiento observable**, ejecutando el conjunto de pruebas después de cada cambio.
- Si algo falla, corregir o revertir el último cambio antes de continuar.

> Refactorizar cambia **cómo** está escrito el código, **no qué hace**.

## Diseñar Casos de Pruebas

Para seleccionar las **entradas** de las pruebas, es inviable evaluar la totalidad de los parámetros de entrada, por ello se debe adoptar la metodología de *particionar los dominios*.

Por ejemplo, implementando una función `abs()` que entrega el valor absoluto de números enteros:
```Scala
trait IntOps:
	def abs(n: Int):
```
la función tiene entrada de tipo `Int` y salida `Int`, pero el comportamiento *depende del valor de entrada*.
Probar todas las entradas es inviable entonces **se particiona** el dominio de entrada en *subdominios* tales que la función tiene comportamiento similar:
Se dividen los números enteros en positivos $n>0$, negativos $n<0$ y el caso especial (o borde) cero $n=0$.
Finalmente, se eligen unos pocos casos de prueba para cada subdominio tal que **se prioricen los casos borde** que, para este caso, sería `-1`, `0`, `1`
> Las discrepancias lógicas suelen concentrarse en las fronteras de los subdominios.

## Testing Frameworks
Se va a emplear la arquitectura de testo *xUnit*, estándar de industria orginado de Smalltalk y adoptado transversalmente por frameworks modernos.
A diferencia de una biblioteca estándar, dónde el código del programador determina el flujo de control, xUnit opera como un framework que *invierte el control*: **El entorno determina cuándo, cómo y en qué orden ejecuta los módulos** (él determina cuándo llama al código del programador). 
Los componentes centrales de xUnit son:
1. El caso de prueba (Test case): La unidad mínima de prueba.
2. El oráculo de prueba, Test Oracle (aserciones): Mecanismo como criterio para decidir si el comportamiento observado es correcto. Una forma común de expresar oráculos es con **aserciones**
3. La suite de pruebas (Test suite): Se agrupan casos de pruebas relacionados entre sí.
4. El fixture de prueba (Test fixture): Pereparación de un entoorno consistente para cada test.
5. Ejecutor de tests (Test runner): Ejecuta los test y muestra los resultados.

### JUnit, MUnit
Hay muchos frameworks derivados de XUnit. En Scala la biblioteca de testing es *MUnit* que, a su vez, es runner del framework ligero *JUnit*.

Se revisa un ejemplo de configuraciones de tests para una calculadora:
1. Un código de ejemplo en JUnit 5.x:
```Scala
// Importar las funcionalidades del framework
import org.junit.jupiter.api.Assertions.assertEquals
import org.junit.jupiter.api.{BeforeEach, DisplayName, Test}

class CalculatorTest:
	var calculator: Calculator = null

	/*
		Con @BeaforeEach se marca el metodo como
		fixture q se ejecuta antes de cada test.
		Si hay 2 metodos de test, se ejecuta 2 veces.
		Metodo suele llamarse setUp()
	*/
	@BeforeEach
	def setUp(): Unit =
		calculator = new Calculator("Test Calculator")

	/*
		con @test se marca metodo como un test, se define
		la logica de prueba
	*/
	@Test
	@DisplayName("Test addition of two positive integers")
	def testAddPositiveIntegers(): Unit =
		val result = calculator.add(2, 3)
		assertEquals(5, result)
```

2. Código de ejemplo en MUnit
En lugar de importar funcioalidades, el test **extiende** `munit.FunSuite`
```Scala
class CalculatorTest extends munit.FunSuite:
	var calculator: Calculator = null

	/*
		En vez de usar anotaciones, se sobrescriben
		metodos del framework con 'override'
	*/
	override def beforeEach(context: BeforeEach): Unit =
		calculator = new Calculator("Test Calculator")

	/*
		Nombre del test descriptivo
	*/
	test("Test addition of two positive integers"):
		val result = calculator.add(2, 3)
		assertEquals(5, result)
```

Si varios test comparten un mismo objeto mutable, un test puede dejarlo en un estado distinto para el siguiente, produciendo *contaminación* entre las pruebas, dependiendo del orden de ejecución determinado por el framework.
```Scala
class CounterTest extends munit.FunSuite:
	val counter = new Counter()
	test("incrementa una vez"):
		counter.increment()
		assertEquals(counter.current, 1)
		/* 
			el counter se incrementa, y el siguiete assert
			 lo recibe modificado
		*/
		test("parte en cero"):
		assertEquals(counter.current, 0)
```
para que cada prueba sea independiente, se reinicializa el estado antes de cada test con `beaforeEach()`
```Scala
class CounterTest extends munit.FunSuite:
	var counter: Counter = null
	
	override def beforeEach(context: BeforeEach): Unit =
			//esto se ejecuta antes de cada test individual
			counter = new Counter()
		
	test("incrementa una vez"):
		counter.increment()
		assertEquals(counter.current, 1)
	test("parte en cero"):
		assertEquals(counter.current, 0)
```

## Ejemplo de diseño: Aritmética de Divisas
Definiendo un caso de prueba que implementa la inferfaz que se busca que la clase `Money`:
```Scala
class MoneyTest extends munit.FunSuite:
	var _12clp: Money = null
	var _14clp: Money = null

override def beforeEach(context: BeforeEach): Unit =
	_12clp = new Money(12, "CLP")
	_14clp = new Money(14, "CLP")
	//...
```
y se definen métodos para realizar pruebas básicas, testeando comportamientos que se esperan:
```Scala
class MoneyTest extends munit.FunSuite:
	//..
	test("Igualdad de dos objetos Money con el mismo monto y divisa"):
		assertEquals(_12clp, _12clp)
		assertEquales(_12clp, new Money/12, "CLP"))
		assertNotEquals(_12clp, _14clp)
		
	test("Money puede sumarse con otro objeto de la misma divisa"):
		val expected = new Money(26, "CLP")
		val result = _12clp.add(_14clp)
		assertEquals(expected, result)
```

### Igualdad de Objetos
Creando dos objetos separados que, a priori, son iguales pues tienen la misma cantidad y divisa, por ejemplo dos montos de 12 CLP y se le pide a MUnit que los compare utilizando `assertEquals()`, se tendrá un error. Se indicará que no son iguales, mostrando algo como `Money@1622f1b` y `Money@a22f9e2`.
Esto sucede pues se están comparando las **direcciones de memoria** de los objetos y no sus valores internos.
Para solucionar este comportamiento, se implementa en la clase dos cosas:
1. Por defecto, la representación en texto de un objeto tiene el formato `<Clase>@<Direccion>`. Luego, se implementa el método `toString` para que muestre una descripción clara del objeto.
```Scala
class Money(val amount: Int, val currency: String):
	// ...
	override def toString: String =
	s"Money($amount, $currency)
```
pero se seguirán comparando las direcciones de memoria.
2. Se define un método de igualdad personalizado
```Scala
override def equals(obj: Any): Boolean =
    if obj.isInstanceOf[Money] then
      val other = obj.asInstanceOf[Money]
      amount == other.amount && currency == other.currency
    else false
```

### Valor OPTION
En lenguajes antiguos, cuando un valor no existía o no se encontraba, se utilizaba un valor nulo `NULL`. Utilizar este valor induce un comportamiento propenso a errores, lo que puede causar fallas de seguridad y de sistemas.
Para evitar utilizar `NULL` en Scala, se utiliza el tipo `Option`. Un `Option` es una estructura que envuelve un valor indicando explícitamente si este se encuentra presente con `Some` o si está ausente con `None`.
Si un valor *puede faltar*, lo mejor es modelarlo como tipo `Option`. Así, el compilador obliga a tratar el caso de la ausencia de forma explícita.
![[Pasted image 20260830134433.png]]
Con `Option` se devuelve:
- `Some(valor)` si hay un valor.
- `None` si no hay.
```Scala
var o1: Option[Money] = None
var o2: Option[Money] = Some(_12clp)
```
