Los métodos default se emplean para darle un implementación concreta a un método que esta en una interfaz.

```java
public interface Identificable(){
	
	public default void mostrarIdentificacion(){
		System.out.println(hashcode());
	}
}
```

de esta manera podemos implementar la interfaz sin que requiera la sobre-escritura

```java
public class Persona implements Identificable {// Esto no arroja ningun error de implementacion
	
}

public class Principal {
	public static void main(String[] args){
		p.mostrarIdentificacion();// arroja el hashcode de objeto por referencia en memoria
	}
}
```

```java

public interface Empleado{
	public default void mostrarTarea(){
		System.out.println("Empleado realizando tarea...");
	}
}

public interface Estudiante{
	public default void mostrarTarea(){
		System.out.println("Estudiante realizando tarea...");
	}
}

public class Persona implements Empleado, Estudiante{
	//Esta sobre escritura se realiza para liberar el conflicto de los 2 metodos default y definirle cual debe utilizar
	
	@Override
	public void realizarTarea(){
		Estudiante.super.realizarTarea();
	}
}
```
