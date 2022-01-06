# 从线段链表中删除中间点的 C 程序

> 原文:[https://www . geesforgeks . org/c-从线段链表中删除中间点的程序/](https://www.geeksforgeeks.org/c-program-for-removing-middle-points-from-a-linked-list-of-line-segments/)

给定相邻点形成垂直线或水平线的坐标链表。从链表中删除水平线或垂直线中间的点。
**例:**

```
Input:   (0,10)->(1,10)->(5,10)->(7,10)
                                  |
                                (7,5)->(20,5)->(40,5)
Output: Linked List should be changed to following
        (0,10)->(7,10)
                  |
                (7,5)->(40,5) 
The given linked list represents a horizontal line from (0,10) 
to (7, 10) followed by a vertical line from (7, 10) to (7, 5), 
followed by a horizontal line from (7, 5) to (40, 5).

Input: (2,3)->(4,3)->(6,3)->(10,3)->(12,3)
Output: Linked List should be changed to following
    (2,3)->(12,3) 
There is only one vertical line, so all middle points are removed.
```

**来源:** [微软面试体验](https://www.geeksforgeeks.org/microsoft-interview-experience-set-41-campus/)

其思想是跟踪当前节点、下一个节点和下一个节点。当下一个节点与下一个节点相同时，继续删除下一个节点。在这个完整的过程中，我们需要关注指针的移动并检查空值。
以下是上述想法的实现。

## C

```
// C program to remove intermediate points 
// in a linked list that represents horizontal 
// and vertical line segments
#include <stdio.h>
#include <stdlib.h>

// Node has 3 fields including x, y 
// coordinates and a pointer to next 
// node
struct Node
{
    int x, y;
    struct Node *next;
};

/* Function to insert a node at 
   the beginning */
void push(struct Node ** head_ref, 
          int x,int y)
{
    struct Node* new_node = 
           (struct Node*) malloc(sizeof(struct Node));
    new_node->x = x;
    new_node->y = y;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

/* Utility function to print 
   a singly linked list */
void printList(struct Node *head)
{
    struct Node *temp = head;
    while (temp != NULL)
    {
        printf("(%d,%d)-> ", 
                 temp->x, temp->y);
        temp = temp->next;
    }
    printf("");

}

// Utility function to remove Next from 
// linked list and link nodes after it 
// to head
void deleteNode(struct Node *head, 
                struct Node *Next)
{
    head->next = Next->next;
    Next->next = NULL;
    free(Next);
}

// This function deletes middle nodes 
// in a sequence of horizontal and 
// vertical line segments represented 
// by linked list.
struct Node* deleteMiddle(struct Node *head)
{
    // If only one node or no node...
    // Return back
    if (head == NULL || head->next == NULL || 
        head->next->next == NULL)
        return head;

    struct Node* Next = head->next;
    struct Node *NextNext = Next->next ;

    // Check if this is a vertical line 
    // or horizontal line
    if (head->x == Next->x)
    {
        // Find middle nodes with same x 
        // value, and delete them
        while (NextNext != NULL && 
               Next->x == NextNext->x)
        {
            deleteNode(head, Next);

            // Update Next and NextNext for 
            // next iteration
            Next = NextNext;
            NextNext = NextNext->next;
        }
    }

    // If horizontal line
    else if (head->y == Next->y) 
    {
        // Find middle nodes with same y 
        // value, and delete them
        while (NextNext != NULL && 
               Next->y == NextNext->y)
        {
            deleteNode(head, Next);

            // Update Next and NextNext for 
            // next iteration
            Next = NextNext;
            NextNext = NextNext->next;
        }
    }

    // Adjacent points must have either 
    // same x or same y
    else  
    {
        puts("Given linked list is not valid");
        return NULL;
    }

    // Recur for next segment
    deleteMiddle(head->next);

    return head;
}

// Driver code
int main()
{
    struct Node *head = NULL;

    push(&head, 40,5);
    push(&head, 20,5);
    push(&head, 10,5);
    push(&head, 10,8);
    push(&head, 10,10);
    push(&head, 3,10);
    push(&head, 1,10);
    push(&head, 0,10);
    printf("Given Linked List: ");
    printList(head);

    if (deleteMiddle(head) != NULL);
    {
        printf("Modified Linked List: ");
        printList(head);
    }
    return 0;
}
```

**输出:**

```
Given Linked List:
(0,10)-> (1,10)-> (3,10)-> (10,10)-> (10,8)-> (10,5)-> (20,5)-> (40,5)->
Modified Linked List:
(0,10)-> (10,10)-> (10,5)-> (40,5)-> 
```

**上述解决方案的时间复杂度**为 O(n)，其中 n 为给定链表中的节点数。
**练习:**
上面的代码是递归的，为同样的问题写一个迭代代码。请参见下面的解决方案。[删除线段链表中点的迭代方法](https://www.geeksforgeeks.org/iterative-approach-for-removing-middle-points-in-a-linked-list-of-line-segements/)
请参考完整的文章[给定线段链表，删除中点](https://www.geeksforgeeks.org/given-linked-list-line-segments-remove-middle-points/)了解更多细节！