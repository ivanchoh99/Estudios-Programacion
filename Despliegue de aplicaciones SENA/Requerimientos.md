
# Generalidades  sobre requerimientos

- Permite identificar las características y funcionalidades que sebe tener el software
- Definir las restricciones
- Entender complejidad, tiempos, herramientas y tecnologías
- Es un proceso crítico y se debe realizar de manera exhaustiva, si no es así el proyecto puede no ser exitoso.

## Tipos de requerimientos

### Requerimientos No Funcionales

No esta relacionado a funcionalidades directas del sistema, estos requerimientos muchas veces están asociados a la calidad, como lo son la fiabilidad, los tiempos de respuesta, capacidades de almacenamiento o computo, entre otros.

Para la recolección de estos requerimientos se recomienda una tabla que contenga la siguiente información: 
- Nombre del requerimiento
- Identificador
- Descripción: Describir la solicitud realizada por el cliente
- Propósito: Finalidad del requerimiento
- Forma de verificación: Escriba como se puede realizar la verificación de que el requerimiento fue alcanzado con éxito, en lo posible utilizar medidas cuantitativas

![[Requerimientos no funcionales.png]]

#### Requerimientos del producto

tienen que ver con los requerimientos de eficiencia, usabilidad, fiabilidad y portabilidad. Un ejemplo de un requerimiento no funcional de producto podría ser que el producto sea desarrollado en HTML5 sin el applet de Java ni Ajax, esto con el ánimo de garantizar que sea compatible con la mayoría de los navegadores en el mercado actual.

#### Requerimientos organizacionales

Son los requerimientos que provienen de las características de la organización. Como por ejemplo: estándares en los procesos, requerimientos de implementación como lenguajes específicos de programación, metodologías de diseño, tiempos de entrega y/o documentación requerida por la organización.

#### Requerimientos externos

Son todos los otros requerimientos que no entran dentro de las otras 2 categorías, entre este tipo de requerimientos están los relacionados con interoperabilidad con otros sistemas _software_ o _hardware_ de la empresa o terceros, lo relacionado con políticas y normativas gubernamentales o leyes, y los de tipo ético que se relacionan directamente con el público objetivo

## Arquitectura de despliegue de aplicaciones y servicios

### Componentes de una arquitectura de software

Durante el proceso de construcción de software debe incluir una serie de elementos o componentes, los cuales definen una estructura o línea de trabajo. Estos componentes se definen teniendo en cuenta el tipo de proyecto que se va a desarrollar. 

- Clientes y servidores.
- Bases de datos.
- Sistemas Operativos.
- Lenguajes de Programación.
- Niveles en sistemas jerárquicos.

La arquitectura de desarrollo define los componentes de software, su función e interacción con otros componentes de software y hardware. Es importante que la arquitectura del software sea definida desde un comienzo para no tener inconvenientes a la hora del funcionamiento y despliegue en entornos productivos.

### Maquinas Virtuales

Son sistemas operativos completos funcionando de manera aislada dentro de otros sistemas operativos anfitrión. En otras palabras podemos estar hablando de un equipo donde se realizo la creación de la maquina virtual para su puesta en producción; esto puede referirse a un proveedor que suministra el hardware necesario para soportarla, como Azure, AWS Google Cloud, Digital Ocean, etc.
![[Maquina Virtual funcionamiento.png]]

