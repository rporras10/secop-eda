# Informe ejecutivo: focalización de la supervisión de contratos de bienes

Oficina de Control Interno
**Base de datos analizada:** 196.390 contratos de compraventa y suministro (2019 y 2025), los cuales fueron registrados en SECOP II. Se excluyó 1 registro debido a la inconcistencia presentada en el valor pendiente de pago  (detalles en Calidad_Datos.ipynb, celdas 3.5 y 3.6).
**Soporte:** Los datos y analisis presentados en este informe son los resultados de `eda_secop.ipynb` y `Calidad_Datos.ipynb`.

## 1. Diagnostico inicial y conclusiones del analisis

- **Cerca del 50% de los contratos (47,9%) presenta por lo menos una desviación en la ejecución.** La irregularidad mas pronunciada es cerrar el contrato sin liquidarlo (28,5% de todos los contratos), le siguen el cierre de contratos dejando más del 10% del presupuesto sin pagar al cierre (24,0%) y de adicionar plazo (9,5%).
- **El riesgo esta concentrado en gran medida de quién contrata y cómo contrata.** El sector, el tipo de entidad como la modalidad de contratacion segregan los grupos con tasas de desviación bastante diferentes, el nivel de desviacion va del 13,5% al 91,1%.
- **Ni el monto de contrato ni el destino del gasto sirven para prevenir fallas**, por lo que no se recomiendan como criterios de selección.
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
| **Modalidad de contratación** | Régimen especial con 62,3% y licitación pública con 59,6%, frente a 45,8% en mínima cuantía y en contratación directa. Adicionalmente las dos primeras modalidades acumulan más días de prórroga: entre 9,8 y 7,9 días adicionales que la contratación directa con condiciones similares (valor, orden y destino del gasto). | Sí |
| **Tipo de entidad** | Las corporaciones autónomas sobresalen con un 59,6% de contratos con desviaciones, entidades nacionales con un 49,7% y territoriales con un 45,8%. | Sí |
| **Sector × modalidad** | Un mismo procedimiento de régimen especial llega al 91,1% de desviacion en defenza, al 89,8% en agricultura pero, baja significativamente al 13,5% en el sector interior. | Sí (criterio principal) |
| **Valor del contrato** | Mediana de $37,5 millones en contratos desviados frente a $30,2 millones en los  cumplidos (correlación de Spearman 0,07). Multiplicar el valor por 10 tan solo suma  4,6 días de prórroga en promedio, explicando solo el 1,2% de la variación. | No como filtro, util para jerarquizar cada nivel |
| **Destino del gasto** | Los contratos etiquetados para funcionamiento se desvian en 48,0% mientras que inversión es de 47,6%. | No |

## 4. Criterios de focalización recomendados

**Factor de riesgo:** sector, modalidad u orden cuya tasa de desviación supera en al menos 5 puntos el promedio (es decir, 52,9% o más), con al menos 30 contratos. Con los resultados del análisis, los factores son:

- **Sectores:** Ciencia y Tecnología (71,7%), Presidencia de la República (61,1%), Relaciones Exteriores (60,5%), Información Estadística (60,0%), Defensa (56,0%), Salud y Protección Social (54,5%), Industria (54,5%) y Trabajo (53,2%).
- **Modalidades:** régimen especial con ofertas (62,3%), licitación pública (59,6%) y selección abreviada de menor cuantía, con y sin manifestación de interés (54,1% y 54,2%).
- **Orden:** corporaciones autónomas (59,6%).

| Nivel | Regla | Acción sugerida |
|---|---|---|
| **1. Alta** | Contratación en régimen especial de los sectores defensa (91,1%) y agricultura (89,8%), las combinaciones de mayor desviación del análisis | Seguimiento cercano desde la firma: cronograma de entregas, pagos y liquidación |
| **2. Media** | Contratos con dos o más factores de riesgo (por ejemplo, un contrato del sector salud adjudicado en régimen especial con ofertas) | Revisión en hitos: a mitad del plazo y al cierre |
| **3. Monitoreo** | Contratos con un solo factor de riesgo | Alertas automáticas: vencimiento sin liquidar, pagos por debajo del 90% al cierre y prórrogas |
| **4. Estándar** | Contratos sin factores de riesgo | Control rutinario |

**Reglas de aplicación:**

1. Dentro de cada nivel, atender primero los contratos de mayor valor: el valor no predice la desviación, pero sí aumenta el impacto cuando ocurre.
2. Como el cierre sin liquidar es la desviación más frecuente (28,5% de los contratos), activar para **todos** los contratos una alerta de liquidación al vencer el plazo, sin importar su nivel.
3. No usar el destino del gasto como criterio: funcionamiento e inversión se desvían prácticamente igual.

## 5. Limitaciones

1. **El análisis es observacional.** Las asociaciones encontradas no implican causalidad: no se puede afirmar que cambiar la modalidad de un contrato cambie su probabilidad de desviarse.
2. **Dos de las tres señales solo se observan en contratos cerrados o terminados** (51,5% del total). Los grupos con más contratos cerrados pueden mostrar tasas más altas en parte por esa razón, y los contratos recientes aparecen con menos desviación de la real: en 2025 solo el 36,0% está cerrado o terminado.
3. **No se aplicaron pruebas de significancia formales.** Las diferencias entre grupos grandes son claras, pero las tasas de grupos pequeños pueden variar de un año a otro (por ejemplo, Inteligencia Estratégica tiene 100 contratos). Por eso se exigió un mínimo de 30 contratos por grupo.
4. **Calidad de los datos de origen:**
   - La mediana del valor pagado registrado es 0, lo que sugiere que parte de los pagos no se registra en SECOP II. Esto puede inflar la señal de presupuesto no ejecutado.
   - El sector conserva la categoría "No aplica/No pertenece" (24.465 contratos), que no se pudo asignar a ningún sector.
   - La duración del contrato presenta problemas en el 21,7% de los registros (ver `Calidad_Datos.ipynb`).
5. **El número de contratos publicados crece durante el periodo**, de 16.425 firmados en 2019 a 40.113 en 2025, por lo que los años no son del todo comparables entre sí.
6. **Los umbrales (promedio + 5 puntos y mínimo de 30 contratos) son decisiones del análisis.** Se recomienda recalcularlos cada año con los datos más recientes.
