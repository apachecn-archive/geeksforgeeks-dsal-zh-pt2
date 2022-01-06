# 在给定约束下删除链表中给定节点的 C 程序

> 原文:[https://www . geesforgeks . org/c-program-for-delete-给定约束下链表中的给定节点/](https://www.geeksforgeeks.org/c-program-for-deleting-a-given-node-in-linked-list-under-given-constraints/)

给定一个单链表，编写一个函数来删除给定的节点。您的函数必须遵循以下约束:

1.  它必须接受指向起始节点的指针作为第一个参数，接受要删除的节点作为第二个参数，即指向头节点的指针不是全局的。
2.  它不应该返回指向头节点的指针。
3.  它不应该接受指向头节点的指针。

您可以假设链表永远不会变成空的。
让函数名为 deleteNode()。在一个简单的实现中，当要删除的节点是第一个节点时，函数需要修改头指针。正如[上一篇文章](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)中所讨论的，当一个函数修改头部指针时，该函数必须使用其中一个[给定的方法](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)，这里我们不能使用这些方法中的任何一个。
**解决方案**
我们明确处理待删除节点是第一个节点的情况，我们把下一个节点的数据复制到头上，删除下一个节点。被删除的节点不是头节点的情况可以通过找到前一个节点并改变前一个节点的下一个来正常处理。以下是实现。

## C

```
#include <stdio.h>
#include <stdlib.h>

// Structure of a linked list 
// node
struct Node
{
    int data;
    struct Node *next;
};

void deleteNode(struct Node *head, 
                struct Node *n)
{
    // When node to be deleted is 
    // head node
    if(head == n)
    {
        if(head->next == NULL)
        {
            printf("There is only one node. " , 
                   "The list can't be made empty ");
            return;
        }

        // Copy the data of next node to head
        head->data = head->next->data;

        // store address of next node
        n = head->next;

        // Remove the link of next node
        head->next = head->next->next;

        // free memory
        free(n);

        return;
    }

    // When not first node, follow the 
    // normal deletion process

    // Find the previous node
    struct Node *prev = head;
    while(prev->next != NULL && 
          prev->next != n)
        prev = prev->next;

    // Check if node really exists in 
    // Linked List
    if(prev->next == NULL)
    {
        printf(
        "Given node is not present in Linked List");
        return;
    }

    // Remove node from Linked List
    prev->next = prev->next->next;

    // Free memory
    free(n);

    return; 
}

/* Utility function to insert a 
   node at the beginning */
void push(struct Node **head_ref, 
          int new_data)
{
    struct Node *new_node =
    (struct Node *)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = *head_ref;
    *head_ref = new_node;
}

/* Utility function to print a 
   linked list */
void printList(struct Node *head)
{
    while(head!=NULL)
    {
        printf("%d ",head->data);
        head=head->next;
    }
    printf("");
}

// Driver code
int main()
{
    struct Node *head = NULL;

    /* Create following linked list
       12->15->10->11->5->6->2->3 */
    push(&head,3);
    push(&head,2);
    push(&head,6);
    push(&head,5);
    push(&head,11);
    push(&head,10);
    push(&head,15);
    push(&head,12);

    printf("Given Linked List: ");
    printList(head);

    /* Let us delete the node with 
       value 10 */
    printf("
    Deleting node %d: ", 
    head->next->next->data);
    deleteNode(head, 
               head->next->next);

    printf(
    "Modified Linked List: ");
    printList(head);

    // Let us delete the first node 
    printf(
    "Deleting first node ");
    deleteNode(head, head);

    printf(
    "Modified Linked List: ");
    printList(head);

    getchar();
    return 0;
}
```

**输出:**

```
Given Linked List: 12 15 10 11 5 6 2 3

Deleting node 10:
Modified Linked List: 12 15 11 5 6 2 3

Deleting first node
Modified Linked List: 15 11 5 6 2 3
```

详情请参考[在给定约束下删除链表中给定节点](https://www.geeksforgeeks.org/delete-a-given-node-in-linked-list-under-given-constraints/)的完整文章！