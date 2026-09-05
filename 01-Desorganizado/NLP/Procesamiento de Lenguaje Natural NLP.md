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

- [ ] Terminar

### Clasificador de Regresión Logística
Dados pares entrada y salida (input/output) $m=(x^{(i)},y^{(i)})$, se tienen:
1. Una **representación de las características** de la entrada. 


# clase 4

## AUX
#### Perplexity
Mide cuán sorprendido esta el modelo 

Se saca la probabilidad de una oración completa
$$
PPL(W)=\frac{1}{\sqrt[n]{ P(w_{1},\dots,w_{n}) }}
$$
$$
PPL(W)=\frac{1}{\sqrt[n]{ P(W) }}
$$

Como es pitatoria, para asignar probabilidades a N-gramas no vistos aún (que van a tener probabilidad 0), se usa smoothing 


> Perplejidad se utiliza para evaluar cuán bueno es un modelo de lenguaje prediciendo texto que todavía no ha visto.

# Auxiliar 1: Introducción a NLP, Fuentes de Datos, Preprocesamiento y Proyectos

---
Objetivos de la sesión
1. **Comprender el panorama de NLP**: Desde métodos simbólicos y estadísticos clásicos hasta la era de LLMs e interpretabilidad.
2. **Aprender a obtener datos (Data Sourcing)**: Cargar datasets con `datasets` (Hugging Face), consultar datos de Kaggle y hacer Web Scraping simple con `BeautifulSoup`.
3. **Dominar el preprocesamiento de texto en español**: Tokenización, normalización, manejo de stopwords, stemming (`nltk`) y lematización (`spacy`).
4. **Inspirar el Proyecto Semestral**: Explorar ideas en interpretabilidad mecanicista e intrínseca, Safety & Alignment, Trustworthy AI, RAG y tareas locales en español.
---


##### Librerias Necesarias
```python
import os
os.environ["NLTK_DISABLE_IMPORT_SECURITY"] = "1"
!pip install marimo unidecode
import marimo as mo
import re
import sys
import pandas as pd
import requests
from bs4 import BeautifulSoup
from unidecode import unidecode
```


## 1. Mini-Introducción: El Espectro de NLP

El **Procesamiento de Lenguaje Natural (NLP)** busca que las máquinas procesen, entiendan y generen lenguaje humano. A lo largo de las décadas, los enfoques han evolucionado radicalmente:

| Era / Paradigma | Enfoque Principal | Ejemplos | ¿Cuándo se usa hoy? |
| :--- | :--- | :--- | :--- |
| **1. Simbólico / Reglas** | Expresiones regulares, gramáticas formales, diccionarios | Regex, autómatas finitos, WordNet | Limpieza de datos, extracción de patrones deterministas (rut, emails, fechas). |
| **2. Estadístico / Clásico** | Modelos de frecuencias y conteos vectoriales | Bag of Words (BoW), TF-IDF, Naive Bayes, SVM | Baselines rápidos, clasificación en CPU ultraliviana, filtros de spam. |
| **3. Embeddings & Redes** | Representaciones densas continuas | Word2Vec, FastText, GloVe, BiLSTM | Búsqueda semántica básica, clasificación con recursos moderados. |
| **4. Transformers & LLMs** | Mecanismo de atención y modelos masivos preentrenados | BERT, RoBERTa, LLaMA, GPT, Mistral | Estado del arte en generación, QA, razonamiento, extracción compleja. |

> [!TIP]
> **Pregunta recurrente**: *¿Por qué estudiamos preprocesamiento clásico si los LLMs usan subword tokenizers (BPE/WordPiece)?*
> 1. **La Tarea 1** y muchos sistemas de producción requieren procesar terabytes de texto donde modelos clásicos (BoW / TF-IDF) son $1000\times$ más rápidos y baratos que inferir con un transformer.
> 2. Comprender la raíz morfológica y léxica de las palabras es fundamental para curar datasets, limpiar ruido de la web y diagnosticar errores en modelos modernos.

---
## 2. Fuentes de Datos para NLP

Para cualquier proyecto o tarea de NLP, el primer paso es **obtener datos de calidad**. Revisaremos las 3 formas más comunes de conseguirlos:
1. **Hugging Face Hub (`datasets`)**
2. **Kaggle Datasets**
3. **Web Scraping con BeautifulSoup**

### 2.1 Hugging Face Datasets Hub (`datasets`)
[Hugging Face](https://huggingface.co/datasets) aloja miles de datasets públicos. Con la librería `datasets`, podemos cargar colecciones enteras en 2 líneas de código.


```python
# Demostración de importación de dataset desde Hugging Face
try:
    from datasets import load_dataset

    # Cargamos un dataset en español de análisis de sentimientos
    # 'mteb/tweet_sentiment_multilingual' contiene tweets etiquetados por sentimiento
    hf_dataset = load_dataset("mteb/tweet_sentiment_multilingual", "spanish", split="train[:5]")
    df_hf = pd.DataFrame(hf_dataset)
    print("✅ Dataset de Hugging Face cargado exitosamente:")
except Exception as e:
    print(f"Nota: Simulación de carga (o conexión no disponible): {e}")
    df_hf = pd.DataFrame({
        "text": [
            "Me encantó el nuevo producto, excelente atención!",
            "El servicio fue pésimo y la entrega llegó con dos días de retraso.",
            "El paquete llegó a tiempo, todo normal."
        ],
        "label": ["positive", "negative", "neutral"]
    })

df_hf.head()
```

> [!NOTE]
> **Tip de Streaming para datasets gigantes**:
> Si el dataset pesa 50 GB, no necesitas descargarlo entero en RAM. Puedes usar `streaming=True`:
> ```python
> dataset_stream = load_dataset("large_corpus", streaming=True)
> for sample in dataset_stream["train"].take(5):
>     print(sample["text"])
> ```

### 2.2 Kaggle Datasets
[Kaggle](https://www.kaggle.com/datasets) es una de las fuentes más populares de datasets tabulares y de texto.

Existen varias formas de consumir datos de Kaggle:
1. **Descarga directa / API de Kaggle (`kagglehub`)**:
   ```python
   import kagglehub
   path = kagglehub.dataset_download("usuario/nombre-del-dataset")
   ```
2. **Lectura directa con Pandas desde URLs públicas / GitHub mirrors**:
   ```python
   import pandas as pd
   df = pd.read_csv("https://url-publica-al-dataset/data.csv")
   ```

### 2.3 Web Scraping con BeautifulSoup (`bs4` + `requests`)
Cuando no existe un dataset pre-construido, podemos extraer datos directamente de la web de forma estructurada y ética.


```python
# Ejemplo práctico: Scrapear frases célebres desde quotes.toscrape.com (sitio público diseñado para practicar scraping)
SCRAPE_URL = "http://quotes.toscrape.com/"

try:
    response = requests.get(SCRAPE_URL, timeout=10)
    soup = BeautifulSoup(response.text, "html.parser")

    # Buscamos todos los bloques de citas
    quote_elements = soup.find_all("div", class_="quote")
    quotes_data = []

    for q in quote_elements[:5]:  # Tomamos las primeras 5
        text_tag = q.find("span", class_="text")
        author_tag = q.find("small", class_="author")

        text = text_tag.get_text(strip=True) if text_tag else ""
        author = author_tag.get_text(strip=True) if author_tag else ""
        tags = [tag.get_text(strip=True) for tag in q.find_all("a", class_="tag")]

        quotes_data.append({
            "quote": text,
            "author": author,
            "tags": ", ".join(tags)
        })

    df_scraped = pd.DataFrame(quotes_data)
    print("✅ Web Scraping ejecutado exitosamente con BeautifulSoup:")
except Exception as e:
    print(f"Error o timeout al scrapear: {e}")
    df_scraped = pd.DataFrame({
        "quote": ["“The world as we have created it is a process of our thinking.”"],
        "author": ["Albert Einstein"],
        "tags": ["change, thinking"]
    })

df_scraped
```

### 2.4 Repositorios Recomendados para Proyectos

| Repositorio | Tipo de Datos | Link |
| :--- | :--- | :--- |
| **Hugging Face Datasets** | Textos en español, clasificación, QA, traducciones, tweets | [huggingface.co/datasets](https://huggingface.co/datasets) |
| **Kaggle NLP** | Competencias de clasificación, fake news, reseñas, foros | [kaggle.com/datasets](https://www.kaggle.com/datasets) |
| **Datos Abiertos Chile** | Datos gubernamentales, licitaciones, reclamos SERNAC | [datos.gob.cl](https://datos.gob.cl) |
| **Laboratorio BCN (Congreso)** | Proyectos de ley, transcripciones del Senado y Cámara | [bcn.cl/laboratorio](https://www.bcn.cl/laboratorio) |
| **Papers With Code Datasets** | Datasets con benchmarks académicos internacionales | [paperswithcode.com/datasets](https://paperswithcode.com/datasets) |

---
## 3. Preprocesamiento de Texto

El preprocesamiento consiste en limpiar y transformar el texto crudo en representaciones normalizadas.
Revisaremos las herramientas fundamentales en Python: **spaCy** y **NLTK**.


```python
import spacy
import nltk

# Descarga automática del modelo en español de spaCy
try:
    nlp = spacy.load("es_core_news_sm")
except OSError:
    print("📥 Descargando modelo 'es_core_news_sm' de spaCy...")
    import spacy.cli
    spacy.cli.download("es_core_news_sm")
    nlp = spacy.load("es_core_news_sm")

# Descarga automática de recursos de NLTK
try:
    from nltk.corpus import stopwords
    _ = stopwords.words("spanish")
except LookupError:
    print("📥 Descargando stopwords y punkt de NLTK...")
    nltk.download("stopwords", quiet=True)
    nltk.download("punkt", quiet=True)
    nltk.download("punkt_tab", quiet=True)

from nltk.corpus import stopwords
from nltk.stem import SnowballStemmer

stemmer_es = SnowballStemmer("spanish")
stopwords_nltk_es = set(stopwords.words("spanish"))
stopwords_spacy_es = nlp.Defaults.stop_words

print("✅ Modelos y diccionarios lingüísticos cargados correctamente.")
```

### 3.1 Normalización y Limpieza de Texto
Antes de procesar morfológicamente, solemos aplicar transformaciones de bajo nivel:
- **Minúsculas (`lower()`)**: Unifica términos ("Chile" == "chile").
- **Remover signos de puntuación**: Usando expresiones regulares (`re`).
- **Remover tildes / caracteres especiales (`unidecode`)**: Opcional según la tarea (útil para búsquedas tolerantes a faltas de ortografía).


```python
texto_ejemplo = "¡Increíble! En Valparaíso, los pingüinos y las aves NO voladoras nadan a 25 km/h... ¿cierto?"

# 1. Minúsculas
texto_min = texto_ejemplo.lower()

# 2. Sin signos de puntuación
texto_sin_punt = re.sub(r"[^\w\s]", "", texto_ejemplo)

# 3. Sin tildes / acentos
texto_sin_tildes = unidecode(texto_ejemplo)

print(f"Texto original:    {texto_ejemplo}")
print(f"1. Minúsculas:     {texto_min}")
print(f"2. Sin puntuación: {texto_sin_punt}")
print(f"3. Sin tildes:     {texto_sin_tildes}")
```

### 3.2 Tokenización (Word vs Sentence)
La **tokenización** divide el texto en unidades atómicas (*tokens*).


```python
# Tokenización lingüística con spaCy (reconoce abreviaciones, números y puntuaciones inteligentes)
doc_spacy = nlp(texto_ejemplo)
tokens_spacy = [token.text for token in doc_spacy]

print("Tokens obtenidos con spaCy:")
print(tokens_spacy)
```

### 3.3 Eliminación de Stop Words
Las *Stop Words* son palabras de alta frecuencia con poco valor semántico discriminativo por sí solas (artículos, preposiciones, pronombres).


```python
tokens_sin_stopwords = [
    token.text for token in doc_spacy
    if token.text.lower() not in stopwords_spacy_es and not token.is_punct
]

print(f"Cantidad de stopwords en spaCy (español): {len(stopwords_spacy_es)}")
print(f"Cantidad de stopwords en NLTK (español):   {len(stopwords_nltk_es)}")
print("\nTexto filtrado (sin stopwords ni puntuación):")
print(tokens_sin_stopwords)
```

> [!WARNING]
> **¿Cuándo NO debemos eliminar Stop Words?**
> - **Análisis de Sentimientos**: La palabra `"no"` es una stopword en casi todas las listas, pero cambia radicalmente el sentido: *"no es bueno"* vs *"es bueno"*.
> - **Modelos de Lenguaje Basados en Transformers**: BERT y GPT necesitan la estructura gramatical completa para computar la atención contextual.

### 3.4 Stemming vs Lematización

- **Stemming (NLTK)**: Algoritmo heurístico que corta sufijos y prefijos para encontrar una "raíz" aproximada. Es **rápido**, pero el resultado no necesariamente es una palabra válida del diccionario.
- **Lematización (spaCy)**: Análisis morfológico completo que busca el **lema** de la palabra (la forma canónica de diccionario, e.g. infinitivo para verbos). Es **preciso y semánticamente correcto**, aunque más costoso computacionalmente.


```python
palabras_test = [
    "comiendo", "comió", "comeré",
    "dije", "dijeron", "diciendo",
    "computadoras", "computación", "computarizado",
    "mejores", "buenísimo", "perros", "estabilidad"
]

comparacion = []
for palabra in palabras_test:
    doc = nlp(palabra)
    lema = doc[0].lemma_
    stem = stemmer_es.stem(palabra)
    comparacion.append({
        "Palabra Original": palabra,
        "Stemming (NLTK)": stem,
        "Lematización (spaCy)": lema
    })

df_comparacion = pd.DataFrame(comparacion)
df_comparacion
```

### 3.5 Playground Interactivo de Preprocesamiento
Escribe cualquier oración o párrafo para ver cómo se descompone y procesa en tiempo real:


```python
# Componente interactivo de marimo (compatible con exportación a Jupyter)
input_text = mo.ui.text_area(
    value="Los estudiantes del DCC están investigando modelos de lenguaje para sus proyectos semestrales.",
    label="📝 Ingresa un texto para preprocesar:",
    full_width=True
)
input_text
```


```python
# Procesamiento reactivo del texto ingresado
texto_a_procesar = input_text.value if hasattr(input_text, "value") else str(input_text)
doc_analisis = nlp(texto_a_procesar)

tabla_analisis = []
for t in doc_analisis:
    if not t.is_space:
        tabla_analisis.append({
            "Token": t.text,
            "Minúscula": t.text.lower(),
            "Lema (spaCy)": t.lemma_,
            "Stem (NLTK)": stemmer_es.stem(t.text.lower()),
            "POS Tag (Tipo)": t.pos_,
            "¿Es Stopword?": "🛑 Sí" if t.text.lower() in stopwords_spacy_es else "✅ No",
            "¿Es Puntuación?": "🔣 Sí" if t.is_punct else "No"
        })

df_analisis = pd.DataFrame(tabla_analisis)
df_analisis
```

---
## 4. Ideas y Sugerencias para el Proyecto Semestral

El proyecto semestral es grupal y de **tema libre**. Las siguientes áreas son solo **fuentes de inspiración** para orientar su búsqueda:

### 4.1 NLP Aplicado y Contexto Local (Chile / Español)
*Resolver problemas reales con datos locales y lenguaje cotidiano:*
- **Discurso Parlamentario**: Clasificación ideológica o análisis de tópicos en debates del Congreso ([Laboratorio BCN](https://www.bcn.cl/laboratorio)).
- **Detección de Sesgos y Toxicidad**: Modelos para detectar agresividad o fake news considerando modismos y chilenismos.
- **NLP Legal o Médico**: Extracción de información en sentencias judiciales o fichas clínicas anonimizadas.

### 4.2 LLMs, RAG y Adaptación de Modelos
*Construir y evaluar sistemas basados en modelos de lenguaje modernos:*
- **Sistemas RAG Especializados**: Asistentes sobre reglamentos de la U. de Chile, leyes nacionales o manuales técnicos.
- **Fine-Tuning Eficiente (LoRA / PEFT)**: Adaptar modelos pequeños (1B–3B parámetros) a dialectos o tareas especializadas en español.

### 4.3 Interpretabilidad Mecanicista
*Entender cómo los LLMs almacenan y procesan conceptos internamente:*
- **Plataforma [Neuronpedia](https://www.neuronpedia.org/)**: Explorar *Sparse Autoencoders (SAEs)* para ver qué conceptos activan neuronas específicas en modelos como Gemma o LLaMA.
- **Steering Vectors & Circuitos**: Intervenir directamente en las activaciones para modificar el comportamiento, sesgo o razonamiento del modelo.

### 4.4 Interpretabilidad Intrínseca (Modelos Transparentes por Diseño)
*En vez de analizar un modelo opaco después de entrenarlo, diseñar arquitecturas transparentes desde su construcción ([Survey ACL](https://aclanthology.org/2026.acl-long.1605.pdf)):*
- **Alineamiento de Conceptos (CBMs)**: Forzar al modelo a predecir conceptos humanos intermedios (ej. formalidad, agresividad, tema) antes de tomar su decisión final.
- **Desentrelazamiento de Representaciones**: Restringir geométricamente el espacio latente para separar limpiamente dimensiones como *estilo/dialecto* de *significado semántico*.
- **Modularidad & Esparcidad**: Modelos con expertos especializados (*MoE*) o activaciones esparsas donde cada componente tiene una función interpretable.

### 4.5 Safety, Alignment y Trustworthy AI en LLMs
*Garantizar que los modelos de lenguaje sean confiables, seguros, justos y alineados con valores humanos (Helpful, Honest, Harmless - HHH):*
- **Alineamiento con Preferencias (RLHF / DPO)**: Entrenar o ajustar modelos para seguir instrucciones seguras usando *Direct Preference Optimization* sobre pares de respuestas preferidas vs. rechazadas.
- **Detección y Mitigación de Alucinaciones (*Factuality*)**: Evaluar la calibración de incertidumbre del modelo y diseñar métodos para verificar y contrastar hechos antes de generar respuestas.
- **Safety Guardrails & Red-Teaming**: Testear vulnerabilidades de seguridad (*jailbreaks*, inyección de prompts) en español y construir capas de moderación y filtrado (ej. *Llama-Guard*).
- **Auditoría de Sesgos y Equidad (*Fairness*)**: Evaluar y mitigar sesgos sociales, de género o ideológicos presentes en modelos abiertos frente al contexto y cultura hispanohablante.
- **Desaprendizaje de Conocimiento (*Machine Unlearning*)**: Métodos para remover selectivamente información sensible, privada o con derechos de autor sin reentrenar el modelo completo.

---
## Consejos Clave para el Proyecto
1. **Define los Datos Temprano**: Un proyecto con datos accesibles desde el inicio tiene el éxito prácticamente asegurado.
2. **Empieza con un Baseline Simple**: Compara siempre tu propuesta con un modelo clásico (BoW / Regresión Logística) antes de usar modelos complejos.
3. **¡Apóyate en el Equipo Docente!**: Consulta tus ideas en los horarios de atención y clases auxiliares para calibrar el alcance.

---

## Referencias y Recursos
- **Survey de Interpretabilidad Intrínseca (ACL)**: [Towards Intrinsic Interpretability of LLMs](https://aclanthology.org/2026.acl-long.1605.pdf)
- **Neuronpedia (Interpretabilidad Mecanicista)**: [neuronpedia.org](https://www.neuronpedia.org/)
- **Safety & Trustworthy Benchmarks**: [TruthfulQA](https://github.com/sylinrl/TruthfulQA) | [BBQ (Bias Benchmark)](https://github.com/nyu-mll/bbq) | [Llama Guard](https://huggingface.co/meta-llama/Llama-Guard-3-8B)
- **Documentación Hugging Face Datasets**: [huggingface.co/docs/datasets](https://huggingface.co/docs/datasets)
- **Documentación Preprocesamiento**: [spaCy](https://spacy.io/) | [NLTK](https://www.nltk.org/)
- **Realizaciones Anteriores CC6205**: [github.com/dccuchile/CC6205](https://github.com/dccuchile/CC6205)



# Auxiliar 2: Semántica Vectorial y Análisis de Sentimiento y Evaluación

##### Librerias necesarias
```python
import re
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from datasets import load_dataset
from sklearn.feature_extraction.text import CountVectorizer, TfidfVectorizer
from sklearn.model_selection import train_test_split, cross_val_score
from sklearn.naive_bayes import MultinomialNB
from sklearn.pipeline import Pipeline
from sklearn.metrics import classification_report, confusion_matrix

# Configuramos el estilo de los gráficos para que se vean modernos
sns.set_theme(style="whitegrid", palette="muted")
```

## Objetivos de la sesión
1. **Semántica Vectorial**: Representar textos matemáticamente mediante *Bag of Words (BoW)* y *TF-IDF*.
2. **Análisis de Sentimiento en 3 niveles usando Naive Bayes**:
   - Nivel Documento (Reseñas largas)
   - Nivel Sentencia (Tweets o frases cortas)
   - Nivel Aspecto (Desglose por temática dentro de una misma oración)
3. **Validación y Métricas**: Validación cruzada y evaluación de modelos mediante *Precision, Recall, F1-Score* y promedios *Micro/Macro*.

---

## 1. Semántica Vectorial

Los algoritmos de Machine Learning no entienden palabras directamente, necesitan números. La **semántica vectorial** transforma documentos en vectores de características numéricas.

### 1.1 Bag of Words (BoW)
El modelo más intuitivo: convertimos el documento en un vector que **cuenta las apariciones** de cada palabra en nuestro vocabulario, ignorando completamente el orden gramatical.

Veamos un ejemplo de juguete:


```python
corpus_toy = [
    "me encantan los perros",
    "los perros son geniales",
    "los gatos y los perros no se llevan bien",
]

_vectorizer_bow = CountVectorizer()
_X_bow = _vectorizer_bow.fit_transform(corpus_toy)

_df_bow = pd.DataFrame(_X_bow.toarray(), columns=_vectorizer_bow.get_feature_names_out())
_df_bow.index = [f"Doc {i+1}" for i in range(len(corpus_toy))]

fig_bow, ax_bow = plt.subplots(figsize=(8, 3))
sns.heatmap(_df_bow, annot=True, cmap="Blues", cbar=False, ax=ax_bow)
ax_bow.set_title("Representación Bag of Words (Conteos)", fontsize=14)
plt.tight_layout()
plt.xticks(rotation=45)
plt.show()
```

![[Aux_2_BoW_Analisis_Sentimientoipynb_3_0.png]]

### 1.2 TF-IDF (Term Frequency - Inverse Document Frequency)

El problema de BoW es que le da mucha importancia a palabras muy frecuentes que no aportan contexto ("los", "y", "en"). **TF-IDF** soluciona esto balanceando la frecuencia local con la rareza global de la palabra.

#### La Fórmula
Para un término $t$ en un documento $d$, perteneciente a un corpus $D$:

$$ \text{TF-IDF}(t, d, D) = \text{TF}(t, d) \times \text{IDF}(t, D) $$

Donde:
1. **TF (Term Frequency)**: Mide qué tan frecuente es el término en el documento específico.

$$ TF(t, d) = \frac{ \text{Conteo de } t \text{ en } d }{ \text{Total de palabras en } d } $$
*(Existen otras variantes, pero esta es la idea intuitiva)*

2. **IDF (Inverse Document Frequency)**: Mide qué tanta información aporta el término. Si está en todos los documentos (ej. "el"), el IDF será bajo. Si es raro, será alto.

$$ IDF(t, D) = \log\left(\frac{N}{|\{d \in D : t \in d\}|}\right) $$
   Donde $N$ es el total de documentos y el denominador es cuántos documentos contienen el término $t$.


```python
_vectorizer_tfidf = TfidfVectorizer()
_X_tfidf = _vectorizer_tfidf.fit_transform(corpus_toy)

_df_tfidf = pd.DataFrame(_X_tfidf.toarray(), columns=_vectorizer_tfidf.get_feature_names_out())
_df_tfidf.index = [f"Doc {i+1}" for i in range(len(corpus_toy))]

fig_tfidf, ax_tfidf = plt.subplots(figsize=(8, 3))
sns.heatmap(_df_tfidf, annot=True, cmap="Oranges", fmt=".2f", cbar=False, ax=ax_tfidf)
ax_tfidf.set_title("Representación TF-IDF (Pesos)", fontsize=14)
plt.tight_layout()
plt.xticks(rotation=45)
plt.show()
```

![[Aux_2_BoW_Analisis_Sentimientoipynb_5_0.png]]

> [!NOTE]
> Nota cómo en TF-IDF la palabra **"los"** recibe un peso menor comparado con BoW, porque aparece en todos los documentos, mientras que palabras más únicas como **"gatos"** o **"encantan"** reciben un peso proporcionalmente mayor.

## 2. Análisis de Sentimiento con Naive Bayes

El Análisis de Sentimiento busca determinar la polaridad de un texto (positivo, negativo, neutral). Usaremos **Naive Bayes**, un algoritmo probabilístico extremadamente rápido y efectivo para texto.

### El Teorema de Bayes Aplicado
Queremos predecir la clase de sentimiento $c$ dado un documento $d$:
$$ p(c|d) = \frac{p(d|c) \cdot p(c)}{p(d)} $$

Como $p(d)$ es igual para todas las clases y buscamos el máximo (argmax), lo podemos omitir.
Además, asumimos que cada palabra ocurre de manera **independiente** (esto es la parte *'Naive'* o ingenua):
$$ \hat{c} = \underset{c \in C}{\operatorname{argmax}} \left( \log(p(c)) + \sum_{x_j \in d} \log(p(x_j | c)) \right) $$
*Usamos logaritmos para evitar el desbordamiento numérico al multiplicar muchas probabilidades pequeñas.*

### Suavizado de Laplace (Laplace Smoothing)
¿Qué pasa si una palabra nueva aparece en el test pero nunca la vimos en el train para esa clase? Su $p(x_j|c)$ será $0$, anulando toda la probabilidad de la oración. Para evitar esto, sumamos un pequeño valor $\alpha$ (usualmente 1) a todos los conteos:
$$ p(x_j | c)=\frac{count(x_j, c) + \alpha}{\sum_{x \in V} count(x, c) + \alpha |V|} $$

### ¿Por qué se llama *Multinomial* Naive Bayes?
Existen distintas variantes de Naive Bayes (Gaussiana, Bernoulli, Multinomial). Se le llama **Multinomial** porque modela los datos como si fueran generados por una distribución multinomial, donde las características son **conteos enteros de ocurrencias** (frecuencias de palabras, como en nuestro Bag of Words). Si solo nos importara si la palabra aparece o no (0 o 1), usaríamos *Bernoulli Naive Bayes*.

### 2.1 Nivel Documento (Reseñas Largas)
Descargaremos un subset de *Amazon Reviews* en español. Al ser documentos largos, el modelo tiene mucho más contexto para captar la intención general del autor.


```python
# Cargar 2000 ejemplos aleatorios de reseñas de Amazon en español
print("⏳ Descargando reseñas largas...")
dataset_doc = load_dataset("SetFit/amazon_reviews_multi_es", split="train").shuffle(seed=42).select(range(2000))
df_doc = pd.DataFrame(dataset_doc)

# Convertir etiquetas (0-4 estrellas) a clases de sentimiento
def stars_to_sentiment(stars):
    if stars <= 1: return "negativo"
    elif stars == 2: return "neutral"
    else: return "positivo"

df_doc['sentimiento'] = df_doc['label'].apply(stars_to_sentiment)

# El dataset ya viene con el texto de la reseña en la columna 'text'
df_doc['texto'] = df_doc['text']

print("✅ Dataset de Nivel Documento listo.")
df_doc[['sentimiento', 'texto']].head(3)
```

#### Separación y Entrenamiento (Nivel Documento)


```python
# Holdout: Separar 70% Train, 30% Test
X_doc = df_doc['texto']
y_doc = df_doc['sentimiento']

X_train_doc, X_test_doc, y_train_doc, y_test_doc = train_test_split(X_doc, y_doc, test_size=0.3, random_state=42, stratify=y_doc)

# Entrenar Pipeline
pipeline_doc = Pipeline([
    ('vectorizador', CountVectorizer()),
    ('clasificador', MultinomialNB(alpha=1.0))
])
pipeline_doc.fit(X_train_doc, y_train_doc)
print("🤖 Modelo a nivel documento entrenado exitosamente.")
```

    🤖 Modelo a nivel documento entrenado exitosamente.


### 2.2 Nivel Aspecto (ABSA - Aspect-Based Sentiment Analysis)
El nivel más granular. En una misma oración, un usuario puede hablar positivamente de una cosa y negativamente de otra.
Ejemplo: *"La comida estuvo deliciosa, pero el mesero se demoró una hora en traernos la cuenta y el lugar era muy ruidoso."*

Para abordar esto de forma sencilla usando Machine Learning clásico:
1. Entrenamos un diccionario (Lexicon) de palabras clave agrupadas por aspectos.
2. Usamos reglas (como puntuación o conectores) para dividir oraciones complejas en **cláusulas** pequeñas.
3. Asociamos cada cláusula a un aspecto, y predecimos el sentimiento *de esa cláusula específica* usando el modelo entrenado a nivel de sentencias.


```python
# 1. Definir los aspectos y sus palabras clave (Lexicon para Productos)
aspectos_lexicon = {
    "diseño": ["diseño", "bonito", "feo", "color", "estética", "maravilloso", "apariencia", "visual"],
    "calidad": ["calidad", "roto", "frágil", "resistente", "material", "tapa", "plástico", "dañado", "construcción"],
    "precio": ["precio", "caro", "barato", "oferta", "costo", "dinero", "valor", "pagar"]
}

# 2. Reseña compleja a evaluar
review_compleja = "Me encanta el diseño, es un libro maravilloso y lo recomiendo totalmente, pero la tapa de plástico llegó completamente rota y el precio me pareció demasiado caro para la calidad."

# 3. Función simple para extraer cláusulas (separando por comas y conjunciones 'y'/'pero')
def extraer_clausulas(texto):
    clausulas = re.split(r'[,;.]|\bpero\b|\by\b', texto)
    return [c.strip() for c in clausulas if len(c.strip()) > 3]

clausulas_review = extraer_clausulas(review_compleja)

# 4. Asignar aspecto a cada cláusula y predecir sentimiento
resultados_absa = []
for _c in clausulas_review:
    _aspecto_detectado = None
    # Buscar intersección entre palabras de la cláusula y el lexicon
    for _aspecto, _palabras in aspectos_lexicon.items():
        if any(_palabra in _c.lower() for _palabra in _palabras):
            _aspecto_detectado = _aspecto
            break

    if _aspecto_detectado:
        # Reutilizamos el modelo NB de nivel documento para predecir el sentimiento de este extracto
        _sentimiento = pipeline_doc.predict([_c])[0]
        resultados_absa.append({
            "Aspecto": _aspecto_detectado.capitalize(),
            "Cláusula": _c,
            "Sentimiento Predicho": _sentimiento.capitalize()
        })

print(f"Reseña original: {review_compleja}\n")
df_absa = pd.DataFrame(resultados_absa)
df_absa
```

    Reseña original: Me encanta el diseño, es un libro maravilloso y lo recomiendo totalmente, pero la tapa de plástico llegó completamente rota y el precio me pareció demasiado caro para la calidad.
    


## 3. Validación y Métricas de Evaluación

### 3.1 Cross-Validation (Validación Cruzada K-Fold)
El *Holdout* (lo que hicimos en `train_test_split`) depende mucho de qué datos cayeron en la partición por suerte.
**Cross-Validation** divide los datos en $K$ partes (folds). Entrena $K$ veces, rotando el fold de prueba y promediando la certeza final.

| Fold 1 | Fold 2 | Fold 3 | Fold 4 | Fold 5 |
|---|---|---|---|---|
| 🧪 Test | 📚 Train | 📚 Train | 📚 Train | 📚 Train |
| 📚 Train | 🧪 Test | 📚 Train | 📚 Train | 📚 Train |
| 📚 Train | 📚 Train | 🧪 Test | 📚 Train | 📚 Train |
| 📚 Train | 📚 Train | 📚 Train | 🧪 Test | 📚 Train |
| 📚 Train | 📚 Train | 📚 Train | 📚 Train | 🧪 Test |


```python
# Evaluamos la robustez del modelo de Documentos con 5-Folds
_scores = cross_val_score(pipeline_doc, X_doc, y_doc, cv=5, scoring='accuracy')
print(f"Scores individuales por fold (Nivel Doc): {_scores}")
print(f"Promedio de Accuracy: {_scores.mean():.4f} (+/- {_scores.std() * 2:.4f})")
```

    Scores individuales por fold (Nivel Doc): [0.6475 0.6425 0.6525 0.615  0.6675]
    Promedio de Accuracy: 0.6450 (+/- 0.0344)


### 3.2 Métricas más allá del Accuracy

![Precision y recall a partir de la matríz de confusión](https://media.licdn.com/dms/image/v2/D5612AQFRWL6tF6f7Ug/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1710956776479?e=2147483647&v=beta&t=wg9-8XjiVxtY4zuk-GkZLwo6A1n5pc57UbOOJOOZjFk)

El **Accuracy** es peligroso si las clases están desbalanceadas (ej. 90% positivo, 10% negativo). Usamos:
1. **Precision:** Si predijo "Negativo", ¿qué % eran realmente negativos? (Penaliza equivocarse y alertar falsamente).
2. **Recall:** De todos los que REALMENTE eran "Negativos", ¿qué % atrapó el modelo? (Penaliza dejar escapar los casos importantes).
3. **F1-Score:** Media armónica entre Precision y Recall.

#### Promedios en Problemas Multiclase
- **Macro-average:** Promedia el F1 de cada clase ignorando su tamaño. Trata igual a la clase mayoritaria y a la minoritaria.
- **Micro-average:** Suma los aciertos globales primero y luego calcula el F1. Da más peso a las clases grandes.


```python
y_pred_doc = pipeline_doc.predict(X_test_doc)

# Imprimir reporte de clasificación para el Nivel Documento
print("Reporte de Clasificación sobre Conjunto de Prueba (Nivel Documento/Reviews):")
print(classification_report(y_test_doc, y_pred_doc))
```

    Reporte de Clasificación sobre Conjunto de Prueba (Nivel Documento/Reviews):
                  precision    recall  f1-score   support
    
        negativo       0.65      0.82      0.73       235
         neutral       0.40      0.06      0.11       126
        positivo       0.66      0.78      0.72       239
    
        accuracy                           0.65       600
       macro avg       0.57      0.56      0.52       600
    weighted avg       0.60      0.65      0.59       600
    


### 3.3 Visualizando Errores: Matriz de Confusión
La matriz de confusión nos ayuda a diagnosticar **en qué** se está confundiendo el modelo (ej. confunde muchos Neutrales con Negativos).


```python
_cm = confusion_matrix(y_test_doc, y_pred_doc, normalize='true')
_etiquetas = pipeline_doc.classes_

fig_cm_eval, ax_cm_eval = plt.subplots(figsize=(8, 6))
sns.heatmap(_cm, annot=True, fmt='.2f', cmap="magma_r", xticklabels=_etiquetas, yticklabels=_etiquetas, ax=ax_cm_eval)
ax_cm_eval.set_title("Matriz de Confusión - Nivel Documento", fontsize=15)
ax_cm_eval.set_xlabel("Predicción del Modelo", fontsize=12)
ax_cm_eval.set_ylabel("Valor Real", fontsize=12)
plt.tight_layout()
plt.show()
```

![[Aux_2_BoW_Analisis_Sentimientoipynb_18_0.png]]


### 3.4 Interpretación: ¿Qué palabras son más importantes para cada sentimiento?
Podemos inspeccionar los pesos (o probabilidades logarítmicas) del modelo Naive Bayes a nivel de documento para entender qué palabras ayudan más a discriminar entre las clases.

Para encontrar las palabras más exclusivas de una clase $c$, calculamos un **Score Discriminativo**. Este score compara la probabilidad logarítmica de la palabra en la clase actual contra la probabilidad máxima de esa misma palabra en cualquier otra clase:

$$ Score(w, c) = \log P(w|c) - \max_{c' \neq c} \log P(w|c') $$

Mientras mayor sea el score, más exclusiva es la palabra $w$ para predecir la clase $c$.


```python
# Extraer componentes del pipeline de nivel documento
_clasificador = pipeline_doc.named_steps['clasificador']
_vectorizador = pipeline_doc.named_steps['vectorizador']

_class_labels = _clasificador.classes_
_feature_names = _vectorizador.get_feature_names_out()
_log_probs = _clasificador.feature_log_prob_

_top_k = 10  # Top N palabras por clase
_colors = plt.cm.tab10.colors

# Configurar subplots: 1 fila x 3 columnas (para 3 clases de sentimiento)
fig_importances, axes_imp = plt.subplots(1, 3, figsize=(15, 5))
fig_importances.tight_layout(pad=4.0)

for _i, _class_label in enumerate(_class_labels):
    # Probabilidades para esta clase y el resto
    _class_log_probs = _log_probs[_i]
    _other_log_probs = np.delete(_log_probs, _i, axis=0)

    # Calculamos cuánto más asociada está cada palabra con esta clase vs las otras
    _max_other_probs = np.max(_other_log_probs, axis=0)
    _discriminative_scores = _class_log_probs - _max_other_probs

    # Obtener los top k índices
    _top_features_idx = np.argsort(_discriminative_scores)[-_top_k:]
    _top_features = [_feature_names[_j] for _j in _top_features_idx]
    _top_scores = _discriminative_scores[_top_features_idx]

    # Graficar
    axes_imp[_i].barh(_top_features, _top_scores, color=_colors[_i % len(_colors)])
    axes_imp[_i].set_xlabel('Score Discriminativo', fontsize=10)
    axes_imp[_i].set_title(f'Sentimiento: {_class_label.capitalize()}', fontsize=12)
    axes_imp[_i].grid(axis='x', linestyle='--', alpha=0.7)

plt.show()
```

![[Aux_2_BoW_Analisis_Sentimientoipynb_20_0.png]]

# Auxiliar 3: Clasificación de texto con Regresión Logística

---
 Objetivos de la clase

En la Auxiliar 2 vimos cómo abordar la **clasificación de texto** usando Naive Bayes, un modelo probabilístico generativo.
Hoy estudiaremos un modelo discriminativo fundamental en Machine Learning y NLP: la **Regresión Logística**.

Al finalizar la clase, deberían ser capaces de:
- Entender la diferencia entre modelos Generativos y Discriminativos.
- Comprender el rol de la **función Sigmoide** en la clasificación binaria.
- Entender qué es la **Cross-Entropy Loss** y cómo optimizarla usando **Stochastic Gradient Descent (SGD)**.
- Visualizar el proceso de aprendizaje (curva de pérdida) e interpretar los atributos (features) que más aportan a la decisión del modelo.

---

## 1. Carga y Preparación de Datos

Utilizaremos un dataset de **Detección de Discursos de Odio en Español** disponible en Hugging Face (`piuba-bigdata/contextualized_hate_speech`).
Nuestro objetivo será predecir si un texto contiene discurso de odio (Clase 1) o no (Clase 0).


```python
import pandas as pd
from datasets import load_dataset
from sklearn.model_selection import train_test_split

# Cargar los datos desde Hugging Face
dataset = load_dataset('piuba-bigdata/contextualized_hate_speech')

# Extraer el split de entrenamiento (usaremos una muestra para la clase)
df = dataset['train'].to_pandas()

# Dejar solo las columnas relevantes
# 'text' es el texto del tweet, 'HATEFUL' es 1 si es discurso de odio y 0 si no
dataset_bin = df[['text', 'HATEFUL']].rename(columns={'HATEFUL': 'label'}).dropna()

# Balancear el dataset para tener igual cantidad de ejemplos de odio y no odio
# Tomaremos 3000 ejemplos de cada clase
num_samples = 3000
df_hate = dataset_bin[dataset_bin['label'] == 1].sample(num_samples, random_state=42)
df_other = dataset_bin[dataset_bin['label'] == 0].sample(num_samples, random_state=42)

dataset_balanced = pd.concat([df_hate, df_other]).sample(frac=1, random_state=42).reset_index(drop=True)                #se quiere la misma cant de datos de odio y del resto

# Train-Test Split
X_train, X_test, y_train, y_test = train_test_split(dataset_balanced['text'], dataset_balanced['label'], test_size=0.3, random_state=42)

print(f"Total de datos de entrenamiento: {X_train.shape[0]}")
print(f"Total de datos de prueba: {X_test.shape[0]}")
```

    Total de datos de entrenamiento: 4200
    Total de datos de prueba: 1800



```python
# Veamos la distribución de clases
dataset_balanced['label'].value_counts()
```

    label
    1    3000
    0    3000
    Name: count, dtype: int64



## 2. Introducción a Regresión Logística

### Modelos Generativos vs Discriminativos

- **Generativos (como Naive Bayes)**: Modelan la distribución conjunta $P(X, Y)$. Para clasificar un texto $X$, calculan qué tan probable es generar ese texto asumiendo que pertenece a la clase $Y$, usando el Teorema de Bayes.
- **Discriminativos (como Regresión Logística)**: Modelan directamente la probabilidad condicional $P(Y|X)$. Aprenden una "frontera" de decisión que separa directamente las clases, sin preocuparse de cómo se generan los datos.

En general, los modelos discriminativos suelen tener mayor poder predictivo cuando hay muchos datos de entrenamiento, ya que optimizan explícitamente para clasificar bien.

### La Función Sigmoide
En un modelo lineal clásico calcularíamos: $z = w_1 x_1 + w_2 x_2 + ... + w_n x_n + b$.
El problema es que $z$ (el **logit**) puede tomar cualquier valor entre $-\infty$ y $+\infty$.

Para convertir este logit en una probabilidad válida entre $0$ y $1$, usamos la **Función Sigmoide** $\sigma(z)$:

$$ \sigma(z) = \frac{1}{1 + e^{-z}} $$

Si $z$ es un número positivo grande, $\sigma(z)$ se acerca a 1 (Clase 1: Odio).
Si $z$ es un número negativo grande, $\sigma(z)$ se acerca a 0 (Clase 0: No Odio).

Veámoslo gráficamente:


```python
import numpy as np
import matplotlib.pyplot as plt

def sigmoide(z):
    return 1 / (1 + np.exp(-z))

z_vals = np.linspace(-10, 10, 100)                                              #intervalo de numeros
sig_vals = sigmoide(z_vals)                                                     #obtener funcion sigmoide

fig, ax = plt.subplots(figsize=(8, 4))
ax.plot(z_vals, sig_vals, color='purple', linewidth=3, label=r'$\sigma(z)$')
ax.axhline(0.5, color='gray', linestyle='--')
ax.axvline(0, color='gray', linestyle='--')
ax.set_title('La Función Sigmoide')
ax.set_xlabel('Logit (z)')
ax.set_ylabel('Probabilidad')
ax.legend()
plt.show()
```

![[Aux_3_Regresion_Logistica_6_0.png]]

en donde -inf, +inf se pasa a 0,1.

## 3. Cross-Entropy Loss y Stochastic Gradient Descent (SGD)

### ¿Cómo aprende el modelo? (Cross-Entropy Loss)
Para que el modelo aprenda los pesos $w$ correctos, necesitamos una métrica de error (o pérdida). En Regresión Logística usamos la **Log-Loss o Binary Cross-Entropy Loss**:

$$ L(y, \hat{y}) = - \left( y \log(\hat{y}) + (1 - y) \log(1 - \hat{y}) \right) $$

- Si la clase real es $y=1$, la pérdida es $- \log(\hat{y})$. Queremos que la probabilidad predicha $\hat{y}$ sea lo más cercana a 1 posible.
- Si la clase real es $y=0$, la pérdida es $- \log(1 - \hat{y})$. Queremos que $\hat{y}$ sea lo más cercana a 0 posible.
- Penaliza fuertemente a las predicciones incorrectas pero con alta confianza.

### Stochastic Gradient Descent (SGD)
Para minimizar esta pérdida, usamos Descenso de Gradiente.
1. **Gradient Descent Clásico**: Calcula el gradiente de la pérdida usando *todos* los datos antes de dar un paso para ajustar los pesos $w$. Es lento y costoso para datasets inmensos.
2. **Stochastic Gradient Descent (SGD)**: Actualiza los pesos $w$ usando *un solo ejemplo* o un *pequeño batch* de ejemplos a la vez. Es mucho más rápido, y aunque da "pasos ruidosos", logra converger eficientemente.

> Se aprende sobre una muestra, la pérdida sobre esa muestra es la aproximada para el dataset.

## 4. Entrenamiento y Visualización del Descenso de Gradiente

Para ver esto en acción, usaremos un vectorizador Bag of Words clásico y la clase `SGDClassifier` de Scikit-Learn.

`SGDClassifier` nos permite indicarle la función de pérdida `loss='log_loss'`, lo que matemáticamente equivale a entrenar una Regresión Logística, pero utilizando el algoritmo SGD puro. Lo interesante es que nos permite usar `partial_fit` para simular el entrenamiento época a época y registrar cómo disminuye la pérdida (Loss).


```python
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.linear_model import SGDClassifier
from sklearn.metrics import log_loss

# 1. Vectorizamos usando Bag of Words (max_features para no explotar memoria)
vectorizer = CountVectorizer(max_features=5000, ngram_range=(1,2))
X_train_vec = vectorizer.fit_transform(X_train)
X_test_vec = vectorizer.transform(X_test)

# 2. Inicializamos SGDClassifier
# learning_rate='constant', eta0=0.01 es un buen punto de partida para visualizar SGD
clf_sgd = SGDClassifier(loss='log_loss', learning_rate='constant', eta0=0.01, random_state=42)

# Parámetros de entrenamiento
epocas = 50
classes = np.array([0, 1])

train_losses = []
test_losses = []

# 3. Entrenamos época por época usando partial_fit
for epoca in range(epocas):
    clf_sgd.partial_fit(X_train_vec, y_train, classes=classes)

    # Guardamos la pérdida (Log-Loss) actual midiendo contra Train y Test
    prob_train = clf_sgd.predict_proba(X_train_vec)                             #perdida para set de entraenamiento
    prob_test = clf_sgd.predict_proba(X_test_vec)

    # se calcula la perdida
    train_losses.append(log_loss(y_train, prob_train))
    test_losses.append(log_loss(y_test, prob_test))

# 4. Graficamos la Curva de Pérdida
fig_loss, ax_loss = plt.subplots(figsize=(10, 5))
ax_loss.plot(range(1, epocas + 1), train_losses, label='Train Loss', color='blue', marker='o', markersize=3)
ax_loss.plot(range(1, epocas + 1), test_losses, label='Test Loss', color='orange', marker='s', markersize=3)
ax_loss.set_title('Convergencia de la Cross-Entropy Loss usando SGD')
ax_loss.set_xlabel('Época (Pasos de optimización sobre el dataset)')
ax_loss.set_ylabel('Binary Cross-Entropy (Log-Loss)')
ax_loss.legend()
ax_loss.grid(True, linestyle='--', alpha=0.6)

plt.show()
```

![[Aux_3_Regresion_Logistica_10_0.png]]

¿Cómo saber en qué punto parar?
Pues los datos de test en este gráfico paran de mejorar significativamente.

La pérdida es qué tan seguro está el modelo en cada predicción.

La función de pérdida puede tener cualquier forma, entonces si se tiene un gap muy grande, se puede 'pasar' de la pérdida mínima y si el gap es muy pequeño, el entrenamiento durará demasiado tiempo. Lo que algunas formas de entrenamiento usan es asumir una forma de potencial (U) y usar pasos logarítmicos para acercarse al punto mínimo.

Como podemos observar en la curva, el optimizador comienza con un nivel de error alto y, en cada época, ajusta los pesos de nuestro clasificador lineal hasta estancarse (convergencia).

A continuación, vamos a revisar el rendimiento final de este modelo en nuestros datos de prueba.


```python
from sklearn.metrics import classification_report, ConfusionMatrixDisplay

y_pred_sgd = clf_sgd.predict(X_test_vec)

print("Reporte de Clasificación (SGD Regresión Logística):")
print(classification_report(y_test, y_pred_sgd, target_names=['No Odio', 'Odio']))

ConfusionMatrixDisplay.from_predictions(
    y_test, y_pred_sgd, display_labels=['No Odio', 'Odio'], cmap='Blues'
)
plt.show()
```

    Reporte de Clasificación (SGD Regresión Logística):
                  precision    recall  f1-score   support
    
         No Odio       0.67      0.80      0.73       887
            Odio       0.77      0.62      0.69       913
    
        accuracy                           0.71      1800
       macro avg       0.72      0.71      0.71      1800
    weighted avg       0.72      0.71      0.71      1800
    

![[Aux_3_Regresion_Logistica_13_1.png]]


## 5. Interpretación: ¿Qué aprendió el modelo?

A diferencia de los modelos de Deep Learning donde es difícil interpretar internamente por qué deciden algo, la Regresión Logística es muy transparente.

El modelo aprendió un peso (coeficiente) $w_i$ para cada token de nuestro vocabulario.
- Si el peso es **positivo y grande**, indica que la palabra suma muchos puntos para que la clase sea 1 (Odio).
- Si el peso es **negativo y grande**, indica que la palabra empuja la predicción hacia la clase 0 (No Odio).

Visualicemos las "Features" más importantes:


```python
# Extraemos coeficientes y palabras del vocabulario
feature_names = vectorizer.get_feature_names_out()
coefs = clf_sgd.coef_[0]  # Array de pesos para la clase 1

# Ordenamos los índices de menor a mayor
sorted_indices = np.argsort(coefs)

# Las 15 más negativas (fuertemente asociadas a Clase 0)
top_negative_idx = sorted_indices[:15]
# Las 15 más positivas (fuertemente asociadas a Clase 1)
top_positive_idx = sorted_indices[-15:]

top_features_idx = np.concatenate([top_negative_idx, top_positive_idx])

top_features_names = [feature_names[i] for i in top_features_idx]
top_features_coefs = coefs[top_features_idx]

# Asignar colores (rojo para negativas, verde para positivas)
colores = ['salmon' if c < 0 else 'lightgreen' for c in top_features_coefs]

fig_coef, ax_coef = plt.subplots(figsize=(10, 8))
ax_coef.barh(top_features_names, top_features_coefs, color=colores)
ax_coef.set_xlabel('Valor del Coeficiente (Peso en Logits)')
ax_coef.set_title('Tokens más importantes aprendidos por SGDClassifier')
ax_coef.axvline(0, color='black', linewidth=1)
ax_coef.grid(axis='x', linestyle='--', alpha=0.5)

plt.show()
```

![[Aux_3_Regresion_Logistica_15_0.png]]


Vemos cómo las palabras con mayor peso positivo están claramente ligadas a insultos y lenguaje tóxico, y las negativas a temas misceláneos u opiniones que típicamente no contienen discurso de odio.



# Auxiliar 4: Modelamiento de Lenguaje, N-gramas y Predicción del Siguiente Token
##### Librerias Necesarias
```python
import os
import sys
import pandas as pd
import numpy as np
import math
import random
import time
import re
from collections import defaultdict, Counter
import spacy
```

---
Objetivos de la sesión
1. **Comprender el concepto de Modelamiento de Lenguaje**: Entender qué significa predecir el siguiente token y la regla de la cadena.
2. **Implementar modelos de N-gramas**: Construir modelos desde cero y entender el supuesto de Markov.
3. **Generar texto paso a paso**: Programar una función de decodificación (Next Token Prediction) para ver a los modelos "escribir".
4. **Evaluar con Perplexity**: Entender e implementar el cálculo de perplejidad con suavizado (Laplace smoothing).
5. **Transición a Embeddings**: Comprender las debilidades de los N-gramas (sparsity) y cómo los embeddings lo solucionan.
---
## 1. Repaso Breve: Modelo de Lenguaje y Markov

Un **Modelo de Lenguaje** asigna una probabilidad a una secuencia de palabras (o tokens) $P(w_1, w_2, ..., w_n)$.
Usando la regla de la cadena de la probabilidad, esto se descompone en:
$$P(w_1, w_2, ..., w_n) = P(w_1) P(w_2|w_1) P(w_3|w_1, w_2) ... P(w_n|w_1, ..., w_{n-1})$$

El **Supuesto de Markov** asume que la probabilidad del siguiente token depende **solamente de los $N-1$ tokens anteriores**.
- **Bigramas (N=2)**: Depende solo del token anterior. $P(w_i | w_1...w_{i-1}) \approx P(w_i | w_{i-1})$
- **Trigramas (N=3)**: Depende de los 2 anteriores. $P(w_i | w_1...w_{i-1}) \approx P(w_i | w_{i-2}, w_{i-1})$

---
## 2. Preparando los Datos (Noticias Chilenas)

Vamos a cargar el mismo corpus de **Noticias de la Radio Bío Bío** que usamos en la auxiliar de Semántica Vectorial.
Limpiaremos un poco el texto y lo dividiremos en oraciones (agregando los tokens especiales de inicio `<s>` y fin `</s>`).


```python
# Cargar los datos
print("Descargando dataset de noticias...")
dataset = pd.read_json('https://github.com/dccuchile/CC6205/releases/download/Data/biobio_clean.bz2')

# Para este ejemplo práctico de la clase, tomaremos una submuestra para no demorar la ejecución en vivo
df = dataset.sample(3000, random_state=42).copy()

# Extraemos el contenido
textos = df['content'].tolist()
print(f"✅ Cargadas {len(textos)} noticias.")
```

    Descargando dataset de noticias...
    ✅ Cargadas 3000 noticias.



```python
# Función simple de preprocesamiento y tokenización
def preprocesar(texto):
    # Pasar a minúsculas
    texto = texto.lower()
    # Separar por puntos para tener "oraciones"
    oraciones_crudas = texto.split('.')

    oraciones_procesadas = []
    for oracion in oraciones_crudas:
        # Mantener solo palabras (alfanuméricos)
        tokens = re.findall(r'\b\w+\b', oracion)
        if len(tokens) > 3: # Solo consideramos oraciones con algo de contenido
            # Agregamos tokens especiales
            tokens = ['<s>'] + tokens + ['</s>']
            oraciones_procesadas.append(tokens)
    return oraciones_procesadas

todas_las_oraciones = []
for t in textos:
    todas_las_oraciones.extend(preprocesar(t))

print(f"Ejemplo de oración tokenizada:\n{todas_las_oraciones[0]}")
print(f"\nTotal de oraciones extraídas: {len(todas_las_oraciones)}")
```

    Ejemplo de oración tokenizada:
    ['<s>', 'el', 'vicepresidente', 'de', 'estados', 'unidos', 'mike', 'pence', 'habló', 'este', 'martes', 'por', 'teléfono', 'con', 'el', 'presidente', 'de', 'la', 'asamblea', 'nacional', 'de', 'venezuela', 'juan', 'guaidó', 'para', 'elogiar', 'su', 'valiente', 'liderazgo', 'tras', 'ser', 'detenido', 'brevemente', 'el', 'fin', 'de', 'semana', 'por', 'agentes', 'de', 'inteligencia', 'del', 'gobierno', 'de', 'nicolás', 'maduro', '</s>']
    
    Total de oraciones extraídas: 40791


---
## 3. Construyendo N-gramas desde Cero

Ahora contaremos las ocurrencias de secuencias de tamaño N en nuestro corpus.
Para un **Bigrama** $(w_{i-1}, w_i)$, la probabilidad condicional empírica es:
$$P(w_i | w_{i-1}) = \frac{Count(w_{i-1}, w_i)}{Count(w_{i-1})}$$


```python
# Contadores
unigram_counts = Counter()
bigram_counts = Counter()
trigram_counts = Counter()

# Recorremos el corpus y contamos
for oracion in todas_las_oraciones:
    for i in range(len(oracion)):
        unigram_counts[oracion[i]] += 1

        if i < len(oracion) - 1:
            bigram_counts[(oracion[i], oracion[i+1])] += 1

        if i < len(oracion) - 2:
            trigram_counts[(oracion[i], oracion[i+1], oracion[i+2])] += 1

vocabulario = set(unigram_counts.keys())
V = len(vocabulario)

print(f"Tamaño del Vocabulario: {V}")
print(f"Total de unigramas distintos: {len(unigram_counts)}")
print(f"Total de bigramas distintos: {len(bigram_counts)}")
print(f"Total de trigramas distintos: {len(trigram_counts)}")
```

    Tamaño del Vocabulario: 52545
    Total de unigramas distintos: 52545
    Total de bigramas distintos: 389998
    Total de trigramas distintos: 768161



```python
# Función para obtener probabilidad SIN smoothing
def prob_bigrama(w1, w2):
    if unigram_counts[w1] == 0:
        return 0
    return bigram_counts[(w1, w2)] / unigram_counts[w1]

def prob_trigrama(w1, w2, w3):
    if bigram_counts[(w1, w2)] == 0:
        return 0
    return trigram_counts[(w1, w2, w3)] / bigram_counts[(w1, w2)]

print("Ejemplos de probabilidades calculadas:")
print(f"P('gobierno' | 'el') = {prob_bigrama('el', 'gobierno'):.4f}")
print(f"P('presidente' | 'el') = {prob_bigrama('el', 'presidente'):.4f}")
print(f"P('perro' | 'el') = {prob_bigrama('el', 'perro'):.4f}")
```

    Ejemplos de probabilidades calculadas:
    P('gobierno' | 'el') = 0.0228
    P('presidente' | 'el') = 0.0272
    P('perro' | 'el') = 0.0006


---
## 4. Predicción del Siguiente Token (Next Token Prediction)

Vamos a hacer que nuestro modelo "hable". Le daremos un contexto y dejaremos que prediga el siguiente token muestreando de las probabilidades que calculó. Utilizaremos un retardo visual para simular cómo el modelo va "escribiendo" token a token.


```python
# Pre-calculamos las probabilidades para el generador
next_token_bi = {}
for (_w1, _w2), count in bigram_counts.items():
    if _w1 not in next_token_bi:
        next_token_bi[_w1] = {"tokens": [], "probs": []}
    next_token_bi[_w1]["tokens"].append(_w2)
    next_token_bi[_w1]["probs"].append(count / unigram_counts[_w1])

def generar_texto_bigrama(max_tokens=20, retardo=0.0):
    context = '<s>'
    generado = []

    for _ in range(max_tokens):
        if context not in next_token_bi:
            break

        candidatos = next_token_bi[context]["tokens"]
        probs = next_token_bi[context]["probs"]

        # Muestreamos el siguiente token basado en la distribución de probabilidad
        siguiente = random.choices(candidatos, weights=probs, k=1)[0]

        if siguiente == '</s>':
            break

        generado.append(siguiente)
        context = siguiente

        # Retardo para efecto visual de "escritura"
        if retardo > 0:
            print(siguiente, end=" ", flush=True)
            time.sleep(retardo)

    if retardo > 0:
        print("") # Salto de línea final
    return " ".join(generado)

print("--- Texto Generado (Modelo Bigrama) ---")
for _ in range(3):
    # Usamos retardo 0.1 para que se vea como máquina de escribir en vivo
    print("🤖: ", end="")
    generar_texto_bigrama(retardo=0.1)
```

    --- Texto Generado (Modelo Bigrama) ---
    🤖: las fronteras de gendarmería cuando pidió quedarse de las clases en la mitad independentistas de pequeña llegó hasta que el 
    🤖: la víspera a permanecer refugiados entre 1972 
    🤖: república y energía y familiares habían sido víctimas debió ser declarada completamente frontera 


> [!TIP]
> Nota cómo el texto de Bigramas tiene sentido "local" (palabras contiguas calzan bien) pero frecuentemente pierde el sentido "global". El modelo no tiene memoria a largo plazo porque olvida de qué estaba hablando hace 2 palabras. Aumentar a Trigramas o usar LLMs modernos soluciona esto.

---
## 5. Evaluando el Modelo: Perplexity (Perplejidad) con Smoothing

La Perplejidad nos dice qué tan "sorprendido" está el modelo al leer un texto de prueba. **A menor perplejidad, mejor.**

Si el modelo nunca vio la frase "el can" en el entrenamiento, $P(can|el) = 0$. Esto arruina el cálculo (sorpresa infinita). Para evitar esto usamos **Laplace Smoothing (Suavizado aditivo)**, sumando 1 al conteo del numerador, y $V$ (tamaño del vocabulario) al denominador.

$$P_{Laplace}(w_i | w_{i-1}) = \frac{Count(w_{i-1}, w_i) + 1}{Count(w_{i-1}) + V}$$


```python
def calcular_perplejidad_bigrama(oracion_tokens):
    N = len(oracion_tokens)
    if N <= 1:
        return 0

    log_prob_sum = 0

    for i in range(1, N):
        w_prev = oracion_tokens[i-1]
        w_curr = oracion_tokens[i]

        count_bg = bigram_counts.get((w_prev, w_curr), 0)
        count_ug = unigram_counts.get(w_prev, 0)

        # Laplace Smoothing
        prob = (count_bg + 1) / (count_ug + V)
        log_prob_sum += math.log2(prob)

    l = (1 / N) * log_prob_sum
    perplexity = 2 ** (-l)
    return perplexity

oracion_real = ['<s>', 'el', 'presidente', 'de', 'la', 'república', 'anunció', 'nuevas', 'medidas', '</s>']
oracion_rara = ['<s>', 'el', 'la', 'que', 'con', 'para', 'computador', 'perro', '</s>']

print(f"Perplejidad de oración con sentido:   {calcular_perplejidad_bigrama(oracion_real):.2f}")
print(f"Perplejidad de oración sin sentido: {calcular_perplejidad_bigrama(oracion_rara):.2f}")
```

    Perplejidad de oración con sentido:   435.82
    Perplejidad de oración sin sentido: 1695.28


---
## 6. Bonus 1: Conectando con LLMs Modernos (Demo en Colab con GPU)

Los modelos actuales como GPT o LLaMA hacen exactamente lo mismo que acabamos de programar: **predecir el siguiente token**. La gran diferencia es que en lugar de usar un simple contador de N-gramas, usan Redes Neuronales (Transformers) y un contexto larguísimo (miles de palabras en vez de $N-1$).



```python
# Ejemplo de código para correr en Colab usando GPU (T4):
!pip install transformers
from transformers import pipeline

generador = pipeline('text-generation', model='DeepESP/gpt2-spanish')
respuesta = generador("El gobierno anunció hoy", max_length=50)
```

```python
print(respuesta[0]['generated_text'])
```

    El gobierno anunció hoy el envío de las tropas de asalto. 
    
    El general se volvió hacia mí. 
    
    —Es un buen hombre, señor. En cuanto a los recursos, no creo que llegue a la altura de los recursos. 
    
    —A la altura de los recursos —contesté. 
    
    —Pero, señor —prosiguió el general—, usted sabe perfectamente que la acción de los soldados es el mayor desafío, y que no debemos emplear las fuerzas que nos atañen a nosotros mismos. 
    
    —Y, además, ha dado una gran importancia a sus recursos, señor —dije yo. 
    
    —Y que, puesto que es usted un hombre de valor, no le agradaría que usted se viera obligado a emplear la fuerza de sus tropas para la defensa de la ciudad. 
    
    —Señor, —exclamé— ¿es usted tan buen hombre como para arriesgarse a un ataque a gran escala? 
    
    —Un hombre de valor, señor —respondió el general— ¡Y qué bien sabe usted de valor! 
    
    —Lo mismo digo, señor —contesté. 
    
    —No, no lo es. 
    
    —Pues me acuerdo. 
    
    —¿Y? 
    
    —Que usted no tiene nada que temer, señor general —dijo el general. 
    
    —


---
## 7. Bonus 2: De N-gramas a Embeddings (El problema de la "Sparsity")

El gran problema de los N-gramas es la **"Sparsity" (escasez)** de los datos.
Si el modelo entrenó con `"el perro ladra"` pero nunca vio `"el can ladra"`, nuestro N-grama le da probabilidad (casi) cero a la segunda. ¡El N-grama no sabe que "perro" y "can" son sinónimos!

**¿Cómo lo resuelven los modelos neuronales?** Con **Embeddings**.
En vez de ver las palabras como entes discretos e independientes, las mapean a un espacio vectorial continuo donde palabras con significado similar están cerca.


```python
try:
    # Try to load the medium Spanish model, which includes word vectors
    nlp_spacy = spacy.load("es_core_news_md")
except:
    print("Descargando modelo de spaCy (es_core_news_md). Esto puede tomar unos minutos...")
    import subprocess
    subprocess.run([sys.executable, "-m", "spacy", "download", "es_core_news_md"])
    nlp_spacy = spacy.load("es_core_news_md")

# Obtenemos los vectores (embeddings) de las palabras
w1 = nlp_spacy("perro")
w2 = nlp_spacy("perrito")
w3 = nlp_spacy("mesa")
w4 = nlp_spacy("gato") # Add gato for direct comparison as per original warning

print("\n--- Similitud Semántica (Usando Embeddings) ---")
print(f"Similitud entre 'perro' y 'can':  {w1.similarity(w2):.4f}")
print(f"Similitud entre 'perro' y 'gato':   {w1.similarity(w4):.4f}") # Compare perro with gato
print(f"Similitud entre 'perro' y 'mesa':  {w1.similarity(w3):.4f}")

print("\n💡 En las próximas clases verán cómo los Modelos Neuronales aprovechan esta similitud para generalizar el lenguaje de forma que los N-gramas clásicos nunca pudieron. 🚀")
```

    
    --- Similitud Semántica (Usando Embeddings) ---
    Similitud entre 'perro' y 'can':  1.0000
    Similitud entre 'perro' y 'gato':   0.8487
    Similitud entre 'perro' y 'mesa':  0.0786
    
    💡 En las próximas clases verán cómo los Modelos Neuronales aprovechan esta similitud para generalizar el lenguaje de forma que los N-gramas clásicos nunca pudieron. 🚀

# Clase 5

## Word Meaning

Idea: When you don't know the meaning of the word, you look it up on a dictionary.
- In humans you can get the meaning 

But how can we represent word meaning computationally?
For example: Mouse
1. a rodent
2. a hand-operated computer device.

A measure for two words having similar meaning is synonymity.
Theres is also antonyms,
relatedness: A semantic relationship between words (ex: relatedness between 'hospital' dworlds like doctor, nurse, etc.
Connotation: The affective, social or cultural associations of a word (ex: trash of a household, and trash as of a depective word for a human being).

### Synonymy

## Word Similarity
Words with similar meaning but they are not necesarrily synonyms, they share some elements of meaning like Car and bicycle.

> Similar meaning != synonymy

Similar meanings are words that are not necessarily synonyms but share some elements of meaning.


## Computational approach to word meaning

A model about word meaning es **vector semantics**

The idea is that words that are close in a multidimensional space diagram, they are closer in meaning. They form clusters of words that give similar meaning or are related.

> "You shall know a word by the company it keeps" - J.R. Firth

A similar approach was Bag-of-Words but it didnt get the context of the words, just the number of ocurrences.

**Co-currence Matrix** gives sparse word vectors, for example $[0,1670,1683,85,5,4,0,0,0,0,0,0,0,0,0,\dots]$ and have  alot of `0`. This translates into a large amount of computation.

---

Dot product and cosine

the most common similarity measure in NLP is the cosine similarity, based on the dot product.
It produces a scalar that tends to be high when the two vectores have large values in the same dimensions.
\* If they dont overlap (i.e., are orthogonal) then $v\cdot w=0$

$$
cosine(x,y)=\frac{x\cdot y}{|x||y|}
$$
\*denominator normalizes dot product.

and
* -1 vectors point in the **opposite** directions
* +1 same direction
* 0: orthogonal direction.

Words with similar meanings tend to point in similar directions.
\* The magnitude can be different, but it doesnt matter much so that is why the dot product is normalized.

$$
\cos(\vec{v},\vec{w})=\frac{\vec{v}\cdot \vec{w}}{|\vec{v}||\vec{w}|}= \frac{\sum_{i=1}^{N}v_{i}w_{i}}{\sqrt{ \sum_{i=1}^{N}v_{i}^{2}}\sqrt{ \sum_{i=1}^{N}w_{i}^{2} }}
$$


--- 
Example:



### Dense Representations

The representation can have a lot of dimensions. 

\* In order to apply Naive Bayes and Logistic Regression there is a 'pipeline'.
1. the input



Features: the proper characteristics that the machine uses to learn patterns in order to do the predictions.

In this method, the feature are the number of ocurrences.

## Word2Vec

It has two variants



### Skip-gram

We apply the idea of logistic regression: to learn the features that distinguish the classes.
We get:
1. Positive examples, words that actually occur together
   $$
   (w,c)\to 1
   $$
   and they are an observed context pair
2. Negative examples, randomly sampled words
   $$
   (w,c) \to 0
   $$
   an unlikely context pair.


