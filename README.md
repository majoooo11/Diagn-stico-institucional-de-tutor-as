# Diagnóstico multicampus del modelo institucional de tutorías como garantía del derecho humano a la educación superior
## Base de Datos y Procesamiento de Estadística de Tutorías Universitarias (2015–2024)

Este repositorio documenta el proceso de construcción, depuración, extrapolación y proyección de datos de tutorías universitarias a partir de una base de datos estructurada en MySQL y trabajada posteriormente en Python (Google Colab).

El objetivo principal es contar con un conjunto de datos consistente y completo para el análisis longitudinal de las tutorías a nivel facultad, cubriendo el periodo 2015–2024.

## Estructura general del proyecto

El trabajo se desarrolló en dos grandes etapas:

1. Estructuración y consolidación de datos en MySQL

2. Procesamiento, extrapolación y proyección en Python

## 1) Contexto del proyecto

Se construyó una **base de datos relacional en MySQL** con información histórica de tutorías, integrando registros desde **2015 hasta 2024**.  
Posteriormente, se exportaron datos a un archivo `.csv` para trabajar en **Python (pandas)** dentro de Google Colab, con el objetivo de:

- Completar valores faltantes (especialmente **2015**) de forma reproducible.
- Generar y/o estimar datos para **2024** usando tendencias históricas y tasas observadas.
- Verificar consistencia interna (reglas lógicas entre matrículas/egresos/titulación).
- Dejar un dataset final limpio y listo para **análisis econométrico longitudinal**, particularmente modelos de datos de panel orientados al estudio de trayectorias académicas.

---

---

## 2. Construcción y procesamiento de la base de datos

### 2.1 Estructuración en MySQL

- Se diseñó una base de datos relacional en **MySQL**, estructurada por:
  - Facultad
  - Año (2015–2024)
- Se integraron variables institucionales relacionadas con:
  - Matrícula (primer semestre, tercer semestre y total)
  - Tutorías e intervenciones
  - Personal académico
  - Egreso y titulación

La base consolidada permitió asegurar consistencia temporal y comparabilidad entre unidades académicas.

### 2.2 Procesamiento y extrapolación en Python

El procesamiento se realizó en un **cuaderno de Google Colab**, utilizando principalmente `pandas`, `numpy` y herramientas de visualización.

Las principales tareas realizadas fueron:

- **Carga y preparación inicial de datos**
  - Importación del archivo `tutorias_facultad_2015_2024.csv`.
  - Configuración de tipos de datos y ordenamiento temporal.

- **Extrapolación de datos faltantes para 2015**
  - Relleno de valores ausentes mediante extrapolación lineal basada en la tendencia histórica 2016–2023, aplicada por facultad.
  - Variables extrapoladas: intervenciones tutoriales, número de tutores y personal académico.

- **Generación de datos proyectados para 2024**
  - Estimación de matrícula de nuevo ingreso mediante extrapolación de tendencias.
  - Cálculo de matrícula de tercer semestre usando tasas históricas de retención.
  - Proyección de matrícula total asegurando consistencia interna.
  - Estimación de egresados y titulados a partir de tasas históricas.
  - Extrapolación de otras variables numéricas mediante métodos lineales.

- **Ajustes y verificaciones de consistencia**
  - Validación de que la matrícula total fuera mayor o igual a la suma de los estudiantes de primer y tercer semestre.
  - Corrección de casos atípicos, incluyendo una facultad donde la matrícula de tercer semestre superaba incorrectamente a la de primer semestre.
  - Revisión gráfica de tendencias para detectar valores atípicos en las proyecciones de 2024.

### 2.3 Resultado final

El resultado es un **DataFrame consolidado (`df_extrap`)** que contiene:

- Datos observados (2015–2023).
- Valores extrapolados para 2015.
- Datos proyectados y ajustados para 2024.

Este conjunto de datos está listo para su uso en **análisis estadístico descriptivo y modelos econométricos de datos de panel**.

---

## 3. Reproducibilidad

El repositorio está diseñado para asegurar:

- Transparencia en el tratamiento de datos.
- Reproducibilidad de los resultados.
- Trazabilidad entre la base administrativa original y los datos analíticos finales.

---

## Licencia

Este repositorio se comparte con fines académicos y de investigación.  
El uso de la información está sujeto a las políticas institucionales de la Universidad de Colima.
