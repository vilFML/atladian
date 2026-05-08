El objetivo de esta tarea es que usted implemente un algoritmo eficiente para encontrar el máximo en una secuencia unimodal.

Supongamos que se tiene una secuencia de $n$ números. Se dice que es unimodal si tiene una sola moda o máximo global y no tiene máximos locales. Por ejemplo, la siguiente secuencia es unimodal y el máximo es $78$.

```
12 18 23 31 37 62 78 71 60 55 43 40 35 31 26 21 20 15
```

Para simplificar, vamos a suponer que la secuencia es estrictamente ascendente hasta llegar al máximo, y a partir de ahí es estrictamente descendente.

# Un algoritmo de dividir para reinar

Supongamos que la secuencia está almacenada en un arreglo $a$, y que en un momento dado sabemos que el máximo se encuentra en el rango $a[i], \ldots, a[j]$ (inicialmente $i=0$, $j=n-1$). A continuación calculamos dos subíndices $k1$, $k2$ tales que $i<k1<k2<j$ y tal que los intervalos definidos por ellos sean aproximadamente del mismo tamaño ($1/3$ de la distancia entre $i$ y $j$). Luego comparamos $a[k1]$ con $a[k2]$ y en base al resultado podemos descartar
uno de los tres tercios y seguimos buscando en los dos tercios restantes. Considere los casos $a[k1]<a[k2]$ y $a[k1]>a[k2]$ (que debiera ser simétrico del anterior). Considere aparte el caso $a[k1]=a[k2]$.

# Desarrollo
# Escriba aquí su algoritmo

Primero se recibe una lista de números 'a', usando índices i = 0 (desde el primer número) hasta j = n - 1 (hasta el último número).
Luego, para esta lista se necesita sub-dividir en 3 tramos de igual tamaño, calculando los subíndices k_1, k_2 y se tienen tres subtramos:
1. (k_1 - i),
2. (k_2 - k_1),
3. (j - k_2)

Se comparan los elementos en estos dos índices y como la lista esta ordenada de forma que el valor máximo esta rodeado de números menores (y sería el único que se repite), esto es que no tiene máximos locales; se ven tres casos:
1. k_1 < k_2: los elementos menores están en el primer tramo, por lo tanto se descarta.
2. k_1 > k_2: los elementos mayores están en el primer tramo, se descarta el último.
3. k_1 == k_2: Son iguales, asi que se puede descartar cualquier tercio.
para todos los casos se aplica la misma función para la nueva lista, usando los índices modificados respectivamente. Así, se incluyen los dos tramos que no se descartan.

```py
import numpy as np
def encuentra_max(a):
  # Iniciar índices: i en primer número, j en último
  n = len(a)

  j = n - 1
  i = 0

  # para tener k_1, k_2: lista se subdivide en 3
  k1 = n // 3                                                                   # Se usa división entera para tener solo el int menor
  k2 = int(np.floor(2 * (n / 3)))                                               # Se multiplica por dos para tener el segundo tercio
                                                                                #   y floor pues se redondea al mínimo para reducir el tmñ

  if (i == j):
    # Se llego a lista de 1 elemento, retornar max
    return a[i]

  #comparaciones#
  if (a[k1] < a[k2]):
    # k1 es menor que k2 -> aumenta inicio hasta k1
    i = k1 + 1

    return encuentra_max(a[i:n])
    
  elif (a[k1] > a[k2]):
    # k1 es mayor a k2 -> dism fin hasta k2
    n = k2

    return encuentra_max(a[i:n])
  
  else:
    # si elementos son iguales, se descarta el último tercio
    i = k1 + 1

    return encuentra_max(a[i:n])
```
