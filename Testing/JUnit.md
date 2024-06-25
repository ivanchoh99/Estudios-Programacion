# JUnit [Curso Testing con JUnit OpenBootcamp](https://www.youtube.com/playlist?list=PLkVpKYNT_U9fG0qEEXIvT9nJrMPZK6ORn)

## Pruebas Unitarias
Las pruebas unitarias consisten en evaluar el correcto funcionamiento y comportamiento de los métodos, clases y objetos en la ejecución de nuestro código.
## Pruebas de Integración 
Las pruebas de integración consisten en evaluar el correcto funcionamiento y comportamiento de la cohesión entre las diferentes partes de nuestro código, por ejemplo que entre la relación que hay entre nuestro controller, servicio y repositorio sea coherente. 

## TestCase
Son casos de prueba. Si yo hago algo y se cumple, es correcto, sino lo cumple es incorrecto

## Coverage
Es la cantidad de clases, métodos y lineas de código que se han ejecutado. Con esto verificamos que hemos probado todo nuestros programas y códigos en un 100%.

## **TDD** -> **T**est **D**riven **D**evelopment
Escribimos primero las pruebas pensando en que es lo que va a ocurrir y posteriormente escribimos el código, definiendo en como va a ocurrir eso.


```java 
public MiClaseTest{

	@BeforeAll
	static void init(){
		// Este codigo se va a ejecutar antes de todos los test
	}
	@AfterAll
	static void end(){
		// Este codigo se va a ejecutar despues de todos los test
	}
	@BeforeEach
	void before(){
		// Este codigo se va a ejecutar antes de cada test
	}
	@AfterEach
	void after(){
		// Este codigo se va a ejecutar despues de cada test
	}
	
	@Test
	void miPrimerTest(){
		
		MiClase mc = new MiClase;
		int resultado = mc.sumar(2, 2);
		
		assertEquals(4, resultado); //El assert es el que comprueba que lo que estoy obteniendo sea igual a lo que se espera como resultado
	}
}
```