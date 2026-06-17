Suponga que se tiene una tabla de hashing con Linear Probing, de tamaño 10, inicialmente vacía, con la función de hashing $h(x) = x \bmod 10$ (por ejemplo, $h(64)=4$). Muestre en la siguiente tabla el resultado de insertar (a mano) la siguiente secuencia de llaves:  
```

34, 59, 45, 27, 14, 22, 75, 25

```

# Desarrollo
Para la función hashing $h(x)=x \bmod 10$
$$
\begin{array}
 \\
h(34)=3 \\
h(59)=9 \\
h(45)=5 \\
h(27)=7 \\
h(14)=4 \\
h(22)=2 \\
h(75)=5 \\
h(25)=5
\end{array}
$$
luego, asignado las llaves $x$ en los índices resultantes $h(x)$, para cada iteración:

1. 

| Tabla |     |     |     | 34  |     |     |     |     |     |     |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| index | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
2.

| Tabla |     |     |     | 34  |     |     |     |     |     | 59  |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| index | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
3.

| Tabla |     |     |     | 34  |     | 45  |     |     |     | 59  |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| index | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
4.

| Tabla |     |     |     | 34  |     | 45  |     | 27  |     | 59  |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| index | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
5.

| Tabla |     |     |     | 34  | 14  | 45  |     |     |     | 59  |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| index | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |

6.

| Tabla |     |     | 22  | 34  |     | 45  |     |     |     | 59  |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| index | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
7.
$h(75)=5$, pero casilla `5` ya contiene un valor, entonces se asigna a $h(75)+1=6$

| Tabla |     |     | 22  | 34  |     | 45  | 75  |     |     | 59  |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| index | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
8.
Lo mismo para $h(25)=5$, y como contigua también tiene valor, se asigna a $h(25)+1+1=7$

| Tabla |     |     | 22  | 34  |     | 45  | 75  | 25  |     | 59  |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| index | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |