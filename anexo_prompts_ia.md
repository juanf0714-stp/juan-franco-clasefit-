# Anexo · Prompts y uso de IA

> Documento complementario a `bitacora_ia.md`. Este anexo conserva con mayor detalle los principales prompts utilizados durante el ejercicio y el resultado obtenido de la IA. La bitácora principal contiene únicamente el resumen requerido para la entrega.

## 1. Exploración del problema

### Objetivo

Comprender el problema antes de diseñar una solución, separando la información explícita de las inferencias y decisiones pendientes.

### Prompt utilizado

```text
$openspec-explore

Te voy a pasar la transcripción de una conversación con Marcela, la dueña de un gimnasio ubicado en un barrio de Medellín.

Quiero analizarla contigo como primer paso de diseño de producto. Ayúdame a entender bien el problema antes de pensar en la solución.

A partir de la conversación, identifica:
- cuál es el problema principal y cuáles son los problemas secundarios;
- quiénes son los usuarios o actores involucrados y qué necesita cada uno;
- qué necesidades están explícitamente mencionadas;
- qué cosas quedan ambiguas o requieren una decisión de negocio;
- qué preguntas debería resolver un PO/BA antes de definir el MVP;
- qué casos límite o situaciones problemáticas deberíamos tener presentes.

No propongas todavía una solución ni conviertas el análisis en requisitos o user stories. Tampoco crees ni modifiques archivos.

Distingue entre lo que está explícitamente dicho en la conversación y lo que estés infiriendo. Si algo no está claro, prefiero que lo señales como una pregunta abierta antes que asumir una respuesta.

Aquí está la transcripción:
--- INICIO ---
[transcripción del caso de Marcela]
--- FIN ---
```

### Resultado de la IA

La exploración identificó:

- **Problema principal:** las reservas gestionadas por WhatsApp pueden generar sobrecupos y espacios desaprovechados, además de carga operativa para la persona que administra las reservas.
- **Problemas secundarios:** cancelaciones tardías, no-shows y miembros que reservan varias clases el mismo día y finalmente solo asisten a una.
- **Actores:** miembros, persona encargada de las reservas, instructores y propietaria. La participación de algunos actores fue tratada por la IA como inferencia cuando no estaba explícitamente definida.
- **Necesidades explícitas:** consultar las clases de la semana, conocer la capacidad disponible, reservar y cancelar.
- **Ambigüedades relevantes:** límite de cancelación, comportamiento cuando una clase está llena, límite de reservas por día, tratamiento de no-shows, cambios de capacidad y comportamiento ante dos personas intentando reservar el último cupo.
- **Casos límite:** reserva simultánea del último cupo, cancelaciones cercanas al inicio, cambios de clase o capacidad y reservas múltiples.

### Criterio aplicado

No tomé las inferencias de la IA como decisiones de producto. Utilicé el resultado para identificar qué debía decidir como PO/BA y qué debía permanecer como pregunta abierta.

---

## 2. Diseño del MVP

### Objetivo

Convertir las decisiones de producto tomadas durante el análisis en un documento claro de diseño, sin adelantarse todavía a los requisitos formales de OpenSpec.

### Prompt de trabajo

```text
Voy a compartir contigo las decisiones de producto que tomé para el caso ClaseFit.

Quiero que estructures estas decisiones en diseno_producto.md.

No quiero que diseñes una solución diferente ni agregues funcionalidades nuevas. El documento debe reflejar las decisiones proporcionadas, dejando explícitamente como preguntas abiertas aquellas que todavía no están decididas.

Incluye:
- problema;
- usuarios y actores;
- alcance del MVP;
- reglas de negocio y su justificación;
- supuestos;
- preguntas abiertas;
- wireframe conceptual como bonus.

Entre las decisiones definidas están:
- máximo inicial de 3 reservas activas por fecha calendario;
- límite de cancelación de 1 hora;
- reglas de reintegro para membresías por paquete;
- membresía ilimitada sujeta al límite diario;
- registro de asistencia;
- dashboard básico para seguimiento operativo;
- instructores y pagos fuera del MVP;
- política de penalización para membresías ilimitadas como pregunta abierta.

No conviertas estas decisiones todavía en requisitos SHALL/MUST ni en escenarios Gherkin.
```

### Resultado

Entre las decisiones estructuradas quedaron:

- máximo inicial de **3 reservas activas por fecha calendario**;
- límite aplicable a membresías por paquete e ilimitadas;
- descuento inmediato de una clase al reservar con membresía por paquete;
- reintegro si se cancela con al menos una hora de anticipación;
- no reintegro ante cancelación tardía o no-show;
- membresía ilimitada sin saldo, pero sujeta al límite diario;
- reserva condicionada a la capacidad disponible;
- liberación inmediata del cupo al cancelar;
- imposibilidad de reservar dos veces la misma clase;
- imposibilidad de reservar una clase ya iniciada;
- registro de asistencia por parte de Daniela;
- dashboard básico para medir la efectividad de la solución y reducir reportes manuales;
- instructores y pagos fuera del MVP;
- política de penalización para membresías ilimitadas como pregunta abierta para Marcela.

### Criterio aplicado

Codex debía estructurar decisiones ya tomadas, no inventar funcionalidades ni resolver preguntas abiertas.

---

## 3. Proposal y primera versión de specs

### Objetivo

Pasar del diseño de producto a la estructura de OpenSpec utilizando `diseno_producto.md` y `openspec/project.md` como fuentes de verdad.

### Prompt de trabajo

```text
Usa diseno_producto.md y openspec/project.md como fuentes de verdad para preparar el change add-class-booking.

Genera la propuesta y las specs necesarias para representar el comportamiento definido en el diseño de producto.

Los requisitos deben cubrir como mínimo:
- consulta de clases y capacidad;
- reservas;
- capacidad disponible;
- concurrencia sobre el último cupo;
- cancelaciones;
- límite de cancelación de 1 hora;
- límite inicial de 3 reservas por fecha;
- membresías por paquete e ilimitadas;
- registro de asistencia y no-show;
- dashboard básico.

Cada requisito debe ser verificable y tener al menos un escenario. Incluye escenarios de error o límite.

No inventes la política de penalización para membresías ilimitadas, porque continúa como pregunta abierta.
```

### Resultado inicial

La primera estructura generada por Codex separó el comportamiento en seis capabilities/specs:

1. `class-booking`
2. `class-cancellation`
3. `capacity-availability`
4. `membership-reservation-limits`
5. `attendance-tracking`
6. `operational-dashboard`

La primera versión contenía **22 requisitos y 24 escenarios**.

Al contrastar esta estructura con el enunciado de la prueba, observé que la entrega sugerida era una única spec delta:

```text
specs/class-booking/spec.md
```

Por esa razón decidí consolidar las seis capacidades en una única capability `class-booking` y una sola spec, manteniendo dentro de ella los comportamientos funcionales que correspondían al MVP.

### Criterio aplicado

La estructura de OpenSpec fue tratada como un medio para expresar la solución, no como sustituto del criterio de producto ni del formato solicitado por la prueba.

---

## 4. Revisión funcional y consolidación

### Objetivo

Revisar críticamente la salida de la IA antes de considerar terminada la spec.

### Prompt de revisión

```text
Revisé las specs generadas y quiero hacer únicamente correcciones puntuales.

1. Eliminar la referencia al instructor en la información de las clases, porque no está definido dentro del alcance del MVP.
2. Revisar la expresión "indicador del comportamiento de reservas múltiples" y reemplazarla por una formulación observable que no suponga una métrica que no hemos definido.
3. Revisar la frase "el sistema evalúa la reserva" para membresías ilimitadas y reemplazarla por un resultado observable y verificable.
4. Consolidar las seis specs en una única:
   specs/class-booking/spec.md

Mantén todos los comportamientos funcionales definidos en el MVP y no agregues funcionalidades nuevas.

Después ejecuta:
openspec validate add-class-booking
```

### Correcciones realizadas

**1. Instructor**

La IA había incluido al instructor dentro de la información consultable de las clases.

**Decisión:** eliminarlo.

**Motivo:** aunque los instructores aparecen en el problema como actores con una necesidad potencial, su funcionalidad no fue incluida en el MVP.

**2. Indicador de reservas múltiples**

La IA había utilizado una expresión equivalente a “indicador del comportamiento de reservas múltiples”.

**Decisión:** reformularlo como información sobre reservas múltiples.

**Motivo:** no se había definido una métrica específica ni un indicador formal.

**3. Membresía ilimitada**

La IA había utilizado una formulación equivalente a “el sistema evalúa la reserva”.

**Decisión:** reemplazarla por un resultado observable, expresando que la reserva puede confirmarse sin requerir saldo cuando se cumplen las demás condiciones.

**Motivo:** “evaluar” describe una acción interna del sistema, pero no define un comportamiento verificable.

**4. Consolidación de specs**

Las seis specs iniciales fueron consolidadas en:

```text
openspec/changes/add-class-booking/specs/class-booking/spec.md
```

La spec final quedó con:

- **19 requisitos**
- **24 escenarios**
- escenarios de error y límite;
- reglas de capacidad;
- concurrencia sobre el último cupo;
- cancelaciones;
- límite de 1 hora;
- límite de 3 reservas por fecha;
- membresías por paquete e ilimitadas;
- asistencia/no-show;
- dashboard básico.

La política de penalización para membresías ilimitadas no fue inventada y permanece como pregunta abierta para Marcela.

### Validación

```text
openspec validate add-class-booking

Change 'add-class-booking' is valid
```

### Criterio aplicado

La validación de OpenSpec confirmó la consistencia estructural del change, pero no sustituyó la revisión funcional. La decisión final sobre qué aceptar, modificar o descartar fue responsabilidad del PO/BA.

---

## 5. Principio de trabajo con IA

El enfoque utilizado durante el ejercicio fue incremental:

```text
Problema
   ↓
Exploración con IA
   ↓
Decisiones de producto
   ↓
Diseño del MVP
   ↓
Proposal
   ↓
Specs
   ↓
Revisión humana
   ↓
Validación OpenSpec
```

Se evitó entregar a Codex todos los documentos de la prueba y solicitarle que resolviera el ejercicio completo. La intención fue utilizar la IA como apoyo para:

- explorar el problema;
- identificar ambigüedades y casos límite;
- estructurar decisiones;
- transformar decisiones en documentación;
- revisar la calidad de los requisitos;
- validar la estructura OpenSpec.

El criterio de producto, el alcance del MVP, las reglas de negocio y las decisiones sobre qué aceptar, modificar o descartar permanecieron bajo responsabilidad humana.
