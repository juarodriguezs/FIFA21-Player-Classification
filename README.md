# ⚽ FIFA21 Player Classification (Decision Tree & Bayesian Classifier)

Este proyecto aplica técnicas de **aprendizaje supervisado** para clasificar jugadores de fútbol según sus características técnicas, físicas y demográficas.  
El objetivo es comparar el desempeño de dos enfoques de clasificación: **Árboles de Decisión (Decision Trees)** y **Clasificación Bayesiana (Bayesian Classification)**, con el fin de analizar su capacidad para predecir categorías o roles de jugadores dentro del conjunto de datos **FIFA21**.

---

## 📘 Descripción general

El análisis se basa en el dataset **`players_21.csv`**, el cual contiene información de jugadores del videojuego FIFA 21, obtenida del portal **SoFIFA (https://sofifa.com)**.  
Cada registro representa a un jugador con atributos relacionados con su rendimiento, posición, potencial, estadísticas de juego y datos contractuales.

El proceso se desarrolla con un enfoque comparativo entre modelos de clasificación supervisada, abarcando limpieza de datos, selección de variables, entrenamiento de modelos y evaluación de desempeño.

---

## 📂 Estructura del proyecto

```plaintext
FIFA21-Player-Classification/
│
├── fifa21_player_classification.ipynb
├── data/
│ ├── players_21.csv
│ └── Summary.txt
│
└── README.md
```

---

## 📊 Descripción de los datos

El dataset **`players_21.csv`** contiene información detallada de jugadores profesionales del videojuego FIFA 21.  
Cada registro corresponde a un jugador e incluye atributos técnicos, físicos, contractuales y de rendimiento.  
Los datos fueron obtenidos de **SoFIFA (https://sofifa.com)** y se usan únicamente con fines académicos.

A continuación se presentan algunas de las variables más relevantes (ver `Summary.txt` para la descripción completa):

| Variable | Descripción |
|-----------|--------------|
| `short_name` | Nombre del jugador |
| `age` | Edad del jugador |
| `overall` | Calificación general (rendimiento actual) |
| `potential` | Potencial máximo de desarrollo |
| `value_eur` | Valor de mercado estimado (en euros) |
| `wage_eur` | Salario semanal |
| `club_position` | Posición en el club |
| `nationality` | Nacionalidad del jugador |
| `height_cm`, `weight_kg` | Altura y peso |
| `pace`, `shooting`, `passing`, `dribbling`, `defending`, `physic` | Atributos técnicos principales |

---

## 🧠 Metodología

1. **Preprocesamiento de datos**
   - Carga del dataset y exploración inicial.  
   - Eliminación de valores nulos y limpieza de datos.  
   - Codificación de variables categóricas (`LabelEncoder`, `OneHotEncoder`).  
   - Escalado de variables numéricas mediante `StandardScaler`.  
   - Selección de la variable objetivo (posición o categoría de rendimiento).

2. **División del conjunto de datos**
   - División del dataset en entrenamiento (80%) y prueba (20%) usando `train_test_split`.  
   - Uso de validación cruzada (`K-Fold`) para garantizar robustez en la evaluación.

3. **Modelos implementados**
   - **Árbol de Decisión (Decision Tree):**  
     Entrenado con distintos criterios (`gini`, `entropy`) y ajustes de hiperparámetros (`max_depth`, `min_samples_split`, `min_samples_leaf`) mediante `GridSearchCV`.  
     Permite interpretar reglas de clasificación y visualizar la jerarquía de decisiones.
   - **Clasificación Bayesiana (Bayesian Classifier):**  
     Evaluación de variantes (`GaussianNB`, `MultinomialNB`, `BernoulliNB`) según la naturaleza de las variables.  
     Basado en el teorema de Bayes, estima probabilidades condicionales de pertenencia a cada clase.

4. **Evaluación del rendimiento**
   - Métricas empleadas: **Accuracy**, **Precision**, **Recall**, **F1-score**.  
   - Visualización de la **matriz de confusión** y análisis de generalización.  
   - Comparación de resultados entre ambos modelos para determinar el mejor desempeño.

5. **Interpretación y análisis**
   - Identificación de variables con mayor peso en las predicciones (`feature_importances_`).  
   - Detección de posibles casos de sobreajuste.  
   - Análisis visual mediante gráficos de barras y mapas de calor.

---

## 📈 Resultados destacados

Los resultados se evaluaron sobre el **conjunto de prueba**, utilizando las métricas estándar de clasificación: **Accuracy**, **Precision**, **Recall** y **F1-score**.  
A continuación, se presentan los valores promedio obtenidos por cada modelo y su respectivo análisis comparativo.

| Modelo | Accuracy (Test) | Precision (Macro) | Recall (Macro) | F1-score (Macro) |
|:--------|:---------------:|:-----------------:|:---------------:|:----------------:|
| 🌳 Árbol de Decisión (Decision Tree) | **0.82** | **0.84** | **0.86** | **0.84** |
| 📊 Clasificación Bayesiana (Bayesian Classifier) | 0.75 | 0.80 | 0.79 | 0.80 |

---

### 🌳 Árbol de Decisión (Decision Tree)

- Obtuvo un **Accuracy de 0.82** en el conjunto de prueba, mostrando un **buen desempeño general**.  
- Presentó un **Precision macro de 0.84**, **Recall de 0.86** y un **F1-score de 0.84**, indicando equilibrio entre predicciones correctas y sensibilidad ante las distintas clases.  
- Comparado con el desempeño en entrenamiento (**Accuracy = 0.84**), se observó una **ligera diferencia**, lo que refleja una **mínima tendencia al sobreajuste**, bien controlada.  
- Las clases más difíciles de distinguir fueron las **0 y 3**, con un Recall menor (0.88 y 0.67 respectivamente), mientras que la clase **2** obtuvo un desempeño perfecto (1.00).  
- Las variables con mayor relevancia en las divisiones del árbol fueron:
  - `overall` (rendimiento general)  
  - `potential` (potencial de desarrollo)  
  - `age` (edad)  
  - `passing` y `defending` (atributos técnicos)

En conjunto, el Árbol de Decisión logró una **clasificación precisa y bien equilibrada**, con interpretabilidad y bajo riesgo de sobreajuste.

---

### 📊 Clasificación Bayesiana (Bayesian Classifier)

- Alcanzó un **Accuracy de 0.75** en el conjunto de prueba, con un **Precision macro de 0.80**, **Recall de 0.79** y **F1-score de 0.80**.  
- Mostró un comportamiento **más estable** entre los datos de entrenamiento (0.76) y prueba (0.75), evidenciando **buena generalización**.  
- Aunque su precisión global fue menor que la del Árbol de Decisión, el modelo fue **más robusto ante el ruido** y menos propenso al sobreajuste.  
- La clase **2** también alcanzó un desempeño perfecto (**Precision, Recall y F1-score = 1.00**), mientras que las clases **0 y 3** mostraron un rendimiento más variable.  
- La variante **GaussianNB** fue la más adecuada, dada la naturaleza continua de los atributos.  

El Clasificador Bayesiano destacó por su **simplicidad, eficiencia computacional** y comportamiento consistente, siendo una alternativa ligera y efectiva para este tipo de problema.

---

### ⚖️ Comparación general

El **Árbol de Decisión** destacó por su **alta interpretabilidad**, su capacidad para representar reglas de clasificación claras y su **buen rendimiento general**, con un Accuracy del 82% y un F1-score de 0.84 en el conjunto de prueba.  
Sin embargo, mostró una **ligera tendencia al sobreajuste** cuando el árbol se profundiza demasiado, lo que podría limitar su generalización en datasets más complejos.

Por otro lado, el **Clasificador Bayesiano** ofreció un **modelo más simple, rápido y estable**, con un Accuracy del 75% y un F1-score de 0.80.  
Aunque su rendimiento global fue algo menor, demostró una **mayor capacidad de generalización** y **robustez ante el ruido**, además de un costo computacional considerablemente más bajo.

En general, el **Árbol de Decisión** logró un mejor rendimiento en términos de **Accuracy** y **F1-score**, mientras que el **Clasificador Bayesiano** ofreció una **mayor estabilidad** y menor variabilidad entre conjuntos.  
Ambos modelos demostraron que las **técnicas supervisadas** permiten **clasificar jugadores de FIFA21** de manera efectiva, a partir de sus características técnicas y físicas.

---

## 🛠️ Tecnologías y librerías utilizadas

- **Python 3.9 o superior**
- `pandas`, `numpy`, `matplotlib`, `seaborn`
- `scikit-learn` (DecisionTreeClassifier, GaussianNB)

---

## 👥 Autores

Proyecto desarrollado colaborativamente como Microproyecto 3 del curso de **Introducción a la Inteligencia Artificial** de la Universidad Nacional de Colombia - Sede Medellín.

**Equipo 9:**

- Jacobo Ochoa Ramírez
- Juan Manuel Rodríguez Sánchez
- Luis Alejandro Varela Ojeda