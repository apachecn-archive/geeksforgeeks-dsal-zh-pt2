# 从链表中删除最后一个条目的程序

> 原文:[https://www . geeksforgeeks . org/c-用于从链接列表中删除最后出现的项目的程序/](https://www.geeksforgeeks.org/c-program-for-deleting-last-occurrence-of-an-item-from-linked-list/)

使用指针，循环遍历整个列表，并使用特殊指针跟踪包含最后一个出现键的节点之前的节点。在此之后，只需将特殊指针的下一个存储到特殊指针的下一个，以从链表中移除所需的节点。

## C

```
#include <stdio.h>
#include <stdlib.h>

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
    while(*head) 
    {
        if((*head)->data == x) 
        {
            tmp1 = head;
        }
        head = &(*head)->next;
    }
    if(tmp1) 
    {
        struct Node* tmp = *tmp1;
        *tmp1 = tmp->next;
        free(tmp);
    }
}

/* Utility function to create a 
   new node with given key */
struct Node* newNode(int x)
{
    struct Node* node = 
           malloc(sizeof(struct Node*));
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
        printf("NULL");
        return;
    }
    while (temp != NULL) 
    {
        printf("%d --> ", 
                temp->data);
        temp = temp->next;
    }
    printf("NULL");
}

// Driver code
int main()
{
    struct Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = 
    newNode(3);
    head->next->next->next = 
    newNode(4);
    head->next->next->next->next = 
    newNode(5);
    head->next->next->next->next->next = 
    newNode(4);
    head->next->next->next->next->next->next = 
    newNode(4);
    printf("Created Linked list: ");
    display(head);

    // Pass the address of the head pointer
    deleteLast(&head, 4);   
    printf("List after deletion of 4: ");
    display(head);
    return 0;
}
```

**输出:**

```
Created Linked list: 1 --> 2 --> 3 --> 4 --> 5 --> 4 --> 4 --> NULL
List after deletion of 4: 1 --> 2 --> 3 --> 4 --> 5 --> 4 --> NULL
```

**当要删除的节点是最后一个节点时，上述解决方案不起作用。**
以下方案处理所有案件。

## C

```
// A C program to demonstrate deletion 
// of last Node in singly linked list
#include <stdio.h>
#include <stdlib.h>

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

/* Utility function to create a 
   new node with given key */
struct Node* newNode(int x)
{
    struct Node* node = 
           malloc(sizeof(struct Node*));
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
        printf("NULL");
        return;
    }
    while (temp != NULL) 
    {
        printf("%d --> ", temp->data);
        temp = temp->next;
    }
    printf("NULL");
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
    printf("Created Linked list: ");
    display(head);
    deleteLast(head, 4);
    printf("List after deletion of 4: ");
    display(head);
    return 0;
}
```

**输出:**

```
Created Linked List: 
1  2  3  4  5  4  4 
Linked List after Deletion of 1: 
1  2  3  4  5  4
```

详情请参考[从链表](https://www.geeksforgeeks.org/delete-last-occurrence-of-an-item-from-linked-list/)中删除最后一个条目的完整文章！