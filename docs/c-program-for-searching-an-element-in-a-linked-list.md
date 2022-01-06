# 用于在链表中搜索元素的 C 程序

> 原文:[https://www . geesforgeks . org/c-program-for-search-a-element-in-a-link-list/](https://www.geeksforgeeks.org/c-program-for-searching-an-element-in-a-linked-list/)

编写一个函数，在给定的单链表中搜索给定的键“x”。如果 x 出现在链表中，函数应该返回 true，否则返回 false。

```
bool search(Node *head, int x)
```

例如，如果要搜索的关键字是 15，链表是 14->21->11->30->10，那么函数应该返回 false。如果要搜索的关键字是 14，那么函数应该返回 true。
**迭代求解:**

```
1) Initialize a node pointer, current = head.
2) Do following while current is not NULL
    a) current->key is equal to the key being searched return true.
    b) current = current->next
3) Return false 
```

下面是上述算法的迭代实现，以搜索给定的关键字。

## C

```
// Iterative C program to search an 
// element in linked list
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>

// Link list node 
struct Node
{
    int key;
    struct Node* next;
};

/* Given a reference (pointer to pointer) to 
   the head of a list and an int, push a new 
   node on the front of the list. */
void push(struct Node** head_ref, 
          int new_key)
{
    // Allocate node
    struct Node* new_node =
           (struct Node*) malloc(sizeof(struct Node));

    // Put in the key
    new_node->key = new_key;

    // Link the old list off the new node
    new_node->next = (*head_ref);

    // Move the head to point to the new node 
    (*head_ref) = new_node;
}

// Checks whether the value x is present
// in linked list 
bool search(struct Node* head, int x)
{
    // Initialize current
    struct Node* current = head;  
    while (current != NULL)
    {
        if (current->key == x)
            return true;
        current = current->next;
    }
    return false;
}

// Driver code
int main()
{
    // Start with the empty list 
    struct Node* head = NULL;
    int x = 21;

    // Use push() to construct list
    // 14->21->11->30->10 
    push(&head, 10);
    push(&head, 30);
    push(&head, 11);
    push(&head, 21);
    push(&head, 14);

    search(head, 21)? printf("Yes") : printf("No");
    return 0;
}
```

**输出:**

```
Yes
```

**递归解:**

```
bool search(head, x)
1) If head is NULL, return false.
2) If head's key is same as x, return true;
3) Else return search(head->next, x) 
```

下面是上述算法的递归实现，用于搜索给定的关键字。

## C

```
// Recursive C program to search an 
// element in linked list
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>
// Link list node
struct Node
{
    int key;
    struct Node* next;
};

/* Given a reference (pointer to pointer) to 
   the head of a list and an int, push a new
   node on the front of the list. */
void push(struct Node** head_ref, 
          int new_key)
{
    // Allocate node
    struct Node* new_node =
           (struct Node*) malloc(sizeof(struct Node));

    // Put in the key
    new_node->key = new_key;

    // Link the old list off the new node
    new_node->next = (*head_ref);

    // Move the head to point to the new node
    (*head_ref) = new_node;
}

// Checks whether the value x is present
// in linked list
bool search(struct Node* head, int x)
{
    // Base case
    if (head == NULL)
        return false;

    // If key is present in current 
    // node, return true
    if (head->key == x)
        return true;

    // Recur for remaining list
    return search(head->next, x);
}

// Driver code
int main()
{
    // Start with the empty list 
    struct Node* head = NULL;
    int x = 21;

    // Use push() to construct list
    // 14->21->11->30->10 
    push(&head, 10);
    push(&head, 30);
    push(&head, 11);
    push(&head, 21);
    push(&head, 14);

    search(head, 21)? printf("Yes") : printf("No");
    return 0;
}
```

**输出:**

```
Yes
```

更多细节请参考完整的文章[在链表中搜索元素(迭代和递归)](https://www.geeksforgeeks.org/search-an-element-in-a-linked-list-iterative-and-recursive/)！