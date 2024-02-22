
# Herencia

En la herencia hay clases que pueden compartir características en común , esto me permite reutilizar clases; creando una nueva clase que ***extienda*** los métodos, atributos y estructura  de la clase existente sin tener que reescribir este código.

Sin embargo en esta nueva clase denominada sub-clase puede tener atributos y métodos que no existían en la super-clase  (Padre).   

# Polimorfismo

El polimorfismo es la capacidad de un objeto de hacer cuna acción de diferentes maneras mediante métodos iguales que se implementen de manera diferentes en varias clases. 

- Polimorfismo estático -> Tiempo de compilación -> [[POO (Programación Orientada a Objetos) - Java#Overload(Sobre Carga)|Overload]]
	mediante la creación de diferentes métodos con el mismo nombre pero con parámetros diferentes y/o en un diferente orden, nos permite tener diferentes comportamientos según lo previamente mencionado.
- Polimorfismo dinámico -> Tiempo de ejecución  -> [[POO (Programación Orientada a Objetos) - Java#Override(Sobre Escritura)|Override]]
	mediante una sobre escritura del método realizamos una implementación que tenga el comportamiento adecuado para la necesidad.

```java
class Animal {
  public void makeSound() {
    System.out.println("Grr...");
  }
}
class Cat extends Animal {
  public void makeSound() {
    System.out.println("Meow");
  }
}
class Dog extends Animal {
  public void makeSound() {
    System.out.println("Woof");
  }
}
```

```java
public static void main(String[ ] args) {
  Animal a = new Dog();
  Animal b = new Cat();
  
  Animal animals[] = new Animal[2];
  animals[0] = a;
  animals[1] = b;
}
```

```java
a.makeSound();
//Outputs "Woof"

b.makeSound();
//Outputs "Meow"
```

# Encapsulamiento

Este concepto nos permite tener claro la capacidad que se tiene de tener acceso a características de nuestra clase, ya sea a los atributos o métodos. 

- **private (privado):**  En este nivel se puede declarar miembros accesibles sólo para la propia clase.
- **public (publico):**  Todos pueden acceder a los datos o métodos de una clase que se definen con este nivel, este es el nivel más bajo, esto es lo que tú quieres que la parte externa(otra clase) vea.
- **protected (protegido):** Podemos decir que estás no son de acceso público, solamente son accesibles dentro de su clase y por subclases, es decir, solo puede ser usados por las clases que la heredan.

# Abstracción

Es el concepto que nos define un SER/ES de una clase, ya que una clase abstracta, debe tener como mínimo un método abstracto y además de eso se debería usar el modificador protected para que sus hijos puedan usar sus atributos y de igual forma con los métodos. Se podría decir que una clase abstracta funciona como una plantilla para una nueva clase que extienda de esta.   



# Interfaces 

- Las interfaces es una colección  de métodos abstractos que por lo regular no tienen atributos pero si dado el caso tienen atributos estos deben ser constantes.
- Una clase y una interfaz puede implementar múltiples interfaces.
- Dice lo que se debe hacer mas no el como, lo que quiere decir que son métodos abstractos lo cual implica que no declara un implementación.

# Override(Sobre Escritura)

Cuando realizamos un override de un método estamos  realizando una implementación de un método abstracto, esto quiere decir que estamos definiendo que va a hacer el método, lo estamos cambiando, por esto se dice que lo estamos sobre-escribiendo. 
# Overload(Sobre Carga)

Son múltiples métodos los cuales tienen el mismo nombre pero los parámetros que se le pasan son diferentes, tanto en cantidad como en orden. Según esto se usara el respectivo donde coincidan los parámetros y realizara la función que tiene asignado el mismo. 

