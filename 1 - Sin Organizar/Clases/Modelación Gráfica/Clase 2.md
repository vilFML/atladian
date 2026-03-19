Computación gráfica: Generación de imágenes desde escenas computacionales

- escena computaional:  la representaicón geométrica (2D o 3D)
- Generación de img: el rendering, superposición de img por segundo en la pantalla (60HZ = 60 img por segundo)

**Objetivo**:
- La modelación de un mundo con computador, en donde el mundo tiene sus propias reglas. También este pueden ser modelos físicos lo suficientemente detallado.

##  Rendering
Tiene más costo computacional según el nivel de detalle (ej: resolución de objetos) 
Se va a enfocar en el rendering 


## Componentes
Típicamente hay 3 ejes a considerar: El modelo, la escena y el rendering

### Modelo
Corresponde a las geometrías que se quieren representar: Los objetos, el piso en donde se apoyan

### Escena
Las transformaciones que se le aplican a los objetos
- De movimiento: Que el objeto se mueva.
- Escalamiento: Cambiar el tamaño del objeto.

Y también se tienen las vistas, en donde se ubica la cámara y por lo tanto modficar la perspectiva.

### Realismo
Es la parte de iluminación de la escena y las físicas del mundo (como la gravedad, o las reglas de interacciones entre ellos como choques).

## Aplicaciones
La modelación gráfica tiene las aplicaciones:
1. Videojuegos: Aplicaciones de rendering en tiempo real más conocido y popular. Pueden intentar simular el mundo físico lo más fielmente posible o  
2. Animaciones
3. Rendering no Fotorealista (Cell-shading): Tomar los vectores normales a la superficie y  asignarles un color, esto puede usarse para renderizar imágenes caricaturescas.
4. Medicina: Renderizar partes del cuerpo.
5. CAD (Computer assisted design): Que se utiliza para fabricar piezas, diseñar estructuras, etc.q