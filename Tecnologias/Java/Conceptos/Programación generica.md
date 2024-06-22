consiste en escribir código que pueda utilizar para diferentes tipos de objetos. Utilizando parámetros de tipo. Permite comprobaciones de errores en tiempo de compilación.

## Clase genérica

```java

public class ClaseGenerica<T> {
	private T primero;
	
	public ClaseGenerica(){
		primero = null
	}
	
	public void setPrimero(T nuevoValor){
		primero = nuevoValor
	}
	
	public T getprimero(){
		return primero
	}
}

public static void main(String[] args){
	
	ClaseGenerica<String> una = new ClaseGenerica<String>();
	una.setPrimero("nuevo valor");
	
	ObjetoCualquiera obj = new ObjetoCualquiera();
	ClaseGenerica<ObjetoCualquiera> otra = new ClaseGenerica<ObjetoCualquiera>();
	otra.setPrimero(obj);
}
```

## Métodos Genéricos

```java

public Matris{
	public static <T> String getElementos(T[] arg){
		return "El array tiene " + arg.length + " elementos";
	}
	
	public static <T extends Comparable> T getMenor(T[] arg){
		if(a == null || a.length == 0) return null;
		
		T elemntoMenor = arg[0];
		
		for(int x = 1; x < arg.length(); i++){
			if(elementoMenor.compareTo(arg[x] > 0)){
				elementoMenor=a[x];
			}
		}
		
		return elementoMenor
	}
}


String nombre[] = {"ivan", "maria", "laura"}

System.out.println(Matris.getElementos(nombres)) // retorna el numero de elementos que tiene el arrreglo 
System.out.println(Matris.getMenor(nombres))// retorna el nombre con un valos lexicográficamente menor del arreglo
```

## Herencia y tipo comodín

Para implementar la programación genérica en conjunto con la herencia no es posible sin utilizar los tipo comodín, ya que si tratamos de asignar tipos padres e hijos con programación genérica se van a arrojar errores. 

```java

public ClaseGenerica{

	public static void imprimirPrimero(ClaseGenerica<? extends Empleado> p){//Utilizable para las clases empleados y sus hijos(herencias)
		Empleado primero = p.getPrimero();
		System.out.println(primero);
	}
}

Empleado administrativa = new Empleado("juan")
Jefe directoraComercial = new Jefe("maria")

Empleado nuevoEmpleado = directoraComercial;
________________________________________________________________________________________

ClaseGenerica<Empleado> administrativa = new ClaseGenerica<Empleado>;
ClaseGenerica<Jefe> directoraComercial = new ClaseGenerica<Jefe>("maria")

ClaseGenerica<Empleado> nuevoEmpleado = directoraComercial; // Esto arroja un error ya que no puede convertir un objeto de tipo a jefe a un objeto de tipo Empleado

ClaseGenerica.imprimirPrimero(directorComercial);
ClaseGenerica.imprimirPrimero(administrativa);
```
