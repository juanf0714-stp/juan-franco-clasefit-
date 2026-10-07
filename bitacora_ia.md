# Bitácora de uso de IA

## Herramientas utilizadas

- **ChatGPT:** apoyo para analizar el caso, discutir decisiones de producto, instalar y configurar OpenSpec, y resolver dudas y validaciones durante el ejercicio.
- **Codex CLI:** ejecución de tareas y edición de archivos dentro del proyecto.
- **OpenSpec:** estructuración del flujo `proposal → specs` y validación del change.
- **Node.js/npm:** instalación y ejecución de las herramientas.

Trabajé de forma incremental y decidí no entregar a Codex todos los documentos de la prueba para que resolviera el ejercicio completo. Mantuve bajo mi responsabilidad las decisiones de producto y utilicé la IA para explorar, estructurar, cuestionar y validar.

## Prompts clave

### Prompt 1 · Exploración del problema

Pedí analizar el caso antes de diseñar una solución. La IA identificó el problema principal y los secundarios, actores y necesidades, ambigüedades, preguntas de descubrimiento y casos límite. Traté sus inferencias como material para explorar, no como decisiones: después definí el MVP, las reglas de negocio y las preguntas abiertas.

### Prompt 2 · Diseño del MVP

Compartí con Codex las decisiones de producto y pedí estructurarlas en `diseno_producto.md`. Entre ellas: límite inicial de tres reservas activas por fecha calendario, corte de cancelación de una hora, reglas para membresías por paquete, membresía ilimitada sujeta al límite diario, registro de asistencia y dashboard básico. Dejé instructores y pagos fuera del MVP, y la política para membresías ilimitadas como decisión pendiente. El criterio fue que Codex ordenara las decisiones sin inventar funcionalidades ni resolver preguntas abiertas.

### Prompt 3 · Proposal y specs

Usé `diseno_producto.md` y `openspec/project.md` como fuentes de verdad. Codex estructuró inicialmente seis capabilities y seis specs a partir de la estructura propuesta por OpenSpec. Al contrastarlo con el enunciado, que proponía una única spec delta en `specs/class-booking/spec.md`, decidí consolidar las seis capacidades en una capability `class-booking` y una sola spec, conservando los comportamientos funcionales necesarios.

### Prompt 4 · Revisión de specs

La primera versión tenía 22 requisitos y 24 escenarios. En la revisión humana eliminé la referencia al instructor, precisé la información sobre reservas múltiples sin suponer una métrica y reemplacé un resultado no observable para las reservas con membresía ilimitada. Tras consolidar, la spec final quedó con 19 requisitos y 24 escenarios. No inventé la política de penalización para membresías ilimitadas; sigue abierta para Marcela.

## Lo que corregí o descarté

| # | Qué me entregó la IA | Qué hice yo | Por qué |
|---|---|---|---|
| 1 | Incluyó al instructor en la información de las clases | Lo eliminé | No estaba definido como parte del alcance |
| 2 | Propuso un indicador del comportamiento de reservas múltiples | Lo reformulé como información sobre reservas múltiples | No había una métrica definida |
| 3 | Indicó que el sistema “evalúa la reserva” para membresías ilimitadas | Lo reformulé | No era un resultado observable ni verificable |
| 4 | Separó las capacidades en seis specs | Las consolidé en una única spec | El enunciado proponía una única spec delta y prioricé alinearme con él |

La validación técnica de OpenSpec pasó antes y después de las correcciones, pero la validación técnica no sustituyó mi revisión funcional de los requisitos, escenarios y decisiones de producto.

## Resultado de validación

```text
openspec validate add-class-booking

Change 'add-class-booking' is valid
```
