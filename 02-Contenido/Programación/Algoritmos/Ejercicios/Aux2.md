# P1
Un entero positivo $n\in \mathbb{Z}^{+}$ puede ser descompuesto como la multiplicación de números primos. A estos números primos se les llamaran factores primos del número $n$. Por ejemplo, el número $n=90$ se descompone por $2*3*3*5$.
Implemente la función recursiva `factoresPrimos(n)` que, dado un número $n\in \mathbb{Z}^{+}$ retorna un string indicando la multiplicación de sus factores primos que lo descompone.
Por ejemplo: `factoresPrimos(90) == "2 * 3 * 3 * 5"`

___

```py
def factoresPrimos(n, d=2):
	## caso base: n es 1
	if (n == 1):
		return ''
	
	## Caso recursivo:
	# si n es divisible por d
	elif (n % d == 0):
		# se divide el nro para llegar a caso base
		resto = factoresPrimos(n/d, d)
	
		# si es el ultimo divisor, no agregar '*'
		if (n/d == 1):
			return str(d) + resto
		
		return str(d) + ' * ' + resto
		
	# n no es div por d, probar con el sig
	else:
		return factoresPrimos(n, d+1)
		
print(factoresPrimos(90))
```

# P2: Diagrama de Estados
Un genio lo ha encerrado en un laberinto con un solo camino con 3 puertas, una detrás de la otra. Para avanzar en cada puerta, usted debe adivinar un número del 1 al 9, si lo acierta, la puerta se abre, si no, vuelve al comienzo del laberinto. Modele este problema utilizando diagramas de estado y complete la función laberinto()

---
Se está frente a una puerta, la 'posición' en el laberinto es *frente a qué puerta se está*: `[INICIO] → Puerta 0 → Puerta 1 → Puerta 2 → [LIBERTAD]`
con el número `estado` representa en qué puerta se está. 
Hay dos tipos de transición y 4 estados posibles.

| Evento     | Resultado                           |
| ---------- | ----------------------------------- |
| Correcto   | Se avanza una puerta: `estado += 1` |
| Incorrecto | Volver al inicio: `estado = 0`      |


```py
def Laberinto():
	codigo = ['3', '6', '1']
	estado = 0
	
	while (estado < 3):
		print('Estas en la puerta', estado)
		x = input('Adivina el número secreto para pasar de puerta: ')
		
		if x == codigo[estado]:
			estado = estado + 1
			
		else:
			print('Incorrecto. Vuelves al inicio')
			estado = 0
	
	# se sale del bucle
	print('Correcto. Escapas del laberinto')
	
Laberinto()
```

