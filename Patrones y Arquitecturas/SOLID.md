# S - Single Responsibility Principle

**_“A class should have one, and only one, reason to change.”_**
Una clase solo debe tener una función y responsabilidad; solo por este motivo y/o responsabilidad esta clase puede cambiar. Si por ejemplo tenemos una clase contenedora de datos, esta solo se debe encargar de contener esos datos y no realizar acciones que no correspondan a contener los datos, si se desea realizar otra acción que implique lógica esta debe dársele la responsabilidad a otra clase diferente. 

```java 
// Clase que se encarga solo de gestionar los pedidos
public class PedidoService {
    public void agregarPedido(Pedido pedido) {
        // Lógica para agregar un pedido
    }

    public void cancelarPedido(Pedido pedido) {
        // Lógica para cancelar un pedido
    }
}

// Clase que se encarga solo de gestionar la notificación
public class NotificationService {
    public void enviarNotificacion(String mensaje) {
        // Lógica para enviar una notificación
    }
}

```

# O - Open/Close Principle

**_“You should be able to extend a classes behavior, without modifying it.”_**
Este principio busca que una clase este abierta para extender y cerradas a las modificaciones. Esto en otras palabras quiere decir que la clase se le deben poder agregar funcionalidades mediante la extensión de esta y no mediante la modificación de la clase principal.

```java
// Clase base para un pedido
public abstract class Pedido {
    public abstract double calcularTotal();
}

// Extensión de la clase Pedido para un tipo específico de pedido
public class PedidoConDescuento extends Pedido {
    private double descuento;

    public PedidoConDescuento(double descuento) {
        this.descuento = descuento;
    }

    @Override
    public double calcularTotal() {
        // Lógica para calcular el total con descuento
    }
}

```
# L - Liskov's Subsistution Principle

**_“Derived classes must be substitutable for their base classes.”_**
Este principio quiere decir que deberíamos poder sustituir una subclase por su clase padre o base sin que esto genere o implique un problema o modificación a nuestro código. Suponiendo que tenemos una clase A y una clase B siempre que se espere un objeto de la clase B se debería poder pasar un objeto de la clase A y que esto no altere su funcionamiento. Por general es fácil de entender pero difícil de visualizar en código. 

```java
public class Rectangulo {
    protected int ancho;
    protected int alto;

    public void setAncho(int ancho) {
        this.ancho = ancho;
    }

    public void setAlto(int alto) {
        this.alto = alto;
    }

    public int getArea() {
        return ancho * alto;
    }
}

public class Cuadrado extends Rectangulo {
    @Override
    public void setAncho(int ancho) {
        this.ancho = ancho;
        this.alto = ancho;
    }

    @Override
    public void setAlto(int alto) {
        this.ancho = alto;
        this.alto = alto;
    }
}

// Uso
Rectangulo rectangulo = new Cuadrado();
rectangulo.setAncho(5);
rectangulo.setAlto(5);
System.out.println(rectangulo.getArea()); // Funciona correctamente

```

# I - Interface Segregation Principle 

**_“Make fine grained interfaces that are client specific.”_**
Este principio nos dice que deberíamos crear interfaces especificas para un tipo de cliente, con una finalidad concreta. Aquí debemos evitar interfaces de propósito general

```java
public interface ImprimirDocumento {
    void imprimirPDF();
    void imprimirWord();
}

public class ImpresoraPDF implements ImprimirDocumento {
    @Override
    public void imprimirPDF() {
        // Lógica para imprimir PDF
    }

    @Override
    public void imprimirWord() {
        // No utilizado
    }
}

// Mejor segregado
public interface ImprimirPDF {
    void imprimirPDF();
}

public interface ImprimirWord {
    void imprimirWord();
}

public class ImpresoraPDFSegregada implements ImprimirPDF {
    @Override
    public void imprimirPDF() {
        // Lógica para imprimir PDF
    }
}
```

# D - Dependency Inversion Principle

**_“Depend on abstractions, not on concretions.”_**
Aquí se nos dice que debemos depender de abstracciones y no de implementaciones concretas, en otras palabras cuando queremos referirnos a un objeto deberíamos referirnos a la interfaz concreta que quisiéramos utilizar y no a la implementación concreta del objeto.

```java
// Interface de una clase de almacenamiento de datos
public interface DataRepository {
    void guardar(Pedido pedido);
}

// Clase que implementa la interfaz de almacenamiento
public class PedidoDatabaseRepository implements DataRepository {
    @Override
    public void guardar(Pedido pedido) {
        // Lógica para guardar el pedido en la base de datos
    }
}

// Clase de servicio que depende de la abstracción en lugar de una implementación concreta
public class PedidoService {
    private DataRepository repository;

    public PedidoService(DataRepository repository) {
        this.repository = repository;
    }

    public void procesarPedido(Pedido pedido) {
        // Lógica para procesar el pedido
        repository.guardar(pedido);
    }
}

// Uso
DataRepository repository = new PedidoDatabaseRepository();
PedidoService service = new PedidoService(repository);
service.procesarPedido(new Pedido());
```