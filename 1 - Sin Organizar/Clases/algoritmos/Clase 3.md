|Materia: Algoritmos
	Fecha cátedra: 17/03/26
	Fecha digitalización: 17/03/26
	*tags:* #algoritmos

# Invariantes

## Potenciación (Algoritmo Binario)

Una primera implementación corresponde a repetir la multiplicación del número $k$ veces. Así, se tienen $k$ operaciones:
```py
def potencia(x, n):
	y=1
	for k in range(0,n):
		y*=x
	return y
```

Con la segunda implemetación:
1. Se tiene un exponente par, se puede amplificar por $\frac{2}{2}$ y se puede hacer $(z^{2})^{k/2}$ luego se tienen que hacer $\frac{k}{2}$ operaciones.
Así, si se quiere la potencia $2^{8}$ este con el cambio de variable de $z$, se pasa a $4^{4}$, y este a su vez $16^{2}=256$. En donde, en vez de hacer 8 veces la operación de multiplicar, se redujo a solo 4 operaciones.

```py
def potencia(x, n):
    y=1
    k=n
    z=x
    while k>0:
        if k%2==0: # caso k par
            z=z*z    # Se aumenta la base a su cuadrado
            k//=2    # Se reduce el exponente a la mitad
        else:      # caso k impar
            y*=z    # 
            k-=1    # Se reduce el exponente impar para ser par
    return y
```

Luego, se puede ver que se tiene un caso favorable y otro desfavorable del valor de $k$: Que sea par o sea impar. Pero, como $k$ es un número entero, este, si es impar, se sabe que la mitad de las veces será par.


La cantidad de veces que se debe dividir un número por 2 para que se tenga un 1 es $\log_{2}(n)$. El resultado es que, para elevar un número $n \approx 1000000$, se tienen 20 operaciones para obtener el resultado, mientras que con la primera implementación se tienen que hacer 1 millón de operaciones.

- La operación principal termina siendo dividir el exponente a la mitad en cada iteración. Y esto se logra en el orden de logaritmo de base 2.

Se puede mejorar en la verificación principal pues si se tiene que el exponente es par, al ser dividido, este siempre será mayor a 0. Así se puede 'capturar' la condición de $k$ par y que 'salga' cuando no lo es.

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

El algoritmo se llama **binario** pues al dividir por dos constantemente un número, se 'arrojan' la cantidad de `0` y `1` para representar el número procesado en código binario.

# Ordenación

Se tiene un problema clásico de ordenar una lista en orden aleatorio en un orden determinado (ascendente o descendente).

## Algoritmo de Inserción
Tiene la siguiente propiedad invariante:
1. Pensar qué esta pasando con el algoritmo en algún punto intermedio (o sea no trivial) arbitrario

Si se tiene el algoritmo en el elemento $k$, los elementos desde la posición `0` a `k-1` ya están ordenados.

Luego, se analiza *de qué forma el elemento en la posición `k`* pase al lado ordenado. Entonces se requiere que el elemento en `k` sea menor que el anterior para pasar dentro de la lista. Esto se repite para cada elemento en la lista y el elemento analizado empieza a avanzar hacia la izquierda en la lista ordenada **hasta que se tiene un número anterior que es menor que el elemento analizado** y el elemento se quedará en tal posición.

```py

```
