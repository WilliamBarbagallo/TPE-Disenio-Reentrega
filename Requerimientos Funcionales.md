### Clientes (Crítico):
   - Permitir el acceso y la gestión de los datos personales de los clientes.
   - El sistema debe garantizar la protección y seguridad de los datos de los clientes.
   
### Pedidos (Semi-crítico):
   - Permitir a los clientes realizar pedidos de productos a la empresa.
   - Limitar los intentos de realización de pedidos a un máximo de 3.
   - Gestionar el flujo de procesamiento de pedidos en tres fases: preprocesado, autorización y aceptación. Cada fase debe completarse correctamente antes de pasar a la siguiente.
   - Escalar el sistema para manejar un alto número de pedidos por hora.

**Reparto y rutas (Crítico)**:
   - Gestionar las rutas de los camiones y la asignación de los repartos a los clientes.
   - Desacoplar la funcionalidad de gestión de reparto.
   - Implementar dos algoritmos de optimización para seleccionar rutas, dependiendo de la demora de los camiones.

**Estadísticas (No crítico)**:
   - Proporcionar información en tiempo real sobre el estado de los pedidos.
   - Mostrar la situación actual de los camiones en sus rutas.
   - Ofrecer estadísticas sobre los clientes.

**Incidencias (Semi-crítico)**:
   - Reportar automáticamente incidencias en las rutas de reparto (por ejemplo, averías de camiones o entregas fallidas).
   - Notificar a los gestores de rutas sobre estas incidencias para tomar decisiones rápidas.

**Pagos (Crítico)**:
   - Integrar un sistema de pagos externo a través de la pasarela de pago de MercadoLibre.
   - Garantizar la seguridad de los pagos y la compatibilidad con diferentes sistemas de pago.

**Gestión de Incidencias y Pedidos**:
   - El sistema debe ser capaz de gestionar y registrar las incidencias relacionadas con los pedidos.
   - Ofrecer un sistema centralizado para gestionar todas las solicitudes de los pedidos de los clientes.

**Protocolo HTTP/REST**:
   - Sustituir el acceso a la base de datos monolítica actual por un sistema de microservicios que utilice HTTP/REST para acceder a las bases de datos (Clientes y Pedidos) desde las aplicaciones cliente (PC y móvil).

