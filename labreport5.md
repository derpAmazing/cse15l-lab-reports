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

But it still doesn't work. I'm still failing the public tests! I suspect maybe it's an error in my logic and I'm missing some sort of variable assignment or doing it wrong?

## TA Response

Hi there,

Consider what an empty LinkedList should look like. What should happen when you try to iterate through an empty LinkedList. How would an iterator iterate through it?

Good luck!

## Student Response

Hi, I've finally found the problem. Thank you for the advice on thinking about iterating through it! I realized that in an empty list, I need to set the next pointer for the head and the previous pointer for the tail to each other in order to properly iterate through them - and also get the "right" structure for the LinkedList. It's a problem in my logic, and I've passed the tests! Here is my code:

```
public void clear() {
    this.head.next = this.tail;
    this.tail.prev = this.head;
    this.size = 0;
}
```

```
public MyLinkedList() {
    Node sentinelHeadNode = new Node(null);
    Node sentinelTailNode = new Node(null);
    this.head = sentinelHeadNode;
    this.tail = sentinelTailNode;
    sentinelHeadNode.setNext(sentinelTailNode);
    sentinelTailNode.setPrev(sentinelHeadNode);
    this.size = 0;
}
```

# Setup Information

## File and Directory Structure
```
pa3-LinkedList/
└── starter/
    └── MyLinkedList.java
    └── MyLinkedListCustomTester.java
    └── MyLinkedListPublicTester.java
└── libs/
    └── hamcrest-2.2.jar
    └── junit-4.13.2.jar
└── README.md
```

## The contents of each file before fixing the bug

Parts of the code that changed are provided above in the conversation (in Edstem it would be inserted code snippets)

## The full command line (or lines) you ran to trigger the bug

I just ran the public tester with:
```
javac -cp ../libs/junit-4.13.2.jar:../libs/hamcrest-2.2.jar:. MyLinkedListPublicTester.java
java -cp ../libs/junit-4.13.2.jar:../libs/hamcrest-2.2.jar:. org.junit.runner.JUnitCore MyLinkedListPublicTester
```

## A description of what to edit to fix the bug

The constructor needs to be edited to add a dummy node at the tail, and then set the next pointer of the head to the tail, and the previous pointer of the tail to the head when initializing.

The clear method needs to change the next pointer of the head node and the previous pointer of the tail node to each other instead of null.

# Part 2 - Reflection

The best thing I learned in the second half of the quarter were about debuggers. I knew about breakpoints and stuff through doing my own projects, but my knowledge on them was very rudimentary and I didn't use them much. I opted to just add temporary statements after the point I wanted, such as printing the value of a variable after a certain line, or printing an indicator to show that a certain if statement ran.

jdb and debuggers seem a lot more convenient to do that now, and I wonder if there's a debugger with a nice, organized interface to debug my program rather than a command line! I'll very likely use some sort of debugger though when I run into a hard problem.


