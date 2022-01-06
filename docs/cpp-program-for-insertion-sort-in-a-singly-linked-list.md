# 用于在单链表中插入排序的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-插入程序-单链表排序/](https://www.geeksforgeeks.org/cpp-program-for-insertion-sort-in-a-singly-linked-list/)

我们已经讨论了数组的插入排序。在本文中，我们将讨论链表的插入排序。
下面是一个简单的链表插入排序算法。

```
1) Create an empty sorted (or result) list.
2) Traverse the given list, do following for every node.
......a) Insert current node in sorted way in sorted or result list.
3) Change head of given linked list to head of sorted (or result) list.
```

主要步骤是(2.a)已经在帖子[单链表排序插入](https://www.geeksforgeeks.org/given-a-linked-list-which-is-sorted-how-will-you-insert-in-sorted-way/)
中介绍过了，下面是上述算法的实现:

## C++

```
// C++ program to sort link list
// using insertion sort
#include <bits/stdc++.h>
using namespace std;

struct Node 
{
    int val;
    struct Node* next;
    Node(int x)
    {
        val = x;
        next = NULL;
    }
};

class LinkedlistIS 
{
    public:
    Node* head;
    Node* sorted;

    void push(int val)
    {
        // Allocate node 
        Node* newnode = new Node(val);

        // Link the old list off the 
        // new node 
        newnode->next = head;
        // Move the head to point to the 
        // new node 
        head = newnode;
    }

    // Function to sort a singly linked list 
    // using insertion sort
    void insertionSort(Node* headref)
    {
        // Initialize sorted linked list
        sorted = NULL;
        Node* current = headref;

        // Traverse the given linked list 
        // and insert every node to sorted
        while (current != NULL) 
        {
            // Store next for next iteration
            Node* next = current->next;

            // Insert current in sorted 
            // linked list
            sortedInsert(current);

            // Update current
            current = next;
        }

        // Update head_ref to point to 
        // sorted linked list
        head = sorted;
    }

    /* Function to insert a new_node in a list. 
       Note that this function expects a pointer 
       to head_ref as this can modify the head of 
       the input linked list (similar to push()) */
    void sortedInsert(Node* newnode)
    {
        // Special case for the head end 
        if (sorted == NULL || 
            sorted->val >= newnode->val) 
        {
            newnode->next = sorted;
            sorted = newnode;
        }
        else 
        {
            Node* current = sorted;

            /* Locate the node before the 
               point of insertion */
            while (current->next != NULL && 
                   current->next->val < newnode->val) 
            {
                current = current->next;
            }
            newnode->next = current->next;
            current->next = newnode;
        }
    }

    // Function to print linked list 
    void printlist(Node* head)
    {
        while (head != NULL) 
        {
            cout << head->val << " ";
            head = head->next;
        }
    }
};

// Driver code
int main()
{
    LinkedlistIS list;
    list.head = NULL;
    list.push(5);
    list.push(20);
    list.push(4);
    list.push(3);
    list.push(30);
    cout << "Linked List before sorting" << 
             endl;
    list.printlist(list.head);
    cout << endl;
    list.insertionSort(list.head);
    cout << "Linked List After sorting" << 
             endl;
    list.printlist(list.head);
}
// This code is contributed by nirajgusain5
```

**输出:**

```
Linked List before sorting
30  3  4  20  5
Linked List after sorting
3  4  5  20  30
```

详情请参考[单链表插入排序](https://www.geeksforgeeks.org/insertion-sort-for-singly-linked-list/)整篇文章！