# Diagnóstico multicampus del modelo institucional de tutorías como garantía del derecho humano a la educación superior
## Base de Datos y Procesamiento de Tutorías Universitarias (2015–2024)

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
- Dejar un dataset final limpio y listo para análisis estadístico/econométrico.

---

## 2) Dataset de trabajo en Python (Colab)

En el cuaderno se trabajó con:

- `tutorias_facultad_2015_2024.csv`

Cargado en un `DataFrame` de pandas para transformar, completar y validar.

---

## 3) ¿Qué se hizo en el cuaderno? (Resumen reproducible)

### A) Carga y preparación inicial
- Se cargó el `.csv` a un DataFrame (`df`) y se aplicaron configuraciones básicas de limpieza/formatos.

### B) Completar valores faltantes para 2015 (extrapolación)
- Se completaron valores faltantes del año **2015** en columnas clave (p. ej., relacionadas con **intervenciones** y **tutores**) mediante **extrapolación lineal** usando la trayectoria histórica **2016–2023**, aplicada **por facultad**.

### C) Generación/estimación de datos para 2024
Se implementó una función para estimar variables de 2024 con base en tendencias y tasas históricas:

- **Matrícula de nuevo ingreso (primer semestre):** extrapolación de tendencia histórica.
- **Matrícula de tercer semestre:** estimada a partir de **tasas históricas de retención**, garantizando que no excediera el primer ingreso.
- **Matrícula total:** extrapolación y ajuste para consistencia con semestres (primer/tercer).
- **Egresados y titulados:** estimados usando **tasas históricas** de egreso y titulación.
- **Otras variables numéricas** (personal, intervenciones, etc.): extrapolación lineal.

### D) Reglas de consistencia y correcciones
Tras generar 2024 se aplicaron verificaciones:

- Se validó que la **matrícula total** fuera **≥** a la suma de estudiantes de **primer** y **tercer semestre**.
- Se detectó y corrigió un caso específico (Facultad 30) donde la matrícula de **tercer semestre** resultaba mayor que la de **primer ingreso**, ajustándolo con una tasa de deserción/retención más robusta.
- Se revisaron posibles **valores atípicos** en la proyección de primer ingreso 2024 y se visualizó la tendencia para una facultad como ejemplo.

### E) Resultado final
El DataFrame final (`df_extrap`) contiene:

- Datos originales,
- Valores completados para 2015,
- Datos estimados para 2024,
- Con consistencia interna verificada,

listo para análisis posterior o exportación.
