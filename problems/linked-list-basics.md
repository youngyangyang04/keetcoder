# What You Should Know About Linked Lists!

A linked list is a linear structure in which elements are connected using pointers. Each node consists of two parts: a data field and a pointer field (which stores a pointer to the next node). The pointer field of the last node points to null (meaning a null pointer).

The entry node of a linked list is called the head node or head.

As shown in the figure:
![Linked List 1](https://file1.kamacoder.com/i/algo/20200806194529815.png)

## Types of Linked Lists

Let's discuss the various types of linked lists:

### Singly Linked List

What we just discussed is a singly linked list.

### Doubly Linked List

In a singly linked list, the pointer field can only point to the next node.

Doubly linked list: Each node has two pointer fields, one pointing to the next node and one pointing to the previous node.

A doubly linked list can be traversed in both forward and backward directions.

As shown in the figure:
![Linked List 2](https://file1.kamacoder.com/i/algo/20200806194559317.png)

### Circular Linked List

A circular linked list, as the name suggests, connects the head and tail of the list.

Circular linked lists can be used to solve the Josephus problem.

![Linked List 4](https://file1.kamacoder.com/i/algo/20200806194629603.png)

## Storage Method of Linked Lists

After understanding the types of linked lists, let's talk about how they are stored in memory.

Arrays have continuous distribution in memory, but linked lists do not.

Linked lists are linked in memory nodes by the pointers in the pointer fields.

Therefore, the nodes in a linked list are not continuously distributed in memory but rather dispersed at various addresses depending on the operating system's memory management.

As shown in the figure:

![Linked List 3](https://file1.kamacoder.com/i/algo/20200806194613920.png)

This linked list starts at node 2 and ends at node 7; each node is distributed at different memory address spaces, linked together by pointers.

## Definition of Linked Lists

Next, let's talk about the definition of linked lists.

Many candidates struggle to write the definition of linked list nodes correctly during interviews.

This difficulty arises because while practicing on LeetCode, the node definitions are predefined and can be directly used, so candidates often overlook how a linked list node is defined.

In interviews, when required to write their own linked list, mistakes are often made.

Here is how to define a linked list node in C/C++:

```cpp
// Singly linked list
struct ListNode {
    int val;  // Element stored in the node
    ListNode *next;  // Pointer to the next node
    ListNode(int x) : val(x), next(NULL) {}  // Constructor for the node
};
```

Some may ask, is defining a constructor necessary? The answer is no, as C++ provides a default constructor.

However, this default constructor does not initialize any member variables. Here are two examples:

Initializing a node with a custom constructor:

```cpp
ListNode* head = new ListNode(5);
```

Initializing a node using the default constructor:

```cpp
ListNode* head = new ListNode();
head->val = 5;
```

Therefore, if the default constructor is used without definition, variables cannot be initialized directly during initialization!

## Operations on Linked Lists

### Deleting a Node

To delete node D, as shown in the figure:

![Linked List - Delete Node](https://file1.kamacoder.com/i/algo/20200806195114541-20230310121459257.png)

Simply point the `next` pointer of node C to node E.

However, some might ask, doesn't node D remain in memory? Yes, that's correct, although it is removed from the linked list.

Therefore, in C++, it's best to manually release node D to free that block of memory.

Other languages like Java or Python have their own memory management mechanisms and do not require manual memory release.

### Adding a Node

As shown in the figure:

![Linked List - Add Node](https://file1.kamacoder.com/i/algo/20200806195134331-20230310121503147.png)

We can see that inserting and removing nodes in a linked list are O(1) operations and do not affect other nodes.

However, if the fifth node needs to be deleted, the search must start from the head node to find the fourth node and perform the deletion via the `next` pointer, making the search time complexity O(n).

## Performance Analysis

Let's compare the characteristics of linked lists with arrays, as shown in the figure:

![Linked List - Array Performance Comparison](https://file1.kamacoder.com/i/algo/20200806195200276.png)

When defining an array, its length is fixed, and if you want to change the array's length, you need to define a new array.

The length of a linked list can be dynamic, and nodes can be added or removed easily, making linked lists suitable for scenarios with dynamically changing data sizes, frequent insertions and deletions, and infrequent retrievals.

Now that you've gained sufficient understanding about linked lists, I will discuss high-frequency interview questions on linked lists in future sessions. See you next time!

## Versions in Other Languages

### Java:

```java
public class ListNode {
    // Node value
    int val;

    // Next node
    ListNode next;

    // Node constructor (no parameters)
    public ListNode() {
    }

    // Node constructor (one parameter)
    public ListNode(int val) {
        this.val = val;
    }

    // Node constructor (two parameters)
    public ListNode(int val, ListNode next) {
        this.val = val;
        this.next = next;
    }
}
```

### JavaScript:

```javascript
class ListNode {
  val;
  next = null;
  constructor(value) {
    this.val = value;
    this.next = null;
  }
}
```

### TypeScript:

```typescript
class ListNode {
  public val: number;
  public next: ListNode|null = null;
  constructor(value: number) {
    this.val = value;
    this.next = null;
  }
}
```

### Python:

```python
class ListNode:
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
```

### Go:

```go
type ListNode struct {
    Val int
    Next *ListNode
}
```

### Scala:

```scala
class ListNode(_x: Int = 0, _next: ListNode = null) {
  var next: ListNode = _next
  var x: Int = _x
}
```

### Rust:

```rust
#[derive(PartialEq, Eq, Clone, Debug)]
pub struct ListNode<T> {
    pub val: T,
    pub next: Option<Box<ListNode<T>>>,
}

impl<T> ListNode<T> {
    #[inline]
    fn new(val: T, node: Option<Box<ListNode<T>>>) -> Self {
        ListNode { next: node, val }
    }
}
```

### C:

```c
typedef struct ListNodeT {
    int val;
    struct ListNodeT next;
} ListNode;
```

### C#

```c#
public class Node<T>
{
    // Data stored in the node
    public T Data { get; set; }

    // Reference to the next node
    public Node<T> Next { get; set; }

    // Node constructor to initialize the node
    public Node(T data)
    {
        Data = data;
        Next = null; // Initially no next node, hence set to null
    }
}
```