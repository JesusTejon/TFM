# Identificación y Clasificación de Sexismo en Memes (EXIST 2026)

Este repositorio contiene el código fuente desarrollado para el Trabajo Fin de Máster titulado **"Identificación y Clasificación Multi-Etiqueta de Sexismo en Memes mediante Arquitecturas Híbridas de Visión-Lenguaje y Datos de Sensores"**. 

El proyecto ha sido desarrollado en la Escuela Técnica Superior de Ingeniería (ETSI) de la Universidad de Huelva (UHU), dentro del grupo de investigación Ingeniería de la Información y el Conocimiento (I2C).

## 📌 Descripción del Proyecto

El objetivo de este trabajo es proponer e implementar sistemas de Inteligencia Artificial capaces de detectar y clasificar contenido sexista y discurso de odio en memes de redes sociales. Para abordar la extrema complejidad semántica, la ironía y la subjetividad de estos formatos, el proyecto se enmarca en el reto internacional **EXIST 2026** y utiliza un enfoque multimodal innovador que combina:
* **Procesamiento de Lenguaje Natural (NLP):** Extracción de texto mediante OCR.
* **Visión por Computador:** Análisis semántico de la imagen.
* **Computación Afectiva:** Integración pionera de bioseñales fisiológicas (Electroencefalografía - EEG, Eye-Tracking - ET y Frecuencia Cardíaca - HR) registradas durante la visualización del meme.

## 📂 Estructura del Repositorio y Arquitecturas

El código fuente está dividido en tres archivos principales, correspondientes a los tres enfoques arquitectónicos investigados en el TFM:

### 1. `5-fold` (Arquitectura 1: Fusión Temprana y Ensemble K-Fold)
Implementa un paradigma de *Early Fusion*. Concatena las características extraídas (embeddings textuales de Twitter-RoBERTa, visuales de CLIP y el vector de bioseñales) en un único vector denso multimodal.
* **Mecanismo:** Entrena una red neuronal (Perceptrón Multicapa) utilizando validación cruzada estratificada (5-Fold).
* **Decisión:** Votación suave (*Soft Voting*) basada en el promedio de las probabilidades de los 5 modelos base.

### 2. `softlabel` (Arquitectura 2: Fusión Tardía por Soft-labels)
Desarrolla un sistema descentralizado de fusión tardía (*Late Fusion*). Entrena cuatro redes neuronales especializadas de forma totalmente independiente:
* Un modelo bimodal (Visión-Lenguaje).
* Tres modelos unimodales para sensores (EEG, HR, ET).
* **Mecanismo:** Fusión matemática ponderada de las distribuciones de probabilidad continuas (*soft-labels*) de cada torre. Destaca la configuración óptima empírica del sistema aislando la respuesta cognitiva (70% Visión-Lenguaje / 30% EEG).

### 3. `llm` (Arquitectura 3: Sistema Multi-Agente con LLMs)
Implementa un estudio exploratorio innovador bajo el paradigma *"LLM-as-a-Judge"* (Zero-Shot Learning), sin entrenamiento de pesos neuronales.
* **Analistas Paralelos:** Dos agentes de visión y lenguaje (LLaMA-3.2-Vision) configurados mediante *prompting* avanzado con roles opuestos (umbral restrictivo vs. umbral sensible).
* **Juez Central:** Un modelo de texto (Qwen-2.5) que actúa como árbitro neutral. Audita los razonamientos textuales de los analistas y emite el veredicto definitivo por consenso, superando en rendimiento a las aproximaciones clásicas.

## 🛠️ Tecnologías y Requisitos

El código está desarrollado íntegramente en Python (3.10) y hace uso de las siguientes tecnologías y librerías principales:
* `PyTorch`: Construcción y entrenamiento de redes neuronales.
* `Transformers` (Hugging Face): Modelos fundacionales CLIP y Twitter-RoBERTa.
* `Ollama`: Ejecución local y eficiente de los Grandes Modelos de Lenguaje (LLaMA-3.2-Vision y Qwen-2.5).
* `Optuna`: Optimización bayesiana de hiperparámetros.
* `Scikit-learn`, `Pandas`, `Matplotlib` y `Seaborn`: Procesamiento de datos y evaluación de métricas.

## ✒️ Autoría y Reconocimientos
* **Autor:** Jesús Tejón Carrillo
* **Tutores:** Jacinto Mata Vázquez y Victoria Pachón Álvarez
* **Institución:** Universidad de Huelva (UHU) - Grupo I2C

Los resultados de la Arquitectura 3 han sido presentados en la *Final Conference NONCONSPIRAHATE Project: Conspiracy theories, online hate speech and disinformation* (Junio 2026).

El dataset de entrenamiento ha sido ofrecido por el reto internacional EXIST 2026.
