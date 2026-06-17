Los diagramas de estado son una forma de visualizar la implementación de un algoritmo gráficamente.

Se busca una función que cuente cuántas palabras tiene un string.
- Se inicia con el primer caracter (en posición `0`) y se crea un contador para almacenar cuántas palabras se tienen.
- El índice puede estar en cualquiera de las letras de la palabra y sigue siendo la misma palabra.
- El índice también puede estar en un espacio. Así el **índice tiene dos estados posibles**. 
Lo anterior se puede ilustrar de la forma:
![[Pasted image 20260429093339.png]]

- El índice se inicia en `0`, pero todavía no se ha visto el primer caracter: **Se encuentra fuera**: Loop en estado 'Fuera' sin aumentar `np`

y luego, se ven los casos posibles: 
- ¿Qué pasa si se tiene un espacio en el inicio? en este caso, *el índice sigue fuera*, representado como un loop en el estado Fuera.
- Si se encuentra un caracter (`s[k] != ' '`) se avanza en el contador: `np += 1`, *el índice pasa al estado 'Dentro'*, representado con la flecha que va desde 'Fuera' hasta 'Dentro'.

Dentro de una palabra, si se sigue en un caracter, se sigue en el estado 'Dentro', pero sin aumentar `np`, *se representa como un lazo en 'Dentro', pero sin aumentar el contador `np`*.
Cuando se está en el estado 'Dentro', si se encuentra un espacio, se pasa al estado 'Fuera': flecha desde 'Dentro' a 'Fuera'.
El proceso completo está activo mientras $k$ esté dentro del rango del largo. Entonces cuando $k$ llega al largo del string, se pasa al estado 'Fin', representado con la flecha hasta 'Fin'.

\* Para la implementación, se puede ver que en la versión iterativa se realiza el proceso mientras $k$ no sea igual a la longitud del string. Esto se encuentra en la condición principal del ciclo: `while (k ! = len(s))`


### Ejemplo: Camel Case
Se le llama "Camel Case" a la convención de escribir una frase sin espacios, pero marcando el inicio de cada palabra poniendo su primera letra en mayúscula.
Por ejemplo, la frase
```py
" Algoritmos y estructuras de datos "
```
transformada a Camel Case queda así:
```py
"AlgoritmosYEstructurasDeDatos"
```

Implementación:
--
usando diagramas de estado:
-  **OUT**: 
   1. El algoritmo entra$i=0$, y el string final es vacío, `sFin = ' '`
   2. Se sigue estando en *out* si la letra del string es un espacio: `if (s[i]==' ')` y se debe aumentar $i$ para pasar a la siguiente posición (caracter) del string.
- **IN**:
  1. Si el caracter actual es distinto a un espacio, se lleva a mayúsculas con `s[i].upper()` y se agrega al string final.
  2. Se mantiene *in* si se tiene caracter distinto de espacio, pero solamente se agregan los caracteres sin llevar a mayúscula.
- **END**: Se termina el ciclo cuando se acaban los caracteres del string. Esto sucede cuando `i=len(s)`

```py
def CamelCase(s):
	n = len(s)
	
	#OUT: inicio i = 0, sFin = ''
	i = 0
	sFin = ''
	
	while (i < n):
		if (s[i] == ' '):
			i += 1
	
	#IN
		else:
			sFin += s[i].upper()
			i += 1
			
			while (s[i] != ' ' and i < n):
				sFin += s[i]
				i += 1
				
	return sFin
```
