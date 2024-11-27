# ADR_7: Uso de Event Sourcing y CQRS para Consistencia y Comunicación en Microservicios

## Contexto del Problema
En nuestra arquitectura basada en microservicios, cada servicio posee su propia base de datos desacoplada, promoviendo escalabilidad y mantenibilidad. Sin embargo, esto genera desafíos para mantener la sincronización y consistencia de datos entre servicios, especialmente en escenarios críticos como:
- **Clientes, Pagos y Reparto y Rutas:** Requieren alta fiabilidad y precisión.
- **Pedidos y Estadísticas:** Manejan alta concurrencia y operaciones complejas.

Es necesario un enfoque que asegure consistencia eventual y optimice el rendimiento en operaciones distribuidas.

## Drivers de Decisión
- [Escalabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#escalabilidad)
- [Modificabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#modificabilidad)
- [Disponibilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#disponibilidad)
- [Interoperabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#interoperabilidad)

## Opciones Consideradas
1. **Sagas**  
   - **Ventajas:** Ofrecen orquestación distribuida para consistencia.  
   - **Desventajas:** Implementación compleja y no permite fácilmente el acceso a eventos históricos.

2. **Consistencia fuerte**  
   - **Ventajas:** Proporciona sincronización inmediata.  
   - **Desventajas:** Limita la escalabilidad y añade latencia.

3. **Event Sourcing + CQRS (Decisión):**  
   - **Event Sourcing:** Registra cada cambio como eventos, permitiendo reconstrucción de estados históricos.  
   - **CQRS:** Separa los modelos de lectura y escritura, optimizando consultas y sincronización.

## Decisión
Se adoptará una combinación de **Event Sourcing** y **CQRS** como los patrones principales para abordar los desafíos:  
- **Event Sourcing:** Actúa como la fuente de verdad mediante un registro de eventos centralizado.  
- **CQRS:** Divide operaciones de lectura y escritura, propagando eventos relevantes entre microservicios.

## Consecuencias

### Ventajas
- **Escalabilidad:** Las consultas y escrituras son optimizadas por separado.
- **Trazabilidad:** Historial completo de eventos para auditoría y análisis.
- **Desacoplamiento:** Los servicios operan de forma independiente, sincronizándose mediante eventos.
- **Consistencia eventual:** Actualización eficiente y oportuna de los datos distribuidos.

### Desventajas
- **Complejidad inicial:** La configuración del registro de eventos y el manejo de consumidores requiere diseño cuidadoso.
- **Latencia en la consistencia:** Los datos no siempre estarán sincronizados en tiempo real.
