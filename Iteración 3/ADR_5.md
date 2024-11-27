# ADR_5: Implementación de Load Balancing en el Microservicio de Clientes

## Contexto y declaración del problema
El microservicio de Clientes es un componente crítico en la arquitectura de la compañía, encargado de gestionar la información personal y sensible de los usuarios. Este servicio es accedido tanto desde aplicaciones móviles como desde clientes PC, lo que genera un tráfico constante y elevado.

La alta concurrencia en el acceso a este microservicio puede provocar problemas como:
- Sobrecarga de las instancias debido al alto número de solicitudes simultáneas.
- Latencia elevada en las respuestas hacia los clientes finales.
- Interrupciones del servicio si las instancias activas no pueden manejar la carga, afectando la experiencia del usuario.

Para mitigar estos riesgos, se requiere una solución que permita distribuir la carga de manera eficiente entre múltiples instancias del microservicio.

## Drivers de decisión
- [Escalabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#escalabilidad)
- [Disponibilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#disponibilidad)
- [Performance](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#performance)
- [Requerimiento funcional del microservicio Cliente](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Requerimientos%20Funcionales.md#clientes-cr%C3%ADtico)

## Opciones consideradas
1. **No implementar balanceo de carga**  
   **Ventaja:** Menor complejidad inicial.  
   **Desventaja:** Las solicitudes serían gestionadas por una única instancia o con un sistema básico de asignación manual, lo que resultaría en problemas de disponibilidad, rendimiento y escalabilidad.

2. **Implementar caching para reducir la carga**  
   **Ventaja:** Mejora los tiempos de respuesta en solicitudes que no requieren procesamiento en tiempo real.  
   **Desventaja:** No resuelve completamente el problema, ya que muchas operaciones en el servicio de Clientes son transaccionales y no cacheables.

3. **Implementar un balanceador de carga**  
   **Ventaja:** Permite distribuir equitativamente las solicitudes, mejorar la disponibilidad y escalar el sistema fácilmente.  
   **Desventaja:** Introduce costos adicionales y mayor complejidad en la configuración.

## Decisión
Se implementará un balanceador de carga para el microservicio de Clientes. Este componente distribuirá las solicitudes entrantes entre múltiples instancias activas del servicio, mejorando su rendimiento, disponibilidad y escalabilidad.  

El balanceador de carga será configurado para:
- Detectar y redirigir el tráfico solo hacia instancias saludables mediante health checks.
- Ajustar dinámicamente la distribución de la carga según la cantidad de solicitudes concurrentes.
- Facilitar la incorporación de nuevas instancias en momentos de alta demanda.

## Consecuencias

### Buenas
- Incremento de la disponibilidad del servicio, incluso en caso de fallos de instancias individuales.
- Mejora en los tiempos de respuesta gracias a la distribución eficiente de solicitudes.
- Escalabilidad horizontal para manejar incrementos en la carga, asegurando la continuidad del negocio.
- Preparación para futuras optimizaciones de balanceo, como algoritmos basados en proximidad o tipo de solicitudes.

### Malas
- Incremento en los costos operativos, ya que el balanceador puede requerir infraestructura adicional o servicios gestionados (por ejemplo, AWS ELB, Google Cloud Load Balancer).
- Mayor complejidad operativa, lo que implica la necesidad de monitorear y mantener el balanceador, así como ajustar las configuraciones según el tráfico.
