
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
Son Errores culpa del programador, que se podrían solventar y manejar de una mejor manera.
Ejemplo: 
-  Recorrer un array con mas posiciones de las que se declararon.
- Asignar a una variable un dato que no es del tipo de esa variable.

### Pila de Errores (StackTrace)
```Java
try{
	%% codigo %%
}catch(Exception e){
	e.printStrackTrice(System.out)
}
```

### throws y throw

- **throws:** Se utiliza para declarar las excepciones que se pueden producir en un método determinado 
```java
public void miMetodo() throws IOException{
//codigo alguno 
}
```
- **throw:** Se utiliza para lanzar la excepción y se pone dentro del bloque de código donde se desea arrojar esta excepción.
```java
	if(condicion) throw new CustomeException
```

### Creación de exception

```java
class CustomeException extends Exception{
	public CustomeException(){} 
	public CustomeException(String msj){
		super(msj);
	} 
}
```
