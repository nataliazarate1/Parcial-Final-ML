# Proyecto final - Machine Learning con PySpark y Docker

## Estudiante: Natalia Zárate Yara

## Problema escogido

Este proyecto analiza manifestaciones de violencia y agresión registradas en datos colombianos desde dos perspectivas complementarias. En los Bloques 1 y 2 se estudian los reportes oficiales de delitos sexuales de la Policía Nacional, con énfasis en patrones territoriales, temporales y demográficos entre 2010 y 2025. En el Bloque 3 se analiza un corpus colombiano de tweets etiquetados como ciberacoso o no ciberacoso, con el fin de estudiar como aparece la agresión en lenguaje digital.

El propósito general no es establecer causalidad ni medir la ocurrencia real total de estos fenómenos, sino caracterizar patrones observables en fuentes disponibles y aplicar técnicas de analisis exploratorio, Machine Learning y NLP. En todos los casos, los resultados deben interpretarse como aproximaciones basadas en registros o corpus etiquetados, reconociendo limitaciones como subregistro, sesgos de denuncia, cobertura de la fuente y diferencias entre violencia registrada y violencia realmente ocurrida.

## Datasets utilizados

### Bloque 1 y Bloque 2

- Nombre: Reporte Delitos sexuales Policia Nacional
- Fuente: datos.gov.co / DIJIN - Policia Nacional
- ID Socrata: `fpe5-yrmw`
- URL: https://www.datos.gov.co/Seguridad-y-Defensa/Reporte-Delitos-sexuales-Polic-a-Nacional/fpe5-yrmw/about_data
- Archivo local de trabajo: `data/raw/reporte_delitos_sexuales_policia_20260527.csv`
- Fecha de descarga local: 2026-05-27
- Registros originales cargados: 392.576
- Registros usados para analisis 2010-2025: 386.224
- Columnas principales: `DEPARTAMENTO`, `MUNICIPIO`, `CODIGO DANE`, `ARMAS MEDIOS`, `FECHA HECHO`, `GENERO`, `GRUPO ETARIO`, `CANTIDAD`, `delito`

### Bloque 3

- Nombre: Colombian Spanish Cyberbullying Dataset
- Fuente: Hugging Face, dataset `FelipeGuerra/Colombian_Spanish_Cyberbullying_Dataset_2`
- URL: https://huggingface.co/datasets/FelipeGuerra/Colombian_Spanish_Cyberbullying_Dataset_2
- Archivo local de trabajo: `bloque3_nlp/corpus.csv`
- Archivo auxiliar con nombre descriptivo: `bloque3_nlp/corpus_ciberacoso_colombiano.csv`
- Registros válidos usados en el notebook: 2.565 tweets
- Variable textual: `texto`
- Variable objetivo: `ciberacoso`
- Uso en el proyecto: clasificación de ciberacoso en tweets colombianos mediante TF-IDF, Regresión Logística y comparación con modelo pre-entrenado de Hugging Face.

## Estructura del repositorio

```text
proyecto_final_zarate/
|-- README.md
|-- bloque1_eda/
|   `-- bloque1_eda_zarate.ipynb
|-- bloque2_ml/
|   `-- bloque2_ml_zarate.ipynb
|-- bloque3_nlp/
|   |-- bloque3_nlp_zarate.ipynb
|   `-- corpus.csv
|-- data/
|   |-- raw/
|   |   `-- reporte_delitos_sexuales_policia_20260527.csv
|   `-- processed/
|-- models/
|-- reporte/
|   `-- reporte_ejecutivo_borrador.md
|-- docker-compose.yml
`-- requirements.txt
```

## Cómo ejecutar

### Opción con Docker

1. Abrir una terminal en la raíz del proyecto.
2. Ejecutar:

```bash
docker compose up
```

3. Abrir JupyterLab en:

```text
http://localhost:8889/lab
```

Si Docker muestra otro puerto en la terminal, usar la URL indicada por Docker.

4. Ejecutar los notebooks en este orden:

```text
1. bloque1_eda/bloque1_eda_zarate.ipynb
2. bloque2_ml/bloque2_ml_zarate.ipynb
3. bloque3_nlp/bloque3_nlp_zarate.ipynb
```

## Resultados principales

- Bloque 1: entre 2010 y 2025 se analizaron 386.224 reportes. Bogotá concentró 70.515 reportes, Antioquia 47.705 y Valle 36.566.
- Bloque 2: se construyeron 8.813 perfiles municipio-anio. Random Forest con entrenamiento balanceado obtuvo accuracy de 0,6769, recall de 0,6821, F1 de 0,5176 y AUC de 0,7511.
- Bloque 3: el modelo TF-IDF con Regresión Logística obtuvo accuracy de 0,9046, F1 de 0,9044 y AUC de 0,9510 para clasificar ciberacoso.

## Conclusión integrada

El análisis muestra que los reportes de delitos sexuales en Colombia presentan concentración territorial y variación temporal importante, con Bogotá, Antioquia y Valle como los departamentos con mayor numero de registros entre 2010 y 2025. Al transformar la base a perfiles municipio-año, fue posible aplicar modelos de Machine Learning para identificar municipios-año con alta proporción de reportes relacionados con menores de 14 años. Finalmente, el analisis NLP permitió estudiar otra forma de agresión, el ciberacoso, desde el lenguaje digital colombiano. En conjunto, los tres bloques conectan datos oficiales, modelos predictivos y análisis textual para estudiar distintas manifestaciones de violencia registrada, manteniendo una lectura cuidadosa sobre las limitaciones de cada fuente.
