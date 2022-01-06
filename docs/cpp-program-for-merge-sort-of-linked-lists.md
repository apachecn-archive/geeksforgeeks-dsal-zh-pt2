# 用于链表合并排序的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-program-for-merge-sort-of-linked-list/](https://www.geeksforgeeks.org/cpp-program-for-merge-sort-of-linked-lists/)

[合并排序](http://en.wikipedia.org/wiki/Merge_sort)通常是对链表进行排序的首选。链表缓慢的随机访问性能使得其他一些算法(如 quicksort)性能很差，而其他算法(如 heapsort)则完全不可能。

![sorting image](img/cc3d3ac699ac03f5792746b3e3e54865.png)

让 head 是要排序的链表的第一个节点，headRef 是指向 head 的指针。请注意，我们需要引用 MergeSort()中的 head，因为下面的实现会更改下一个链接以对链表进行排序(而不是节点处的数据)，因此如果原始 head 处的数据不是链表中的最小值，就必须更改 head 节点。

```
MergeSort(headRef)
1) If the head is NULL or there is only one element in the Linked 
   List then return.
2) Else divide the linked list into two halves.  
      FrontBackSplit(head, &a, &b); /* a and b are two halves */
3) Sort the two halves a and b.
      MergeSort(a);
      MergeSort(b);
4) Merge the sorted a and b (using SortedMerge() discussed here) 
   and update the head pointer using headRef.
     *headRef = SortedMerge(a, b);
```

## C++

```
// C++ code for linked list merged sort
#include <bits/stdc++.h>
using namespace std;

// Link list node 
class Node 
{
    public:
    int data;
    Node* next;
};

// Function prototypes 
Node* SortedMerge(Node* a, 
                  Node* b);
void FrontBackSplit(Node* source,
                    Node** frontRef, 
                    Node** backRef);

// Sorts the linked list by changing 
// next pointers (not data) 
void MergeSort(Node** headRef)
{
    Node* head = *headRef;
    Node* a;
    Node* b;

    // Base case -- length 0 or 1 
    if ((head == NULL) || 
        (head->next == NULL)) 
    {
        return;
    }

    /* Split head into 'a' and 'b' 
       sublists */
    FrontBackSplit(head, &a, &b);

    // Recursively sort the sublists 
    MergeSort(&a);
    MergeSort(&b);

    /* answer = merge the two sorted 
       lists together */
    *headRef = SortedMerge(a, b);
}

/* See https:// www.geeksforgeeks.org/?p=3622 
   for details of this function */
Node* SortedMerge(Node* a, Node* b)
{
    Node* result = NULL;

    // Base cases 
    if (a == NULL)
        return (b);
    else if (b == NULL)
        return (a);

    /* Pick either a or b, and 
       recur */
    if (a->data <= b->data) 
    {
        result = a;
        result->next = 
                SortedMerge(a->next, b);
    }
    else 
    {
        result = b;
        result->next = 
                SortedMerge(a, b->next);
    }
    return (result);
}

// UTILITY FUNCTIONS 
/* Split the nodes of the given list into 
   front and back halves, and return the two 
   lists using the reference parameters. If 
   the length is odd, the extra node should 
   go in the front list. Uses the fast/slow 
   pointer strategy. */
void FrontBackSplit(Node* source,
                    Node** frontRef, 
                    Node** backRef)
{
    Node* fast;
    Node* slow;
    slow = source;
    fast = source->next;

    /* Advance 'fast' two nodes, and 
       advance 'slow' one node */
    while (fast != NULL) 
    {
        fast = fast->next;
        if (fast != NULL) 
        {
            slow = slow->next;
            fast = fast->next;
        }
    }

    /* 'slow' is before the midpoint in 
        the list, so split it in two at 
        that point. */
    *frontRef = source;
    *backRef = slow->next;
    slow->next = NULL;
}

/* Function to print nodes in a 
   given linked list */
void printList(Node* node)
{
    while (node != NULL) 
    {
        cout << node->data << " ";
        node = node->next;
    }
}

/* Function to insert a node at the 
   beginning of the linked list */
void push(Node** head_ref, int new_data)
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

// Driver code
int main()
{
    // Start with the empty list 
    Node* res = NULL;
    Node* a = NULL;

    /* Let us create a unsorted linked lists 
       to test the functions created lists shall 
       be a: 2->3->20->5->10->15 */
    push(&a, 15);
    push(&a, 10);
    push(&a, 5);
    push(&a, 20);
    push(&a, 3);
    push(&a, 2);

    // Sort the above created Linked List 
    MergeSort(&a);

    cout << "Sorted Linked List is: ";
    printList(a);

    return 0;
}
// This is code is contributed by rathbhupendra
```

**输出:**

```
Sorted Linked List is: 
2 3 5 10 15 20
```

**时间复杂度:** O(n*log n)

**空间复杂度:** O(n*log n)

**方法 2:** 这种方法比较简单，使用 log n 空间。

**mergeSort():**

1.  如果链表的大小是 1，那么返回头
2.  用龟兔赛跑法找到 mid
3.  将 mid 的下一个存储在 head2 中，即右子链表中。
4.  现在使下一个中点为空。
5.  递归调用左右子链表的 mergeSort()，并存储左右链表的新头。
6.  给定参数，调用 merge()创建左右子链表的新头，并存储合并后返回的最终头。
7.  返回合并链接列表的最后一个标题。

**合并(标题 1、标题 2):**

1.  取一个指针，比如说合并，将合并的列表存储在其中，并在其中存储一个虚拟节点。
2.  取一个指针 temp，并为其分配 merge。
3.  如果标题 1 的数据小于标题 2 的数据，则将标题 1 存储在 temp 的下一行，并将标题 1 移动到标题 1 的下一行。
4.  否则将标题 2 存储在 temp 的下一行，并将标题 2 移动到标题 2 的下一行。
5.  将温度移到下一个温度。
6.  重复步骤 3、4 和 5，直到标题 1 不等于空，标题 2 不等于空。
7.  现在将第一个或第二个链接列表的任何剩余节点添加到合并的链接列表中。
8.  返回下一个合并的(这将忽略哑元并返回最终合并链表的头部)

## C++

```
// C++ program to implement
// the above approach
#include<iostream>
using namespace std;

// Node structure
struct Node
{
    int data;
    Node *next;
};

// Function to insert in list
void insert(int x, Node **head) 
{
    if(*head == NULL)
    {
        *head = new Node;
        (*head)->data = x;
        (*head)->next = NULL;
        return;
    }

    Node *temp = new Node;
    temp->data = (*head)->data;
    temp->next = (*head)->next;
    (*head)->data = x;
    (*head)->next = temp;
}

// Function to print the list
void print(Node *head) 
{
    Node *temp = head;
    while(temp != NULL) 
    {
        cout << temp->data << " ";
        temp = temp->next;
    }
}

Node *merge(Node *firstNode,
            Node *secondNode) 
{
    Node *merged = new Node;
    Node *temp = new Node;

    // Merged is equal to temp so in the 
    // end we have the top Node.
    merged = temp;

    // while either firstNode or secondNode 
    // becomes NULL
    while(firstNode != NULL && 
          secondNode != NULL) 
    {    
        if(firstNode->data <= 
           secondNode->data) 
        {
            temp->next = firstNode;
            firstNode = firstNode->next;
        }

        else 
        {
            temp->next = secondNode;
            secondNode = secondNode->next;
        }
        temp = temp->next;
    }

   // Any remaining Node in firstNode or 
   // secondNode gets inserted in the temp 
   // List
    while(firstNode!=NULL) 
    {
        temp->next = firstNode;
        firstNode = firstNode->next;
        temp = temp->next;
    }

    while(secondNode!=NULL) 
    {
        temp->next = secondNode;
        secondNode = secondNode->next;
        temp = temp->next;
    }

    // Return the head of the sorted list
    return merged->next;
}

// Function to calculate the middle 
// Element
Node *middle(Node *head) 
{
    Node *slow = head;
    Node *fast = head->next;

    while(slow->next != NULL && 
         (fast!=NULL && fast->next!=NULL)) 
    {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}

// Function to sort the given list
Node *sort(Node *head)
{    
    if(head->next == NULL) 
    {
        return head;
    }

    Node *mid = new Node;
    Node *head2 = new Node;
    mid = middle(head);
    head2 = mid->next;   
    mid->next = NULL;

    // Recursive call to sort() hence diving 
    // our problem, and then merging the solution
    Node *finalhead = merge(sort(head),
                            sort(head2));  
    return finalhead;
}

int main(void) 
{
    Node *head = NULL;
    int n[] = {7, 10, 5, 20, 3, 2};
    for(int i = 0; i < 6; i++) 
    {
        // Inserting in the list
        insert(n[i], &head);   
    }

    cout << "Sorted Linked List is: ";

    // Printing the sorted list returned 
    // by sort()
    print(sort(head));     
    return 0;
}
```

**输出:**

```
Sorted Linked List is: 
2 3 5 7 10 20 
```

**时间复杂度** : O(n*log n)

**空间复杂度:** O(对数 n)

详情请参考[链表合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)整篇文章！