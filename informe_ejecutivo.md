# Informe ejecutivo: focalización de la supervisión de contratos de bienes

**Para:** Oficina de Control Interno
**Base de datos:** 196.390 contratos de compraventa y suministro firmados entre 2019 y 2025 y publicados en SECOP II. Se excluyó 1 registro con un valor de contrato erróneo (ver `Calidad_Datos.ipynb`, celdas 3.5 y 3.6).
**Soporte:** todas las cifras de este informe provienen de los resultados de `eda_secop.ipynb` y `Calidad_Datos.ipynb`.

## 1. Mensajes clave

- **Casi la mitad de los contratos (47,9%) presenta al menos una desviación en su ejecución.** La más frecuente es cerrar el contrato sin liquidarlo (28,5% de todos los contratos), seguida de dejar más del 10% del presupuesto sin pagar al cierre (24,0%) y de adicionar plazo (9,5%).
- **El riesgo depende sobre todo de quién contrata y cómo contrata.** El sector, la modalidad de contratación y el tipo de entidad separan grupos con tasas de desviación muy distintas, y su combinación va del 13,5% al 91,1%.
- **El valor del contrato y el destino del gasto casi no distinguen los contratos que se desvían**, por lo que no se recomiendan como criterios de selección.
- **Proponemos cuatro niveles de prioridad** construidos con esos tres factores, para concentrar la supervisión cercana en los contratos con mayor probabilidad de desviarse desde el momento de la firma.

## 2. Cómo se midió la desviación

Un contrato se considera desviado si presenta al menos una de estas tres señales (pueden coincidir en un mismo contrato):

| Señal | Definición | % de contratos |
|---|---|---|
| Adición de plazo | Días adicionados mayores a 0 | 9,5% |
| Presupuesto no ejecutado | Contrato cerrado o terminado con más del 10% de su valor pendiente de pago | 24,0% |
| Cierre sin liquidar | Contrato cerrado o terminado sin liquidación | 28,5% |

## 3. Qué se asocia con la desviación

| Factor | Evidencia | ¿Sirve como criterio? |
|---|---|---|
| **Sector** | Tasas entre 34,0% (Inteligencia Estratégica) y 71,7% (Ciencia y Tecnología). Entre los sectores con más contratos: defensa 56,0% (34.585 contratos), Salud y Protección Social 54,5% (22.037) y Trabajo 53,2% (14.759), frente a Servicio Público 43,2% (37.390). | Sí |
| **Modalidad de contratación** | Régimen especial con ofertas 62,3% y licitación pública 59,6%, frente a 45,8% en mínima cuantía y en contratación directa. Estas dos modalidades también acumulan más días de prórroga: en promedio 9,8 y 7,9 días más que la contratación directa con ofertas, con igual valor, orden y destino del gasto. | Sí |
| **Tipo de entidad (orden)** | Corporaciones autónomas 59,6%, entidades nacionales 49,7% y territoriales 45,8%. | Sí (corporaciones autónomas) |
| **Sector × modalidad** | La misma modalidad cambia de riesgo según el sector: la contratación en régimen especial llega a 91,1% en defensa y a 89,8% en agricultura, y baja a 13,5% en el sector interior. | Sí, es el criterio más fuerte |
| **Valor del contrato** | Mediana de $37,5 millones en contratos desviados frente a $30,2 millones en los no desviados (correlación de Spearman 0,07). Cada vez que el valor se multiplica por 10 se suman en promedio 4,6 días de prórroga, pero el modelo explica solo el 1,2% de la variación. | No como filtro; sí para ordenar dentro de cada nivel, por su mayor impacto |
| **Destino del gasto** | Funcionamiento 48,0% frente a inversión 47,6%. | No |

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
