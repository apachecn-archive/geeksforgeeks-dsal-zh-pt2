# 如何创建可折叠堆栈？

> 原文:[https://www.geeksforgeeks.org/create-mergable-stack/](https://www.geeksforgeeks.org/create-mergable-stack/)

使用以下操作设计堆栈。

a) push(Stack s，x):向 stack s
添加项 x b)pop(Stack s):从 stack s
中移除顶部项 c)合并(Stack s1，Stack s2):将 s2 的内容合并到 s1 中。

上述所有操作的时间复杂度应为 0(1)。
如果我们**使用数组**实现堆栈，那么合并是不可能在 O(1)时间内完成的因为我们要做以下步骤。
a)删除旧数组。
b)为 s1 创建一个新数组，其大小等于 s1 的旧数组加上 s2 的大小。
c)将 s1 和 s2 的旧内容复制到 s1 的新数组中
上述操作需要 O(n)个时间。

我们可以使用一个带有两个指针的[](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)**链表，一个指针指向第一个节点(从开始添加和删除元素时也用作顶部)。最后一个节点需要另一个指针，这样我们就可以在 s1 的末尾快速链接 s2 的链表。以下是所有操作。
a) push():使用第一个指针在链表开头添加新项。
b) pop():使用第一个指针从开头移除一个项目。
c) merge():将第一个指针链接到第二个堆栈，作为第一个列表的最后一个指针的下一个。
*如果不允许我们使用*一个*额外的指针，我们能做到吗？*
我们可以用 [**循环链表**](https://www.geeksforgeeks.org/circular-linked-list/) 来做。其思想是跟踪链表中的最后一个节点。最后一个节点的下一个表示堆栈的顶部。
a) push():添加新项作为最后一个节点的下一个。**

**b) pop():移除最后一个节点的下一个。
c) merge():将第二个列表的顶部(倒数第二个)链接到第一个列表的顶部(倒数第二个)。并使第二个列表的最后一个成为整个列表的最后一个。
本文由**拉胡尔·古普塔**供稿。如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论**

**上述代码如下所示:**

## **C++**

```
#include <iostream>
using namespace std;

class node {
public:
    int data;
    node* next;
};

class mystack {
public:
    node* head;
    node* tail;

    mystack()
    {
        head = NULL;
        tail = NULL;
    }
};

mystack* create()
{
    mystack* ms = new mystack(); // creating a new stack
    return ms;
}

void push(int data, mystack* ms)
{
    node* temp = new node();
    temp->data = data;
    temp->next = ms->head;

    // when pushing first element in the stack the tail
    // must be pointed by that first element
    if (ms->head == NULL)
        ms->tail = temp;

    ms->head = temp;
}

int pop(mystack* ms)
{
    if (ms->head == NULL) {
        cout << "stack underflow" << endl;
        return 0;
    }
    else {
        node* temp = ms->head;
        ms->head = ms->head->next;
        int popped = temp->data;
        delete temp;
        return popped;
    }
}

// making the next pointer of tail of
// one stack point to other stack
void merge(mystack* ms1, mystack* ms2)
{
if (ms1->head == NULL)
{
    ms1->head = ms2->head;
    ms1->tail = ms2->tail;
    return;
}

ms1->tail->next = ms2->head;
ms1->tail = ms2->tail;
}

void display(mystack* ms)
{
    node* temp = ms->head;
    while (temp != NULL) {
        cout << temp->data << " ";
        temp = temp->next;
    }
}

int main()
{
    mystack* ms1 = create();
    mystack* ms2 = create();

    push(6, ms1);
    push(5, ms1);
    push(4, ms1);
    push(9, ms2);
    push(8, ms2);
    push(7, ms2);
    merge(ms1, ms2);
    display(ms1);
}

// This code is contributed by jayshmi
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
import java.io.*;

// The class Node contains the
// structure of our Node of
// the linked list
class Node
{
    Node next;
    Node prev;
    int data;

    // Create a node with the
    // given value
    Node(int value)
    {
        data = value;
        next = null;
        prev = null;
    }
}

class Stack{

private Node head;
private Node tail;

// Initialize stack class
// with its head and tail as null
Stack()
{
    head = null;
    tail = null;
}

public void push(int value)
{
    Node newNode = new Node(value);
    if(head == null)
    {
        head = newNode;
        head.next=null;
        head.prev = null;
        tail = newNode;
    }
    else
    {
        newNode.prev = tail;
        tail.next = newNode;
        tail = newNode;
    }
}

public void pop()
{
    if(head == null)
        System.out.println("stack underflow");

    if(head == tail)
    {
        head = null;
        tail = null;
    }
    else
    {
        Node n = tail;
        tail = tail.prev;
        n.prev = null;
        tail.next = null;
    }
}

public void merge(Stack s)
{
    head.prev = s.tail;
    s.tail.next = head;
    head = s.head;
    s.tail = null;
    s.head = null;
}

public void display()
{
    if(tail != null)
    {
        Node n = tail;
        while(n != null)
        {
            System.out.print(n.data + " ");
            n = n.prev;
        }
        System.out.println();
    }
    else
    {
        System.out.println("Stack Underflow");
    }
}
}

class GFG{
public static void main (String[] args)
{
    Stack ms1 = new Stack();
    Stack ms2 = new Stack();

    ms1.push(6);
    ms1.push(5);
    ms1.push(4);
    ms2.push(9);
    ms2.push(8);
    ms2.push(7);

    ms1.merge(ms2);
    ms1.display();
}
}

// This code is contributed by Ayaan
```

## **蟒蛇 3**

```
# The Node class for Linked List
class Node():
    def __init__(self,data):

        self.next = None
        self.prev = None
        self.data = data

class Stack():

    # Initialize stack class with
    # its head and tail as None
    def __init__(self):

        self.head = None
        self.tail = None

    def push(self, data):

        new_node = Node(data)

        if (self.head == None):
            self.head = new_node
            self.head.next= None
            self.head.prev = None
            self.tail = new_node

        else:
            new_node.prev = self.tail
            self.tail.next = new_node
            self.tail = new_node

    def pop(self):

        if (self.head == None):
            print("Stack underflow")

        if (self.head == self.tail):
            self.head = None
            self.tail = None

        else:
            node = self.tail
            self.tail = self.tail.prev
            del node
            self.tail.next = None

    # self (stack) is linked on top (which is tail here) of stack
    # self becomes the merged stack
    def merge(self, stack):
        if stack.head == None: return  # if stack is empty self stays as it is
        if self.head == None:        # self (stack) is empty -> point to stack
            self.head = stack.head
            self.tail = stack.tail
            return
        self.head.prev = stack.tail # link self on top of stack
        stack.tail.nxt = self.head
        self.head = stack.head      # set new head for self (stack)

    def display(self):

        if (self.tail != None):
            n = self.tail

            while (n != None):
                print(n.data, end = " ")
                n = n.prev

            print()

        else:
            print("Stack Underflow")

# Driver code
ms1 = Stack()
ms2 = Stack()

ms1.push(6)
ms1.push(5)
ms1.push(4)
ms2.push(9)
ms2.push(8)
ms2.push(7)

ms1.merge(ms2)
ms1.display()
while ms1.head != ms1.tail:
  ms1.pop ()
print ("check pop all elements until head == tail (one element left)")
print ("on merged stack: ", end = "")
ms1.display()
# This code is contributed by maheswaripiyush9
```

## **C#**

```
using System;
// The class Node contains the
// structure of our Node of
// the linked list
public

    class Node {
    public

        Node next;
    public

        Node prev;
    public

        int data;

    // Create a node with the
    // given value
    public

        Node(int value)
    {
        data = value;
        next = null;
        prev = null;
    }
}

public

    class Stack {

    private Node head;
    private Node tail;

    // Initialize stack class
    // with its head and tail as null
    public Stack()
    {
        head = null;
        tail = null;
    }

    public void Push(int value)
    {
        Node newNode = new Node(value);
        if (head == null) {
            head = newNode;
            head.next = null;
            head.prev = null;
            tail = newNode;
        }
        else {
            newNode.prev = tail;
            tail.next = newNode;
            tail = newNode;
        }
    }

    public void Pop()
    {
        if (head == null)
            Console.WriteLine("stack underflow");

        if (head == tail) {
            head = null;
            tail = null;
        }
        else {
            Node n = tail;
            tail = tail.prev;
            n.prev = null;
            tail.next = null;
        }
    }

    public void merge(Stack s)
    {
        head.prev = s.tail;
        s.tail.next = head;
        head = s.head;
        s.tail = null;
        s.head = null;
    }

    public void display()
    {
        if (tail != null) {
            Node n = tail;
            while (n != null) {
                Console.Write(n.data + " ");
                n = n.prev;
            }
            Console.WriteLine();
        }
        else {
            Console.WriteLine("Stack Underflow");
        }
    }
}

public class GFG {
    public static void Main(String[] args)
    {
        Stack ms1 = new Stack();
        Stack ms2 = new Stack();

        ms1.Push(6);
        ms1.Push(5);
        ms1.Push(4);
        ms2.Push(9);
        ms2.Push(8);
        ms2.Push(7);

        ms1.merge(ms2);
        ms1.display();
    }
}
// This code contributed by aashish1995
```

****Output**

```
4 5 6 7 8 9 
```**