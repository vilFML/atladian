## Instrucciones iterativas: while

La instrucción `while` ejecuta instrucciones mientra la condición especificada sea verdadera:

```py
# Dice si un número dado es primo o no
def es_primo(n):
	if n==2:
		return True # 2 es primo
	if n%2==0:
		return False # ningún otro par es primo
	
	k=3
	while k**2<=n: # no es necesario buscar posibles factores más allá de sqrt(n)
	if n%k==0:
		return False # n es divisible por k => no es primo
	k+=2 # probamos solo los impares
	# si no se encontró ningún factor menor que raíz de n, es primo
	return True

print(es_primo(2), es_primo(7), es_primo(9), es_primo(79823492843), es_primo(79823492869))
```
