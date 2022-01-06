# 用于从链表中删除最后一个条目的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-用于从链接列表中删除最后出现的项目的程序/](https://www.geeksforgeeks.org/cpp-program-for-deleting-last-occurrence-of-an-item-from-linked-list/)

使用指针，循环遍历整个列表，并使用特殊指针跟踪包含最后一个出现键的节点之前的节点。在此之后，只需将特殊指针的下一个存储到特殊指针的下一个，以从链表中移除所需的节点。

## C++

```
// C++ program to implement the 
// above approach
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

// A linked list Node
struct Node 
{
    int data;
    struct Node* next;
};

// Function to delete the last 
// occurrence
void deleteLast(struct Node** head, 
                int x)
{
    struct Node** tmp1 = NULL;
    while (*head)
    {
        if ((*head)->data == x) 
        {
            tmp1 = head;
        }
        head = &(*head)->next;
    }
    if (tmp1)
    {
        struct Node* tmp = *tmp1;
        *tmp1 = tmp->next;
        free(tmp);
    }
}

// Utility function to create a new 
// node with given key 
struct Node* newNode(int x)
{
    Node* node = new Node ;
    node->data = x;
    node->next = NULL;
    return node;
}

// This function prints contents of 
// linked list starting from the given 
// Node
void display(struct Node* head)
{
    struct Node* temp = head;
    if (head == NULL)
    {
        cout << "NULL";
        return;
    }
    while (temp != NULL)
    {
        cout << temp->data << 
                " --> ";
        temp = temp->next;
    }
    cout << "NULL";
}

// Driver code
int main()
{
    struct Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = newNode(3);
    head->next->next->next = 
    newNode(4);
    head->next->next->next->next = 
    newNode(5);
    head->next->next->next->next->next = 
    newNode(4);
    head->next->next->next->next->next->next = 
    newNode(4);

    cout << "Created Linked list: ";
    display(head);

    // Pass the address of the head 
    // pointer
    deleteLast(&head, 4);   
    cout << "List after deletion of 4: ";

    display(head);    
    return 0;
}
// This code is contributed by khushboogoyal499
```

**输出:**

```
Created Linked list: 1 --> 2 --> 3 --> 4 --> 5 --> 4 --> 4 --> NULL
List after deletion of 4: 1 --> 2 --> 3 --> 4 --> 5 --> 4 --> NULL
```

给定一个喜欢的列表和一个要删除的键。从链接中删除键的最后一次出现。该列表可能有重复项。

**示例**:

```
Input:   1->2->3->5->2->10, key = 2
Output:  1->2->3->5->10
```

想法是从头到尾遍历链表。遍历时，跟踪最后一个出现的键。遍历完整列表后，通过复制下一个节点的数据并删除下一个节点来删除最后一个匹配项。

## C++

```
// A C++ program to demonstrate deletion 
// of last Node in singly linked list
#include <bits/stdc++.h>

// A linked list Node
struct Node 
{
    int key;
    struct Node* next;
};

void deleteLast(Node* head, 
                int key)
{
    // Initialize previous of Node 
    // to be deleted
    Node* x = NULL;

    // Start from head and find the 
    // Node to be deleted
    Node* temp = head;
    while (temp) 
    {
        // If we found the key, 
        // update xv
        if (temp->key == key)
            x = temp;

        temp = temp->next;
    }

    // Key occurs at-least once
    if (x != NULL) 
    {
        // Copy key of next Node to x
        x->key = x->next->key;

        // Store and unlink next
        temp = x->next;
        x->next = x->next->next;

        // Free memory for next
        delete temp;
    }
}

/* Utility function to create a 
   new node with given key */
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->next = NULL;
    return temp;
}

// This function prints contents of 
// linked list starting from the 
// given Node
void printList(struct Node* node)
{
    while (node != NULL) 
    {
        printf(" %d ", 
               node->key);
        node = node->next;
    }
}

// Driver code
int main()
{
    // Start with the empty list 
    struct Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = newNode(3);
    head->next->next->next = 
    newNode(5);
    head->next->next->next->next = 
    newNode(2);
    head->next->next->next->next->next = 
    newNode(10);

    puts(
    "Created Linked List: ");
    printList(head);
    deleteLast(head, 2);
    puts(
    "Linked List after Deletion of 1: ");
    printList(head);
    return 0;
}
```

**输出:**

```
Created Linked List: 
1  2  3  5  2  10 
Linked List after Deletion of 1: 
1  2  3  5  10
```

**当要删除的节点是最后一个节点时，上述解决方案不起作用。**
以下方案处理所有案件。

## C++

```
// A C++ program to demonstrate deletion 
// of last Node in singly linked list
#include <bits/stdc++.h>
using namespace std;

// A linked list Node
struct Node 
{
    int data;
    struct Node* next;
};

// Function to delete the last 
// occurrence
void deleteLast(struct Node* head, 
                int x)
{
    struct Node *temp = head, 
                *ptr = NULL;
    while (temp) 
    {
        // If found key, update
        if (temp->data == x) 
            ptr = temp;        
        temp = temp->next;
    }

    // If the last occurrence is the 
    // last node
    if (ptr != NULL && 
        ptr->next == NULL) 
    {
        temp = head;
        while (temp->next != ptr) 
            temp = temp->next;       
        temp->next = NULL;
    }

    // If it is not the last node
    if (ptr != NULL && 
        ptr->next != NULL) 
    {
        ptr->data = ptr->next->data;
        temp = ptr->next;
        ptr->next = ptr->next->next;
        free(temp);
    }
}

/* Utility function to create a new 
   node with given key */
struct Node* newNode(int x)
{
    Node* node = new Node ;
    node->data = x;
    node->next = NULL;
    return node;
}

// This function prints contents of 
// linked list starting from the given 
// Node
void display(struct Node* head)
{
    struct Node* temp = head;
    if (head == NULL) 
    {
        cout << "NULL";
        return;
    }
    while (temp != NULL) 
    {
        cout <<" --> "<< temp->data;
        temp = temp->next;
    }
    cout << "NULL";
}

// Driver code
int main()
{
    struct Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = newNode(3);
    head->next->next->next = 
    newNode(4);
    head->next->next->next->next = 
    newNode(5);
    head->next->next->next->next->next = 
    newNode(4);
    head->next->next->next->next->next->next = 
    newNode(4);
    cout <<
    "Created Linked list: ";
    display(head);
    deleteLast(head, 4);
    cout << 
    "List after deletion of 4: ";
    display(head);
    return 0;
}
// This code is contributed by shivanisinghss2110
```

**输出:**

```
Created Linked List: 
1  2  3  4  5  4  4 
Linked List after Deletion of 1: 
1  2  3  4  5  4
```

详情请参考完整文章[从链表](https://www.geeksforgeeks.org/delete-last-occurrence-of-an-item-from-linked-list/)中删除一项的最后一次出现！