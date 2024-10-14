## Inheritance and Polymorphism

### General

- **Subclass extends SuperClass** ⇔ **Subclass inherits SuperClass**.
- Multiple methods can be overridden in an object, but the **most specific** (lowest in the hierarchy) version is invoked.

### Inheritance

- **Is-a** and **Has-a** relationships:
  - **A extends B** ⇔ **A is B**.
    - Example: If `Cat extends Animal`, then asking "Is a cat an animal?" makes sense.
  - **A extends B** works only in one direction.
    - Example: Water is a drink, but not all drinks are water.
  - If "A is B" doesn’t make sense, it’s a **Has-a** relationship.
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
