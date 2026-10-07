# Proposal

## Why

Las reservas y cancelaciones manuales por WhatsApp dependen principalmente de Daniela, generan carga operativa y riesgo de errores, y pueden provocar sobrecupos o cupos desaprovechados. El autoservicio para consultar clases, reservar y cancelar es la necesidad prioritaria para reducir esa dependencia y mejorar el uso de la capacidad.

## What Changes

- Incorporar la consulta semanal de clases y disponibilidad, y permitir reservar y cancelar según capacidad y las condiciones de membresía.
- Controlar la capacidad, el límite de reservas activas por fecha calendario y el saldo de las membresías por paquete; las membresías ilimitadas no requieren saldo, están sujetas al límite diario y mantienen pendiente su política de penalización.
- Permitir a Daniela registrar asistencia o no-show.
- Incorporar un dashboard operativo básico con ocupación, cancelaciones tardías y no-shows, información sobre reservas múltiples y tendencias de las últimas cuatro semanas.
- Pagos, funcionalidades para instructores, lista de espera, analítica avanzada, predicciones y recomendaciones quedan fuera de este cambio.

## Capabilities

### New Capabilities

- `class-booking`: gestión funcional del flujo de reservas de clases del MVP, incluyendo consulta semanal de clases y disponibilidad, reservas, cancelaciones, capacidad, límites de reservas, reglas de membresía, registro de asistencia y dashboard operativo básico.

### Modified Capabilities

No hay capacidades existentes que modificar.

## Impact

- **Socios:** podrán consultar clases y disponibilidad, y gestionar reservas y cancelaciones conforme a las condiciones vigentes.
- **Daniela:** reducirá la gestión manual por WhatsApp y podrá supervisar la operación, gestionar excepciones y registrar asistencia.
- **Marcela:** tendrá información básica para evaluar las reservas y la capacidad y tomar decisiones operativas y de producto.
- **Operación del gimnasio:** contará con un flujo de reservas y control de capacidad orientado a reducir sobrecupos y subutilización.

Quedan fuera del alcance los pagos, las funcionalidades para instructores, la lista de espera, la analítica avanzada, las predicciones y las recomendaciones. La política de penalización para membresías ilimitadas sigue pendiente de decisión de Marcela.
