# Algorithm

> This repo is an **organized collection** of resources to help you learn algorithm.

[Data Structures](#data-structures)


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


## Resources

* [Data Science Tutorials](https://www.topcoder.com/community/data-science/data-science-tutorials/)