# Bitácora de uso de IA

## Herramientas que usé
1. Inicialmente usé ChatGPT para que me guiara en las instalaciones desde la terminal de mi Mac. En pocos minutos tenía a punto lo siguiente. También creé una carpeta para usarla como directorio activo en esta prueba.
Homebrew  7.0.8       ✅
Node.js   26.10.0     ✅
npm       11.19.1     ✅
OpenSpec  1.14.1      ✅

2. Luego decidí usar Codex CLI porque se puede integrar con OpenSpec y me permite trabajar directamente sobre los archivos del proyecto desde la terminal (y por disponibilidad ya que está incluido en mi plan de ChatGPT).

3. Con Node.js, OpenSpec y Codex configurados, inicialicé el proyecto y dejé habilitadas las skills de OpenSpec, estableciendo el entorno necesario para comenzar el ejercicio y trabajar de forma iterativa con la IA bajo mi revisión y criterio.

4. Aunque era posible proporcionar a Codex los documentos completos de la prueba y solicitarle que generara los entregables, decidí trabajar de forma incremental. Proporcioné el contexto necesario en cada etapa y utilicé la IA como apoyo para explorar, estructurar y validar mis decisiones, manteniendo bajo mi responsabilidad el análisis del problema, el alcance, las reglas de negocio y los criterios de aceptación. Busqué reproducir un flujo de trabajo más cercano a una situación real de PO/BA.
-

## Prompts clave (3 a 5)
| # | Etapa (diseño / proposal / specs) | Prompt | Qué obtuve |
|---|---|---|---|

| 1 | Exploración | $openspec-explore Te voy a pasar la transcripción de una conversación con Marcela, la dueña de un gimnasio ubicado en un barrio de Medellin.

Quiero analizarla contigo como primer paso de diseño de producto, somos senior Product Owners expertos en proyectos de tecnología en IA. Ayúdame a entender bien el problema antes de pensar en la solución.

A partir de la conversación, identifica:
- cuál es el problema principal y cuáles son los problemas secundarios;
- quiénes son los usuarios o actores involucrados y qué necesita cada uno;
- qué necesidades están explícitamente mencionadas;
- qué cosas quedan ambiguas o requieren una decisión de negocio;
- qué preguntas debería resolver un PO/BA antes de definir el MVP;
- qué casos límite o situaciones problemáticas deberíamos tener presentes.

No propongas todavía una solución ni conviertas el análisis en requisitos o user stories.

Distingue entre lo que está explícitamente dicho en la conversación y lo que estés infiriendo. Si algo no está claro, prefiero que lo señales para que iteremos en lugar de asumir de forma inmediata. | Qué obtuve 

## Lo que cuenta la conversación

**Explícitamente dicho:** el gimnasio lleva seis años funcionando y tiene alrededor de 250 socios. Las reservas se gestionan por WhatsApp con ayuda de Daniela, la recepcionista. Hay clases grupales con cupos distintos: spinning, 20; funcional, 15; yoga, 12; rumba, aproximadamente 30.

**Explícitamente dicho:** a veces se excede el cupo y otras veces quedan espacios vacíos porque algunas personas reservan y no asisten. La dueña quiere que los socios puedan consultar las clases de la semana, ver los cupos disponibles, reservar y cancelar desde el celular. También quiere que los instructores puedan ver cuántas personas están inscritas. El pago de mensualidad por una app es algo que le gustaría tener “algún día”, pero no es urgente ahora.

## Problema principal

**Explícitamente dicho:** la gestión de reservas por WhatsApp le genera carga a Daniela y no evita errores de cupo ni las pérdidas de espacios por inasistencias. La necesidad inmediata es que los socios puedan reservar y cancelar sin depender de Daniela.

**Inferencia:** el problema parece combinar dos cosas: coordinación manual que recae en recepción y falta de una manera confiable de relacionar las reservas con la capacidad de cada clase. La conversación no permite saber cuál de las dos causa más impacto.

## Problemas secundarios

- **Explícito:** algunos socios reservan varias clases el mismo día y solo asisten a una.
- **Explícito:** la dueña quiere evitar cancelaciones de última hora, pero aún no define qué significa “última hora”.
- **Explícito:** los instructores quieren conocer el número de inscritos.
- **Inferencia:** los cupos que quedan vacíos podrían estar relacionados con las reservas que no se usan, aunque no se indica con qué frecuencia pasa ni cuánto afecta la asistencia.

## Actores y necesidades

| Actor | Necesidad expresada | Lo que falta entender |
|---|---|---|
| Socios | Ver las clases de la semana, consultar cupos, reservar y cancelar desde el celular. | Si todos tienen celular o acceso digital; si necesitan ayuda; cómo se enteran de cambios o de que ya no hay cupo. |
| Daniela, recepcionista | **Inferido:** dejar de gestionar manualmente cada reserva por WhatsApp y evitar errores de cupo. | Si seguirá atendiendo excepciones, cambios o problemas de socios. |
| Instructores | Ver cuántas personas están inscritas en sus clases. | Si necesitan solo un total o también nombres, cambios y hora de consulta. |
| Dueña | Reducir problemas operativos y controlar las reservas sin ser “tan estricta”. | Qué resultados espera y qué reglas considera aceptables. |

## Necesidades explícitas

1. Consultar las clases de la semana desde el celular.
2. Ver cuántos cupos quedan.
3. Reservar una clase y poder cancelar si no se va a asistir.
4. Evitar cancelaciones a última hora, con un plazo aún por definir.
5. Controlar a quienes reservan varias clases en un día y asisten solo a una, manteniendo flexibilidad para quienes sí hacen doble clase.
6. Permitir que los instructores vean cuántas personas están inscritas.
7. Mantener el pago de mensualidades fuera de la urgencia actual.

## Ambigüedades y decisiones de negocio

- ¿“Clases de la semana” significa una semana fija o una ventana móvil de siete días? ¿Con cuánta anticipación se publican?
- ¿El cupo cuenta reservas confirmadas, asistentes presentes o ambos? ¿Qué pasa cuando alguien cancela?
- ¿Cuál es el límite de cancelación y qué pasa si alguien intenta cancelar después?
- ¿Qué significa “controlar” las reservas múltiples? ¿Un límite, una advertencia, una revisión posterior u otra regla? La conversación no define esto.
- ¿Cómo se distingue una doble clase legítima de varias reservas que no se usarán?
- ¿Qué debe pasar con una clase llena si alguien cancela? No se menciona lista de espera ni cómo se asignaría un cupo liberado.
- ¿Quién puede modificar horarios, cupos o clases? No se especifica.
- ¿Los instructores solo consultan el total de inscritos o necesitan otra información?
- ¿La disponibilidad de cupos debe actualizarse inmediatamente para todos? La conversación no define expectativas sobre actualización ni concurrencia.

## Preguntas para resolver antes de definir el MVP

1. ¿Cuál es el principal resultado esperado: menos trabajo para Daniela, evitar sobrecupos, reducir espacios vacíos o una combinación? ¿Cómo sabrían que mejoró?
2. ¿Cuántas reservas, cancelaciones e inasistencias ocurren en una semana típica, y con qué frecuencia hay sobrecupos?
3. ¿Con cuántas horas de anticipación se permite cancelar y qué ocurre fuera de ese plazo?
4. ¿Qué regla consideran razonable para las reservas múltiples y qué excepciones debe permitir?
5. ¿Qué información necesita ver un instructor y en qué momento?
6. ¿Quién administra el calendario y los cupos?
7. ¿Cómo se enteran los socios de una clase llena, un cambio de horario o un cupo liberado?
8. ¿Qué papel debe conservar Daniela cuando la reserva ya no pase por ella?

## Casos límite que conviene tener presentes

- Dos socios intentan reservar el último cupo casi al mismo tiempo.
- Un socio cancela cuando la clase ya está llena o muy cerca de empezar.
- Una persona reserva y no llega; no se indica cómo se registra la asistencia.
- Un socio necesita reservar dos clases el mismo día y otra persona reserva varias sin intención de asistir a todas.
- Cambian el horario, el instructor o el cupo después de que ya existen reservas.
- Una clase se cancela o no se dicta.
- Un socio intenta reservar una clase llena, o cancelar una reserva que no encuentra.
- Las cifras de capacidad son aproximadas en algunos casos —por ejemplo, rumba tiene “como 30”— y deberían confirmarse antes de tomar decisiones sobre cupos.

El proyecto tiene OpenSpec, pero no hay cambios activos ni especificaciones existentes relevantes. Por ahora, el análisis queda como conversación; no he creado artefactos ni planteado una solución.| 




| 1 | Exploración | |
| 1 | Exploración | |
| 1 | Exploración | |
| 1 | Exploración | |

## Lo que corregí o descarté
| # | Qué me entregó la IA | Qué hice yo | Por qué |
|---|---|---|---|
| 1 | Un resultado muy completo de exploración pero con mucha información poco relevante y demasiado amplia para la definición de un MVP | Seleccionar lo realmente relevante para atender el problema principal, por ejemplo de momento no atender la necesidad de pago desde el celular o las funciones de consulta para los instructores del gimnasio. También omitir supuestos que en términos reales no son tan críticos, como preocuparnos de si todos los clientes tiene acceso a internet y un celular para poder reservar sus clases | Porque esto no es clave para la definición de un mínimo viable, son aspectos que pueden ir a un backlog a futuro para entregas de valor incrementales o lo que conocemos como funcionalidades nice to have en las que inicialmente no nos generarían tanto valor como atender el problema principal. |
 

## Resultado de `openspec validate`
```
(pega aquí la salida)
```
