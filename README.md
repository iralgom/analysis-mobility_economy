# Movilidad Urbana y Productividad Económica en Ciudades de LATAM

## Resumen Ejecutivo

Este proyecto fue desarrollado como parte de un ejercicio de análisis de datos para el American Development Bank, con el objetivo de explorar la relación entre la movilidad urbana y la productividad económica en ciudades latinoamericanas durante 2024.

A partir de datos de tráfico urbano proporcionados por TomTom Traffic Index y datos económicos de OECD Cities, se construyó un dataset integrado que permitió comparar indicadores de congestión vehicular, tiempos de viaje y retrasos con variables económicas como PIB per cápita, desempleo y población.

Los resultados muestran que las ciudades con mayor actividad económica no necesariamente presentan mejores condiciones de movilidad, evidenciando la importancia de la infraestructura de transporte como un factor relevante para la competitividad urbana.

## Objetivos del Proyecto
### Objetivo General

Construir un dataset integrado de movilidad y economía urbana para analizar posibles relaciones entre congestión vehicular y productividad económica.

### Objetivos Específicos
- Limpiar y transformar datos provenientes de distintas fuentes.
- Estandarizar formatos y estructuras de información.
- Consolidar indicadores de tráfico por ciudad.
- Integrar información económica y de movilidad.
- Explorar relaciones entre variables mediante análisis visual.
- Generar un dataset final listo para futuros análisis.

## Fuentes de Datos
### TomTom Traffic Index

Fuente de información sobre movilidad urbana en tiempo real.

Variables utilizadas:

- Traffic Index
- Jams Delay
- Jams Length
- Jams Count
- Travel Time
- Minutes Delay

### OECD Cities

Base de indicadores económicos y urbanos.

Variables utilizadas:

- PIB per cápita
- Desempleo
- PM2.5
- Población

## Metodología
**1. Exploración Inicial**

Se realizó una revisión de la estructura de ambos datasets mediante:

- Identificación de columnas.
- Revisión de tipos de datos.
- Validación de valores nulos.
- Comprensión de la granularidad de cada fuente.

Hallazgos iniciales:

- Las fechas del dataset de tráfico se encontraban almacenadas como texto.
- Diversas variables económicas estaban almacenadas como cadenas de caracteres debido al uso de formatos regionales (comas y puntos).

**2. Limpieza y Transformación**
Dataset de Tráfico

Se realizaron las siguientes acciones:

- Conversión de fechas a formato datetime.
- Estandarización de nombres de columnas utilizando snake_case.
- Extracción del año de cada observación.
- Dataset Económico

Se efectuaron las siguientes transformaciones:

- Eliminación de separadores de miles.
- Conversión de variables numéricas a formato float.
- Eliminación de símbolos porcentuales.
- Conversión de población de millones a habitantes absolutos.

**3. Filtrado Temporal**

Para mantener consistencia entre ambas fuentes se seleccionaron exclusivamente registros correspondientes al año 2024.

Datasets generados:

- traffic_2024
- eco_2024

**4. Agregación de Datos de Movilidad**

Debido a que TomTom registra múltiples observaciones por ciudad, se calcularon promedios anuales para cada indicador.

Variables agregadas:

- jams_delay
- traffic_index_live
- jams_length_kms
- jams_count
- mins_delay
- travel_time_live_per_10kms_mins
- travel_time_hist_per_10kms_mins

Resultado:

- 387 ciudades resumidas a nivel ciudad-año.

5. Integración de Datos

Los datasets fueron combinados mediante una unión tipo INNER utilizando:

- city
- year

Resultado:

- Dataset final compuesto por 15 ciudades latinoamericanas para 2024.

## Análisis Exploratorio

Se desarrollaron visualizaciones para identificar patrones y posibles relaciones entre movilidad y economía.

**Distribución de Congestión**

Se utilizó un boxplot de jams_delay para:

- Identificar valores atípicos.
- Comparar media y mediana.
- Evaluar dispersión de la congestión urbana.
- Distribución del PIB per Cápita

**Se construyó un histograma de city_gdp_capita para:**

- Analizar la distribución económica de las ciudades.
- Detectar concentraciones o sesgos.
- Comparación por Ciudad

**Se elaboró un gráfico de barras comparando:**

- Retrasos promedio por congestión.
- PIB per cápita.

## Principales Hallazgos
**Ciudad de México**

Presentó el mayor nivel promedio de congestión:
- Jams Delay promedio: 2,833 minutos.

Esto la convierte en un caso atípico dentro del conjunto analizado.

**Bogotá**

Mostró niveles elevados de congestión acompañados de un PIB per cápita relativamente moderado.

**Buenos Aires**

Presentó una combinación de congestión significativa y productividad económica intermedia.

**Santiago**

Mostró niveles relevantes de congestión en comparación con otras ciudades con niveles similares de ingreso.

## Dataset Final

Archivo generado:

- ladb_mobility_economy_2024_clean.csv

Contenido:

- Indicadores de movilidad urbana.
- Indicadores económicos.
- Información demográfica.

Una fila por ciudad para el año 2024.

## Tecnologías Utilizadas
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## Conclusiones

Los resultados sugieren que la movilidad urbana puede representar un factor relevante para la competitividad económica de las ciudades. Aunque no se observa una relación lineal directa entre congestión y productividad, los hallazgos muestran que varias ciudades con altos niveles de congestión enfrentan retos que podrían mitigarse mediante inversiones estratégicas en infraestructura de transporte.

El proyecto permitió aplicar técnicas fundamentales de limpieza, transformación, integración y análisis exploratorio de datos, generando un dataset consolidado que puede servir como base para modelos predictivos o estudios más avanzados sobre desarrollo urbano.

## Aprendizajes y Retos del Proyecto
Este proyecto permitió aplicar de manera práctica el proceso completo de preparación y análisis de datos, desde la exploración inicial hasta la generación de un dataset consolidado para la toma de decisiones.

**Principales retos enfrentados**

**1. Estandarización de formatos heterogéneos**

Uno de los principales desafíos fue trabajar con fuentes de datos que utilizaban formatos distintos para representar valores numéricos y fechas.

En el dataset económico se encontraron variables almacenadas como texto debido al uso de formatos regionales, incluyendo:

- Separadores de miles mediante puntos (.).
- Separadores decimales mediante comas (,).
- Porcentajes representados con símbolos (%).

Fue necesario desarrollar procesos de limpieza y transformación para convertir correctamente estas variables a formatos numéricos utilizables.

**2. Conversión y validación de fechas**

El dataset de tráfico almacenaba las fechas como cadenas de texto. Para poder realizar análisis temporales fue necesario convertir las columnas a formato datetime y validar que no existieran errores de conversión o registros inválidos.

**3. Integración de fuentes con diferente granularidad**

Los datos de movilidad y los datos económicos tenían niveles de detalle distintos.

Mientras que la información económica se encontraba consolidada a nivel ciudad-año, la información de tráfico contenía múltiples observaciones diarias para cada ciudad.

Para resolver esta diferencia se calcularon métricas promedio anuales por ciudad antes de realizar la integración de ambas fuentes.

**4. Manejo de grandes volúmenes de información**

El dataset de tráfico contenía más de un millón de registros, lo que requirió aplicar procesos eficientes de agrupación y agregación para resumir la información sin perder representatividad.

**5. Homologación de claves de unión**

La integración de las bases dependía de que las ciudades estuvieran representadas de manera consistente entre ambas fuentes.

Fue necesario verificar que los nombres de ciudades y años coincidieran correctamente para evitar pérdidas de información durante el proceso de unión.

**Aprendizajes obtenidos**

Durante el desarrollo de este proyecto se fortalecieron competencias en:

- Limpieza y transformación de datos con Pandas.
- Conversión y validación de tipos de datos.
- Manipulación de fechas y variables temporales.
- Agregación de grandes volúmenes de información.
- Integración de múltiples fuentes de datos.
- Análisis exploratorio de datos (EDA).
- Visualización de información mediante Matplotlib y Seaborn.
- Documentación de procesos analíticos reproducibles en Jupyter Notebook.

**Próximos pasos**

Como extensión futura de este análisis, podrían desarrollarse modelos estadísticos y predictivos para cuantificar el impacto de la congestión urbana sobre variables económicas como el PIB per cápita o el desempleo.

Asimismo, podrían incorporarse nuevas variables relacionadas con infraestructura de transporte, inversión pública, transporte masivo o indicadores ambientales para construir una visión más integral del desarrollo urbano.

## Autor

Irving Alejandro Canseco Gómez

Analista de datos en formación con experiencia en planeación estratégica, indicadores de desempeño, análisis de información y evaluación de políticas públicas.

Habilidades aplicadas en este proyecto
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Limpieza de datos
- Análisis exploratorio de datos (EDA)
- Integración de bases de datos
- Visualización de información
- Documentación técnica

Contacto

LinkedIn: [https://www.linkedin.com/in/iralgom/]

GitHub: [https://github.com/iralgom/]
