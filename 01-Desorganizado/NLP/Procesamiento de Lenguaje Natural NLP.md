# Clase 1
El Procesamiento de Lenguaje Natural (NLP) es un campo de estudio de la Inteligencia Artificial (AI) que se enfoca en la interacción entre computadores y el lenguaje humano.

\* El lenguaje natural es el propio de los humanos para comunicarse entre ellos. Por su parte, el artificial es el lenguaje que entienden los computadores, tales como Python, C, Assembly, etc.


El NLP es un estudio *multidisciplinar* pues hay una necesidad por entender la computación y el lenguaje humano, usando conocimientos de la lingüística y psicología.

La NLP no es solamente un campo técnico, también impacta social y éticamente. Por ejemplo,
- ¿Quién se beneficia de las tecnologías NLP? Cuáles lenguas están incluidas, traducidas y representadas? Esta es una barrera del lenguaje y de inequidad.
- Los sistemas NLP replican o amplifican los juicios sociales? Los NLP son entrenados en bases de datos de lenguajes. El lenguaje es un fenómeno complejo que incluye aspectos culturales de las sociedades. Si se entrena un NLP mediante un lenguaje, este tendrá los componentes propios del lenguaje.

## Objetivos NLP

Hay dos objetivos para un NLP:
1. Entender el lenguage natural (Natural Language Understanding NLU): Entender e interpretar el lenguage humano.
2. Generar lenguage natural (Natural Language Generation NLG): Permitir a los computadores generar mensajes coherentes en lenguage natural.

## Lenguaje
En general, el estudio lingüístico tiene 5 niveles:
- Signos: caracteres, fonemas
- Morfología: palabras
- Sintaxis
- Semántica
- Pragmática: frases, intenciones, etc.
![[Pasted image 20260811210511.png]]

El lenguage es complejo pues requiere resolver ambigüedades de diferentes niveles (por ejemplo palabras con distintos significados) que requiere el reconocimiento del contexto y conocimiento de la cultura. Entender el lenguage requiere reconocer sarcasmo, ironía, humor y lenguage figurativo.

## Temas de NLP
### Part-of-Speech (POS)
Tarea fundamental del NLP en donde a cada palabra de una oración se le asigna una categoría gramatical, p.ej: sustantivo, verbo, adjetivo o adverbio.
\*Hay librerías de Python que pueden clasificar palabras de un lenguaje en particular.

### Named Entity Recognition (NER) Detection
Tarea de NLP en la cual se identifican y clasifican aspectos fundamentales de los elementos que componen un texto en categorías predefinidas. Por ejemplo personas, organizaciones, ubicaciones, fechas, etc.

### Estructura Sintáctica (Dependency Parsing)
Tarea de análisis sintáctico en NLP que identidica la estructura gramatical de una oración, estableciendo relaciones entre las palabras


Cuando se tiene una frase con una jerarquización:

*The brown fox jumped over the lazy dog*



### Clasificación de Texto
La clasificación de texto tiene una estructura de trabajo:
1. Datos (Input/Entrada)
2. Procesamiento (Features)
3. Predicción (Output/salida)

Las tareas se pueden implementar con distintos algoritmos, tales como Support Vector Machines (SVM), Naive Bayes, Logistic Regression, Decision Trees, etc.

# Clase 2: Clasificación de Texto / Text Classification

La clasificación de texto es una tarea de NLP que se puede usar para:
- Análisis de Sentimiento: Identificar si la sensación es positiva, negativa o neutral de una reseña, por ejemplo.
- Clasificación de Tópico: Identificar la categoría de un texto.
  Por ejemplo: 'El gobierno aprobó un nuevo presupuesto' -> Política; 'El nuevo iPhone tiene una cámara muy buena' -> Tecnología.
- Detección de Spam: Identificar si un correo electrónico tiene información relevante.
- Clasificación de la Intención: Identificar la intención de una oración por una persona.
  Por ejemplo: 'Dónde esta mi paquete?' -> Consulta de una orden; 'Necesito ayuda para restablecer mi contraseña' -> Soporte de Cuenta.

## Clasificación de Texto - Definición
El proceso de clasificación de texto se define como:
1. Input/Entrada:
   - Un documento $d$
   - Un conjunto fijo de clases $C = \{ c_{1},c_{2},\dots,c_{n} \}$
1. Output/Salida:
   - Una *clase* **predecida** $c'\in C$

## Métodos

### Hand-Coded Rules
Es cuando se determinan las intenciones por palabra 'manualmente', de la forma:
$$
c'=
\left\{
	\begin{array}{ll}
		\text{Positivo}\; , \text{si }(\text{'great'}\in d)\vee
		 (\text{'excellent'}\in d)\vee\dots \\
		\text{Negativo}\; , \text{si }\dots \\
		\text{Neutral}\;, \text{si }\dots
	\end{array}
\right.
$$
y también se pueden incluir reglas de palabras combinadas.

Para este método, se puede tener una alta precisión si tiene una expertiz en el caso, pero el mantenimiento y escalamiento es limitado. Por ejemplo, se tienen problemas en caso de sarcasmo, uso de sinónimos, etc.

### Supervised Learning
Es un proceso que se define como:
1. Input:
   - Un documento $d$
   - Un conjunto fijo de clases $C=\{ c_{1},c_{2},\dots,c_{n} \}$
   - Un conjunto de entrenamiento de $m$ documentos ya etiquetados $(d_{1},c_{1}),(d_{2},c_{2}),\dots,(d_{m},c_{m})$
1. Output:
   - Una clasificación aprendida $\gamma:d\to c$

##### Ejemplo: Análisis de Sentimiento
Para un conjunto $C=\{ \text{Positivo, Negativo} \}$ y un conjunto de entrenamiento:
- $d_{1}=\text{'Que buena pelicula'}$, $c_{1}=\text{Positivo}$
- $d_{2}=\text{'Esta pelicula estuvo terrible'}$, $c_{2}=\text{Negativo}$

El modelo adquiere los patrones de los ejemplos ya etiquetados. Así, dado un nuevo documento $d'$:
$$
d'=\text{'disfrute mucho esta pelicula'}
$$
$$
\gamma(d')=\text{Positivo}
$$

## Bag-of-Words (BoW)
El método Bag-of-Words BoW es una representación simple de un documento, en donde se detecta cada palabra del texto y se contabiliza la aparición de cada una. Luego, se tabula la palabra con la cantidad de veces que aparece.
Ejemplo: 'Excellent product, arrived fast ... '

| Palabra   | Cantidad |
| --------- | -------- |
| arrived   | 1        |
| excellent | 2        |

## Machine Learning Supervisado
El framework de trabajo es:
1. Datos (Input/Entrada)
2. Características (Features)
3. Predicción (Output/salida)

Para ello, una clasificación de palabras es necesaria. Hay varios tipos de clasificadores:
1. Naive Bayes
2. Regresión Logística
3. Support Vector Machines (SVMs)
4. $k$-nearest Neighbors ($k$-NN)


## Naive Bayes
Un documento puede ser representado por sus características (features):
$$
d=(x_{1},x_{2},\dots,x_{n})
$$
que, **para un texto, las características pueden ser las palabras**.
Ejemplo: 'Gran película' puede ser representaod por sus características $x_{1}=\text{gran},x_{2}=\text{pelicula}$.
Por lo tanto: $P(d|c)=P(x_{1},x_{2},\dots,x_{n}|c)$ y el clasificador es:
$$
C_{MAP}=\underbrace{ argMAX }_{ c\in C } P(x_{1},x_{2},\dots,x_{n}|c)P(c)
$$

Naive Bayes asume que:
1. Bag-of-Words BoW: La posición no es relevante
2. Independencia Condicional: Se asume que las probabilidades de las caracaterísticas $P(x_{i}|c)$ son independientes para una clase $c$, entonces se puede hacer:
   $$
   P(x_{1},x_{2},\dots,x_{n}|c)=P(x_{1}|c)\cdot P(x_{2}|c)\cdot\dots\cdot P(x_{n}|c)
   $$
   así, para un texto, Naive Bayes asume que las palabras son independientes pero se sabe que esto no es así en la realidad.

> Naive Bayes estima la probabilidad de que a cada palabra le sea asignada una clase, asumiendo independencia condicional entre palabras.
> Combina las probabilidades para computar un puntaje para cada clase y predice la clase con el mayor puntaje.

---
Ejemplo: Clasificando una nueva reseña con Naive Bayes.
Sea $d=\text{'The movie was amazing'}$ el documento, se quiere predecir si es una reseña positiva o negativa. O sea se hace la pregunta de las probabilidades condicionales: $P(\text{Positivo}|d)$ versus $P(\text{Negativo}|d)$.
Si el modelo se entrena con los datos:

| Clase | Reseña          |
| ----- | --------------- |
| pos   | movie amazing   |
| pos   | movie good      |
| pos   | amazing good    |
| neg   | movie boring    |
| neg   | movie terrible  |
| neg   | boring terrible |
de ello, se tienen las probabilidades:
$$
P(\text{Pos})=\frac{3}{6}=0.5
$$
$$
P(Neg)=\frac{3}{6}=0.5
$$
Y luego se cuenta la ocurrencia de cada palabra en cada clase.
Para algunos casos no se van a tener ocurrencias, lo que entrega una probabilidad $P$ nula, como $P(\text{movie}|\text{neg})=\frac{0}{6}=0$ y luego la multiplicación de probabilidades (por independencia) se anularía. Para evitar esto se hace una **'Suavización' de Laplace**, de la forma:
$$
P(w|c)=\frac{\text{Count}(w,c)+1}{\text{TotalWords}(c)+|V|}
$$
para este caso se tienen 5 palabras: $|V|=5$ y cada clase contiene 6 palabras. Entonces
$$
\text{TotalWords}(c)+|V|=6+5=11
$$
y para la palabra 'amazing':
$$
P(amazing|Pos)=\frac{2+1}{11}=0,273
$$
$$
P(amazing|Neg)=\frac{0+1}{11}=0.091
$$
el nuevo documento $d'=\{ \text{movie},\text{amazing} \}$, para positivo:
$$
\begin{array}
P(pos)=0.5 \\
P(d|Pos)\approx P(movie|Pos)\cdot P(amazing|Pos) \\
\therefore Score(Pos)=0.5\cdot 0.273\cdot 0.273  \\
Score(Pos)=0.372 \\
\end{array}
$$
para negativo:
$$
\begin{array}
Score(Neg)=0.5\cdot 0.273\cdot 0.091 \\
Score(Neg) \approx 0.0124
\end{array}
$$
y finalmente, se elige la clase 'más probable' como la que tiene mayor puntaje. O sea:
$$
c'=\underbrace{ argMAX }_{ c }\  P(c)\ \prod_{i=1}^{n}P(w_{i}|c)
$$
luego $c'=Pos$
> $argMAX$ significa elegir la clase con el mayor puntaje.
## Stop-Words
Las Stop Words son palabras con mucha frecuencia y poca relevancia para el análisis deseado, como conectores o adverbios.

En algoritmo Naive Bayes usualmente se ignoran las stop words
\* Una implementación es ordenadar por frecuencia, clasificar las primeras 10-50 palabras stopwords e ignorarlas.

## Lexicons
Los lexicons son diccionarios preclasificados para cuando se tienen pocos datos de entrenamiento. Este diccionario asigna un puntaje predefinido a una lista de palabtas según el sentimiento y su intensidad.

## Evaluación
Considerando solo textos de clasificación binaria, 


### Accuracy
La medida de precisión no es útil para el caso de los kuchen pues solamente se entrega el porcentaje de menciones del tópico, pero es necesario también saber qué dicen los comentarios.

### F-Score
Combina la precisión y el Recall.
La medida F-measure es un número que combina la Precisión y Recall, de la forma:
$$
F_{\beta}=\frac{(b^{2}+1)PR}{\beta^{2}P+R}
$$
casi siempre se usa la medida $F_{1}$, esto es con $\beta=1$:
$$
F_{1}=\frac{2PR}{P+R}
$$

## 
Cuando se tienen muchos documentos (textos) se separan en sets de:
- Entrenamiento
- Desarrollo
- Prueba
la idea es dejar uno (el de prueba) para el final; Hacer todas las modificaciones en el conjunto de entrenamiento y en el de desarrollo para las iteraciones y se evalúa en el de prueba.
Para el caso de modelos pequeños se puede no usar el set de desarrollo.

## Micro|Macro-Averaging
Una forma de combinar las medidas de éxito y fracaso:
Si se tienen más de una clase, ¿cómo combinar múltiples medidas en solo una?

- Macroaveraging: Calcular para cada clase y luego promediar.
- Mircoaveraging: 


# Clase 3: Logistic Regression

## Logistic Regression
El método de Naive Bayes utiliza la probabilidad de cada palabra para predecir el nuevo documento. Mientras que la Regresión Logística utiliza *pesos* para la predicción.
La idea del método es entender **qué distingue** a las clases, por ejemplo:
Distinguir imágenes entre perros y gatos corresponde a observar las características que los diferencian, o también en entender cuáles características distinguen a cada uno.
\* hay que notar la situación de una característica no deseada que se identifica como el elemento relevante, como por ejemplo que en el entrenamiento, los perros tengan collar y los gatos no puede llevar a que tener collar sea una característica propia de perros. En este sentido, con Naive Bayes se puede elegir qué parte entra en el entrenamiendo y con la Regresión Log. no se pueden separar características.

> Regresión Logística utiliza el **peso (weight)** que entrega la importancia o relevancia de la característica para obtener la predicción.

### Clasificador de Regresión Logística
Dados pares entrada y salida (input/output) $m=(x^{(i)},y^{(i)})$, se tienen:
1. Una **representación de las características** de la entrada. 
