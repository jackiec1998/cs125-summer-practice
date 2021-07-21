# Quiz 8: Algorithm Analysis and Lists (and Their Implementations)

Practice problems here will assess your ability to:
* Understand what the requirements are for a `List`.
* Recall the differences between an `ArrayList` and `LinkedList` implementations of a `List`.
* Be able to navigate through a `LinkedList`.
* Be able to read and assess the runtime of code snippets.


A good place to run some of the code is on the [home page](https://cs125.cs.illinois.edu/). Some of these questions are copied from CS 199: Even More Practice (EMP) from Spring '21, source is [here](https://cs199emp.netlify.app/).

----------

## Algorithms and Runtime Analysis

*Disclaimer: Going to be kind of loosey goosey with the definitions so don't nitpick too hard. It's just how I, personally, have come to understand these concepts.*

*Algorithm*, another buzzword you can use that makes you sound smarter, but in actuality it's practically just a recipe/set of directions.

An essential aspect of an *algorithm* is that it's language agnostic, which means that it doesn't depend on any particular programming language. It should follow basic programming functionalities, but resemble English for the most part.

How an algorithm looks depends on the context. If you're writing some academic paper then there's probably some formal way of going about it, but for this course writing directions in English that can be covered to code can be an algorithm. I'm pretty loose with the term.

----------

We'd like to know attributes about algorithms though right? E.g. how fast does it run? How much space does it take up? Those seem like important aspects to know! That's where *runtime analysis* comes in which is the practice of determining the speed of an algorithm. Computer scientists also consider other attributes like space, but you don't have to worry about that for this course. People who work in theory, particularly [complexity theory](https://en.wikipedia.org/wiki/Computational_complexity_theory), think about this stuff all day—how is another question.

----------

What you basically need to know it the method we used to do runtime analysis, called *Big-O notation*. Big-O notation describes the upper-bound/worse-case scenario runtime for an algorithm.

Here are some common runtimes you may encounter.

![Runtimes](https://cdn-media-1.freecodecamp.org/images/1*KfZYFUT2OKfjekJlCeYvuQ.jpeg)

They're usually referred to as these terms (not sure if you need to know this, but it's cool):
* $O(1)$ is constant time, i.e. no matter how big the input is, it takes a fixed number of steps to complete. For example, returning the first element in a list.
* $O(logn)$ is logarithm time. Not a big focus here, but you'll see it later.
* $O(n)$ is linear time, i.e. if the size of the input doubles, then the runtime should be some constant multiple of the input. For example, going through an array and calculating the sum of the integers.
* $O(nlogn)$ doesn't have a word I don't think? But you'll see it later with sorting algorithms.
* $O(n^x)$ where $x > 1$ is called polynomial time, think polynomials from high school mathematics.
* $O(x^n)$ where $x \geq 1$ is called exponential time. If you're getting to this point, then man that sucks. For example, generating all the groups of students for a group of students size $x$.
* $O(n!)$ not sure if there's a word for this, but man you really messed up to get here.

----------

When thinking about $O(n)$, you might be wondering what is $n$? The answer is usually, whatever the algorithm depends on for speed. Consider the following code below.

```java
for (int i = 0; i < arr.length; i++) {
  sum += arr[i];
}
```

Here, the $n$ would be the length of the array $arr$ because we're looping through it/operating on it. Usually you can tell what $n$ is based on the loop/what you're looping through.

----------

What's the runtime for the code snippets below? If there's no question, just give the worse-case runtime.

1.

```java
int a(int[] arr) {
  int b = 0;

  for (int i = 0; i < arr.length; i++) {
    b += arr[i];
  }

  return b;
}
```

<details>
  <summary>Answer!</summary>

  This function is summing through a given array and needs to go through each element in the array, thus the runtime is going to be linear, i.e. $O(n)$.
</details>

----------

2.

```java
int a(int[] arr) {
  int b = 0;

  for (int i = 0; i < arr.length; i++) {
    return 0;
  }

  return b;
}
```

<details>
  <summary>Answer!</summary>

  The function returns immediately whatever array is given. Trivial function and will run in constant time, i.e. $O(1)$.
</details>

----------

3. What's the best-case and worse-case runtime for this code?

```java
int a(int[] arr) {
  int b = 0;

  for (int i = 0; i < arr.length; i++) {
    b += arr[i];

    if (b == 10) {
      return 10;
    }
  }

  return b;
}
```


<details>
  <summary>Answer!</summary>

  The best case is when the first element in the array is `10` and immediately exits, thus the best-case runtime would be constant time, i.e. $O(1)$.

  Worse-case runtime would be never hitting `b == 10` and the function loops through the entire array, thus it's linear time, i.e. $O(n)$.
</details>

----------

4.

```java
int[] m(int[] a, int[] b) {
  int[] c = new int[a.length + b.length];

  for (int i = 0; i < a.length; i++) {
    c[i] = a[i];
  }

  for (int i = a.length; i < c.length; i++) {
    c[i] = b[i];
  }

  return c;
}
```

<details>
  <summary>Answer!</summary>

  This function appends to arrays together and returns. The runtime should be $O(mn)$ where $m$ is the length of $a$ and $n$ is the length of $b$. Totally legal to have the runtime be based on two terms!

  You could argue that it's linear time by doing $O(max(m, n))$.
</details>

----------

5. What's the best-case and worse-case runtime?

```java
boolean m(int[] a, int[] b) {
  for (int i = 0; i < a.length; i++) {
    for (int j = 0; j < b.length; j++) {
      if (a[i] != b[j]) {
        return false;
      }
    }
  }
}
```

<details>
  <summary>Answer!</summary>

  Best case runtime is when the conditional statement executes immediately, thus making it constant time, i.e. $O(1)$.

  Worse case runtime it loops through both arrays making it $O(mn)$ where $m$ is the length of $a$ and $n$ is the length of $b$.
</details>

----------

6. 

```java
boolean m(int[] a, int[] b) {
  int x = -1;

  if (a.length < b.length) {
    x = a.length;
  } else {
    x = b.length;
  }

  boolean p = true;

  for (int i = 0; i < x; i++) {
    if (a[i] != b[i]) {
      p = false;
    }
  }

  return false;
}
```

<details>
  <summary>Answer!</summary>

  The runtime for this function will be $O(min(m, n))$ where $m$ is the length of $a$ and $n$ is the length of $b$ because of the conditional statement after the declaration of `x`.
</details>

----------

7. What's the best-case runtime for this code? Worse-case?

```java
boolean m(int[] a, int[] b) {
  int x = -1;

  if (a.length < b.length) {
    x = a.length;
  } else {
    x = b.length;
  }

  for (int i = 0; i < x; i++) {
    if (a[i] != b[i]) {
      return false;
    }
  }

  return true;
}
```

<details>
  <summary>Answer!</summary>

  The best-case runtime will be constant time when the conditional statement in the loop returns immediately, i.e. $O(1)$.

  The worse-case runtime will be $O(min(m, n))$ where $m$ is the length of $a$ and $n$ is the length of $b$.
</details>

----------

## Lists

When we talk about lists, we're talking about the abstract idea of what a list should do. A list is technically an abstract data type, but I don't think Geoff cares about this right now so we'll just call it a data structure.

<details>
  <summary>Abstract Data Type vs. Data Structure, You Don't Need to Know This.</summary>

  A list is actually an abstract data type because it's an abstract idea of what a list should do, e.g. you should be able to read and add things to the list.

  A data structure on the other hand is how you actually implement those requirements specified by an abstract data type. For example, `ArrayList` is a data structure used to implement the abstract data type of a list.
</details>

Lists have some basic functionalities that are specified. With a list, you should be able to:
* Add, either at an index or to the ends.
* Remove, either at an index or to the ends.
* Read, at any index.
* Get the size.

In the following sections, we'll cover two ways of going about fulfilling those requirements, as well as their benefits and compromises.

### Array Lists

This is an array list.

```java
// Initial SimpleArrayList
interface SimpleList {
  Object get(int index);
  void set(int index, Object value);
  Object remove(int index);
  void add(int index, Object value);
  int size();
}
public class SimpleArrayList implements SimpleList {
  private Object[] values;

  public SimpleArrayList() {
    values = new Object[0];
  }

  public SimpleArrayList(Object[] setValues) {
    values = setValues;
  }

  public int size() {
    return values.length;
  }

  public Object get(int index) {
    assert index >= 0 && index < values.length;
    return values[index];
  }

  public void set(int index, Object value) {
    assert index >= 0 && index < values.length;
    values[index] = value;
  }

  public Object remove(int index) {
    // Code
  }
  public void add(int index, Object value) {
    // Code
  }
}
```

You can tell it's an array list because there's an underlying array, called `values`, in this instance that stores the values.

Thoughts About Array Lists:
* Array lists are fast at reading/returning values, i.e. just go to the index! We can say it's constant time, $O(1)$.
* Array lists, are usually, slower to insert/removing values, especially if it's in the middle! Why? Because you need to shift values around in the array or, even worse, have to declare in entirely new array if you don't have space! Moving all these values around or declaring a new array takes linear time, $O(n)$.
* You can get the size of an array list fast! Just call `arr.length`. Another constant time operation, $O(1)$.

----------

We'll be using this class to code.

```java
public class SimpleArrayList {
  private Object[] values;

  public SimpleArrayList(Object[] setValues) {
    this.values = setValues;
  }
}

SimpleArrayList ls = new SimpleArrayList(new Integer[]{1, 2, 3, 4, 5});
```

You probably need the `Integer` wrapper class documentation up. Particularly casting it to an `Integer` wrapper will be helpful, `Integer.MAX_VALUE`, and `new Integer(4).intValue()` will be helpful for the last one. 

1. Write a function with the following signature: `public int isGreater(Object o)` that counts the number of elements in `o` is greater than in the array list. Should return zero if any types are not `Integer`.

<details>
  <summary>Answer!</summary>

  ```java
  public int isGreater(Object o) {
    
    int count = 0;
    
    if (o instanceof Integer i) {
      for (Object value : values) {
        if (value instanceof Integer j && i > j) {
          count++;
        }
      }
    }
    
    return count;
  }
  ```
</details>

----------

2. Write a function with the following signature: `public int countEquals(Object[] arr)` that returns the number of matches between the two `Object[]`. Keep in mind that these are any `Object` arrays.


<details>
  <summary>Answer!</summary>

  ```java
  public int countEquals(Object[] arr) {
    int count = 0;
    int min = -1;
    
    if (this.values.length < arr.length) {
      min = this.values.length;
    } else {
      min = arr.length;
    }
    
    for (int i = 0; i < min; i++) {
      if (this.values[i] == arr[i]) {
        count++;
      }
    }
    
    return count++;
  }
  ```
</details>


----------

3. Wrote a function with the following function signature: `public int minimumPair()` that finds the two distinct `Integer` wrappers that make the minimum sum.

For example, this code should return `3`.

*Note: As I said at the beginning, `Integer.MAX_VALUE` and `new Integer(3).intValue()` will be helpful.*

```java
SimpleArrayList ls = new SimpleArrayList(new Integer[]{1, 2, 3, 4, 5});
System.out.println(ls.minimumPair()); // prints 3.
```

<details>
  <summary>Answer!</summary>

  ```java
  public int minimumPair() {
    int minimumPair = Integer.MAX_VALUE;
    
    for (int i = 0; i < this.values.length; i++) {
      for (int j = 0; j < this.values.length; j++) {
        if (this.values[i] instanceof Integer first && this.values[j] instanceof Integer second) {
          if (first + second < minimumPair && i != j) {
            minimumPair = first.intValue() + second.intValue();
          }
        }
      }
    }
    
    return minimumPair;
  }
  ```
</details>

----------

### Linked Lists

A linked list is a chain of nodes/elements that could look like this.

```java
public class Item {
  public Object value;
  public Item next;
}

public class SimpleLinkedList {
  public Item start;

  public SimpleLinkedList(Item setStart) {
    this.start = setStart;
  }
}
```

Thoughts About Linked Lists:
* Without keeping track of the size at the start/whenever you add or remove elements from the linked list, you can't know the size without walking the list.
* To get to any arbitrary position on the linked list, you need to *walk* the linked list, i.e. keeping asking for the next element until the next element is null, thus denoting that you're at the end of the list. This is generally slower than an array list which can just look up the index.
* Adding and removing elements from a linked list is fast, compared to array lists, because you just need to move some references around.
* You could make a normal linked list faster if we kept track of the end reference.

----------

We'll work with the `SimpleLinkedList` implementation below.

```java
public class Item {
  public Object value;
  public Item next;
  
  public Item(Object setValue, Item setNext) {
    this.value = setValue;
    this.next = setNext;
  }
}

public class SimpleLinkedList {
  public Item start;

  public SimpleLinkedList(Item setStart) {
    this.start = setStart;
  }
}

Item start = new Item("Jackie", new Item("Is", new Item("Awesome", null)));

SimpleLinkedList ls = new SimpleLinkedList(start);
```

1. Write a `toString()` function for the `SimpleLinkedList` class that prints the values contained with the linked list separated by a single space.

```java
Item start = new Item("Jackie", new Item("Is", new Item("Awesome", null)));

SimpleLinkedList ls = new SimpleLinkedList(start);

System.out.println(ls); // Prints "Jackie Is Awesome"
```

<details>
  <summary>Answer!</summary>

  ```java
  @Override
  public String toString() {
    String output = "";
    
    for (Item i = this.start; i != null; i = i.next) {
      output += i.value + " ";
    }
    
    return output;
  }
  ```
</details>

----------

2. Write an append function that takes a `SimpleLinkedList` and adds it to the end of the list you're working with.

```java
Item start = new Item("Jackie", new Item("Is", new Item("Awesome", null)));
SimpleLinkedList ls = new SimpleLinkedList(start);
Item anotherStart = new Item("Sike", new Item("You", new Item("Thought", null)));
SimpleLinkedList ts = new SimpleLinkedList(anotherStart);
ls.append(ts);
System.out.println(ls); // Prints "Jackie Is Awesome Sike You Thought"
```

<details>
  <summary>Answer!</summary>

  ```java
  public void append(SimpleLinkedList appending) {
    Item last = this.start;
    
    while (last.next != null) {
      last = last.next;
    }
    
    last.next = appending.start;
  }
  ```
</details>

----------

3. Write a getter function for the last element in the linked list.

```java
Item start = new Item("Jackie", new Item("Is", new Item("Awesome", null)));
SimpleLinkedList ls = new SimpleLinkedList(start);
System.out.println(ls.getLast()); // Prints "Awesome"
```

<details>
  <summary>Answer!</summary>

  ```java
  public Object getLast() {
    Item last = this.start;
    
    while (last.next != null) {
      last = last.next;
    }
    
    return last.value;
  }
  ```
</details>

----------
