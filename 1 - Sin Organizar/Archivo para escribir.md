# Arbol-23

## Implementaciones

### Insert
Similar a ABB, se realiza búsqueda infructuosa.
Está: no hacer nada 
No está: La inserción se realiza en el último nodo visitado antes de llegar a un nodo externo (para no aumentar la altura del árbol).

#### Nodo Binario
Llave en nodo binario `Nodo2` , se llama función `insert(self,x):` dentro de su clase, de campos `(izq, info, der)`

Por la implementación, se debe manejar la inserción de una llave `x` además de que el nodo hijo puede (o no) hacer split.
1. Si no hay split, resultado es puntero al nodo resultante: `return self`
2. si hay split, se recibe tupla (`tuple`) de la forma `(arbolDer, llave, arbolIzq)`
para manejar esto, se almacena el resultado en una variable `rec`

* si llave está `x == self.info`: retornar None
* Si no, casos recursivos
	* llave es menor: `rec =` recursivo hacia la izq
	* llave es mayor: `rec =`recursivo hacia la der

luego, se analiza el resultado de la recursión:
* el resultado fue `None`,  solamente se actualiza el 

1. si fue tupla, se retornan nodos según de donde viene el split
	* viene de hijo der -> se modifica der y se mantiene izq
	* viceversa para izq
2. si no fue tupla, se actualiza puntero según orden de x y llave


#### Ternario
dos llaves $(x,y):x<y$:
y es de la forma:
```py
self.izq < x < self.mid < y < self.der
```
Se pueden tener como máximo dos llaves: si hay 3 y queda de la forma $(x,y,z)$ (*overflow*) se divide: **el de al medio sube a ser binario** con los `x,z` como hijos.

Luego, para ternario se tiene un plantemiento similar que para binario, solo que se requieren revisar más casos para la llave que se inserta y la tupla que ese recibe (pues se pueden dividir cualquiera de los 3 hijos).

#### Hoja
Es el caso base. Recibe una llave y se divide en dos hojas con la recibida como su padre. Esto se retorna como una tupla (pues hubo split):
```py
return (Nodoe, x, Nodoe)
```
esto siempre se cumple, pues comienza a subir la llave que se inserta. Y si la llave ya existía, tal caso está manejado en `insert()` en cada clase de nodo binario o ternario.

### Search
Es similar a un ABB, con sus llaves interiores ordenadas.

#### Binario
Se tienen dos hijos y una llave:
* Si buscada es la almacenada: `return self` (se retorna el puntero para todos los casos)
* Si no es la almacenada, se llama recursivamente según llave buscada es menor o mayor:
	* `if (buscada < almacenada):` retornar la búsqueda recursiva en subárbol izq
	* `if (buscada > almacenada):` retornar la búsqueda recursiva en subárbol der

##### Ternario
Se tienen tres hijos y dos llaves. Es similar al nodo binario, solamente se revisan mas casos:
* Si buscada está almacenada (`buscada == info1 or info2`) retornar el puntero.
* Si buscada no está en llave:
	* es menor que valor a la izq: buscar recursivamente en subárbol izq
	* esta entre valor izq y derecho: buscar rec en subárbol medio.
		  También es posible solamente indicar que sea menor a valor derecho, pues ya se comprobó el caso que sea menor que el izq y solo queda entermedio (descartando que sea mayor que el derecho).
	* es mayor que der: buscar recursivamente a la derecha.

