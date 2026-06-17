## Ordenar Números (Hoare)

Se quiere encontrar el máximo valor entre tres números. Una posibilidad es comparar cada número:
```py
def max3(a,b,c):
	if (a>b):
		if (a>c):
			m = a
		else:
			m = c
	else:
		if (b>c):
			m = b
		else:
			m = c
	return m
```
se vé que la cantidad de líneas en el código crece exponencialmente, con cada número que se agrega.
Se puede implementar esta función de una mejor forma si se asume el primer número como mayor y luego comparar con los elementos restantes, reemplazando el mayor número según el caso:
```py
def max3_v2(a,b,c);
	m = a # Se asume el 1er elemento como el máximo
	if (b > m):
		m = b
	elif (c > m):
		m = c
		return m
```

### Propiedad Invariante
Viendo el algoritmo de la siguiente forma: 
Se tiene un conjunto de números en una lista $a$: $a[0],a[1],\dots,a[n-1]$ y un valor de 'corte' $p$. El algoritmo consiste en revisar la lista por la izquierda y por la derecha. En *un paso arbitrario* cuando se analizan los números en los índices $i$ por la izquierda y $j$ por la derecha:
- Con respecto al análisis por la izquierda: Cuando se está revisando el i-ésimo número (antes de revisarlo), desde el primer número $a[0]$ hasta el anterior al que se va a revisar $a[i-1]$, son **menores que $p$**. 
- Para la derecha, se tiene algo similar. Antes de que se revise el j-ésimo número, ya se tienen ordenados desde el último número $a[n-1]$ hasta el siguiente del que se va a revisar $a[j+1]$, que son **mayores que $p$**.


| Lista  | <p  | <p  | <p    |     | ... |     | >p    | >p  | >p    |
| ------ | --- | --- | ----- | --- | --- | --- | ----- | --- | ----- |
| Índice | $0$ |     | $i-1$ | $i$ |     | $j$ | $j+1$ |     | $n-1$ |

Para que el conjunto solución *por la izquierda* **crezca**, se necesita que *el elemento en la i-ésima posición sea* **mayor que $p$**. De esta forma el elemento $i$ se mantendrá en su posición luego de ser comparado con $p$, pasando a estar dentro del conjunto que contiene a los números menores que $p$: el conjunto solución. De forma similar, para que el conjunto por la derecha crezca, se necesita que el elemento en la posición $j$ debe ser **mayor que $p$**. En pseudocódigo:
```py
if (a[i] < p):
	# no hacer nada
	i = i + 1 # se pasa a siguiente elemento desde la izquierda
```
```py
if (a[j] > p):
#  no hacer nada
j = j - 1
```

Ahora, viendo el caso en que no cumplan las condiciones respectivas:
1. Si el $i$ésimo número es *mayor* que $p$, entonces el número debiese pertenecer al conjunto de los números a la derecha, entonces se debe *intercambiar la posición con $j$*.
2. Para el $j$ésimo número, si es menor que $p$, se intercambia con el número $i$.

| Lista  |     |     |     | x   | <-     | <p  |     |     |     |
| ------ | --- | --- | --- | --- | ------ | --- | --- | --- | --- |
| Índice | $0$ |     |     | $i$ | **->** | $j$ |     |     |     |
La condición que cumplen los elementos $i,j$ para ser parte del conjunto solución es **la propiedad invariante** que es la que se evalúa para los números.

Finalmente, el procesamiento se puede ver según los estados: Configuración Inicial, En progreso y Final.
1. **Configuración Inicial**: Se observa el estado inicial de los índices, antes de realizar algún procesamiento (o sea cómo inician los índices).
   En este caso, se inician los dos índices $i,j$ en el principio y final de la lista, respectivamente. O sea $i = 0$, $j=n-1$ (recordar que `len(A)` entrega el número de elementos, entonces el índice debe corresponder a una posición menos).
2. **En progreso**: Corresponde al método (o el algoritmo), esto es el análisis de los índices, cuál es la propiedad invariante y cómo cambian los conjuntos solución.
   Para este caso, para las posiciones arbitrarias a mitad de la lista $i,j$, se tiene que:
	   - Para la izquierda: Desde el primer elemento $a[0]$ hasta el anterior al que se va a procesar $a[i-1]$ son *menores que $p$*; Si el $i$-ésimo número es *menor* que $p$, entonces se pasa al siguiente número: `i += 1`
	   - Para la derecha: Desde el último elemento $a[n-1]$ hasta el siguiente que se va a procesar $a[j+1]$ son *mayores que $p$*. Si el $j$-ésimo número es mayor que $p$ entonces se pasa al siguiente número: `j -= 1`
	   - En ambos casos, si no se cumplen las condiciones, se intercambian las posiciones $i$ con $j$.
3. **Final**: Es el estado cuando ya se ha analizado la lista completa, según el algoritmo. Se debe notar *cómo finalizan los índices.*
   Para el ejemplo, como $i$ crece y $j$ disminuye, al final se encontrarán, de forma que $i$ será eventualmente mayor (o igual) que $j$.
En código:
```py
def particionHoare(a,p):
# retorna pto de corte,nro de elementos <p y la lista particionada

n=len(a)

# Condicion de inicio
i = 0
j = n - 1

# Proceso
while i<=j: # Condición de fin: hasta que i supere (o sea igual) a j
	if a[i]<p:   # Si elem a la izq es <p, no hacer nada
		i+=1
	elif a[j]>p: # Si nro a la der es >p, no hacer nada
		j-=1
	else:        # No se cumple alguna condición: intercambiar
		(a[i],a[j])=(a[j],a[i]) # si no se cumplen: intercambio
		# y seguir avanzando en ambos sentidos
		i+=1
		j-=1
	return (p,i,a)
```

## Exponenciación
La implementación de la potenciación se hacer de una forma común, multiplicando el mismo número $k$ veces:
```py
def potenciacion(x,n):
	y = 1
	for k in range(0,n):
		y = y * x
	return y
```
Pero también, se puede implementar de forma alternativa:
Cuando se tiene un número elevado a exponente par, si se amplifica el exponente por $\frac{2}{2}$, y se tiene: $z^{k \cdot \frac{2}{2}}=(z^{2})^{\frac{k}{2}}$, en donde se pasó al número $z^{2}$ elevado a $\frac{k}{2}$. Entonce se tienen que hacer $\frac{k}{2}$ operaciones.
- Ejemplo: $2^{8}=2^{8\cdot\frac{2}{2}}=(2^{2})^{\frac{8}{2}}=(2^{2})^{4}=4^{4}=4^{4\cdot\frac{2}{2}}=(4^{2})^{\frac{4}{2}}=16^{2}$ y sólo se debe elevar 16 al cuadrado.
  *Se redujo de hacer 8 operaciones a solamente 2 operaciones.*
```py
def potencia(x, n):
	y=1
	k=n
	z=x
	while k>0:
		if k%2==0: # caso k par
		z=z*z
		k//=2
	else: # caso k impar
		y*=z
		k-=1
	return y
```

### Algoritmo Binario
Lo anterior también se puede implementar de forma que, cuando $k$ se dividide por 2 se preserva el invariante y además $k > 0$ y, por lo tanto, no es necesario en tal caso volver a preguntar por aquella condición en el ciclo `while` :
```py
def potencia(x, n):
    y=1
    k=n
    z=x
    while k>0:
        while k%2==0: # caso k par
            z=z*z
            k//=2
        y*=z # aquí estamos seguros que k es impar
        k-=1
    return y
```
Este algoritmo tiene complejidad del orden de $O(\log_{2}n)$


OBS: Este algoritmo funciona para cualquier par de elementos de un conjunto que tenga multipicación asociativa. Por lo tanto, este algoritmo no solo sirve para elevar a potencia números enteros o reales, sino que además, por ejemplo, para calcular potencias de *matrices*.

## Ordenación: Algoritmo de Inserción
Se tiene un arreglo $a$ de tamaño $n$, y se quieren reordenar los datos para que queden todos los números de forma ascendente.
El algoritmo por inserción se basa en formar un conjunto ordenado hacia la izquierda de la lista, de forma que en sus estados se tiene:
1. **Inicio**: Se comienza con un subconjunto de tamaño $0$: $i=0$
2. **Proceso**: En un punto arbitrario $k$, se tiene que los elementos a la izquierda, desde el primero $a[0]$ hasta $a[k-1]$ están ordenados de forma ascendente.
   Para que $k$-ésimo pase a conjunto solución, se necesita que sea menor que el anterior para pasar dentro del conjunto solución, si cumple esto, se intercambian de posición y se repite el proceso hasta que el anterior sea menor que el analizado.
3. **Final**: El proceso termina cuando los $n$ elementos ya han sido procesados, esto es cuando $k = n$
En código:
```py
def ordena_insercion(a):
	n = len(a)
	for k in range(0,n):
		insertar(a,k)

def insertar(a,k):
	j = k   # señala la pos del elem que está siendo insertado
	while (k > 0 and a[k] < a[k-1]):
		(a[j], a[j-1]) = (a[j-1], a[j])
		j -= 1   # siguiente elemento para comparar
```
En este algoritmo, el elemento que se analiza pasa por muchos lugares antes de llegar a su lugar correspondiente, y se pueden ahorrar recursos si se almacena el elemento a cambiar en una variable auxiliar y se van moviendo los restantes hacia la derecha, y al final se inserta el nuevo elemento en su posición:
```py
def insertar(a, k):
	b = a[k]   # se almacena elem a cambiar
	j = k
	while (j > 0 and b < a[j-1]):
		a[j] = a[j-1]   # nro anterior se corre hacia pos a al derecha
		j -= 1
	a[j] = b   # Se inserta en la posición
```
Para la eficiencia, se pueden ver varios casos:
1. El mejor caso es si el arreglo ya está ordenado, en cuyo caso, el procesamiento principal de `insertar()` (el ciclo `while`) termina de inmediato. Pero de todas formas se analizan los $n$ elementos de la lista, entonces se tiene una complejidad del orden de $O(n)$.
2. El peor caso es si el arreglo viene en orden decreciente, pues para cada número desde la derecha se deben revisar todos los números a la izquierda de él. En la función de `insertar()` se hacen el máximo de iteraciones ($k = n$). Si esto se realiza para los $n$ números, entonces se tiene una complejidad de orden cuadrático $O(n^{2})$
3. Caso promedio: si el arreglo viene en orden aleatorio, en la función `insertar()` se harán aproximadamente $\frac{k}{2}$ operaciones y la suma de estos costos igual será de $O(n^{2})$.

## Ordenación por Selección
Anteriormente se vió que se pueden ordenar números si se hace una comparación entre ellos. Por consiguiente, se puede tomar como idea de ordenación *identificar el máximo número* en un arreglo y luego *insertarlo en su posición correspondiente: la última*. Como este último elemento ya está ordenado, se busca el número más alto sin contar el que ya se ordenó, y este irá en la posición siguiente (desde la derecha).
### Propiedad Invariante
Hasta una k-ésima posición se sabe que los elementos a la derecha ya están ordenados y a la izquierda no todavía, pero además está garantizado que no hay número mayor que los ya ordenados en los números a la izquierda. Formalmente:
$$
\forall j\in[k.n-2]:a[j]<a[j-1]
$$
Viéndolo por estados:
1. **Inicio**: Antes de empezar a procesar, se tiene que $k$ es el n-ésimo elemento de la lista (el último).
2. **Proceso**: En un punto arbitrario $k$ del proceso, se busca el máximo número de entre los números a la izquierda. Al encontrarlo, se intercambia de posición con el elemento que sigue a $k$: $a[k-1]$, haciendo crecer el conjunto solución por derecha.
3. **Final**: Teóricamente el proceso finaliza cuando $k=0$, pero también termina en $k=1$ pues se cuenta como que el mismo elemento $k$ ya está ordenado.
En código:
```py
def ordena_seleccion(A):
	n = len(A)
	for k in range(n,1,-1):   #se empieza desde el final hasta 1 y se decrece en 1
		j = pos_max(A,k)   #fn que entrega el indice del mayor nro de la lista desde el inicio hasta kesima pos.
		(a[j], a[k-1] = a[k-1], a[j])

def pos_max(A,k):
	j = 0   #j es la pos del max, se asume el primero como maximo
	
	# para cada elemento hasta el kesimo, si es mayor al almacenado, reemplazar como elemento mayor
	for i in range(1,k):
		if (a[i] > a[j]):
			j = i
	return j
```

En este algoritmo siempre se recorre todo el conjunto de tamaño $k$ para encontrar el máximo, pues se van comparando los números adyacentes y la suma de todos estos costos da un total de $O(n^{2})$.

### Contar Número de Operaciones
Para comparar un elemento de un total de $n$, se toma como referencia el elemento y se compara con los otros $n-1$. Luego, para cada elemento, se hace cada vez una comparación menos (pues ya se ha comparado), entonces se tienen:
$$
(n-1)+ (n-2)+\dots=\frac{(n-1)\cdot n}{2}=\frac{n^{2}-n}{2}
$$
en donde, para un número $n$ de elementos muy grande, el término cuadrático toma preponderancia sobre el término lineal $n$. Entonces se tiene una complejidad del orden de $O(n^{2})$.

## Ordenación: Algoritmo Burbuja
Para ordenar una secuencia de $n$ elementos, este algoritmo consiste en realizar una comparación de a pares de los números e intercambiarlos de posición si están fuera de orden. Notar que cada comparación incluye al que se acaba se acaba de cambiar de posición, esto requiere recorrer la lista varias veces para ordenarla completamente.
Es similar al algoritmo de selección, pues de hacen comparaciones entre los números. La diferencia es que este algoritmo mueve los números mas bajos cada vez mas cerca de su posición final aproximada (hacia la izquierda de la lista).
### Propiedad Invariante
En un punto $k$ arbitrario, se tiene que los elementos, **desde el k-ésimo elemento** ya están ordenados, y los de la izquierda todavía no.
> Analizando el efecto de una pasada de izquierda a derecha, vemos que, aparte de los pequeños desórdenes que pueda ir arreglando por el camino, una vez que el algoritmo se encuentra con el máximo, los intercambios lo empiezan a trasladar paso a paso hacia la derecha, hasta que finalmente queda en el extremo derecho del arreglo. Eso significa que ya ha llegado a su posición definitiva, y no necesitamos volver a tocarlo. Por lo tanto, el algoritmo puede ignorar esos elementos al extremo derecho, los que por construcción están ordenados y son mayores que todos los de la izquierda.
Implementación:
```py
def ordena_burbuja(a):
	n = len(a)
	k = n   #Inicio: nro de elementos todavía desordenados
	while (k > 1):   #cuando k llega al inicio, ya se tomo cada elem hacia la derecha para llevarlo a su posición correcta
		# Se hace una pasada desde a[0] hasta a[k-1] intercambiando elem contiguos desordenados
		for j in range(0,k-1):
			if (a[j] > a[j+1]):
				(a[j], a[j+1]) = (a[j+1], a[j])
		k -= 1
	
```


Este algoritmo siempre tiene complejidad del orden $O(n^{2})$, incluso si se tiene un arreglo ya ordenado. Pues realiza las $n$ comparaciones para los $n$ elementos.
Una segunda implementación es agregar una variable booleana que indique si se realizó algún intercambio en la pasada actual: Si no se realizan cambios, entonces la lista ya se ordenó y se debiese terminar de ejecutar el algoritmo. En este sentid, también se pueden 'saltar' comparaciones: Si hasta cierto punto ya están ordenados, se quisiera empezar a analizar desde ese mismo punto, entonces se introduce una variable $i$ que almacena la última posición en donde se hizo un intercambio (entre $a[i-1],a[i]$), así, si desde este punto no se encontraron elementos fuera de orden, se tiene que $a[i-1]<a[i]$ y luego a partir de ahí todos los elementos hasta el final del arreglo están ordenados.
```py
def ordena_burbuja_v2(a):
	n = len(a)
	k = n
	while (k>1):
		i = 0
		for j in range(0, k-1):
			if (a[j] > a[j+1]):
				(a[j], a[j+1]) = (a[j+1], a[j])
				i = j+1
				
		k = i
```
así se ordenan elementos en un tiempo de ejecución lineal si se tiene una lista ordenada. Para el peor caso posible, sigue siendo de orden cuadrático.

## Ejercicio 1: Ordenación Lomuto

Existe un algoritmo alternativo a Hoare, que resulta en una codificación más sencilla. Este algoritmo, debido a **Lomuto**, se basa en el siguiente invariante:

![particion-Lomuto](https://github.com/ivansipiran/AED-Apuntes/blob/main/recursos/particion-Lomuto.png?raw=1)  

En este algoritmo, en cada iteración, si $a[j]<p$, se intercambian $a[i]$ con $a[j]$ y se incrementa $i$, porque ahora hay un elemento más en el grupo de los menores que $p$. Después de esto, se incrementa $j$, *incondicionalmente* (¿por qué es correcto hacer eso?).

- Se debe aumentar $j$ porque se mantiene la cantidad de mayores que $p$ y se aumentó la cantidad de menores que $p$. Entonces, se debe desplazar el análisis al siguiente elemento de la lista sin revisar.

Implementación:
1. Inicialmente no hay elementos de la lista procesados, entonces el tamaño de los conjuntos solución de los menores que $p$ es vacío: $i=0$ y los mayores que $p$ también: $i=0$
2. **En proceso**:  Cada elemento no procesado pertenece a la lista marcada con '?', entonces se analiza el número j-ésimo:
   - Si $a[j]<p:$ entonces el número debiese estar en el conjunto solución izquierdo, se debiese hacer crecer dicho conjunto al pasar este elemento a la i-ésima posición y el elemento que está en $i$ es parte de los $>p$ y se intercambia con elemento en $j$ (así se procesa después como $>p$)
   - Si $a[j] > p$, el elemento pertence al conjunto solución $>p$. Entonces se hace crecer el conjunto solamente acrecentando $j$.
1. **Final**: El análisis de la lista se termina cuando el índice $j$ supera la cantidad total de elementos $n$, o sea cuando $j>n$


```py
def particionLomuto(a,p):
	# Retorna pto de corte: p; nro de elementos <p: i; lista procesada: a
	
	n = len(a)   # total elementos de lista	
	i = 0        # inicialmente <p no tiene elementos (ninguno procesado)
	
	for j in range(0,n):   # para cada jesimo (elemento de la lista)
		if (a[j] < p):     # si jesimo es menor que p:
			#intercambiar: jesimo pertenece a conj <p, iesimo sigue perteneciendo a >p
			numGuardado = a[i]   # respaldar iesimo
			a[i] = a[j]          # almacenar jesimo en iesimo
			a[j] = numGuardado   # se preserva el >p en conjunto derecho
			i += 1               # crece conjunto solucion <p
	
	return (p,i,a)
	
```
