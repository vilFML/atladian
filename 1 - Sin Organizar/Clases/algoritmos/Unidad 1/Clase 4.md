# Ordenación Selección
Se tiene un conjunto de números cualquiera

En la primera posición se debiese tener el menor elemento y en la última posición el mayor elemento.
Se vio anteriormente que en una secuencia de números se puede tener el máximo y el mínimo valor haciendo comparaciones de a pares.

Si se identifica el máximo en una posición $j$ este debe ir al final, entonces se intercambia con el que está en la última posición. Luego, este elemento no debiese moverse pues ya es el máximo. 
Para ordenar el penúltimo elemento, se debe notar que el último elemento ya es el máximo de todos los números, pues ya fue procesado. Así, se debiese realizar el mismo proceso para la lista de números hasta la posición $n-2$

Prop. invariante:
hasta una $k$esima posición, los elementos a la derecha de $k$ ya están ordenados y los elementos a la izquierda están desordenados *pero* se sabe que *ninguno de los elementos sin ordenar (a la izq) va a ser mayor que alguno de los elementos en la parte ya ordenada*. Formalmente:
$$
a[j]<a[j+1], \forall j\in[k,n-2]
$$
esto dice que lo que está a la derecha del elemento en $k$ están ordenados,
$$
a[i]<a[j], \forall i \in[a,k-1],j\in[k,k-1]
$$
![[Pasted image 20260319105029.png]]
1. En el inicio no se ha hecho el procesamiento, entonces $k$ es el elemento $n$ pues por la propiedad invariante se requiere que los elementos a la derecha de $k$ estén ordenados. Al inicio no se ha ordenado, entonces ninguno es mayor por ahora.
2. Progreso: En un punto arbitrario $k$ dentro de la secuencia de números. Se encuentra el valor máximo en la lista desordenada (a la izq de $k$) y se intercambia con el que se encuentra en $k-1$ posición para *hacer crecer la colección de números ordenados* y se hace retroceder a $k$.
3. Final: $k = 0$ teóricamente, pero también $k=1$ pues, por la propiedad invariante, se sabe que el elemento en $k$ pertenece al conjunto ordenado y, por lo tanto, no se necesita comparar el elemento restante en la primera posición.

**Implementación**:
```py
# Ordenación por Selección
def ordena_seleccion(a):
    n=len(a)
    for k in range(n,1,-1): # Se comienza en el final hasta la pos 1.
        j=pos_maximo(a,k) # fn entrega pos de max de lista 'a' desde inicio hasta la pos k
        (a[j],a[k-1])=(a[k-1],a[j])
```

```py
# Encuentra posición del máximo entre a[0],...,a[k-1]
def pos_maximo(a, k):
    j=0 # j señala la posición del máximo, se asume el 1er elem como max (pos 0)
    for i in range(1,k):
        if a[i]>a[j]: # si elem en posicion i es mayor que el de la pos j
            j=i # cambiar la posicion del maximo al q se encontro
    return j
```

## Contar número de operaciones
Para comparar un elemento en $n$ elementos, se deben comparar todos los elementos (sin contar el de referencia). Entonces se hacen $n-1$ comparaciones. Así, para cada elemento de una lista de $n$, se hacen:
$$
n-1+n-2+m-3+\dots+1 =\frac{(n-1)n}{2}\approx \frac{n^{2}-n}{2}
$$
que si se compara con números grandes, el $n^{2}$ domina el polinomio. Así, cuando el algoritmo se ejecuta en una cantidad de $n$ elementos, se hacen operaciones del orden de $O(n^{2})$ en el peor caso. Pero para el mejor caso (que la lista ya esté ordenada) también se realiza cada comparación de elementos pues es la única forma de asegurar que cada elemento es mayor que los otros. Así, también se tienen operaciones del orden de $O(n^{2})$.

# Algoritmo Burbuja
Dada una secuencia de $n$ elementos, el algoritmo consiste en ir comparando de a pares los elementos e intercambiarlos de posición si están fuera de orden; notar que cada comparación se hace incluyendo el elemento que se cambió (o si no se cambió) . Esto requiere recorrer la lista varias veces para tenerla completamente ordenada.
En comparación al algoritmo de selección, este algoritmo mueve también los números menores hacia las posiciones a la izquierda, cada vez más cerca de su posición correcta en la ordenación.

## Propiedad Invariante
En un punto arbitrario $k$ del procesamiento, se tiene que los elementos **desde** el $k$esimo elemento ya están ordenados y los de la izquierda todavía no.
![[Pasted image 20260319111330.png]]

*implementación:*
```py
# Ordenación de la Burbuja (versión 1)
def ordena_burbuja(a):
    n=len(a)
    k=n # Inicio: elementos a la derecha no ordenados -> se comienza desde final
    while k>1:
        # Hacer una pasada sobre a[0],...,a[k-1]
        # intercambiando elementos adyacentes desordenados
        for j in range(0,k-1):    # Se comienza desde el primer elem (pos 0)
            if a[j]>a[j+1]:
                (a[j],a[j+1])=(a[j+1],a[j])
        # Disminuir k
        k-=1
```
