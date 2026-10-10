# 🌐 Proyecto: Primeros Pasos del Dato a la Decisión
## Análisis de la Brecha Digital y Cobertura Wi-Fi en Barcelona

¡Bienvenido/a a este proyecto guiado! Este repositorio está diseñado como una actividad práctica e introductoria para estudiantes de Data Analytics. A través de este caso real, aprenderás a cargar, limpiar, consultar con SQL, visualizar y reflexionar sobre datos de acceso público.

---

## 🛠️ Estructura del Proyecto y Ejecución Paso a Paso

### 1. Requisitos Previos
* Cuenta en [Google Colab](https://colab.research.google.com/) o un cuaderno local de **Jupyter Notebook** (Python 3.8+).
* Librerías necesarias: `pandas`, `numpy`, `matplotlib`, `seaborn`, `sqlite3`.


### 2. Instrucciones para la Reproducción
1. **Clonar el repositorio:**
   git clone [https://github.com/tu-usuario/brecha-digital-barcelona.git](https://github.com/tu-usuario/brecha_digital_wifi_barcelona.git)
2. **Cargar el entorno:** Abre el archivo `notebook.ipynb` en Google Colab o Jupyter Notebook.
3. **Subir el Dataset:** Asegúrate de colocar el archivo `opendatabcn_wifi.csv`(le cambié el nombre para que sea más corto) en la raíz del entorno de ejecución o utiliza la ruta directa desde el portal *Open Data BCN*.
4. **Ejecución del Cuaderno:** Corre las celdas de forma secuencial de arriba a abajo (`Shift + Enter`).

---

## 📄 Descripción del Dataset

* **Origen de los datos:** Portal oficial *Open Data BCN* (Ayuntamiento de Barcelona).
* **Temática:** Infraestructura de red Wi-Fi pública municipal.
* **Unidad de análisis (Fila):** Cada fila representa un punto de acceso Wi-Fi individual e independiente ubicado en un equipamiento o vía pública.
* **Variables Clave Utilizadas:**
  * `register_id`: Identificador único de cada punto de acceso.
  * `nombre_equipamiento` (`name`): Nombre del espacio público donde se ubica la red.
  * `distrito` (`addresses_district_name`): Distrito municipal al que pertenece el punto.
  * `barrio` (`addresses_neighborhood_name`): Barrio específico donde está ubicado (clave utilizada para vincular los datos socioeconómicos).

---

## 💡 Explicación Didáctica 

### ¿Qué es un DataFrame en Pandas?

> **La analogía de la hoja de cálculo de Excel:**
> Imagina que estás trabajando con un libro de contabilidad o una hoja de cálculo en Excel que contiene filas y columnas. 
> En Python, un **DataFrame** es exactamente esa misma estructura de tabla bidimensional, pero optimizada para interactuar con ella a través de código.
> 
> * **Las Filas (Registros):** Representan cada elemento individual del análisis (en nuestro proyecto, cada punto Wi-Fi registrado).
> * **Las Columnas (Variables):** Representan las características o atributos de esos elementos (ejemplo: el nombre del edificio, el barrio o el distrito).
> 
> Trabajar con un DataFrame nos permite filtrar miles de filas, calcular promedios o corregir errores en cuestión de milisegundos sin modificar el archivo original de forma permanente.

---

## ⚠️ Anticipación de Errores Comunes del Alumnado

Al iniciarse en el análisis de datos con Python, es habitual cometer ciertos errores de sintaxis o de ruta. A continuación, analizamos 2 errores muy frecuentes y cómo solucionarlos en el aula:

### 🔴 Error 1: `FileNotFoundError: [Errno 2] No such file or directory`
* **¿Por qué ocurre?:** Python intenta buscar el archivo `.csv` en el directorio de trabajo actual, pero no lo encuentra porque el usuario olvidó subirlo a la sesión de Colab o escribió mal la ruta o el nombre del archivo.
* **💡 Guía de solución pedagógica:** 
  1. Muestra al alumnado la barra lateral izquierda en Google Colab y haz clic en el icono de la carpeta (📁).
  2. Verifica que el archivo `opendatabcn_wifi_bcn.csv` figure en ese listado.
  3. Asegúrate de que las mayúsculas, minúsculas y extensiones coincidan exactamente entre el código y el archivo real.

### 🔴 Error 2: `KeyError: 'Barrio'`
* **¿Por qué ocurre?:** Ocurre cuando intentamos acceder a una columna que no existe en el DataFrame con esa grafía exacta (por ejemplo, escribir `'Barrio'` con mayúscula cuando la columna se llama `'barrio'` en minúsculas).
* **💡 Guía de solución pedagógica:**
  1. Enseña al estudiante a ejecutar siempre el comando `print(df.columns)` antes de filtrar.
  2. Acostumbra al alumnado a copiar y pegar directamente el nombre de la variable desde la lista resultante para evitar errores tipográficos o espacios invisibles.

---

## 📊 Resumen de Consultas SQL de Negocio

Para resolver las preguntas de negocio sobre la infraestructura digital, trasladamos los datos limpios a un motor en memoria (`SQLite`) y ejecutamos las siguientes consultas:

1. **Consulta 1 (Agregación Macro):** Cuenta la cantidad total de puntos Wi-Fi registrados en cada distrito (`GROUP BY`).
2. **Consulta 2 (Detección de Brecha Digital):** Filtra e identifica los barrios con un nivel de vulnerabilidad social `'Alta'` que poseen menos de 3 puntos de conexión (`INNER JOIN` + `WHERE` + `GROUP BY` + `HAVING`).
3. **Consulta 3 (Comparativa Socioeconómica):** Calcula la cobertura de puntos y la renta media estimada en distritos clasificados con vulnerabilidad `'Media'` y `'Alta'` (`INNER JOIN` + `WHERE` + `GROUP BY`).

---

## 📈 Justificación Pedagógica de los Gráficos

1. **Gráfico de Barras Horizontales:** Se eligió para mostrar los distritos en el eje vertical ($Y$) porque sus nombres son largos; esto evita la rotación de etiquetas y facilita una lectura clara ordenada por volumen de cobertura.
2. **Gráfico de Dispersión con Línea de Tendencia (`sns.regplot`):** Se utilizó para evaluar visualmente si existe una relación entre la renta media del hogar ($X$) y la cantidad de puntos Wi-Fi ($Y$) en cada barrio, permitiendo identificar patrones de desigualdad.
3. **Gráfico de Barras por Categoría Socioeconómica:** Permite resumir la disponibilidad media de red pública según el grado de vulnerabilidad del barrio, mostrando de forma directa la brecha entre zonas favorecidas y vulnerables.

---

## 📢 Storytelling con Datos: Del Análisis a la Decisión

### 1. Conclusiones Clave 
* **Distribución Territorial Desigual:** La presencia de redes Wi-Fi públicas en Barcelona está fuertemente concentrada en distritos con alta presencia de equipamientos municipales (como bibliotecas o centros cívicos), dejando ciertas áreas con menor densidad de puntos.
* **Brecha en Zonas Vulnerables:** Existen barrios clasificados con una vulnerabilidad socioeconómica 'Alta' que cuentan con una oferta muy reducida de infraestructura Wi-Fi gratuita (menos de 3 puntos de acceso), lo que limita las oportunidades de inclusión digital para hogares con menos ingresos.

### 2. ¿A quién le sirve esta información?
* **Administración Pública y Concejales de Barrio:** Para priorizar la inversión en telecomunicaciones e instalar nuevos puntos de conexión en equipamientos de barrios vulnerables.
* **Entidades Sociales y ONGs:** Para focalizar sus proyectos de entrega de dispositivos móviles o aulas de alfabetización digital en las zonas con menor cobertura pública.

### 3. Reflexión sobre las Limitaciones del Dato
* **Falta de Métricas de Calidad:** El dataset solo contabiliza el número de puntos registrados, pero no ofrece datos sobre el estado operativo, el ancho de banda disponible ni la velocidad de conexión.
* **Aislamiento de la Densidad Poblacional:** No se pondera la cantidad de puntos Wi-Fi en relación con el número total de habitantes por barrio, lo que podría ocultar saturaciones de la red en zonas muy pobladas.
