# Quiz 3: Strings, More Functions, Multi-Dimensional Arrays

Practice problems here will try and assess your ability to:


A good place to run some of the code is on the [home page](https://cs125.cs.illinois.edu/). Some of these questions are copied from CS 199: Even More Practice (EMP) from Spring '21, source is [here](https://cs199emp.netlify.app/).

## Strings

`String` is a new data type and also your first introduction to objects. They operate differently than the data types you've encountered already—called primitives: `int`, `double`, `char`, `boolean`. You can tell the difference between objects and primitives because *objects are capitalized.*

```java
String name = "Jackie"; // This is an object.
int age = 23; // This is a primitive.
```

Because `String`s are objects, they come with their own functions that you can access through the dot-notation. Here's the [documentation](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html) that lists some functions that `String` comes with, but here are the important ones that you should probably know: `.length()`, `.split()`, `.substring()`, `.charAt()`, `.indexOf()`, `.equals()`. There's probably more, but those are some important ones.

```java
String name = "Jackie";
System.out.println(name.length());
```

Notice that it's different than how we worked with arrays which don't require the parentheses. That might be a common misstep you'll later experience so keep this in mind.

```java
String name = "Jackie";
char[] charName = {'J', 'a', 'c', 'k', 'i', 'e'};

System.out.println(name.length());
System.out.println(charName.length);
```

Again, the reason for that difference is because `String`s are objects and to access the length of a `String` you need to call its respective function that returns the length. For a `char[]`, it's just an attribute of an array.

1. Write a function that sandwiches two strings together where the longer string will be on the ends. For example, if `String a = "Jackie"` and `String b = "Chan"`, then the function `comboString("Jackie", "Chan")` should return `"JackieChanJackie"`. Another example if that doesn't make sense: `String a = "cat"`, `String b = "poodle"`, returns `"poodlecatpoodle"`.

```java
String comboString(String a, String b) {
  return "";
}
```

<details>
  <summary>Answer!</summary>

  ```java
  public String comboString(String a, String b) {
    if (a.length() > b.length()) {
      return b + a + b;
    } else {
      return a + b + a;
    }
  }
  ```
</details>

---

2. Fill out the function below that takes a `String`, called `source`, and if a character is contained in `char[] find` then you should replace it with its respective character in `char[] replace`.

*Note: The `find` and `replace` arrays should be the same size. If they're not, then return an empty `String`.*

An example of how this works is below.

```java
char[] find = {'a', 'e'};
char[] replace = {'@', '3'};

System.out.println(swap("Jackie", find, replace));
// Prints "J@cki3"
System.out.println(swap("Charlie", find, replace));
// Prints "Ch@rli3"
```

Here's the function to fill out.

```java
String swap(String source, char[] find, char[] replace) {
  return "";
}

char[] find = {'a', 'e'};
char[] replace = {'@', '3'};

System.out.println(swap("Jackie", find, replace));
System.out.println(swap("Charlie", find, replace));
```

This may be a bit difficult, so the hint will give you some functions that might be helpful to solve the problem.

<details>
  <summary>Hint!</summary>

  I found it useful to use `.toCharArray()` in the `String` [documentation](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/String.html). It's also helpful to have a variable to store the `String` as you loop through and build it character-by-character.
</details>

<details>
  <summary>Answer!</summary>

  ```java
  String swap(String source, char[] find, char[] replace) {
    if (find.length != replace.length) {
      return "";
    }
    
    String replaced = "";
    
    for (char letter : source.toCharArray()) {
      
      boolean found = false;
      
      for (int i = 0; i < find.length; i++) {
        if (letter == find[i]) {
          replaced += replace[i];
          found = true;
        }
      }
      
      if (!found) {
        replaced += letter;
      }
    }
    
    return replaced;
  }
  ```
</details>

---

3. Write a function that will take a `String[]` and make a new `String` from the first letters contained in the array of `String`s.

Here's an example.

```java
String[] codeWords = {"Got", "edible", "otters", "from", "friends"};

System.out.println(secretCode(codeWords));
// Prints "Geoff".
```

Here's an outline for the function.

```java
String secretCode(String[] codeWords) {
  return "";
}

String[] codeWords = {"Got", "edible", "otters", "from", "friends"};

System.out.println(secretCode(codeWords));
// Prints "Geoff".
```

<details>
  <summary>Answer!</summary>

  ```java
  String secretCode(String[] codeWords) {
    String finalCode = "";
    
    for (String codeWord : codeWords) {
      finalCode += codeWord.charAt(0);
    }
    
    return finalCode;
  }
  ```
</details>

---

4. A classic interview question. Write a function that will return a `boolean` that is `true` if the `String` passed is a palindrome, i.e. is the `String` backwards the same string? For example, `racecar` is a palindrome.

```java
boolean palindrome(String word) {
  return false;
}

System.out.println(palindrome("racecar")); // Prints true.
System.out.println(palindrome("jackie")); // Prints false.
System.out.println(palindrome("anna")); // Prints true.
```

<details>
  <summary>Answer!</summary>

  ```java
  boolean palindrome(String word) {

    for (int i = 0; i < word.length() / 2; i++) {
      if (word.charAt(i) != word.charAt(word.length() - 1 - i)) {
        return false;
      }
    }
    
    return true;
  }
  ```
</details>

---

## More Functions

Again, functions are awesome. The lesson titled [More About Functions](https://cs125.cs.illinois.edu/lessons/Summer2021/014_morefunctions) talked about two important concepts: method overloading, void functions.

Method overloading allows you to have functions with the same name, but different parameters.

For example, in the lesson we present.

```java
void printIt(int count) {
  System.out.println(count);
}
void printIt(int first, int second) {
  System.out.println(first + second);
}

printIt(10);
printIt(40, 50);
```

Java can figure out which function to use by looking at the parameters.

1. Here's an intuitive example of when to use function overloading: calculating the area of different shapes. Fill out the functions below.

```java
double pi = 3.14159;

double area(double radius) {
  return -1;
}

double area(double base, double height) {
  return -1;
}
```

<details>
  <summary>Answer!</summary>

  ```java
  double area(double radius) {
    return 3.14159 * radius * radius;
  }

  double area(double base, double height) {
    return base * height / 2.0;
  }
  ```
</details>

*Note: Can't really think of another, intuitive, example of when you want to use this. It's arguably not necessary because this function name conflict can be bad design if not known and can be easily resolved by having different names. Just know that Java has this capability.*

---

If you want your function to not return anything, then `void` is the keyword you're looking for. You can still have a `return` statement, but it must be immediately followed by a semicolon. Just like other `return` statements, it immediately exits the function.

For example, you might see me write this because it's more explicit on where the function ends.

```java
void sayHello() {
  System.out.println("Hello!");
  return;
}
```

2. Create a function, called `likesCS125AndCoding()`, that will print out statements based on two `boolean` parameters passed: `likesCS125` and `likesCoding`. If you like both, it should print out `"Yay, we're so glad you like this class."`. If you liked only one, print out `"Aww, which one didn't you like?"`. If you liked neither, print out `"Dang, what can we do better?"`. Use a `void` function.

<details>
  <summary>Answer!</summary>

```java
void likesCS125AndCoding(boolean likesCS125, boolean likesCoding) {
  if (likesCS125 && likesCoding) {
    System.out.println("Yay, we're so glad you like this class");
  } else if (likesCS125 || likesCoding) {
    System.out.println("Aww, which one didn't you like?");
  } else { 
    System.out.println("Dang, what can we do better?");
  }
}

likesCS125AndCoding(true, true);
likesCS125AndCoding(true, false); 
```
</details>

---

## Multi-Dimensional Arrays

You must be asking, "why multidimensional arrays, they're so annoying!" Well, not all data can be represented intuitively by a one-dimensional array! Consider images `double[64][64][3]` (64-by-64 image with three color channels), chessboards `char[8][8]` where different characters represent pieces, or Rubrik's Cubes `char[6][3][3]` (six three-by-three faces where a `char` is associated with a color).

They're even more necessary for matrices (if you've taken linear algebra) or tensors (the next level for matrices). These are essential for machine learning if you have any interest in that.

*Note: The last problem is probably the easiest one, just lazy to move stuff around.*

1. Write a function that takes a rectangular two-dimensional `int` array that will fill out the bottom diagonal by counting from `1`.

Here's an example.

```java
void printArray(int[][] arr) {
  for (int i = 0; i < arr.length; i++) {
    for (int j = 0; j < arr[i].length; j++) {
      System.out.print(arr[i][j] + " ");
    }
    System.out.println();
  }
  
  return;
}

printArray(diagonal(new int[3][3]));
/// Prints
// 1 0 0 
// 2 3 0 
// 4 5 6

printArray(diagonal(new int[10][10]));
// 1 0 0 0 0 0 0 0 0 0 
// 2 3 0 0 0 0 0 0 0 0 
// 4 5 6 0 0 0 0 0 0 0 
// 7 8 9 10 0 0 0 0 0 0 
// 11 12 13 14 15 0 0 0 0 0 
// 16 17 18 19 20 21 0 0 0 0 
// 22 23 24 25 26 27 28 0 0 0 
// 29 30 31 32 33 34 35 36 0 0 
// 37 38 39 40 41 42 43 44 45 0 
// 46 47 48 49 50 51 52 53 54 55 
```

Here's code you can fill out.

```java
int[][] diagonal(int[][] arr) {
  return arr;
}

void printArray(int[][] arr) {
  for (int i = 0; i < arr.length; i++) {
    for (int j = 0; j < arr[i].length; j++) {
      System.out.print(arr[i][j] + " ");
    }
    System.out.println();
  }
  
  return;
}

printArray(diagonal(new int[3][3]));
printArray(diagonal(new int[10][10]));
```

The `printArray()` function is there to check your answers. *Remember to write an if statement that checks if the two-dimensional array is rectangular.*

---

2. Write a function that will return a boolean of whether or not a phone number was found in a two-dimensional array that lists phone numbers. The function takes a two-dimensional `int` array as well as a one-dimensional array for the target phone number.

*Note: None of these are my phone number, so don't try.*

```java
boolean phoneLookUp(int[][] phoneNumbers, int[] targetNumber) {
  // Your code here.
}

int[][] phoneNumbers = new int[4][10];
phoneNumbers[0] = new int[]{4, 5, 3, 5, 4, 3, 4, 6, 7, 8};
phoneNumbers[1] = new int[]{7, 5, 6, 3, 4, 6, 2, 6, 8, 3};
phoneNumbers[2] = new int[]{8, 4, 3, 3, 5, 3, 1, 4, 5, 6};
phoneNumbers[3] = new int[]{1, 3, 6, 7, 8, 4, 3, 2, 5, 6};

int[] firstTarget = {4, 5, 3, 5, 4, 3, 4, 6, 7, 8};
int[] secondTarget = {5, 3, 5, 3, 2, 8, 6, 3, 6, 7};


System.out.println(phoneLookUp(phoneNumbers, firstTarget)); // Prints true.
System.out.println(phoneLookUp(phoneNumbers, secondTarget)); // Prints false.
```

<details>
  <summary>Answer!</summary>

  ```java
  boolean phoneLookUp(int[][] phoneNumbers, int[] targetNumber) {
    for (int[] phoneNumber : phoneNumbers) {

      boolean match = true;

      for (int i = 0; i < phoneNumber.length; i++) {
        if (phoneNumber[i] != targetNumber[i]) {
          match = false;
          break;
        }
      }
      
      if (match) {
        return true;
      }
      
    }
    
    return false;
  }

  int[][] phoneNumbers = new int[4][10];
  phoneNumbers[0] = new int[]{4, 5, 3, 5, 4, 3, 4, 6, 7, 8};
  phoneNumbers[1] = new int[]{7, 5, 6, 3, 4, 6, 2, 6, 8, 3};
  phoneNumbers[2] = new int[]{8, 4, 3, 3, 5, 3, 1, 4, 5, 6};
  phoneNumbers[3] = new int[]{1, 3, 6, 7, 8, 4, 3, 2, 5, 6};

  int[] firstTarget = {4, 5, 3, 5, 4, 3, 4, 6, 7, 8};
  int[] secondTarget = {5, 3, 5, 3, 2, 8, 6, 3, 6, 7};


  System.out.println(phoneLookUp(phoneNumbers, firstTarget)); // Prints true.
  System.out.println(phoneLookUp(phoneNumbers, secondTarget)); // Prints false.
  ```
</details>

---

3. Given any two-dimensional `int` array, including ones that are not rectangular, calculate the sum. Call the function `sum()` and return the sum.

Here's a test case, this should print `95`.

```java
System.out.println(sum(new int[][]{
    {10, 10, 10},
    {25, 25},
    {0, 0, 0, 7, 8}
}));
```

<details>
  <summary>Answer!</summary>

  ```java
  int sum(int[][] arr) {
    
    int sum = 0;
    
    for (int[] subArr : arr) {
      for (int element : subArr) {
        sum += element;
      }
    }
    
    return sum;
  }
  ```

</details>