# 求链表长度的 C 程序

> 原文:[https://www . geeksforgeeks . org/c-寻找链表长度的程序-迭代递归方法/](https://www.geeksforgeeks.org/c-program-for-finding-length-of-a-linked-list-iterative-and-recursive-approach/)

编写一个函数来计算给定单链表中的节点数。

![linkedlist_find_length](img/e38a7cce1aae90394ef3ebc5cd8323c1.png)

例如，对于链表 1->3->1->2->1，函数应该返回 5。

**迭代解:**

```
1) Initialize count as 0 
2) Initialize a node pointer, current = head.
3) Do following while current is not NULL
     a) current = current -> next
     b) count++;
4) Return count 
```

下面是上述算法的迭代实现，用于查找给定单链表中的节点数。

## C

```
// Iterative C program to find length or count 
// of nodes in a linked list
#include<stdio.h>
#include<stdlib.h>

// Link list node
struct Node
{
    int data;
    struct Node* next;
};

/* Given a reference (pointer to pointer) to 
   the head of a list and an int, push a new
   node on the front of the list. */
void push(struct Node** head_ref,  
          int new_data)
{
    // Allocate node
    struct Node* new_node =
           (struct Node*) malloc(sizeof(struct Node));

    // Put in the data 
    new_node->data = new_data;

    // Link the old list off the new node
    new_node->next = (*head_ref);

    // Move the head to point to the new node
    (*head_ref) = new_node;
}

// Counts no. of nodes in linked list
int getCount(struct Node* head)
{
    // Initialize count
    int count = 0;  

    // Initialize current
    struct Node* current = head;  
    while (current != NULL)
    {
        count++;
        current = current->next;
    }
    return count;
}

// Driver code
int main()
{
    // Start with the empty list
    struct Node* head = NULL;

    // Use push() to construct list
    // 1->2->1->3->1 
    push(&head, 1);
    push(&head, 3);
    push(&head, 1);
    push(&head, 2);
    push(&head, 1);

    // Check the count function
    printf("count of nodes is %d", 
            getCount(head));
    return 0;
}
```

**输出:**

```
count of nodes is 5
```

详情请参考[求链表长度(迭代和递归)](https://www.geeksforgeeks.org/find-length-of-a-linked-list-iterative-and-recursive/)整篇文章！