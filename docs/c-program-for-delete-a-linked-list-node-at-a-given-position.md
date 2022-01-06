# 删除给定位置链表节点的 C 程序

> 原文:[https://www . geesforgeks . org/c-program-for-delete-a-linked-list-node-at-a-给定位置/](https://www.geeksforgeeks.org/c-program-for-delete-a-linked-list-node-at-a-given-position/)

给定一个单链表和一个位置，删除给定位置的链表节点。

**示例:**

```
Input: position = 1, Linked List = 8->2->3->1->7
Output: Linked List =  8->3->1->7

Input: position = 0, Linked List = 8->2->3->1->7
Output: Linked List = 2->3->1->7
```

如果要删除的节点是根，只需将其删除即可。要删除中间节点，我们必须有一个指向要删除的节点之前的节点的指针。所以如果位置不为零，我们运行一个位置循环 1 次，得到一个指向前一个节点的指针。

以下是上述想法的实现。

## C

```
// A complete working C program to delete a node in a linked list
// at a given position
#include <stdio.h>
#include <stdlib.h>

// A linked list node
struct Node
{
    int data;
    struct Node *next;
};

/* Given a reference (pointer to pointer) to the head of a list
   and an int inserts a new node on the front of the list. */
void push(struct Node** head_ref, int new_data)
{
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));
    new_node->data  = new_data;
    new_node->next = (*head_ref);
    (*head_ref)    = new_node;
}

/* Given a reference (pointer to pointer) to the head of a list
   and a position, deletes the node at the given position */
void deleteNode(struct Node **head_ref, int position)
{
   // If linked list is empty
   if (*head_ref == NULL)
      return;

   // Store head node
   struct Node* temp = *head_ref;

    // If head needs to be removed
    if (position == 0)
    {
        *head_ref = temp->next;   // Change head
        free(temp);               // free old head
        return;
    }

    // Find previous node of the node to be deleted
    for (int i=0; temp!=NULL && i<position-1; i++)
         temp = temp->next;

    // If position is more than number of nodes
    if (temp == NULL || temp->next == NULL)
         return;

    // Node temp->next is the node to be deleted
    // Store pointer to the next of node to be deleted
    struct Node *next = temp->next->next;

    // Unlink the node from linked list
    free(temp->next);  // Free memory

    temp->next = next;  // Unlink the deleted node from list
}

// This function prints contents of linked list starting from
// the given node
void printList(struct Node *node)
{
    while (node != NULL)
    {
        printf(" %d ", node->data);
        node = node->next;
    }
}

/* Driver program to test above functions*/
int main()
{
    /* Start with the empty list */
    struct Node* head = NULL;

    push(&head, 7);
    push(&head, 1);
    push(&head, 3);
    push(&head, 2);
    push(&head, 8);

    puts("Created Linked List: ");
    printList(head);
    deleteNode(&head, 4);
    puts("
Linked List after Deletion at position 4: ");
    printList(head);
    return 0;
}
```

**输出:**

```
Created Linked List: 
 8  2  3  1  7 
Linked List after Deletion at position 4: 
 8  2  3  1 
```

详情请参考[删除给定位置](https://www.geeksforgeeks.org/delete-a-linked-list-node-at-a-given-position/)的链表节点整篇文章！