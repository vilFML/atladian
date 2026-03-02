[[Cálculo]]

Se busca el mín de f(x) s.a:
	1. x está en Rd
	2. x esta en un conjunto C, que una función

def:
	min global de f :
		f(xo) <= f(x), para todo x en Rd
	max global de f:
		f(xo) >= f(x), para todo x en Rd

Cuando se quieren resolver problemas de optimización, se buscan los máxs o mín globales, pero no hay teoría general para hacerlo.
Aunque en ciertos casos particulares, se puede resolver el problema:
	min (1/x) con x > 0,
	este problema no tiene solución.


pasando por encontrar un cjto más grande
def:
	Sea f desde Rd -> R
	x0 en Rd,
	decimos que:
	$\epsilon$
	
1. $x_0$ es un mínimo local de f si:
	1. $\exists \epsilon > 0 : f(x_0) \leq f(x) ,\forall x \in B(x_0,\epsilon)$
	2. 
2. 
3. 
	1. xo es un mínimo local de f si:
	existe  $\epsilon$ > 0 tq: f(xo) <= f(x), Para todo x en B(xo,\epsilon)



como resolver problema de opt:
1. probar que la solución existe. (probar q el min/max global existe)
2. encontrar min/maxs locales
3. ver cuál es el min/max global.


Criterios de optimalidad
teo: condición necesaria de primer orden CNPO

sea f : A $\subset$ Rd -> R
una función diferenciable en un abierto A, y sea Xo un min local de f:
	entonces: $\nabla f(x_0)$ = 0

pero, si $\nabla f(x) = 0$, para algún x en $R^d$
no necesariamente x es un mín o máx local

DEF:
sea f: a C R^d -> R, una fnc diferenciable,
x en Rd es un PTO CRÍTICO de f si $\nabla f(x) = 0$

el CNPO asegura q los mín/max locales de f son PTOS CRITICOS



Condición necesaria de segundo orden CNSG 
Sea f : A C Rd -> R
una función de clase C, en un abierto A
y sea x_o un min local de f
entonces:
	$\nabla f (x_o) = 0 \wedge H_f(x_o) >= 0$

