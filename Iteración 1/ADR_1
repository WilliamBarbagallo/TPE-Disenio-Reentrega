# ADR_1 Propuesta y Selección de Arquitecturas
Migración de Arquitectura Monolítica a Microservicios

## Contexto y declaración del problema
Una compañía de productos alimenticios desea migrar su sistema existente de arquitectura monolítica a una arquitectura basada en microservicios. El objetivo es hacer que el sistema sea menos rígido, más escalable y más fácil de evolucionar. Actualmente, el sistema cuenta con clientes PC y móviles que acceden a dos bases de datos SQL que gestionan información como datos de clientes, pagos y pedidos. La compañía necesita garantizar la escalabilidad, seguridad, disponibilidad y mantenimiento del nuevo sistema, utilizando protocolos HTTP/REST.
Decision drivers

[Escalabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#escalabilidad)

[Modificabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#modificabilidad)

[Mantenibilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#mantenibilidad)

## Opciones Consideradas
- Arquitectura de Microservicios: Permite escalar y mantener los servicios de forma independiente, lo que facilita actualizaciones sin interrumpir todo el sistema y maximiza la reutilización de componentes.
- API Gateway:Actúa como un único punto de entrada para los clientes, gestionando la autenticación, autorización y enrutamiento de solicitudes hacia los microservicios. Simplifica el acceso y reduce la carga en los servicios al manejar caché, límites de tasa y equilibrio de carga.
- Mantener el sistema monolítico original: se ahorran todos los costos de dinero, tiempo, desarrollo y se deja el sistema tal cual está. 

## Decisión
Se decide hacer la migración a arquitectura de microservicios porque permite el desacoplamiento y escalabilidad independiente de los distintos servicios. Va a trabajar en sinergía con API Gateway, el cual nos va permitir centralizar el acceso a los servicios. Con ambas cosas, se logra satisfacer los principales atributos de calidad requeridos: escalabilidad, modificabilidad, y mantenimiento. 
Consecuencias

### Bien, porque:
Escalabilidad: La arquitectura de microservicios permite escalar cada servicio de forma independiente según la demanda, optimizando el uso de recursos y garantizando un rendimiento eficiente incluso con altos volúmenes de tráfico.
Modificabilidad: Al estar los servicios desacoplados, es posible realizar cambios o actualizaciones en un servicio específico sin afectar al resto del sistema, lo que facilita la evolución del sistema.
Mantenibilidad: La separación de responsabilidades entre servicios hace que el código sea más fácil de entender, depurar y extender, reduciendo el tiempo y esfuerzo necesario para resolver errores o implementar nuevas funcionalidades.

### Malo, porque:
Complejidad: La transición a microservicios puede aumentar la integridad operativa, requiriendo más herramientas de monitoreo y gestión.
Costos iniciales: Implementar microservicios y un API Gateway puede requerir inversiones significativas en infraestructura y capacidad.
Sobrecarga inicial: La transición de un sistema monolítico a microservicios requiere un esfuerzo considerable, incluyendo el rediseño de bases de datos, la creación de APIs y la implementación de herramientas como un API Gateway.
Latencia: La comunicación entre microservicios a través de redes puede incrementar la latencia en comparación con la arquitectura monolítica.

