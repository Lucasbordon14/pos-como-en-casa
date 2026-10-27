# Indicadores de control y estándares de desempeño

Este documento define cómo se controla el cumplimiento de las metas M1 a M4 de la Entrega N.º 2. Corresponde a la etapa de **Control** del proceso administrativo: **medir** el desempeño real, **compararlo** con un estándar y **corregir** los desvíos. Las mediciones se ubican en los hitos del Gantt: la prueba integral con medición de metas (tarea 4.2, semana 16), la prueba piloto con soporte (5.3, semanas 19–20) y la evaluación de resultados frente a las metas (5.4, semana 20).

Como en la Entrega N.º 2, las metas miden solo la parte del proceso que depende del sistema. Por ejemplo, el tiempo que el cliente tarda en elegir no se incluye.

## Criterios generales

- **Fórmula en porcentaje de casos, no en promedio.** Un promedio esconde los casos que fallan. Si 99 comandas llegan en 1 s y una tarda 2 minutos, el promedio da unos 2,2 s y parece que todo anda bien, pero una mesa esperó 2 minutos. El porcentaje da 99 % y muestra la falla.
- **Estándar = el valor de la meta.** La Entrega N.º 2 no prevé excepciones ("transmisión ≤ 5 s", "0 errores"), así que el estándar es 100 % y cada caso que no lo cumple se registra como **desvío** y se analiza su causa.
- **Medir y evaluar son tareas distintas.** Mide quien está en el local durante la prueba, y evalúa frente al estándar el responsable de la tarea 5.4. Después del proyecto, el control queda a cargo de la propietaria, que es quien usa la información del sistema para dirigir el negocio (Entrega N.º 3).

## M1 – Pedidos y comandas (historias POS-5 y POS-6)

Meta: reducir el tiempo entre la toma del pedido y su recepción en cocina en horario pico a menos de 1 minuto, con una transmisión a cocina de no más de 5 s desde su confirmación. La meta tiene dos tramos que se miden con fuentes distintas, por eso lleva dos indicadores.

### M1-a – Transmisión a cocina

| Elemento | Definición |
|---|---|
| **Fórmula** | (Comandas con `fecha_hora_recepcion − fecha_hora_envio` ≤ 5 s ÷ total de comandas) × 100 |
| **Estándar** | 100 %. Cada comanda de más de 5 s es un desvío. |
| **Frecuencia** | Diaria durante la prueba integral y la piloto, con foco en el horario pico. Semanal después de la implementación. |
| **Fuente del dato** | Entidad **Comanda** (registro automático del sistema). |
| **Responsable** | Medición: ambos integrantes (4.2) y Valentin (5.3). Evaluación: Lucas (5.4). Después del proyecto: la propietaria. |

**Recepción** es el momento en que **la tablet de cocina muestra la comanda**, no el momento en que el servidor la guarda. El tramo servidor → tablet forma parte de la transmisión. Aunque el local tiene cobertura de wifi y datos todo el día, el indicador existe justamente para detectar cuándo esa transmisión falla.

### M1-b – Toma del pedido → recepción en cocina

| Elemento | Definición |
|---|---|
| **Fórmula** | (Pedidos cronometrados en menos de 1 min ÷ total de pedidos cronometrados) × 100 |
| **Estándar** | 100 % |
| **Frecuencia** | En la prueba integral (4.2) y en cada día de la piloto (5.3), en horario pico. |
| **Fuente del dato** | Planilla de cronometraje (ver más abajo). Es la "medición con cronómetro" prevista en la Entrega N.º 2. |
| **Responsable** | Medición: ambos integrantes (4.2) y Valentin (5.3). Evaluación: Lucas (5.4). |

Se mide con cronómetro porque el sistema no puede saber cuándo el cliente terminó de elegir, y la Entrega N.º 2 excluye ese tiempo de la meta. El cronómetro arranca cuando el cliente terminó de elegir y se detiene cuando la tablet muestra la comanda.

**Planilla de cronometraje (M1-b):**

| Fecha | Mesa | N.º de comanda | Inicio (cliente terminó de elegir) | Recepción (tablet muestra) | Tiempo (mm:ss) | ¿Horario pico? | Medido por |
|---|---|---|---|---|---|---|---|

El número de comanda permite cruzar los datos con M1-a. Si un pedido supera el minuto, se puede ver si la demora estuvo en la transmisión (sistema) o en la carga del pedido (moza).

## M2 – Cobro (historia POS-7)

Meta: generar el total de cada mesa en menos de 10 s, con 0 errores de cálculo durante el período de prueba. La Entrega N.º 2 prevé dos formas de verificación: cronómetro y control de las cuentas. Por eso lleva dos indicadores.

### M2-a – Tiempo de cálculo del total

| Elemento | Definición |
|---|---|
| **Fórmula** | (Cuentas cronometradas con total en menos de 10 s ÷ total de cuentas cronometradas) × 100 |
| **Estándar** | 100 % |
| **Frecuencia** | En la prueba integral (4.2) y en cada día de la piloto (5.3). |
| **Fuente del dato** | Planilla de cronometraje de cuentas: fecha, mesa, inicio (la moza pide el total en el sistema), fin (el total aparece en pantalla), tiempo (mm:ss) y quién midió. |
| **Responsable** | Medición: ambos integrantes (4.2) y Valentin (5.3). Evaluación: Lucas (5.4). |

### M2-b – Exactitud de las cuentas

| Elemento | Definición |
|---|---|
| **Fórmula** | (Cuentas con error de cálculo o de promoción ÷ total de cuentas revisadas) × 100 |
| **Estándar** | 0 % |
| **Frecuencia** | En la prueba integral (4.2), sobre todas las cuentas de prueba. Diaria durante la piloto (5.3). |
| **Fuente del dato** | **Recálculo manual de las cuentas**: a partir del detalle cargado (cantidad × precio unitario − descuento de cada línea), se calcula el total a mano y se compara con el que generó el sistema. En la prueba integral se recalculan todas las cuentas. En la piloto, todas las que tienen promoción (por ejemplo, el 2x1 en jugos) más una muestra de las demás. |
| **Responsable** | Medición: ambos integrantes (4.2) y Valentin (5.3). Evaluación: Lucas (5.4). Después del proyecto: la propietaria. |

**Qué errores cuentan para M2-b.** M2 mide el **cálculo del total**, así que solo cuentan dos tipos de error:

- **Cálculo:** el total no coincide con la suma de las líneas.
- **Promoción:** el descuento aplicado no corresponde a la promoción vigente.

Otros dos tipos de error se registran como desvíos, pero no de M2:

- **Carga:** la moza cargó un producto o una cantidad que no correspondía. Se registra como desvío de POS-5, porque es lo que busca evitar el resumen de confirmación antes de enviar la comanda. Se detecta por un reclamo del cliente o de la moza al entregar.
- **Cobro:** por ejemplo, un vuelto mal dado o una transferencia que no se recibió. No depende del sistema, y se detecta en el **arqueo diario**: lo cobrado según el sistema, separado por `medio_pago`, se compara con el efectivo contado y con las transferencias recibidas. Esa comparación toma como base el registro que la dueña ya lleva, con una columna de efectivo y otra de transferencias (Entrega N.º 3).

**Por qué el arqueo no sirve como fuente de M2-b.** Un control solo detecta un error si compara contra una fuente independiente de lo que se quiere controlar. Si el sistema calcula mal un total, el cliente paga ese total mal calculado, y la caja coincide con lo que registró el sistema. El arqueo cierra igual, y el error de cálculo pasa sin detectarse. Tampoco alcanza con comparar las cuentas contra los pedidos registrados, porque el sistema calcula el total desde esos mismos registros. Por eso la fuente es el recálculo manual: es un cálculo independiente del que hace el sistema.

## M3 – Escalabilidad

Meta: gestionar en simultáneo las 11 mesas, un catálogo de hasta 200 productos y al menos un año de historial (≈ 11.000 pedidos) sin degradar el tiempo de respuesta.

| Elemento | Definición |
|---|---|
| **Fórmula** | Con la carga simulada: (comandas con transmisión ≤ 5 s ÷ total de comandas de la prueba) × 100, y (cuentas con total en menos de 10 s ÷ total de cuentas de la prueba) × 100 |
| **Estándar** | 100 % en ambos |
| **Frecuencia** | Una vez en la etapa de pruebas (4.2), y se repite después de la corrección de errores (4.3) si hubo desvíos. |
| **Fuente del dato** | Prueba de carga con datos simulados: 11 mesas con pedidos en simultáneo, 200 productos activos y una base con 11.000 pedidos. Los tiempos se toman de la entidad Comanda (M1-a) y del cronometraje de cuentas (M2-a). |
| **Responsable** | Medición: ambos integrantes (4.2). Evaluación: Lucas (5.4). |

M3 reutiliza los estándares de M1 y M2. "Sin degradar el tiempo de respuesta" significa que, con el volumen pensado para la futura comercialización, se siguen cumpliendo los mismos tiempos que con la demanda actual.

## M4 – Plazo de implementación

Meta: implementar el sistema en funcionamiento en el local en un plazo máximo de 20 semanas desde el inicio del desarrollo (05/10/2026 a la semana del 15/02/2027).

| Elemento | Definición |
|---|---|
| **Fórmula** | Desvío de plazo = semana real de cumplimiento del hito − semana planificada. Seguimiento: (tareas terminadas a la fecha ÷ tareas planificadas a la fecha) × 100 |
| **Estándar** | Desvío ≤ 0 semanas en el hito final (semana 20). Seguimiento: 100 % de las tareas de la ruta crítica al día. |
| **Frecuencia** | Semanal (revisión del tablero), y en cada hito de control: validación de prototipos (semana 6), prueba integral (semana 16) y evaluación de resultados (semana 20). |
| **Fuente del dato** | Diagrama de Gantt (Entrega N.º 2) como plan, y tablero de Jira como registro del avance real. Como establece la Entrega N.º 2, "el seguimiento de las tareas se realizará en Jira". Siguiendo Scrum, las tareas del Gantt se cargan en el backlog de cada sprint a medida que avanza el proyecto. Por eso hoy Jira tiene solo las tres historias de usuario del Sprint 1. |
| **Responsable** | Seguimiento: ambos integrantes, porque la ruta crítica incluye tareas de los dos (Entrega N.º 2). Evaluación final: Lucas (5.4). |

Si se detecta un atraso en una tarea de la ruta crítica, la acción correctiva es usar la holgura prevista: la semana de espera entre el diseño y la construcción de la base de datos (semana 6) y el margen de contingencia de la semana 12. Se usa primero la holgura más cercana al atraso, para no consumir antes de tiempo la reserva del receso de Navidad.

### Desvío registrado N.º 1 – Tarea 1.4 (historias de usuario)

| Elemento | Registro |
|---|---|
| **Tarea** | 1.4 Redacción y priorización de historias de usuario (ambos integrantes). Pertenece a la ruta crítica. |
| **Planificado** | Semana 3 (19/10 al 25/10). |
| **Real** | Semana 4: se formalizó el 26/10, primer día de la semana, con la aprobación del PR #1. |
| **Desvío** | +1 semana. |
| **Causa** | La tarea se postergó porque el equipo organizó su trabajo según los requisitos de cada entrega académica, y las historias de usuario recién se exigieron en la Entrega N.º 4. |
| **Acción correctiva** | Se usó la holgura de la semana 6. El diseño de la base de datos (2.1) y el diseño de interfaces (2.2), que dependen de 1.4, pasan a las semanas 5–6, y el hito de validación de prototipos (2.3), a la semana 7. La construcción de la base de datos (3.1) sigue empezando en la semana 7, por lo que la ruta crítica y el plazo final no cambian. El margen de contingencia de la semana 12 queda intacto. |
| **Impacto en otros hitos** | El hito 2.3 se corre una semana, pero no pertenece a la ruta crítica: la tarea que depende de él (3.2) empieza en la semana 9. |
| **Aprendizaje** | Las tareas del Gantt se cargan en el backlog de cada sprint, para que no dependan de las fechas de entrega. |

## Acción ante desvíos

Cada desvío (una comanda de más de 5 s, una cuenta con error, una tarea atrasada) se registra con fecha, causa probable y acción correctiva. Durante las pruebas, los desvíos se corrigen en la tarea 4.3 (corrección de errores) antes de la instalación. Durante la piloto, se resuelven como parte del soporte (5.3) y se consideran en la evaluación final (5.4).

## Cambio al diccionario de datos que requiere M1

Para medir M1-a se incorporó la entidad **Comanda**, que representa cada envío a cocina. Un pedido puede tener varios envíos: cuando la mesa pide algo más, se agrega al pedido abierto y a cocina viaja solo lo nuevo. Por eso, dos campos de fecha en Pedido se pisarían con cada envío. El cambio se ubica en la tarea 2.1 del Gantt (diseño de la base de datos), en la que la Entrega N.º 3 ya preveía ampliar el diccionario preliminar.

| Campo | Tipo de dato | Descripción funcional |
|---|---|---|
| id_comanda | Integer | Identificador único de cada envío a cocina. |
| id_pedido | Integer | Clave foránea: pedido (cuenta de la mesa) al que pertenece. |
| estado | String | Pendiente, en preparación, lista o entregada (en femenino, porque son estados de la comanda). |
| fecha_hora_envio | DateTime | Momento en que la moza confirma y el sistema envía la comanda. |
| fecha_hora_recepcion | DateTime | Momento en que la tablet de cocina muestra la comanda. |

Además:

- En **Detalle de Pedido**, `id_pedido` se reemplaza por `id_comanda`, para que cada dato se registre una sola vez. El total (M2) se sigue calculando sumando las líneas de todas las comandas del pedido.
- En **Pedido**, `estado` pasa a ser abierto o cobrado, y `fecha_hora` es el momento en que se abre la cuenta.
