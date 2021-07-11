# Quiz 6: Polymorphism

Pratice problems here will try and assess your ability to:
* Write functions that can take an Object as well as their child classes.
* Understand the "Is A" relationships between classes and their ancestors.
* Be comfortable with overwriting functions that were inherited from parents.

A good place to run some of the code is on the [home page](https://cs125.cs.illinois.edu/). Some of these questions are copied from CS 199: Even More Practice (EMP) from Spring '21, source is [here](https://cs199emp.netlify.app/).

----------

## Reminder

If you haven't completed them already, `q5-objects-continued.md` contains practice problems touching on polymorphism. I'd encourage you to start there if you haven't completed them.

----------

## Polymorphism Review

Remember, polymorphism is the ability for an object to behave like multiple objects, hence the poly- prefix in the term. Here's the formal definition from [Wikipedia](https://en.wikipedia.org/wiki/Polymorphism_(computer_science)) (specifically the *subtyping* definition), but I don't think it's too helpful.

> In programming languages and type theory, polymorphism is the provision of a single interface to entities of different types

----------

## Enemies Example

Below, the example is suppose to illustrate the inheritance relationships for the respective classes shown.

![Enemies Tree](https://raw.githubusercontent.com/harsh183/emp-125/master/pics/enemies_tree.png)

Let's consider the "Is A" relationships for `Hydra`. `Hydra` *is a* `Hydra`, clearly, but through polymorphism, `Hydra` "Is A" `Dragon`, `Enemy`, and `Object` as well, i.e. `Hydra` are also the classes above it.

To prove it, here's some code.

```java
public class Enemy { }
public class Dragon extends Enemy { }
public class Hydra extends Dragon { }

Hydra h = new Hydra();

System.out.println(h instanceof Hydra);  // true
System.out.println(h instanceof Dragon); // true
System.out.println(h instanceof Enemy);  // true
System.out.println(h instanceof Object); // true
```

Now, let's answer the questions in the image regarding function overrides. Consider the example with `Wyvern` `fly()`.

1. What does the traversal look like for a `Necromancer` object to request health?

2. What does the traversal look like for a `Hydra` object to call `stab()`?

<details>
  <summary>Answer!</summary>

  1. When you try and access the `health` field for a `Necromancer` object, it'll check whether there's a `health` field within `Necromancer`. Once Java figures out that one doesn't exist, it'll check the `Enemy` class and find that there is a `health` field.

  2. When a `Hydra` object calls `stab()`, it'll check within the `Hydra` object and find that there doesn't exist a `stab()` function. Fortunately, there are parent classes to see whether the `stab()` behavior exists. Java will then check `Dragon`, `Enemy`, and finally `Object`. Once Java finds that there doesn't exist a `stab()` function, it'll return an error.
</details>

----------

## Giving Prizes Example

Thanks to `@aehasan2` for this idea.

1. Write a function, called `void givePrize(Prize p)` that accepts a `Prize` object and prints out the correct statement depending on whether it's a `Prize` object, or any of its children classes.

* If it's a `Car` object, then print the following.

```
You received a {model}.
Where are you going to go with it?
```

* If it's a `Check` object, then print the following.

```
You received a ${amount} check.
What are you going to spend it on?
```

* If it's a `Prize` object only, then print the following.

```
You received a {name}.
```

*Keep the fields private and write the necessary getters and setters.*

```java
public class Prize {
  private String name;
  
  public Prize(String setName) {
    this.name = setName;
  }
}

public class Car extends Prize {
  private String model;
  
  public Car(String setModel) {
    super("Car");
  }
}

public class Check extends Prize {
  private int amount;
  
  public Check(int setAmount) {
    super("Check");
    this.amount = setAmount;
  }
}
```

<details>
  <summary>Answer!</summary>

  ```java
  void givePrize(Prize p) {
    if (p instanceof Car c) {
      System.out.println("You received a " + c.getModel());
      System.out.println("Where are you going to go with it?");
    } else if (p instanceof Check c) {
      System.out.println("You received a $" + c.getAmount() + " check.");
      System.out.println("What are you going to spend it on?");
    } else {
      System.out.println("You received a " + p.getName() + ".");
    }
  }

  givePrize(new Check(4500));
  ```
</details>

----------

2. [Creative] Write another class that extends `Prize` and write a statement it should print for the `givePrize()` function.

<details>
  <summary>Answer!</summary>

  ```java
  public class Prize {
    private String name;
    
    public Prize(String setName) {
      this.name = setName;
    }
    
    public String getName() {
      return this.name;
    }
  }

  public class Car extends Prize {
    private String model;
    
    public Car(String setModel) {
      super("Car");
    }
    
    public String getModel() {
      return this.model;
    }
  }

  public class Check extends Prize {
    private int amount;
    
    public Check(int setAmount) {
      super("Check");
      this.amount = setAmount;
    }
    
    public int getAmount() {
      return this.amount;
    }
  }

  public class Vacation extends Prize {
    private String location;
    
    public Vacation(String setLocation) {
      super("Vacation");
      this.location = setLocation;
    }
    
    public String getLocation() {
      return this.location;
    }
  }

  void givePrize(Prize p) {
    if (p instanceof Car c) {
      System.out.println("You received a " + c.getModel());
      System.out.println("Where are you going to go with it?");
    } else if (p instanceof Check c) {
      System.out.println("You received a $" + c.getAmount() + " check.");
      System.out.println("What are you going to spend it on?");
    } else if (p instanceof Vacation v) {
      System.out.println("You received a trip to " + v.getLocation() + "!");
      System.out.println("What are you going to do when you get there?");
    } else {
      System.out.println("You received a " + p.getName() + ".");
    }
  }

  givePrize(new Vacation("Cancun"));
  ```
</details>

----------

## Social Media Posts Example

We'll try and get some practice with objects, inheritance, and polymorphism by playing with the object defined below in the context of social media posts.

```java
public class Post {
  private String post;
  private String user;
  private String platform;
  private int likes;
  
  public Post(String setPost, String setUser, String setPlatform, int setLikes) {
    this.post = setPost;
    this.user = setUser;
    this.platform = setPlatform;
    this.likes = setLikes;
  }
  
  @Override
  public String toString() {
    String output = this.user + " posted: \n";
    output += this.post + "\n";
    output += this.likes + " likes | " + this.platform;
    
    return output;
  }
}

Post p = new Post("I'm having a good day.", "jackiec3", "Twitter", 3);

System.out.println(p);
```

2. Your first task is to *extend* this class to `TwitterPost` as well as `RedditPost` that has the additional features below.

`TwitterPost`:
* An additional field for `retweets`.
* An additional function, with the signature `public void retweet(String user)` that increments `retweets` and prints the following given a user.

```
{retweetUser} retweeted:
{post}
- {user}
```

`RedditPost`:
* An additional field called `isComment`.
* An additional function, with the signature `public void upvote()`, that increments `likes`.

*Keep all the fields in `Post` private and write getter and setter functions as necessary. Remember to write out constructors for these new classes.*


<details>
  <summary>Answer!</summary>

  ```java
  public class Post {
    private String post;
    private String user;
    private String platform;
    private int likes;
    
    public Post(String setPost, String setUser, String setPlatform, int setLikes) {
      this.post = setPost;
      this.user = setUser;
      this.platform = setPlatform;
      this.likes = setLikes;
    }
    
    @Override
    public String toString() {
      String output = this.user + " posted: \n";
      output += this.post + "\n";
      output += this.likes + " likes | " + this.platform;
      
      return output;
    }
    
    public String getUser() {
      return this.user;
    }
    
    public String getPost() {
      return this.post;
    }
    
    public void addLike() {
      this.likes++;
    }
    
    public int getLikes() {
      return this.likes;
    }
  }

  public class TwitterPost extends Post {
    private int retweets;
    
    public TwitterPost(String setPost, String setUser, int setLikes,
        int setRetweets) {
      super(setPost, setUser, "Twitter", setLikes);
      this.retweets = setRetweets;
    }
    
    public void retweet(String retweetUser) {
      System.out.println(retweetUser + " retweeted:\n" + getPost() 
          + "\n- " + getUser());
    }
  }

  public class RedditPost extends Post {
    private boolean isComment;
    
    public RedditPost(String setPost, String setUser, int setLikes,
        boolean setIsComment) {
      super(setPost, setUser, "Reddit", setLikes);
      this.isComment = setIsComment;
    }
    
    public void upvote() {
      addLike();
    }
    
    public int getUpvotes() {
      return getLikes();
    }
  }

  // Post p = new Post("I'm having a good day.", "jackiec3", "Twitter", 3);
  // System.out.println(p);

  // TwitterPost t = new TwitterPost("I'm on Twitter!", "jackiec3", 4, 2);
  // t.retweet("challen");

  // RedditPost r = new RedditPost("Cool Cat Picture!", "jackiec3", 1032, false);
  // r.upvote();
  // System.out.println(r.getUpvotes());
  ```
</details>

----------

3. Write a `public static boolean sameAccount(Post one, Post two)` function that checks if the two given posts come from the same platform and from the same user.

<details>
  <summary>Answer!</summary>

  ```java
  public class Post {
    private String post;
    private String user;
    private String platform;
    private int likes;
    
    public Post(String setPost, String setUser, String setPlatform, int setLikes) {
      this.post = setPost;
      this.user = setUser;
      this.platform = setPlatform;
      this.likes = setLikes;
    }
    
    @Override
    public String toString() {
      String output = this.user + " posted: \n";
      output += this.post + "\n";
      output += this.likes + " likes | " + this.platform;
      
      return output;
    }
    
    public String getUser() {
      return this.user;
    }
    
    public String getPost() {
      return this.post;
    }
    
    public void addLike() {
      this.likes++;
    }
    
    public int getLikes() {
      return this.likes;
    }
    
    // Answer here.
    public static boolean sameUser(Post one, Post two) {
      
      boolean sameUser = one.user.equals(two.user);
      
      if (one instanceof TwitterPost && two instanceof TwitterPost) {
        return sameUser;
      } else if (one instanceof RedditPost && two instanceof RedditPost) {
        return sameUser;
      } else {
        return sameUser && one.platform.equals(two.platform);
      }
    }
  }

  public class TwitterPost extends Post {
    private int retweets;
    
    public TwitterPost(String setPost, String setUser, int setLikes,
        int setRetweets) {
      super(setPost, setUser, "Twitter", setLikes);
      this.retweets = setRetweets;
    }
    
    public void retweet(String retweetUser) {
      System.out.println(retweetUser + " retweeted:\n" + getPost() 
          + "\n- " + getUser());
    }
  }

  public class RedditPost extends Post {
    private boolean isComment;
    
    public RedditPost(String setPost, String setUser, int setLikes,
        boolean setIsComment) {
      super(setPost, setUser, "Reddit", setLikes);
      this.isComment = setIsComment;
    }
    
    public void upvote() {
      addLike();
    }
    
    public int getUpvotes() {
      return getLikes();
    }
  }

  // Post p = new Post("I'm having a good day.", "jackiec3", "Twitter", 3);
  // System.out.println(p);

  TwitterPost t = new TwitterPost("I'm on Twitter!", "jackiec3", 4, 2);
  // t.retweet("challen");

  RedditPost r = new RedditPost("Cool Cat Picture!", "jackiec3", 1032, false);
  // r.upvote();
  // System.out.println(r.getUpvotes());

  RedditPost r2 = new RedditPost("Another Cat Picture!", "jackiec3", 342, false);

  System.out.println(Post.sameUser(t, r));
  System.out.println(Post.sameUser(r, r2));
  ```
</details>

----------

4. With the `User` class defined below, write a copy constructor that takes a `User` and deep copies the posts.

```java
public class User {
  private String user;
  private Post[] posts;
  
  public User(String setUser, Post[] setPosts) {
    this.user = setUser;
    this.posts = setPosts;
  }
  
  public User(User copyUser) {
    // Your code here.
  }
}

Post[] pArray = new Post[3];
pArray[0] = new RedditPost("Cool Cat Picture!", "jackiec3", 1032, false);
pArray[1] = new RedditPost("Another Cat Picture!", "jackiec3", 342, false);
pArray[2] = new RedditPost("More Cat Pictures!", "jackiec3", 561, false);

User u = new User("jackiec3", pArray);
User u2 = new User(u);
```

<details>
  <summary>Answer!</summary>

  ```java
  public class Post {
    private String post;
    private String user;
    private String platform;
    private int likes;
    
    public Post(String setPost, String setUser, String setPlatform, int setLikes) {
      this.post = setPost;
      this.user = setUser;
      this.platform = setPlatform;
      this.likes = setLikes;
    }
    
    public Post(Post copyPost) {
      this.post = new String(copyPost.post);
      this.user = new String(copyPost.user);
      this.platform = new String(copyPost.platform);
      this.likes = likes;
    }
    
    @Override
    public String toString() {
      String output = this.user + " posted: \n";
      output += this.post + "\n";
      output += this.likes + " likes | " + this.platform;
      
      return output;
    }
    
    public String getUser() {
      return this.user;
    }
    
    public String getPost() {
      return this.post;
    }
    
    public void addLike() {
      this.likes++;
    }
    
    public int getLikes() {
      return this.likes;
    }
    
    public static boolean sameUser(Post one, Post two) {
      
      boolean sameUser = one.user.equals(two.user);
      
      if (one instanceof TwitterPost && two instanceof TwitterPost) {
        return sameUser;
      } else if (one instanceof RedditPost && two instanceof RedditPost) {
        return sameUser;
      } else {
        return sameUser && one.platform.equals(two.platform);
      }
    }
  }

  public class TwitterPost extends Post {
    private int retweets;
    
    public TwitterPost(String setPost, String setUser, int setLikes,
        int setRetweets) {
      super(setPost, setUser, "Twitter", setLikes);
      this.retweets = setRetweets;
    }
    
    public void retweet(String retweetUser) {
      System.out.println(retweetUser + " retweeted:\n" + getPost() 
          + "\n- " + getUser());
    }
  }

  public class RedditPost extends Post {
    private boolean isComment;
    
    public RedditPost(String setPost, String setUser, int setLikes,
        boolean setIsComment) {
      super(setPost, setUser, "Reddit", setLikes);
      this.isComment = setIsComment;
    }
    
    public void upvote() {
      addLike();
    }
    
    public int getUpvotes() {
      return getLikes();
    }
  }

  public class User {
    private String user;
    private Post[] posts;
    
    public User(String setUser, Post[] setPosts) {
      this.user = setUser;
      this.posts = setPosts;
    }
    
    public User(User copyUser) {
      this.user = copyUser.user;
      
      this.posts = new Post[copyUser.posts.length];
      
      for (int i = 0; i < posts.length; i++) {
        this.posts[i] = new Post(copyUser.posts[i]);
      }
    }
  }

  Post[] pArray = new Post[3];
  pArray[0] = new RedditPost("Cool Cat Picture!", "jackiec3", 1032, false);
  pArray[1] = new RedditPost("Another Cat Picture!", "jackiec3", 342, false);
  pArray[2] = new RedditPost("More Cat Pictures!", "jackiec3", 561, false);

  User u = new User("jackiec3", pArray);
  User u2 = new User(u);
  ```
</details>

----------

<!-- <details>
  <summary>Answer!</summary>
</details> -->
