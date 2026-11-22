# Análisis de uso de clientes de ConnectaTel

Proyecto de análisis de datos sobre una empresa de telecomunicaciones
con operaciones en México y Colombia. Se exploran, limpian y analizan
tres fuentes de datos para entender cómo usan los clientes las llamadas
y los mensajes, detectar valores atípicos y crear segmentos útiles para
el negocio.

## Objetivo

Responder preguntas de negocio como:

-   ¿Qué segmentos de clientes muestran mayor o menor uso de llamadas y
    mensajes?
-   ¿Qué usuarios presentan valores atípicos que podrían indicar
    comportamientos inusuales o errores de registro?
-   ¿Cómo varía el uso según la edad y el plan contratado?
-   ¿Qué patrones ayudan a mejorar la oferta de planes?

## Datasets

  -----------------------------------------------------------------------
  Archivo                             Contenido
  ----------------------------------- -----------------------------------
  `plans.csv`                         Catálogo de planes: precio mensual,
                                      mensajes, GB y minutos incluidos, y
                                      costo por extra.

  `users_latam.csv`                   Clientes: edad, ciudad, fecha de
                                      registro, plan y fecha de baja
                                      (churn).

  `usage.csv`                         Registros de uso: tipo (llamada o
                                      mensaje), fecha, duración y
                                      longitud.
  -----------------------------------------------------------------------

Los datos cubren hasta el año 2024.

## Etapas del análisis

1.  **Carga y exploración:** estructura, tipos de datos y vista rápida
    de los tres datasets.
2.  **Calidad de datos:** conteo de nulos, detección de sentinels
    (`-999` en `age`, `"?"` en `city`) y revisión de fechas imposibles
    (registros con año 2026).
3.  **Limpieza:** reemplazo de sentinels, marcado de fechas fuera de
    rango como nulas y verificación de que los nulos de `duration` y
    `length` dependen del tipo de registro (MAR).
4.  **Resumen estadístico por usuario:** agregación del uso (mensajes,
    llamadas y minutos) y combinación con la tabla de usuarios.
5.  **Visualización y outliers:** histogramas por plan, boxplots y
    límites IQR.
6.  **Segmentación:** grupos de uso (Bajo, Medio y Alto) y grupos de
    edad (Joven, Adulto y Adulto Mayor).
7.  **Conclusiones ejecutivas:** hallazgos y recomendaciones para el
    negocio.

## Hallazgos principales

-   **Datos:** 55 edades con `-999` (1.4%), 565 ciudades nulas o con
    `"?"` (14.1%) y 40 fechas de registro del año 2026 (1.0%).
-   **Uso:** la mayoría de los usuarios envía entre 4 y 7 mensajes y
    hace entre 3 y 6 llamadas, con una cola de usuarios muy activos
    (outliers solo por arriba).
-   **Planes:** Básico (64.9%) y Premium (35.1%) muestran el mismo
    patrón de uso, y la edad tampoco los distingue.
-   **Recomendación:** revisar la propuesta de valor de Premium y crear
    ofertas diferenciadas por nivel de uso.

## Cómo ejecutar el notebook

### Opción A: Google Colab

1.  Abre el notebook desde GitHub con **Open in Colab** (o sube el
    `.ipynb` a Colab).
2.  Sube `plans.csv`, `users_latam.csv` y `usage.csv` al entorno de
    Colab.
3.  Ajusta las rutas de lectura (ver abajo) y ejecuta **Runtime \> Run
    all**.

### Opción B: local

``` bash
git clone <URL-del-repositorio>
cd <nombre-del-repositorio>
pip install pandas numpy seaborn matplotlib jupyter
jupyter notebook
```

### Ajuste de rutas

El notebook original lee los archivos desde `/datasets/`, que solo
existe en el entorno del curso. Para ejecutarlo en otro lugar, cambia
las rutas, por ejemplo:

``` python
plans = pd.read_csv("data/plans.csv")
users = pd.read_csv("data/users_latam.csv")
usage = pd.read_csv("data/usage.csv")
```

## Guía de reproducción

1.  Coloca los tres CSV en la ruta que uses y ajusta las rutas del paso
    1.
2.  Ejecuta las celdas **en orden**, de arriba abajo. Cada paso depende
    de las variables creadas en los anteriores (`plans`, `users`,
    `usage` y `user_profile`).
3.  Si reinicias el kernel, vuelve a ejecutar desde la primera celda.

## Estructura del repositorio

``` text
├── README.md
├── notebooks/
│   └── S7_Proyecto_ConnectaTel.ipynb
└── data/            # los CSV (si se pueden compartir)
```

## Tecnologías

Python, pandas, numpy, seaborn, matplotlib y Jupyter Notebook.

## Autor

**Andres Alberto Uribe Ochoa**
