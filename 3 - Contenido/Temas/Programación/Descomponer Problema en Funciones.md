Una solución que no descompone el problema en varias funciones tiende a no ser escalable y tener una mala depuración 

1. Siempre diseñar funciones auxiliares para cad sub-problema que se pueda identificar.
2. Dar nombres descriptivos a las funciones y variables

### Ejemplo
En la famosa tienda “Danquin Donuts”, se encuentran actualmente en un proceso de automatización de sus ventas. Usted se ofrece a ayudar a la tienda debido a que tiene mayor conocimiento en programación, ante lo cual la tienda le entrega la siguiente información de las donuts:


| Tipo de Donut | Impuesto | Costo Individual de Donut |
| ------------- | -------- | ------------------------- |
| Chocolate     | 10%      | 1900                      |
| Crema         | 15%      | 1000                      |
| Frambuesa     | 20%      | 1200                      |
El impuesto es un porcentaje adicional que debe pagar el cliente, el cual es fijo y
distinto para cada tipo de Donut.
- Por ejemplo, si un usuario compra 7 donuts de crema, entonces el usuario debería pagar: costoTotal = 1.15 ∗ 1000 ∗ 7
Se le pide entonces crear una función que dada la cantidad de donuts de chocolate, crema y frambuesa, entregue el costo total del pedido.

#### Solucion 1
Una posible solución al problema es crear una función que reciba el número de donuts de cada tipo, y realizar el cálculo completo.

```py
# costoTotal: int, int, int -> num
# calcula el costo total de una cantidad dada de donuts de chocolate, crema
# y frambuesa.
# ej: costoTotal(1,1,1) entrega 4680
def costoTotal(nChoco, nCrema, nFrambu):
	costoChoco = 1.10 * 1900 * nChoco
	costoCrema = 1.15 * 1000 * nCrema
	costoFrambu = 1.20 * 1200 * nFrambu
	
	return costoChoco + costoCrema + costoFrambu

# tests

assert costoTotal(1, 1, 1) == 4680
```

sucede que la función realiza muchas labores: El cálculo del costo de cada sabor de donut. Así que si se agregan más tipos de donuts, la función se hará cada vez más compleja.
Además el cálculo interno de costos no se está testeando.

#### Composición de Funciones
La solución anterior es correcta, sin embargo, carece de escalabilidad y de testeabilidad, por lo que es más susceptible a errores.
Para enfrentar este problema se va a descomponer el subproblemas y se van a crear *funciones auxiliares*.
Cada función se encargará de resolver un solo problema, con su propia receta de diseño asociada.
\* Las funciones pueden invocar dentro de sus instrucciones a otras funciones.

#### Ver dependencias y relaciones
1. De la tabla se puede ver que se tienen *tres* problemas separados: el costo de cada tipo de donut.
2. Los tres problemas se relacionan entre sí al momento de calcular el costo total de un predido.

#### Esquematizar las Funciones
Por cada una de las funciones que se crean, se debe seguir la receta de diseño.

```py
# costoChoco: int -> num
# calcula el costo de una determinada
# cantidad de donuts de chocolate
# ej: costoChoco(1) debe dar 2090
def costoChoco(nChoco):
	# ...

#tests
assert costoChoco(1) == 2090
assert costoChoco(3) == 6270
```
 y así para cada sabor. Además,
 
```py
# costoTotal: int, int, int -> num
# calcula el costo total de una cantidad dada
# de donuts de chocolate, crema y frambuesa
# ej: costoTotal(1,1,1) entrega 4680
def costoTotal(nChoco, nCrema, nFrambu):
	# ...

# tests
assert costoTotal(1, 1, 1) == 4680
```


#### Implementar las Funciones
Se implementa el cuerpo de las funciones:

```py
# costoChoco: int -> num
# calcula el costo de una determinada
# cantidad de donuts de chocolate
# ej: costoChoco(1) debe dar 2090
def costoChoco(nChoco):
	return 1.10 * 1960 * nChoco

#tests
assert costoChoco(1) == 2090
assert costoChoco(3) == 6270
```

#### Resolver el Problema
Finalmente se utilizan las funciones auxiliares definidas.
**Las funciones que calculan el costo de cada dona deben estar definidas antes de la función de costo total, ya que esta utiliza las otras funciones.**

```py
# costoTotal: int, int, int -> num
# calcula el costo total de una cantidad dada de dounts
# de chocolate, crema y frambuesa
# ej: costoTotal(1,1,1) entrega 4680
def costoTotal(nChoco,nCrema,nFrambu):
	return costoChoco(nChoco) + costoCrema(nCrema) + costoFrambu(nFrambu)

#tests
assert costoTotal(1, 1, 1) == 4680
```
