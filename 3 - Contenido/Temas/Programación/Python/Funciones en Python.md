## Crear Funciones
\* Se recomienda seguir la [[Receta de Diseño]].
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

##### Errores comunes
Un error común es intentar guardar en una variable el resultado del retorno de la función. Se estaría guardando None en una variable y si se usa `print()` con la variables, se mostraría None.

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

# Funciones siempre disponibles
 Hay funciones que están siempre disponibles para programas en python (no es necesario invocar un módulo para usarlas). 

| Función        | Efecto                                                      | Ejemplo             | Resultado |
| -------------- | ----------------------------------------------------------- | ------------------- | --------- |
| `abs(x)`       | $\|x\|$, valor absoluto de $x$                              | `abs(-7)`           | `7`       |
| `max(x,y,...)` | Máximo valor entre todos los valores ingresados.            | `max(4,3,-2,8)`     | `8`       |
| `min(x,y,...)` | Mínimo entre todos los valores ingresados.                  | `min(4,3,-2,8)`     | `-2`      |
| `round(x,z)`   | Aproxima un número decimal $x$ dejándolo con $z$ decimales. | `round(2.73545, 2)` | `2.74`    |
