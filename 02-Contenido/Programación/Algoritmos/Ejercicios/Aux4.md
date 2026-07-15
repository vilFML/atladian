# P1
Se van a desarmar las listas previas y cambiar los punteros para ir creando la lista final, de la forma:
![[aux4-p1a.drawio.png]]
luego, en la primera iteración:
![[aux4-p1-1aIteracion.drawio.png]]
y en la tercera iteración
![[aux4-p1a-iteracion2.drawio.png]]

```py
def unir_listas(lista1, lista2):
  if not lista1: return lista2
  if not lista2: return lista1

  # LNodo para empezar
  nodo_inicial = LNodo()
  ptr = nodo_inicial
  ptr1 = lista1
  ptr2 = lista2
  while ptr1 and ptr2:
    # si el LNodo de lista 1 es menor al LNodo en lista 2
    if ptr1.val < ptr2.val:
      # el siguiente es el LNodo de lista 1
      ptr.sig = ptr1
      # avanzo en la lista 1
      ptr1 = ptr1.sig
    else:
      ptr.sig = ptr2
      ptr2 = ptr2.sig
    # avanzo al siguiente en la lista unida
    ptr = ptr.sig

  # si todavia quedan LNodos de la lista 1
  if ptr1:
    # uno los que quedan
    ptr.sig = ptr1
  elif ptr2:
    ptr.sig = ptr2

  # el primer LNodo era solo para conectar
  return nodo_inicial.sig
```

# P2
Un árbol binario es una estructura de datos que ordena los datos de forma que cada vez que se avanza, se reduce la cantidad de datos a analizar: Si se busca un número, no hay que revisar todos los casos.
Para un nodo se tiene: Valor, referencia izquierda y referencia derecha.

En una lista se revisa secuencialmente. En un árbol hay tres formas: Pre, In y Post Orden.
1. PreOrden: Revisar valor -> revisar nodo izq -> revisar nodo der.
   Ejemplo:
	   ```py
			2
		  /   \
		4       7
	  /    \	
	3       10
		```
- En ejemplo, raiz:2 -> nodo izq: 4 -> nodo izq: 3 -> no quedan más entonces se devuelve -> derecha de 4: 10 , no quedan mas entonecs se se vuelve a raíz y se revisa subarbol derecho -> 7
1. In: Sin contar el mismo nodo: revisar a la izquierda tanto como se pueda.
   - En ejemplo: 3 -> 4 -> 10 -> 2 -> 7   
   - Implementación:
	  ```py
	  def f1():
		f1(self.izq)
		...
		f1(self.der)
	  ```
  
     
1. Post: Lo más que se pueda a la izquierda, lo más que se pueda a la derecha y finalmente el mismo nodo.
   - Max izq: 3; no hay izq ni der -> subir, hay derecho -> derecho = 10; no hay izq ni der -> subir, se revisó izq y derecho -> nodo = 4 y subir en nodo arriba. Ya se revisó izq, pero hay derecho -> derecho = 7, no hay más -> subir -> nodo = 2

> pre order revista (o entrega) raíz al principio y postorder al final.

##### a)
implementar obtener número de nodos:
```py
def f():
	if (nodo is None):
		return 0
	else:
		return 1 + f(nodo.izq) + f(nodo.der)
```
##### b)
idea: tomar raíz y comparar con nodos hacia abajo.
```py
def obtenerMax(nodo):
	if (nodo is None):
		return -np.inf
	else:
		max_hijos = max(obtenerMax(nodo.izq), obtenerMax(nodo.der))
		return max(max_hijos, nodo.val)
```

##### c)
tener suma de los valores de nodos es similar a contar nodos pero se cambia el contar por sumar el valor del nodo.
```py
def obtenerSuma(nodo):
  #caso base
  if nodo is None:
    return 0
  else:
    return nodo.val + obtenerSuma(nodo.izq) + obtenerSuma(nodo.der)
```
##### d)
La altura del nodo es la distancia entre el nodo mas arriba y el de más abajo (Un árbol de 1 solo nodo tiene altura 1).
La idea es comparar la altura de los sub-árboles de la raíz.
Para tener altura:
```py
return 1 + max(obtenerAlt(nodo.izq), obtenerAlt(nodo.der))
```
y de caso base se tiene un nodo vacío, que devuelve altura 0:
```py
if nodo is None:
	return 0
```
juntando:
```py
def obtenerAltura(nodo):
  #caso base
  if nodo is None:
    return 0 #Puede ser 1 dependiendo de la definición de altura
  else:
    return 1+max(obtenerAltura(nodo.izq), obtenerAltura(nodo.der))

```

# P3
Dado un árbol binario encuentre el ACB de dos nodos de un árbol.
Según Wikipedia, el ACB se define como: 'El ancestro común más bajo entre dos nodos v y w se define como el nodo más bajo en el árbol que tiene a v y w como descendientes (donde se permite a un nodo ser descendiente de él mismo).'
___

la idea es usar post-order pues se revisan los nodos de abajo y si no se encuentra ancestro común, entonces ahí se revisa el de más arriba. La función recursiva hace llamado recursivo a la izquierda y derecha. Se va a llevar un valor booleano que determina si es el nodo que se está buscando.

```py
# version explicita (más entendible)
def acb_exp(raiz: ANodo, nodo_p: ANodo, nodo_q: ANodo):
    # Bajamos el árbol al final y subimos propagando hacia arriba 3 datos:
    # 1. Si se encontro el nodo_p
    # 2. Si se encontro el nodo_q
    # 3. El primer nodo donde los dos fueron encontrados que es el ACB, None si no se tiene
    def acb_recursivo(raiz: ANodo, nodo_p: ANodo, nodo_q: ANodo):
        # caso base
        if not raiz:
            return False, False, None

        # bajamos en el arbol, obteniendo información en la subida
        nodo_p_en_izq, nodo_q_en_izq, acb_izq = acb_recursivo(raiz.izq, nodo_p, nodo_q)
        nodo_p_en_der, nodo_q_en_der, acb_der = acb_recursivo(raiz.der, nodo_p, nodo_q)

        nodo_p_encontrado = nodo_p_en_izq or nodo_p_en_der or raiz == nodo_p
        nodo_q_encontrado = nodo_q_en_izq or nodo_q_en_der or raiz == nodo_q

        # el ACB que se propago hacia arriba
        acb = acb_izq if acb_izq else acb_der
        # si recien en este nivel se encontraron ambos
        if not acb and nodo_p_encontrado and nodo_q_encontrado:
            acb = raiz

        return nodo_p_encontrado, nodo_q_encontrado, acb

    # retornamos solo el ACB
    return acb_recursivo(raiz, nodo_p, nodo_q)[2]

```

```py
# version directa, con tracking indirecto de p y q
# Usar una sola variable para prograpagar información hacia arriba
# Si no se tiene el ACB, no se ha encontrado ni p ni q entonces propagamos None
# Si encontramos el ACB propagamos el ACB
# Si encontramos p o q propagamos este mismo
def acb_sim(raiz: ANodo, nodo_p: ANodo, nodo_q: ANodo):
    if not raiz or raiz == nodo_p or raiz == nodo_q:
        return raiz

    # post orden
    izq = acb_sim(raiz.izq, nodo_p, nodo_q)
    der = acb_sim(raiz.der, nodo_p, nodo_q)

    # si ambos lados devuelven algo, significa que p y q están en subárboles
    # distintos por lo tanto, este nodo es el ACB

    # Notese que si p o q es el MCA, al subir el ultimo en encontrarse se propaga
    # sin cambios como MCA
    if izq and der:
        return raiz

    # si solo recibimos uno puede ser que se encontro p, q o el MCA
    # por ende lo retornamos para propagar la información
    return izq if izq else der
```

# P4
Supongamos que cada nodo de un árbol binario representa un ingrediente de un anticucho.
Queremos «ensartar» los ingredientes en un palito de forma ordenada, formando una lista
doblemente enlazada.
Para ello, se deben reutilizar los punteros izq y der como prev y next. El orden en que se colocan
los ingredientes en el anticucho corresponde al recorrido in-order del árbol. El primer ingrediente
(el nodo más a la izquierda) será el inicio del anticucho.

---

```py
    # Solución:
    def a_lista_doble_enlace(self):
        # creamos variables de estado para el recorrido
        # head: el primero de la lista
        self.head = None
        # prev: el que irá avanzando (último añadido al anticucho)
        self.prev = None

        # Función auxiliar que hace el recorrido
        # esta es la función CLAVE
        self.lista_doble_enlace(self.raiz)

        # Ahora, solo arreglamos para que quede bien formateado
        self.cabecera = NodoArbol(None, 0, None)

        # Cerramos conectando los extremos
        # Caso que el arbol estaba vacío:
        if self.head is None:
            self.cabecera.der = self.cabecera
            self.cabecera.izq = self.cabecera
        # Caso que el árbol no estaba vacío
        else:
            # head quedó como el primero,
            # prev quedó como el último que agragamos (ahora el último global)

            # Cabecera conecta en der con el primero (head), en izq con el
            # último (prev)
            self.cabecera.der = self.head
            self.cabecera.izq = self.prev

            # Ahora, el primero (head) debe conectar con cabecera
            # el último (prev) también, pero por el otro lado
            self.cabecera.der.izq = self.cabecera
            self.cabecera.izq.der = self.cabecera



    def lista_doble_enlace(self, nodo):
        # Caso Base: nodo es None
        if nodo is None:
            return

        # inorden: izq, raiz, der
        self.lista_doble_enlace(nodo.izq)

        # Si self.prev es None, quiere decir que no hemos empezado el anticucho
        if self.prev is None:
           self.head = nodo
        else:
          # crear punteros de la lista
          self.prev.der = nodo
          nodo.izq = self.prev

        # Avanzar el prev y seguir con lado derecho
        self.prev = nodo
        self.lista_doble_enlace(nodo.der)
```
