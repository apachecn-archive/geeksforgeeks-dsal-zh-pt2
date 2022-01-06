# 通过改变链接成对交换给定链表元素的 C 程序

> 原文:[https://www . geeksforgeeks . org/c-成对交换程序-通过改变链接来交换给定链表的元素/](https://www.geeksforgeeks.org/c-program-for-pairwise-swapping-elements-of-a-given-linked-list-by-changing-links/)

给定一个单链表，编写一个成对交换元素的函数。例如，如果链表是 1->2->3->4->5->6->7，那么函数应该把它改成 2->1->4->3->6->5->7，如果链表是 1->2->3->4->5->6，那么函数应该把它改成 2->1->4->3->6->5

这个问题已经在[这里](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list/)讨论过了。这里提供的解决方案交换节点的数据。如果数据包含许多字段，将会有许多交换操作。所以一般来说，改变链接是一个更好的主意。下面是更改链接而不是交换数据的实现。

## C

```
/* This program swaps the nodes of 
   linked list rather than swapping 
   the field from the nodes. Imagine 
   a case where a node contains many 
   fields, there will be plenty of 
   unnecessary swap calls. */

#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>

// A linked list node 
struct Node 
{
    int data;
    struct Node* next;
};

/* Function to pairwise swap 
   elements of a linked list */
void pairWiseSwap(struct Node** head)
{
    // If linked list is empty or there 
    // is only one node in list
    if (*head == NULL || 
       (*head)->next == NULL)
        return;

    // Initialize previous and current 
    // pointers
    struct Node* prev = *head;
    struct Node* curr = (*head)->next;

    // Change head before proceeding
    *head = curr; 

    // Traverse the list
    while (true) 
    {
        struct Node* next = curr->next;

        // Change next of current as 
        // previous node
        curr->next = prev; 

        // If next NULL or next is the 
        // last node
        if (next == NULL || 
            next->next == NULL) 
        {
            prev->next = next;
            break;
        }

        // Change next of previous to 
        // next next
        prev->next = next->next;

        // Update previous and curr
        prev = next;
        curr = prev->next;
    }
}

/* Function to add a node at the 
   beginning of Linked List */
void push(struct Node** head_ref, 
          int new_data)
{
    // Allocate node 
    struct Node* new_node = 
          (struct Node*)malloc(sizeof(struct Node));

    // Put in the data  
    new_node->data = new_data;

    // Link the old list off the 
    // new node 
    new_node->next = (*head_ref);

    // Move the head to point to 
    // the new node 
    (*head_ref) = new_node;
}

/* Function to print nodes in a 
   given linked list */
void printList(struct Node* node)
{
    while (node != NULL) 
    {
        printf("%d ", 
               node->data);
        node = node->next;
    }
}

// Driver code
int main()
{
    struct Node* start = NULL;

    /* The constructed linked list is:
       1->2->3->4->5->6->7 */
    push(&start, 7);
    push(&start, 6);
    push(&start, 5);
    push(&start, 4);
    push(&start, 3);
    push(&start, 2);
    push(&start, 1);

    printf("
    Linked list before calling  pairWiseSwap() ");
    printList(start);

    pairWiseSwap(&start);

    printf("
    Linked list after calling  pairWiseSwap() ");
    printList(start);

    getchar();
    return 0;
}
```

**输出:**

```
Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7
```

**时间复杂度:**上述程序的时间复杂度为 O(n)，其中 n 为给定链表中的节点数。while 循环遍历给定的链表。

下面是同样方法的**递归实现**。我们更改前两个节点，并对剩余的列表重复执行。感谢 geek 和 omer salem 提出这个方法。

## C

```
/* This program swaps the nodes of linked list 
   rather than swapping the field from the nodes.
   Imagine a case where a node contains many 
   fields, there will be plenty of unnecessary 
   swap calls. */

#include <stdbool.h>
#include <stdio.h>
#include <stdlib.h>

// A linked list node 
struct node 
{
    int data;
    struct node* next;
};

/* Function to pairwise swap elements of 
   a linked list. It returns head of the 
   modified list, so return value of this
   node must be assigned */
struct node* pairWiseSwap(struct node* head)
{
    // Base Case: The list is empty or has 
    // only one node
    if (head == NULL || 
        head->next == NULL)
        return head;

    // Store head of list after two nodes
    struct node* remaining = 
           head->next->next;

    // Change head
    struct node* newhead = head->next;

    // Change next of second node
    head->next->next = head;

    // Recur for remaining list and change 
    // next of head
    head->next = pairWiseSwap(remaining);

    // Return new head of modified list
    return newhead;
}

/* Function to add a node at the 
   beginning of Linked List */
void push(struct node** head_ref, 
          int new_data)
{
    // Allocate node 
    struct node* new_node = 
          (struct node*)malloc(sizeof(struct node));

    // Put in the data  
    new_node->data = new_data;

    // Link the old list off the 
    // new node 
    new_node->next = (*head_ref);

    // Move the head to point to 
    // the new node 
    (*head_ref) = new_node;
}

/* Function to print nodes in a 
   given linked list */
void printList(struct node* node)
{
    while (node != NULL) 
    {
        printf("%d ", node->data);
        node = node->next;
    }
}

// Driver code
int main()
{
    struct node* start = NULL;

    /* The constructed linked list is:
        1->2->3->4->5->6->7 */
    push(&start, 7);
    push(&start, 6);
    push(&start, 5);
    push(&start, 4);
    push(&start, 3);
    push(&start, 2);
    push(&start, 1);

    printf("
    Linked list before calling  pairWiseSwap() ");
    printList(start);

    // NOTE THIS CHANGE
    start = pairWiseSwap(start); 

    printf("
    Linked list after calling  pairWiseSwap() ");
    printList(start);

    return 0;
}
```

**输出:**

```
Linked list before calling  pairWiseSwap() 1 2 3 4 5 6 7
Linked list after calling  pairWiseSwap() 2 1 4 3 6 5 7
```

更多细节请参考完整的文章[通过改变链接来成对交换给定链表的元素](https://www.geeksforgeeks.org/pairwise-swap-elements-of-a-given-linked-list-by-changing-links/)！