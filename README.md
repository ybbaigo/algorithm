# Algorithm

@(topic)


> This repo is an **organized collection** of resources to help you learn algorithm.

* [Data Structures](#data-structures)
* [Sorting](#sorting)


## Data Structures

**Arrays**, a very simple data structure, and may be thought of as a list of a fixed length. Arrays are nice because of their simplicity, and are well suited for situations where the number of data items is known (or can be programmatically determined).

**Linked Lists**, a data structure that can hold an arbitrary number of data items, and can easily change size to add or remove items. A linked list, at its simplest, is a pointer to a data node. Each data node is then composed of data (possibly a record with several data values), and a pointer to the next node. At the end of the list, the pointer is set to null.

A typical linked list implementation would have code that defines a node, and looks something like this:
```java
class ListNode {
    String data;
    ListNode nextNode;
}
ListNode firstNode;
```

You could then write a method to add new nodes by inserting them at the beginning of the list:
```java
ListNode newNode = new ListNode();
NewNode.nextNode = firstNode;
firstNode = newNode;

Iterating through all of the items in the list is a simple task:

ListNode curNode = firstNode;
while (curNode != null) {
    ProcessData(curNode);
    curNode = curNode.nextNode;
}
```

**Queues**, a data structure that is best described as "first in, first out". A real world example of a queue is people waiting in line at the bank. As each person enters the bank, he or she is "enqueued" at the back of the line. When a teller becomes available, they are "dequeued" at the front of the line.

For instance, if you know that you are trying to get from point A to point B on a 50×50 grid, and have determined that the direction you are facing (or any other details) are not relevant, then you know that there are no more than 2,500 "states" to visit. Thus, your queue is programmed like so:

```java
class StateNode {
    int xPos;
    int yPos;
    int moveCount;
}

class MyQueue {
    StateNode[] queueData = new StateNode[2500];
    int queueFront = 0;
    int queueBack = 0;

    void Enqueue(StateNode node) {
        queueData[queueBack] = node;
        queueBack++;
    }

    StateNode Dequeue() {
        StateNode returnValue = null;
        if (queueBack > queueFront) {
            returnValue = queueData[queueFront];
            QueueFront++;
        }
        return returnValue;
    }

    boolean isNotEmpty() {
        return (queueBack > queueFront);
    }
}
```

Then, the main code of your solution looks something like this.

```java
MyQueue queue = new MyQueue();
queue.Enqueue(initialState);
while (queue.isNotEmpty()) {
    StateNode curState = queue.Dequeue();
    if (curState == destState)
        return curState.moveCount;
    for (int dir = 0; dir < 3; dir++) {
        if (CanMove(curState, dir))
            queue.Enqueue(MoveState(curState, dir));
    }
}
```
**Stacks**, the opposite of queues, in that they are described as "last in, first out". The classic example is the pile of plates at the local buffet. The workers can continue to add clean plates to the stack indefinitely, but every time, a visitor will remove from the stack the top plate, which is the last one that was added.

**Trees**, a data structure consisting of one or more data nodes. The first node is called the "root", and each node has zero or more "child nodes". The maximum number of children of a single node, and the maximum depth of children are limited in some cases by the exact type of data represented by the tree.

**Binary Trees**, a special type of tree is a binary tree. A binary tree also happens to be one of the most efficient ways to store and read a set of records that can be indexed by a key value in some way. The idea behind a binary tree is that each node has, at most, two children.

**Priority Queues**, a priority queue accepts states, and internally stores them in a method such that it can quickly pull out the state that has the least cost.

**Hash Tables**, a unique data structure, and are typically used to implement a "dictionary" interface, whereby a set of keys each has an associated value. The key is used as an index to locate the associated values. This is not unlike a classical dictionary, where someone can find a definition (value) of a given word (key).


##### Source(s) and further reading

* [Data Structures](https://www.topcoder.com/community/data-science/data-science-tutorials/data-structures/)

## Sorting

When comparing various sorting algorithms, there are several things to consider. The first is usually runtime. A second consideration is memory space. A third consideration is stability. Stability, simply defined, is what happens to elements that are comparatively the same. In a stable sort, those elements whose comparison key is the same will remain in the same relative order after sorting as they were before sorting. In an unstable sort, no guarantee is made as to the relative output order of those elements whose sort key is the same.

**Bubble Sort**, The idea is to pass through the data from one end to the other, and swap two adjacent elements whenever the first is greater than the last. This is O(n^2) runtime, and hence is very slow for large data sets.

```cpp
for (int i = 0; i < data.Length; i++)
   for (int j = 0; j < data.Length - 1; j++)
      if (data[j] > data[j + 1])
      {
         tmp = data[j];
         data[j] = data[j + 1];
         data[j + 1] = tmp;
      }
```

**Insertion Sort**, an algorithm that seeks to sort a list one element at a time. One of the principal advantages of the insertion sort is that it works very efficiently for lists that are nearly sorted initially. Furthermore, it can also work on data sets that are constantly being added to.
```cpp
for (int i = 0; i <= data.Length; i++) {
   int j = i;
   while (j > 0 && data[i] < data[j - 1])
      j--;
   int tmp = data[i];
   for (int k = i; k > j; k--)
      data[k] = data[k - 1];
   data[j] = tmp;
}
```

**Merge Sort**, A merge sort works recursively. First it divides a data set in half, and sorts each half separately. Next, the first elements from each of the two lists are compared. The lesser element is then removed from its list and added to the final result list. The runtime of this algorithm is O(n * log n)
```cpp
int[] mergeSort (int[] data) {
   if (data.Length == 1)
      return data;
   int middle = data.Length / 2;
   int[] left = mergeSort(subArray(data, 0, middle - 1));
   int[] right = mergeSort(subArray(data, middle, data.Length - 1));
   int[] result = new int[data.Length];
   int dPtr = 0;
   int lPtr = 0;
   int rPtr = 0;
   while (dPtr < data.Length) {
      if (lPtr == left.Length) {
         result[dPtr] = right[rPtr];
         rPtr++;         
      } else if (rPtr == right.Length) {
         result[dPtr] = left[lPtr];
         lPtr++;
      } else if (left[lPtr] < right[rPtr]) {
         result[dPtr] = left[lPtr];
         lPtr++;
      } else {
         result[dPtr] = right[rPtr];
         rPtr++;         
      }
      dPtr++;
   }
   return result;
}
```

**Heap Sort**, we create a heap data structure. A heap is a data structure that stores data in a tree such that the smallest (or largest) element is always the root node. The runtime of a heap sort has an upper bound of O(n * log n).

```java
Heap h = new Heap();
for (int i = 0; i < data.Length; i++)
   h.Add(data[i]);
int[] result = new int[data.Length];
for (int i = 0; i < data.Length; i++)
   data[i] = h.RemoveLowest();
```

**Quick Sort**, First, divide the data into two groups of “high” values and “low” values. Then, recursively process the two halves. Finally, reassemble the now sorted list. In a best case, the runtime is O(n * log n). In the worst case-where one of the two groups always has only a single element-the runtime drops to O(n^2).

```java
Array quickSort(Array data) {
   if (Array.Length <= 1)
      return;
   middle = Array[Array.Length / 2];
   Array left = new Array();
   Array right = new Array();
   for (int i = 0; i < Array.Length; i++)
      if (i != Array.Length / 2) {
         if (Array[i] <= middle)
            left.Add(Array[i]);
         else
            right.Add(Array[i]);
      }
   return concatenate(quickSort(left), middle, quickSort(right));
}
```

**Radix Sort**, The radix sort was designed originally to sort data without having to directly compare elements to each other. A radix sort first takes the least-significant digit (or several digits, or bits), and places the values into buckets. If we took 4 bits at a time, we would need 16 buckets. We then put the list back together, and have a resulting list that is sorted by the least significant radix. We then do the same process, this time using the second-least significant radix. We lather, rinse, and repeat, until we get to the most significant radix, at which point the final result is a properly sorted list.

For example, let’s look at a list of numbers and do a radix sort using a 1-bit radix. Notice that it takes us 4 steps to get our final result, and that on each step we setup exactly two buckets:

> {6, 9, 1, 4, 15, 12, 5, 6, 7, 11}
> {6, 4, 12, 6} {9, 1, 15, 5, 7, 11}
> {4, 12, 9, 1, 5} {6, 6, 15, 7, 11}
> {9, 1, 11} {4, 12, 5, 6, 6, 15, 7}
> {1, 4, 5, 6, 6, 7} {9, 11, 12, 15}

Radix sort visualization
https://www.cs.usfca.edu/~galles/visualization/RadixSort.html

##### Source(s) and further reading

* [Sorting](https://www.topcoder.com/community/data-science/data-science-tutorials/sorting/)
* [Radix Sort Visualization](https://www.cs.usfca.edu/~galles/visualization/RadixSort.html)
