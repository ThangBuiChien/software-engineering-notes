## Inheritance and polymorphism

### General

Subclass extends SuperClass <=> Subclass inherited SuperClass

Many method override in one object? => the **lowest** the most **specifics** one wins

### Inheritance

- Using is-a and has-a
  - A extends B <=> A is B
  - Ex: Cat extends Animal then ask "Cat is animals" is make sense or not?
  - A extends B in just **one direction**
  - Ex: Water is a drinks but not all drinks is water
  - "A is B" not make sense => it is "has-a" relationship
    Ex: desk "is-a" room is not make sends but room "has-a" desk ok
- Private properties is **not** inherited
- Override method but not change whole but want reuse some ==> **super**

```java
public void eat(){
    super.eat();
    // new more code below
}
```

- Use Inheritance with **_caution_** -> it not all-size-fit-all for reuse. ALWAYS check the "is-a" test

### Polymorphism

- How reference object is created?

  ```java
  Dog myDog = new Dog();
  ```

  - **Dog myDog** = new Dog()=> allocate space for a reference variable, think it like like **an remote** which store an reference to the object
  - Dog myDog = **new Dog()** => create **dog object**
  - Dog myDog **=** new Dog(); => program, link the remote control

- Object of subclass is could be linked in parent reference varibles

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
    animal.eat() //Call the eat method in Dog class
    //it based on the run time type of object to call the method ==> run time polymorphism
```

==> polymorphism. Any object of class that extends superclass could use these method

### Override vs Overload

#### Override

=> Keep the contract

- Arguments must be the same
- Return types must be compatible
- The method can’t be less accessible

#### Overload

- **Must** change arguments
- Return type, accessible could be changed **optional**
