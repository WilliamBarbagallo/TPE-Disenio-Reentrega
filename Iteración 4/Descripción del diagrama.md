# Descripción del diagrama final
En la arquitectura se ha decidido aplicar el patrón CQRS (Command Query Responsibility Segregation) para cada microservicio, lo que implica separar las operaciones de escritura y lectura en dos bases de datos distintas. La base de datos de escritura maneja las operaciones de modificación de datos, mientras que la base de datos de lectura está optimizada para consultas rápidas y no se ve afectada por las operaciones de escritura.

Ambas bases de datos se sincronizan mediante el patrón Event Sourcing. Cuando un comando es procesado por el microservicio de pedidos, se genera un evento que se almacena en el Event Store. Este almacén de eventos actúa como un registro de todas las transiciones de estado del sistema.

Los eventos almacenados en el Event Store son luego procesados por un Event Handler, que se encarga de actualizar la base de datos de lectura con los datos derivados de esos eventos, manteniendo así los datos consistentes y optimizados para consultas.
