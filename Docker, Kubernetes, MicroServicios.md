
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

# Persistencia de los datos en docker 

se usan volúmenes y cuando arrancamos nuestro contenedor este volumen se especifica con la bandera -v

# Contenedor utilitario

se conecta a nuestro conector de base de datos y nos  permite manipular la consola de nuestro contenedor de base de datos mediante la terminal.

- Habilitar la linea de comandos -> -it
- Se elimina el contenedor cuando se detenga -> --rm
- Se establece la red en de la cual va a hacer parte el contendor -> --network
- Se establece la imagen para el contenedor --> mysql:8
- Linea de comandos -> bash o bin/bash

``` docker
docker run -it --rm --network spring mysql:8 bash
```

# Arguments y Environment

## ARG 
- Se utiliza únicamente dentro del Dockerfile. 
- Configuración dinámica en la construcción de la imagen con la bandera --build-arg
## ENV
- Se configura dentro del Dockerfile y también en nuestro código (comandos). 
- Se puede configurar en el Dockerfile ENV y vía comandos con la bandera -e o --env

```Docker
docker run -p 8001:8090 --env PORT=8090 -d --name conenedorName --network networkName imagenBase
```

