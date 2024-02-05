
# Diferencia entre Error y Exception

## Error

## Exception


# Diferencia entre == y .equals

## == 
- Se emplea para comparar el objeto y su referencia en memoria.
- Se puede emplear para comparar objetos de tipo primitivo y objetos.
## .equals
- Se emplea para comparar el valor del objeto.
- Solo se emplea para comparar objetos
- Se puede sobre escribir el comportamiento de este método en una clase


# Memoria JVM 

[[[Tutorial JVM - La arquitectura de la máquina virtual de Java explicada para principiantes (freecodecamp.org)](https://www.freecodecamp.org/espanol/news/tutorial-jvm-la-arquitectura-de-la-maquina-virtual-de-java-explicada-para-principiantes/)|Articulo FreeCodeCamp - JVM]]

![JVM-general|600](https://www.freecodecamp.org/espanol/news/content/images/2022/10/figura2.png)
## Arquitectura de la maquina virtual de Java

### 1. Cargador de clase (Class Loader)

![JVM-Cargador de clase|600](https://www.freecodecamp.org/espanol/news/content/images/2022/10/figura3-1.png)

Cuando se compila el código en java esto se almacena en un fichero .java, donde se obtiene bytecode almacenado en un fichero .class.  Si en un programa se va a hacer uso de esta clase, será cargado en memoria principal por el cargador de clases.

La primera clase en ser cargada en memoria es, normalmente, aquella que contiene el método `main()` .

#### 1.1. Carga (loading)
Encontrar la representacion binara (bytecode) y crear una clase o interfaz apartir de la misma.

Si un cargador de clases es incapaz de encontrar una clase, delega el trabajo en el cargador de una subclase suya. Si el último cargador de la jerarquía tampoco es capaz de encontrar la clase en cuestión, se producirá `NoClassDefFoundError` o `ClassNotFoundException`.
##### 1.1.1. Cargador de clases de arranque (Boostrap Class Loader)
Carga los paquetes estándares de Java, localizados en fichero `rt.jar` y bibliotecas fundamentales. `java.lang`,`java.net`,`java.util`,`java.io`,....
##### 1.1.2. Cargador de clases de extensiones (Extension Class Loader)
Carga las extensiones de las bibliotecas estándar de Java presentes en el directorio `$JAVA_HOME/jre/lib/ext` .
##### 1.1.3. Cargador de clases de aplicaciones (Application Class Loader)
Carga los ficheros indicados en el _classpath_ (variable de entorno que almacena la ruta a las clases creadas por el usuario). Por defecto, la variable classpath es establecida al directorio actual de la aplicación; puede ser modificada desde la línea de comandos con la opción `-classpath` o `-cp`


#### 1.2. Enlazado (linking) 

Después de que una clase haya sido cargada en memoria, se somete al proceso de enlazado. Enlazar una clase o una interfaz supone resolver las referencias externas y dependencias, integrando la clase en el conjunto del programa que hace uso de ella.

##### 1.2.1. Verificación
Verificación estructural del archivo .class. Si esta falla arrojara un `VerifyException`.

##### 1.2.2. Preparación
Asigna los espacios de memoria para los campos estáticos de clases o interfaces, inicializándolos con valores por defecto.

##### 1.2.3. Resolución
Se resuelve dinámicamente las constantes y referencias simbólicas utilizadas en las clases; esto es el proceso de remplazar las referencias por los valores reales durante la carga de la clase.

#### 1.3. Inicialización (initialization)

Se asignan los valores a las variables estáticas. Se cambian los valores por defecto que se habían asignado por los valores reales. 

### 2. Área de datos/ memoria en tiempo de ejecución (Runtime memory/ Data Area)




3. Motor de ejecución (Execution Engine)


[[[The Node.js Master Class - No Frameworks, No NPM (youtube.com)](https://www.youtube.com/watch?v=zSRO_b4y2cA)|Como funciona la memoria en Java]] -> **Video Youtube**

Se basa en 2 regiones de memoria llamada stack y heap, esto hace que se segmente la memoria 
## Stack

- Almacenamos los nombres de las variables y sus valores siempre y cuando sean tipos de datos primitivos, sino se almacena la referencia en memoria donde se almaceno el dato o el objeto.

```
int a = 500;
int b = 500;

if(a==b) --> true
```

| Nombre Valor | referencia memoria/ valor |
| ---- | ---- |
| a | 500 |
| b | 500 |
## Heap

- Almacena los objetos creados e instanciados en tiempo de ejecución asignándoles un espacio de memoria dinámica 

```
Integer c = 500;
Integer d = 500;

if(c==d) --> false
if(c.equals(d)) --> true
```

## Integer Cache

Cuando creamos un objeto Integer con valor entre -127 hasta 128, este se almacena en la memoria stack con una referencia de memoria hacia la memoria cache, con el fin de optimizar el uso de memoria, de la siguiente manera.

```
Integer e = 100;
Integer f = 100;

if(e==f) --> true 

%% Pero si quiero que sean diferentes debo realizar %%

Integer g = new Integer(100);
Integer h = new Integer(100);

if(e==f) --> false 

```

## String Pool

Cuando creamos un String de la forma: 

```
String texto = "hola mundo";
String texto2 = "hola mundo";
```

Estamos creando un objeto de tipo String que se  esta almacenando en la String pool, al contener los 2 string el mismo contenido solo se crea una instancia del objeto y se relaciona mediante la referencia de memoria, pero si se modifica alguno de los dos:

```
String texto = "hola mundo";
String texto2 = "hola mundo";

texto2 += "mundial";
```

se va a crear otro nuevo objeto diferente al que estaban compartiendo la referencia de memoria
para almacenar "hola mundo mundial".

Sin embargo similar que con los Integer si realizamos la creación del objeto string de la siguiente manera:

```
String 2texto = new String ("hola mundo");
String 2texto2 = new String("hola mundo");
```

Se crearan 2 objetos diferentes en la memoria Heap y no en la String pool a pesar que tengan el mismo contenido.

| Nombre Valor | referencia memoria/ valor |
| ---- | ---- |
| a | 500 |
| b | 500 |
| c | 0x8a7b |
| d | 0x8574 |
| e | 0x555 |
| f | 0x555 |
| g | 0x6ac5 |
| h | 0x7a7b |
| texto | 0x6728 |
| texto2 | 0x6728 |
| 2texto | 0x76b4 |
| 2texto2 | 0x54c4 |
# Collections

