# Instrucciones
## If
La instrucción `if` permite ejecutar bloques de código solo si es que se cumple una determinada condición.

### Sintaxis en Python

```py
if 'condicion':
	instruccion 1
	instruccion 2
	...
	instrucion n

instruccion #fuera del bloque condicional
```

Cuando se tiene un `if` ocurre que:
1. Si es que la condición se evalúa a `True`, entonces se ejecutan sucesivamente la instrucción 1, instrucción 2, y así hasta que se ejecuten las $n$ instrucciones.
2. Si es que la condición se evalúa a `False`, *se ignora* todo el conjunto de instrucciones y, por lo tanto, se ejecuta la instrucción fuera del bloque condicional.

gráficamente en un diagrama de flujo:
![[Pasted image 20260302140637.png]]


## if-else
Para ejecutar líneas de código únicamente en caso de que la confición sea evaluada a `False`, se utiliza la palabra reservada `else`. En este caso, las instrucciones del bloque `else` se ejecutarán únicamente si es que la condición es `False`.

**Sintaxis:**
```py
if 'condicion':
	instrucciones bloque if
else:
	instrucciones bloque else

instrucciones #fuera del bloque condicional
```

gráficamente:
![[Pasted image 20260302141022.png]]

## elif
`elif` es una abrevación de else-if