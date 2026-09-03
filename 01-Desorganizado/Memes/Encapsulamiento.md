# Encapsulamiento
El encapsulamiento oculta y restringe el acceso de los estados internos del objeto.
Esto permite exponer solo lo necesario.

![[Pasted image 20260902144323.png]]

La interfaz pública de Class está dada por los miembos con +.
> Si Class implementara un trait, la interfaz del trait sería el contrato abstracto, mientras que la interfaz pública concreta es lo que efectivamente se expone al usar la clase.

Interfaz pública: Qué puedo usar del objeto concreto.
Trait: Qué debe cumplir una clase.

##### Encapsulamiento en Python
en Python no se puede restringir el acceso, pero sí hay convenciones para indicar que algo no debiese ser accedido desde fuera, esto se denota con `_algo`

## En Scala
Se tienen las palabras clave `private` y `protected`. Si no se declara explícitamente, por defecto todo es publico (explicitamente es `public`).

En UML
- públic: +
- protected: #
- private: -

si es public: 

| Modificador                | UML | Clase | Paquete | Subclase | Mundo |
| -------------------------- | --- | ----- | ------- | -------- | ----- |
| Sin modificador (`public`) | +   |       |         |          |       |
| `protected`                | #   |       |         |          |       |
| `private`                  | -   |       |         |          |       |
desde una misma clase siempre se puede acceder a una variable protected o private.

```Scala
class Animal(name: String, var age: Int, private var weight: Double)
```
la variable `weight` es privada y puede ser accedida solamente por esta clase.

Por ejemplo
```Scala
package cl.uchile.dcc

class Foo:
	private val isFoo = true
	
	def doFoo(f: Foo): Unit =
		if f.isFoo then ???
 
```
esta si compila 

```Scala
package cl.uchile.dcc

class Bar extends Foo:
	private val isBar = true

	def doBar(b: Bar): Unit =
		if b. isFoo then ???

```

> Las cosas privadas no se heredan pero `protected` si.

---
No se puede acceder a un valor protegido en una nueva instancia 



---
```Scala
package cl.uchile.dccpackage cl.uchile.dcc.bar

class Foo:
	protected val isFoo = trueclass Bar extends Foo:

	def doFoo(f: Foo): Unit =
		if f.isFoo then ???
```


```Scala
package cl.uchile.dcc.bar

class Bar extends Foo:
	private val isBar = true

	def doBar(b: Bar): Unit =
		if b. isFoo then ???
```
a pesar de que está en un paquete distinto, una subclase sí puede accederlo


## Invariantes
Un invariante es una condición lógica que debe cumplirse siempre para que el objeto sea válido. Por ejemplo en una cuenta bancaria, el saldo nunca puede ser negativo.
Entonces se protege un estado interno evitando modificaciones que no se controlan, solamente la *interfaz pública* controla cómo se altera el estado. Así se garantiza que las invariantes no se rompan.

```Scala
class BankAccount(private var balance: Int):
	def deposit(amount: Int): Unit =
	if amount > 0 then balance += amount
	
	def withdraw(amount: Int): Unit =
		if amount > 0 && amount <= balance then balance -= amount
	def getBalance: Int = balance
```
`balance` no es modificable directamente.


El encapsulamiento reduce el acoplamiento pues restringe el acceso al estado interno de la clase y obliga a depender **solo de la interfaz pública**. Luego, los cambios internos no modifican el código fuente.

```Scala
class Order:
val items = mutable.ListBuffer[String]()

@main def orderMain(): Unit =
	val order = new Order
	order.items += "Pizza"
```
Qué pasa si `items` se quiere cambiar a otro tipo de lista? (enlazada, etc.)
```Scala
class Order:
	private val items = mutable.ListBuffer[String]()
	
	def addItem(item: String): Unit = items += item
	
@main def orderMain(): Unit =
	val order = new Order
	order.addItem("Pizza")
```
el código del cliente pasa a depender solo de `Order`, sin conocer cómo están representados internamente.



## Exposición Mínima

> Una sugerencia es empezar todo como privado e ir liberando cosas a medida que son necesarias.

**Métodos Accesores (Getter y Setter)**
En OOP se llama *accessor* a métodos que leen o actualizan el estado.

- **Getter**: `getX(): T`
- **Setter**: `setX(x: T): Unit`

la idea es mantener encapsulado el estado interno, y poder validar y mantener invariantes en un solo lugar.

```Scala
class User(private var name: String, private var age: Int):
	// getters
	def getName(): String = name
	def getAge(): Int = age
	// setters (con validación)
	def setName(n: String): Unit =
	if n.nonEmpty then name = n
	
	def setAge(a: Int): Unit =
		if a >= 0 then age = a
```

### Diseño de accesores
- Si no se quiere exponer escritura y **ofrecer solo lectura**: solo **getter**
- Para mantener invariantes: setter
- Evitar exponer estructuras mutables directamente. Ejemplo si se quiere devolver una lista y asegurarse de que no se modifique: pasar a inmutable y devolver.

```Scala
class Order:
	private val items = mutable.ListBuffer[String]()
	
	def getItems(): List[String] =
		// Evita filtrar la estructura mutable al exterior
		items.toList
		
	def addItem(i: String): Unit =
		if i.nonEmpty then items += i
```


## Propiedades

En tiempo de compilación, una propiedad se traduce a métodos, luego se  genera un getter por defecto y solamente setter si el campo es mutable.
`val` inmutable entonces se genera solo getter.
`var` es mutable, entonces se generan métodos getter y setter.



```Scala
class User(var age: Int)
// Equivale a:
class User(private var _age: Int):
	def age: Int = _age
	def age_=(value: Int): Unit = _age = value
```

## Principios SOLID
Acrónimo de cinco principios clásicos de diseño orientado a objetos:
•Single Responsibility (Principio de responsabilidad única)
•Open/Closed (Principio de abierto/cerrado)
•Liskov Substitution (Principio de sustitución de Liskov)
•Interface Segregation (Principio de segregación de la interfaz)
•Dependency Inversion (Principio de inversión de la dependencia)

---

```Scala
trait Player:
	var hp: Int


class Controller(val player: Player):
	def hit(): Unit =
		player.hp = Math.max(0, player.hp - 10)
```
Por un lado, la interfaz `Player` permite la lectura *y escritura* de `hp`. Además `Controller` devuelve el player (no está escrito) al acceder al player, se puede acceder y modificar su hp.

Entonces es **segrega**

```Scala
trait PlayerView:
	def hp: Int

trait Player extends PlayerView:
	def hp_=(hp: Int): Unit

class Controller(private val _player: Player):
	def hit(): Unit =
		_player.hp = Math.max(0, _player.hp - 10)
	
	def player: PlayerView = _player
```
así cuando se pregunte por player, se devuelve como tipo `PlayerView`

\* Cuando se hace `_hp` se está creando un método getter.


### Principio de Sustitución de Liskov LSP

Sea 𝑞(𝑥) una propiedad demostrable sobre objetos 𝑥 de
tipo 𝑇.
Entonces 𝑞(𝑦) debe cumplirse para objetos 𝑦 de tipo 𝑆,
donde 𝑆 es subtipo de 𝑇.


*Cláse Frágil*: Si un subtipo no es aceptado en una función `foo()` se dice que B es frágil en presencia de `foo`.



2. La visibilidad no puede hacerse más restrictiva en un subtipo:
   Sí se puede aumentar la visibilidad para los subtipos

```Scala
class A:
private def foo(): Unit =
println("A")
class B extends A:
protected def foo(): Unit =
println("B")
class C extends B:
override def foo(): Unit =
println("C")
```
\* se hace override en la 3a pues B no vé la definición de foo, pero C si (pues protected se hereda) entonces se haec override.

```Scala
class A:
	def foo(): Unit =
		println("A")

class B extends A:
	override protected def foo(): Unit =
		println("B")

class C extends B:
	override private def foo(): Unit =
		println("C")
```
el problema es que C técnicamente no tiene `foo` pues no es visible.