# Quiz 2: Loops, Arrays, Functions

Practice problems here will try and assess your ability to:
* Use both `for` and `while` loops, i.e. know how to declare and manipulate `for` and `while` loops.
* Extend our knowledge of data types and declare arrays that store the respective data types that we've learned: `int`, `double`, `char`, `boolean`.
* Know how to declare and call functions by understanding a function's components: return value, parameters, etc.
* Understand why functions are helpful in your code.

A good place to run some of the code is on the [home page](https://cs125.cs.illinois.edu/). Some of these questions are copied from CS 199: Even More Practice (EMP) from Spring '21, source is [here](https://cs199emp.netlify.app/).

## Loops

From the lesson introducing [loops](https://cs125.cs.illinois.edu/lessons/Summer2021/008_loops), you were introduced to two types of loops: the `for` and `while` loops. Being familiar with how to read, write, and manipulate these will be essential for the course. Both of these loops can be used interchangeably, but `for` loops might look more elegant than `while` loops—and vice versa—in some occasions. You'll get a more intuitive sense of when to use them with more practice.

You need to specify three components for a `for` loop described below.

```java
for (<initialization>; <condition>; <update>) {
   <body>
}
// 1. When will this for loop stop? What variable is being incremented each loop?
for (int age = 0; age < 15; age++) {
  System.out.println("I am " + age + " years old.");
}
```

<details>
  <summary>Answer!</summary>

  1. The loop above runs fifteen times running through 0 to 14. It excludes 15 because `15 < 15` is a false conditional expression. The `age` variable gets incremented each pass through.
</details>

---

2. Create a `for` loop that prints out consecutively the integergs from 50 to 0 backwards, i.e. the first iteration should print 50, the last should print 0.

3. Write a `for` loop that begins at your current age and decrements by 2 at every iteration until 0. Within the loop, write a conditional statement to check if the counter for the loop is below to 2. If so, print out "Hurray!"

<details>
  <summary>Answer!</summary>

  2.
  ```java
  for (int i = 50; i >= 0; i--) {
    System.out.println(i);
  }
  ```

  3.
  ```java
  for (int age = 23; age >= 0; age = age - 2) {

    System.out.println(age);

    if (age < 2) {
      System.out.println("Hurray!");
    }

  }
  ```
</details>

---

`while` loops have a different structure than `for` loops. With a `while` loop, the incrementing should be happening within the code block. Here's an example of converting from a `for` loop to a `while` loop to illustrate that change.

```java
for (int even = 2; even < 100; even += 2) {
  System.out.println("This is an even number: " + even);
}
System.out.println(even); // This line doesn't work.
```
```java
int even = 2;
while (even < 100) {
  System.out.println("This is an even number: " + even);
  even += 2;
}
System.out.println(even); // This line works.
```

The above `for` loop does the same thing as the `while` loop below. The only difference is that the variable `even` doesn't get deleted after the loop completes.

4. Try converting this `for` loop to a while loop.

```java
double interest = 1.07;
int years = 0;
double savings = 1000;

for (; savings < 1000000; savings *= interest) {
  savings += 6000;
  years++;
}

System.out.println("Time to retire! You retired in " + years + " years.");
System.out.println("You have $" + savings + " in savings.");
```

<details>
  <summary>Answer!</summary>

  ```java
  double interest = 1.07;
  int years = 0;
  double savings = 1000;

  while (savings < 1000000) {
    savings += 6000;
    years++;
    savings *= interest;
  }

  System.out.println("Time to retire! You retired in " + years + " years.");
  System.out.println("You have $" + savings + " in savings.");
  ```
</details>

---

5. Use whatever loop you want to figure out how many years it'll take for a two-dollar candy bar to cost more than ten dollars with a five percent inflation rate.

<details>
  <summary>Answer!</summary>

  ```java
  int years = 0;

  for (double candyBar = 2.0; candyBar < 10.0; candyBar *= 1.05) {
    years++;
  }

  System.out.println(years);
  ```

  ```java
  while (candyBar < 10.0) {
    candyBar *= 1.05;
    years++;
  }

  System.out.println(years);
  ```
</details>

---

## Arrays
Arrays allow you to store sequential data. Here's how they look syntactically.

```
<datatype>[] <varName> = new <datatype>[<length>];
```

Sometimes you don't need to specify the size of the array if you immediately declare its contents.

```java
char[] varName = {'x', 'y', 'z', 'f'}; 
```

Remember that the first element in an array is at the zero index, i.e. look below.

```java
char[] name = {'J', 'a', 'c', 'k', 'i', 'e'};
System.out.println("The first letter is: " + name[0]);
```

1. Initialze a boolean array that stores seven values.
2. Set the last value in the above array to `true`.
3. Print out the first value in the array.
4. Use a loop to print out all the values of that array.

<details>
  <summary>Answer!</summary>

  ```java
  boolean[] solution = new boolean[7];
  solution[6] = true;
  // solution[solution.length - 1] = true; // This works too.
  System.out.println("First value is: " + solution[0]);

  // Should remember this pattern.
  for (int i = 0; i < solution.length; i++) {
    System.out.println(solution[i]);
  }
  ```
</details>

---

5. Initialize a char array with four elements and set the four elements to be the first four letters of your name (lowercase). If you don't have enough letters, just make stuff up.
6. Use a loop to go through each element in the array and print it if it's the letter 'a'. If so, then print `"Found an 'a'!"`.

<details>
  <summary>Answer!</summary>

  ```java
  char[] letters = {'j', 'a', 'c', 'k'};
  for (int i = 0; i < letters.length; i++) {
    if (letters[i] == 'a') {
      System.out.println("Found an 'a'!");
    }
  }
  ```
</details>

---

## Functions

Functions are awesome. They allow us to write reusable code. Functions are called and they usually have inputs, called parameters, and outputs—don't believe there's a word, but I'd just call them return values. In Java, you need to specify the return type as well as the types for all the parameters, if any.

Here's an example of a function.

```java
boolean youAreYoung(int age) {
  if (age < 30) {
    System.out.println("You are young!");
    return true;
  }

  return false;
}
```

Here, we have a function called `youAreYoung()` that has one parameter, `int age`. Within the function is the code and it will either return `true` or `false`based on the value of the parameter. You can tell it returns a boolean by the `boolean` keyword on the first line.

1. Fill out the function below by summing up all the prices contained in `prices` and apply a sales tax of six percent before returning the total. Print out the total after you call it with the declared `prices` array.

```java
<blank> calculateTotal(double[] prices) {
  <your code>;

  return <blank>;
}

double prices[] = {5.64, 4.99, 13.68};
System.out.println("Your total is: " + calculateTotal(prices));
```

<details>
  <summary>Answer!</summary>

  ```java
  double calculateTotal(double[] prices) {
    double total = 0;
    
    for (int i = 0; i < prices.length; i++) {
      total += prices[i];
    }
    
    return total * 1.05;
  }

  double[] prices = {5.64, 4.99, 13.68};
  System.out.println("Your total is: " + calculateTotal(prices));
  ```
</details>

---

2. Write a function that will return the absolute value of a `double`. The absolute value of a number is its distance to zero.

<details>
  <summary>Answer!</summary>

  ```java
  double absoluteValue(double value) {
    if (value < 0) {
      return value * -1;
    }

    return value;
  }
  ```
</details>

---

3. Fill out the following function template. It will only return true if all the parameters are true.

```
<blank> readyForQuiz(<blank> studied, <blank> sleptWell) {
  <code>
}
```

<details>
  <summary>Answer!</summary>

  ```java
  boolean readyForQuiz(boolean studied, boolean sleptWell) {
    return studied && sleptWell;
  }
  ```
</details>