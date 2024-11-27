# ADR_2: Descomposición Funcional de Microservicios

## Contexto y declaración del problema
Para iniciar el proceso, primero se debe decidir con qué criterio se van a separar los microservicios y cómo será la comunicación entre ellos.

## Decision Drivers
Los criterios en los que se tienen que separar los microservicios se encuentran [acá](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Requerimientos%20Funcionales.md).

## Opciones consideradas
1. **Descomposición por Capacidad de Negocio**  
   **Pros:**
   - Alineación directa con dominios de negocio.
   - Límites claros entre servicios.
   - Cohesión funcional alta.  
   **Contras:**
   - Posible duplicación de datos.
   - Complejidad en transacciones cross-service.
   - Potencial acoplamiento funcional.

2. **Descomposición por Subdominios Técnicos**  
   **Pros:**
   - Optimización técnica por tipo de función.
   - Reutilización de componentes.
   - Especialización técnica clara.  
   **Contras:**
   - Menor alineación con el negocio.
   - Mayor acoplamiento.
   - Dificultad en la autonomía de equipos.

3. **Descomposición Híbrida por Criticidad**  
   **Pros:**
   - Mejor manejo de requisitos de calidad.
   - Balance entre aspectos técnicos y de negocio.
   - Flexibilidad en la granularidad.  
   **Contras:**
   - Complejidad en la gestión organizacional.
   - Necesidad de criterios claros.
   - Potencial inconsistencia en el diseño.

## Decisión
Basándose en los requisitos funcionales proporcionados, se ha decidido implementar una arquitectura de microservicios con una **Descomposición por Capacidad de Negocio**. Además, se tendrá en cuenta la criticidad de cada componente a lo largo del proyecto, enfocándose en garantizar la disponibilidad y el rendimiento de los componentes más críticos.

## Consecuencias

### Buenas
- Clara separación de responsabilidades.
- Escalabilidad independiente por dominio.
- Mejor manejo de fallos.
- Facilidad de evolución por dominio.

### Neutras
- Necesidad de comunicación entre servicios.
- Gestión de datos distribuidos.
- Complejidad en el testing.

### Malas
- Overhead en comunicación entre servicios.
- Desafíos en consistencia de datos.
- Mayor complejidad operacional.
