# Arbol-23
Nodo2: binario -> una llave $x$, 2 hijos:

izq < x < der
  

Nodo3: ternario -> dos llaves, x<y:

izq < x < mid < y < der

NodoE: vacío

## Implementaciones

### Insert
Similar a ABB, se realiza búsqueda infructuosa.
Está: no hacer nada 
No está: La inserción se realiza en el último nodo visitado antes de llegar a un nodo externo (para no aumentar la altura del árbol).

#### Nodo Binario
Llave en nodo binario `Nodo2` , se llama función `insert(self,x):` dentro de su clase, de campos `(izq, info, der)`

Por la implementación, se pueden recibir dos formas de resultados: tupla o una llave, se revisa con ` if (isinstance(x, tuple))`
1. Si se recibe tupla es porque se dividió el nodo hijo. Nodo binario no hace split pues puede aceptar una llave más entonces simplemente se agrega llave: se retorna nodo ternario:
   ```py
   return Nodo3(
   ```
   
   
2. `else:` se recibe llave que viene 'desde arriba', se inserta recursivamente para que pase hasta nodo externo:
   ```py
   if (x < self.info):
	   self.izq.insert(x)
	...
   ```
   

* Si se inserta una llave en un nodo ternario hay que insertarla recursivamente en el hijo izquierdo, en el del medio o en el derecho, según corresponda. Si esto no produce un *split* del hijo, el resultado es un puntero al nodo resultante (que puede ser binario o ternario), lo cual se anota en el lugar respectivo y se retorna un puntero al nodo resultante. Pero si el hijo se divide, se recibe el resultado que es una tupla que contiene el árbol izquierdo, el árbol derecho, y la llave que los separa. Con esto este nodo tiene la información para a su vez dividirse y retornar la tupla resultante.

#### Ternario
dos llaves $(x,y):x<y$:
y es de la forma:
```py
self.izq < x < self.mid < y < self.der
```

se pueden tener como máximo dos llaves: si hay 3 y queda de la forma $(x,y,z)$ (*overflow*) se divide: **el de al medio sube a ser binario** con los `x,z` como hijos.

1. buscar llave: `if (self.info1 == x or self.info2 == x)`
	-  Si llave está: salir y retornar 'ya esta' `return None`
	-  llave no está `else:` (búsqueda infructuosa), se tienen casos: 
		1. si hijos son externos,
		    `if (isinstance(self.izq, Nodoe) & isinstance(self.der, Nodoe)):`
		    insertar en este mismo nodo (pasa a ser ternario) según key mayor o menor
		    
		2. Si nodos hijos no son externos,  insertar recursivamente según desigualdad llave,
			- x es menor: rec a izq, `self.izq.insert(x)`
			- x es mayor: rec a der, `self.der.insert(x)`


> Si se inserta una llave en un nodo ternario hay que insertarla recursivamente en el hijo izquierdo, en el del medio o en el derecho, según corresponda. Si esto no produce un *split* del hijo, el resultado es un puntero al nodo resultante (que puede ser binario o ternario), lo cual se anota en el lugar respectivo y se retorna un puntero al nodo resultante. Pero si el hijo se divide, se recibe el resultado que es una tupla que contiene el árbol izquierdo, el árbol derecho, y la llave que los separa. Con esto este nodo tiene la información para a su vez dividirse y retornar la tupla resultante.

#### Hoja
Recibe una llave y se divide en dos hojas con la llave como su padre. Esto se retorna como una tupla:
```py
return (Nodoe, x, Nodoe)
```
esto siempre se cumple, pues comienza a subir la llave que se inserta. Y si la llave ya existía, tal caso está manejado en `insert()` en cada clase de nodo binario o ternario.