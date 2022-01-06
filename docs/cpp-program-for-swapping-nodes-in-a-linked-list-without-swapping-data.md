# 用于交换链表中的节点而不交换数据的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-以程序交换链接列表中的节点-不交换数据/](https://www.geeksforgeeks.org/cpp-program-for-swapping-nodes-in-a-linked-list-without-swapping-data/)

给定一个链表和其中的两个键，用两个给定的键交换节点。应该通过更改链接来交换节点。当数据包含许多字段时，交换节点的数据在许多情况下可能是昂贵的。

可以假设链表中的所有键都是不同的。

**示例:**

```
Input : 10->15->12->13->20->14,  x = 12, y = 20
Output: 10->15->20->13->12->14

Input : 10->15->12->13->20->14,  x = 10, y = 20
Output: 20->15->12->13->10->14

Input : 10->15->12->13->20->14,  x = 12, y = 13
Output: 10->15->13->12->20->14
```

这看起来可能是一个简单的问题，但这是一个有趣的问题，因为它有以下情况需要处理。

1.  x 和 y 可以相邻，也可以不相邻。
2.  x 或 y 都可以是头节点。
3.  x 或 y 可能是最后一个节点。
4.  链接列表中可能不存在 x 和/或 y。

如何编写一个干净的工作代码来处理上述所有可能性。

想法是首先在给定的链表中搜索 x 和 y。如果他们中的任何一个不存在，那么返回。在搜索 x 和 y 时，跟踪当前和以前的指针。首先更改上一个指针的下一个，然后更改当前指针的下一个。

下面是上述方法的实现。

## C++

```
// C++ program to swap the nodes of linked list rather
// than swapping the field from the nodes.
#include <bits/stdc++.h>
using namespace std;

// A linked list node 
class Node 
{
    public:
    int data;
    Node* next;
};

// Function to swap nodes x and y in 
// linked list by changing links 
void swapNodes(Node** head_ref, 
               int x, int y)
{
    // Nothing to do if x and y 
    // are same
    if (x == y)
        return;

    // Search for x (keep track of 
    // prevX and CurrX
    Node *prevX = NULL, 
         *currX = *head_ref;
    while (currX && currX->data != x) 
    {
        prevX = currX;
        currX = currX->next;
    }

    // Search for y (keep track of 
    // prevY and CurrY
    Node *prevY = NULL,
         *currY = *head_ref;
    while (currY && currY->data != y) 
    {
        prevY = currY;
        currY = currY->next;
    }

    // If either x or y is not present, 
    // nothing to do
    if (currX == NULL || 
        currY == NULL)
        return;

    // If x is not head of linked list
    if (prevX != NULL)
        prevX->next = currY;
    else 

        // Else make y as new head
        *head_ref = currY;

    // If y is not head of linked list
    if (prevY != NULL)
        prevY->next = currX;
    else // Else make x as new head
        *head_ref = currX;

    // Swap next pointers
    Node* temp = currY->next;
    currY->next = currX->next;
    currX->next = temp;
}

// Function to add a node at the
// beginning of List 
void push(Node** head_ref, 
          int new_data)
{
    // Allocate node 
    Node* new_node = new Node();

    // Put in the data 
    new_node->data = new_data;

    // Link the old list off the new node 
    new_node->next = (*head_ref);

    // Move the head to point to the 
    // new node 
    (*head_ref) = new_node;
}

// Function to print nodes in a 
// given linked list 
void printList(Node* node)
{
    while (node != NULL) 
    {
        cout << node->data << " ";
        node = node->next;
    }
}

// Driver code
int main()
{
    Node* start = NULL;

    /* The constructed linked list is:
       1->2->3->4->5->6->7 */
    push(&start, 7);
    push(&start, 6);
    push(&start, 5);
    push(&start, 4);
    push(&start, 3);
    push(&start, 2);
    push(&start, 1);

    cout << "Linked list before calling swapNodes() ";
    printList(start);
    swapNodes(&start, 4, 3);
    cout << "Linked list after calling swapNodes() ";
    printList(start);
    return 0;
}
// This is code is contributed by rathbhupendra
```

**输出:**

```
Linked list before calling swapNodes() 1 2 3 4 5 6 7 
Linked list after calling swapNodes() 1 2 4 3 5 6 7 
```

**优化:**以上代码可以优化为单次遍历搜索 x 和 y。两个循环用于保持程序简单。

**更简单的方法:**

## C++

```
// C++ program to swap two given nodes 
// of a linked list
#include <iostream>

using namespace std;

// A linked list node class
class Node
{
    public:
    int data;
    class Node* next;

    // constructor
    Node(int val, Node* next)
        : data(val)
        , next(next)
    {
    }

    // print list from this
    // to last till null
    void printList()
    {
        Node* node = this;

        while (node != NULL) 
        {
            cout << node->data << " ";
            node = node->next;
        }

        cout << endl;
    }
};

// Function to add a node
// at the beginning of List
void push(Node** head_ref, 
          int new_data)
{
    // Allocate node
    (*head_ref) = new Node(new_data, 
                           *head_ref);
}

void swap(Node*& a, Node*& b)
{
    Node* temp = a;
    a = b;
    b = temp;
}

void swapNodes(Node** head_ref, 
               int x, int y)
{
    // Nothing to do if x and 
    // y are same
    if (x == y)
        return;

    Node **a = NULL, **b = NULL;

    // Search for x and y in the linked list
    // and store their pointer in a and b
    while (*head_ref) 
    {
        if ((*head_ref)->data == x) 
        {
            a = head_ref;
        }

        else if ((*head_ref)->data == y) 
        {
            b = head_ref;
        }

        head_ref = &((*head_ref)->next);
    }

    // If we have found both a and b
    // in the linked list swap current
    // pointer and next pointer of these
    if (a && b) 
    {
        swap(*a, *b);
        swap(((*a)->next), ((*b)->next));
    }
}

// Driver code
int main()
{
    Node* start = NULL;

    // The constructed linked list is:
    // 1->2->3->4->5->6->7
    push(&start, 7);
    push(&start, 6);
    push(&start, 5);
    push(&start, 4);
    push(&start, 3);
    push(&start, 2);
    push(&start, 1);

    cout << "Linked list before calling swapNodes() ";
    start->printList();
    swapNodes(&start, 6, 1);
    cout << "Linked list after calling swapNodes() ";
    start->printList();
}
```

**输出:**

```
Linked list before calling swapNodes() 1 2 3 4 5 6 7 
Linked list after calling swapNodes() 6 2 3 4 5 1 7 
```

更多详情请参考完整文章[在链表中交换节点不交换数据](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)！