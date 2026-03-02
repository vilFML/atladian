# Expresiones
Las expresiones son valores que interactúan entre sí usando **operadores**. Producen un nuevo valor al evaluarse:
```py
2+3
```

```py
5*7
```

```py
'hola'+' '+'mundo'
```

```py
7>5
```

En cada una de las expresiones, python evalúa los valores y operadores para generar un nuevo valor como resultado.

## Expresiones existentes
**Positivo**: convierte el valor entregado a positivo
```py
+7
```
```py
+2.5
```

**Negativo**: convierte el valor entregado a negativo
```py
-7
```
```py
--2.5
```

**Suma**
```py
7+11
```
```py
7.5+10
```

**Resta**
```py
7-11
```
```py
-2.5+5.2
```

**Multiplicación**
```py
3*5
```

**División**
```py
5/2
```

**Potencia**
```py
3**5
```

**Potencia para raíces**
```py
4**0.5
```

**División Entera**
Entrega el resto entero de una división.
```py
5//2
```

**Resto o módulo**
Entrega el resto de una división entre dos valores:
```py
5%2
```
```py
5%2.7
```

## Tipo del Resultado
El tipo de dato que resulta de una expresión depende del tipo de los valores que se operan. *En general*, si existe al menos un valor con tipo float, entonces el resultado será de tipo float.

```py
1+2
```
```py
1+2.0
```
```py
1.0+2
```
```py
1.0+2.0
```

**Para la división**, lo anterior no se cumple. El tipo del resultado de una división **siempre es un float.**
```py
4/2
```
```py
4/2.0
```
```py
4.0/2
```
```py
4.0/2.0
```

## Prioridad entre operadores
En general, se siguen las mismas reglas del álgebra.

| Prioridad | Operador                                            | Signo                            |
| --------- | --------------------------------------------------- | -------------------------------- |
| Mayor     | Exponenciación                                      | `**`                             |
|           | Operadores positivo y negativo                      | `+x`, `-x`                       |
|           | Multiplicación, División, División Entera y Módulo. | `*`, `/`, `//`, `%`              |
|           | Adición y Substracción                              | `+`, `-`                         |
|           | Comparadores booleanos                              | `==`, `!=`, `<`, `<=`, `>`, `>=` |
|           | Booleano *Not*                                      | `not`                            |
|           | Booleano *and*                                      | `and`                            |
| Menor     | Booleano *or*                                       | `or`                             |

- En caso de que se tengan dos operadores de igual prioridad, se evalúa de izquierda a derecha:
```py
10+8/4*2
```

- Se pueden poner paréntesis para que se tenga mayor prioridad para una expresión
```py
3 + ((2 * 5) / 8)
```
```py
(3 + 2) * (5 / 8)
```

## Operaciones con String
**Concatenar Strings**: Para juntar dos textos se usa el operador **+**
```py
"los pollitos dicen" + " " + "pio pio pio"
```
en donde entre los operadores se incluyó un espacio.
```py
'10' + '7'
```
el resultado en este caso fue el `'107'` que corresponde a un string (está entre comillas).

**Repetir string**: Usando la analogía de que concatenar es sumar los strings, se puede multiplicar un string para repetirlo cuantas veces se indica.
```py
"hola" * 4
```

**Mezclar números con strings**: Python no sabe interpretar las expresiones con strings e ints.
```py
"yo tengo " + 5 + " perros."
```
para ello, el int (o float) se debe convertir a string usando la correspondiente función para convertir a tipo string `str()`
```py
"yo tengo " + str(5) + " perros."
```
