# Exam 2: Data Structures and Algorithms

Here's a list of the content I would focus on for the exam. *Keep in mind that all the content in this course is fair game, but we will be focusing on the content we've learned recently [[Geoff's words](https://cs125-forum.cs.illinois.edu/t/exam-2/37183/2?u=jackiec3)].*

## Data Structures

In this course we've learned about these data structures (and their respective implementations):
* Lists
    * Array Lists
    * Linked Lists
* Maps
    * Hash Maps
* Trees
    * Binary Trees

1. Given the root node of a binary tree, return the sum for all values that fall within a range given, inclusive. You will be implementing `rangeSum` in the class `BinaryTreeOperations`.

```java
public class TreeNode {
  
  private int val;
  private TreeNode left;
  private TreeNode right;
  
  TreeNode() { }
  
  TreeNode(int setVal) { 
    this.val = setVal; 
  }
  
  TreeNode(int setVal, TreeNode setLeft, TreeNode setRight) {
    this.val = setVal;
    this.left = setLeft;
    this.right = setRight;
  }
  
  TreeNode getRight() {
    return right; 
  }
  
  TreeNode getLeft() {
    return left; 
  }
  
  int getValue() {
    return val; 
  }
  
}

public class BinaryTreeOperations {
  public static int rangeSum(TreeNode root, int low, int high) {
    // write your code here 
  }
}

// Test cases.
TreeNode b = new TreeNode(1, null, null);
TreeNode c = new TreeNode(3, null, null);
TreeNode a = new TreeNode(2, b, c);
BinaryTreeOperations ops = new BinaryTreeOperations();
System.out.println(ops.rangeSum(a, 1, 3)); // should print 6
System.out.println(ops.rangeSum(a, 5, 8)); // should print 0 
```

----------

2. Convert the linked list class below so that it's a cycle! I.e. the end node should be pointing to the beginning. Additionally, write a `toStringCycle()` function that takes an integer and prints the values in the cycle `n` times.

```java
public class LinkedList {
  
  public Item start;
  public int length;
  
  LinkedList() {
    this.start = null;
    this.length = 0;
  }
  
  public class Item {
    public int value;
    public Item next;
    
    Item(int setValue, Item setNext) {
      this.value = setValue;
      this.next = setNext;
    }
  }
  
  public void add(int value, int index) {
    assert index >= 0 && index <= this.length;
    int step = 1;
    
    if (index == 0) {

      this.start = new Item(value, this.start);

    } else {

      for (Item i = this.start; i != null; i = i.next) {
        if (index == step) {
          Item addition = new Item(value, i.next);
          i.next = addition;
        }
        step++;
      }

    }

    this.length++;
  }
  
  @Override
  public String toString() {
    String buffer = "";
    
    for (Item i = this.start; i != null; i = i.next) {
      buffer += i.value + " -> ";
    }
    
    return buffer + "null";
  }
  
  public String toStringCycle(int n) {
    return "";
  }
  
}

// Test case for cyclical implementation.
LinkedList ls = new LinkedList();
ls.add(1, 0);
ls.add(2, 0);
ls.add(3, 0);
System.out.println(ls);
System.out.println(ls.start);
// If correct, should print the same String as above.
System.out.println(ls.start.next.next.next);

// Test case for cyclical print.
System.out.println(ls.toStringCycle(3));
// Should print: 3 -> 2 -> 1 -> 3 -> 2 -> 1 -> ...
```

----------


## Algorithms

We've learned about a variety of sorting algorithms, here's a list of them:
* Bubble Sort
* Selection Sort
* Insertion Sort
* Merge Sort
* Quick Sort

For these sorting algorithms, you should be able to deduce their big-O runtimes, best/worse cases (or even if they have best/worse cases), and major components required to implement them (e.g. quick sort requires partition, merge sort requires a merge function that merges two already sorted arrays).

----------


## Recursion

Recursion is the ability to break down problems into smaller, trivial cases and build up from those trivial cases to solve a larger problem. Classic examples include calculating factorials or Fibonacci numbers.

Additionally, you should know that recursion is very useful for navigating and manipulating linked lists and binary trees due to their recursive nature—i.e. if you take the subtree of a tree, it's still a tree.

1. Add a function that will delete a node in the existing linked list class below. The `deleteNode()` function will take a value to delete from the list and if it doesn't find it, then it will not modify the list.

```java
public class LinkedList {

  private Item start;

  class Item {
    public int value;
    public Item next;
    
    Item(int setValue, Item setNext) {
      this.value = setValue;
      this.next = setNext;
    }
  }
  
  public void add(int s) {
    Item addition = new Item(s, this.start);
    this.start = addition;
  }
  
  @Override
  public String toString() {
    Item i = this.start;
    String output = "";
    
    while (i != null) {
      output += i.value + " -> ";
      i = i.next;
    }
  
    return output + "null";
  }

}

LinkedList ls = new LinkedList();
ls.add(1);
ls.add(3);
ls.add(4);
System.out.println(ls.toString()); // should print 4 -> 3 -> 1 -> null
ls.deleteNode(1);
System.out.println(ls.toString()); // should print 4 -> 3 -> null
ls.deleteNode(5);
System.out.println(ls.toString()); // should print 4 -> 3 -> null
```

----------
