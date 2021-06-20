# Quiz 1: Variables and Conditionals

Practice problems here will try and assess your ability to:

* Declare Java variables: `int`, `double`, `char`, `boolean`.
* Use operations on said variables and know the outcome without running the code.
* Know the difference between a conditional expression and a conditional statement.
* Be able to evaluate a conditional expression/statements without running the code.
* Use conditional expressions/statements to write coherent, productive code.

A good place to run some of the code is on the [home page](https://cs125.cs.illinois.edu/). Some of these questions are copied from CS 199: Even More Practice (EMP) from Spring '21, source is [here](https://cs199emp.netlify.app/).

## Declaring Variables

The lesson on [Variable and Types](https://cs125.cs.illinois.edu/lessons/Summer2021/001_variablesandtypes#declaration-and-initialization) introduced you to four different variable types: `int`, `double`, `boolean`, `char`.

1. What do these variables store? Can you think of a real-life example of when you want to use each of these variables?

<details>
  <summary>Answer!</summary>

  * `int` means integer! That means they store integers. You can use `int` variables to store the number of students in a Zoom call or in a course during registration.

  * `double` stores floating point numbers, just like `float`. The reason why we use `double` instead of `float` is because `double` as *double* the number of bits to represent a floating point number giving it more precision. You can use `double` to store the temperature outside or coordinates on a plane.

  * `boolean` stores boolean values, i.e. `true` or `false`. (Not necessary to know, but the variable is named after [George Boole](https://en.wikipedia.org/wiki/George_Boole)) You can use `boolean` to store whether someone is logged in successfully into a website.

  * `char` stores characters as the name hints. You can use it to store the letter grade you get out of this course!
</details>

---

Reminder that variable declarations have three parts: (1) the data type, (2) the variable name, and (3) the assignment which is optional. Below is not valid code, it's just there to demonstrate the components described above.

```
<data type> <variable name> = <value>;
```

What is the data type for these variables:

2. `int studentsInCall = 13;`
3. `char letterGrade = 'A';`
4. `boolean CSIsAwesome = true;`
5. What makes a good variable name?
6. What happens with the code below?

```java
double temperature;
System.out.println(temperature); // does it print 0.0? does it even run?
```

<details>
  <summary>Answer!</summary>

  2. The data type is `int`.
  3. The data type is `char`.
  4. The data type is `boolean`.
  5. Good variable names describe what it's used for, e.g. `int songsRemaining = 5;`. Good variables should be camel-cased (at least for this course) and are *not* single letters.
  6. The code does not run because the variable has not been declared.
</details>

---

7. What does this piece of code do? Why?

```java
char foo = 54;
System.out.println(foo);
// does it print out 54? does it even run?
// no worries if you don't know what exactly it prints out.
```

<details>
  <summary>Answer!</summary>

  7. It prints out `6`, the character not the number. That's because `54` on the [ASCII table](http://www.asciitable.com/) is the character `6`.
</details>

---

8. Declare a variable called `firstLetter` with the first *letter* of your name.
9. Declare a variable `hadGoodSleep` that is `true` if you had good sleep, and `false` otherwise.
10. Declare a variable `minimumGPA` that is the minimum GPA for your program.
11. Declare a variable `mealsPerDay` with the number of meals you eat per day.

Hint: You'll need to use `int`, `double`, `boolean`, and `char` only once in some order.

<details>
  <summary>Answer!</summary>

  8. `char firstLetter = 'J';`
  9. `boolean hadGoodSleep = true;`
  10. `double minimumGPA = 3.5;`
  11. `int mealsPerDay = 3;`
</details>

---

## Operations on Variables

Here are some operations you should be familiar with by now: `+`, `-`, `/`, `*`, `++`, `--`, `+=`, `-=`, `/=`, `*=` and `!`. You should also know what data types they work on.

What do these pieces of code output?

1.
```java
int giesStudents = 34;
int graingerStudents = 56;
graingerStudents = graingerStudents + 10;
int totalStudents = giesStudents + graingerStudents;
System.out.println(totalStudents);
```
2.
```java
int songsInPlaylist = 21;
System.out.println(songsInPlaylist / 4);
```

3.
```java
double half = 0.5;
int cakes = 3 * 0.5;
System.out.println(cakes);
```

4.
```java
boolean itIsHotOutside = true;
itIsHotOutside = !itIsHotOutside;
System.out.println(itIsHotOutside);
```

5.
```java
int picturesOfCats = 12;
int picturesOfDogs = 3;
int picturesOfCats += picturesOfDogs;
System.out.println(picturesOfCats);
```

<details>
  <summary>Answer!</summary>

  1. Prints `100`.
  2. Prints `5`.
  3. Does not run because `int` cannot store floating point numbers.
  4.  Prints `false` because `!` means *not* and `itIsHotOutside` gets reassigned to *not* `itIsHotOutside`.
  5.  Doesn't run because `picturesOfCats` gets declared twice.
</details>

---

Let's track the number of people on the Zoom call.

6. Declare a variable `peopleInZoom` that is equal to the number of people in this Zoom call.
7. On the next line, increment `peopleInZoom` by one using `++`.
8. On the next line, add `7` to the variable `peopleInZoom` using `+=`.

<details>
  <summary>Answer!</summary>

  ```java
  int peopleInZoom = 15;
  peopleInZoom++;
  peopleInZoom += 7;
  System.out.println(peopleInZoom);
  ```
</details>

---

Practice with some negation.

9. Declare a boolean called `drankWater` if you have drank water today.
10. Reassign `drankWater` with the opposite value of `drankWater` using `!`.

<details>
  <summary>Answer!</summary>

  ```java
  boolean drankWater = true;
  drankWater = !drankWater;
  System.out.println(drankWater);
  ```
</details>

---

## Conditional Expressions and Statements

Reminder, these are some of the operations you should be familiar with: `&&`, `||`, `!`, `==`.

1. What's the difference between a conditional expression and a conditional statement?

<details>
  <summary>Hint!</summary>

  One of these is an expression, one of these is a statement.

  ```java
  // This is a conditional ___?
  boolean readyForDate = showered && placedDeodorant && dressedUp;
  // This is a conditional ___?
  if (readyForDate) {
    // Code to call your date.
  }
  ```
</details>

<details>
  <summary>Answer!</summary>

  A conditial expression is code that will either evaluate to `true` or `false`. Conditional expressions are like questions. For the hint, the question is: "Have you showered *and* placed deodorant *and* dressed up?" Each of those boolean: `showered`, `placedDeodorant`, and `dressedUp` will have boolean values (`true` or `false`) that will be used to evaluate whether `readyForDate` is `true` or `false`.

  A conditional statement, on the other hand, *uses* a conditional expression and based on the value of that conditional expression will execute another piece of code. These are otherwise known as if-statements. In the hint, it says: "If you're `readyForDate`, then call your date."
</details>

---

2. Consider the code below and answer the questions proposed.

```java
double mealCost = 3.75 + 8.66;
mealCost *= 1.08;
boolean mealIsExpensive = mealCost > 10.0; // is this an expression or statement?

if (mealIsExpensive) { // is this an expression or statement?
    System.out.println("I'll put that on my business card!");
    // will the print statement execute?
}

// Note: The above is the same as.

if (mealIsExpensive == true) {
    System.out.println("I'll put that on my business card!");
}

if (mealCost > 10.0) {
    System.out.println("I'll put that on my business card!");
}
```

<details>
  <summary>Answer!</summary>

  For the first question, it is a conditional expression that will evaluate to `true` because the `mealCost` is greater than `10.0`.

  For the second question, that is a conditional statement because it's an if-statement.

  For the third question, the print statement will execute because the meal is expensive, i.e. `mealIsExpensive` is `true`.
</details>

---

3. Declare a variable `myAge` that contains your age.
4. Declare a variable called `canBuyAlcohol` that is true when `myAge` is greater or equal to `21` and false otherwise.
5. Write a conditional statement that prints "Get out of my store!" if `canBuyAlcohol` is false. Reminder that `!` is the negation operator.
6. Add an else statement to the if statement that prints "What can I help you with?". When will this print?


If-else statements look like.
```
if (<expression>) {
    <code to execute if expression is true>;
} else {
    <code to be execute if otherwise>;
}
```

<details>
  <summary>Answer!</summary>

  ```java
  int myAge = 23;
  boolean canBuyAlcohol = myAge >= 21;
  
  if (!canBuyAlcohol) {
    System.out.println("Get out of my store!");
  } else {
    System.out.println("What can I help you with?");
  }
  ```
</details>

---

7. I was writing code late on night, as usual, and wrote this. There's an error here, where is it?

```java
int twitterFollowers = 100;

if (twitterFollowers > 1000) {
  System.out.println("Wow, you're very popular!");
} else if (twitterFollowers = 0) {
  System.out.println("You got no friends!");
} else {
  System.out.println("Time to buy some followers!");
}
```

<details>
  <summary>Answer!</summary>

  The error is from `twitterFollowers = 0` because the `=` operator, known as the *assignment* operator, is different than the `==` operator, known as the equality operator. I should've used the `==` to check if both values on the left and right side are equal to each other.
</details>

---

## Blocks and Scope

1. What does the code below do? And why?

```java
boolean isHalloween = true;

if (isHalloween) {
  System.out.println("Here is some candy!");
  int candy = 4;
}

System.out.println(candy);
```

<details>
  <summary>Answer!</summary>

  The code doesn't run because variables only exist in the block that they were declared. The variable `candy` was declared within the conditional statement block—we know this because of the curly brackets. Thus, once we leave those curly brackets the variable candy no longer exists and cannot be called anymore.
</details>