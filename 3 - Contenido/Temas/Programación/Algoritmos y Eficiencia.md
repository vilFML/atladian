# Verificación de Correctitud de Algoritmos

Es necesario ver el método (o algoritmo) de una solución **antes de implementarlas**. Esto se hace en base a las matemáticas. 

- Esto no es lo mismo que verificar la **eficiencia** del algoritmo. Solamente verifica que el algoritmo soluciona el problema, pero no el *tiempo de ejecución*.
## Con IF

Encontrar el máximo valor entre dos valores:

```py
# Encontrar el máximo entre dos valores
def max2(a, b):
	if a>b:
		m=a
	else:
		m=b
	return m
print(max2(3,7))
```

Esto se puede generalizar a 3 valores, pero la cantidad de líneas de código *crece exponencialmente* con la cantidad de valores agregados.

```py
# Encontrar el máximo entre tres valores
def max3(a, b, c):
    if a>b:
        if a>c:
            m=a
        else:
            m=c
    else:
        if b>c:
            m=b
        else:
            m=c
    return m
print(max3(4,3,7))
```

Una mejor alternativa se puede obtener si se asume el primer elemento como el mayor, luego basta comparar con los otros elementos restantes. Así la cantidad de código ya no crece de forma exponencial.
```py
# Encontrar el máximo entre tres valores
def max3(a, b, c):
    m=a
    if b>m:
        m=b
    if c>m:
        m=c
    return m
print(max3(4,3,7))
```


Al ejecutar el código, hasta una posición $k$ arbitraria, se va a tener lo que se conoce como *propiedad invariante*. En este caso



# Propiedad Invariante

todos los elementos desde `a[0]` hasta `a[i-1]` son menores que $p$, y todos los elementos desde `a[j+1]` hasta `a[n-1]` son mayores que $p$ 

1. Para que *crezca* el conjunto solución por la izquierda, se necesita que el elemento en la posición `i` sea menor que $p$, así el elemento se mantiene en su posición y pasa a ser parte del conjunto que contiene los números menores que $p$.
   O sea, `a[i] < p` y luego `i + 1` para seguir al siguiente elemento.
2. Para que crezca el conjunto solución por la derecha, se necesita que el elemento en la posición `j` sea *mayor* que $p$, que se tiene lo mismo que el caso anterior.
   O sea, `a[j] > p` y luego `j - 1` para seguir al siguiente elemento (desde la izquierda).
3. Y en el caso en que *no* se cumplan que los elementos sean menores o mayores, respectivamente, se intercambian los elementos para ser parte del conjunto contrario, pues si un elemento a la derecha es menor que $p$, este debiese ser parte del conjunto a la izquierda y lo mismo para un elemento del otro lado. 
4. Luego, se intercambian la posición de los elementos.

Luego, 
1. Configuración inicial cuando se está viendo el caso inicial: Cuando los elementos solución son listas vacías pues no se están analizando elementos. 
2. En progreso: Lo anterior (el método)
3. Final: Cuando `i` es igual a `j` se asegura que se terminó el análisis

## Eficiencia

Se puede tener el *mejor* o *peor* caso. 
1. El mejor caso es que ya se tenga una lista ordenada, por ejemplo. 
2. El peor caso es que se tenga que realizar la operación en absolutamente cada uno de los elementos, aumentando 