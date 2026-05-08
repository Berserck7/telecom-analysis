# ConnectaTel — Análisis de Comportamiento de Clientes
Este repositorio contiene el análisis realizado durante el Sprint 7 del caso ConnectTel

## 🎯Objetivo
Evaluar el comportamiento de los clientes de ConnectaTel, una empresa de telecomunicaciones en Latinoamérica, a partir de datos registrados hasta el año 2024. El análisis busca identificar patrones de consumo, detectar comportamientos atípicos y construir segmentos de clientes para apoyar decisiones comerciales orientadas a la retención y optimización de la oferta de planes.

## 📋 Datasets utilizados
Archivo
Descripción
plans.csv
Información de los planes disponibles: precio mensual, minutos, GB y mensajes incluidos, costos por exceso
users_latam.csv
Datos de clientes: edad, ciudad, fecha de registro, plan contratado y fecha de cancelación
usage.csv
Registro de uso por cliente: llamadas y mensajes con fecha, duración y longitud

## Etapas del análisis

### 1. Exploración inicial
Carga de los tres datasets y revisión de estructura, tipos de datos, dimensiones y primeras filas con .head(), .info() y .describe().
### 2. Diagnóstico de calidad de datos
Identificación de valores nulos, sentinels y fechas imposibles:
age: sentinel -999 detectado y cuantificado
city: 469 nulos reales + 96 registros con "?" (14.1% del total)
reg_date: 40 fechas en 2026 fuera del rango válido
usage.date: 50 nulos (0.125% de 40,000 filas)
duration / length: nulos confirmados como MAR según columna type
### 3. Limpieza de datos
Sentinel -999 en age reemplazado por la mediana (calculada sin el sentinel)
Sentinel "?" en city y nulos unificados como "Unknown"
Fechas fuera de rango marcadas como NaT
Conversión de reg_date, churn_date y date a datetime
Drop de 50 filas sin fecha en usage
### 4. Agregación de uso por usuario
Construcción de tabla de métricas por user_id: total de mensajes, llamadas y minutos de llamada. Unión con users mediante merge left por user_id.
### 5. Estadísticas descriptivas
Resumen estadístico de variables numéricas clave y distribución porcentual del tipo de plan (Básico / Premium).
### 6. Visualización de distribuciones
Histogramas con hue='plan' para age, cant_mensajes, cant_llamadas y cant_minutos_llamada. Análisis de forma de distribución y diferencias entre planes.
### 7. Detección de outliers
Boxplots por variable y cálculo de límites superiores con método IQR (×1.5). Outliers identificados como comportamiento real de uso intensivo. Decisión: conservar.
### 8. Segmentación de clientes
grupo_uso: Bajo uso / Uso medio / Alto uso según llamadas y mensajes
grupo_edad: Joven / Adulto / Adulto Mayor según edad
Cruce de segmentos con tipo de plan mediante tabla de contingencia
### 9. Insight ejecutivo
Traducción de hallazgos en recomendaciones accionables para el negocio.

## 🧠 Principales hallazgos

⚠️ Problemas detectados en los datos

🔍 Segmentos por Edad 50.45% Adultos (30-60 años) y corresponde al grupo dominante 30.55% Adultos Mayores (+60 años) correspondiente al segundo grupo relevante 19% Jóvenes (-30 años) grupo minoritario
➡️ Los Adultos Mayores superan a los Jóvenes y sugiere que la oferta debería considerar las necesidades de usuarios maduros, no solo enfocarse en el segmento joven.

📊 Segmentos por Nivel de Uso 73.6% Uso medio son gran mayoría 19.5% Bajo uso y son clientes con poca actividad 7% Alto uso. Son la minoría pero potencialmente los más valiosos ya que son los que más consumen los servicios de ConnectaTel.
➡️ Esto sugiere que los usuarios de Alto uso están en el plan Básico. Eso significa que ConnectaTel tiene clientes que consumen mucho pero pagan poco encontrando una oportunidad clara de migrarlos a Premium.

💡 Recomendaciones

Diseñar una campaña dirigida específicamente al segmento Alto uso + Básico. Son clientes ya comprometidos con el servicio.
El 30.5% de la base son mayores de 60 años. Este segmento probablemente prioriza llamadas sobre datos, por ende, la creación de un plan con más minutos incluidos y precio accesible orientado a este perfil sería una gran oportunidad de negocio.
El 14% de registros sin ciudad válida. Validar la ciudad en el proceso de registro para habilitar segmentación regional en futuros análisis.
Evaluar un plan "Exclusivo" con límites más altos o sin límite. Dicha recomendación se hace a partir de los resultados analizados por los outliers.

Cómo ejecutar el notebook
Opción 1 — Google Colab (recomendado)

Abre Google Colab

## ▶ Cómo abrir el notebook en Google Colab

Haz clic en el siguiente botón:
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Berserck7/telecom-analysis/blob/main/S7-Version-Estudiante-Project-ConnectaTel.ipynb)

## ▶ Cómo abrir el notebook en GitHub
Haz clic en el siguiente botón:
[![GitHub](https://img.shields.io/badge/GitHub-Repositorio-black?logo=github)](https://github.com/berserck7/telecom-analysis)


# Instalar dependencias
pip install pandas matplotlib seaborn

# Abrir el notebook
jupyter notebook S7-Version-Estudiante-Project-ConnectaTel.ipynb

Dependencias
Librería   Versión mínima
Python         3.9+
pandas         1.3+ 
matplotlib     3.4+
seaborn        0.11+

Estructura del repositorio
connectatel-analysis/
├── datasets/
│   ├── plans.csv
│   ├── users_latam.csv
│   └── usage.csv
├── S7-Version-Estudiante-Project-ConnectaTel.ipynb
└── README.md

Autor
# Jose Luis Pinto Camargo
Analista de Datos Jr. | TripleTen Data Analytics Bootcamp
[GitHub](https://github.com/Berserck7) · LinkedIn: https://www.linkedin.com/in/joseluispintocamargo/
