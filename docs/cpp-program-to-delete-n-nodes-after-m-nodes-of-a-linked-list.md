# C++程序删除链表 M 个节点后的 N 个节点

> 原文:[https://www . geesforgeks . org/CPP-program-to-delete-n-nodes-after-m-nodes-of-a-link-list/](https://www.geeksforgeeks.org/cpp-program-to-delete-n-nodes-after-m-nodes-of-a-linked-list/)

给定一个链表和两个整数 M 和 N。遍历链表，保留 M 个节点，然后删除下 N 个节点，一直到链表结束。
难度等级:菜鸟
**示例:**

```
Input:
M = 2, N = 2
Linked List: 1->2->3->4->5->6->7->8
Output:
Linked List: 1->2->5->6

Input:
M = 3, N = 2
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->2->3->6->7->8

Input:
M = 1, N = 1
Linked List: 1->2->3->4->5->6->7->8->9->10
Output:
Linked List: 1->3->5->7->9
```

问题的主要部分是维护节点之间的适当链接，确保所有的角落案例都得到处理。下面是 skipMdeleteN()函数的 C 实现，它跳过 M 个节点，删除 N 个节点，直到列表结束。假设 M 不能为 0。

## C++

```
// C++ program to delete N nodes
// after M nodes of a linked list 
#include <bits/stdc++.h>
using namespace std;

// A linked list node 
class Node 
{ 
    public:
    int data; 
    Node *next; 
}; 

/* Function to insert a node 
   at the beginning */
void push(Node ** head_ref, 
          int new_data) 
{ 
    // Allocate node 
    Node* new_node = new Node();

    // Put in the data 
    new_node->data = new_data; 

    // Link the old list off the 
    // new node 
    new_node->next = (*head_ref); 

    // Move the head to point to 
    // the new node 
    (*head_ref) = new_node; 
} 

// Function to print linked list 
void printList(Node *head) 
{ 
    Node *temp = head; 
    while (temp != NULL) 
    { 
        cout<<temp->data<<" "; 
        temp = temp->next; 
    } 
    cout<<endl; 
} 

// Function to skip M nodes and then
// delete N nodes of the linked list. 
void skipMdeleteN(Node *head, 
                  int M, int N) 
{ 
    Node *curr = head, *t; 
    int count; 

    // The main loop that traverses
    // through the whole list 
    while (curr) 
    { 
        // Skip M nodes 
        for (count = 1; count < M && 
             curr!= NULL; count++) 
            curr = curr->next; 

        // If we reached end of list, 
        // then return 
        if (curr == NULL) 
            return; 

        // Start from next node and delete 
        // N nodes 
        t = curr->next; 
        for (count = 1; count<=N && 
             t!= NULL; count++) 
        { 
            Node *temp = t; 
            t = t->next; 
            free(temp); 
        } 

        // Link the previous list with 
        // remaining nodes 
        curr->next = t; 

        // Set current pointer for next 
        // iteration 
        curr = t; 
    } 
} 

// Driver code 
int main() 
{ 
    /* Create following linked list 
       1->2->3->4->5->6->7->8->9->10 */
    Node* head = NULL; 
    int M=2, N=3; 
    push(&head, 10); 
    push(&head, 9); 
    push(&head, 8); 
    push(&head, 7); 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    cout << "M = " << M<< " N = " << 
             N << "Given Linked list is :"; 
    printList(head); 

    skipMdeleteN(head, M, N); 

    cout<<"Linked list after deletion is :"; 
    printList(head); 

    return 0; 
} 
// This code is contributed by rathbhupendra
```

**输出:**

```
M = 2, N = 3
Given Linked list is :
1 2 3 4 5 6 7 8 9 10
Linked list after deletion is :
1 2 6 7
```

**时间复杂度:**
O(n)，其中 n 为链表中的节点数。

更多详情请参考完整文章[删除链表](https://www.geeksforgeeks.org/delete-n-nodes-after-m-nodes-of-a-linked-list/)M 个节点后的 N 个节点！