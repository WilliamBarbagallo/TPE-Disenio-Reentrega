# ADR_4:Bases de Datos Independientes por Microservicio
## Contexto y Planteamiento del Problema

En nuestra arquitectura de microservicios para el sistema de gestión de productos alimenticios, necesitamos definir una estrategia para el almacenamiento de datos. Actualmente, el sistema monolítico utiliza dos bases de datos SQL compartidas para toda la aplicación. Surge la cuestión de si debemos mantener este modelo de bases de datos compartidas o adoptar un enfoque de base de datos independiente por microservicio.

## Drivers de Decisión
[Modificabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#modificabilidad)

[Escalabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#escalabilidad)

[Disponibilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#disponibilidad)

[Performance](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#performance)

Siguiendo también los [requerimientos funcionales](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Requerimientos%20Funcionales.md)
en los cuales tenemos servicios criticos y otros no tanto, debemos asegurar que cada uno pueda acceder a sus registros.  

## Opciones Consideradas
- Mantener bases de datos compartidas (actual arquitectura monolítica)
- Implementar base de datos única centralizada con esquemas separados
- Implementar base de datos independiente por microservicio

## Decisión
La decisión de adoptar bases de datos independientes para cada microservicio responde a la necesidad de construir una arquitectura más flexible y adaptable. Al desacoplar el almacenamiento de datos, permitimos que cada servicio evolucione de manera autónoma, seleccionando el modelo de persistencia más adecuado a su naturaleza y requisitos específicos. Este enfoque no solo mejora la escalabilidad y el rendimiento, sino que también facilita la gestión individual de cada componente, reduciendo el riesgo de impactos transversales en el sistema.

## Consecuencias

### Positivas:
- Cada microservicio tiene total autonomía de datos
- Posibilidad de usar diferentes tipos de bases de datos según necesidad.
- Mejor aislamiento de fallos
- Escalabilidad independiente de cada servicio
  
### Negativas:
- Mayor complejidad operativa
- Necesidad de gestionar la consistencia de datos entre servicios
- Potencial overhead en la gestión de múltiples bases de datos
- Mayor consumo de recursos
