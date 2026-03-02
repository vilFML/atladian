
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
