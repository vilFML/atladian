# Lenguaje C

C es un lenguaje tipado. Esto es que cada variable se define según el tipo de dato que se almacenará.

##### Archivo en C 
Ejemplo hello world, "hello.c": 
```C
#include <stdio.h> 

int main(void){
	printf("Hello, world"); 
}
```
 
`printf()` es una función que muestra texto. El argumento es el texto `'Hello, world'`.

##### Librerías 
Por la limitación de memoria en computadores antiguos, era necesario incluir solamente las funciones que se iban a utilizar mediante 'header files', denotados con la extensión '.h'. Estos archivos contienen la información de las funciones incluidas en las Librerías requeridas. 

Escencialmente, un header file le está comunicando al compilador que se quiere utilizar la librería indicada. 

Las librerias contienen funciones que se deben integrar en el código fuente cuando se requiera. 

En C se debe integrar la libreria <stdio.h> para utilizar la función 'printf()'. 

## Tipos
### Tipos Primitivos
Es posible definir nuevos tipos en C, pero los que son parte, de base, del lenguaje C son los **tipos primitivos**.

* **Para representar números enteros $\mathbb{Z}$:**

| Con signo   | Sin signo            | Tamaño (Bytes)  |
| ----------- | -------------------- | --------------- |
| `char`      | `unsigned char`      | 1 Byte = 8 bits |
| `short`     | `unsigned short`     | 2 Bytes         |
| `int`       | `unsigned int`       | 4 Bytes         |
| `long`      | `unsigned long`      | 8 Bytes         |
| `long long` | `unsigned long long` | 8 Bytes         |
las diferencies entre tamaños de tipos es necesario en la actualidad para acercarse a una programación lo mas eficiente posible. Pero antes los computadores tenian memoria limitada, entonces era necesario el manejo eficiente de la memoria.

* **Para representar números reales $\mathbb{R}$:**

| Con signo | Sin signo         | Tamaño (Bytes) |
| --------- | ----------------- | -------------- |
| `float`   | `unsigned float`  | 4 Bytes        |
| `double`  | `unsigned double` | 8 Bytes        |

* Para punteros se usarán 8 Bytes.

> C no tiene tipo `bool`. Para tal propósito, este interpreta el `int 0` como `False` y cualquier otro `int` como `True`.

> La diferencia entre los `unsigned` es que la representación con signo utiliza 1 bit (el primero a la izquierda) de los 8 que se utilizan para almacenar el número. Así, quedan 7 bits para el almacenamiento del módulo del número.
> Ejemplo: $\underbrace{1}_{ \text{Signo Negativo} }\underbrace{ 0101100 }_{ \text{Nro} }$

### Rangos de Representación

Cada tipo tiene una cantidad finita de números que puede representar, delimitados por rangos:

1. Para números enteros $\mathbb{Z}$ sin signo:

| Tamaño \[Bytes] | Tipo                 | Rango         |
| --------------- | -------------------- | ------------- |
| 1               | `unsigned char`      | $[0,2^{8})$   |
| 2               | `unsigned short`     | $[0, 2^{16})$ |
| 4               | `unsigned int`       | $[0,2^{36}]$  |
| 8               | `unsigned long`      | $[0,2^{64})$  |
| 8               | `unsigned long long` | $[0,2^{64})$  |

2. Para números enteros $\mathbb{Z}$ con signo.
Para $n$ bits del tipo, en general es de rango $[-2^{n-1},2^{n-1})$

| Tamaño \[Bytes] | Tipo        | Rango              |
| --------------- | ----------- | ------------------ |
| 8               | `char`      | $[-2^{7},2^{7})$   |
|                 | `short`     | $[-2^{15},2^{15})$ |
|                 | `int`       | $[-2^{31},2^{31})$ |
|                 | `long`      | $[-2^{63},2^{63})$ |
|                 | `long long` | $[-2^{63},2^{63})$ |
3. Para números reales $\mathbb{R}$, como C solo opera en base 2 (binario) no tiene una representación exacta de números reales. *La igualdad puede no cumplirse por el error en la representación*, entonces lo más seguro es usar un $\epsilon$ lo suficientemente pequeño que sea el rango de distancia entre dos números reales. 
   Por ejemplo:
   `float x;`, `float y;` y hacer: $|x-y| < \epsilon = 0,1$. Usualmente la igualdad se cumple, pero puede no suceder.
   

> **Overflow**
> 
A pesar de los rangos de los tipos, si el programa tiene una operación que tenga como resultado un número que esté fuera del rango de representación, C no entrega error, sino que **resuelve cambiando el número al menor que se úeda representar dentro del respectivo rango**.
\* También se cumple para la definición de una variable en la cual se asigna un valor que no está dentro del rango de su respectivo tipo.
Ejemplo: 
```C
unsigned char x = 255;
unsigned char y = 1;
unsigned char a = x+y;
```
luego `a` almacenenará un 0 pues no hay número más allá para el tipo `char`. El lenguaje resolvió a el menor número que puede almacenar el tipo. 

## Operadores

En C se puede hacer aritmética con: 

| Símbolo | Operación      |
| ------- | -------------- |
| `+`     | Suma           |
| `-`     | Resta          |
| `*`     | Multiplicación |
| `/`     | División       |
| `%`     | Módulo         |
\* El operador módulo `%` entrega el resto de una división. 

Las operaciones `*`, `/`, `+`, `-` no están definidas para los tipos `char` y `short`. En el caso en que se utilicen tales operadores, se hace un cast implícito a tipo `int`.

### Operadores Booleanos

Para realizar operaciones lógicas: 

| Símbolo | Operación |
| ------- | --------- |
| `&&`    | AND       |
| \|      | OR        |
| `!`     | NOT       |

y realizar comparaciones lógicas: Las expresiones booleanas resultan en dos posibles resultados: `TRUE` o `FALSE`. Y son utilizados en bloques condicionales.

| Símbolo | Significado             |
| ------- | ----------------------- |
| <       | menor que               |
| >       | mayor que               |
| <=      | menor o igual que       |
| >=      | mayor o igual que       |
| ==      | igual                   |
| !=      | no igual (diferente de) |

\* No es necesario utilizar el tipo de dato 'bool', en C cualquier número distinto de 0 es considerado como TRUE y el valor 0 como FALSE. 

## Variables 
Al definir una variable se está dando la instrucción al computador de reservar una cantidad fija de memoria según el tipo indicado.

**Definir**: Crear variable sin asignar un valor. Para ello simplemente se indica su tipo y su nombre, por ejemplo:
```C
int n;
```
En este caso se reserva un espacio de memoria adecuado y estas direcciones **pueden no estar vacías**. Por ello no necesariamente se tendrá un 0 almacenado en la variable.

**Inicializar**: Crear una variable y asignarle un valor a almacenar. Por ejemplo:
```C
int x = 10;
```
El símbolo '=' indica almacenar el valor a su derecha, en la variable indicada a su izquierda.

**Asignación**: Corresponde a almacenar un dato en una línea diferente a su declaración, por ejemplo:
```C
int n = 27;
n = 2
```
se creó la creó la variable `n` en una línea y en la otra se cambió el `int` que almacena.

También se puede indicar si se requiere que la variable no cambie luego de ser creada, para ello se agrega `const` antes de indicar el tipo. Por ejemplo:
```C
const int x i = 1;
```
en donde la variable `x` almacenará siempre un 1 de tipo `int` y no se podrá asignar otro valor en ella.

La idea de indicar el tipo es que con ello se indica la cantidad de memoria que se reservará para la variable, y la cantidad de memoria, especialmente en los primeros computadores, es limitada. Además de indicar el tipo de dato correcto para evitar confusiones, como por ej. tratar '01' como string en vez de su valor binario. 

También se pueden **crear múltiples variables en una misma línea**, separando con comas los nombres de cada variable que se creará. Las variables que se creen de esta manera *serán del mismo tipo*, por ejemplo:
```C
 int i,j = 10, 2
```
y se tienen dos variables de tipo `int` almacenando `10` y `2`, respectivamente.    

Una variable se puede visualizar como:
\* diagrama

Para tener el espacio que utiliza una variable se puede utilizar la función `sizeof()`. También se puede obtener de un tipo de dato `sizeof(int)`

Para saber la dirección de memoria en donde está almacenada una variable:
```C
&y
```
`&` entrega la primera dirección de memoria en donde se almacena la variable. El resto de direcciones se puede deducir según el tamaño del tipo pues las direcciones en memoria, para una misma variable, son contiguas.

## Funciones
Las funciones  por el usuario permite al programador abstraer ciertos bloques de código, además de aumentar la eligibilidad del código fuente, mantiendolo más ordenado.

### Creación de Funciones
Se debe indicar el tipo de dato que retornará (`int`, `string`, etc), luego el nombre de la función y entre paréntesis los argumentos que utilizará la función, de la forma:
```C
tipo identificador_funcion (tipo1 entrada1, tipo2 entrada2,...){
	...
}
```

\* Si no retorna un valor, si no que realiza algo estético, por ej., se indica el tipo de retorno `void`.

y la función se usa indicando el identificador con los datos de entrada:
```C
...
tipofunc var = identificador_fn(var1, var2,...);
```

Por ejemplo una función que calcula la suma entre dos números:
```C
int suma(int a, int b){
	int c = a+b;
	return c
}
```

### Funciones Nativas

Existen las funciones `while` e `if` usuales y se utilizan con la misma sintaxis al llamar una función por su identificador, pero el argumento es la condición a evaluar.

#### If
Se ejecuta un bloque de código después de evaluar una expresión booleana. La sintaxis es:
```C
if (expresion){
	//codigo a ejecutar en caso true
}
```
para incluir más expresiones a evaluar, se utilizan los bloques `else if`:
```C
if(){
}
else if (expresion2){
	// bloque de codigo 2
}
else if (expresion3){
	//bloque de codigo 3
}
```

Hay operadores booleanos (or, and, etc.) que se pueden agregar a las expresiones para combinar en una sola expresión. Se tienen:

| Operador | Código |
| -------- | ------ |
| OR       | \|     |
| AND      | `&&`   |
en caso de que todas las expresiones sean falsas y no se ejecute ningún bloque, el programa seguirá secuencialmente hacia abajo. Pero es posible indicar un bloque de código a ejecutar en caso de que ninguna de las condiciones se cumpla con el bloque `else()`:
```C
}
else{
	//codigo a ejecutar en caso 'por default'
}
```

#### While
En C se utilizan los ciclos WHILE() para ejecutar un bloque de código mientras las expresión dentro de los paréntesis sea verdadera, de la forma:
```C
while (condicion){
	//codigo mientras condicion sea V
}
```

#### For
Busca consolidar la implementación del ciclo `while()` dentro de una línea. Sintaxis:
```C
for (int i = 0; i<3; i++){
	//codigo en cada ciclo
}
```
Dentro de un mismo ciclo: 
- Solo en el primer ciclo se inicializa la variable `i` con valor 0.  
- Luego, se evalúa la expresión `i<3`
- Se ejecuta el bloque si es la expresión es verdadera.
- Al final de cada ciclo, se incrementa la variable de forma indicada `i++`.

## Expresiones

En C se puede usar la asociatividad de expresiones con paréntesis. Pero también hay precedencia de operadores en el mismo orden de la aritmética, por ejemplo: `a*b+c -> (a*b)+c`
También se puede hacer $a=b=c$ que el lenguaje lleva a `a = (b = c)`
> Lo mejor es explicitar los paréntesis para evitar que C haga asociaciones no esperadas.

### Inferencia de Tipos
La conversión de un tipo a otro se denomina **Cast**.

Cuando se tienen expresiones de distinto tipo, C infiere el tipo de dato. Por ejemplo, al dividir entre enteros `int`:
```C
int a = 1;
int b = 2;
int c = a/b;
```
C hace:
1. Observa el tipo de `a` y `b` y ve que son del tipo `int`. Luego, como se tiene una operación entre `int`: El resultado será `int` **independiente del tipo de la variable en donde se almacena el resultado `c`**.
2. Observa el tipo de `c` y le hace la conversión a su tipo.

Ejemplo:
```C
int a = 1;
int b = 2;
float c = a/b;
```
1. Primero se hará la división entre `int` lo que dará un `int`, entonces el $0.5$ pasa a ser 0.
   > C se queda con la parte entera del número.
2. Como `c` es de tipo `float`, entonces se hace una conversión de tal forma que `c` almacenará el valor `0.0`

En C las expresiones son entre variables del mismo tipo, entonces al tener una expresión entre tipos distintos **hace una conversión** ([Cast Implícito]) según la regla:
$$
\text{int} < \text{long} < \dots < \text{float}
$$

Si bien la conversión desde `char` a `int` sí cabe, no necesariamente se cumple al revés. En tal caso, se podría tener un overflow.

> Al hacer cast implícito, siempre se va convertir al tipo de mayor tamaño (en memoria) de las variables involucradsa en la expresión.

También se puede hacer cast implícito a toda una expresión, de la forma:
```C
(unsigned int)(a*b)
```
en donde:
1. Si `a`y `b` son de tipo `int`: hace la multiplicación de `a` y `b` int
2. Hace el cast del resultado de `(a*b)`

#### Cast Explícito
También se puede hacer un cast explícito de la forma:
```C
var = a/[float(b)]
```
en donde se convierte el tipo de `b` **solamente por la expresión**. Para cualquier otra sección del código, la variable sigue con el tipo con que se definió.


#### Cast Constantes
Al castear a `long long` y `unsigned long long` se puede usar equivalentemente sufijos para cortar el código, de la forma:
```C
[(long long) var] <-> varLL

[(unsigned long long) var] <-> varULL
```

## Números Binarios

En C los números se pueden representar indicando diferentes bases:
1. Para utilizar decimal: `int x = 10;`
2. Para utilizar octal: `int x=O10;`
3. Para utilizar Hexadecimal: `int x = 0x10;`
\* no nay base binaria
El más usado es hexadecimal.

##### Hexadecimal


Tabla resumen por tamaño (tipos comunes)

| Tipo | Tamaño (bits) | Rango hexadecimal (mínimo a máximo) | Ejemplo mínimo | Ejemplo máximo |
|------|---------------|--------------------------------------|----------------|----------------|
| `signed char` | 8 | `0x80` a `0x7f` | `0x80` (-128) | `0x7f` (127) |
| `unsigned char` | 8 | `0x00` a `0xff` | `0x00` (0) | `0xff` (255) |
| `short` | 16 | `0x8000` a `0x7fff` | `0x8000` (-32768) | `0x7fff` (32767) |
| `unsigned short` | 16 | `0x0000` a `0xffff` | `0x0000` (0) | `0xffff` (65535) |
| `int` | 32 | `0x80000000` a `0x7fffffff` | `0x80000000` (-2147483648) | `0x7fffffff` (2147483647) |
| `unsigned int` | 32 | `0x00000000` a `0xffffffff` | `0x00000000` (0) | `0xffffffff` (4294967295) |
| `long` (64-bit) | 64 | `0x8000000000000000` a `0x7fffffffffffffff` | `0x8000000000000000` (-9223372036854775808) | `0x7fffffffffffffff` (9223372036854775807) |
| `unsigned long` (64-bit) | 64 | `0x0000000000000000` a `0xffffffffffffffff` | `0x0000000000000000` (0) | `0xffffffffffffffff` (18446744073709551615) |
| `long long` (64-bit) | 64 | `0x8000000000000000` a `0x7fffffffffffffff` | `0x8000000000000000` (-9223372036854775808) | `0x7fffffffffffffff` (9223372036854775807) |
| `unsigned long long` (64-bit) | 64 | `0x0000000000000000` a `0xffffffffffffffff` | `0x0000000000000000` (0) | `0xffffffffffffffff` (18446744073709551615) |

Notas importantes:

- **Complemento a dos:** En tipos con signo, el valor más significativo (primer bit = 1) representa números negativos
- **Truncamiento:** Al asignar un valor hexadecimal a un tipo más pequeño, se pierden los bits más significativos
- **Sufijos:** Usa `u`, `l`, `ll`, `ul`, `ull` para forzar el tipo del literal
- **Dependencia de plataforma:** El tamaño de `int`, `long` y `long long` puede variar según la arquitectura y el compilador

### Operadores
Si 1 representa verdadero y 0 falso:
1. 'y' lógico: `&`:
   `0 & 0` = 0
   `0 & 1` = 0
   `1 & 0` = 0
   `1 & 1` = 1
Se puede operar con `&` entre dos números, en donde se opera cada bit entre sus respectivas posiciones con `&`. Por ejemplo:

$$
\begin{array}
   & & 0 & 0 & 1 & 1 \\
\& &   0 & 1 & 0 & 1 \\
  & - & - & - & -  \\
 &  0 & 0 & 0 & 1 
\end{array}

$$

2. 'o' lógico `|`:
   `0 | 0` = 0
   `0 | 1` = 1
   `1 | 0` = 1
   `1 | 1` = 1
También se pueden operar los bits respectivos:

$$
\begin{array}
 & & 0 & 0 & 1 & 1 \\
| &   0 & 1 & 0 & 1 \\
   & - & - & - & -  \\
   &  0 & 1 & 1 & 1 
\end{array}

$$

Los operadores `&`, `|` se pueden usar como funcionalidad en números:
1. `&` se puede utilizar para **extraer bits**:
Si se quieren extraer los últimos 4 bits, se debe operar el número procesado con un número que tenga `1` en las posiciones de los bits que se quieren extraer. Por ejemplo:
$$
\begin{array}
 &  & 0 & 0 & 1 & 1  & 0 & 0 & 1 & 1 \\
 \& & 0 & 0 & 0 & 0 & 1 & 1 & 1 & 1 \\
  &  - & - & - & - & - & - & - & - \\
   &  0 & 0 & 0 & 0 & 0 & 0 & 1 & 1 
\end{array}
$$

2. `|` para **unir** bits:
Si hay una ocurrencia de un `1`, el operador `|` va a entregarlo. Por ejemplo:
$$
\begin{array}
  &   & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 \\
| & 0 & 0 & 0 & 0 & 1 & 0 & 0 & 0 \\
  & - & - & - & - & - & - & - & - \\
  & 0 & 0 & 0 & 0 & 1 & 0 & 0 & 1 
\end{array}
$$

3. Negación `~`
Cambia el valor de verdad de un valor booleano.
- `~0` = 1
- `~1` = 0
Se puede usar para negar todos los bits de un número, por ej:
```
~ 1 1 1 0 1 ... 1
= 0 0 0 1 0 ... 0
```
se cambia el valor de cada bit (son 32 bits).

#### Desplazamiento de Binarios
Se pueden desplazar todos los bits de un número en una cantidad de posiciones.


##### Desplazamiento hacia izquierda `<<`
Para desplazar todos los bits de un número $i$ posiciones a la izquierda:
```C
valor << i
```
- Los bits que salen del rango de la variable se pierden
- Los espacios que se van creando a la derecha se van llenando con `0`.
Por ejemplo, mover a la izquierda 1 posición el número `0001` es:
```C
0001 << 1 == 0010
```

* Para números con signo **el bit correspondiente al signo también se mueve**, entonces se puede perder el signo de un número.

El desplazamiento a la izquierda **reemplaza a la multiplicación**. La equivalencia es que la cantidad $i$ de posiciones representa un multiplicación del número por $2^{i}$:

`valor << i` $\iff \text{valor}\cdot 2^{i}$

Por ejemplo, `0001 == 1` y `0010 == 2` luego `0001 << 1` entrega `0010`.

También se puede multiplicar por valores que no son potencias de 2 descomponiendo la multiplicación del factor en potencias de 2, como:
`valor * 5` $\iff$`valor * 4 + valor * 1` $\iff$ `val<<2 + val`

##### Desplazamiento hacia la derecha `>>`
De la forma:
```C
val >> i;
```
con $i$ la cantidad de posiciones a desplazar.

Se tienen comportamientos distintos según si el número es con o sin signo.
1. Número sin signo:
Los bits a la derecha se pierden por overflow y a la izquierda se llena con `0`. Ejemplo:
```C
1000 >> 1 == 0100
1000 >> 3 == 0001
```

2. Números **con** signo:
Los bits que hacen overflow se pierden y los bits nuevos intentan preservar el signo, entonces **se rellena con los bits del signo respectivo**. O sea,
- Para signo **negativo** se tiene un `1` como primer bit, luego se va a rellenar con `1`
- Para signo **positivo** se tiene un `0` como primer bit, luego se rellena con `0`.

Al desplazar constantes hacia la derecha, se consideran como `int` entonces se considera el signo. Por ello, si se tiene una constante negativa, se va a rellenar con `1`.

Ejemplo:
```C
1000 >> 1 == 1100

0100 >> 1 == 0010
```

> Por lo tanto en desplazamiento a la derecha se tiene comportamiento distinto según si el tipo es `unsigned` o no.

\* Los desplazamientos de una variable que se desplaza a sí misma se puede denotar equivalentemente como `x = x>>i` $\iff$ `x >>= i`

Si se quiere hacer un desplazamiento sin considerar el signo de un número, se puede hacer un cast a `unsigned`:
```C
(unsigned int)1 >> 1
```


---

El desplazamiento a la derecha es equivalente a dividir por una potencia de 2, en donde $i$ son las posiciones a desplazar que indica la $i$ésima potencia $2^{i}$:
`valor >> i` $\iff \frac{\text{valor}}{2^{i}}$

##### Máscara
Una máscara es un número tal que al operarlo con otro permite extraer sus bits, o sea este va a tener `1` en las posiciones que se quieran extraer.
Formas de formar una máscara:
1. Notación directa: Usando la notación hexadecimal, se indican los bits a almacenar directamente
   - Para `int` se tienen 8 bits
   `int m = 0xff`
2. Para una capacidad de 32 bits, se forma la máscara desplazando los bits una cantidad $32-i$ con $i$ la cantidad de `1` que tendrá la máscara desde la derecha.
   Por ejemplo, para una máscara con cuatro `1` o sea el número `000...0001111` se hace `int m = (unsigned int)-1 >> 28`: Por $32-4=28$ quedan cuatro `1` y se rellenan las posiciones a la izquierda con `0` por hacer cast a `unsigned` lo que ignora el `1` en el primer bit. 
3. Generar solo `1` en todas las posiciones y desplazar hacia la izquierda para tener `0` en las posiciones deseadas pues finalmente se niega todo el número para tener la máscara deseada.
   `int m = ~(-1<<4)` genera `000...001111` pues se negaron los bits `111111...11110000`.

## Punteros
Un puntero es un tipo particular de dado que **almacena una dirección de memoria** de una variable. No almacena valores (e.g. `int`, `float`, etc.).
> Se dice que un puntero *apunta* a una variable

Para definir un puntero se indica:
1. el tipo de la variable que almacena
2. un \* antes de su identificador
de la forma:
```C
int *identificadorPuntero
```

Un puntero se visualiza como:
![[Pasted image 20260821084540.png]]

- Se puede tener el tamaño del puntero con `sizeof(puntero)`
- Para tener la dirección de memoria a la que apunta `&puntero`

Ejemplo:
```C
int x = 10;
int *px;
px = &x;
```
en la última línea se asigna en el puntero la *dirección de memoria* de la variable `x`.

- Para acceder **valor que almacena x**, a partir del puntero: `*px`$\iff$`x`. 
  Con ello también se puede cambiar el valor que almacena `x`, por ejemplo: `*px = 20`$\iff$`x = 20`

Se puede cambiar la variable a la que apunta, o sea cambiar la dirección que almacena el puntero con:
```C
int z = 20;
px = &z;
*px = 50;
```
resumido como
```C
int z = 50;
int *pz = &z
```

> No se puede asignar una dirección de memoria manualmente, pues va a interpretar tal número indicado como un `int` y no una dirección de memoria. O sea *no* se puede hacer: `int *px = 0xffff`

## Arreglos
Los arreglos son conjuntos (tuplas) de variable que están contiguas en lameoria. 
> En C los arreglos deben **almacenar datos del mismo tipo**.

Se definen con `[]` indicando en el interior la cantidad de elementos que se almacenarán en él, para reservar los espacios de memoria necesarios. Es de la forma:
```C
tipo identificadorArreglo[nroDatos]
```
en donde solamente se está reservando el espacio de memoria según el número de datos indicado. En ello, el programa puede reutilizar espacios de memoria no vacíos (no necesariamente de inicializará con 0 en las casillas, incluso puede ser cualquier valor).

Para inicializar arreglo (e.g. asignar valores explícitamente), en el momento de definir:
```C
int a[5] = {1, 2, 3, 4, 5};
```
el identificador utilizado se define como **un puntero** que almacena la dirección de memoria **del primer dato** del arreglo. En el caso anterior se define un puntero `a` que apunta a `1`.
Para un arreglo `a` que almacena datos de tipo `double`:
![[Pasted image 20260821090818.png]]
el puntero almacena la dirección del primer dato.

Para acceder al primer valor del arreglo, se puede hacer de las formas:
1. `a[0]`
2. Usar el hecho de que `a` es un puntero, o sea se puede indicar `*a` que entrega el valor de la variable a la que apunta.
3. Usando aritmética de punteros: `*(a+0)`, lo que dice que se accede al valor apuntado por `a` y se 'avanza 0 posiciones'.

Para acceder al $i$ésimo elemento del arreglo `a`:
1. `a[i]`
2. `*(a+i)` en donde el puntero almacena la primera posición y hacer que se mueva $i$ posiciones a la derecha.
3. Usando ciclo `for()`: Se mueve el puntero a una nueva posición. En este caso **se modifica el arreglo** pues se apunta a otra dirección de memoria, cambiando *el origen del arreglo*.
```C
for (int w=0; w<i; w++){
	a++
}
```
en `i`=3 el cuarto elemento pasa a ser el origen del arreglo.

> En C no se puede saber el tamaño de un arreglo

> Acceder a un valor fuera del rango del arreglo está permitido (no entrega error), lo que entregaría cualquier valor que se encuentre en la dirección indicada.


## Strings
Un string es un arreglo de caracteres. Lo especial de los strings es que **siempre terminan con el valor 0 (o \0)** y gracias a este último caracter, se puede tener el largo de un string. Excepto eso, funciona como cualquier arreglo.
Formas de definir un string en C:
1. No se entrega el largo directamente y se indican los caracteres con un 0 al final, por tal caracter, el sistema puede saber cuánta memoria reservar.
```C
char s[] = {'h','o','l','a',0};
```
entregar el 0 al final le indica al lenguaje que es un string. Luego, `s` es un puntero hacia el primer caracter.

El corchete indica que será un **string mutable**, esto es que se puede *leer* y modificar como `s[] = "Otro"`

2. Indicar con doble comilla el string directamente. 
```C
char s[] = "Hola";
```
y no es necesario indicar el largo pues se deduce del texto dentro de las dobles comillas.

> En C las dobles comillas están reservadas para indicar que el dato es un string, y las comillas simples para un caracter singular (luego `"a"=='a'` es falso).
> \* Si se indica un string con doble comillas `""` se considera inmutable.

3. Se puede usar el hecho de que es un arreglo, luego se inicializa un puntero que almacene el string indicado:
```C
char *s = "Hola";
```

la variable con asterisco indica que será un **string estático**, o sea que solamente podrá leerse pero *no modificarse*.

---

Un string se puede imprimir con
```C
printf('%s', s);
```
se indica la posición con `%s` en donde irá el string a insertar `s`.
\* No se imprime el 0.

Como `s` es un puntero, se puede mover a la siguiente dirección del arreglo, cambiando el origen del string y, por lo tanto, un string distinto al inicial. Para el string anterior:
```C
s++;
printf('%s',s);
```
entregará el string `ola`.

---

Para modificar caracteres dentro de un string, primero se debe tener un string mutable. Luego, se puede reasignar el valor que almacena el puntero por otro caracter:
```C
*s = 'B'
```
en donde `*s` es el acceso al valor al que apunta el puntero `s`.

> No se puede cambiar el tamaño del string después de definirlo, este se mantiene hasta el fin del programa. Sin embargo sí se puede acortar un string adelantando el 0 final, pero se debe notar que la memoria no se libera.

---
Problema ejemplo: Contar caracteres en mayúsculas
```C
int countMayus(char *s){
	int res = 0;
	while(*s != 0){
		if('A' <= *s && *s<='Z'){
			//*s pues se quiere analizar caracter apuntado
			res++;
		}
		s++; //avanzar ptero a sig char
	}
	return res;
}
```




### Funciones de String
De la librería `<string.h>`
1. Obtener el largo de un string:
```C
int strlen(char *s);
```
`char *s` es el string al que se le calcula el largo. El número resultante no incluye el 0 final.
Ejemplo:
```C
strelen("Hola") == 4
```

\* Si se indica un string con doble comillas `""` se considera inmutable.

2. Comparar strings:
```C
int strcomp(char *s1, char *s2);
```
se comparan de forma **lexicógráfica** o sea según cuál se encuentra primero en un diccionario ASCII, entregando un número menor si se encuentra primero.
- Si `==0` $\implies$ `s1 == s2`
- `>0` $\implies$ `s1 > s2`: `s1` se encuentra después de `s2`.
- `<0` $\implies$ `s1 < s2`: `s1` se encuentra antes que `s2`.

Ejemplos:
```C
strcomp("Hola", "Hola") == 0
strcomp("Algo", "Hola") < 0
strcomp("Hola", "Algo") > 0
```
hacer `s1 == s2` **sin asterisco** es una comparación de los valores de los punteros, o seauna comparación de los números que indican la dirección de memoria que almacenan. Estas direcciones si pueden ser iguales, si se asigna en otro puntero la dirección de memoria que almacena un puntero. `char *s2 = s1;`

`strcomp()` diferencia entre mayúsculas y minúsculas, pues ASCII tiene las letras mayúsculas antes y entonces tienen un menor número que los representa en comparación a las letras minúsculas.

> Entre minúsculas y mayúsculas hay una diferencia de 32 (como número) entonces para llevar una letra a minúsculas basta sumarle 32 a su representación (y viceversa).

3. Copiar string en otro:
```C
char *strcpy(char *s1, char *s2);
```
el string `char *s1` es el string en donde se almacenará el string `char *s2`. **El de destino debe ser mutable y tener una capacidad igual o mayor que el de origen**.
\* También copia el 0 final.
\* `strcpy` es una función que retorna 1.
Ejemplo:
```C
char *s = "Hola";
char s2[strlen(s)+1];
strcpy(s2,s);
```
en donde `s2` se inicializó con el tamaño exacto de `s` pues se entrega la cantidad efectiva de caracteres con `strlen()` y se suma 1 para el espacio del 0 final.

---
Problema ejemplo: Eliminar un cierto caracter de un string tal que se deje espacio en blanco al inicio por cada caracter eliminado.
```C
void delete(char *s, char x){
	char *aux = strlen(s)-1;
	char *cpy = aux;
	while(aux>=s){
		if(*aux==x){
			aux--;
		}
		else{
			*cpy = *aux;//cambiar caract de cpy por el != de x
			cpy--;
			aux--;
		}
	}//fin 1er while
	while(cpy>=s){
		*cpy = ' ';
		cpy--;
	}//fin 2o while
	return
}
```

## Malloc
Las variables tienen un 'tiempo de vida' desde que se define hasta que se libera la memoria que utilizaba (destrucción).
```C
int fn (int x){
	int y;
	if (...){
		int z;
	}
	return;
}
```
el tiempo de vida de `x` es desde la definción de la función hasta el fin de ella; para `y` es desde la segunda línea hasta el fin de la misma función; y para `z` es solamente dentro del bloque `if()`.

Las variables comunes 'mueren' en el retorno de la función en donde se definen.
\* Todas las variables se mueren en el `return` de la función `main`.

### Variables Dinámicas
Las variables dinámicas son las que sobreviven al retorno de la función en donde se definió. Estas tienen un ciclo de vida desde que **es definida hasta que explícitamente se libera su memoria**.
Las variables dinámicas se crean utilizando `malloc()`, de la forma:
```C
void * malloc(int size);
```
en donde `void *` es un *puntero opaco* e `int size` es el tamaño de la memoria a utilizar (en Bytes).

Por ejemplo: para crear un arreglo de `int`, para almacenar 5 números:
```C
int *p = malloc(5*sizeof(int));
```
y se tiene un arreglo de memoria de 5 bloques exactos para números de tipo `int`. Las variables son
- `*p` es una variable local.
- `malloc()` indica una variable dinámica.

Otro ejemplo es
```C
char *p = malloc(20)
```
en donde se reservaron 20 Bytes de memoria, pero en este caso se *subdividen de forma diferente* por la capacidad que utiliza el tipo de dato `char`.

---

Para **liberar** el espacio de una variable dinámica, se utiliza `free()` de la forma:
```C
void free(void *ptr);
```
en donde `*ptr` es una variable que se creó con `malloc()`.

Liberar memoria tiene restricciones:
1. **Solo se puede hacer `free()` a variables que se crearon con `malloc()`**, o sea solamente se pueden liberar espacios de memoria de variables dinámicas (pues estas *sobreviven* a término de una función).
2. **Solo se puede liberar la memoria 1 vez**.
3. Siempre se libera **toda la memoria** utilizada por la variable dinámica. Esto suele suceder cuando se libera un arreglo mediante su puntero, definido como variable dinámica, y este *haya sido desplazado y ya no apunte al primer elemento del arreglo* como por ejemplo:
   ```C
   int *p = malloc(20);
   p++;
   free(p);   //error: p no apunta al 1er elem
   ```

> Si se modifica un puntero y este ya no apunta al primer elemento de un arreglo, no hay forma de liberar el espacio del arreglo.

Si no se libera la memoria utilizada antes de finalizar el programa (o sea ejecutar `return;` de `main()`), se podría llenar la memoria del PC. Por ejemplo el caso de tener un bucle que vaya reservando memoria con `malloc()`.
\*Se puede liberar matando el programa con `CTRL+C`.

##### Comando sanidad
\* Comando que revisa tareas del curso.
Este reclama cuando:
1. Pedir más memoria de la que se utiliza efectivamente en el programa.
2. Goteo de memoria (*Memory Leak*): Cuando no se libera la memoria de ua variable dinámica.

### Problemas de malloc
El uso de `malloc()` debe ser controladamente pues es propenso a errores:
1. *Memory Leak*: La memoria reservada por el programa no se liberó durante su ejecución.
   Por ejemplo usar una variable auxiliar y no liberarla al terminar su uso:
   ```C
   char *copia(char *s){
	   char *res = malloc(strlen(s) + 1);
	   char *aux = malloc(strlen(s) + 1);   //no se le hace free
	   return strcpy(res, s);
   }
   ```
   en donde se debiese hacer `free()` a `*aux` antes de retornar.

2. **Referencia Colgante (*Dangling Reference*)**: Es cuando se hacer `free` a la variable (o puntero) y este queda apuntando a bloques de memoria vacias.
   Por ejemplo,
   ```C
   char *p = malloc(20);
   ...
   free(p);
   ...
   *p      //SEGFAULT
   return;
   ```
   Si se hace `free()` un puntero y se utiliza, se va a intentar acceder a bloques de memoria vacios.
   > Para prevenir: **hacer `free()` justo antes de retornar**.
   
# Estructuras

## Typedef
`typedef` es un comando para redefinir **el nombre** de un tipo de dato, o sea se le define un 'alias'.
Se hace de la forma:
```C
typedef tipo alias;
```
luego, se puede usar el alias en vez del nombre del tipo completo,
```C
tipo x = ...
//equivalente a
alias x = ...
```


Por ejemplo, el tipo de dato `unsigened longlong` es muy largo de escribir. Se le puede dar un alias `ull` para referise a él:
```C
typedef unsigned long long ull;
```
luego, hacer ` ull=10;` $\iff$ `unsigned long long = 10;`

## Estructuras
En C no hay clases, pero se usan estructuras (`struct`) para simular el comportamiento de clases de lenguajes modernos.

Una estructura es una **unión** de múltiples variables **en un único tipo**. Se definen de la forma:
```C
struct id_estructura {
	tipo1 var1;
	tipo2 var2;
	...
}
```
y para crear una variable con la estructura anterior:
```C
struct id_estructura var_struct ={
	valor1;
	valor2;
	...
}
```
en donde `var_struct` es la variable que será del tipo `id_estructura`, y se ingresan los valores directamente en el campo en donde se señala.

Para acceder a los campos de la estructura (o las variables que tiene la estructura en su interior), se señala el nombre de la variable creada con la estructura, seguida de punto y el campo al que acceder:
```C
tipo varx = var_struct.campo
```

> La estructura creada es como un nuevo tipo de dato.

Por ejemplo,
```C
struct persona{
	int edad;
	char nom[20];
	char rut[9];
}
```
```C
struct persona P = {
	20;
	"Luis";
	"111111111";
}
```
```C
int edadP = P.edad;
char *nombreP = P.nom
```

El espacio de memoria  que ocupa la variable creada con una estructura es **a lo menos** la suma de los espacios que ocupan los campos en su interior. Esto pues puede haber espacio vacío entre memoria de los campos. En el ejemplo a anterior, el espacio que ocupa `P` (una variable con la estructura) es a lo menos la suma del espacio que ocupa su campo `P.edad`, el campo nombre `P.nom` y  el campo de su rut `P.rut`, o sea
$$
sizeof(P)\geq sizeof(edad)+sizeof(nom)+sizeof(rut)
$$ 
Luego, en C es necesario que la dirección de memoria de la variable en donde se va a guardar la variable creada con la estructura, sea un *múltiplo del tipo a guardar*.

Por lo tanto, como el espacio de memoria a usar no siempre es una suma simple de las memorias de los campos, es mejor usar `sizeof(estructura)` para indicar un espacio a reservar.

### Alias de Estructuras
El nombre de una estructura puede ser largo, entonces se le puede dar un alias para que sea más corto el código. Hay tres maneras:
1. Uso de `typedef` usual,
   ```C
   typedef struct id_estructura alias_estructura;
   ```

2. Asignar `typedef` en la misma definición de la estructura,
   ```C
   typedef [struct id_estructura{
	   //definicion estructura
	}] alias_estruct;
   ```
   lo que permite hacer `struct persona P` $\iff$ `pers P` 

3. Sin indicar el nombre de la estructura, solamente la definición (o plantilla)
   ```C
   typedef struct{
	   //plantilla
   } alias;
   ```
   y después se puede hacer `alias varStruct = {20, "Luis", "11..."}`

## Ámbito de Variable

En el lenguaje C se tienen distintos ámbitos en donde viven las variables creadas, lo que no siempre se cumple que al modificar una variable en una función, modifica el valor esperado, si no que se puede modificar una *copia* que hace C cuando se ingresa el valor en una función.
Por ejemplo,
```C
typed struct{
	double r;
	double im;
} Complejo;
```
```C
void suma(Complejo x, Complejo y){
	x.r += y.r;
	x.im += y.im;
}
```
```C
int main(){
	Complejo x = {1, 20};
	Compleyo y = {-2, 3};
	suma (x,y);
	return;
}
```
en donde en la función `main` , la invocación de `suma(x,y)` **no cambia el valor de `x` o `y`** pues `suma` usa una *réplica* de ambos como variables locales solamente para aquella función; No se están modificando las variables `x`,`y` que se encuentran en `main()`.

Para modificar efectivamente la variable, se deben entregar **punteros** a las variables que se buscan cambiar. Así, se debe cambiar también la definición de la función `suma` tal que utilice punteros.
```C
typed struct{
	double r;
	double im;
} Complejo;
```
```C
void suma(Complejo *px, Complejo y){
	(*px).r += y.r;
	(*px).im += y.im;
}
```
en `(*px)` se está accediendo al valor de `x`, y luego a su campo `r`.
```C
int main(){
	Complejo x = {1, 20};
	Compleyo y = {-2, 3};
	suma (&x,y);
	return 0;
}
```
finalmente, a `suma` se le debe entregar la dirección de memoria de `x` pues esta funciona son puntero a la dirección de memoria en donde se encuentra `x`. Así se modifica efectivamente `x` pues se está cambiando la 'variable que vive en esa dirección de emoria'

> Cuando se quiere modificar una variable en otro ámbito, se debe entregar la dirección de memoria de la variable a la función que va a modificarla, para que 'vea' la variable real.

Para acceder al campo de un puntero que contiene la dirección de memoria de una variable definida según una estructura, se puede ser más conciso con
```C
(*px).campo
```
es equivalente a hacer
```C
px -> r
```
que significa que `px` es un puntero que apunta a una variable con el campo `r`, y se está accediendo a tal campo.

## Estructura Recursiva
Una estructura es recursiva cuanndo uno o más campos de la estructura se definen como un tipo de dato de su misma estructura.
> En este caso **se debe tener el nombre de la estructura** para que el campo pueda ver la misma estructura en la que se encuentra.

Por ejemplo, se puede implementar una lista enlazada, tal que cada nodo es una estructura que incluye un  dato y un puntero al siguiente nodo. Pero para que el puntero pueda ser definido, se debe indicar que apuntará a una variable del tipo de la misma estructura.
```C
typedef struct nodo{
	int x;
	struct nodo *prox;
} Nodo;
```

luego una lista enlazada se puede inicializar como
```C
Nodo a = {1, NULL};
Nodo b = {2, &a};
Nodo c = {3, &b};
```
en donde se entregan las direcciones de memoria de los nodos siguientes para almacenarlos en el puntero; además el nodo `a` apunta a un nodo `NULL` (o vacío) marcando el final de la lista enlazada.
