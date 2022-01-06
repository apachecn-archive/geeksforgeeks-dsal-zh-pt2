# 删除链表中间的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-程序-删除-链表中间/](https://www.geeksforgeeks.org/cpp-program-to-delete-middle-of-linked-list/)

给定一个单链表，删除链表的中间。例如，如果给定的链表是 1->2->3->4->5，那么链表应该被修改为 1->2->4->5

如果有偶数个节点，那么就会有两个中间节点，我们需要删除第二个中间元素。例如，如果给定的链表是 1->2->3->4->5->6，那么它应该被修改为 1->2->3->5->6。
如果输入链表为空，那么应该保持为空。

如果输入的链表有 1 个节点，那么这个节点应该被删除，并返回一个新的头。

**简单的解决方案:**思路是先统计链表中的节点数，然后用简单的删除过程删除第 n/2 个节点。

## C++14

```
// C++ program to delete middle
// of a linked list
#include <bits/stdc++.h>
using namespace std;

// Link list Node 
struct Node 
{
    int data;
    struct Node* next;
};

// Count of nodes
int countOfNodes(struct Node* head)
{
    int count = 0;
    while (head != NULL) 
    {
        head = head->next;
        count++;
    }
    return count;
}

// Deletes middle node and returns
// head of the modified list
struct Node* deleteMid(struct Node* head)
{
    // Base cases
    if (head == NULL)
        return NULL;
    if (head->next == NULL) 
    {
        delete head;
        return NULL;
    }
    struct Node* copyHead = head;

    // Find the count of nodes
    int count = countOfNodes(head);

    // Find the middle node
    int mid = count / 2;

    // Delete the middle node
    while (mid-- > 1) 
    {
        head = head->next;
    }

    // Delete the middle node
    head->next = head->next->next;

    return copyHead;
}

// A utility function to print
// a given linked list
void printList(struct Node* ptr)
{
    while (ptr != NULL) 
    {
        cout << ptr->data << "->";
        ptr = ptr->next;
    }
    cout << "NULL";
}

// Utility function to create 
// a new node.
Node* newNode(int data)
{
    struct Node* temp = new Node;
    temp->data = data;
    temp->next = NULL;
    return temp;
}

// Driver code
int main()
{
    // Start with the empty list 
    struct Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = newNode(3);
    head->next->next->next = newNode(4);

    cout << "Given Linked List";
    printList(head);
    head = deleteMid(head);
    cout << "Linked List after deletion of middle";
    printList(head);
    return 0;
}
```

**输出:**

```
Given Linked List
1->2->3->4->NULL
Linked List after deletion of middle
1->2->4->NULL
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    链表需要两次遍历
*   **辅助空间:** O(1)。
    不需要额外的空间。

**高效解决方案:**
**方法:**上述解决方案需要链表的两次遍历。中间节点可以通过一次遍历删除。想法是使用两个指针，slow_ptr 和 fast_ptr。两个指针都从列表头开始。当 fast_ptr 到达终点时，slow_ptr 到达中间。这个思路和[这个](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)帖子的方法二用的是一样的。这篇文章的额外内容是跟踪前一个中间节点，这样中间节点就可以被删除了。

下面是实现。

## C++

```
// C++ program to delete middle
// of a linked list
#include <bits/stdc++.h>
using namespace std;

// Link list Node 
struct Node 
{
    int data;
    struct Node* next;
};

// Deletes middle node and returns 
// head of the modified list
struct Node* deleteMid(struct Node* head)
{
    // Base cases
    if (head == NULL)
        return NULL;
    if (head->next == NULL) 
    {
        delete head;
        return NULL;
    }

    // Initialize slow and fast pointers
    // to reach middle of linked list
    struct Node* slow_ptr = head;
    struct Node* fast_ptr = head;

    // Find the middle and previous 
    // of middle.
    // To store previous of slow_ptr    
    struct Node* prev; 
    while (fast_ptr != NULL && 
           fast_ptr->next != NULL) 
    {
        fast_ptr = fast_ptr->next->next;
        prev = slow_ptr;
        slow_ptr = slow_ptr->next;
    }

    // Delete the middle node
    prev->next = slow_ptr->next;
    delete slow_ptr;

    return head;
}

// A utility function to print 
// a given linked list
void printList(struct Node* ptr)
{
    while (ptr != NULL) 
    {
        cout << ptr->data << "->";
        ptr = ptr->next;
    }
    cout << "NULL";
}

// Utility function to create 
// a new node.
Node* newNode(int data)
{
    struct Node* temp = new Node;
    temp->data = data;
    temp->next = NULL;
    return temp;
}

// Driver code
int main()
{
    // Start with the empty list 
    struct Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = newNode(3);
    head->next->next->next = newNode(4);

    cout << "Given Linked List";
    printList(head);
    head = deleteMid(head);
    cout << "Linked List after deletion of middle";
    printList(head);
    return 0;
}
```

**输出:**

```
Given Linked List
1->2->3->4->NULL
Linked List after deletion of middle
1->2->4->NULL
```

**复杂度分析:**

*   **时间复杂度:** O(n)。
    只需要遍历链表一次
*   **辅助空间:** O(1)。
    因为不需要额外的空间。

详情请参考[删除链表中间](https://www.geeksforgeeks.org/delete-middle-of-linked-list/)整篇文章！