# Sobrescritura, Sobrecarga y Búsqueda de Métodos
Primero se debe establecer un concepto fundamental en lenguajes de tipado estático: la **firma** de un método.

## Firma de Método
La firma de un método (*method signature*) es la convención que permite al compilador unívocamente una operación dentro de una clase. La firma esta compuesta por tres elementos:
1. **Nombre** del método.
2. **Número** de parámetros (aridad).
3. **Tipos** de los parámetros.

por ejemplo, la declaración
```Scala
def greet(name: String, age: Int): Unit
```
su firma formal es simplemente
```Scala
greet(String, Int)
```

Se debe notar que el *tipo de retorno* no es parte de la firma de un método.
> **Regla general**: No pueden coexistir en el mismo ámbito dos métodos con el mismo nombre y la misma secuencia de tipos de parámetros, independiente de lo que retornen.

Un segundo ejemplo:
```Scala
class Turtle(val name: String):
  def useWeapon(): String = s"$name uses a nunchuck"
  def useWeapon(): Int = 420
```
aunque los tipos de retorno de ambas funciones sean distintos (`String`  e `Int`), la firma de ambos métodos es idéntica: `useWeapon()`. Luego al intentar compilar, se tendrá error de doble definición.
También, un segundo caso es omitir los paréntesis en una de las definiciones
```Scala
class Turtle(val name: String):
  def useWeapon(): String = s"$name uses a nunchuck"
  def useWeapon: Int = 420
```
la ausencia se paréntesis no altera la *aridad* del método: Ambos métodos siguen teniendo cero parámetros y el mismo nombre, por lo que sus siguen en conflicto.

## Sobrescritura (overriding)
En la programación orientada a objetos, invocar un método se conceptualiza como **enviar un mensaje a un objeto**.

La sobrescritura corresponde a cuando un método en una subclase reemplaza el comportamiento de un método definido en una superclase. Esto requiere estrictamente que el método de la subclase **debe poseer exactamente la misma firma** que el de la superclase.

Por ejemplo, considerando un *trait* abstracto `Animal` que define un contrato con operacions como `getName`, `greet(Animal)` y `talk(String)`
```Scala
trait Animal:
	def getName: String
	def greet(a: Animal): String
	def talk(s: String): String
```
una clase abstracta `AbstractAnimal` provee una implementación base para `greet` y `talk`
```Scala
abstract class AbstractAnimal(val name: String) extends Animal:
	override def greet(a: Animal): String = s"Hola ${a.getName}, soy $name"
	override def talk(s: String): String = s"$name dice: $s"
```
una clase concreta `Cat` extiende la clase abstracta e implementa `getName`, pero además decide reemplazar el comportamiento de `talk`:
```Scala
class Cat(name: String) extends AbstractAnimal(name):
	override def getName: String = name
	override def talk(s: String): String = s"$name maúlla: $s"
```
El uso explícito de `override` es necesario pues lenguajes modernos requieren explicitar la operación de sobrescritura.
\* Esto pues en caso de una modificación del método de origen, si no se tiene marcada la sobrescritura, el compilador puede tomar el método como uno nuevo y separado.
> Con `override` el compilador verifica que el método efectivamente esté sobrescribiendo una firma existente.


- Una pregunta de verificación pertinente en este punto es: si asignamos una instancia de `Cat` a una variable de tipo estático `Animal`, ¿qué versión del método `talk` se ejecutará en tiempo de ejecución? Como indica la diapositiva 11, aunque el compilador utiliza el tipo estático para asegurar que el mensaje `talk` es válido, en tiempo de ejecución se decide qué método invocar basándose en el tipo dinámico del objeto. Por lo tanto, se ejecutará el comportamiento definido en `Cat` (el maullido), demostrando el despacho dinámico (_dynamic dispatch_).

## Sobrecarga (overloading)
La sobrecarga consiste en definir dos o más métodos dentro de la misma jerarquía que comparten el mismo nombre pero que **poseen diferentes firmas**. Las diferencias pueden estar dadas por métodos de distinta aridad o diferentes tipos de parámetros.
La sobrecarga presenta una complejidad inherente, pues, por ejemplo: 
Suponiendo la clase `Animal` con un método `greet(a: Animal)` y la subclase `Cat` que define un método adicional `greet(a: Cat)`. Luego, en `Cat` se tienen **dos firmas distintias** para `greet` el hereado por `Animal ` y el definido propio.
```Scala
val cat1: Animal = new Cat("Sakamoto")
val cat2: Cat = new Cat("Jiji")
cat1.greet(cat2)
```


> La sobrecarga resuelve estáticamente: A diferencia de la sobrescritura, que resuelve en tiempo de ejecución mirando el tipo real del objeto, el compilador determina qué método sobrecargado llamar basándose solamente **en los tipos estáticos** de las variables en tiempo de compilación.

En el ejemplo anterior, como la variable `cat1` está declarada con el tipo estático `Animal`, el compilador solo tiene visibilidad sobre el método `greet(Animal)` definido en esa clase. El tipo dinámico (`new Cat(...)`) es irrelevante para resolver la sobrecarga.

Un error común es hacer
```Scala
class Cat(name: String) extends Animal(name):
  override def equals(obj: Animal): Boolean = ...
```
- Esto es incorrecto metodológicamente. El método original en la raíz de la jerarquía de Scala (la clase `Any`) tiene la firma `equals(Any)`. Al escribir `equals(Animal)`, el programador no está sobreescribiendo, sino **sobrecargando** el método, dejando expuesta la implementación original para comparaciones con referencias de tipo genérico, lo que rompe la simetría de la igualdad. La forma general correcta es siempre coincidir con la firma base: `override def equals(obj: Any)`.

Como regla general: La sobrecarga es segura cuando los métodos tienen **diferente aridad** o cuando los tipos de los parámetros **no tienen relación de herencia entre sí**.
\* Cuando hay subtipado, hay mucha probabilidad de tener errores.

## Búsqueda de Métodos (Method Lookup)
Cuando se envía un mensaje a un objeto en ejecución, el entorno de ejecución sigue un algoritmo para **encontrar la implementación** correspondiente:
1. Se busca una coincidencia de firma en la clase real (dinámica) del objeto receptor.
2. Si no se encuentra, la búsqueda pasa a la superclase directa del objeto.
3. El proceso se repite hacia arriba en la jerarquía hasta llegar a la clase raíz `Any` (en Scala).

\* En lenguajes de tipado estático, si el compilador determinó previamente que el mensaje era válido, el método está garantizado de encontrarse. Si el lenguaje es de tipado dinámico, la falta del método resultará en un error en tiempo de ejecución.

El algoritmo se ve directamente afectado por el uso de las instrucciones `this` y `super`.
Ambas `this` y `super` se refieren siempre al **mismo objeto** físico, o sea el objeto receptor del mensaje. La diferencia es en la etapa del algoritmo de la búsqueda de método que activan:
1. Enviar un mensaje a `this` inicia la búsqueda de métodos desde la **clase inferior**, o sea el tipo dinámico real del objeto receptor.
2. Enviar mensaje a `super` hace que el algoritmo de búsqueda ignore la clase actual e inicie **desde la superclase** de la clase cuyo código se está haciendo la llamada.

Como ilustración: Considerar una clase `Animal` con un método `isSameAnimal` que llama a `compare(this, a)`. Si una clase `Persian` (que hereda de `Cat`, que a su vez hereda de `Animal`) llama a `compareToSelf`, la pseudo-variable `this` dentro de la implementación de `Animal` no se referirá a una instancia genérica de `Animal`, sino al objeto original `Persian` que inició la cadena de llamadas. Cualquier método llamado sobre `this` reiniciará la búsqueda desde `Persian`, permitiendo que el despacho dinámico y la sobreescritura funcionen correctamente independientemente del nivel de la jerarquía en el que se encuentre el código.
