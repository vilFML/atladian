# Arbol-23

  

Nodo2: binario -> una llave $x$, 2 hijos:

izq < x < der

  

Nodo3: ternario -> dos llaves, x<y:

izq < x < mid < y < der

NodoE: vacío
  

## Implementaciones

### Insert

* Si se inserta una llave en un nodo binario, hay que insertarla recursivamente en el hijo izquierdo o en el derecho, según corresponda.

  
#### Nodo Binario
Llave en nodo binario `Nodo2` , se llama función `insert(self,x):` dentro de su clase, de campos `(izq, info, der)`

1. Primer paso, buscar llave: `if (self.info == x)`
	1. Si llave está: salir y retornar 'ya esta' `return None`
	2. llave no está (búsqueda infructosa): llamar recursivamente
		1. x es menor: rec a izq, `self.izq.insert(x)`
		2. x es mayor: rec a der, `self.der.insert(x)`




Si esto no produce un *split* del hijo, el resultado es un puntero al nodo resultante (que puede ser binario o ternario), lo cual se anota en el lugar respectivo y se retorna un puntero al nodo resultante. Pero si el hijo se divide, se recibe el resultado que es una tupla que contiene el árbol izquierdo, el árbol derecho, y la llave que los separa. Con esto este nodo tiene la información para mutar a ternario y retornar el resultado.