## Instrucciones iterativas: for

La instrucción `for` itera con una variable que toma valores de una lista dada. A menudo, esa lista se especifica mediante `range`.

Ilustraremos su uso generalizando los algoritmos que vimos antes para encontrar el máximo de un conjunto de dos o tres números, al caso de un conjunto con un número cualquiera de elementos:



```py
# Encuentra el máximo de una lista a
def maximo(a):
	m=a[0]
	# Al comenzar cada iteración, se cumple que m==max(a[0],...,a[k-1])
	for k in range(1,len(a)):
		if a[k]>m:
			m=a[k]
	return m

print(maximo([25, 42, 93, 17, 54, 28]))
```


El comentario que aparece junto al `for` describe lo que se llama el **invariante** del ciclo, y es muy útil para poder argumentar la correctitud del programa, así como para poder ayudar a su diseño.

  

El invariante una afirmación lógica que debe ser verdadera cada vez que se intenta iniciar una nueva iteración, lo cual incluye tanto la primera vez como el último intento, en que se detecta que el rango ya se ha agotado y el ciclo termina.

  

* La validez del invariante la primera vez la deben asegurar las instrucciones previas al ciclo, que se llaman instrucciones de *inicialización*. En este ejemplo, al comenzar el ciclo se tiene que $k=1$, y por lo tanto trivialmente se cumple que $m=\max(a[0])$.

  

* Las instrucciones al interior del ciclo (el "cuerpo de ciclo") parten de la premisa de que el invariante se cumple al inicio, y deben garantizar que se cumpla al final (para dejar todo listo para la próxima iteración). Esto se llama _preservar el invariante_. En este ejemplo, para asegurar que $m=\max(a[0],\ldots,a[k])$ sabiendo que ya era cierto que $m=\max(a[0],\ldots,a[k-1])$, se debe modificar $m$ solo en el caso de que $a[k]$ sea mayor que $m$, o dejarlo igual si no.

  

* Cuando se detecta que el rango se ha agotado, el invariante igualmente se cumple, y ambas cosas juntas deben asegurar que haya logrado el objetivo final deseado. En este ejemplo, cuando $k$ llega a ser igual a $len(a)$, el invariante implica que $m=\max(a[0],\ldots,a[len(a)-1])$, o sea, es el máximo de toda la lista.