Si $g(n)$ es el número de formas de completar $n$ pasos estando en el origen y sea $f(n)$ la cantidad de formas de completar $n$ pasos estando a distancia 1: 
1. $g(n)$: para completar n passos estando en el origen: ver siguientes 4 pasos a distancia 1, osea $g(n)=f(n-1)$ pues siempre se alejará en el primer paso.
2. $f(n)$: para completar $n$ pasos estando a distancia 1, se tienen dos subcasos:
	1. Volver al origen y queda resolver $n-1$ pasos desde origen, o sea $g(n-1)$
	2. Otra forma: mantener la distancia 1 del origen y quedan $n-1$ pasos por resolver, o sea $f(n-1)$
Luego,
$$
f(n)=g(n-1)+f(n-1),g(n)=f(n-1)\iff g(n-1)=f(n-2)
$$
$$
f(n)=f(n-1)+f(n-2) \implies f(5)=f(3)+f(4)
$$
