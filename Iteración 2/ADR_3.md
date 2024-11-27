# ADR_3: Protocolo de Comunicación entre Microservicios

## Contexto y declaración del problema
La aplicación en desarrollo requiere una arquitectura modular y escalable que permita el desarrollo, despliegue y escalado independiente de sus diferentes funcionalidades. Para lograr esto, se tomó la decisión de implementar un diseño basado en microservicios, donde cada capacidad de negocio distintiva se encapsula en un servicio separado.

## Drivers de decisión
- [Escalabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#escalabilidad)
- [Disponibilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#disponibilidad)
- [Mantenibilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#mantenibilidad)
- [Performance](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#performance)
- [Interoperabilidad](https://github.com/WilliamBarbagallo/TPE-Disenio-Reentrega-Grupo12/blob/main/Atributos%20de%20Calidad.md#interoperabilidad)

## Decisión
Se ha decidido adoptar **REST sobre HTTP** como el protocolo de comunicación entre los microservicios. Esta elección se basa en la amplia adopción y madurez de este enfoque, así como en su capacidad para satisfacer los principales atributos de calidad requeridos.  

REST sobre HTTP permite una comunicación con un acoplamiento débil entre los servicios, lo que favorece la modularidad y escalabilidad del sistema. Además, el ecosistema de herramientas y mejores prácticas establecidas para HTTP facilita el desarrollo, el monitoreo y la resolución de problemas, mejorando la mantenibilidad general.  

Si bien existen algunas consideraciones en torno a la seguridad y la modificabilidad a largo plazo, se considera que los beneficios en escalabilidad, interoperabilidad, desempeño y disponibilidad superan estos desafíos, y que pueden ser abordados mediante una implementación y gestión adecuadas.

## Consecuencias

### Bien, porque:
- **Escalabilidad**: REST sobre HTTP permite una comunicación escalable y eficiente, aprovechando la naturaleza sin estado y almacenable en caché de HTTP.
- **Interoperabilidad**: El uso de REST favorece la interoperabilidad entre microservicios, ya que es un estándar ampliamente adoptado.
- **Mantenibilidad**: HTTP proporciona herramientas y prácticas establecidas para monitorear, registrar y solucionar problemas en la comunicación, mejorando la mantenibilidad.
- **Performance**: El protocolo HTTP ofrece un desempeño adecuado para la comunicación entre microservicios.
- **Disponibilidad**: REST sobre HTTP ayuda a evitar puntos únicos de falla, mejorando la disponibilidad del sistema.

### Malo, porque:
- **Seguridad**: Aunque HTTP puede ser seguro, se requiere una configuración y gestión adecuadas para garantizar la seguridad de las comunicaciones.
- **Modificabilidad**: Cambiar el protocolo de comunicación en el futuro podría requerir una mayor cantidad de trabajo que con otras opciones más acopladas.
