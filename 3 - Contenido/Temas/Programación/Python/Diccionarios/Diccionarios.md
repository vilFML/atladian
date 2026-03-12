Un diccionario es similar a una lista, pero los elementos se indexan con datos no necesariamente numéricos. Por ejemplo, supongamos que queremos convertir "piedra", "papel" y "tijera" a una representación numérica 0, 1, 2, respectivamente:
```py
p_a_n = {"piedra":0, "papel":1, "tijera":2} # para convertir de palabra a número

print(p_a_n["papel"])
```

La conversión inversa se puede hacer simplemente con una lista:

```py
n_a_p = ["piedra", "papel", "tijera"] # para convertir de número a palabra
print(n_a_p[1])
```

##### Ejemplo
Se puede construir una función en que el programa juegue 'cachípun' contra el usuario:
```py
def juega():
	from random import randint
	programa=randint(0,2)
	usuario=p_a_n[input("¿piedra, papel o tijera? ")]
	resultado="Empate" if programa==usuario else\
		"Gana Usuario" if (programa+1)%3==usuario else "Gana Programa"
	print("Usuario juega", n_a_p[usuario])
	print("Programa juega", n_a_p[programa])
	print("Resultado:", resultado)
```
