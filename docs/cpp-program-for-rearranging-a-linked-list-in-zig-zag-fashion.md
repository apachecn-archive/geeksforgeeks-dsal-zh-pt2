# 用于以之字形方式重新排列链表的 C++程序

> 原文:[https://www . geeksforgeeks . org/CPP-program-for-rewarding-a-link-list-in-zig-zag-fashion/](https://www.geeksforgeeks.org/cpp-program-for-rearranging-a-linked-list-in-zig-zag-fashion/)

给定一个链表，重新排列它，使得转换后的列表应该是 a < b > c < d > e < f …的形式，其中 a，b，c…是链表的连续数据节点。

**示例:**

```
Input:  1->2->3->4
Output: 1->3->2->4 
Explanation: 1 and 3 should come first before 2 and 4 in
             zig-zag fashion, So resultant linked-list 
             will be 1->3->2->4\. 

Input:  11->15->20->5->10
Output: 11->20->5->15->10 
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/probfunc-page.php?pid=700085)

一个简单的方法是使用合并排序对链表进行排序，然后交换替换，但是这需要 O(n Log n)的时间复杂度。这里 n 是链表中的元素个数。

一种需要 O(n)时间的**有效方法是，使用类似于冒泡排序的单次扫描，然后维护一个标志来表示我们当前所处的顺序()。如果当前的两个元素不是按这个顺序排列的，那么交换这些元素，否则就不是。关于对换顺序的详细说明，请参考[本](http://geeksquiz.com/converting-an-array-of-integers-into-zig-zag-fashion/)。**

## C++

```
// C++ program to arrange linked
// list in zigzag fashion
#include <bits/stdc++.h>
using namespace std;

// Link list Node 
struct Node 
{
    int data;
    struct Node* next;
};

// This function distributes the
// Node in zigzag fashion
void zigZagList(Node* head)
{
    // If flag is true, then next
    // node should be greater
    // in the desired output.
    bool flag = true;

    // Traverse linked list starting 
    // from head.
    Node* current = head;
    while (current->next != NULL) 
    {
        // "<" relation expected 
        if (flag) 
        {
            /* If we have a situation like 
               A > B > C where A, B and C 
               are consecutive Nodes in list 
               we get A > B < C by swapping B
               and C */
            if (current->data > 
                current->next->data)
                swap(current->data, 
                     current->next->data);
        }
        // ">" relation expected 
        else 
        {
            /* If we have a situation like 
               A < B < C where A, B and C  
               are consecutive Nodes in list we
               get A < C > B by swapping B and C */
            if (current->data < 
                current->next->data)
                swap(current->data, 
                     current->next->data);
        }

        current = current->next;

        // flip flag for reverse checking 
        flag = !flag; 
    }
}

// UTILITY FUNCTIONS 
// Function to push a Node 
void push(Node** head_ref, 
          int new_data)
{
    // Allocate Node 
    struct Node* new_Node = new Node;

    // Put in the data  
    new_Node->data = new_data;

    // Link the old list off the 
    // new Node 
    new_Node->next = (*head_ref);

    // Move the head to point to 
    // the new Node 
    (*head_ref) = new_Node;
}

// Function to print linked list 
void printList(struct Node* Node)
{
    while (Node != NULL) 
    {
        printf("%d->", Node->data);
        Node = Node->next;
    }
    printf("NULL");
}

// Driver code
int main(void)
{
    // Start with the empty list 
    struct Node* head = NULL;

    // create a list 4 -> 3 -> 7 -> 
    // 8 -> 6 -> 2 -> 1 
    // answer should be -> 3  7  4  
    // 8  2  6  1
    push(&head, 1);
    push(&head, 2);
    push(&head, 6);
    push(&head, 8);
    push(&head, 7);
    push(&head, 3);
    push(&head, 4);

    printf("Given linked list ");
    printList(head);

    zigZagList(head);

    printf("Zig Zag Linked list ");
    printList(head);

    return (0);
}
```

**输出:**

```
Given linked list 
4->3->7->8->6->2->1->NULL
Zig Zag Linked list 
3->7->4->8->2->6->1->NULL
```

更多详情请参考[以之字形方式重新排列链表](https://www.geeksforgeeks.org/linked-list-in-zig-zag-fashion/)的完整文章！