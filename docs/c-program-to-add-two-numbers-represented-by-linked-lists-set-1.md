# 用链表表示的两个数相加的 C 程序-集合 1

> 原文:[https://www . geesforgeks . org/c-program-add-two-numbers-由链表表示-set-1/](https://www.geeksforgeeks.org/c-program-to-add-two-numbers-represented-by-linked-lists-set-1/)

给定两个由两个列表表示的数字，编写一个返回求和列表的函数。求和列表是两个输入数字相加的列表表示。

**例**:

```
Input: 
List1: 5->6->3 // represents number 563 
List2: 8->4->2 // represents number 842 
Output: 
Resultant list: 1->4->0->5 // represents number 1405 
Explanation: 563 + 842 = 1405

Input: 
List1: 7->5->9->4->6 // represents number 75946
List2: 8->4 // represents number 84
Output: 
Resultant list: 7->6->0->3->0// represents number 76030
Explanation: 75946+84=76030

```

**接近**:遍历两个列表，逐个选择两个列表的节点，并添加值。如果总和大于 10，则进位为 1 并减少总和。如果一个列表中的元素比另一个列表中的多，则认为该列表的剩余值为 0。步骤如下:

1.  从头到尾遍历两个链表
2.  将相应链接列表中的两位数字相加。
3.  如果其中一个列表已到达末尾，则取 0 作为它的数字。
4.  继续下去，直到两个列表都结束。
5.  如果两位数之和大于 9，则将进位设置为 1，将当前数字设置为*和% 10*

下面是这个方法的实现。

## C

```
// C program to implement the
// above approach
#include <stdio.h>
#include <stdlib.h>

// Linked list node 
struct Node 
{
    int data;
    struct Node* next;
};

/* Function to create a new node 
   with given data */
struct Node* newNode(int data)
{
    struct Node* new_node = 
           (struct Node*)malloc(sizeof(struct Node));
    new_node->data = data;
    new_node->next = NULL;
    return new_node;
}

/* Function to insert a node at the 
   beginning of the Singly Linked List */
void push(struct Node** head_ref, 
          int new_data)
{
    // Allocate node 
    struct Node* new_node = newNode(new_data);

    // Link the old list off the new node 
    new_node->next = (*head_ref);

    // Move the head to point to the 
    // new node 
    (*head_ref) = new_node;
}

/* Adds contents of two linked
   lists and return the head node
   of resultant list */
struct Node* addTwoLists(struct Node* first,
                         struct Node* second)
{
    // res is head node of the resultant 
    // list
    struct Node* res = NULL;
    struct Node *temp, *prev = NULL;
    int carry = 0, sum;

    // while both lists exist
    while (first != NULL || 
           second != NULL) 
    {
        // Calculate value of next digit in 
        // resultant list. The next digit is 
        // sum of following things
        // (i)  Carry
        // (ii) Next digit of first
        // list (if there is a next digit)
        // (ii) Next digit of second
        // list (if there is a next digit)
        sum = carry + (first ? first->data : 0) + 
              (second ? second->data : 0);

        // Update carry for next calculation
        carry = (sum >= 10) ? 1 : 0;

        // Update sum if it is greater than 10
        sum = sum % 10;

        // Create a new node with sum as data
        temp = newNode(sum);

        // If this is the first node then
        // set it as head of the resultant 
        // list
        if (res == NULL)
            res = temp;

        // If this is not the first node
        // then connect it to the rest.
        else
            prev->next = temp;

        // Set prev for next insertion
        prev = temp;

        // Move first and second pointers to 
        // next nodes
        if (first)
            first = first->next;
        if (second)
            second = second->next;
    }

    if (carry > 0)
        temp->next = newNode(carry);

    // return head of the resultant list
    return res;
}

// A utility function to print a 
// linked list
void printList(struct Node* node)
{
    while (node != NULL) 
    {
        printf("%d ", node->data);
        node = node->next;
    }
    printf("");
}

// Driver code
int main(void)
{
    struct Node* res = NULL;
    struct Node* first = NULL;
    struct Node* second = NULL;

    // Create first list 7->5->9->4->6
    push(&first, 6);
    push(&first, 4);
    push(&first, 9);
    push(&first, 5);
    push(&first, 7);
    printf("First List is ");
    printList(first);

    // Create second list 8->4
    push(&second, 4);
    push(&second, 8);
    printf("Second List is ");
    printList(second);

    // Add the two lists and see result
    res = addTwoLists(first, second);
    printf("Resultant list is ");
    printList(res);

    return 0;
}
```

**输出:**

```
First List is 7 5 9 4 6 
Second List is 8 4 
Resultant list is 5 0 0 5 6 
```

**复杂度分析:**

*   **时间复杂度:** O(m + n)，其中 m 和 n 分别是第一和第二列表中的节点数。
    列表只需遍历一次。
*   **空间复杂度:** O(m + n)。
    需要一个临时链表来存储输出号

更多详情请参考[整篇文章添加两个链表表示的数字|集合 1](https://www.geeksforgeeks.org/add-two-numbers-represented-by-linked-lists/) ！