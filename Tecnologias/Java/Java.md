Lenguaje de propósito general, orientado a objetos, este es conocido por su filosofía de "escribir una vez , ejecutarse en cualquier lugar" lo que significa que el código puede ejecutarse en cualquier sistema que tenga una maquina virtual de Java sin necesidad de modificación.

-  [[JVM]]
- [[Diferencia entre Error y Exception]]
- [[Sockets]]
- [[Programación generica]]
- [[Métodos Default]]
- [[Programación concurrente]]
- [[Stream]]
- [[Collections]]
# Sintaxis 

## STATIC

la palabra static se usa para acceder a la clase, método o campo sin necesidad de instanciar un objeto de la clase. Además de esto cuando un campo es estático quiere decir que este campo se comparte de manera comunitaria para todas las instancias de la clase, de tal forma que si tenemos campo incremental y lo aumentamos cada vez que se crea un objeto este va a tener el mismo numero de instancias creadas del objeto. Ej:

```java
public class Persona{
	private String nombre;
	private static int personasInstanciadas = 0;

	public Persona(String nombre){
		this.nombre = nombre;
		personasInstanciadas++;
	}
}

public class Principal{

	public static void main(String[] args){
		Persona p1 = new Persona("ivan");
		Persona p2 = new Persona("maria");
		
		System.out.println("Personas instanciadas: " + Persona.personasInstanciadas);
	}
}

```

Desde un contexto statico no podemos acceder a un contexto dinámico pero si de manera viceversa.

## Argumentos variables
```java
private static void variosParametros(int... numeros){ 
%% Cuando se pasa multiples parametros estos se trabajan como si fueran un array %%
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

## Diferencia entre == y .equals
### == 
- Se emplea para comparar el objeto y su referencia en memoria.
- Se puede emplear para comparar objetos de tipo primitivo y objetos.
### .equals
- Se emplea para comparar el valor del objeto.
- Solo se emplea para comparar objetos
- Se puede sobre escribir el comportamiento de este método en una clase

