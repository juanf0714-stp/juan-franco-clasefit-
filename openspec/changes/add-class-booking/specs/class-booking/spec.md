# Spec Delta

## Purpose

Permite a los socios gestionar el flujo de reservas de clases grupales, con control de capacidad, condiciones de membresía, registro de asistencia e indicadores operativos básicos.

## ADDED Requirements

### Requirement: Consulta semanal de clases y disponibilidad
El sistema SHALL permitir a los socios consultar las clases de la semana y ver la fecha, hora, ocupación o cupos disponibles e información básica de cada clase.

#### Scenario: Socio consulta las clases de la semana
- **WHEN** un socio consulta las clases de la semana
- **THEN** el sistema muestra las clases con fecha, hora, ocupación o cupos disponibles e información básica de la clase

### Requirement: Capacidad máxima por clase
El sistema SHALL mantener una capacidad máxima definida para cada clase, configurable por Marcela o Daniela.

#### Scenario: Administradora configura la capacidad de una clase
- **WHEN** Marcela o Daniela configura la capacidad máxima de una clase
- **THEN** el sistema registra esa capacidad máxima para la clase

### Requirement: Disponibilidad actualizada tras operaciones confirmadas
El sistema SHALL reflejar las reservas y cancelaciones confirmadas en la disponibilidad de la clase para las consultas y reservas posteriores.

#### Scenario: Se confirma una reserva
- **WHEN** se confirma una reserva para una clase
- **THEN** las consultas y reservas posteriores reflejan el cupo ocupado

#### Scenario: Se confirma una cancelación
- **WHEN** se confirma la cancelación de una reserva
- **THEN** las consultas y reservas posteriores reflejan el cupo liberado

### Requirement: Reservar una clase disponible
El sistema SHALL permitir confirmar una reserva para una clase no iniciada cuando existe un cupo y se cumplen las demás condiciones aplicables al socio.

#### Scenario: Reserva confirmada con cupo disponible
- **WHEN** un socio que cumple las condiciones aplicables reserva una clase no iniciada con cupo disponible
- **THEN** el sistema confirma la reserva

### Requirement: No duplicar una reserva activa
El sistema SHALL impedir que un socio cree una segunda reserva activa para la misma clase.

#### Scenario: Socio intenta reservar de nuevo la misma clase
- **WHEN** un socio que ya tiene una reserva activa intenta reservar la misma clase
- **THEN** el sistema no confirma una segunda reserva para ese socio y esa clase

### Requirement: No reservar una clase llena
El sistema SHALL impedir confirmar una reserva cuando la clase alcanzó su capacidad máxima.

#### Scenario: Socio intenta reservar una clase llena
- **WHEN** un socio intenta reservar una clase sin cupos disponibles
- **THEN** el sistema no confirma la reserva

### Requirement: Confirmación única para el último cupo
El sistema SHALL confirmar como máximo una reserva cuando dos socios intentan reservar simultáneamente el último cupo de una clase.

#### Scenario: Dos socios intentan reservar simultáneamente el último cupo
- **WHEN** dos socios intentan reservar al mismo tiempo el único cupo disponible
- **THEN** solo una de las dos reservas queda confirmada
- **AND** la capacidad de la clase no se excede

### Requirement: No reservar una clase iniciada
El sistema SHALL impedir confirmar una reserva para una clase que ya comenzó.

#### Scenario: Socio intenta reservar una clase que ya comenzó
- **WHEN** un socio intenta reservar una clase después de su hora de inicio
- **THEN** el sistema no confirma la reserva

### Requirement: Cancelar una reserva y liberar su cupo
El sistema SHALL permitir que un socio cancele una reserva activa y liberar inmediatamente el cupo para que pueda utilizarlo otro socio.

#### Scenario: Socio cancela una reserva activa
- **WHEN** un socio cancela una reserva activa
- **THEN** el sistema cancela la reserva y libera inmediatamente el cupo

### Requirement: Clasificar cancelaciones según anticipación
El sistema SHALL clasificar como oportuna una cancelación realizada con una hora o más antes del inicio de la clase y como tardía una cancelación realizada con menos de una hora.

#### Scenario: Cancelación con una hora o más de anticipación
- **WHEN** un socio cancela una reserva activa con una hora o más antes del inicio de la clase
- **THEN** el sistema registra la cancelación como oportuna

#### Scenario: Cancelación con menos de una hora de anticipación
- **WHEN** un socio cancela una reserva activa con menos de una hora antes del inicio de la clase
- **THEN** el sistema registra la cancelación como tardía
- **AND** permite cancelar y libera inmediatamente el cupo

### Requirement: Límite de reservas activas por fecha calendario
El sistema SHALL aplicar inicialmente un límite de tres reservas activas por socio y fecha calendario tanto a membresías por paquete como ilimitadas; Marcela o Daniela podrán modificarlo sin modificar ni invalidar reservas existentes.

#### Scenario: Socio intenta superar el límite diario
- **WHEN** un socio con tres reservas activas para una fecha calendario intenta reservar otra clase en esa fecha
- **THEN** el sistema no confirma la nueva reserva

#### Scenario: Administradora modifica el límite diario
- **WHEN** Marcela o Daniela modifica el límite de reservas por fecha calendario
- **THEN** las reservas existentes permanecen sin cambios
- **AND** las nuevas reservas se evalúan usando el límite vigente

### Requirement: Saldo suficiente para reservar con un paquete
El sistema SHALL impedir una reserva con membresía por paquete cuando el socio no tiene saldo de clases disponible.

#### Scenario: Socio intenta reservar sin saldo suficiente
- **WHEN** un socio sin clases disponibles en su paquete intenta reservar una clase
- **THEN** el sistema no confirma la reserva

### Requirement: Descontar clase del paquete al reservar
El sistema SHALL descontar inmediatamente una clase del saldo de una membresía por paquete cuando confirma una reserva.

#### Scenario: Reserva confirmada con membresía por paquete
- **WHEN** se confirma una reserva para un socio con membresía por paquete
- **THEN** el sistema descuenta una clase del saldo del paquete

### Requirement: Reintegrar clase del paquete tras cancelación oportuna
El sistema SHALL reintegrar al saldo del paquete la clase descontada cuando el socio cancela con una hora o más de anticipación.

#### Scenario: Socio cancela oportunamente con membresía por paquete
- **WHEN** un socio con membresía por paquete cancela una reserva con una hora o más antes del inicio de la clase
- **THEN** el sistema reintegra la clase al saldo del paquete

### Requirement: No reintegrar clase del paquete tras cancelación tardía o no-show
El sistema SHALL mantener consumida la clase del paquete ante una cancelación tardía o un no-show.

#### Scenario: Socio cancela tarde con membresía por paquete
- **WHEN** un socio con membresía por paquete cancela una reserva con menos de una hora antes del inicio de la clase
- **THEN** el sistema no reintegra la clase al saldo del paquete

#### Scenario: Socio no se presenta con membresía por paquete
- **WHEN** una reserva de un socio con membresía por paquete queda registrada como no-show
- **THEN** el sistema no reintegra la clase al saldo del paquete

### Requirement: Reservar con membresía ilimitada sin saldo de clases
El sistema SHALL permitir confirmar una reserva con membresía ilimitada sin requerir saldo de clases cuando se cumplen las demás condiciones y el socio está dentro del límite aplicable.

#### Scenario: Socio con membresía ilimitada reserva dentro del límite
- **WHEN** un socio con membresía ilimitada intenta reservar sin exceder el límite de reservas activas para esa fecha y cumple las demás condiciones de reserva
- **THEN** el sistema permite confirmar la reserva sin requerir saldo de clases

### Requirement: Registrar asistencia o no-show por reserva
El sistema SHALL permitir a Daniela registrar para cada reserva de una clase si el socio asistió o no se presentó (no-show).

#### Scenario: Daniela registra asistencia
- **WHEN** Daniela marca como asistencia la reserva de un socio
- **THEN** el sistema registra el resultado de esa reserva como asistencia

#### Scenario: Daniela registra un no-show
- **WHEN** Daniela marca como no-show la reserva de un socio
- **THEN** el sistema registra el resultado de esa reserva como no-show

### Requirement: Mostrar indicadores operativos básicos
El sistema SHALL presentar en el dashboard el porcentaje de ocupación, información sobre cancelaciones tardías y no-shows, e información sobre reservas múltiples.

#### Scenario: Administradora consulta los indicadores básicos
- **WHEN** Marcela o Daniela consulta el dashboard
- **THEN** el dashboard presenta el porcentaje de ocupación, información sobre cancelaciones tardías y no-shows, e información sobre reservas múltiples

### Requirement: Mostrar tendencias de las últimas cuatro semanas
El sistema SHALL mostrar la evolución de los indicadores del dashboard durante las últimas cuatro semanas.

#### Scenario: Administradora consulta tendencias
- **WHEN** Marcela o Daniela consulta la evolución de los indicadores
- **THEN** el dashboard presenta las tendencias correspondientes a las últimas cuatro semanas
