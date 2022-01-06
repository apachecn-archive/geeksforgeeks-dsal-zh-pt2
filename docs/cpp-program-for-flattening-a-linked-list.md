# 展平链表的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-program-for-扁平化-a-link-list/](https://www.geeksforgeeks.org/cpp-program-for-flattening-a-linked-list/)

给定一个链表，其中每个节点代表一个链表，并包含两个同类型的指针:

1.  指向主列表中下一个节点的指针(我们在下面的代码中称之为“右”指针)。
2.  指向该节点所在的链表的指针(我们在下面的代码中称之为“向下”指针)。

所有链接列表都已排序。请参见以下示例

```
       5 -> 10 -> 19 -> 28
       |    |     |     |
       V    V     V     V
       7    20    22    35
       |          |     |
       V          V     V
       8          50    40
       |                |
       V                V
       30               45
```

编写函数 flat()将列表展平为一个链表。展平的链表也应该排序。例如，对于上面的输入列表，输出列表应该是 5-> 7-> 8-> 10-> 19-> 20-> 22-> 28-> 30-> 35-> 40-> 45-> 50。

想法是使用[的 Merge()过程对链表进行合并排序。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)我们使用 merge()逐个合并列表。我们递归合并()当前列表和已经展平的列表。
向下指针用于链接展平列表的节点。

下面是上述方法的实现:

## C++

```
// C++ program for flattening a 
// Linked List
#include <bits/stdc++.h>
using namespace std;

// Link list node 
class Node
{
    public:
    int data;
    Node *right, *down;
};

Node* head = NULL;

// An utility function to merge 
// two sorted linked lists
Node* merge(Node* a, Node* b)
{    
    // If first linked list is empty 
    // then second is the answer
    if (a == NULL)
        return b;

    // If second linked list is empty 
    // then first is the result
    if (b == NULL)
        return a;

    // Compare the data members of the 
    // two linked lists and put the larger 
    // one in the result
    Node* result;

    if (a->data < b->data) 
    {
        result = a;
        result->down = merge(a->down, b);
    }

    else 
    {
        result = b;
        result->down = merge(a, b->down);
    }
    result->right = NULL;
    return result;
}

Node* flatten(Node* root)
{    
    // Base Cases
    if (root == NULL || 
        root->right == NULL)
        return root;

    // Recur for list on right
    root->right = flatten(root->right);

    // Now merge
    root = merge(root, root->right);

    // Return the root
    // It will be in turn merged 
    // with its left
    return root;
}

// Utility function to insert a node at
// beginning of the linked list
Node* push(Node* head_ref, int data)
{    
    // Allocate the Node & 
    // Put in the data
    Node* new_node = new Node();

    new_node->data = data;
    new_node->right = NULL;

    // Make next of new Node as head
    new_node->down = head_ref;

    // Move the head to point to 
    // new Node
    head_ref = new_node;

    return head_ref;
}

void printList()
{
    Node* temp = head;
    while (temp != NULL)
    {
        cout << temp->data << " ";
        temp = temp->down;
    }
    cout << endl;
}

// Driver code
int main()
{    
    /* Create the following linked list
        5 -> 10 -> 19 -> 28
        |    |     |     |
        V    V     V     V
        7    20    22    35
        |          |     |
        V          V     V
        8          50    40
        |                |
        V                V
        30               45
    */
    head = push(head, 30);
    head = push(head, 8);
    head = push(head, 7);
    head = push(head, 5);

    head->right = push(head->right, 20);
    head->right = push(head->right, 10);

    head->right->right = 
    push(head->right->right, 50);
    head->right->right = 
    push(head->right->right, 22);
    head->right->right = 
    push(head->right->right, 19);

    head->right->right->right = 
    push(head->right->right->right, 45);
    head->right->right->right = 
    push(head->right->right->right, 40);
    head->right->right->right = 
    push(head->right->right->right, 35);
    head->right->right->right = 
    push(head->right->right->right, 20);

    // Flatten the list
    head = flatten(head);

    printList();
    return 0;
}
// This code is contributed by rajsanghavi9.
```

**输出:**

```
5 7 8 10 19 20 20 22 30 35 40 45 50
```

更多详情请参考[整平链表](https://www.geeksforgeeks.org/flattening-a-linked-list/)整篇文章！