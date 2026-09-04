# 📊 Proyecto EDA: Análisis Exploratorio de Campañas de Marketing Bancario

## 📝 Descripción del Proyecto
Este proyecto realiza un Análisis Exploratorio de Datos (EDA) sobre las campañas de marketing directo de una institución bancaria portuguesa. El objetivo principal es identificar el perfil de los clientes y las variables socioeconómicas o de contacto que influyen en la contratación de un producto de depósito a plazo bancario (`y`).

---

## 🛠️ Herramientas y Librerías Utilizadas
- **Lenguaje:** Python
- **Entorno de desarrollo:** Visual Studio Code & Jupyter Notebooks
- **Librerías principales:**
  - `pandas`: Carga, manipulación y limpieza de datos.
  - `numpy`: Cálculo de métricas estadísticas.
  - `matplotlib` & `seaborn`: Visualización de datos y gráficos exploratorios.
  - `openpyxl`: Lectura de datos estructurados en formato Excel.

---

## 📁 Estructura del Repositorio

- **`data/raw/`**: Datos brutos de origen (CSV y Excel sin modificar).
- **`data/processed/`**: Dataset final unificado y limpio (`bank_cleaned.csv`).
- **`notebooks/01_limpieza_y_union.ipynb`**: Fase de ETL, fusión y tratamiento de nulos.
- **`notebooks/02_eda_visualizacion.ipynb`**: Fase de análisis descriptivo y visualización.
- **`README.md`**: Informe final del proyecto e insights de negocio.

---

## ⚙️ Pasos de Limpieza y Transformación de Datos (ETL)
En la primera fase del proyecto (`01_limpieza_y_union.ipynb`), se han completado los siguientes pasos:

1. **Unificación de datos de origen:**
   - Se leyeron y concatenaron las 3 hojas del archivo `customer-details.xlsx` en un único DataFrame de clientes.
   - Se unificó el dataset bancario (`bank-additional.csv`) con el dataset de clientes utilizando sus identificadores únicos (`id_` e `ID`) mediante un *inner join*.

2. **Verificación de duplicados y limpieza:**
   - Se comprobó la presencia de registros duplicados en el conjunto unificado (0 duplicados encontrados).
   - Se eliminaron columnas redundantes de ID tras el proceso de unión.

3. **Tratamiento de Tipos de Datos y Valores Faltantes (Nulos):**
   - **Variables Numéricas (`age`, `euribor3m`, `cons.price.idx`):** Se forzó su conversión a tipo numérico para corregir inconsistencias de formato y se imputaron sus valores nulos utilizando la **mediana** para no distorsionar las distribuciones con valores extremos.
   - **Variables Categóricas (`job`, `marital`, `education`, `default`, `housing`, `loan`):** Se imputaron los registros ausentes mediante la categoría `'Unknown'`.
   - **Registros con fecha ausente:** Se descartaron las filas sin registro de fecha (`date`), afectando a menos del 0.6% del total de registros.

4. **Exportación del Dataset Procesado:**
   - El conjunto final limpio consta de más de 42,000 registros y 30 columnas, guardado en `data/processed/bank_cleaned.csv`.

---

## 📈 Análisis Exploratorio de Datos (EDA) e Insights

En la segunda fase del proyecto (`02_eda_visualizacion.ipynb`), se analizaron los patrones de comportamiento de los clientes y los factores clave de éxito de las campañas:

### 1. Tasa de Conversión Global
- **Rendimiento de la campaña:** De los 42,752 clientes analizados, un **11.3%** (4,811 clientes) aceptó contratar el depósito a plazo, mientras que el **88.7%** restante rechazó la oferta.
- **Conclusión:** Existe un marcado desbalanceo de clases, habitual en campañas de marketing directo, lo que requiere focalizar esfuerzos en los perfiles de mayor respuesta.

### 2. Perfil Socio-Demográfico del Cliente
- **Profesión (`job`):**
  - **Top Conversión:** Los **estudiantes (31.4%)** y los **jubilados (25.3%)** presentan las mayores tasas de aceptación, triplicando y duplicando la media general de la campaña, respectivamente.
  - **Baja Conversión:** El sector *blue-collar* (operarios y trabajadores manuales) registra el menor rendimiento con una conversión del **6.9%**.
- **Edad (`age`):**
  - La contratación se concentra principalmente en los extremos de edad: jóvenes (estudiantes) y personas mayores de 60 años (jubilados), quienes disponen de mayor liquidez o interés en productos de ahorro garantizados.

### 3. Factores Operativos y de Contacto
- **Duración de la Llamada (`duration`):**
  - Se identificó una relación fuertemente positiva entre la duración de la interacción telefónica y la contratación del depósito. Las llamadas con conversión exitosa presentan tiempos de conversación significativamente más largos.
- **Canal de Comunicación (`contact`):**
  - El contacto a través de teléfono móvil (*cellular*) muestra una efectividad notablemente superior frente al teléfono fijo tradicional (*telephone*).

---

## 🚀 Recomendaciones Estratégicas de Negocio

1. **Segmentación Prioritaria:** Rediseñar la asignación de base de datos priorizando a los segmentos de **jubilados** y **estudiantes**, donde la tasa de éxito justifica un mayor presupuesto comercial.
2. **Optimización del Discurso Comercial:** Capacitar al equipo de telemarketing para retener la atención del cliente durante los primeros minutos de la llamada, ya que superar el umbral promedio de tiempo incrementa exponencialmente las probabilidades de conversión.
3. **Canalización Digital/Móvil:** Migrar los esfuerzos de contacto hacia telefonía móvil y canales digitales, reduciendo la dependencia del teléfono fijo tradicional.
