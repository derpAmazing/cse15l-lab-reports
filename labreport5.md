# Original Edstem Post

## Title: My LinkedList clear() method somehow fails!

Hi everyone. My LinkedList clear() method is failing the public tests provided for the Programming Assignment. It really should be a *very* simple method, but I can't seem to wrap my head around why it doesn't work. Here is the clear() method code:

```
public void clear() {
    this.head.next = null;
    this.size = 0;
}
```

I suspect there might be an issue with the structure of my LinkedList, but I'm really not sure! Here is the code of my constructor:


```
public MyLinkedList() {
        Node sentinelHeadNode = new Node(null);
        this.head = sentinelHeadNode;
        this.size = 0;
}
```

# Continuing Conversation

## TA Response

Hi there,

Thanks for reaching out! I suggest you try to think about the type of LinkedList you're being asked to create in the PA and what basic structure you need to initialize. Reading through the write-up and the PA description should be helpful! Try to use jdb in a bash script to debug what your LinkedList looks like when you initialize it!

Good luck!

## Student Response

Hi again. I wrote a temporary main method that creates a LinkedList, inserts a few nodes, and I also wrote a bash script to sort-of visualilze what my LinkedList looks like.

```
javac *.java

jdb MainMethod <<EOF
run
locals
print linkedList
print linkedList.head
print linkedList.head.next
```

I see that I've misunderstood the type of LinkedList I was directed to create - I created a LinkedList with one dummy node at the head when I was supposed to make two dummy nodes, one at the head, and one at the tail. I've changed my constructor to this:

```
public MyLinkedList() {
        Node sentinelHeadNode = new Node(null);
        Node sentinelTailNode = new Node(null);
        this.head = sentinelHeadNode;
        this.tail = sentinelTailNode;
        this.size = 0;
}
```

And my clear method now looks like this:

```
public void clear() {
    this.head.next = null;
    this.tail.next = null;
    this.size = 0;
}
```

But it still doesn't work. I'm still failing the public tests!
