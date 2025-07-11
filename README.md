# MSI-608
# Proyecto 1: Análisis de Factores Asociados al Riesgo de Enfermedades Crónicas

Este repositorio contiene un script de Python generado a partir de un Notebook de Colab que realiza un análisis y predicción de factores asociados al riesgo de enfermedades crónicas utilizando PySpark, pandas, scikit-learn y diversas técnicas de visualización.

## Requisitos

* **Python 3.8+**
* **Java 8+** (para ejecutar PySpark)
* **Dependencias** (puedes instalarlas con pip):

  ```bash
  pip install pyspark imblearn pandas numpy scipy matplotlib seaborn scikit-learn
  ```

## Estructura de Archivos

```plaintext
├── Proyecto 1.py          # Script principal de análisis y modelado
├── dataset_elpino.csv     # Datos clínicos del Hospital El Pino
├── CIE_9.csv              # Catálogo de códigos de procedimientos (CIE-9)
├── CIE_10.csv             # Catálogo de códigos de diagnósticos (CIE-10)
├── requirements.txt       # Dependencias del proyecto
```

> **Nota:** `requirements.txt` puede crearse con:
>
> ```bash
> pip freeze > requirements.txt
> ```

## Uso

1. **Clona el repositorio** y accede al directorio:

   ```bash
   git clone <URL-del-repositorio>
   cd <nombre-del-repositorio>
   ```
2. **Entorno virtual**:

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```
3. **Instala las dependencias**:

   ```bash
   pip install -r requirements.txt
   ```
4. **Ejecuta el script**:

   ```bash
   python "Proyecto 1.py"
   ```

## Descripción del Flujo

1. **Configuración y dependencias**: Importa paquetes y configura PySpark.
2. **Carga de datos**:

   * `dataset_elpino.csv`
   * `CIE_9.csv` (procedimientos)
   * `CIE_10.csv` (diagnósticos)
3. **Preprocesamiento**:

   * Limpieza y renombrado de columnas.
   * UDF para extraer el código principal de diagnósticos y procedimientos.
   * Clasificación etaria basada en rangos de edad (`Niñez`, `Adolescencia`, `Juventud`, `Adultez`, `Adulto Mayor`).
   * Conversión de la tabla de Spark a pandas para análisis detallado.
4. **Análisis exploratorio**:

   * Cálculo de porcentajes de valores nulos.
   * Estadísticas descriptivas de variables (edad, sexo, GRD).
   * Visualizaciones: histogramas, boxplots, gráficos de barras y mapa de calor de correlaciones utilizando V de Cramer.
5. **Modelado**:

   * Selección de variables predictoras (`Sexo_Desc`, `Diag_01_Principal_codes`, `Proced_01_Principal_codes`, `Edad_grupo`).
   * Filtrado de las 50 GRD más frecuentes o inclusión de clases con al menos 2 muestras.
   * División en conjuntos de entrenamiento y prueba (80/20) con estratificación.
   * Oversampling de clases minoritarias (`RandomOverSampler`).
   * Pipelines de scikit-learn que combinan `OneHotEncoder` y clasificadores:

     * **Logistic Regression**
     * **Random Forest**
     * **Gradient Boosting**
     * **Neural Network (MLPClassifier)**
   * Evaluación con **accuracy**, **precision**, **recall**, **F1-score** y matrices de confusión (Top 3 GRD más frecuentes).
6. **Resultados**:

   * Impresión de métricas de desempeño para cada modelo.
   * Visualización de matrices de confusión para las tres GRD más frecuentes.
