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
| 4. Generación de resultados | `informe_ejecutivo.md` |

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

Resumen; el detalle completo está en `informe_ejecutivo.md`.

- Cerca de la mitad de los contratos (47.9%) presenta al menos una desviación en su ejecución; la más frecuente es el cierre sin liquidar (28.5%).
- **El sector y el orden de la entidad son los factores más predictivos**: la tasa de desviación va del 34.0% (Inteligencia Estratégica) al 71.7% (Ciencia y Tecnología) según el sector, y del 45.8% al 59.6% según el orden.
- El efecto de la modalidad de contratación depende del sector: "Contratación régimen especial" tiene 91.1% de desviación en Defensa pero solo 13.5% en Interior — la combinación sector×modalidad es más informativa que cada atributo por separado.
- **El valor del contrato y el destino del gasto no sirven como criterio de priorización**: su correlación con la desviación es prácticamente nula, contrario a la intuición inicial.
- Una regresión lineal de días adicionados en función del valor y las categorías del Top 5 explica apenas 1.2% de la varianza (R² = 0.012), evidencia adicional de que estos factores por sí solos no predicen bien la magnitud de la desviación.
- Se proponen 4 niveles de prioridad de supervisión combinando sector, modalidad y orden (ver `informe_ejecutivo.md`, sección 4).

## Limitaciones

- El análisis es observacional: las asociaciones encontradas no implican causalidad.
- No se aplicaron pruebas de significancia estadística formal (chi-cuadrado, t-test); los contrastes son descriptivos, consistente con las técnicas vistas en el curso.
- Dos de las tres señales de desviación solo se observan en contratos cerrados o terminados (51.5% del total); los contratos de 2025 muestran una tasa de cierre más baja (36.0% vs. 53-59% en años anteriores), aunque se verificó que las conclusiones no cambian al excluirlos.
- El dataset tenía un valor atípico extremo (un contrato mal digitado por 1.28e16) que fue identificado y excluido (ver `Calidad_Datos.ipynb`, celdas 3.5-3.6); persisten otras inconsistencias menores de calidad ya documentadas y tratadas.
- El valor del contrato y el destino del gasto se incluyeron en el análisis porque el enunciado del taller los señala explícitamente, no porque los datos los respalden como buenos discriminadores.
