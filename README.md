# POS Como en Casa

Sistema de punto de venta (POS) para la cafetería y pastelería artesanal **"Como en Casa"**: toma de pedidos desde el celular de la moza, comandas digitales en una tablet de cocina y cálculo automático de la cuenta con registro del medio de pago.

Trabajo Práctico Integrador de **Organización Empresarial**, Tecnicatura Universitaria en Programación a Distancia, Universidad Tecnológica Nacional.

## Integrantes

- Lucas Bordón ([@Lucasbordon14](https://github.com/Lucasbordon14))
- Valentin Thorlet ([@ValentinThorlet](https://github.com/ValentinThorlet))

## Enlaces

- **Tablero de gestión ágil (Jira):** https://lucasbor14.atlassian.net/jira/software/projects/POS/boards/1. Requiere invitación: el plan gratuito de Jira no permite acceso público. Las capturas del tablero están en el documento final del TPI.
- **Proceso de venta en mesa (BPMN):** [docs/proceso-venta-pos.svg](docs/proceso-venta-pos.svg). El archivo editable es [docs/proceso-venta-pos.bpmn](docs/proceso-venta-pos.bpmn) y se abre en [bpmn.io](https://demo.bpmn.io).

## Documentación

| Archivo | Contenido |
|---|---|
| [docs/historias-usuario.md](docs/historias-usuario.md) | Historias de usuario POS-5, POS-6 y POS-7, con sus criterios de aceptación y la definición de terminado del Sprint 1. |
| [docs/proceso-venta-pos.bpmn](docs/proceso-venta-pos.bpmn) | Modelo BPMN del proceso de venta en mesa: pools Cliente y Cafetería, lanes Atención al cliente y ventas, Producción y Sistema POS. |
| [docs/indicadores-control.md](docs/indicadores-control.md) | Indicadores de control y estándares de desempeño de las metas M1 a M4, y el registro de desvíos. |

## Forma de trabajo

- Cada tarea se desarrolla en su propia rama (`docs/<tema>`), nunca directamente sobre `main`.
- Los commits siguen la convención [Conventional Commits](https://www.conventionalcommits.org/es/v1.0.0/) e incluyen la clave de la historia de Jira cuando corresponde (por ejemplo, `POS-5`).
- Cada Pull Request lo revisa y aprueba el otro integrante, con un comentario sobre el contenido, y se integra con *Create a merge commit*.
- El tablero de Jira está vinculado al repositorio mediante GitHub for Atlassian: cada historia muestra sus ramas, commits y Pull Requests.

## Declaración de Uso de IA

Cada integrante trabajó con un asistente de IA generativa (Claude, de Anthropic) en sus propias sesiones. Lo usamos para guiar con preguntas la redacción de las historias de usuario y la definición del flujo del proceso, para generar el archivo `.bpmn` a partir del flujo que definimos nosotros, para acompañar la configuración de GitHub Desktop, Jira y su integración, para revisar los indicadores y su coherencia con las entregas anteriores, y para redactar los textos a partir de nuestras decisiones.

**Prompt base y por qué lo usamos.** *"Guiame paso a paso, una cosa por vez. Antes de darme una solución, haceme preguntas para que yo proponga, porque en el coloquio tengo que poder explicar y defender cada decisión. Todo tiene que ser coherente con las Entregas 1, 2 y 3. Si encontrás una contradicción, marcámela."* Lo formulamos así para que las decisiones fueran nuestras y para usar al asistente como control de coherencia entre las entregas, no como fuente de contenido. En parte de los indicadores M2 a M4, por falta de tiempo, le pedimos respuestas directas, que revisamos contra las Entregas 2 y 3 antes de usarlas.

**Correcciones humanas sobre los resultados del asistente:**

- **BPMN:** corregimos el bucle de confirmación (el pedido se modifica, no se vuelve a cargar), agregamos el momento de consumo antes de pedir algo más, descartamos tarjeta y QR porque el local no los ofrece, ajustamos la verificación de transferencias a cómo se hace en el local y señalamos que la preparación es responsabilidad de la cocina, lo que obligó a corregir el organigrama.
- **Entidad Comanda:** el asistente advirtió que dos campos de fecha en Pedido se pisarían con cada agregado. Valentin propuso tratar cada envío como una unidad separada y, al contrastarlo con la Entrega 3, lo reformulamos como la entidad Comanda, que validamos entre los dos antes de usarla.
- **Fuente de M2-b:** en la revisión del PR #3, el asistente propuso usar el arqueo diario como alarma de errores de cálculo. Al analizarlo detectamos que no funcionaba, porque si el sistema calcula mal, el cliente paga ese total y la caja cierra igual, y lo reemplazamos por el recálculo manual de las cuentas.
- **Acción correctiva del desvío N.º 1:** el asistente propuso usar el margen de contingencia de la semana 12. Al verificar el Gantt usamos la holgura de la semana 6, que absorbe el atraso sin consumir la reserva de Navidad.

Los datos del caso y todas las decisiones fueron nuestros. Asumimos la responsabilidad sobre la veracidad y coherencia del trabajo, incluidos los errores que pudieran provenir de las herramientas utilizadas.
