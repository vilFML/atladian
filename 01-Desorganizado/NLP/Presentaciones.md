# Apuntes presentaciones

## I. Traducción Automática con RNN y Atención

Machine Translation (MT) es el uso de computadoras para traducir texto de un idioma a otro, modelado como una tarea de secuencia a secuencia (sequence-to-sequence) pues, para una secuencia de palabras en un idioma, sale una secuencia de palabras en otro idioma.

No basta con traducir por palabra pues la entrada y la salida pueden tener diferencias en:
- La longitudes de las oraciones.
- El orden de palabras (sujeto-objeto-verbo).

### Encoder-Decoder

1. **Codificador (Encoder)**: Lee la oración fuente por palabra, pasándolas a una serie de estados ocultos.
   El último estado resume la información de la oración.
2. **Decodificacor (Decoder)**: Usa la información del último estado para generar la traducción.
   Genera las palabras de a una, condicionada a las anteriores ya generadas.

### Atención

El almacenamiento en el último estado oculto trae un problema para oraciones muy largas, pues se puede perder información, especialmente en el inicio de ella. Así, surge el mecanismo de **atención** que permite al decodificador saber qué partes de la oración de entrada son importantes.

La atención es tal que, en vez de usar solamente el vector final, el decodificador observa **todos los estados ocultos** y les **asigna pesos distintos** según la relevancia para la palabra que va a generar.
- La atención se reajusta dinámicamente a medida que el decodificador genera cada palabra.
- La atención tiene un buen efecto secundario, el cual le permite al modelo alinear palabras entre los dos idiomas, en caso de una diferencia en el orden de los componentes.

Al observar los pesos de atención, se puede ver qué palabras mira el modelo en cada paso.

#### Funcionamiento
1. **Puntaje**: Compara el estado del decodificador con cada estado del codificador.
2. **Softmax**: Convierte los puntajes en pesos $\alpha$ que suman 1.
3. **Promedio Ponderado**: El nuevo contexto mezcla todos los estados según sus pesos.

#### Ejemplo
El modelo lleva generado "el gato" y al generar "negro", el modelo le da 0.80 de peso a "black".

|            | The  | black | cat  | sleeps |
| ---------- | ---- | ----- | ---- | ------ |
| **El**     | 0.82 | 0.06  | 0.08 | 0.04   |
| **gato**   | 0.05 | 0.12  | 0.78 | 0.05   |
| **negro**  | 0.04 | 0.80  | 0.12 | 0.04   |
| **duerme** | 0.03 | 0.04  | 0.10 | 0.83   |
cada fila muestra a qué palabra se le puso atención (e.g. asignar mayor peso) al generar la palabra en español.
- Al generar "gato", el modelo le toma una mayor atención a "cat".

**El modelo aprende por sí solo a reordenar.**

---

# II. Transformers

En lenguaje natural, el significado de un token depende de su contexto, esto es, las palabras (o tokens) a su alrededor.
Modelos como RNN o LSTM procesan la secuencia paso a paso, lo que dificulta la relación entre tokens alejados.

La idea de transformers es permitir que cada token acceda directamente a la información relevante del resto de la secuencia. Luego, como no se depende del paso anterior, **todas las posiciones se procesan en paralelo**, haciendo posible el entrenamiento con una gran cantidad de parámetros en GPU/TPU.

## Self-attention
Para entender una palabra en una oración, no todas las demás tienen la misma relevancia. Self-attention permite que cada token observe al resto de tokens, para ver su relevancia.

## Multi-Head Self-attention
No basta con una sola cabeza de atención pues esta aprende solamente un patrón de relación. Pero en el lenguaje se tienen más relaciones, como sintaxis, correferencia o posición. 

### Arquitectura Transformer
Se compone de
1. Capa de codificador
2. Capa de decodificador
3. Embeddings 
4. Multi-Head Self-Attention
5. Red Feed Forward
6. Proyección de salida

### Encoder vs Decoder
- Encoder: Atención bidireccional, cada token observa toda la secuencia
- Decoder: Atención casual, el token solo puede ver los anteriores. Para predecir el siguiente, añade cross-attention sobre la salida del codificador.

---

# III. Modelos Pre-entrenados

Un mismo modelo sirve para múltiples tareas de lenguaje. El proceso de entrenamiento se repita muchas veces, tal que:
1. Se entrega el corpus de texto
2. Tokenización y Embeddings
3. Modelo Neuronal, procesa el contexto y produce predicciones
4. Pérdida y actualización de parámetros, compara la predicción hecha (con el objetivo) y aprende para corregir.

Se usan transformers para hacer entrenamiento paralelo y construir una representación contextualizada, con dos enfoques:
1. **BERT**: El modelo aprende a recuperar el token oculto utilizando el contexto de ambos lados.
2. **GPT**: El modelo predice el siguiente token utilizando el contexto anterior y continúa generando.

### Tarea Específica
Para que el modelo pre-entrenado realice una tarea en específico, se hace un **fine-tuning**: Se actualizan parámetros con datos de una tarea concreta.

---

# IV. Adaptación de Modelos

La idea es reutilizar el conocimiento adquirido durante el preentrenamiento para nuevas tareas. Así, se aprovecha el conocimiento anterior y se puede mejorar el rendimiento para tales tareas, además de reducir el tiempo de desarrollo. Pero el resultado, de todas maneras depende de la calidad el modelo original.
### Fine-Tuning

Es continuar el entrenamiento de un modelo pre-entrenado con datos de la tarea nueva. Se ajustan sus parámetros para adaptarlo a la nueva temática.

#### Parameter-Efficient Fine-Tuning (PEFT)

Familia de técnicas de adaptación que actualiza una pequeña parte de los parámetros (o incorpora adicionales).
Congela la mayor parte del modelo y reduce los parámetros entrenables.

#### Low-Rank Adaptation: LoRA

Adapta un modelo pre-entrenado introduciendo matrices de bajo rango, entrenables, manteniendo congelados los pesos originales.

$$
W = W_{0} + A\cdot B
$$
en donde,
- $W_{0}$ es la matriz original, congelada
- $A,B$ son las adicionales entrenables
### Prompting

El modelo aprende un conjunto de prompts entrenables mientras mantiene sin cambios los parámetros originales del modelo.

### Retrieval-Augmented Generation RAG

Es un proceso en donde se combina un modelo de lenguaje con un sistema de recuperación de información externa; se incorporan documentos relevantes al contexto antes de generar la respuesta.
Se pretende aumentar la especificidad del dominio.

---

# V. LLM Fundamentals

El objetivo es tomar un predictor de texto y llevarlo a un sistema de asistencia útil y seguro.

## 1. Preparación de Datos

Se debe tener una gran cantidad de datos que representen el conocimiento humano, desde fuentes como páginas web, libros, repositorios de código, papers científicos, etc. Estos datos se preparan tal que:
- Se filtran los datos de baja calidad o irrelevantes.
- Se eliminan los datos duplicados.
- Se saca la información personal.

## 2. Pre-entrenamiento

El mecanismo de aprendizaje es una predicción del siguiente token con entrenamiento auto-regresivo. Esto es, que se corrija a sí mismo, dado un objetivo.

El pre-entrenamiento requiere muchos recursos debido al escalamiento del modelo: La capacidad del modelo aumenta con la cantidad de cómputo, datos y parámetros.
\* Alto costo de entrenamiento (de cómputo y ambientales) entregan modelos de alta capacidad.

No obstante, el modelo está entrenado en base a las fuentes, lo que no siempre garantiza que sea útil en otras tareas. Por ello, se introduce el Post-Training o Alineamiento.

## Supervised Fine-Tuning (SFT)
Se busca enseñarle al modelo el formato y estilo adecuado de interacción, por ejemplo:
Para un prompt que pida resumir el texto, el modelo debiese responder en un estilo similar: "Aquí hay un resumen ...". Para ello, son necesarias instrucciones dadas por humanos.

## Reward Modeling

Se basa en que es más sencillo para un humano analizar que escribir una buena respuesta.
Por ello, se entregan dos alternativas de respuestas y se hace elegir al usuario por la que considere mejor, refinando el post-entrenamiento del modelo.

## Evaluación de Modelos
La evaluación no es siempre con respecto a una sola tarea, si no que pueden ser a varias, por ello no hay una medición única que indique calidad de respuesta.
Hay de varios tipos:
- Mediciones académicas, como pruebas automatizadas de cómputo.
- Evaluaciones de Seguridad: Análisis de toxicidad o de respuestas con contenido potencialmente violento.
- Preferencia humana: Supone la mejor comparativa para trabajar en una interacción con humanos.

---

# VI. Prompt Engineering
Cómo utilizar el conocimiento para una tarea específica.

Prompt Engineering consiste en el diseño de las instrucciones y contexto que se le entregan a un modelo, para guiarlo a un resultado deseado. Tal que los aspectos involucrados no queden a interpretación del modelo y la tarea y salidas queden bien definidas.

> Un buen prompt reduce la ambigüedad sobre qué hacer, con qué información y cómo responder.
## Diseño

Cinco elementos que debiese tener un buen prompt:
1. Tarea: Qué se quiere que haga el modelo.
2. Contexto: Información necesaria para resolver la tarea.
3. Ejemplos: Mostrar el comportamiento que se espera en la salida.
4. Restricciones: Condiciones que debe respetar el modelo.
5. Formato de salida: Cómo se quiere recibir la respuesta.

## Limitaciones

Los modelos son sensibles a la redacción del prompt, o sea que pequeños cambios en una instrucción pueden producir respuestas distintas y un buen prompt no garantiza una respuesta correcta (como una salida con errores o alucinaciones) y un buen prompt para un modelo puede no serlo para otro.

---

# VII. RAG

RAG es una técnica que combina un modelo de lenguaje (LLM) co un sistema de búsqueda de texto sobre fuentes de información, en donde las fuentes pueden (o no) ser parte del entrenamiento previo del modelo.

## Funcionamiento

### 1. Indexación

 Se entregan los documentos al modelo, este lo lleva a fragmentos más pequeños y realiza el proceso de embedding para él.
 1. Se entrega el documento.
 2. Fragmenta en chunks.
 3. Obtiene los vectores de significado.
 4. Realiza el procesamiento de la base vectorial.

### 2. Recuperación y Generación

Un usuario realiza una consulta y el modelo hace una búsqueda en su base vectorial según el prompt. Con ello, el modelo genera la respuesta agregando las fuentes.

## Aplicaciones

Tiene usos en modelos de atención al cliente, en motores de búsqueda o en tareas de dominios más delicados, como medicina o asistencia jurídica, que requieren de información contextual mucho más específica. 

## Ventajas y Limitaciones

El modelo obtiene información actualizada más frecuentemente, o más acorde al contexto que indica el usuario, lo que reduce la imprecisión y la probabilidad de que el modelo utilice hechos inexistentes.
A pesar de ello, no elimina completamente las alucinaciones y además introduce más latencia y costo computacional; Además que añadir contexto tiene una capacidad limitada.

---
