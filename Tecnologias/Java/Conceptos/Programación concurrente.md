# Threads(Hilos) - Programación de hilos

La programación con hilos nos permite manejar y ejecutar varias acciones al mismo tiempo mediante el uso de estos hilos, con lo que por ejemplo podemos descargar con un hilo e realizar otra acción de asignación de datos con otro hilo, estas acciones se realizan simultáneamente.

1. Una clase que implemente la interfaz Runnable
2. Implementar el método run()
3. Instanciar la clase y almacenar la instancia en variable de tipo Runnable
4. Crear una instancia de la clase Thread pasando como parametro el objeto Runnable
5. Poner en ejecución el hilo con el método start() de la clase Thread

Clase Thread nos determina una ejecución de hilo, dentro esta clase tenemos múltiples métodos para manipular la ejecución de nuestro método. Ej "stativ void sleep()" pausa la ejecución de nuestro hilo y con "void interrupt()" nos arroja una excepción y detiene la ejecución del hilo, aquí debemos manipular la excepción.  

Para la sincronización de hilos podemos usar diferentes opciones. Si deseamos solo sincronizar para que se sincronicen basado en una sola condición podemos usar la palabras reservadas syncronized, await y notify. Sin embargo si deseamos validar diferentes condiciones debemos emplear la interfaces Condition

 ```java
 public class MiClase{
	
	private Lock bloqueo = new ReentrantLock();
	private Condition condicion;
	condicion = bloque.newConditio();
	condicion1 = bloque.newConditio();
	
	public synchronized void miMetodo(){
			
		bloqueo.lock();
		try{
			while(condicionNesaria){
				condicion.await();
			}
			condicion.signalAll();
		} finally {
			bloqueo.unlock
		}
	}
	
 }


public synchronized class MiClase2{
	
	private Lock bloqueo = new ReentrantLock();
	private Condition condicion;
	condicion = bloque.newConditio();
	condicion1 = bloque.newConditio();
	
	public synchronized void miMetodo(){
			
			while(condicionNesaria){
				await();
			}
			notify();
		}
	}
	
}

public class EjecucionHilo implements Runnable{
	
	@Override
	public void run(){
		while(true){
			banco.miMetodo();
		}
	}
	
}
```
