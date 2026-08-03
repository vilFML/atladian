# Funciones Predefinidas
 Hay funciones que están siempre disponibles para programas en Python (no es necesario invocar un módulo para usarlas). 
```python
import math
a=3
b=4
c=math.sqrt(a**2+b**2)
print(c)
```
    5.0

## Input
Para tener un programa interactivo y que éste no sea siempre predefinido, o evitar modificar las declaraciones de las variables en el código siempre que se busque realizar un cálculo con diferentes valores.

La función `input()` permite que al ejecutar un programa, se pueda pedir al usuario que ingrese un valor para almacenarlos en una variable y procesarlo posteriormente.
- Se puede mostrar un mensaje al usuario que ejecuta el código de la forma: `input('Ingrese un numero: ')`.

Para uso:
```py
n = input('Ingrese un numero: ')
```
en donde 'n' será la variable en la que se almacenará el valor ingresado mediante la función input.

**Todo lo que la función input recibe, es de tipo string.** Para el caso de procesos numéricos es necesario convertir el tipo de dato a lo que se requiera usar (int, float, etc.)

## Print
Para mostrar usuario resultados intermedios o dentro del proceso del programa, se usa `print()`.
Dentro del paréntesis se indica lo que se desea mostrar: Se puede indicar una variable o un dato directamente:
```py
n = 11
print(n)
```
```py
print('ejemplo')
```

Usos de `print()`:
1. Para mostrar sólamente strings se pueden concatenar y siguiendo lo aprendido en la concatenación de strings: Solamente se puede hacer concatenación entre strings, por lo que los datos numéricos deben convertirse a tipo string y luego concatenar con '+' usualmente.
```py
n = 11
n2 = n * 2 + 7
print(n)
print('El valor de n2 es ' + str(n2))
```
\* se muestran dos valores diferentes con dos funciones print diferentes

2. Uso con comas `,`
   Otra forma es separar los datos mediante el uso de comas, así no se están concatenando strings y no es necesario convertir los datos. Se puede tener el mismo efecto de concatenación:
```py
nombre = 'Dante'
edad = 3
print('Mi perro se llama', nombre, 'y tiene', edad, 'años.' )
```
\* se agregan espacios en la comillas automáticamente.

3. Usar f-strings:
   se llaman también strings fromateados y es una nueva forma de crear texto en python, facilitando el uso de variables al interior de cadenas de texto.
   Se agrega `f` antes de la comilla en el inicio de un string: `f'string formateado` y es posible ingresar variables en su interior, indicando el nombre de la variable entre llaves `{}`, quedando:
```py
nombre = 'Dante'
edad = 3
print(f'Mi perro se llama {nombre} y tiene {edad} años.')
```
usar f-string es mejor cuando se tienen múltiples variables y el código es más legible.

## Otras funciones

| Función        | Efecto                                                      | Ejemplo             | Resultado |
| -------------- | ----------------------------------------------------------- | ------------------- | --------- |
| `abs(x)`       | $\|x\|$, valor absoluto de $x$                              | `abs(-7)`           | `7`       |
| `max(x,y,...)` | Máximo valor entre todos los valores ingresados.            | `max(4,3,-2,8)`     | `8`       |
| `min(x,y,...)` | Mínimo entre todos los valores ingresados.                  | `min(4,3,-2,8)`     | `-2`      |
| `round(x,z)`   | Aproxima un número decimal $x$ dejándolo con $z$ decimales. | `round(2.73545, 2)` | `2.74`    |


# Funciones Propias
El usuario puede definir sus propias funciones:

```python
def hipotenusa(a,b):
    import math
    c=math.sqrt(a**2+b**2)
    return c
print(hipotenusa(3,4))
```

    5.0

\* Se recomienda seguir la [[#^0deee8|Receta de Diseño]].
Para crear una [[Funciones|función]] se usa la palabra reservada **def**, seguida del nombre que se le asignará a la función:
```py
def nombreDeFuncion(parametro1,parametro2):
	#istruccion1
	#instruccion2
	#...
	return salida
```
- Las instrucciones dentro de la función deben estar *indentadas.* Las indentaciones deben ser consistentes (de a 4 o 2, pero todas iguales).

Para usar (invocar) funciones se escribe el nombre de la función y entre paréntesis los argumentos o parámetros que se quieren entregar a la función. De la forma:
```py
resultado1 = nombreDeFuncion(47,'perro')
resultado2 = nombreDeFuncion(12,'gato')
```

1. Los parámetros son variables internas de la función que almacenarán los valores con los que se invoca la función.
2. Cuando se ejecuta la línea de return en una función, no se ejecutan las siguientes lineas indentadas y se termina le ejecución de la función. **Y todos los parámetros y variables usados al interior de una función desaparecen.**

### Funciones sin Argumentos
Hay funciones que pueden no recibir argumentos y aún así retornar un valor.
- En el contrato se indica que recibe *None* por la ausencia de un valor.
- No se ingresa un argumento entonces al invocar la función se colocan solamente los paréntesis sin un valor dentro.

*Ej*
```py
# numeroMagico: None -> int
# funcion que solamente retorna el numero 42
# Ej: numeroMagico() retorna 42

def numeroMagico():
    return 42

assert numeroMagico() == 42

```

### Funciones sin Retorno
Las funciones también pueden no retornar un valor a donde es invoca y, en cambio, realizar un proceso. Es típico en funciones que muestran mensajes con `print()` en su interior.
- Cuando las funciones no tienen explícitamente la instrucción de `return`, python implícitamente declara que la función retorna *None*.
- De todas formas, en el contrato se indica como salida *None*. Y no se entrega ejemplo.
- No se pueden testear ya que retornan None.


```py
# saludoMundo: None -> None
# muestra en la pantalla un saludo hacia el mundo.
#SIN EJEMPLO

def saludoMundo():
	print('Hola Mundo!')
	print('Espero esten bien')

#SIN TESTS
```

### Funciones sin Retorno pero con Argumento
```py
# mostrarSuma: num, num -> None
# muestra en pantalla la suma de dos numeros
# Sin Ejemplo
def mostrarSuma(n1, n2):
	print(f'La suma de {n1} y {n2} es: {n1+n2}

# Sin tests
```

\* Un error común es intentar guardar en una variable el resultado del retorno de la función. Se estaría guardando None en una variable y si se usa `print()` con la variables, se mostraría None.

### Funciones que retornan y muestran
También es posible que una función utilice `print()` y además que retorne un valor.
- Es importante que la instrucción de `return` no esté antes de la función `print()`, ya que si no, la función saldrá antes de mostrar el resultado.
```py
# retornarSuma: num, num -> num
# muestra la suma de los numeros y además la devuelve.
# EJ: retornarSuma(3,4) retorna 7

def retornarSuma(n1,n2):
	print(f'La suma de {n1} y {n2} es: {n1+n2}')
	return n1 + n2

# tests
assert retornarSuma(3,4) == 7
assert retornarSuma(-1,2) == 1
```


### Funciones Interactivas
Se puede encapsular la lógica de interactuar con el usuario mediante `input()` y `print()` en una función.
No reciben parámetros ya que adquieren los datos a través de `input()` desde el usuario. Y tampoco retornan valores pues muestran mensajes con `print()`.
```py
# programaInteractivo: None -> None
# funcion que pide dos numeros al usuario y muestra la suma y resta
# Ej: sin ejemplo
def programaInteractivo():
	primerNum = int(input('Ingresar el primer numero: '))
	segundoNum = int(input('Ingresar el segundo numero: '))
	
	print(f'La suma de {primerNum} y {segundoNum} es: {suma(primerNum, segundoNum)}')
	print(f'La resta de {primerNum} y {segundoNum} es: {resta(primerNum, segundoNum)}')
	return None

```
\* No es necesario agregar que se retorna None, si no se hace, Python lo hace de forma implícita.

## Recursión de Funciones
Una función puede invocar otras funciones que hayan sido definidas previamente.


# Receta de Diseño

^0deee8

Es una receta o guía para escribir funciones correctamente. Ayuda a extraer la información importante de un problema, entenderlo y tener un orden al momento de programar una función.
Entrega la información de:
1. Entender el propósito de la función (Para qué sirve)
2. Dar ejemplos de uso de la función (Cómo se usa)
3. Probar/verificar la función (Demostrar que sirve)
4. Especificar el cuerpo de la función.

*Ejemplo*: Se va a definir una función para obtener el área de un rectángulo.
```py
# areaRectangulo: num, num -> num
# calcula el área de un rectángulo de lados 'largo' y 'ancho'
# ejemplo: areaRectangulo(7,2) devuelve 14

def areaRectangulo(largo,ancho)
	return largo * ancho
	
# tests
assert areaRectangulo(7,2) == 14
assert areaRectangulo(3,5) == 15
```

se tienen los siguientes elementos según las lineas:
1. La linea 1 es el **contrato**: Se especifica el *nombre* de la función, con los *tipos que recibe y los que retorna*.
   \* indicar el tipo 'num' se refiere a que se recibe cualquiera de int o float (un dato numérico cualquiera).
2. La **descripción:** Corresponde a una explicación breve de lo que hace la función; breve, simple y conciso.
   Esto ayuda a quien lea el código a saber qué hace la función sin leer la implementación.
3. Ejemplo de uso: Especifica cómo se invoca la función de forma concreta y qué se espera que retorne, o el efecto que produce la función.
4. **Firma o Encabezado** de una función: Representa en código cómo debe escribirse la función.
   Inicia con *def*, lleva el nombre representativo de la función, dentro de paréntesis se indican los parámetros que recibe la función (separados por comas ','), finaliza con ':'.
5. **Cuerpo** de la función: Es el bloque de instrucciones que está encapsulado en la función. Deben estar indentadas un nivel hacia la derecha con respecto a la firma de la función.
6. **Testing** de la función: Corresponden a la verificación formal de la implementación de la función. O sea se comprueba con código ejecutable que la función retorna lo que se espera. Lo ideal es probar los casos límites.

### Sobre los Test
Se usa la palabra clave **assert** para verificar y afirmar la validez de una expresión que se indica a su derecha.
En el ejemplo: `assert areaRectangulo(7,2) == 14` se está **afirmando** que: Si se ingresa como parámetro de largo y ancho 7 y 2 respectivamente, entonces la salida de la función será si o si igual a 14.

Un fallo ('AssertionError') sucede cuando la afirmación no se cumple. *Una posible estrategia para enfrentar un error de assertion es reemplazar el assert por un print para mostrar qué entrega la función.*
