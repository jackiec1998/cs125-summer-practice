# Quiz 9: Maps, Hashing, Exceptions

Practice problems here will assess your ability to:

A good place to run some of the code is on the [home page](https://cs125.cs.illinois.edu/). Some of these questions are copied from CS 199: Even More Practice (EMP) from Spring '21, source is [here](https://cs199emp.netlify.app/).

----------

## Hashing

Here's the definition of a hash function from [Wikipedia](https://en.wikipedia.org/wiki/Hash_function).

> A hash function is any function that can be used to map data of arbitrary size to fixed-size values. The values returned by a hash function are called hash values, hash codes, digests, or simply hashes.

![Hash Function](https://upload.wikimedia.org/wikipedia/commons/thumb/5/58/Hash_table_4_1_1_0_0_1_0_LL.svg/300px-Hash_table_4_1_1_0_0_1_0_LL.svg.png)

*What does that mean in laymen terms?* Usually, at least on the context of this course, it means a function that takes some arbitrary data and converts it to some fixed number.

You might be thinking: how does it convert it over? What makes a good hash function? Good questions! Obviously, a hash function that just returns `1` wouldn't be that helpful, but what is helpful?

Here are some attributes to helpful hash functions:
* *Returns fixed size values.* The hash function must return values in a specified range, for example plus or minus 1,000.
* *Must be a deterministic function.* Another fancy word, but it just means that if you pass in the same input, you get the same output every time, i.e. you can determine what the output is based solely on the input.
* *The outputs must be uniform.* In other words, given a bunch of inputs, the outputs shouldn't all cluster in one place. Let's take a hash function that only returns values from 0 to 10. What it means to be uniform is when you take a lot of inputs, the outputs are evenly spread throughout the range. It wouldn't be helpful to just have them land on 0 because of *collisions*.

A *collision* happens when a hash function takes two different inputs and produces the same output. A good hash function reduces this as much as possible.

> An example of hashing is your (assuming you're American for a second) social security number. The government takes information about you: when you're born, where you're born, etc. and gives you a number that looks like XXX-XX-XXXX. It's clear in this instance that collisions would be really bad. Also, the outputs of this hash function aren't uniform because two people from Minneapolis, or the same hospital, are likely to have similar social security numbers which is bad.

----------

1. Take the `Infant` class below and create a `getSocialSecurity()` that returns an integer from 0 to 999, that represents a dumb-version of a Social Security number, based on the attributes in the class. Feel free to use `.hashCode()` on the `String`.

```java
public class Infant {
  private String name;
  private String hospital;
  private String city;
  
  public Infant(String setName, String setHospital, String setCity) {
    this.name = setName;
    this.hospital = setHospital;
    this.city = setCity;
  }
}

Infant jackie = new Infant("Jackie", "St. John", "Minneapolis");
System.out.println(jackie.getSocialSecurity());
```

<details>
  <summary>Answer!</summary>

  ```java
  public int getSocialSecurity() {
    return Math.abs(this.name.hashCode()
      + this.hospital.hashCode()
      + this.city.hashCode()) % 1000;
  }
  ```
</details>

----------

2. You're on the Internet and want to download a file. On the website, it hosts the file you want as well as a hash associated with that function. How does the hash help you confirm that you downloaded the correct file? What attributes of hash functions allow you to confirm the file you installed is the same one hosted on the website?

<details>
  <summary>Answer!</summary>

  Once you download the file, you can use the same hash function that the website used on the file you downloaded and see if the hash that comes out is the same one on the website.

  If the hash function is deterministic and uniform, then the same file will return the same hash and any permutation to the file will result in a drastically different hash.
</details>


----------

## Maps

Maps are an interface that `HashMap`s implement. You can think of a map like a dictionary where it holds keys, say the words in a dictionary, and values, the definitions associated with those words.

What do you expect a map to do?
* *Add.* Be able to place key, value pairs into a map.
* *Remove.* Remove key, value pairs into a map.
* *Get.* Given a key, get the value associated with the key.

1. Why are collisions bad for maps?

<details>
  <summary>Answer!</summary>

  Because multiple collisions will result in longer retrieval times because it needs to traverse the associated linked list at that table index/bucket.
</details>

----------

2. What can we do to reduce the number of collisions in a `HashMap` implementation?

<details>
  <summary>Answer!</summary>

  Having a good hash function—remember that we said that a good hash function is both deterministic and uniform—would resolve this issue, particularly the uniform attribute because it will result in indices that are spread out.
</details>

----------

3. How does the table size underlying the `HashMap` influence the hash function?

<details>
  <summary>Answer!</summary>

  The table size under the `HashMap` will determine the fixed values that the hash function can return. If the table only has ten indices, then the hash function can only return values from 0 to 9.
</details>

----------

4. What's the big-O runtime for the `get()` function for `HashMap`? Think about the worse-case.

<details>
  <summary>Answer!</summary>

  Because big-O concerns the worse-case scenario, we need to consider the instance where the hash function returns the same index over and over again resulting in collisions after the first value as been placed.

  If that's the case, then we would need to traverse a linked list of $n$ elements for each `.get()` call because they all fall into the same index/bucket. Thus making `.get()` a linear time operation, $O(n)$.

  Despite `.get()` being a theoretically linear time operation, practically/the average case though, assuming that we have a good hash function, it would be a constant time algorithm.
</details>

----------

5. What data types can `HashMap` store? How do you specify the data types?

<details>
  <summary>Answer!</summary>

  You can store any object within a `HashMap`! You can specify the data types through the type parameters in the angle brackets. For example, consider the `HashMap` below that links a `Person` object to a `String`.

  ```java
  Map<Person, String> yearbookQuote = new HashMap<>();
  ```
</details>

----------

6. Make a public class called `BanList` that contains a map of `String` keys and `Boolean`, note the capitalization, as values. Initialize the map as a `HashMap` in the constructor and write these functions below.

* A function called `analyzePost()` that takes a `String` for the user and `String` for their `post`. The function will check if the `post` contains the word `"cheat"`. If the post does, then add them to the ban list map with the value `true`.

* A function called `getUser()` that takes a `String` for the user and looks up whether they're banned by returning a `boolean`.

Here's some test code.

```java
BanList bl = new BanList();
bl.analyzePost("jackiec3", "here's an easy way to cheat!");
System.out.println(bl.getUser("jackiec3")); // Prints true.
```

<details>
  <summary>Answer!</summary>

  ```java
  import java.util.Map;
  import java.util.HashMap;

  public class BanList {
    private Map<String, Boolean> banList;
    
    public BanList() {
      this.banList = new HashMap<>();
    }
    
    public void analyzePost(String user, String post) {
      if (post.contains("cheat")) {
        banList.put(user, new Boolean(true));
      }
    }
    
    public boolean getUser(String user) {
      return banList.getOrDefault(user, false);
    }
  }

  BanList bl = new BanList();
  bl.analyzePost("jackiec3", "Here's an easy way to cheat!");
  System.out.println(bl.getUser("jackiec3"));
  ```
</details>

----------

## Exceptions

You're going to write buggy code, it's inevitable. Things are going to go wrong. If that's not you, go to Silicon Valley and make your millions.

Luckily Java has the ability, as well as other programming languages, to deal with errors gracefully.

The main piece of code we'll be concerning is this try-catch block. Where we *try* some code that might *throw* an exception and a place to *catch* said exception.

To be thrown by the keyword `throw`, it must be a `Throwable` which has three subclasses: checked exceptions, unchecked exceptions, and errors.

* *Checked exceptions.* Must be caught, enforced by the compiler, anything that comes from the `Exception` class.
* *Unchecked exceptions.* Doesn't have to be caught, but they may arise from programmer error.
* *Errors.*  Serious problems, you shouldn't be catching these. Asserts produce errors as well as other things we'll cover later on.

Another component to keep in mind is the `finally` block in the try-catch statement which states what code should be executed at the end *always*.

You can also create your own exceptions as well through the syntax below.

```java
public class MyException extends Exception { }
```

1. Start off by writing a class called `Safe` that has two `String` fields that are private: `contents` and `passCode`. Set those values in the constructor.

2. Write your own exception called `IncorrectPassCode`.

3. Write a function called `unlockSafe()` that take a `String` attempting the passcode. If it matches, then return the contents, else throw that exception you made. Make sure that the function specifies that it throws that exception.

4. Create a `Safe` instance, pass in an incorrect pass code and catch the exception.

<details>
  <summary>Answer!</summary>

  ```java
  public class IncorrectPassCode extends Exception { }

  public class Safe {
    
    private String contents;
    private String passCode;
    
    public Safe(String setContents, String setPassCode) {
      this.contents = setContents;
      this.passCode = setPassCode;
    }
    
    public String unlockSafe(String s) throws IncorrectPassCode {
      if (s.equals(this.passCode)) {
        return this.contents;
      } else {
        throw new IncorrectPassCode();
      }
    }
  }

  Safe mySafe = new Safe("Embarassing middle school picture.", "Hippo341");
  try {
    mySafe.unlockSafe("Apple311");
  } catch (IncorrectPassCode e) {
    System.out.println("Darn, that wasn't right.");
  }
  ```
</details>

----------


5. Is the `IncorrectPassCode` a checked exception, unchecked exception, or an error?

<details>
  <summary>Answer!</summary>

  It's a checked exception because it extends the `Exception` class.
</details>

----------