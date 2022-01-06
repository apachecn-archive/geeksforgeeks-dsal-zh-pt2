# 用下一个随机指针集克隆链表的 C++程序 2

> 原文:[https://www . geesforgeks . org/CPP-克隆程序-带有下一个随机指针集的链表-2/](https://www.geeksforgeeks.org/cpp-program-for-cloning-a-linked-list-with-next-and-random-pointer-set-2/)

我们已经讨论了克隆链表的两种不同方法。在[这篇](https://www.geeksforgeeks.org/a-linked-list-with-next-and-arbit-pointer/)的帖子中，讨论了一个更简单的克隆链表的方法。

想法是使用哈希。下面是算法。

1.  遍历原始链表，根据数据进行复制。
2.  制作一个键值对与原始链表节点和复制链表节点的哈希映射。
3.  再次遍历原始链表，并使用哈希映射调整克隆链表节点的下一个随机引用。

下面是上述方法的实现。

## C++

```
// C++ program to clone a linked list 
// with random pointers
#include<bits/stdc++.h>
using namespace std;

// Linked List Node
class Node
{
    public:

    // Node data
    int data;

    // Next and random reference
    Node *next, *random;

    Node(int data)
    {
        this->data = data;
        this->next = 
        this->random = NULL;
    }
};

// Linked list class
class LinkedList
{
    public:

    // Linked list head reference
    Node *head;

    LinkedList(Node *head)
    {
        this->head = head;
    }

    // Push method to put data always at
    // the head in the linked list.
    void push(int data)
    {
        Node *node = new Node(data);
        node->next = head;
        head = node;
    }

    // Method to print the list.
    void print()
    {
        Node *temp = head;
        while (temp != NULL)
        {
            Node *random = temp->random;
            int randomData = ((random != NULL) ?
                               random->data : -1);
            cout << "Data = " << 
                    temp->data << ", ";
            cout << "Random Data = " << 
                     randomData << endl;
            temp = temp->next;
        }
        cout << endl;
    }

    // Actual clone method which returns
    // head reference of cloned linked
    // list.
    LinkedList* clone()
    {
        // Initialize two references,
        // one with original list's head.
        Node *origCurr = head;
        Node *cloneCurr = NULL;

        // Hash map which contains node 
        // to node mapping of original 
        // and clone linked list.
        unordered_map<Node*, Node*> mymap;

        // Traverse the original list and
        // make a copy of that in the 
        // clone linked list.
        while (origCurr != NULL)
        {
            cloneCurr = new Node(origCurr->data);
            mymap[origCurr] = cloneCurr;
            origCurr = origCurr->next;
        }

        // Adjusting the original list 
        // reference again.
        origCurr = head;

        // Traversal of original list again
        // to adjust the next and random 
        // references of clone list using 
        // hash map.
        while (origCurr != NULL)
        {
            cloneCurr = mymap[origCurr];
            cloneCurr->next = 
            mymap[origCurr->next];
            cloneCurr->random = 
            mymap[origCurr->random];
            origCurr = origCurr->next;
        }

        // return the head reference of 
        // the clone list.
        return new LinkedList(mymap[head]);
    }
};

// Driver code
int main()
{
    // Pushing data in the linked list.
    LinkedList *mylist = 
                new LinkedList(new Node(5));
    mylist->push(4);
    mylist->push(3);
    mylist->push(2);
    mylist->push(1);

    // Setting up random references.
    mylist->head->random = 
    mylist->head->next->next;

    mylist->head->next->random =
    mylist->head->next->next->next;

    mylist->head->next->next->random =
    mylist->head->next->next->next->next;

    mylist->head->next->next->next->random =
    mylist->head->next->next->next->next->next;

    mylist->head->next->next->next->next->random =
    mylist->head->next;

    // Making a clone of the original
    // linked list.
    LinkedList *clone = mylist->clone();

    // Print the original and cloned 
    // linked list.
    cout << "Original linked list";
    mylist->print();
    cout << "Cloned linked list";
    clone->print();
}
// This code is contributed by Chhavi
```

**输出:**

```
Original linked list
Data = 1, Random data = 3
Data = 2, Random data = 4
Data = 3, Random data = 5
Data = 4, Random data = -1
Data = 5, Random data = 2

Cloned linked list
Data = 1, Random data = 3
Data = 2, Random data = 4
Data = 3, Random data = 5
Data = 4, Random data = -1
Data = 5, Random data = 2
```

**时间复杂度:**O(n)
T3】辅助空间 : O(n)
更多详情请参考[克隆一个带有 next 和随机指针的链表| Set 2](https://www.geeksforgeeks.org/clone-linked-list-next-arbit-pointer-set-2/) 完整文章！