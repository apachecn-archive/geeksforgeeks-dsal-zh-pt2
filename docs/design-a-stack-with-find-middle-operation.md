# 设计一个对中间元素进行操作的堆栈

> 原文:[https://www . geesforgeks . org/design-a-stack-with-find-middle-operation/](https://www.geeksforgeeks.org/design-a-stack-with-find-middle-operation/)

如何在 **O(1)时间复杂度**中实现一个支持后续操作的栈？
1) push()将元素添加到堆栈顶部。
2) pop()从堆栈顶部移除元素。
3) findMiddle()将返回堆栈的中间元素。
4)删除中间()将删除中间元素。
推送和弹出是标准堆栈操作。
重要的问题是，栈的实现是使用链表还是数组？
请注意，我们需要找到并删除中间元素。从中间删除元素对于数组来说不是 O(1)。此外，当我们按下一个元素时，我们可能需要向上移动中间指针，当我们弹出()时，我们可能需要向下移动中间指针。在单链表中，不能双向移动中间指针。
思路是使用双链表(DLL)。我们可以通过维护中间指针来删除 O(1)时间中的中间元素。我们可以使用上一个和下一个指针在两个方向上移动中间指针。
下面是 push()、pop()和 findMiddle()操作的实现。deleteMiddle()的实现只是一个练习。如果堆栈中有偶数个元素，findMiddle()将返回第二个中间元素。例如，如果堆栈包含{1，2，3，4}，那么 findMiddle()将返回 3。

## C++

```
/* C++ Program to implement a stack
that supports findMiddle() and
deleteMiddle in O(1) time */
#include <bits/stdc++.h>
using namespace std;

class myStack
{
    struct Node
    {
        int num;
        Node *next;
        Node *prev;

        Node(int num)
        {
            this->num = num;
        }
    };

    //Members of stack
    Node *head = NULL;
    Node *mid = NULL;
    int size = 0;

public:
    void push(int data)
    {
        Node *temp = new Node(data);
        if (size==0)
        {
            head = temp;
            mid = temp;
            size++;
            return;
        }

        head->next = temp;
        temp->prev = head;

        //update the pointers
        head = head->next;
        if (size%2==1)
        {
            mid = mid->next;
        }
        size++;
    }

    void pop()
    {
        if (size!=0)
        {
            if (size==1)
            {
                head = NULL;
                mid = NULL;
            }
            else
            {
                head = head->prev;
                head->next = NULL;
                if (size%2==0)
                {
                    mid = mid->prev;
                }
            }
            size--;
        }
    }

    int findMiddle()
    {
        if (size==0)
        {
            return -1;
        }
        return mid->num;
    }

    void deleteMiddle()
    {
        if (size!=0)
        {
            if (size==1)
            {
                head = NULL;
                mid = NULL;
            }
            else if (size==2)
            {
                head = head->prev;
                mid = mid->prev;
                head->next =NULL;
            }
            else
            {
                mid->next->prev = mid->prev;
                mid->prev->next = mid->next;
                if (size%2==0)
                {
                    mid = mid->prev;
                }
                else
                {
                    mid = mid->next;
                }
            }
            size--;
        }
    }
};

int main()
{
    myStack st;
    st.push(11);
    st.push(22);
    st.push(33);
    st.push(44);
    st.push(55);
    st.pop();
    st.pop();
    st.pop();
    cout<<st.findMiddle()<<endl;
    st.deleteMiddle();
    cout<<st.findMiddle()<<endl;
    return 0;
}
// This code is contributed by Nikhil Goswami
```

## C

```
/* Program to implement a stack that supports findMiddle()
   and deleteMiddle in O(1) time */
#include <stdio.h>
#include <stdlib.h>

/* A Doubly Linked List Node */
struct DLLNode {
    struct DLLNode* prev;
    int data;
    struct DLLNode* next;
};

/* Representation of the stack data structure that supports
   findMiddle() in O(1) time.  The Stack is implemented
   using Doubly Linked List. It maintains pointer to head
   node, pointer to middle node and count of nodes */
struct myStack {
    struct DLLNode* head;
    struct DLLNode* mid;
    int count;
};

/* Function to create the stack data structure */
struct myStack* createMyStack()
{
    struct myStack* ms
        = (struct myStack*)malloc(sizeof(struct myStack));
    ms->count = 0;
    return ms;
};

/* Function to push an element to the stack */
void push(struct myStack* ms, int new_data)
{
    /* allocate DLLNode and put in data */
    struct DLLNode* new_DLLNode
        = (struct DLLNode*)malloc(sizeof(struct DLLNode));
    new_DLLNode->data = new_data;

    /* Since we are adding at the beginning,
      prev is always NULL */
    new_DLLNode->prev = NULL;

    /* link the old list off the new DLLNode */
    new_DLLNode->next = ms->head;

    /* Increment count of items in stack */
    ms->count += 1;

    /* Change mid pointer in two cases
       1) Linked List is empty
       2) Number of nodes in linked list is odd */
    if (ms->count == 1) {
        ms->mid = new_DLLNode;
    }
    else {
        ms->head->prev = new_DLLNode;

        if (ms->count & 1) // Update mid if ms->count is odd
            ms->mid = ms->mid->prev;
    }

    /* move head to point to the new DLLNode */
    ms->head = new_DLLNode;
}

/* Function to pop an element from stack */
int pop(struct myStack* ms)
{
    /* Stack underflow */
    if (ms->count == 0) {
        printf("Stack is empty\n");
        return -1;
    }

    struct DLLNode* head = ms->head;
    int item = head->data;
    ms->head = head->next;

    // If linked list doesn't become empty, update prev
    // of new head as NULL
    if (ms->head != NULL)
        ms->head->prev = NULL;

    ms->count -= 1;

    // update the mid pointer when we have even number of
    // elements in the stack, i,e move down the mid pointer.
    if (!((ms->count) & 1))
        ms->mid = ms->mid->next;

    free(head);

    return item;
}

// Function for finding middle of the stack
int findMiddle(struct myStack* ms)
{
    if (ms->count == 0) {
        printf("Stack is empty now\n");
        return -1;
    }

    return ms->mid->data;
}

// Driver program to test functions of myStack
int main()
{
    /* Let us create a stack using push() operation*/
    struct myStack* ms = createMyStack();
    push(ms, 11);
    push(ms, 22);
    push(ms, 33);
    push(ms, 44);
    push(ms, 55);
    push(ms, 66);
    push(ms, 77);

    printf("Item popped is %d\n", pop(ms));
    printf("Item popped is %d\n", pop(ms));
    printf("Middle Element is %d\n", findMiddle(ms));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Java Program to implement a stack that supports
findMiddle() and deleteMiddle in O(1) time */

public class GFG {
    /* A Doubly Linked List Node */
    class DLLNode {
        DLLNode prev;
        int data;
        DLLNode next;
        DLLNode(int d) { data = d; }
    }

    /* Representation of the stack data structure that
       supports findMiddle() in O(1) time.  The Stack is
       implemented using Doubly Linked List. It maintains
       pointer to head node, pointer to middle node and
       count of nodes */
    class myStack {
        DLLNode head;
        DLLNode mid;
        int count;
    }

    /* Function to create the stack data structure */
    myStack createMyStack()
    {
        myStack ms = new myStack();
        ms.count = 0;
        return ms;
    }

    /* Function to push an element to the stack */
    void push(myStack ms, int new_data)
    {

        /* allocate DLLNode and put in data */
        DLLNode new_DLLNode = new DLLNode(new_data);

        /* Since we are adding at the beginning,
          prev is always NULL */
        new_DLLNode.prev = null;

        /* link the old list off the new DLLNode */
        new_DLLNode.next = ms.head;

        /* Increment count of items in stack */
        ms.count += 1;

        /* Change mid pointer in two cases
           1) Linked List is empty
           2) Number of nodes in linked list is odd */
        if (ms.count == 1) {
            ms.mid = new_DLLNode;
        }
        else {
            ms.head.prev = new_DLLNode;

            if ((ms.count % 2)
                != 0) // Update mid if ms->count is odd
                ms.mid = ms.mid.prev;
        }

        /* move head to point to the new DLLNode */
        ms.head = new_DLLNode;
    }

    /* Function to pop an element from stack */
    int pop(myStack ms)
    {
        /* Stack underflow */
        if (ms.count == 0) {
            System.out.println("Stack is empty");
            return -1;
        }

        DLLNode head = ms.head;
        int item = head.data;
        ms.head = head.next;

        // If linked list doesn't become empty, update prev
        // of new head as NULL
        if (ms.head != null)
            ms.head.prev = null;

        ms.count -= 1;

        // update the mid pointer when we have even number
        // of elements in the stack, i,e move down the mid
        // pointer.
        if (ms.count % 2 == 0)
            ms.mid = ms.mid.next;

        return item;
    }

    // Function for finding middle of the stack
    int findMiddle(myStack ms)
    {
        if (ms.count == 0) {
            System.out.println("Stack is empty now");
            return -1;
        }
        return ms.mid.data;
    }

    // Driver program to test functions of myStack
    public static void main(String args[])
    {
        GFG ob = new GFG();
        myStack ms = ob.createMyStack();
        ob.push(ms, 11);
        ob.push(ms, 22);
        ob.push(ms, 33);
        ob.push(ms, 44);
        ob.push(ms, 55);
        ob.push(ms, 66);
        ob.push(ms, 77);

        System.out.println("Item popped is " + ob.pop(ms));
        System.out.println("Item popped is " + ob.pop(ms));
        System.out.println("Middle Element is "
                           + ob.findMiddle(ms));
    }
}

// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
''' Python3 Program to implement a stack
that supports findMiddle()
and deleteMiddle in O(1) time '''

''' A Doubly Linked List Node '''

class DLLNode:

    def __init__(self, d):
        self.prev = None
        self.data = d
        self.next = None

''' Representation of the stack
data structure that supports
findMiddle() in O(1) time. The
Stack is implemented using
Doubly Linked List. It maintains
pointer to head node, pointer
to middle node and count of
nodes '''

class myStack:

    def __init__(self):
        self.head = None
        self.mid = None
        self.count = 0

''' Function to create the stack data structure '''

def createMyStack():
    ms = myStack()
    ms.count = 0
    return ms

''' Function to push an element to the stack '''

def push(ms, new_data):
    ''' allocate DLLNode and put in data '''
    new_DLLNode = DLLNode(new_data)

    ''' Since we are adding at the beginning,
    prev is always NULL '''
    new_DLLNode.prev = None

    ''' link the old list off the new DLLNode '''
    new_DLLNode.next = ms.head

    ''' Increment count of items in stack '''
    ms.count += 1

    ''' Change mid pointer in two cases
    1) Linked List is empty
    2) Number of nodes in linked list is odd '''
    if(ms.count == 1):
        ms.mid = new_DLLNode

    else:
        ms.head.prev = new_DLLNode

        # Update mid if ms->count is odd
        if((ms.count % 2) != 0):
            ms.mid = ms.mid.prev

    ''' move head to point to the new DLLNode '''
    ms.head = new_DLLNode

''' Function to pop an element from stack '''

def pop(ms):
    ''' Stack underflow '''
    if(ms.count == 0):

        print("Stack is empty")
        return -1

    head = ms.head
    item = head.data
    ms.head = head.next

    # If linked list doesn't become empty,
    # update prev of new head as NULL
    if(ms.head != None):
        ms.head.prev = None
    ms.count -= 1

    # update the mid pointer when
    # we have even number of elements
    # in the stack, i,e move down
    # the mid pointer.
    if(ms.count % 2 == 0):
        ms.mid = ms.mid.next
    return item

# Function for finding middle of the stack

def findMiddle(ms):
    if(ms.count == 0):
        print("Stack is empty now")
        return -1
    return ms.mid.data

# Driver code
if __name__ == '__main__':

    ms = createMyStack()
    push(ms, 11)
    push(ms, 22)
    push(ms, 33)
    push(ms, 44)
    push(ms, 55)
    push(ms, 66)
    push(ms, 77)

    print("Item popped is " +
          str(pop(ms)))
    print("Item popped is " +
          str(pop(ms)))
    print("Middle Element is " +
          str(findMiddle(ms)))

    # This code is contributed by rutvik_56.
```

## C#

```
/* C# Program to implement a stack
that supports findMiddle()
and deleteMiddle in O(1) time */
using System;

class GFG {
    /* A Doubly Linked List Node */
    public class DLLNode {
        public DLLNode prev;
        public int data;
        public DLLNode next;
        public DLLNode(int d) { data = d; }
    }

    /* Representation of the stack
    data structure that supports
    findMiddle() in O(1) time. The
    Stack is implemented using
    Doubly Linked List. It maintains
    pointer to head node, pointer
    to middle node and count of
    nodes */
    public class myStack {
        public DLLNode head;
        public DLLNode mid;
        public int count;
    }

    /* Function to create the stack data structure */
    myStack createMyStack()
    {
        myStack ms = new myStack();
        ms.count = 0;
        return ms;
    }

    /* Function to push an element to the stack */
    void push(myStack ms, int new_data)
    {

        /* allocate DLLNode and put in data */
        DLLNode new_DLLNode = new DLLNode(new_data);

        /* Since we are adding at the beginning,
        prev is always NULL */
        new_DLLNode.prev = null;

        /* link the old list off the new DLLNode */
        new_DLLNode.next = ms.head;

        /* Increment count of items in stack */
        ms.count += 1;

        /* Change mid pointer in two cases
        1) Linked List is empty
        2) Number of nodes in linked list is odd */
        if (ms.count == 1) {
            ms.mid = new_DLLNode;
        }
        else {
            ms.head.prev = new_DLLNode;

            // Update mid if ms->count is odd
            if ((ms.count % 2) != 0)
                ms.mid = ms.mid.prev;
        }

        /* move head to point to the new DLLNode */
        ms.head = new_DLLNode;
    }

    /* Function to pop an element from stack */
    int pop(myStack ms)
    {
        /* Stack underflow */
        if (ms.count == 0) {
            Console.WriteLine("Stack is empty");
            return -1;
        }

        DLLNode head = ms.head;
        int item = head.data;
        ms.head = head.next;

        // If linked list doesn't become empty,
        // update prev of new head as NULL
        if (ms.head != null)
            ms.head.prev = null;

        ms.count -= 1;

        // update the mid pointer when
        // we have even number of elements
        // in the stack, i,e move down
        // the mid pointer.
        if (ms.count % 2 == 0)
            ms.mid = ms.mid.next;

        return item;
    }

    // Function for finding middle of the stack
    int findMiddle(myStack ms)
    {
        if (ms.count == 0) {
            Console.WriteLine("Stack is empty now");
            return -1;
        }
        return ms.mid.data;
    }

    // Driver code
    public static void Main(String[] args)
    {
        GFG ob = new GFG();
        myStack ms = ob.createMyStack();
        ob.push(ms, 11);
        ob.push(ms, 22);
        ob.push(ms, 33);
        ob.push(ms, 44);
        ob.push(ms, 55);
        ob.push(ms, 66);
        ob.push(ms, 77);

        Console.WriteLine("Item popped is " + ob.pop(ms));
        Console.WriteLine("Item popped is " + ob.pop(ms));
        Console.WriteLine("Middle Element is "
                          + ob.findMiddle(ms));
    }
}

// This code is contributed
// by Arnab Kundu
```

**Output**

```
Item popped is 77
Item popped is 66
Item popped is 55
Middle Element is 33
Deleted Middle Element is 33
Middle Element is 22
```

本文由 [**钱德拉·普拉卡什**](https://www.facebook.com/chandra.prakash.52643) 供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息