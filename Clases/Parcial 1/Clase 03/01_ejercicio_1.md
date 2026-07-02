# Plataforma de Eventos y Entradas (Eventos → Sesiones → Tickets)

1. El sistema gestiona **Eventos** (con nombre, descripción, lugar, fechas).
2. Un Evento puede tener **múltiples Sesiones** (fechas/horas distintas en mismo evento).
3. Cada Sesión tiene **Tipos de Ticket** (General, VIP, Early-bird) con precio y cantidad limitada por tipo.
4. **Asiento opcional**: algunas sesiones son numeradas (asientos), otras son libres (capacidad general).
5. Un **Cliente** compra uno o varios **Tickets** para una sesión — cada ticket es único y puede cambiar de estado (reservado, pagado, cancelado, usado).
6. Soportar **descuentos/promocodes** aplicables a sesiones específicas o tipo de ticket.
7. Registrar **Check-in** cuando el asistente usa el ticket; no se puede volver a usar.
8. Posibilidad de **reembolso parcial** con reglas (plazo para devolución, comisión).
9. **Reseñas** del evento por asistentes después de la sesión.
10. Necesidad de reportes: ocupación por sesión, ingresos por evento, tickets vendidos por tipo.

## Identificación de entidades

**Entidad EVENTO**

- id_evento (PK)
- nombre
- descripcion
- lugar
- fecha_inicio
- fecha_fin

**Entidad SESION**

- id_sesion (PK)
- id_evento (FK)
- fecha
- hora
- capacidad (opcional si no numerada)

**Entidad TIPO_TICKET**

- id_tipo_ticket (PK)
- id_sesion (FK)
- nombre_tipo (General, VIP, etc.)
- precio
- cantidad_max

**Entidad ASIENTO** (solo si numerada)

- id_asiento (PK)
- id_sesion (FK)
- fila
- numero
- estado (disponible, ocupado)

**Entidad CLIENTE**

- id_cliente (PK)
- nombre
- email
- telefono

**Entidad TICKET**

- id_ticket (PK)
- id_cliente (FK)
- id_sesion (FK)
- id_tipo_ticket (FK)
- id_asiento (FK, nullable si no numerada)
- estado (reservado, pagado, cancelado, usado)

**Entidad PAGO**

- id_pago (PK)
- id_ticket (FK)
- monto_pagado
- fecha_pago
- metodo_pago
- estado_pago (completado, reembolsado parcial, reembolsado total)

**Entidad REEMBOLSO**

- id_reembolso (PK)
- id_pago (FK)
- monto_devuelto
- fecha_reembolso
- motivo
- porcentaje_comision

**Entidad DESCUENTO**

- id_descuento (PK)
- codigo
- porcentaje
- valido_desde
- valido_hasta

**Entidad CHECKIN**

- id_checkin (PK)
- id_ticket (FK)
- fecha_checkin
- validado_por (usuario del staff)

**Entidad RESEÑA**

- id_resena (PK)
- id_cliente (FK)
- id_evento (FK)
- calificacion
- comentario
- fecha_resena

## Identificación de relaciones

### Relación Evento–Sesión

- **Evento → Sesión:** *"Evento tiene sesiones"* (1:N)
- **Sesión → Evento:** *"Sesión pertenece a un evento"* (N:1, pero cada sesión solo a 1 evento)

### Relación Sesión–TipoTicket

- **Sesión → TipoTicket:** *"Sesión ofrece tipos de ticket"* (1:N)
- **TipoTicket → Sesión:** *"Tipo de ticket corresponde a una sesión"* (N:1)

### Relación Sesión–Asiento

- **Sesión → Asiento:** *"Sesión contiene asientos"* (1:N, opcional si numerada)
- **Asiento → Sesión:** *"Asiento pertenece a una sesión"* (N:1)

### Relación Sesión–Ticket

- **Sesión → Ticket:** *"Sesión genera tickets"* (1:N)
- **Ticket → Sesión:** *"Ticket corresponde a una sesión"* (N:1)

### Relación Cliente–Ticket

- **Cliente → Ticket:** *"Cliente compra tickets"* (1:N)
- **Ticket → Cliente:** *"Ticket fue comprado por cliente"* (N:1)

### Relación Ticket–Pago

- **Ticket → Pago:** *"Ticket se paga mediante pago"* (1:1)
- **Pago → Ticket:** *"Pago pertenece a un ticket"* (1:1)

### Relación Pago–Reembolso

- **Pago → Reembolso:** *"Pago genera reembolsos"* (1:N, pueden existir reembolsos parciales múltiples)
- **Reembolso → Pago:** *"Reembolso corresponde a un pago"* (N:1)

### Relación Ticket–Descuento

- **Ticket → Descuento:** *"Ticket usa descuento"* (N:1, opcional)
- **Descuento → Ticket:** *"Descuento se aplica a tickets"* (1:N)

### Relación Ticket–Checkin

- **Ticket → Checkin:** *"Ticket genera check-in"* (1:1, opcional si el cliente no asistió)
- **Checkin → Ticket:** *"Check-in valida ticket"* (1:1)

### Relación Cliente–Reseña

- **Cliente → Reseña:** *"Cliente escribe reseña"* (1:N)
- **Reseña → Cliente:** *"Reseña fue escrita por cliente"* (N:1)

### Relación Evento–Reseña

- **Evento → Reseña:** *"Evento recibe reseñas"* (1:N)
- **Reseña → Evento:** *"Reseña corresponde a evento"* (N:1)

