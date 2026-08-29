Clase abstracta


```Scala
abstract class GameUnit {
	def findTarget(): Unit = {
		val t = findTarget)(
```


TRAIT: Define comportamiento de una clase:
> todas las clases que hereden este trait tendrán este comportamiento, deben implementar las funciones y variables que el trait determine. ES LA FIRMA.

Cuando se define el comportamiento o forma de una clase, se debe usar trait.

Clase ABSTRACTA: puede ser una mezcla
Es una capa de abstracción para el programador. No son implementadas
Sirven para reciclar código, no se usan como tipos (para eso esta `trait`).
puede definir comportamientos pero no es una interface
- no se puede usar como tipo
- no se puede instanciar con new
