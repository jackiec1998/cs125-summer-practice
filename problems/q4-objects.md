# Quiz 4: Introduction to Objects

Practice problems here will try and assess your ability to:
* Define objects using classes.
* Understand the terminology around objects.
* Have the ability to create a constructor.
* Be able to write getters and setters.
* Know how visibility modifiers change the scope of certain fields within a class.

A good place to run some of the code is on the [home page](https://cs125.cs.illinois.edu/). Some of these questions are copied from CS 199: Even More Practice (EMP) from Spring '21, source is [here](https://cs199emp.netlify.app/).

## Objects: The Basics

Objects encompass two attributes: state and behavior. You define objects using *classes*.

Here's an example of a class with both state and behavior highlighted.

```java
class Cat {

  // Here's the state.
  String name;
  String breed;
  int age;
  boolean hasWorms;

  // Here's the behavior.
  void meow() {
    System.out.println("Meow!");
  }

  void purr() {
    System.out.println("Purrr.");
  }
}
```

To use some of the terminology listed in [Introduction to Objects](https://cs125.cs.illinois.edu/lessons/Summer2021/027_objects1). The `cat` object is defined using the `cat` class above. We can declare *instances* of `cat` objects, e.g. `Cat rocky = new Cat();`. The methods in the class define the class's/object's behavior, and the variables defined within are its state.

----------

Here's a list version if that's more helpful.

- **Object:** A bundle of variables and functions/methods that specify the behavior of a new structure, e.g. `String name` and `int age` for a `Person` object.
- **Class:** The blueprint to define the *state and behaviors* of an object, e.g. a `Car` class.
- **Instance**: An occurance (was about to use instance) of a class.

**Altogether:** I'm going to define a `Vehicle` *object* using a *class* so that I can produce *instances* of `Vehicles` like a 2013 Toyota Camry.

Objects, and *object-oriented programming*, is a defining feature to most programming languages. It won't go away. Understanding it will help you program in other languages and represent the real world computationally.

----------

Creating new instances of an object require you to use the `new` keyword. To access the variables within the class, otherwise known as *fields*, you use dot notation.

Here's an example.

```java
class Cat {
  String name;
  String breed;
  int age;
  boolean hasWorms;

  void meow() {
    System.out.println("Meow!");
  }

  void purr() {
    System.out.println("Purrr.");
  }
}

Cat rocky = new Cat();

rocky.name = "Rocky";
rocky.breed = "House Cat";
rocky.age = 4;
rocky.hasWorms = false;

System.out.println(rocky.name);
```

This may seem familiar to `String`, and that's because `String`s are objects too! Now you have the ability to define your own objects just like `String`. What a power!

1. Let's define an object, using a class, called `Enemy` for a video game. The enemy should have a `name`, `healthPoints`, `loot`, `weapon`, and other variables (be creative). Enemies should also be able to `attack`, `die` and `heal`. Feel free to add other methods.

```java
class Enemy {
  // your variables and methods here.
}

Enemy goblin = new Enemy();

goblin.name = "Wruk";
goblin.healthPoints = 10;
goblin.weapon = "Club";
goblin.loot = "Gold Pouch";

goblin.attack();
String loot = goblin.die();

System.out.println("You killed the goblin, this is your loot: " + loot);
```

<details>
  <summary>Answer!</summary>

  ```java
  class Enemy {
    String name;
    int healthPoints;
    String weapon;
    String loot;

    void attack() {
      System.out.println(name + " attacked with a " + weapon);
      return;
    }

    String die() {
      System.out.println(name + " died.");
      return loot;
    }

    void heal() {
      healthPoints += 10;
      return;
    }
  }
  ```
</details>

----------

2. Create a `SocialMediaAccount` object by filling out the requirements and functions below.

```java
class SocialMediaAccount {
  // I need variables to store:
  // - username
  // - age
  // - bio
  // - pronouns
  // - country
  // - logged in, denoting whether you're logged in or not
  
  void makePost(String post) {
    // Should print out the below if logged in.

    // <username>, <pronouns> posted:
    // 
    // <post>
    // 
    // From <country>.

    // If you're not logged in, then print "You need to log in first!"
  }

  void login() {
    // Make the variable storing login to true if you're not logged in.
    // Or print "You're already logged in!" if they're already logged in.
  }

  void logout() {
    // Similar behavior to login().
  }
}

// Try making an account, fill in each variable, and making a post!
```

<details>
  <summary>Answer!</summary>

  ```java
  class SocialMediaAccount {
    String username;
    int age;
    String bio;
    String pronouns;
    String country;
    boolean loggedIn;
    
    void makePost(String post) {
      if (loggedIn) {
        System.out.println(username + ", " + pronouns + " posted:");
        System.out.println(post);
        System.out.println("From " + country);
      } else {
        System.out.println("You need to log in first!");
      }
    }

    void login() {
      if (!loggedIn) {
        loggedIn = true;
      } else {
        System.out.println("You're already logged in!");
      }
    }

    void logout() {
      if (loggedIn) {
        loggedIn = false;
      } else {
        System.out.println("You're already logged out!");
      }
    }
  }

  SocialMediaAccount myAccount = new SocialMediaAccount();
  myAccount.username = "jackiec3";
  myAccount.age = 23;
  myAccount.bio = "I am a graduate student.";
  myAccount.pronouns = "he/him/his";
  myAccount.country = "United States";
  myAccount.login();
  myAccount.makePost("I am having a good day today!");
  ```
</details>

----------

## Constructors

Remember how much it sucked to write this?

```java
class Person {
  String name;
  int age;
  String undergrad;
}

Person jackie = new Person();
jackie.name = "Jackie";
jackie.age = 23;
jackie.undergrad = "Carleton College";

Person jeanne = new Person();
jeanne.name = "Jeanne";
jeanne.age = 19;
jeanne.undergrad = "University of Minnesota";
```

So many lines. Well, constructors resolves this a little!

```java
class Person {
  String name;
  int age;
  String undergrad;

  Person(String setName, int setAge, String setUndergrad) {
    name = setName;
    age = setAge;
    undergrad = setUndergrad;
  }
}

Person jackie = new Person("Jackie", 23, "Carleton College");

Person jeanne = new Person("Jeanne", 19, "University of Minnesota");
```

Much more elegant and less repetitive! Less repetitive means less prone to errors.

1. Write a constructor for this class below that initializes all the fields.

```java
class Email {
  String subject;
  String body;
  String recipients;
}

// Declare an email instance using the constructor.
```

<details>
  <summary>Answer!</summary>

  ```java
  class Email {
    String subject;
    String body;
    String recipients;

    Email(String setSubject, String setBody, String setRecipients) {
      subject = setSubject;
      body = setBody;
      recipients = setRecipients;
    }
  }

  // Declare an email instance using the constructor.
  Email invitation = new Email(
      "Increase Grade?",
      "Hey Geoff. I'm really close to a D, can you increae my grade?",
      "challen@illinois.edu"
  );
  ```
</details>

----------

2. Overload the constructor in the `Email` object so you can set just the `subject` and `body` and default the `recipients` to `""`.

<details>
  <summary>Answer!</summary>

  ```java
  class Email {
    String subject;
    String body;
    String recipients;

    Email(String setSubject, String setBody, String setRecipients) {
      subject = setSubject;
      body = setBody;
      recipients = setRecipients;
    }

    Email(String setSubject, String setBody) {
      subject = setSubject;
      body = setBody;
      recipients = "";
    }
  }

  // Declare an email instance using the constructor.
  Email invitation = new Email(
      "Increase Grade?",
      "Hey Geoff. I'm really close to a D, can you increae my grade?",
      "challen@illinois.edu"
  );
  ```
</details>

----------

## Encapsulation

What a fancy word, huh?

*Laymen Explanation:* Only let the user interact with what is *necessary*.

How do you limit visibility to users? Using *access/visibility modifiers* (e.g. `private`, `public`) and getter and setter methods. For example, take an account object already defined.

```java
class Account {
  String username;
  String password; // should be "private String password;"
}

Account jackiec3 = new Account("jackiec3", "computerscienceisawesome2!");

// Without visibility modifiers, I can do. Not good.
System.out.println(jackiec3.password);
```

1. Take the `Playlist` object defined below. Add the visibility modifiers and define these getter and setter methods.

```java
class Playlist {
  String[] playlist;
  String name;
  int numSongs;

  Playlist(String setName) {
    name = setName;
    playlist = new String[100]; // only 100 songs
  }

  // addSong(String song)
  // getPlaylist()
  // getSongByIndex(int index) gets the song at a particular index in the playlist
  // setName(String name) sets the name of the playlist
}
```

<details>
  <summary>Answer!</summary>

  ```java
  class Playlist {
    private String[] playlist;
    private String name;
    private int numSongs;

    Playlist(String setName) {
      name = setName;
      playlist = new String[100]; // only 100 songs
    }

    void addSong(String song) {
      playlist[numSongs] = song;
      numSongs++;
    
      return;
    }

    String[] getPlaylist() {
      return playlist;
    }

    String getSongByIndex(int index) {
      if (index < numSongs) {
        return playlist[index];
      } else {
        return "No song at index.";
      }
    }

    void setName(String setName) {
      name = setName;
      return;
    }
  }
  ```
</details>

----------

2. Define a `Tweet` object that has private variables for `String body`, `String username`, `String date`, `int numRetweets`, `int numMentions`, `int numReplies`, and `Tweet[] replies`.

    When you initialize a `Tweet`, you must pass in the `username`, `body`, and `date` and those cannot be changed once created (*use a constructor*). Define getters and setters listed: `addRetweet/Mentions()`, `addReply(Tweet reply)`, and `getBody/Username/Date/NumRetweets/NumMentions/Replies()`.

```java
class Tweet {
  
  // variables
  private Tweet[] replies;

  // constructor
  Tweet(String setBody, String setUsername, String setDate) {
    // your code
    replies = new Tweet[100]; // only 100 replies allowed
  }

  // getters and setters
}

Tweet myTweet = new Tweet("Summer CS 125 is going great!", "jackiec3", "06/30/2021");

// add a bunch of retweets cause I'm popular
for (int i = 0; i < 100; i++) {
  myTweet.addRetweet();
}

myTweet.addReply(new Tweet("That's good to hear!", "challen", "06/30/2021"));
```

<details>
  <summary>Answer!</summary>

  ```java
  class Tweet {
    
    // variables
    private Tweet[] replies;
    private String body;
    private String username;
    private String date;
    private int numRetweets;
    private int numMentions;
    private int numReplies;

    // constructor
    Tweet(String setBody, String setUsername, String setDate) {
      body = setBody;
      username = setUsername;
      date = setDate;

      replies = new Tweet[100]; // only 100 replies allowed
      numRetweets = 0;
      numMentions = 0;
      numReplies = 0;
    }

    void addReply(Tweet reply) {
      replies[numReplies] = reply;
      numReplies++;
      return;
    }

    // repeat for addMentions
    void addRetweet() {
      numRetweets++;
      return;
    }

    // repeat for username, date, numRetweets, numMentions, replies
    String getBody() {
      return body;
    }
  }
  ```
</details>
