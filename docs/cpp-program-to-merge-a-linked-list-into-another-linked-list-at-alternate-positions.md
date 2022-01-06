# C++程序在交替位置将一个链表合并到另一个链表中

> 原文:[https://www . geesforgeks . org/CPP-程序-将一个链表合并到另一个链表中-交替位置/](https://www.geeksforgeeks.org/cpp-program-to-merge-a-linked-list-into-another-linked-list-at-alternate-positions/)

给定两个链表，在第一个链表的交替位置将第二个链表的节点插入第一个链表。
例如，如果第一个列表是 5- > 7- > 17- > 13- > 11，第二个是 12- > 10- > 2- > 4- > 6，则第一个列表应该变成 5->12->7->10->17->2->13->4->11->仅当有位置可用时，才应插入第二个列表的节点。例如，如果第一个列表是 1- > 2- > 3，第二个列表是 4- > 5- > 6- > 7- > 8，那么第一个列表应该变成 1->4->2->5->3->6，第二个列表应该变成 7- > 8。
不允许使用额外的空间(不允许创建额外的节点)，即必须就地插入。预期时间复杂度为 O(n)，其中 n 是第一个列表中的节点数。

想法是在第一个循环中有可用位置时运行一个循环，并通过更改指针来插入第二个列表的节点。下面是这种方法的实现。

## C++

```
// C++ program to merge a linked list 
// into another at alternate positions 
#include <bits/stdc++.h>
using namespace std;

// A nexted list node 
class Node 
{ 
    public:
    int data; 
    Node *next; 
}; 

/* Function to insert a node 
   at the beginning */
void push(Node ** head_ref, 
          int new_data) 
{ 
    Node* new_node = new Node();
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Utility function to print a 
   singly linked list */
void printList(Node *head) 
{ 
    Node *temp = head; 
    while (temp != NULL) 
    { 
        cout << temp -> data << " "; 
        temp = temp -> next; 
    } 
    cout << endl;
} 

// Main function that inserts nodes of 
// linked list q into p at alternate positions. 
// Since head of first list never changes and 
// head of second list may change, we need single 
// pointer for first list and double pointer for 
// second list. 
void merge(Node *p, Node **q) 
{ 
    Node *p_curr = p, *q_curr = *q; 
    Node *p_next, *q_next; 

    // While therre are available positions 
    // in p 
    while (p_curr != NULL && 
           q_curr != NULL) 
    { 
        // Save next pointers 
        p_next = p_curr->next; 
        q_next = q_curr->next; 

        // Make q_curr as next of p_curr 
        // Change next pointer of q_curr 
        q_curr->next = p_next; 

        // Change next pointer of p_curr 
        p_curr->next = q_curr; 

        // Update current pointers for 
        // next iteration 
        p_curr = p_next; 
        q_curr = q_next; 
    } 

    // Update head pointer of second list 
    *q = q_curr; 
} 

// Driver code 
int main() 
{ 
    Node *p = NULL, *q = NULL; 
    push(&p, 3); 
    push(&p, 2); 
    push(&p, 1); 
    cout << "First Linked List:"; 
    printList(p); 

    push(&q, 8); 
    push(&q, 7); 
    push(&q, 6); 
    push(&q, 5); 
    push(&q, 4); 
    cout << "Second Linked List:"; 
    printList(q); 

    merge(p, &q); 

    cout << 
    "Modified First Linked List:"; 
    printList(p); 

    cout << 
    "Modified Second Linked List:"; 
    printList(q); 

    return 0; 
} 
// This code is contributed by rathbhupendra
```

**输出:**

```
First Linked List:
1 2 3
Second Linked List:
4 5 6 7 8
Modified First Linked List:
1 4 2 5 3 6
Modified Second Linked List:
7 8 
```

更多详情请参考[整篇文章在交替位置](https://www.geeksforgeeks.org/merge-a-linked-list-into-another-linked-list-at-alternate-positions/)将一个链表合并成另一个链表！