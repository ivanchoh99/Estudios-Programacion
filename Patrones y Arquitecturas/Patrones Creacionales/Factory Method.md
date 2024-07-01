Este patrón proporciona una interfaz para crear objetos en una superclase, mientras permite a las subclases alterar el tipo de objetos que se crean.

![[Factory Method.png]]

 Para aclarar este concepto vamos a definir y entender las partes en este patrón mediante un ejemplo de productos:

1. Producto > Interfaz: Características que puede tener en común los objetos que pueden producir los creadores
2. Producto-X > Implementaciones concretas de la interfaz Producto
3. Creador > Es la clase abstracta que se encarga de devolver los objetos de productos. Aquí es importante que el tipo de retorno del método que genera los objectos de productos sea de la interfaz producto. Al este ser una clase abstracta obliga a las clases concretas a que implementen la creación de su objeto concreto Producto-X en nuestro ejemplo, además de eso esta clase abstracta implica alguna lógica que tengan en común todos los productos que se pueden producir.
4. CreadorConcretoProductoX > Aquí tenemos las diferentes implementaciones de la fabricación de los objetos concretos, esto lo hace sobrescribiendo la clase abstracta Creador, esta también podría devolver objetos existentes en una memoria caché, una agrupación de objetos u otra fuente.

[Ejemplo Typescript]([Factory Method en TypeScript / Patrones de diseño (refactoring.guru)](https://refactoring.guru/es/design-patterns/factory-method/typescript/example)) 
```Typescript
/**
 * The Creator class declares the factory method that is supposed to return an
 * object of a Product class. The Creator's subclasses usually provide the
 * implementation of this method.
 */
abstract class Creator {
    /**
     * Note that the Creator may also provide some default implementation of the
     * factory method.
     */
    public abstract factoryMethod(): Product;

    /**
     * Also note that, despite its name, the Creator's primary responsibility is
     * not creating products. Usually, it contains some core business logic that
     * relies on Product objects, returned by the factory method. Subclasses can
     * indirectly change that business logic by overriding the factory method
     * and returning a different type of product from it.
     */
    public someOperation(): string {
        // Call the factory method to create a Product object.
        const product = this.factoryMethod();
        // Now, use the product.
        return `Creator: The same creator's code has just worked with ${product.operation()}`;
    }
}

/**
 * Concrete Creators override the factory method in order to change the
 * resulting product's type.
 */
class ConcreteCreator1 extends Creator {
    /**
     * Note that the signature of the method still uses the abstract product
     * type, even though the concrete product is actually returned from the
     * method. This way the Creator can stay independent of concrete product
     * classes.
     */
    public factoryMethod(): Product {
        return new ConcreteProduct1();
    }
}

class ConcreteCreator2 extends Creator {
    public factoryMethod(): Product {
        return new ConcreteProduct2();
    }
}

/**
 * The Product interface declares the operations that all concrete products must
 * implement.
 */
interface Product {
    operation(): string;
}

/**
 * Concrete Products provide various implementations of the Product interface.
 */
class ConcreteProduct1 implements Product {
    public operation(): string {
        return '{Result of the ConcreteProduct1}';
    }
}

class ConcreteProduct2 implements Product {
    public operation(): string {
        return '{Result of the ConcreteProduct2}';
    }
}

/**
 * The client code works with an instance of a concrete creator, albeit through
 * its base interface. As long as the client keeps working with the creator via
 * the base interface, you can pass it any creator's subclass.
 */
function clientCode(creator: Creator) {
    // ...
    console.log('Client: I\'m not aware of the creator\'s class, but it still works.');
    console.log(creator.someOperation());
    // ...
}

/**
 * The Application picks a creator's type depending on the configuration or
 * environment.
 */
console.log('App: Launched with the ConcreteCreator1.');
clientCode(new ConcreteCreator1());
console.log('');

console.log('App: Launched with the ConcreteCreator2.');
clientCode(new ConcreteCreator2());
```