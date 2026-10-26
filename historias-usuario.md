# Historias de Usuario – POS Como en Casa

Las historias de usuario corresponden a la tarea 1.4 planificada en el Diagrama de Gantt (Entrega N.º 2) y se formalizan en esta entrega. Cada una surge de un componente del POS propuesto en la Entrega N.º 1 y se mide con una meta de la Entrega N.º 2.

| Clave Jira | Componente | Usuario | Meta |
|---|---|---|---|
| POS-5 | Toma de pedidos | Moza | M1 |
| POS-6 | Comandas en cocina | Personal de cocina | M1 |
| POS-7 | Cobro | Personal de atención y ventas | M2 |

---

## POS-5 – Toma de pedidos

**Como** moza, **quiero** registrar los pedidos de las mesas desde mi celular, **para** no tener que trasladarlos a la cocina y quedar disponible para atender otras mesas.

**Criterios de aceptación:**
- Antes de enviar el pedido, el sistema muestra un resumen para que la moza lo repita al cliente y lo confirme o lo modifique.
- La comanda llega a cocina en 5 segundos o menos desde que se confirma (meta M1).
- Se pueden agregar productos a un pedido mientras no esté cobrado.
- Solo se pueden elegir productos activos de la carta.

## POS-6 – Comandas en cocina

**Como** personal de cocina, **quiero** ver las comandas pendientes con su detalle y marcarlas en preparación y listas, **para** prepararlas sin errores de lectura o interpretación.

**Criterios de aceptación:**
- Las comandas se muestran en orden de llegada, con mesa, productos y cantidades.
- Al marcar una comanda como "lista", la moza recibe un aviso en su celular.

## POS-7 – Cobro

**Como** personal de atención y ventas, **quiero** ver el total de cada mesa calculado automáticamente y registrar el cobro con su medio de pago, **para** cobrar sin errores de cálculo, incluso cuando hay promociones.

**Criterios de aceptación:**
- El total se calcula sumando cantidad × precio unitario, menos el descuento de cada línea.
- El total se muestra en menos de 10 segundos, sin errores de cálculo (meta M2).
- Al registrar el cobro se elige el medio de pago (efectivo o transferencia) y el pedido pasa a estado "cobrado".

---

## Definición de terminado (Sprint 1 – Entrega 4)

En esta etapa el sistema todavía no se codifica (Codificación: semanas 7 a 14 del Gantt). Una historia pasa a **Listo** cuando en el repositorio están aprobados, mediante Pull Request:

1. Su tramo del proceso modelado en BPMN.
2. El indicador de control que mide su meta.
3. La historia con sus criterios de aceptación documentada en este archivo.
