el vertex shader se ejecuta una vez por cada vértice

EBO: sr pasa los índices

se tienen las posiciones
$$
\begin{matrix}
[0,1,2 \\
2,1,0]
\end{matrix}
$$

Se tiene un cuadrado, que se compone 

se vé q se repiten algunos vértices (por el lado que comparten los triángulos) entonces es más eficiente entregar una lista de los vértices y luego una lista con los 

vértices:
$$
\begin{matrix}
[(0,0), (0.5, 0), (0.5,0.5) \\
(0,0), (0, 0.5), (0.5, 0.5)]
\end{matrix}
$$

que es mejor entregar una lista de todos los vértices posibles:

$$
[(0, 0), (0.5, 0), (0, 0.5), (0.5, 0.5)]
$$
la información que almacena la información es el **VBO**



y luego entregar los índices de los vértices que tendrán los triángulos:
índices:
$$
[0, 1, 3, 0, 2, 3]
$$

así un triángulo tiene los vértices en los índices $(0, 1, 3)$ y el otro $(0, 2, 3)$

el último arreglo es el **VAO** que no almacena datos, si no que tiene información que indica a la GPU cómo vienen ordenados los datos: 
*Por ej:* Si la posición viene en forma de un arreglo de 3 números, el color de a 2, de qué tipo son los números (ej: `int`).


Los shaders modifican la geom y color en base a lo que se desee: profundidad del obj, altura, velocidad, etc.
Cada punto tiene su posición
y si se quiere pasar a todos los puntos de igual forma, se tienen los `uniforms`

# Partículas

Sirven para simular fluidos, masas deformes, etc.
Las partículas son una colección de objetos individuales, cada partícula sabe la información deella misma (pos, vel, etc)
las partículas se van a mover en base a fuerzas (externa o externas)
En cada frame se va a **actualizar su posición** en base a reglas definidas.

# P1
Se quiere hacer una clase partícula que tenga posición.
