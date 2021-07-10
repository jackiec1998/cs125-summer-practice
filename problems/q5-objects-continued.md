# Quiz 5: Objects Continued

Practice problems here will try and assess your ability to:
* Use `static`, `final`, and `this` keyword when defining classes.
* Understand inheritance and how to use `extend` to create child classes.
* Know what polymorphism is, the "is a" relationships, and up/downcasting associated with polymorphism.
* Have the capability to override functions from a parent class, e.g. checking for equality, converting objects to `String`, and copying.
* Grasp references and how they relate to objects.


A good place to run some of the code is on the [home page](https://cs125.cs.illinois.edu/). Some of these questions are copied from CS 199: Even More Practice (EMP) from Spring '21, source is [here](https://cs199emp.netlify.app/).

## `static`, `final`, and `this`

In the lesson titled, [Static](https://cs125.cs.illinois.edu/lessons/Summer2021/034_static), we actually introduce three new keywords: `static`, `final`, and `this`. In my opinion, `this` is probably the most unintuitive keyword to get your head around. I'll be using it because it makes clearer code, despite having to type more. You do you.

Laymen Definitions for New Keywords:
* `static`: A keyword you use in front of methods and variables to specify that you want all instances to share a particular method/variable, e.g. "All dog instances will use the same bark method because all dogs bark the same. I don't care about the particular instance." *Note: You cannot access instance variables and you can call static methods/variables without initializing an instance.*

```java
public class Dog {
  static void bark() {
    System.out.println("Bark, bark, bark!");
  }
}

Dog.bark(); // Calling bark() without a declared instance.

Dog myDog = new Dog();
Dog herDog = new Dog();

myDog.bark();
herDog.bark();
// myDog and herDog are calling the same method, not special to a particular instance.
```

* `final`: A keyword you place in front of variables to specify that you *cannot* reassign them from their initial value, i.e. "I want this variable to not change/be a constant."

```java
public class Circle {
  static final double PI = 3.14159;
}

System.out.println(Circle.PI);
Circle.PI = 3; // Error because PI is final.
```

* `this`: A keyword you use to refer to the *current* instance that's executing the method, i.e. "I want the object I'm working on right now, thus I need to use `this`." *Note: `this` is largely unnecessary, but more clear usually. It is required to call other constructors when you overload your constructor.*

```java
public class Student {
  
  String name;

  public Student() {
    this("Noname"); // Call the second constructor, with "Noname" as the name.
  }

  public Student(String setName) {
    this.name = setName; // this.name meaning the name variable in the student we're initializing.
  }

  public void introduction() {
    // Yes, this isn't necessary, but it's more clear.
    System.out.println("Hi, my name is " + this.name + "!");
  }
}

Student me = new Student("Jackie");
me.introduction();
```

1. Add a `private`, `static` variable to the `Student` class below called `numStudents`, initialized to `0`. `numStudents` will increment up by one each time the constructor is called. Also add a get function for the `numStudents` variable. Your code should execute the following lines after the class declaration.

```java
public class Student {
  // variable

  // constructor

  // get function
}

Student jeff = new Student();
Student jessica = new Student();

System.out.println("There are " + Student.getStudents() + " students.");
```

<details>
  <summary>Answer!</summary>

  ```java
  public class Student {
    private static int numStudents = 0;
    
    public Student() {
      numStudents++;
    }
    
    public static int getStudents() {
      return numStudents;
    }
  }
  ```
</details>

----------

2. Add a constructor to the `Warrior` class that takes no parameters, and call the given constructor with default values for `healthPoints`, `weapon`, and `armor`. You can choose what the default values are.

```java
public class Warrior {
  private int healthPoints;
  private String weapon;
  private String armor;
  
  public Warrior(int setHealthPoints, String setWeapon, String setArmor) {
    this.healthPoints = setHealthPoints;
    this.weapon = setWeapon;
    this.armor = setArmor;
  }
}

Warrior leif = new Warrior(); // This should work with the additional constructor.
```
<details>
  <summary>Answer!</summary>

```java
public class Warrior {
  private int healthPoints;
  private String weapon;
  private String armor;
  
  public Warrior(int setHealthPoints, String setWeapon, String setArmor) {
    this.healthPoints = setHealthPoints;
    this.weapon = setWeapon;
    this.armor = setArmor;
  }

  public Warrior() {
    this(100, "Club", "Iron Plate Armor");
  }
}

Warrior leif = new Warrior(); // This should work with the additional constructor.
```
</details>

----------

3. Create a class called `Country`. Set up three instance variables inside `Country` called: `name`, `nationalBird`, and `populationSize`. Create a constructor that uses the `this` keyword to initialize all three variables.

<details>
  <summary>Answer!</summary>

  ```java
  public class Country {
    private String name;
    private String nationalBird;
    private int populationSize;

    public Country(String setName, String setNationalBird, int setPopulationSize) {
      this.name = setName;
      this.nationalBird = setNationalBird;
      this.populationSize = setPopulationSize;
    }
  }
  ```
</details>

----------

4. Create a second constructor for `Country` that takes in a national bird and name, but not population size. Reuse the previous constructor above and set the default population size to 100.

<details>
  <summary>Answer!</summary>

  Add this constructor to the above answer.

  ```java
  public Country(String setName, String setNationalBird) {
    this(setName, setNationalBird, 100);
  }
  ```
</details>

----------

## Inheritance

Inheritance allows us to create relationships between classes. We can *inherit* the behaviors/attributes of one class by *extending* another class. Inheritance can be useful when we have objects that share functionality.

`extends` is used to create a one-way relationship between two classes; the child class *extends* the parent class. `super` is used by the child constructor to call the parent constructor; it **must** be called at the start of the constructor.

`private` variables in the parent class are *not* accessible by the child classes, but children can access `protected`, `public`, and default visible variables and functions.

1. Create a class called `Animal`. `Animal` has one method called `sleep()` that prints `"I am sleeping."`. After that, create a class called `Fish`. `Fish` is a child class of `Animal`. `Fish` has one method called `swim()` that prints `"I am swimming!"`. A correctly defined `Fish` instance should be able to print both `"I am sleeping."` and `"I am swimming!"`.

```java
Fish nemo = new Fish(); 
System.out.println(nemo.swim());
System.out.println(nemo.sleep());
```

<details>
  <summary>Answer!</summary>

  ```java
  public class Animal {
    public String sleep() {
      return "I am sleeping.";
    }
  }

  public class Fish extends Animal {
    public String swim() {
      return "I am swimming!";
    }
  }
  Fish nemo = new Fish(); 
  System.out.println(nemo.swim());
  System.out.println(nemo.sleep());
  ```
</details>

----------

2. Follow the steps below that walk you through a `Computer` object definition and respective child classes.

* Create a `Computer` class with two instance variables: `name` and `batteryPercentage`. Create a constructor for `Computer` that initializes both of these variables.

* Create a class called `DellComputer`. `DellComputer` should inherit the same instance variables as `Computer`, but it also has an instance variable called `screenSize`. Create a constructor for `DellComputer` that uses `super` to call the parent constructor and initializes `screenSize`.

* Create a class called `AppleComputer`. `AppleComputer` should inherit the same instance variables as `Computer`, but also has an instance variable called `color`. Create a constructor for the `AppleComputer` class that uses the `super` keyword and initializes `color`.

<details>
  <summary>Answer!</summary>

  ```java
  // Computer is the parent class.
  public class Computer {
    String name; 
    int batteryPercentage; 
    public Computer(String setName, int setBatteryPercentage) {
      this.name = setName; 
      this.batteryLife = setBatteryPercentage; 
    }
  }

  // DellComputer is a child class of Computer.
  public class DellComputer extends Computer {
    int screenSize; 
    public DellComputer(int setScreenSize) {
      super("Dell Computer", 100);
      this.screenSize = setScreenSize; 
    }
  }

  // AppleComputer is a child class of Computer.
  public class AppleComputer extends Computer {
    String color; 
    public AppleComputer(String setColor) {
      super("Apple Computer", 100);
      this.color = setColor;
    }
  }
  ```
</details>

----------

3. Inheritance also allows you to override certain functionality from a parent class. Use the `@Override` annotation to override the `equals()` function for the `Enemy` class. Two `Enemy` classes will be equal to each other if their `healthPoints` and `mana` are equal.

```java
class Enemy {
  int maxHealth;
  int maxMana;

  // some annotation here
  public boolean equals(Object o) {

    // check if o is an instance of an Enemy.

    // cast and check maxHealth and maxMana.

  }
}

class Dragon extends Enemy { }
class Griffin extends Enemy { }

Dragon d = new Dragon();
d.maxHealth = 100;
d.maxMana = 200;

Griffin g = new Griffin();
g.maxHealth = 100;
g.maxMana = 200;

// Should print out true.
System.out.println(d.equals(g));
```
<details>
  <summary>Answer!</summary>

  ```java
  class Enemy {
    int maxHealth;
    int maxMana;

    @Override
    public boolean equals(Object o) {

      if (o instanceof Enemy) {
        Enemy e = (Enemy) o;
        
        if (e.maxHealth == this.maxHealth && e.maxMana == this.maxMana) {
          return true;    
        }
        
      }
      
      return false;

    }
  }
  ```
</details>

## Polymorphism

Another fancy word like encapsulation. *Polymorhpism* is the idea that objects can morph into multiple (hence the *poly-*) different objects.

```java
// Pet is a Object
class Pet { }

// Dog is a Pet
// Dog is a Object
class Dog extends Pet { }

// Mutt is a Dog
// Mutt is a Pet
// Mutt is a Object
class Mutt extends Dog { }
```

1. Given the code, answer the question for each function.

```java
class FlyingObject { }
class UFO extends FlyingObject { }
class Airplane extends FlyingObject { }
class JetLiner extends Airplane { }
class AirbusA380 extends JetLiner { }
class Missile extends FlyingObject { }

// What inputs are acceptable for these functions?
void foo(Object o) { }
void voo(JetLiner j) { }
void too(UFO u) { }
void woo(FlyingObject f) { }
```

<details>
  <summary>Answer!</summary>

  `foo()` can take in all objects, i.e. `FlyingObject`, `UFO`, `Airplane`, `JetLiner`, `AirbusA380`, and  `Missile`.

  `voo()` can only take `JetLiner` and `AirbusA380` objects because the latter is a child of `JetLiner`.

  `too()` can only take `UFO`, not `FlyingObject` because `FlyingObject` are not necessarily `UFO`s.

  `woo()` can take all objects defined above, i.e. `FlyingObject`, `UFO`, `Airplane`, `JetLiner`, `AirbusA380`, and `Missile` because they're all flying objects/have `FlyingObject` as an ancestor at some point.
</details>

----------

Another part of polymorphism is the ability to upcast and downcast objects from parents to children. For example, we can downcast an `Animal` instance to a `Dog`.

Upcasting, child going to a parent, is nice because the instance is losing some abilities/attributes from extending the parent.

```java
FlyingObject myPrivateJet = new JetLiner();
```

Downcasting, on the other hand, is annoying because we need to check if downcasting is possible.

Here's a case where it would go wrong, assuming we have an `Animal` class with two child classes: `Dog`, `Cat`.

```java
public class Animal { }
public class Dog extends Animal { }
public class Cat extends Animal { }

Animal myAnimal = new Cat(); // Upcasting, good, no problems.
Dog myDog = (Dog) myAnimal; // Downcasting, bad, because myAnimal is not an instance of Dog.

System.out.println(myAnimal instanceof Animal); // true
System.out.println(myAnimal instanceof Cat); // true
System.out.println(myAnimal instanceof Dog); // false
```

Going back to the `FlyingObject` example, to downcast, we need to check if it's possible using `instanceof`.

```java
FlyingObject myPrivateJet = new JetLiner();

if (myPrivateJet instanceof JetLiner) { // Check if downcasting is possible.
  JetLiner jet = (JetLiner) myPrivateJet; // Downcasting.
  // Now I have access to JetLiner unique fields and methods.
  jet.flyLuxuriously();
}

// Does the same thing.
if (myPrivateJet instanceof JetLiner jet) {
  jet.flyLuxuriously();
}
```

2. Write a function that takes any `Drink` object, and its children classes, and spills it by printing `"I spilled {name}!"` and setting `empty` to `true`.

```java
public class Drink {
  private String name;
  public boolean empty;
  
  public Drink(String setName) {
    this.name = setName;
    this.empty = true;
  }
  
  public String getDrink() {
    return this.name;
  }
}

public class Boba extends Drink {
  public Boba() {
    super("Boba");
  }
}
public class Soda extends Drink {
  public Soda() {
    super("Soda");
  }
}
public class Beer extends Drink {
  public Beer() {
    super("Beer");
  }
}
```

<details>
  <summary>Answer!</summary>

  ```java
  public void spill(Drink d) {
    System.out.println("I spilled " + d.getDrink() + "!");
    d.empty = true;
  }
  ```
</details>

----------

3. Create a method called `vetVisit()` that accepts a single `Pet` parameter and returns a `String` depending on the type `Pet` that's visiting. You can assume that all `Pets` have a method called `isRegular()` which returns a `boolean` value indicating whether the pet is a regular. If the `Pet` is `null` or not one of the described ones, you should return `null`.

* If the pet is a `Dog` and regular, the visit will be a `"Regular Grooming"`. If the pet is a Dog but not a regular, the visit will be a `"Parasite Prevention Session"`.

* If the pet is a `Cat`, the visit will be a `"Cat Wellness Exam"`.

* If the pet is a `Hamster`, the visit will be a `"Dental Care Visit"`.

```java
public class Pet {
  boolean isRegular() {
    return true;
  }
}

public class Dog extends Pet { }
public class Cat extends Pet { }
public class Hamster extends Pet { }
```
<details>
  <summary>Answer!</summary>

  ```java
  public String vetVisit(Pet p) {

    if (p instanceof Dog) {
      if (p.isRegular()) {
        return "Regular Grooming";
      } else {
        return "Parasite Prevention Session";
      }
    }

    if (p instanceof Cat) {
      return "Cat Wellness Exam";
    }

    if (p instanceof Hamster) {
      return "Dental Care Visit";
    }

    return null; 
  }
  ```
</details>

----------

4. Use the `Movie` class to accomplish the following.

* What's anothe class that could descend from `Movie`? What's a unique attribute/method it would have?

* Create the child class you came up with on the previous bullet point.

* Create an instance of your custom class and store it in a `Movie` object. After that, downcast it and call its unique function.

```java
class Movie {
  private int generalRating; 
  public int getGeneralRating() {
    return generalRating; 
  }
}

class Romance extends Movie { 
  private int cheesyRating; 
  public int getCheesyRating() {
    return cheesyRating;
  }
  
}

Movie twilight = new Romance(); // upcasting example 
twilight.getCheesyRating(); // will this run?
twilight.getGeneralRating(); // will this run? 
```

<details>
  <summary>Answer!</summary>

  ```java
  class Movie {
    private int generalRating; 
    public int getGeneralRating() {
      return generalRating; 
    }
    
  }

  // new child class 
  class International extends Movie {  
    private int language; 
    public int getLanguage() {
      return language;
    }
  }

  Movie parasite = new International();
  if (parasite instanceof International) {
    International parasiteMovie = (International) parasite;
    parasiteMovie.getLanguage();
  }
  ```
</details>

----------

## Object Equality and Copying

We already did a problemm on object equality above in inheritance where we're checking if two `Enemy` instances are equal to each other. The essential component to that question is our new ability to *override* certain functions from the parent class. Another helpful instance is overriding the `toString()` function which will allow us to print objects elegantly.

Here's an example of overriding the `toString()` function to make print statements look better.

```java
public class Mountain {
  String name;
  int height;
  int numSummits;

  public Mountain(String setName, int setHeight, int setNumSummits) {
    this.name = setName;
    this.height = setHeight;
    this.numSummits = setNumSummits;
  }

  @Override
  public String toString() {
    return this.name + " is " + this.height + " meters tall.\n"
        + "There have been " + this.numSummits + " summits.";
  }
}

Mountain kilimanjaro = new Mountain("Mount Kilimanjaro", 5885, 2345);
System.out.println(kilimanjaro);
```

Moving onto copying, there is no built in way to copy objects. That's why you have to program one yourself! You can do that by defining a copy constructor that takes an instance of itself and assigns its values to the passed in instance.

1. Give it a try with the `Goblin` object below.

```java
class Goblin {
  String clan;
  String weapon;

  Goblin(Goblin c) {
    // Your code here.
  }
}

int armySize = 100;
Goblin original = new Goblin();
original.clan = "Highlands";
original.weapon = "Spear";

Goblin[] army = new Goblin[armySize];

for (int i = 0; i < armySize; i++) {
  army[i] = new Goblin(original);
}
```

<details>
  <summary>Answer!</summary>

  ```java
  class Goblin {

    String clan;
    String weapon;

    Goblin(Goblin c) {
      this.clan = c.clan;
      this.weapon = c.weapon;
    }

  }
  ```
</details>

2. Implement deep copy with the following `Playlist` class.

```java
public class Playlist {
  private String[] playlist; 
  
  public Playlist(String[] songs) {
    this.playlist = songs;
  }

  // Write your copy constructor here.
}

String[] songs = {"Dear John", "22", "cardigan"};
Playlist one = new Playlist(songs);
Playlist second = new Playlist(one);
```

<details>
  <summary>Answer!</summary>

  ```java
  public class Playlist {
    private String[] playlist; 
    
    public Playlist(String[] songs) {
      this.playlist = songs;
    }

    // Write your copy constructor here.
    public Playlist(Playlist copy) {
      this.playlist = new String[copy.playlist.length];
      for (int i = 0; i < copy.playlist.length; i++) {
        playlist[i] = copy.playlist[i];
      }
    }
  }
  ```
</details>

----------

Here are some images I find helpful in remembering the difference between shallow and deep copy.

![Shallow Copy](https://raw.githubusercontent.com/harsh183/emp-125/master/pics/shallow_copy.png)

![Deep Copy](https://raw.githubusercontent.com/harsh183/emp-125/master/pics/deep_copy.png)

## References

Here's some analogies to understand references better. The address is a house's reference. A phone number is the reference to a phone. A student ID is a reference to a particular student.

An object just stores the reference to the object, not the object itself. You can see the reference by running the following.

```java
public class Student {
  String name;

  public Student(String setName) {
    this.name = setName;
  }
}

Student me = new Student("Jackie");
System.out.println(me);
```

After the `Student@` part, the following is the reference in memory for that particular `Student` object. That's also why this works the way it does.

```java
public class Student {
  String name;

  public Student(String setName) {
    this.name = setName;
  }
}

Student me = new Student("Jackie");
Student another = me;
another.name = "John";
System.out.println(me.name);
```

Because `another` is manipulating the same reference as `me`. It's also the reason why we avoid using `==` for objects because it's just reference equality, i.e. if the object is in the same memory position. That's a trivia definition of equality—sometimes objects are equal to each other when they're in different memory locations.

There aren't any practice problems for references. This new understanding of references helps you understand your code more thoroughly, so reflect on some previous assignments with this new concept of references!

Good luck, have fun on the quiz.