## Argumentos variables
```
private static void variosParametros(int... numeros){ %% Cuando se pasa multiples parametros estos se trabajan como si fueran un array %%
	for(int numero: numeros){
	System.out.println("numero: "+ numero);
	}
}

private static void variosParametros(String nombre, int... numeros){ 
	for(int numero: numeros){
	System.out.println("nombre: "+ nombre);
	System.out.println("numero: "+ numero);
	}
}
```
## Modificador de acceso
**_default:_** este modificador de acceso solo nos permite acceder a objetos dentro del mismo paquete. es mas restrictivo que protected pero no mas que private.

# Diferencia entre Error y Exception

![Jerarquia de Errores|750](https://programacion.abrilcode.com/lib/exe/fetch.php?w=600&tok=d53c65&media=bloque3:jerarquiaexcepciones.png)

## Error
Los Error representan situaciones que son irrecuperables, estos implican una interrupción del proceso y/o ejecución, dando como resultado la finalización del mismo sin posibilidades de reiterar el mismo o seguir con otro. Estos son eventos graves que indican un problema en el sistema o en la aplicación que no se puede solucionar en el tiempo de ejecución.

Normalmente están fuera del control del programador y son causados por factores externos, como falta de memoria, errores de hardware o incompatibilidades del sistema operativo. **Ejemplos:** `OutOfMemoryError`, `ThreadDeath`, `VirtualMachineError`
## Exception

Las Exception representan situaciones recuperables, esto implica que a pesar de que algo no funciono como debía es algo a lo que se le puede dar un manejo dentro del programa o su código fuente. Estas ocurren debido a condiciones especificas que surgen durante la ejecución del programa, como lo puede ser intentar acceder a un índice inválido en un array o abrir un archivo inexistente.

El programa puede incluir bloques `try-catch` para interceptar excepciones específicas y tomar acciones alternativas, como mostrar un mensaje de error al usuario o intentar corregir la situación. **Ejemplos:** `ArrayIndexOutOfBoundsException`, `FileNotFoundException`, `NullPointerException`.

### Excepciones comprobadas
No son culpa del programador
Ejemplo: 
- El programa busca una imagen en una carpeta pero esta no se encuentra ahí por algún motivo.

### Excepciones NO comprobadas
Son Errores culpa del programador 
Ejemplo: 
-  Recorrer un array con mas posiciones de las que se declaraón.
- Asignar a una variable un dato que no es del tipo de esa variable.



### Pila de Errores (StackTrace)
```
try{
	%% codigo %%
}catch(Exception e){
	e.printStrackTrice(System.out)
}
```

# Diferencia entre == y .equals

## == 
- Se emplea para comparar el objeto y su referencia en memoria.
- Se puede emplear para comparar objetos de tipo primitivo y objetos.
## .equals
- Se emplea para comparar el valor del objeto.
- Solo se emplea para comparar objetos
- Se puede sobre escribir el comportamiento de este método en una clase


# Memoria JVM 

[[[Tutorial JVM - La arquitectura de la máquina virtual de Java explicada para principiantes (freecodecamp.org)](https://www.freecodecamp.org/espanol/news/tutorial-jvm-la-arquitectura-de-la-maquina-virtual-de-java-explicada-para-principiantes/)|Articulo FreeCodeCamp - JVM]] --> Articulo de referencia 

![JVM-general|600](https://www.freecodecamp.org/espanol/news/content/images/2022/10/figura2.png)
## Arquitectura de la maquina virtual de Java

### 1. Cargador de clase (Class Loader)

![JVM-Cargador de clase](https://www.freecodecamp.org/espanol/news/content/images/2022/10/figura3-1.png)

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

![JVM-Área de datos](https://www.freecodecamp.org/espanol/news/content/images/2022/10/figura4-1.png)
#### 2.1. Área de métodos
Todos los datos de la clase se almacenan en esta área, tanto los campos como los métodos. Si con la memoria disponible no se puede satisfacer la petición de asignación la JVM generara `OutOfMemoryError` 

#### 2.2. Área del montículo (heap)
Acá se almacenan todos los objetos y sus variables de instancia. Este se ejecuta en tiempo de ejecución, aquí asigna los arreglos e instancia de clases. 

#### 2.3. Área del pilas (stack)
Almacena las variables locales, resultados parciales(resultados de los métodos) y llamadas a métodos (Construcción de objetos). Si se requiere un tamaño de pila mayor al permitido se generara un error `StackOverflowError`.

Para la llamadas de métodos se genera una entrada en la pila, llamada marco de pila (stack frame), al finalizar el llamado el stack frame se destruye

##### Stack Frame (Marco de pila)

- **Variables locales:** Arreglo que almacena variables locales (nombres) y sus valores. La longitud se define en el tiempo de compilación
- **Pila de operandos:** Estructura de tipo pila que realiza operaciones intermedias durante las llamadas de los métodos. La profundidad máxima se define en tiempo de compilación.
	
	Las operaciones intermedias en los Stack Frames de la JVM son **instrucciones que se ejecutan durante la interpretación del bytecode**. Estas operaciones pueden ser:
	
	- **Operaciones aritméticas:** suma, resta, multiplicación, división, etc. 
	- **Operaciones lógicas:** AND, OR, NOT, etc. 
	- **Comparaciones:** mayor que, menor que, igual que, etc. 
	- **Carga y almacenamiento de variables:** cargar una variable en la pila o almacenar un valor en una variable. 
	- **Llamadas a métodos:** invocar otro método. 
	- **Saltos condicionales:** ir a una instrucción específica si se cumple una condición.
	- **Lanzamiento de excepciones:** indicar que ha ocurrido un error.
	
	**Las operaciones intermedias se ejecutan en orden secuencial**, siguiendo el flujo de control del programa. La JVM utiliza una pila para mantener un registro de las operaciones que se han ejecutado y de las que aún están pendientes.
	
- **Marco de datos:** Almacena todos los símbolos del método invocado asi como la información del bloque catch, por si se produce una excepción.

#### 2.4. Registros de contador de programa (PC, program counter)
La JVM admite múltiples hilos simultáneamente. Cada hilo tiene su propio registro contador de programa (PC) para guardar la dirección de la instrucción de la JVM ejecutándose en ese momento. Una vez ejecutada dicha instrucción, el registro PC es actualizado con la dirección de la próxima instrucción.

#### 2.5. Pila de  métodos  nativos
La JVM puede hacer uso de pilas que soporten métodos _nativos_, métodos escritos en lenguajes diferentes a Java, como C o C++. Cada hilo posee su propia pila de métodos nativos.

### 3. Motor de ejecución (Execution Engine)

![JVM-Execution Engine](https://www.freecodecamp.org/espanol/news/content/images/2022/10/figura6.png)

Una vez que el bytecode se ha cargado en memoria y la información necesaria está disponible en el área de datos de tiempo de ejecución, el siguiente paso es ejecutar el programa. El motor de ejecución gestiona este proceso ejecutando el código de cada clase.

Sin embargo, antes de ejecutar el programa, hay que traducir el bytecode a instrucciones del lenguaje máquina, usando un intérprete o un compilador JIT.

#### 3.1. Intérprete
El intérprete lee y ejecuta las instrucciones del bytecode línea a línea. Debido a esta ejecución línea por línea, el intérprete es comparativamente más lento.

Otra desventaja es la reinterpretación de un método cada vez que es llamado.

#### 3.2. Compilador JIT
El motor de ejecución utiliza al interprete para ejecutar el bytecode, allí trabaja el compilador cuando encuentra código repetido. 

El compilador traduce el bytecode a código maquina nativo; que es usado en las reiteradas llamadas a métodos, mejorando el rendimiento.

- Generador de código intermedio
- Optimizador de código
- Generador de código objetivo: Traduce el código intermedio en código máquina nativo
- Perfilador (profiler): Encuentra los _HotSpots_ (código que es ejecutado repetidamente)

#### 3.3. Recolector de basura (Garbage Collector)
El recolector de basura detecta y elimina los objetos que no tengan referencia en el área heap. Es el proceso de recuperar automáticamente durante el tiempo de ejecución la memoria que esta siendo usada por objetos que no se utilizaran nuevamente. Para esto se realizan 2 procesos.

- **Marcado:** Identificación de objetos no referenciados
- **Barrido:** Destruir los objetos identificados. 

La JVM realiza automáticamente la recolección de basura a intervalos regulares, no siendo necesaria su gestión separadamente. Puede ser disparada invocando `System.gc()`, aunque la ejecución no está garantizada.

**Nota:** hay otro tipo de colector de basura llamado **Barrido de Marcas Concurrente** **_(Concurrent Mark Sweep (CMS) GC)_**. Sin embargo, fue declarado obsoleto en Java 9 y completamente eliminado en Java 14 en favor de G1GC.
##### 3.3.1. En serie
Usando un solo hilo, produce un evento de tipo "parar el mundo" en el que todos los hilos de aplicación son detenidos hasta que la operación se complete.
##### 3.3.2. En paralelo
Es la implementación por defecto en la JVM, conocido como recolector de rendimiento _(throughput collector)_. Uitiliza múltiples hilos, pero aún necesita parar los hilos de aplicación.
##### 3.3.3. Garbage First
para aplicaciones multihilo con gran cantidad disponible de heap (más de 4GB). Particiona el heap en un conjunto de regiones de igual tamaño, utilizando múltiples hilos para explorarlas. G1GC identifica las regiones con el máximo de basura y realiza la limpieza prioritaria de esas regiones.


-------------------------------------------------------------------------------

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

Las colecciones son estructuras similares a los arreglos pero la principal diferencia y característica es que son dinámicos y solo almacenan objetos (No pueden almacenar tipos de datos primitivos). En Java se emplean mediante la interfaz Collection la cual permite usar una serie de métodos con los cuales manipulamos los arreglos.

![Collections-Java-Diagram](https://dcodingames.com/wp-content/uploads/2023/05/JCF.png)

- Entre mas funciones pueda realizar un collection, este va a ser menos eficiente 
## 1. List
- Permite una colección de elementos repetidos y esta indexado con valores numéricos
- Permite acceso aleatorio
- Puede llegar a tener bajo rendimiento en operaciones concretas que podría  ser mejor usar otras interfaces.
## 2. Set
Permitir una colección de elementos no repetidos sin ordenar

## 3. Queue
- No permite acceso aleatorio 
## 4. Map
- Colección de elementos  repetibles 
- Indexado por clave única arbitraria 


