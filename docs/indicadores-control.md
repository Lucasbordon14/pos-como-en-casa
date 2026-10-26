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
| **Fórmula** | (Cuentas con error ÷ total de cuentas cobradas) × 100 |
| **Estándar** | 0 % |
| **Frecuencia** | Diaria durante la piloto (cierre de caja). En la prueba integral, sobre todas las cuentas de prueba. |
| **Fuente del dato** | 1) **Arqueo diario:** lo cobrado según el sistema, separado por `medio_pago`, se compara con el efectivo contado en caja y con las transferencias recibidas. 2) **Revisión manual de las cuentas con promociones** (por ejemplo, el 2x1 en jugos): se recalcula a mano el total y se compara con el del sistema. |
| **Responsable** | Medición: ambos integrantes (4.2) y Valentin (5.3). Evaluación: Lucas (5.4). Después del proyecto: la propietaria, en su cierre de caja. |

No alcanza con comparar las cuentas contra los pedidos registrados. El sistema calcula el total desde esos mismos registros, así que se estaría comparando consigo mismo. Los errores que sí pueden ocurrir son **de carga** (un producto o cantidad mal cargados) o **de promoción** (un descuento mal aplicado), y se detectan comparando con una fuente externa al cálculo: la caja real. Esa comparación toma como base el registro que la dueña ya lleva, con una columna de efectivo y otra de transferencias (Entrega N.º 3).

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
| **Fuente del dato** | Diagrama de Gantt (Entrega N.º 2) y tablero de Jira (estado de las tareas por sprint). |
| **Responsable** | Seguimiento: ambos integrantes, porque la ruta crítica incluye tareas de los dos (Entrega N.º 2). Evaluación final: Lucas (5.4). |

Si se detecta un atraso en una tarea de la ruta crítica, la acción correctiva es usar la holgura prevista: el margen de contingencia de la semana 12 y la semana de espera entre el diseño y la construcción de la base de datos (semana 6).

## Acción ante desvíos

Cada desvío (una comanda de más de 5 s, una cuenta con error, una tarea atrasada) se registra con fecha, causa probable y acción correctiva. Durante las pruebas, los desvíos se corrigen en la tarea 4.3 (corrección de errores) antes de la instalación. Durante la piloto, se resuelven como parte del soporte (5.3) y se consideran en la evaluación final (5.4).

## Cambio al diccionario de datos que requiere M1

Para medir M1-a se incorporó la entidad **Comanda**, que representa cada envío a cocina. Un pedido puede tener varios envíos: cuando la mesa pide algo más, se agrega al pedido abierto y a cocina viaja solo lo nuevo. Por eso, dos campos de fecha en Pedido se pisarían con cada envío. El cambio se ubica en la tarea 2.1 del Gantt (diseño de la base de datos), en la que la Entrega N.º 3 ya preveía ampliar el diccionario preliminar.

| Campo | Tipo de dato | Descripción funcional |
|---|---|---|
| id_comanda | Integer | Identificador único de cada envío a cocina. |
| id_pedido | Integer | Clave foránea: pedido (cuenta de la mesa) al que pertenece. |
| estado | String | Pendiente, en preparación, listo o entregado. |
| fecha_hora_envio | DateTime | Momento en que la moza confirma y el sistema envía la comanda. |
| fecha_hora_recepcion | DateTime | Momento en que la tablet de cocina muestra la comanda. |

Además:

- En **Detalle de Pedido**, `id_pedido` se reemplaza por `id_comanda`, para que cada dato se registre una sola vez. El total (M2) se sigue calculando sumando las líneas de todas las comandas del pedido.
- En **Pedido**, `estado` pasa a ser abierto o cobrado, y `fecha_hora` es el momento en que se abre la cuenta.
