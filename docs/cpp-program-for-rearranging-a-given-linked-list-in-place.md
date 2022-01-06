# 就地重新排列给定链表的 C++程序。

> 原文:[https://www . geesforgeks . org/CPP-用于重新排列给定链接列表的程序-就地/](https://www.geeksforgeeks.org/cpp-program-for-rearranging-a-given-linked-list-in-place/)

给定一个单链表 L<sub>0</sub>->L<sub>1</sub>->……->L<sub>n-1</sub>->L<sub>n</sub>。重新排列列表中的节点，使新形成的列表为:L<sub>0</sub>->L<sub>n</sub>->L<sub>1</sub>->L<sub>n-1</sub>->L<sub>2</sub>->L<sub>n-2</sub>……
您需要在不改变节点值的情况下就地执行此操作。

**示例:**

```
Input: 1 -> 2 -> 3 -> 4
Output: 1 -> 4 -> 2 -> 3

Input: 1 -> 2 -> 3 -> 4 -> 5
Output: 1 -> 5 -> 2 -> 4 -> 3
```

**简单解决方案:**

```
1) Initialize current node as head.
2) While next of current node is not null, do following
    a) Find the last node, remove it from the end and insert it as next
       of the current node.
    b) Move current to next to next of current
```

上述简单解法的时间复杂度为 O(n <sup>2</sup> )，其中 n 为链表中的节点数。

**更好的解决方案:**
1)将给定链表的内容复制到一个向量。
2)通过交换两端的节点来重新排列给定的向量。
3)将修改后的向量复制回链表。
此方法的实施:[https://ide.geeksforgeeks.org/1eGSEy](https://ide.geeksforgeeks.org/1eGSEy)
感谢阿鲁什·达美佳提出此方法。

**高效解决方案:**

```
1) Find the middle point using tortoise and hare method.
2) Split the linked list into two halves using found middle point in step 1.
3) Reverse the second half.
4) Do alternate merge of first and second halves.
```

该解决方案的时间复杂度为 0(n)。

下面是这个方法的实现。

## C++

```
// C++ program to rearrange a 
// linked list in-place
#include <bits/stdc++.h>
using namespace std;

// Linkedlist Node structure
struct Node 
{
    int data;
    struct Node* next;
};

// Function to create newNode 
// in a linkedlist
Node* newNode(int key)
{
    Node* temp = new Node;
    temp->data = key;
    temp->next = NULL;
    return temp;
}

// Function to reverse the 
// linked list
void reverselist(Node** head)
{
    // Initialize prev and current 
    // pointers
    Node *prev = NULL, 
         *curr = *head, *next;

    while (curr) 
    {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }

    *head = prev;
}

// Function to print the 
// linked list
void printlist(Node* head)
{
    while (head != NULL) 
    {
        cout << head->data << " ";
        if (head->next)
            cout << "-> ";
        head = head->next;
    }
    cout << endl;
}

// Function to rearrange a 
// linked list
void rearrange(Node** head)
{
    // 1) Find the middle point using 
    // tortoise and hare method
    Node *slow = *head, 
         *fast = slow->next;
    while (fast && fast->next) 
    {
        slow = slow->next;
        fast = fast->next->next;
    }

    // 2) Split the linked list in 
    // two halves
    // head1, head of first half- 1 -> 2
    // head2, head of second half- 3 -> 4
    Node* head1 = *head;
    Node* head2 = slow->next;
    slow->next = NULL;

    // 3) Reverse the second half, 
    // i.e.,  4 -> 3
    reverselist(&head2);

    // 4) Merge alternate nodes
    // Assign dummy Node
    *head = newNode(0); 

    // curr is the pointer to this 
    // dummy Node, which will be 
    // used to form the new list
    Node* curr = *head;
    while (head1 || head2) 
    {
        // First add the element 
        // from list
        if (head1) 
        {
            curr->next = head1;
            curr = curr->next;
            head1 = head1->next;
        }

        // Then add the element from 
        // the second list
        if (head2) 
        {
            curr->next = head2;
            curr = curr->next;
            head2 = head2->next;
        }
    }

    // Assign the head of the new 
    // list to head pointer
    *head = (*head)->next;
}

// Driver program
int main()
{
    Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = newNode(3);
    head->next->next->next = newNode(4);
    head->next->next->next->next = newNode(5);

    printlist(head); // Print original list
    rearrange(&head); // Modify the list
    printlist(head); // Print modified list
    return 0;
}
```

**输出:**

```
1 -> 2 -> 3 -> 4 -> 5 
1 -> 5 -> 2 -> 4 -> 3
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
感谢高拉夫·阿希瓦尔提出上述方法。

**另一种做法:**
1。取两个指针 prev 和 curr，保存 head 和 head 的地址- >下一个。
2。比较他们的数据并交换。
之后，形成新的链表。

下面是实现:

## C++

```
// C++ code to rearrange linked list
// in place
#include <bits/stdc++.h>
using namespace std;

struct node 
{
    int data;
    struct node* next;
};
typedef struct node Node;

// Function for rearranging a 
// linked list with high and low
// value.
void rearrange(Node* head)
{
    // Base case.
    if (head == NULL) 
        return;

    // Two pointer variable.
    Node *prev = head, 
         *curr = head->next;

    while (curr) 
    {
        // Swap function for swapping data.
        if (prev->data > curr->data)
            swap(prev->data, curr->data);

        // Swap function for swapping data.
        if (curr->next && 
            curr->next->data > curr->data)
            swap(curr->next->data, curr->data);

        prev = curr->next;

        if (!curr->next)
            break;
        curr = curr->next->next;
    }
}

// Function to insert a node in the 
// linked list at the beginning.
void push(Node** head, int k)
{
    Node* tem = (Node*)malloc(sizeof(Node));
    tem->data = k;
    tem->next = *head;
    *head = tem;
}

// Function to display node of 
// linked list.
void display(Node* head)
{
    Node* curr = head;
    while (curr != NULL) 
    {
        printf("%d ", curr->data);
        curr = curr->next;
    }
}

// Driver code
int main()
{
    Node* head = NULL;

    // Let create a linked list.
    // 9 -> 6 -> 8 -> 3 -> 7
    push(&head, 7);
    push(&head, 3);
    push(&head, 8);
    push(&head, 6);
    push(&head, 9);

    rearrange(head);
    display(head);

    return 0;
}
```

**输出:**

```
6 9 3 8 7
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
感谢[阿迪蒂亚](https://auth.geeksforgeeks.org/user/aditya1011/articles)提出这个方法。

**另一种方法:**(使用递归)

1.  持有指向头节点的指针，并使用递归一直到最后一个节点
2.  到达最后一个节点后，开始将最后一个节点交换到下一个头节点
3.  将头指针移动到下一个节点
4.  重复此操作，直到头部和最后一个节点相遇或相邻
5.  一旦满足停止条件，我们需要丢弃左边的节点，以修复交换节点时在列表中创建的循环。

## C++

```
// C/C++ program to implement
// the above approach
#include <stdio.h>
#include <stdlib.h>

// Creating the structure 
// for node
struct Node 
{
    int data;
    struct Node* next;
};

// Function to create newNode 
// in a linkedlist
struct Node* newNode(int key)
{
    struct Node* temp = 
           malloc(sizeof(struct Node));
    temp->data = key;
    temp->next = NULL;
    return temp;
}

// Function to print the list
void printlist(struct Node* head)
{
    while (head) 
    {
        printf("%d ", head->data);
        if (head->next)
            printf("->");
        head = head->next;
    }
    printf("");
}

// Function to rearrange
void rearrange(struct Node** head, 
               struct Node* last)
{
    if (!last)
        return;

    // Recursive call
    rearrange(head, last->next);

    // (*head)->next will be set to NULL
    // after rearrangement.
    // Need not do any operation further
    // Just return here to come out of recursion
    if (!(*head)->next)
        return;

    // Rearrange the list until both head
    // and last meet or next to each other.
    if ((*head) != last && (*head)->next != last)
    {
        struct Node* tmp = (*head)->next;
        (*head)->next = last;
        last->next = tmp;
        *head = tmp;
    }
    else 
    {
        if ((*head) != last)
            *head = (*head)->next;
        (*head)->next = NULL;
    }
}

// Drivers Code
int main()
{
    struct Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = newNode(3);
    head->next->next->next = newNode(4);
    head->next->next->next->next = newNode(5);

    // Print original list
    printlist(head);

    struct Node* tmp = head;

    // Modify the list
    rearrange(&tmp, head);

    // Print modified list
    printlist(head);
    return 0;
}
```

**输出:**

```
1 ->2 ->3 ->4 ->5 
1 ->5 ->2 ->4 ->3
```

请参考[上的完整文章，就地重新排列给定的链表。](https://www.geeksforgeeks.org/rearrange-a-given-linked-list-in-place/)了解更多详情！