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

<details>
  <summary>Answer!</summary>

```java
  public static int rangeSum(TreeNode root, int low, int high) {
    
    // Base case.
    if (root == null) {
      return 0;
    }
    
    int sum = 0;
    
    if (low <= root.getValue() && root.getValue() <= high) {
      sum += root.getValue();
    }
    
    sum += rangeSum(root.getLeft(), low, high);
    sum += rangeSum(root.getRight(), low, high);
    
    return sum;
    
  }
```
</details>

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

<details>
  <summary>Answer!</summary>

```java
public class LinkedList {
  
  public Item start;
  public Item end;
  public int length;
  
  LinkedList() {
    this.start = null;
    this.end = null;
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
    
    
    assert index >= 0;
    
    if (this.length == 0) {

      this.start = new Item(value, null);
      this.start.next = this.start;
      this.end = this.start;

    } else if (index == 0) {

      this.start = new Item(value, this.start);
      this.end.next = this.start;

    } else {
      
      int step = 1;
      
      // Taking the remainder is a smarter way to add because you don't
      // have to loop around the cyclical linked list a bunch of times.
      index = index % this.length;

      for (Item i = this.start; i != null; i = i.next) {
        if (index == step) {
          Item addition = new Item(value, i.next);
          i.next = addition;
          break;
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
    int loops = 0;
    String output = "";
    
    for (Item i = this.start; loops < n; i = i.next) {
      
      output += i.value + " -> ";
      
      // Are we at the beginning again?
      if (this.end == i) {
        loops++;
      }
    }
    
    output += "...";
    
    return output;
  }
  
}

LinkedList ls = new LinkedList();
ls.add(1, 0);
ls.add(2, 0);
ls.add(3, 0);
ls.add(4, 28);
System.out.println(ls.toStringCycle(1));
```
</details>

----------


## Algorithms

We've learned about a variety of sorting algorithms, here's a list of them:
* Bubble Sort
* Selection Sort
* Insertion Sort
* Merge Sort
* Quick Sort
* Binary Search (not a sorting algorithm, but a search algorithm)

For these sorting algorithms, you should be able to deduce their big-O runtimes, best/worse cases (or even if they have best/worse cases), and major components required to implement them (e.g. quick sort requires partition, merge sort requires a merge function that merges two already sorted arrays).

1. In merge sort, you need to have a function that is able to merge two already sorted arrays together. Let's add one more array! Your job is to code a `triMerge()` function that merges three already sorted arrays together. *There's probably a way to go about this by zipping together three arrays concurrently, but I'm just going to settle with using the merge function for two arrays as a helper.*

```java
import java.util.Arrays;

int[] merge(int[] first, int[] second) {
  if (first == null || second == null) {
    throw new IllegalArgumentException();
  }
  if (first.length == 0) {
    return second;
  }
  if (second.length == 0) {
    return first;
  }
  int[] merged = new int[first.length + second.length];
  int firstIndex = 0;
  int secondIndex = 0;
  for (int i = 0; i < merged.length; i++) {
    if (firstIndex == first.length) {
      merged[i] = second[secondIndex++];
    } else if (secondIndex == second.length) {
      merged[i] = first[firstIndex++];
    } else if (first[firstIndex] < second[secondIndex]) {
      merged[i] = first[firstIndex++];
    } else {
      merged[i] = second[secondIndex++];
    }
  }
  return merged;
}

int[] triMerge(int[] first, int[] second, int[] third) {
  // Your code here.
  return null;
}

int[] first = new int[]{2, 4, 6};
int[] second = new int[]{1, 3, 5};
int[] third = new int[]{0, 7};

// The final, merged array should be: {0, 1, 2, 3, 4, 5, 6, 7}
int[] merged = triMerge(first, second, third);
System.out.println(Arrays.toString(merged));
```

<details>
  <summary>Answer!</summary>

```java
import java.util.Arrays;

int[] triMerge(int[] first, int[] second, int[] third) {
  
  int[] merged = merge(first, second);
  merged = merge(merged, third);
  
  return merged;
  
}

int[] merge(int[] first, int[] second) {
  if (first == null || second == null) {
    throw new IllegalArgumentException();
  }
  if (first.length == 0) {
    return second;
  }
  if (second.length == 0) {
    return first;
  }
  int[] merged = new int[first.length + second.length];
  int firstIndex = 0;
  int secondIndex = 0;
  for (int i = 0; i < merged.length; i++) {
    if (firstIndex == first.length) {
      merged[i] = second[secondIndex++];
    } else if (secondIndex == second.length) {
      merged[i] = first[firstIndex++];
    } else if (first[firstIndex] < second[secondIndex]) {
      merged[i] = first[firstIndex++];
    } else {
      merged[i] = second[secondIndex++];
    }
  }
  return merged;
}

int[] first = new int[]{2, 4, 6};
int[] second = new int[]{1, 3, 5};
int[] third = new int[]{0, 7};

// The final, merged array should be: {0, 1, 2, 3, 4, 5, 6, 7}
int[] merged = triMerge(first, second, third);
System.out.println(Arrays.toString(merged));
```
</details>

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

<details>
  <summary></summary>

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
  
  public boolean deleteNode(int value) {
    return deleteNodeHelper(value, null, this.start);
  }
  
  private boolean deleteNodeHelper(int value, Item previous, Item item) {
    
    // Base cases:
    //   1. If the list is empty, then we can't delete the value. 
    //    It was unsuccessful, so return false.
    //   2. If the value is here, then delete!
    if (item == null) {
      return false;
      
    } else if (item.value == value) {
      // When previous is null, then we're at the beginning of the list.
      if (previous == null) {
        this.start = item.next;
      } else {
        previous.next = item.next;
      }
      
      return true;
      
    } else {
      // Recursive case: Delete the same value from the rest of the list.
      return deleteNodeHelper(value, item, item.next);
    }
  }

}

LinkedList ls = new LinkedList();
ls.add(1);
ls.add(3);
ls.add(4);
System.out.println(ls.toString()); // should print 4 -> 3 -> 1 -> null
ls.deleteNode(1);
System.out.println(ls.toString()); // should print 4 -> 3 -> null
System.out.println(ls.deleteNode(5));
System.out.println(ls.toString()); // should print 4 -> 3 -> null
```
</details>

----------
