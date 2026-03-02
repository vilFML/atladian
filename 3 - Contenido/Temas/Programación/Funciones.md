Al desarrollar código se puede tener repeticiones de lineas de código: Se 'copian y pegan' bloques de código en diferentes partes del programa. Esto trae dificultad para realizar cambios en el programa: para cambiar algo en todos los bloques idénticos de código, se debe modificar uno por uno; además no permite escalar la solución: Para realizar un proceso una gran cantidad de veces, se requiere repetir tantas veces el código como sea necesario.
Para solucionar esto se hace uso de **funciones.**

*Las funciones son bloques reutilizables de códigos, encapsulados bajo un cierto nombre y que realizan un proceso específico.*
1. Reciben datos de entrada: **Parámetros o argumento**
2. Se procesan los datos de entrada.
3. Se retorna un resultado de salida.

$$
\underbrace{ x,y,z,\dots }_{ \text{Argumentos/parametros} } \to \text{func } f \to\underbrace{ \text{resultado}=f(x,y,z,\dots) }_{ \text{Salida} }
$$