# Quiz 7: Interfaces

Practice problems here will try and assess your ability to:
* Understand the difference between abstract classes, interfaces, anonymous classes and their respective use cases.
* Be able to implement abstract classes, interfaces, and anonymous classes.

A good place to run some of the code is on the [home page](https://cs125.cs.illinois.edu/). Some of these questions are copied from CS 199: Even More Practice (EMP) from Spring '21, source is [here](https://cs199emp.netlify.app/).

## Abstract Classes

The `abstract` keyword can be used for *both* classes and methods. To use it in methods, it need to be in an abstract class.

The usual case for using abstract classes and methods is when there is a common parent class, but it doesn't make sense to be able to instantiate it. The classic example is a `Shape` class where you don't want your user to declare `Shape`s, rather they should declare its descendents.

Again, abstract classes *cannot* be instantiated, but they can be inherited.

Abstract methods within abstract classes are functions that are shared with descendents, but the implementation details are left empty for the parent class. The details of the abstract methods are left for the children to fill in.

Here's an example using `NPC` or non-player characters in a video game.

*Note: Just like regular classes, you can only inherit from one abstract class, unlike interfaces which will see later on.*

```java
public abstract class NPC {
  private String name;
  private int health;
  private String[] inventory;
  
  public NPC(String setName, int setHealth, String[] setInventory) {
    this.name = setName;
    this.health = setHealth;
    this.inventory = setInventory;
  }
  
  public abstract void greet();
}

public class Merchant extends NPC {
  
  private int gold;
  private String merchantType;
  
  public Merchant(String setName, int setHealth, String[] setInventory,
      int setGold, String setMerchantType) {
    super(setName, setHealth, setInventory);
    
    this.gold = setGold;
    this.merchantType = setMerchantType;
  }
  
  public void greet() {
    System.out.println("Greetings traveler! Would you like to see my goods?");
  }
  
}
```

1. Extend this `NPC` class to `Wizard` where `Wizard`s have a `private int mana` field. Be sure to fill in the `greet()` implementation details so that it prints: `"I study spells and enchantations, how may I help you?"`

<details>
  <summary>Answer!</summary>

  ```java
  public class Wizard extends NPC {
    private int mana;
    
    public Wizard(String setName, int setHealth, String[] setInventory,
        int setMana) {
      super(setName, setHealth, setInventory);
      
      this.mana = setMana;
    }
    
    public void greet() {
      System.out.println("I study spells and enchantations, how may I help you?");
      
    }
  }
  ```
</details>

----------

2. Create an abstract class for `SocialMediaPlatform` with the following functions and extend it to your favorite social media platform.

`SocialMediaPlatform` should have these *abstract* functions:
* `public void login()`
* `public void logout()`
* `public String post(String content, String author)`

Logging in and out should just print a message saying you're logged into a particular social media platform you implement, and `post()` should just return a `String` containing the formatted post, for example:

```
{author} posted:
{content}
```

<details>
  <summary>Answer!</summary>

  ```java
  public abstract class SocialMediaPlatform {
    public abstract void login();
    public abstract void logout();
    public abstract String post(String content, String author);
  }

  public class Twitter extends SocialMediaPlatform {
    public void login() {
      System.out.println("Welcome to Twitter!");
    }
    
    public void logout() {
      System.out.println("Goodbye! Hope to see you again soon on Twitter.");
    }
    
    public String post(String content, String author) {
      return author + " tweeted:\n" + content;
    }
  }

  Twitter twitterInstant = new Twitter();
  System.out.println(twitterInstant.post("Hello, Twitter!", "jackiec3"));
  ```
</details>

----------

## Interfaces

Interfaces allow you to write, in a sense, contracts that classes that *implement* said interface should fulfill. For example, you've seen `Comparable` already. If you implement the `Comparable` interface, you promise that you will write a function called `public int compareTo(Object o)`.

Someone asked, what's stopping you from just providing a function the interface requires and returning some garbage? Nothing. But that wouldn't be too helpful.

Another helpful aspect of interfaces is using it as a parameter in another function. For example, take a look at the code below.

```java
interface Vehicle {
  void start();
}

public class FordF150 implements Vehicle {
  public void start() {
    System.out.println("Vroom, vroom, I'm a truck.");
  }
}

public class ToyotaCamry implements Vehicle {
  public void start() {
    System.out.println("Vroom, vroom, I'm a mid-size car.");
  }
}

void startCar(Vehicle v) {
  v.start();
}

startCar(new ToyotaCamry());
```

*Note: Interfaces can only specify public-facing functions.*

1. A local resturant has hired you to be their technical consultant. The resturant's online ordering system currently has a class for Pizza, Burgers, and Salads. The resturant wants to add a new feature to their site for special items on their menu. To properly connect with specials page they are designing, the menu items must implement the following methods:
* `void setDealPrice()` - sets the price of the item to be half the original price.
* `void removeAllToppings()` - removes all the toppings on the items (i.e. sets it to `null`)
* `void setSpecialName()` - sets the name of the special to be `specialName`, e.g. specialPizza.

```java
public interface Special {
  // Your code here.
}

// Implement the interface for Pizza.
public class Pizza {
  String name;
  double price;
  String[] toppings; 
}
```

<details>
  <summary>Answer!</summary>

  ```java
  public interface Special {
    void setDealPrice();
    void removeAllToppings();
    void setSpecialName(); 
  }

  public class Pizza implements Special {
    String name;
    double price;
    String[] toppings; 

    public void setDealPrice() {
      price *= 0.5;
    }

    public void removeAllToppings() {
      for (int i = 0; i < toppings.length; i++) {
        toppings[i] = null;
      }
    }

    public void setSpecialName() { 
      name = "special" + name;
    }
  }
  ```
</details>

----------

2. Implement these interfaces to the Mansion class.
* `Pool` interface: `swim()` should print `"Splash"` and `suntan()` should print `"Getting sun-kissed skin!`.
* `Butler` interface: `callButler()` should print `"What may I help you with?"`.
* `Vineyard` interface: `getGrapeType()` should return the grape type in the vineyard.

```java
interface Pool {
  void swim();
  void suntan();
}

interface Butler {
  void callButler();
}

interface Vineyard {
  String getGrapeType();
}

class Mansion {
  // Your code here.
}
```

<details>
  <summary>Answer!</summary>

  ```java
  class Mansion implements Pool, Butler, Vineyard {
    public void swim() {
      System.out.println("Splash!");
    }
    
    public void suntan() {
      System.out.println("Getting sun-kissed skin!");
    }
    
    public void callButler() {
      System.out.println("What may I help you with?");
    }
    
    public String getGrapeType() {
      return "Sauignon Blanc";
    }
  }
  ```
</details>

----------

3. Modify the `Player` so that it implements `DungeonMaster`.

```java
public interface DungeonMaster {
  boolean canCreateDungeonInstance(); // should return true 
  int increaseHealth(); // should increase health points by one 
};

public class Player {
  private String userName;
  private int healthPoints;
  private String state;
  
  public Player(String name) {
    userName = name;
    state = "ALIVE";
    healthPoints = 100;
  }
  public String isAlive() {
    return state;
  }
}
```

<details>
  <summary>Answer!</summary>

  ```java
  public interface DungeonMaster {
    boolean canCreateDungeonInstance();
    int increaseHealth();
  };

  public class Player implements DungeonMaster {
    private String userName;
    private int healthPoints;
    private String state;
    
    public Player(String name) {
      userName = name;
      state = "ALIVE";
      healthPoints = 100;
    }
    public String isAlive() {
      return state;
    }
    
    public boolean canCreateDungeonInstance() {
      return true;
    }
    
    public int increaseHealth() {
      return healthPoints++;
    }
  }
  ```
</details>

----------

4. Implement the `Comparable` interface for `Player` above. Two players are equal if they have the same health points. A player is greater than the other player if they have more health points.

<details>
  <summary>Answer!</summary>

  ```java
  public interface DungeonMaster {
    boolean canCreateDungeonInstance();
    int increaseHealth();
  };


  public class Player implements DungeonMaster, Comparable {
    private String userName;
    private int healthPoints;
    private String state;
    
    public Player(String name) {
      userName = name;
      state = "ALIVE";
      healthPoints = 100;
    }
    public String isAlive() {
      return state;
    }
    
    public boolean canCreateDungeonInstance() {
      return true;
    }
    
    public int increaseHealth() {
      return healthPoints++;
    }
    
    public int compareTo(Object o) {
      assert o instanceof Player;
      Player p = (Player) o;
      return this.healthPoints - p.healthPoints;
    }
  }
  ```
</details>

----------

## Anonymous Classes

Anonymous classes have no name, must extend another class or implement an interface, be created immediately since they can't be named later, cannot provide a constructor, and can capture variables outside of the scope of the anonymous class.

Here's an example.

```java
public class Camera {
  public String getType() {
    return "Nikon";
  }
}
Camera basic = new Camera(); 

Camera dslr = new Camera() { // extending a class.
  @Override
  public String getType() {
    return "Nikon D90 DX";
  }
};

System.out.println(basic.getType());
System.out.println(dslr.getType());

interface Include {
  boolean include(int x);
};

int y = 0;

Include in = new Include() { // implementing an interface.
  @Override 
  public boolean include(int x) {
    return x > y; // captures y outside on previous line.
  }
};

System.out.println(in.include(10));
```

1. Use an anonymous class to implement the following interface for a language of your choice.

```java
interface Greet {
  void greetSomeone(String name);
}

// create an anonymous class.

<your anonymous class>.greetSomeone("Jackie");
```

<details>
  <summary>Answer!</summary>

  ```java
  interface Greet {
    void greetSomeone(String someone);
  };

  // create your anonymous class here
  Greet spanishGreeting = new Greet() {
    public void greetSomeone(String someone) {
      System.out.println("Hola " + someone);
    }
  };

  spanishGreeting.greetSomeone("Jackie"); //prints Hola Akhila 
  ```
</details>

----------

2. Modify the class below so that it implements `Iterable` and `Iterator` interfaces correctly.

```java
import java.util.Iterator;

// Ignore the <String>, it's generics, but it makes it look prettier.
public class PlaylistIterable implements Iterable<String>, Iterator<String> {
  private String[] songs;
  
  public PlaylistIterable(String[] setSongs) {
    this.songs = setSongs;
  }

  public Iterator iterator() {
    // Your code here.
  }

  public boolean hasNext() {
    // Your code here.
  }

  public String next() {
    // Your code here.
  }
}

String[] songs = {"Melancholy Hill", "Boredom", "willow", "Gasoline"};

PlaylistIterable iterable = new PlaylistIterable(songs);
for (String value : iterable) {
  System.out.println(value);
}
```

<details>
  <summary>Answer!</summary>

  ```java
  import java.util.Iterator;

  // Ignore the <String>, it's generics, but it makes it look prettier.
  public class PlaylistIterable implements Iterable<String>, Iterator<String> {
    private String[] songs;
    
    public PlaylistIterable(String[] setSongs) {
      this.songs = setSongs;
    }

    private int currentIndex;

    public Iterator iterator() {
      currentIndex = 0;
      return this;
    }

    public boolean hasNext() {
      return currentIndex < songs.length;
    }

    public String next() {
      String nextSong = songs[currentIndex];
      currentIndex++;
      return nextSong;
    }
  }

  String[] songs = {"Melancholy Hill", "Boredom", "willow", "Gasoline"};

  PlaylistIterable iterable = new PlaylistIterable(songs);
  for (String value : iterable) {
    System.out.println(value);
  }
  ```
</details>