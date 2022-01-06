# 用于比较两个表示为链表的字符串的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-用于比较两个字符串的程序-表示为链表/](https://www.geeksforgeeks.org/cpp-program-for-comparing-two-strings-represented-as-linked-lists/)

给定两个字符串，表示为链表(每个字符都是链表中的一个节点)。编写一个与 strcmp()类似的函数 compare()，即如果两个字符串相同，则返回 0，如果第一个链表在字典序上更大，则返回 1，如果第二个字符串在字典序上更大，则返回-1。
**例:**

```
Input: list1 = g->e->e->k->s->a
       list2 = g->e->e->k->s->b
Output: -1

Input: list1 = g->e->e->k->s->a
       list2 = g->e->e->k->s
Output: 1

Input: list1 = g->e->e->k->s
       list2 = g->e->e->k->s
Output: 0
```

## C++

```
// C++ program to compare two strings 
// represented as linked lists
#include<bits/stdc++.h>
using namespace std;

// Linked list Node 
// structure
struct Node
{
    char c;
    struct Node *next;
};

// Function to create newNode 
// in a linkedlist
Node* newNode(char c)
{
    Node *temp = new Node;
    temp->c = c;
    temp->next = NULL;
    return temp;
};

int compare(Node *list1, 
            Node *list2) 
{    
    // Traverse both lists. Stop when 
    // either end of a linked list is 
    // reached or current characters 
    // don't match
    while (list1 && list2 && 
           list1->c == list2->c) 
    {         
        list1 = list1->next;
        list2 = list2->next;
    }

    //  If both lists are not empty, 
    // compare mismatching characters
    if (list1 && list2) 
        return ((list1->c > 
                 list2->c)? 1: -1);

    // If either of the two lists has 
    // reached end
    if (list1 && !list2) return 1;
    if (list2 && !list1) return -1;

    // If none of the above conditions 
    // is true, both lists have reached 
    // end 
    return 0;
}

// Driver code
int main()
{
    Node *list1 = newNode('g');
    list1->next = newNode('e');
    list1->next->next = newNode('e');
    list1->next->next->next = 
           newNode('k');
    list1->next->next->next->next = 
           newNode('s');
    list1->next->next->next->next->next = 
           newNode('b');

    Node *list2 = newNode('g');
    list2->next = newNode('e');
    list2->next->next = newNode('e');
    list2->next->next->next = 
           newNode('k');
    list2->next->next->next->next =  
           newNode('s');
    list2->next->next->next->next->next = 
           newNode('a');

    cout << compare(list1, list2); 
    return 0;
}
```

**输出:**

```
1
```

更多详细信息，请参考完整的文章[比较两个链表表示的字符串](https://www.geeksforgeeks.org/compare-two-strings-represented-as-linked-lists/)！