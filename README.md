# 🧠 CNN para Clasificación de Imágenes – CIFAR-10

> **Proyecto Final – Red Neuronal Convolucional en TensorFlow/Keras**

Este proyecto implementa una **Red Neuronal Convolucional (CNN)** diseñada para clasificar imágenes del dataset **CIFAR-10**. El flujo de trabajo abarca desde el preprocesamiento y la aumentación de datos hasta la construcción, entrenamiento y evaluación del modelo.

---

## 📌 Características del Proyecto

* **Dataset:** Uso estándar de CIFAR-10 (60.000 imágenes, 10 clases).
* **Preprocesamiento:** Normalización de imágenes.
* **Data Augmentation:** Implementado para reducir el sobreajuste (overfitting).
* **Arquitectura Robusta:** 3 bloques convolucionales con Batch Normalization, MaxPooling y Dropout.
* **Optimización:** Entrenamiento con Adam y `categorical_crossentropy`.
* **Early Stopping:** Detención temprana para evitar el sobreentrenamiento.
* **Evaluación:** Métricas detalladas, curvas de aprendizaje y matriz de confusión.

---

## 🗂 Dataset: CIFAR-10

El conjunto de datos consta de imágenes a color de **32x32 píxeles**.

* **Volumen:** 60.000 imágenes en total.
    * 50.000 para Entrenamiento + Validación.
    * 10.000 para Test.
* **Clases (10):**
    `airplane`, `automobile`, `bird`, `cat`, `deer`, `dog`, `frog`, `horse`, `ship`, `truck`.

---

## 🏗 Arquitectura del Modelo

El modelo sigue una estructura secuencial con capas de aumento de datos al inicio:

### 🔹 Preprocesamiento
* **Data Augmentation:** `RandomFlip`, `RandomRotation`, `RandomZoom`.

### 🔹 Bloque 1
* `Conv2D` (32 filtros)
* `BatchNorm`
* `Conv2D` (32 filtros)
* `MaxPooling`
* `Dropout` (0.2)

### 🔹 Bloque 2
* `Conv2D` (64 filtros)
* `BatchNorm`
* `Conv2D` (64 filtros)
* `MaxPooling`
* `Dropout` (0.3)

### 🔹 Bloque 3
* `Conv2D` (128 filtros)
* `BatchNorm`
* `MaxPooling`
* `Dropout` (0.4)

### 🔹 Clasificación (Top)
* `Flatten`
* `Dense` (128) + Regularización L2 + `Dropout`
* `Dense` (10, activación `softmax`)

---

## ⚙️ Entrenamiento

El modelo se compila y entrena con la siguiente configuración:

```python
model.compile(
    optimizer='adam',
    loss='categorical_crossentropy',
    metrics=['accuracy']
)
```

- **Optimizador:** Adam
- **Función de Pérdida:** Categorical Crossentropy (multiclase)
- **Callbacks:**
  - **EarlyStopping:** Monitorea `val_loss` con una paciencia de 10 épocas y restaura los mejores pesos (`restore_best_weights=True`)

## 📊 Resultados

El rendimiento del modelo en el conjunto de prueba (Test Set) fue el siguiente:

| Métrica | Valor |
|---------|-------|
| Accuracy Test | 74.21% |
| Loss Test | 0.9066 |

### 📝 Interpretación:

El modelo acierta aproximadamente **3 de cada 4 imágenes** que nunca ha visto antes. Un loss de 0.90 se considera un valor intermedio y aceptable para modelos iniciales en CIFAR-10 (típicamente entre 0.7 y 1.2).

## 📈 Gráficos Generados

El notebook incluye la generación de las siguientes visualizaciones para el análisis:

- **Curva de Accuracy:** Entrenamiento vs. Validación
- **Curva de Loss:** Entrenamiento vs. Validación
- **Matriz de Confusión:** Para identificar en qué clases falla más el modelo

## 🛠 Instalación y Uso

### 1. Clonar el repositorio
```bash
git clone https://github.com/mnahuelanca/TpFinalDesarrolloIA
```

### 2. Instalar dependencias
```bash
pip install -r requirements.txt
```


### 3. Ejecutar el proyecto

Puedes ejecutar el notebook directamente:
```bash
python index.ipynb
```

O abrirlo mediante **Jupyter Notebook** o **Google Colab**.

## 📦 Requisitos

- tensorflow
- numpy
- matplotlib
- scikit-learn
- seaborn
