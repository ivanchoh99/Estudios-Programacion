
# ¿ Qué es Docker ?

Es una plataforma de contenedores, una herramienta para crear y administrar contenedores. Es importante aclarar que un contenedor no es una maquina virtual, ya que los contenedores manejar capas con lo justo y necesario de un sistema operativo, optimizando y obteniendo el mejor rendimiento posible; construyéndose mediante imágenes y estas se pueden compartir para que nuestro equipo lo replique.

## Contenedor 
- Es una caja de herramientas aislada con una porción de un sistema operativo para ejecutar aplicaciones en nuestra maquina host
- Es un empaquetado del código y dependencias para ejecutar que ese código, la aplicación. (aplicación + JDK)
- Un mismo contenedor que se ejecuta siempre debe reproducir exactamente el mismo comportamiento de la aplicación, sin importar dónde o quién lo ejecute.
- Un contenedor se encuentra aislado a el resto del sistema, permitiendo tener múltiples contenedores muy diferentes por sistema operativo, lenguaje. Sin embargo estos contenedores pueden estar comunicados entre si. 

# ¿ Por qué contenedores ?

- Diferentes ambientes de desarrollo y producción (Poder ejecutar nuestra aplicación en un entorno de producción futuro).
- Diferentes ambientes y versiones en un mismo equipo de trabajo .
- Evitar conflicto con las versiones de múltiples proyectos. 

# Arquitectura de Docker

1. Sistema Operativo Host.
2. Soporte de Contenedores S.O / Virtualización (Kernel).
3. Docker Engine.
4. CONTENEDOR 

