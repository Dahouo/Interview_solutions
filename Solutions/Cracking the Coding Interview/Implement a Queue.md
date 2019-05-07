### Provided code

Let's assume we're given the following `Node` class, with variables marked `public` for simplicity.

```java
class Node {
    public Node next;
    public int data ;
    public Node(int d) {
      next = null;
      data = d;
    }
}
```

### Solution

```java
class Queue {
    private Node head = null;
    private Node tail = null;

    public void enqueue(int data) {
        Node n = new Node(data);
        if (head == null) {
            head = n;
            tail = n;
        } else {
            tail.next = n;
            tail = n;
        }
    }

    public Node dequeue() {
        if (head == null) {
            return null;
        }
        Node front = head;
        head = head.next;
        if (head == null) {
            tail = null;
        }
        front.next = null; // rips the Node from the Queue
        return front;
    }

    public Node peek() {
        return head;
    }
}
```
