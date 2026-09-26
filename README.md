# Taller 1 – Supervisión de contratación pública de bienes (SECOP II)

EDA para apoyar a la oficina de control interno de una entidad estatal a focalizar la supervisión de los contratos de compra de bienes, específicamente compraventa y suministros, analizando qué características de un contrato se asocian con desviaciones en su ejecución.

Curso: Ciencia de Datos – Maestría en Ingeniería de Información (MINE), Universidad de los Andes.

## Integrantes

| Nombre | Usuario GitHub | Correo |
|---|---|---|
| Rafael Porras | [@rporras10](https://github.com/rporras10) | r.porrasm@uniandes.edu.co |
| Sebastián Rodríguez | _completar_ | _completar_ |

## Objetivo

Identificar qué atributos de un contrato (valor, modalidad de contratación, sector, tipo de entidad, destino del gasto, entre otros) se relacionan con desviaciones en su ejecución como puede ser adición de plazo, presupuesto no ejecutado y cierre sin liquidar y, a partir de estos hallazgos, proponer criterios de prioridad  para la supervisión a partir  del momento de la firma.

## Alcance

- **Datos:** contratos de bienes firmados por entidades públicas colombianas entre 2019 y 2025, extraídos de SECOP II.
- **Incluye:** entendimiento inicial y calidad de los datos, análisis univariado y multivariado, pruebas de hipótesis y recomendaciones basadas en datos.
- **No incluye:** modelos predictivos. Las hallazgos encontrados son puramente observacionales.

## Datos

| | |
|---|---|
| Archivo | `secop_bienes.parquet` (incluido en este repositorio) |
| Fuente original | [Enlace provisto en el enunciado del taller](https://drive.google.com/file/d/1R0pSXh2bgCoPKcXlAlafdavVwvzZX6AQ/view?usp=sharing) |
| Dimensiones | 196.391 contratos × 36 columnas |
| Periodo | Contratos firmados entre 2019 y 2025 |

Los notebooks **no modifican** el archivo de datos ya que toda la limpieza se hace en memoria.

## Organización del repositorio

```
secop-eda/
├── README.md               <- este archivo
├── environment.yml         <- ambiente conda para reproducir el análisis
├── secop_bienes.parquet    <- datos
├── Calidad_Datos.ipynb     <- 1. Diagnóstico de calidad de datos
├── eda_secop.ipynb         <- 2. EDA, estrategia e hipótesis
└── Taller 1.pdf            <- enunciado del taller
```

### Ubicacion de cada punto del taller

| Punto del taller | Ubicación |
|---|---|
| 1. Entendimiento inicial de datos | `Calidad_Datos.ipynb` (dimensiones, tipos de datos, problemas de calidad y decisiones) y `eda_secop.ipynb`, sección 1 (Top 5 de atributos, análisis univariado y tratamiento aplicado) |
| 2. Estrategia de análisis | `eda_secop.ipynb`, sección 2 |
| 3. Desarrollo de la estrategia | `eda_secop.ipynb`, sección 3 |
| 4. Generación de resultados | _completar: informe ejecutivo o presentación_ |

## Orden de ejecución

Los notebooks son independientes (cada uno carga los datos desde el parquet), pero deben leerse y ejecutarse en el siguiente orden, debido a que el segundo ejecuta decisiones que estan basadas en en el primero:

1. **`Calidad_Datos.ipynb`**: identifica y documenta los problemas de calidad de datos y las decisiones de tratamiento.
2. **`eda_secop.ipynb`**: aplica esas decisiones y desarrolla el análisis, la estrategia y las pruebas de hipótesis.

Cada notebook debe ejecutarse completo, desde arriba hacia abajo.

## Instrucciones de ejecución

Requisitos: [Miniconda o Anaconda](https://docs.conda.io/en/latest/miniconda.html) y Git. Abrir la carpeta en VS Code y seleccionar el kernel `secop-eda`.

## Dependencias

Definidas en `environment.yml`:

| Paquete | Versión | Uso |
|---|---|---|
| Python | 3.11 | |
| pandas | ≥ 3.0 | Manipulación de datos (el código depende del tipo `str` de pandas 3) |
| numpy | | Cálculo numérico y regresión por mínimos cuadrados |
| pyarrow | | Lectura del archivo parquet |
| matplotlib | ≥ 3.9 | Visualizaciones (usa el parámetro `tick_labels` de `boxplot`) |
| scipy | | Pruebas de hipótesis |
| jupyter / ipykernel | | Ejecución de los notebooks |

## Principales hallazgos (insights)

_Completar al cerrar el punto 4. Resumir en 4 a 6 viñetas los hallazgos que respaldan los criterios de focalización, cada uno con su cifra clave._

## Limitaciones

_Completar al cerrar el punto 4 (calidad de los datos de origen, periodo analizado, carácter observacional del análisis, etc.)._
