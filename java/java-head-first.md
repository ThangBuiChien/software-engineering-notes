# Table of Contents

[Inheritance and Polymorphism](#inheritance-and-polymorphism)

[Interfaces and Abstract classes](#interfaces-and-abstract-classes)

## Inheritance and Polymorphism

[Back to Table of Contents](#table-of-contents)

### General

- **Subclass extends SuperClass** ⇔ **Subclass inherits SuperClass**.
- Multiple methods can be overridden in an object, but the **most specific** (lowest in the hierarchy) version is invoked.

### Inheritance

- **Is-a** and **Has-a** relationships:
  - **A extends B** ⇔ **A is B**.
    - Example: If `Cat extends Animal`, then asking "Is a cat an animal?" makes sense.
  - **A extends B** works only in one direction.
    - Example: Water is a drink, but not all drinks are water.
  - If "A is B" doesn’t make sense. Considering using **Has-a** relationship.
    - Example: A desk "is a" room doesn’t make sense, but a room "has a" desk does.
- **Private properties** are **not inherited**.
- To override a method but still reuse some functionality of the superclass, use **`super`**:

  ```java
  public void eat() {
      super.eat(); // Reuse superclass method
      // Additional code below
  }
  ```

- Use inheritance with **caution** — it’s not a one-size-fits-all solution for reuse. Always check the **Is-a** test.

### Polymorphism

- **How is a reference object created?**

  ```java
  Dog myDog = new Dog();
  ```

  - `Dog myDog` creates a reference variable (like a remote control) that stores a reference to the object.
  - `new Dog()` creates the actual Dog object.
  - `=` links the reference variable to the object.

- A subclass object can be assigned to a parent reference variable:

  ```java
  Animal[] animals = new Animal[3];
  animals[0] = new Dog();
  animals[1] = new Cat();
  animals[2] = new Lion();

  for (Animal animal : animals) {
      animal.eat();
      animal.roam();
  }
  ```

  ```java
  Animal animal = new Dog();
  animal.eat(); // Calls the eat method in the Dog class
  ```

  - The method called depends on the runtime type of the object, known as **runtime polymorphism**.

- Polymorphism allows any object of a subclass to use methods of the superclass.

### Override vs Overload

#### Override

- Keeps the same method signature:
  - Arguments must be the same.
  - Return types must be compatible.
  - The method can’t be less accessible.

#### Overload

- **Must** change the arguments.
- Return type and accessibility can be changed, but it's **optional**.

## Interfaces and Abstract classes

[Back to Table of Contents](#table-of-contents)

### Abstract classes

- Abstract classes mean that a class can’t be instantiated.
- Abstract methods are methods without a body.
- Have abstract method => **must** be abstract class
- In an abstract class, you can have both abstract and non-abstract methods.
- In concrete classes, you **must** implement all abstract methods.

### Object class

- Every class in Java extends class Object
- Any class that doesn’t explicitly extend another
  class, implicitly extends Object
- Object class has methods like `toString()`, `equals()`, `hashCode()`, `getClass()`

### Supper class and subclass method

- The compiler checks the class of the reference variable, not the class of the actual object at the other end of the reference.

```java
Animal animal = new Dog();
animal.bark(); // Won't work although Dog has bark method
```

=> The complier care only about the reference type, not the actual object type. It like an remote, although object could have different method outside supperclass, but the reference can only access the method of the supperclass. The others method is hidden.

```java
Animal animal = new Dog();
if (animal instanceof Dog) {
  Dog d = (Dog) animal;
}
d.bark(); // work
```

### Interfaces

- Multiple inheritance => causes Deadly Diamond of Death (DDD)
  - Ex: class Dog is extends both Pet and Animal class. Both Pet and Animal class have eat() method. So, when Dog class call eat() method, it will be ambiguous, what method will be used??
  - => using interfact solution mean abstract all method solve those problem
- A Java interface is like a 100% pure abstract class
- A class that implements an interface must implement all the methods of the interface, except default and static methods
