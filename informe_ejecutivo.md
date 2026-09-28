# Informe ejecutivo: focalización de la supervisión de contratos de bienes

Oficina de Control Interno
**Base de datos analizada:** 196.390 contratos de compraventa y suministro (2019 al 2025), los cuales fueron registrados en SECOP II. Se excluyó 1 registro debido a la inconsistencia presentada en el valor del contrato (detalles en Calidad_Datos.ipynb, celdas 3.5 y 3.6).
**Soporte:** Los datos y analisis presentados en este informe son los resultados de `eda_secop.ipynb` y `Calidad_Datos.ipynb`.

## 1. Diagnostico inicial y conclusiones del analisis

- **Cerca del 50% de los contratos (47,9%) presenta por lo menos una desviación en la ejecución.** La irregularidad mas pronunciada es cerrar el contrato sin liquidarlo (28,5% de todos los contratos), le siguen el cierre de contratos dejando más del 10% del presupuesto sin pagar al cierre (24,0%) y de adicionar plazo (9,5%).
- **El riesgo depende de quién contrata y cómo contrata.** El sector, el tipo de entidad como la modalidad de contratacion segregan los grupos con tasas de desviación bastante diferentes, combinados va del 13,5% al 91,1%.
- **Ni el monto de contrato ni el destino del gasto sirven para identificar qué contratos se desvían**, por lo que no se recomiendan como criterios de selección.
- **Se proponen cuatro niveles de prioridad**  para enfocar la supervisión en los contratos con mayor probabilidad de desviarse a partir del momento de la firma.

## 2. Indicadores de desviacion 

Se marcó un contrato como "desviado" si presenta al menos una de estas tres anomalias (cabe aclarar que pueden coincidir en un mismo contrato):

| Señal | Definición | % de contratos |
|---|---|---|
| Prorroga en tiempo | Días adicionados mayores a 0 | 9,5% |
| Presupuesto no ejecutado | Contrato ya finalizado donde la cuenta por pagar  sobrepasa el 10% del total del valor adjudicado | 24,0% |
| Inexistencia de liquidacion | Contrato cerrado o terminado que omitió el proceso formal de liquidación | 28,5% |

## 3. Factores de riesgo

| Factor | Evidencia | Criterio de filtro |
|---|---|---|
| **Sector** | Brechas existentes desde el 34,0% (inteligencia estratégica) hasta el 71,7% (ciencia y tecnología). Los sectores que presentan más contratos: defensa 56,0% (34.585 contratos), salud  54,5% (22.037) y trabajo 53,2% (14.759), en contraste al servicio público 43,2% (37.390). | Sí |
| **Modalidad de contratación** | Régimen especial con ofertas 62,3% y licitación pública con 59,6%, frente a 45,8% en mínima cuantía y en contratación directa. Adicionalmente las dos primeras modalidades acumulan más días de prórroga, en promedio 9,8 y 7,9 días más, respectivamente, que la contratación directa con ofertas bajo condiciones similares (valor, orden y destino del gasto). | Sí |
| **Tipo de entidad** | Las corporaciones autónomas sobresalen con un 59,6% de contratos con desviaciones, entidades nacionales con un 49,7% y territoriales con un 45,8%. | Sí |
| **Sector × modalidad** | Un mismo procedimiento de régimen especial llega al 91,1% de desviacion en defensa, al 89,8% en agricultura pero, baja significativamente al 13,5% en el sector interior. | Sí (criterio principal) |
| **Valor del contrato** | Mediana de $37,5 millones en contratos desviados frente a $30,2 millones en los  cumplidos (correlación de Spearman 0,07). Multiplicar el valor por 10 tan solo suma  4,6 días de prórroga en promedio, explicando solo el 1,2% de la variación. | No como filtro, útil para jerarquizar cada nivel |
| **Destino del gasto** | Los contratos etiquetados para funcionamiento se desvian en 48,0% mientras que inversión es de 47,6%. | No |

## 4. Criterios de focalización recomendados

Para escoger los factores de riesgo se definió: sector, modalidad u orden cuya tasa de desviación supere el promedio general (47,9%) en al menos 5 puntos, es decir 52,9% o más, y con al menos 30 contratos para evitar conclusiones apresuradas de grupos pequeños, los criterios resultantes son:

- Sectores: Ciencia y Tecnología (71,7%), Presidencia de la República (61,1%), Relaciones Exteriores (60,5%), Información Estadística (60,0%), Defensa (56,0%), Salud y Protección Social (54,5%), Industria (54,5%) y Trabajo (53,2%).
- Modalidades: régimen especial con ofertas (62,3%), licitación pública (59,6%) y selección abreviada de menor cuantía, con y sin manifestación de interés (54,1% y 54,2%).
- Orden: corporaciones autónomas (59,6%).

Con esos factores proponemos 4 niveles de prioridad:

| Nivel | Regla | Acción sugerida |
|---|---|---|
| 1. Alta | Régimen especial en defensa (91,1%) o agricultura (89,8%) — las combinaciones más altas del análisis | Seguimiento cercano desde la firma: cronograma de entregas, pagos y liquidación |
| 2. Media | Dos o más factores de riesgo a la vez (ej. un contrato de salud adjudicado en régimen especial con ofertas) | Revisión en hitos: a mitad del plazo y al cierre |
| 3. Monitoreo | Un solo factor de riesgo | Alertas automáticas: vencimiento sin liquidar, pagos por debajo del 90% al cierre y prórrogas |
| 4. Estándar | Sin factores de riesgo | Control rutinario |

Un par de cosas a tener en cuenta al aplicar esto: dentro de cada nivel conviene atender primero los contratos de mayor valor (no porque el valor prediga la desviación, sino porque aumenta el impacto cuando sí ocurre); y como el cierre sin liquidar es la desviación más frecuente (28,5% de los contratos), esa alerta de liquidación al vencer el plazo debería activarse para todos los contratos, sin importar el nivel. El destino del gasto no se usa como criterio porque funcionamiento e inversión se desvían casi igual.

## 5. Limitaciones

El análisis es observacional — las asociaciones que encontramos no implican causalidad, no podemos afirmar que cambiar la modalidad de un contrato vaya a cambiar su probabilidad de desviarse.

Tampoco aplicamos pruebas de significancia formales: las diferencias entre grupos grandes son claras a simple vista, pero en grupos chicos (Inteligencia Estratégica tiene apenas 100 contratos, por ejemplo) la tasa puede variar bastante de un año a otro. Por eso exigimos mínimo 30 contratos por grupo antes de confiar en una cifra.

Dos de las tres señales de desviación solo se pueden observar en contratos ya cerrados o terminados (51,5% del total), lo que introduce un sesgo hacia años más viejos: en 2025 apenas el 36,0% de los contratos está cerrado, contra 53-59% en años anteriores, así que los contratos recientes van a verse artificialmente "menos desviados" de lo que en realidad terminarán estando.

También hay temas de calidad de los datos de origen que vale la pena mencionar: la mediana del valor pagado registrado es 0, lo que sugiere que buena parte de los pagos no se registra en SECOP II (y eso puede estar inflando la señal de presupuesto no ejecutado); el sector todavía tiene una categoría "No aplica/No pertenece" con 24.465 contratos sin asignar; y la duración del contrato tiene problemas en el 21,7% de los registros (detalle en `Calidad_Datos.ipynb`).

Por último, el número de contratos crece bastante durante el periodo (de 16.425 en 2019 a 40.113 en 2025), así que los años no son del todo comparables entre sí, y los umbrales que usamos (promedio + 5 puntos, mínimo 30 contratos) son decisiones nuestras, no verdades absolutas — recomendamos recalcularlos cada año con datos más recientes.
