# ClaseFit — Diseño de producto

## 1. Problema

La gestión ineficiente de la capacidad de las clases genera sobrecupos y subutilización de los espacios disponibles. Actualmente, las reservas y cancelaciones se gestionan manualmente por WhatsApp y dependen principalmente de Daniela, la recepcionista. Esto genera carga operativa, riesgo de errores, reservas que pueden superar la capacidad y espacios desaprovechados cuando las personas reservan y no asisten.

El objetivo inmediato es que los socios gestionen directamente sus reservas y cancelaciones, con visibilidad de la disponibilidad, reduciendo la dependencia de Daniela y mejorando el uso de la capacidad disponible.

## 2. Usuarios y actores

### Socios / miembros

Necesitan consultar las clases de la semana, ver información básica y capacidad u ocupación, conocer los cupos disponibles y reservar desde el celular cuando cumplan las condiciones. También necesitan poder cancelar una reserva.

### Daniela

Es la responsable principal de la operación de reservas. Necesita reducir la gestión manual por WhatsApp, supervisar la operación, gestionar excepciones cuando sea necesario y registrar la asistencia de los socios.

### Marcela

Es la dueña del gimnasio. Necesita reducir los problemas operativos de reservas y capacidad, supervisar el comportamiento de las reservas, contar con información básica para evaluar la efectividad de la solución y tomar decisiones sobre reglas y futuras mejoras.

### Instructores

La necesidad de consultar cuántas personas están inscritas está identificada, pero la gestión o consulta para instructores queda fuera del MVP y pasa al backlog.

## 3. Alcance del MVP

### Qué entra

1. **Consulta semanal de clases:** mostrar las clases disponibles y la información básica de cada clase, incluida su capacidad y ocupación o cupos disponibles.
2. **Reserva de clases:** permitir reservar solo si existe capacidad, sin duplicar una reserva para la misma clase y respetando el saldo disponible de la membresía y el límite diario.
3. **Cancelación de reservas:** permitir cancelar. Con al menos una hora de anticipación, se libera inmediatamente el cupo. Con menos de una hora, se considera cancelación tardía y aplica la penalización correspondiente. En ambos casos, el cupo queda disponible para otro socio.
4. **Control de reservas múltiples:** aplicar un límite inicial de tres reservas activas por fecha calendario. El límite podrá modificarse posteriormente y el cambio no afectará las reservas ya realizadas.
5. **Control según tipo de membresía:** contemplar membresías por paquete e ilimitadas. En una membresía por paquete, reservar descuenta inmediatamente una clase; cancelar con al menos una hora de anticipación la reintegra; una cancelación tardía o un no-show no la reintegra. Sin saldo no se puede reservar. La membresía ilimitada no depende de un saldo de clases, pero sí está sujeta al límite diario.
6. **Registro de asistencia:** Daniela registra la asistencia de los socios en cada clase y marca para cada reserva si el socio asistió o no. En el MVP, una cancelación tardía y un no-show reciben el mismo tratamiento de penalización.
7. **Administración básica:** Marcela y Daniela tendrán las mismas capacidades administrativas. Esta decisión responde al tamaño reducido del negocio y a que ambas deben poder cubrir las necesidades operativas. Daniela mantiene la responsabilidad operativa principal.
8. **Dashboard básico:** presentar indicadores sencillos de porcentaje de ocupación, cancelaciones tardías y no-shows, comportamiento de reservas múltiples y tendencias de las últimas cuatro semanas. Su propósito es evaluar la efectividad de la solución y apoyar decisiones operativas, de producto y estratégicas, evitando volver a depender de reportes manuales en Excel. Se mantendrá deliberadamente simple, sin convertirse en un sistema avanzado de analítica.

### Qué queda fuera

- **Gestión o consulta para instructores:** la necesidad está identificada, pero no forma parte de la urgencia del MVP y puede abordarse posteriormente.
- **Pagos o mensualidades dentro de la aplicación:** quedan fuera del problema inmediato de reservas y capacidad.
- **Lista de espera y asignación automática desde una lista de espera:** no son necesarias para el flujo urgente y ampliarían el alcance.
- **Reglas de reserva diferentes por tipo de clase o personalizadas por usuario:** el MVP se limita a las reglas generales definidas; las variantes pueden evaluarse más adelante.
- **Analítica avanzada, predicciones o recomendaciones:** el dashboard se limita a indicadores básicos; el análisis avanzado puede abordarse cuando exista evidencia de necesidad.
- **Funcionalidades avanzadas de administración y otras no necesarias para resolver el problema inmediato:** se excluyen para mantener el alcance enfocado y podrán considerarse posteriormente si surge evidencia de necesidad.

### Justificación del alcance

El MVP se concentra en que los socios consulten disponibilidad, reserven y cancelen directamente, aplicando capacidad, membresía y límite diario. Esto aborda la dependencia operativa de Daniela y los problemas de sobrecupo y subutilización. El registro de asistencia permite identificar no-shows; el dashboard básico ayuda a evaluar si la solución funciona sin reintroducir reportes manuales. Las capacidades para instructores, pagos, listas de espera y analítica avanzada no son parte de la necesidad urgente o ampliarían el alcance, por lo que quedan para una etapa posterior si se confirma su necesidad.

## 4. Reglas de negocio decididas

| RN | Regla | Justificación |
|---|---|---|
| RN-01 | Cada clase tiene una capacidad máxima configurable. | Permite representar el aforo de cada clase y administrar la capacidad disponible. |
| RN-02 | Una reserva solo puede confirmarse si existe un cupo disponible. | Evita que las reservas superen la capacidad de la clase. |
| RN-03 | La disponibilidad debe reflejar una reserva o cancelación confirmada para las operaciones posteriores. | Mantiene la información de cupos alineada con las reservas y cancelaciones realizadas. |
| RN-04 | Si dos socios intentan reservar simultáneamente el último cupo, solo una reserva puede ser confirmada. | Evita exceder la capacidad cuando varias personas intentan tomar el último cupo. |
| RN-05 | Un socio no puede reservar dos veces la misma clase. | Evita duplicar la ocupación de una clase por un mismo socio. |
| RN-06 | El límite inicial es de tres reservas activas por fecha calendario. | Controla las reservas múltiples que pueden dejar cupos desaprovechados. |
| RN-07 | El límite diario aplica tanto a membresías por paquete como a membresías ilimitadas. | Mantiene un límite común de reservas múltiples para ambos tipos de membresía. |
| RN-08 | Una membresía por paquete debe tener saldo suficiente para realizar una reserva. | Evita reservar clases que excedan el saldo disponible del paquete. |
| RN-09 | Al confirmar una reserva de una membresía por paquete se descuenta inmediatamente una clase. | Refleja el uso del paquete desde el momento de la reserva. |
| RN-10 | Una cancelación realizada con al menos una hora de anticipación reintegra la clase de una membresía por paquete. | Devuelve el saldo cuando la cancelación ocurre dentro del plazo establecido. |
| RN-11 | Una cancelación realizada con menos de una hora de anticipación no reintegra la clase y se considera cancelación tardía. | Aplica la penalización decidida para cancelaciones tardías y conserva el consumo de la clase. |
| RN-12 | Un no-show tampoco reintegra la clase y recibe el mismo tratamiento que una cancelación tardía en el MVP. | Da un tratamiento común a los dos incumplimientos definidos para el MVP. |
| RN-13 | Una clase no puede reservarse una vez iniciada. | Evita reservar una clase cuyo horario ya comenzó. |
| RN-14 | Una cancelación libera inmediatamente el cupo. | Hace que el espacio vuelva a estar disponible para otro socio. |
| RN-15 | El cambio del límite diario de reservas no modifica las reservas existentes. | Permite ajustar la regla sin invalidar reservas ya realizadas. |
| RN-16 | Daniela registra la asistencia y determina si una reserva terminó en asistencia o no-show. | Permite identificar los no-shows y contar con información de asistencia. |
| RN-17 | Marcela y Daniela tienen las mismas capacidades administrativas en el MVP. | Por el tamaño del negocio, ambas deben poder cubrir las necesidades operativas. |

## 5. Supuestos

- Cada clase tiene una capacidad máxima definida.
- La capacidad de cada clase puede ser configurada por la administración.
- Las clases tienen una fecha y hora claramente definidas.
- La disponibilidad se actualiza después de una reserva o cancelación confirmada.
- Existen dos tipos de membresía: paquete e ilimitada.
- Los socios tienen un estado de membresía que permite determinar si pueden reservar.
- Daniela registra la asistencia de los socios.
- Las cancelaciones tardías y los no-shows reciben el mismo tratamiento en el MVP.
- El dashboard analiza tendencias de las últimas cuatro semanas.
- El límite inicial de reservas múltiples es de tres reservas activas por fecha calendario.
- El límite puede modificarse sin afectar reservas previamente realizadas.

## 6. Preguntas abiertas para Marcela

1. **¿Qué política de penalización quiere aplicar a los socios con membresía ilimitada cuando existe una cancelación tardía o no-show?**
   - **Alternativa A:** la primera cancelación tardía/no-show del mes no tiene penalización; posteriormente se aplica una penalización equivalente al valor de una clase.
   - **Alternativa B:** se utiliza un sistema de strikes; al llegar a tres, el socio no puede renovar o adquirir nuevamente una membresía ilimitada y debe utilizar una membresía por paquete.
2. **Si elige una penalización monetaria o equivalente para la membresía ilimitada, ¿cuál será el valor individual de una clase utilizado para calcularla?**
3. **¿Desea alguna funcionalidad administrativa exclusiva para ella?** La propuesta actual es mantener los mismos permisos para Marcela y Daniela debido al tamaño del negocio.

La elección de la política y cualquier funcionalidad exclusiva quedan pendientes de Marcela.

## 7. Bonus · Wireframe

```text
+--------------------------------------------------+
| ClaseFit                         Semana / fecha  |
|                         < 12 - 18 oct >          |
+--------------------------------------------------+
| LUN 12 OCT                                        |
| Spinning                         7:00 a. m.       |
| Cupos disponibles: 5 de 20                       |
| Estado: Disponible                 [ Reservar ]   |
+--------------------------------------------------+
| LUN 12 OCT                                        |
| Yoga                             8:00 a. m.       |
| Cupos disponibles: 0 de 12                       |
| Estado: Sin cupos                                |
+--------------------------------------------------+
| MAR 13 OCT                                        |
| Funcional                        6:00 p. m.       |
| Cupos disponibles: 1 de 15                       |
| Estado: Reservada                   [ Cancelar ]  |
+--------------------------------------------------+
```
