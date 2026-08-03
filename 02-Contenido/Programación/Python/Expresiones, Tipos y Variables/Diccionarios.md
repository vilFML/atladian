Un diccionario es similar a una lista, pero a cada elemento se le asigna (se indexa) con datos no necesariamente numéricos, llamada *clave*.

|             | 'valor1' | 'valor1' | ... | 'elementoN' |
| ----------- | -------- | -------- | --- | ----------- |
| Lista       | `0`      | `1`      | ... | `N`         |
| Diccionario | 'clave1' | 'clave2' | ... | 'claveN'    |

Ya no se usa un número para acceder a un elemento, si no que se usa *una palabra clave*.


## Creación
Para crear un diccionario, se declara similar a una lista, pero con `{}`, indicando la palabra clave y su valor, separados por `:`, de la forma:
```py
Diccionario = {'clave1':valor1, 'clave2':valor2,  ... , 'claveN':valorN
```

Los valores pueden ser de cualquier tipo, específicamente, pueden ser una lista:
```py
Diccionario = {'clave1':[1,70,'perro']}


#y para acceder
valorEnLista = Diccionario['clave1'][indice]}
```

## Acceder
Para acceder a un valor, se hace de la forma:
```py
datoX = Diccionario['claveX']
```

## Ejemplo

Por ejemplo, supongamos que queremos convertir "piedra", "papel" y "tijera" a una representación numérica 0, 1, 2, respectivamente:
```python
p_a_n = {"piedra":0, "papel":1, "tijera":2} # para convertir de palabra a número
print(p_a_n["papel"])
```
    1
La conversión inversa se puede hacer simplemente con una lista:
```python
n_a_p = ["piedra", "papel", "tijera"] # para convertir de número a palabra
print(n_a_p[1])
```
    papel
Con esto podemos hacer una función en que el programa juegue "cachipún" contra el usuario:
```python
def juega():
    from random import randint
    programa=randint(0,2)
    usuario=p_a_n[input("¿piedra, papel o tijera? ")]
    resultado="Empate" if programa==usuario else\
        "Gana Usuario" if (programa+1)%3==usuario else "Gana Programa"
    print("Usuario juega", n_a_p[usuario])
    print("Programa juega", n_a_p[programa])
    print("Resultado:", resultado)
```
```python
juega()
```
    ¿piedra, papel o tijera? tijera
    Usuario juega tijera
    Programa juega tijera
    Resultado: Empate
