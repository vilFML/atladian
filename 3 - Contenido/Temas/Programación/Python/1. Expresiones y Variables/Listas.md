Una lista es una secuencia de datos de largo variable. Los datos pueden ser distintos tipos.
Los elementos de la lista se indexan partiendo desde `0`.

# Funciones

## Construir una lista
Una lista se puede construir como una declaración, indicando los elementos que tendrá en sus respectivas posiciones:
```py
Lista = [50,4.5,'gato']
```

también se puede construir en base a iterar una fórmula, para ir 'rellenando' los espacios con los resultados que se obtienen:
```py
C = [n**2 for n in range(1,7)]
```


## Agregar elementos
Se puede agregar un elemento *después del último elemento* con la función `'Lista'.append()`

## Extraer elementos

Con la función `'Lista'.pop()` se puede acceder a un elemento de la lista y, además, extraerlo de ella. 
- Por defecto se realiza al último elemento.

## Acceso a los Elementos

Se puede acceder a los elementos en una lista indicando su posición en ella, de la forma: `Lista[n]`, en donde se accede al dato en la n-ésima posición.
La primera posición en una lista es de posición `0`, o sea: `Lista[0]` corresponde al primer elemento en la lista.
- También se puede comenzar contando las posiciones desde el final de la lista, si se indica un número negativo, `Lista[-1]` es el último elemento de la lista.

También se puede recorrer la lista a través de una iteración en su subíndices:
```py

Lista = [5000,75.34,'perro']

for i in range(0,len(Lista)):
	print(Lista[i])
```

O bien, iterando *sobre los elementos* en la lista con la función `for`:
```py
Lista = [5000,75.34,'perro']

for l in L:
	print(l)
```


