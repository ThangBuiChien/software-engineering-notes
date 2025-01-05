# OCA Oracle Certified Associate Java SE 8 Programmer I Study Guide

# table of content

[Chapter 1: Java Building Blocks](#chapter-1-java-building-blocks)

[Chapter 2: Operators and Statements](#chapter-2-operators-and-statements)

[Chapter 3: Core Java APIs](#chapter-3-core-java-apis)

[Chapter 4: Methods and Encapsulation](#chapter-4-methods-and-encapsulation)

[Chapter 5: Class Design](#chapter-5-class-design)

[Chapter 6: Exceptions](#chapter-6-exceptions)

## Chapter 1: Java Building Blocks

## Chapter 2: Operators and Statements

## Chapter 3: Core Java APIs

## table of content

[string is something special](#string-is-something-special)

[immutable](#immutable)

[string pool](#string-pool)

[important string methods](#important-string-methods)

[string builder](#stringbuilder)

[understanding equality](#understanding-equality)

[Array](#java-array)

### String is something special

```java
String name = "Fluffy"; //Check in string pool if it already exists
String name = new String("Fluffy"); //Create new one and not care about string pool
```

=> String could be created with a literal or a new keyword. The slightly different is in "String pool"

### Immutable

String is immutable. Once a String object is created, it cannot be changed. You can think of a string as a storage box you have perfectly full and whose sides can’t
bulge.

### String pool

String pool store all the string literals => reuse the same string literal for memory efficiency.

### Important String methods

#### length()

```java
String string = "animals";
System.out.println(string.length()); // 7
```

#### charAt()

```java
String string = "animals";
System.out.println(string.charAt(0)); // a
System.out.println(string.charAt(6)); // s
System.out.println(string.charAt(7)); // throws exception
```

#### indexOf()

```java
String string = "animals";
System.out.println(string.indexOf('a')); // 0
System.out.println(string.indexOf("al")); // 4
System.out.println(string.indexOf('a', 4)); // 4
System.out.println(string.indexOf("al", 5)); // -1
```

#### substring()

```java
String string = "animals";
System.out.println(string.substring(3)); // mals
System.out.println(string.substring(3, 4)); // m
System.out.println(string.substring(3, 7)); // mals
System.out.println(string.substring(3, 3)); // empty string
System.out.println(string.substring(3, 2)); // throws exception
System.out.println(string.substring(3, 8)); // throws exception
```

#### toLowerCase() and toUpperCase()

```java
String string = "animals";
System.out.println(string.toLowerCase()); // animals
System.out.println(string.toUpperCase()); // ANIMALS
```

#### equals() and equalsIgnoreCase()

```java
String string = "animals";
System.out.println(string.equals("animals")); // true
System.out.println(string.equals("Animals")); // false
System.out.println(string.equalsIgnoreCase("Animals")); // true
```

#### startsWith() and endsWith()

```java
String string = "animals";
System.out.println(string.startsWith("ani")); // true
System.out.println(string.startsWith("Ani")); // false
System.out.println(string.endsWith("als")); // true
System.out.println(string.endsWith("Als")); // false
```

#### contains()

```java
String string = "animals";
System.out.println(string.contains("al")); // true
System.out.println(string.contains("Al")); // false
```

#### replace()

```java
String string = "animals";
System.out.println(string.replace('a', 'A')); // AnimAls
System.out.println(string.replace("al", "AL")); // AnimALs
```

#### trim()

```java
String string = " animals ";
System.out.println(string.trim()); // animals
```

#### Methods chaining

```java
String result = "AniMaL ".trim().toLowerCase().replace('a', 'A');
System.out.println(result); // Animal
```

### StringBuilder

```java
StringBuilder sb = new StringBuilder("start");
sb.append("+middle");
StringBuilder same = sb.append("+end");
System.out.println(sb); // start+middle+end
System.out.println(same); // start+middle+end
```

#### Creating a StringBuilder

```java
StringBuilder sb1 = new StringBuilder(); // empty string
StringBuilder sb2 = new StringBuilder("animal"); // animal
StringBuilder sb3 = new StringBuilder(10); // reserve a certain number of slots
```

#### Important methods

```java
charAt(), indexOf(), length(), and substring()
// Like string methods
```

append()

```java
StringBuilder sb = new StringBuilder().append(1).append('c');
sb.append("-").append(true);
System.out.println(sb); // 1c-true
```

insert()

```java
StringBuilder sb = new StringBuilder("animals");
sb.insert(7, "-");
sb.insert(0, "-");
sb.insert(4, "-");
System.out.println(sb); // -ani-mals
```

delete() and deleteCharAt()

```java
StringBuilder delete(int start, int end)
StringBuilder deleteCharAt(int index)

StringBuilder sb = new StringBuilder("animals");
sb.delete(0, 2);
sb.deleteCharAt(1);
System.out.println(sb); // mals
```

reverse()

```java
StringBuilder sb = new StringBuilder("ABC");
sb.reverse();
System.out.println(sb); // CBA
```

toString()

```java
StringBuilder sb = new StringBuilder("animals");
String s = sb.toString();
```

#### StringBuilder vs StringBuffer

String buffer is exactly the same StringBuilder but with thread safe

### Understanding Equality

== compares the value of two references (on the stack) to see whether they refer to the same object on the heap.
equals() compares the value of two objects to see if they are meaningfully equivalent.

### Java array

```java
int[] numbers1 = new int[3];
// type of array, array symbol, name of array, size of array
```
