# 用于排序已按绝对值排序的链表的 C++程序

> 原文:[https://www . geeksforgeeks . org/CPP-用于排序的程序-链表-绝对值排序/](https://www.geeksforgeeks.org/cpp-program-for-sorting-linked-list-which-is-already-sorted-on-absolute-values/)

给定一个基于绝对值排序的链表。根据实际值对列表进行排序。
**例:**

```
Input:  1 -> -10 
Output: -10 -> 1

Input: 1 -> -2 -> -3 -> 4 -> -5 
Output: -5 -> -3 -> -2 -> 1 -> 4 

Input: -5 -> -10 
Output: -10 -> -5

Input: 5 -> 10 
Output: 5 -> 10
```

来源:[亚马逊采访](https://www.geeksforgeeks.org/amazon-interview-experience-set-258-for-sde1/)

一个简单的解决方案是从头到尾遍历链表。对于每个被访问的节点，检查它是否有问题。如果是，将其从当前位置移除，并将其插入正确的位置。这是链表的[插入排序的实现，这个解决方案的时间复杂度是 O(n*n)。
更好的解决方案是](http://geeksquiz.com/insertion-sort-for-singly-linked-list/)[使用合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)对链表进行排序。这个解决方案的时间复杂度是 O(n Log n)。
高效的解决方案可以在 O(n)时间内工作。一个重要的观察是，所有的负元素都以相反的顺序出现。所以我们遍历列表，每当我们发现一个元素有问题，我们就把它移到链表的前面。
以下是上述思路的实现。

一旦我们发现一个元素有问题，我们就把它移到链表的前面。
以下是上述思路的实现。

## C++

```
// C++ program to sort a linked list, 
// already sorted by absolute values
#include <bits/stdc++.h>
using namespace std;

// Linked List Node
struct Node
{
    Node* next;
    int data;
};

// Utility function to insert a 
// node at the beginning
void push(Node** head, int data)
{
    Node* newNode = new Node;
    newNode->next = (*head);
    newNode->data = data;
    (*head) = newNode;
}

// Utility function to print 
// a linked list
void printList(Node* head)
{
    while (head != NULL)
    {
        cout << head->data;
        if (head->next != NULL)
            cout << " -> ";
        head = head->next;
    }
    cout<<endl;
}

// To sort a linked list by actual values.
// The list is assumed to be sorted by 
// absolute values.
void sortList(Node** head)
{
    // Initialize previous and current 
    // nodes
    Node* prev = (*head);
    Node* curr = (*head)->next;

    // Traverse list
    while (curr != NULL)
    {
        // If curr is smaller than prev, 
        // then it must be moved to head
        if (curr->data < prev->data)
        {
            // Detach curr from linked list
            prev->next = curr->next;

            // Move current node to beginning
            curr->next = (*head);
            (*head) = curr;

            // Update current
            curr = prev;
        }

        // Nothing to do if current 
        // element is at right place
        else
            prev = curr;

        // Move current
        curr = curr->next;
    }
}

// Driver code
int main()
{
    Node* head = NULL;
    push(&head, -5);
    push(&head, 5);
    push(&head, 4);
    push(&head, 3);
    push(&head, -2);
    push(&head, 1);
    push(&head, 0);

    cout << "Original list :";
    printList(head);

    sortList(&head);

    cout << "Sorted list :";
    printList(head);

    return 0;
}
```

**输出:**

```
Original list :
0 -> 1 -> -2 -> 3 -> 4 -> 5 -> -5
Sorted list :
-5 -> -2 -> 0 -> 1 -> 3 -> 4 -> 5
```

详见[排序链表整篇文章，该链表已经按绝对值](https://www.geeksforgeeks.org/sort-linked-list-already-sorted-absolute-values/)排序！