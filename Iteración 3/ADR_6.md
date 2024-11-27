# ADR_6: Optimización del Flujo de Procesamiento de Pedidos con Parallel Processing y Orquestación de Flujo

## Contexto y declaración del problema
El proceso de pedidos en la arquitectura actual de la compañía sigue una secuencia estricta de tres pasos: preprocesado del pedido, autorización y aceptación. Estos pasos deben completarse en orden para garantizar la consistencia de los datos y el éxito del flujo. Sin embargo, en un sistema de alta demanda, esperar a que cada paso se complete antes de pasar al siguiente introduce latencia, lo cual puede afectar negativamente a la performance y la experiencia del usuario.

El flujo secuencial actual genera tiempos de espera que podrían reducirse si algunos pasos pudieran ejecutarse en paralelo, siempre y cuando no se afecte la lógica del negocio. Además, el sistema necesita ser escalable para manejar picos de carga, y el proceso debe seguir siendo coherente y fiable, garantizando que no se omitan pasos críticos.

## Drivers de decisión
- **[Escalabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#escalabilidad)**
- **[Performance](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#performance)**
- El requerimiento funcional del **[microservicio Pedido](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Requerimientos%20Funcionales.md#pedidos-semi-cr%C3%ADtico)**

## Opciones consideradas
### 1. Mantener el flujo secuencial actual (sin cambios)
- **Ventaja:** Mantiene la simplicidad del diseño actual y la consistencia del flujo.
- **Desventaja:** Genera una latencia mayor y baja escalabilidad, lo que afecta la experiencia del usuario en momentos de alta demanda.

### 2. Implementar Parallel Processing y Orquestación de Flujo
- **Ventaja:** Agiliza el proceso de pedidos al paralelizar tareas que no dependen de otros pasos, lo que reduce la latencia y mejora la escalabilidad.
- **Desventaja:** Introduce mayor complejidad en la orquestación del flujo y podría requerir cambios en la infraestructura para soportar la ejecución paralela.

### 3. Implementar un sistema de cacheo o pre-cálculo
- **Ventaja:** Puede acelerar la validación de ciertos pasos (por ejemplo, disponibilidad de inventario) sin necesidad de realizar todo el procesamiento desde cero.
- **Desventaja:** No resuelve el problema de la secuencia de los pasos críticos, ya que el proceso de autorización y aceptación sigue siendo secuencial.

## Decision
Se ha decidido implementar **Parallel Processing y Orquestación de Flujo** para agilizar el procesamiento de los pedidos. Los pasos de preprocesado, autorización y aceptación se reorganizarán de manera que se puedan realizar en paralelo siempre que no interfieran entre sí.

Específicamente:
- **Preprocesado:** Se realizará la validación de inventario, datos del cliente y la preparación del pedido en paralelo con la autorización del pedido, siempre y cuando la autorización no dependa directamente de los resultados del preprocesado.
- **Autorización y Aceptación:** La autorización puede ejecutarse sin esperar que el preprocesado termine por completo, siempre que las condiciones de negocio lo permitan. Una vez que la autorización esté completada, se pasa al paso de aceptación.
- **Orquestación del flujo:** Utilizaremos un motor de orquestación de flujo (por ejemplo, Apache Camel, Spring Integration) para manejar la secuencia de ejecución de los pasos. Esto asegurará que, aunque los pasos se realicen en paralelo, el flujo de trabajo se mantenga coherente y no se salte ningún paso.

## Consecuencias

### Buenas
- **Reducción de la latencia:** Al procesar tareas en paralelo, el tiempo total de procesamiento de cada pedido se reduce significativamente.
- **Mejora de la escalabilidad:** El sistema podrá manejar un mayor volumen de solicitudes, especialmente durante picos de alta demanda, distribuyendo la carga entre múltiples instancias de los microservicios.
- **Mayor eficiencia operativa:** El flujo de trabajo será más rápido, lo que implica una mejor experiencia para el usuario y una optimización de recursos.
- **Flexibilidad:** El sistema se vuelve más flexible y preparado para futuros cambios, como la introducción de nuevos pasos o la modificación de las fases existentes sin afectar la lógica de negocio.

### Malas
- **Mayor complejidad de implementación:** Requiere una reestructuración del flujo de trabajo actual y la integración de herramientas de orquestación, lo que aumenta la complejidad operativa.
- **Riesgo de incoherencia temporal:** Si no se maneja correctamente la orquestación, podría haber casos en los que un paso (como la autorización) se realice sin que se haya completado completamente el preprocesado, aunque esto se gestionará cuidadosamente mediante control de dependencias.
- **Costos adicionales de infraestructura:** Para soportar la ejecución paralela y la orquestación, podría ser necesario ampliar la infraestructura o modificar la infraestructura existente, lo que aumentará los costos operativos.
