
Es una lista en donde, en lugar de que a cada elemento se le asigna un índice de posición, se le asigna una palabra denominada *clave*.


|             | 'valor1' | 'valor1' | ... | 'elementoN' |
| ----------- | -------- | -------- | --- | ----------- |
| Lista       | `0`      | `1`      | ... | `N`         |
| Diccionario | 'clave1' | 'clave2' | ... | 'claveN'    |
Ya no se usa un número para acceder a un elemento, si no que se usa *una palabra clave*.

**Sintaxis**
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

