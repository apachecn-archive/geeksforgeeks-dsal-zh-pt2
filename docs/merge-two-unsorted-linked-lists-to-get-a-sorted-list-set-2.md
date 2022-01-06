# 合并两个未排序的链表，得到一个排序的链表–集合 2

> 原文:[https://www . geesforgeks . org/merge-two-unsorted-link-list-to-get-a-sorted-list-set-2/](https://www.geeksforgeeks.org/merge-two-unsorted-linked-lists-to-get-a-sorted-list-set-2/)

给定两个未排序的 [链表](https://www.geeksforgeeks.org/data-structures/linked-list/)**L1**的 **N** 节点和 **M** 节点的 **L2** ，任务是将它们合并得到一个排序的 [单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/) 。

**示例:**

> **输入:** L1 = 3→5→1，L2 = 6→2→4→9
> T3】输出: 1→2→3→4→5→6→9
> 
> **输入:** L1 = 1→5→2，L2 = 3→7
> T3】输出: 1→2→3→5→7

**注意:**在 O(1)辅助空间中解决这个问题的内存高效方法已经被接近[这里](https://www.geeksforgeeks.org/merge-two-unsorted-linked-lists-to-get-a-sorted-list/)，

**方法:**想法是使用辅助的[数组](https://www.geeksforgeeks.org/array-data-structure/)来存储两个链表的元素，然后[按照递增的顺序对数组进行排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。最后，[将所有元素重新插入链表](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)。按照以下步骤解决问题:

*   将两个列表连接起来，方法是将第一个列表的尾节点的下一个、 **L1** 指向第二个列表的第一个节点、 **L2** 。
*   [遍历链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)、 **L1** 、[将所有元素](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)推合成一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **V** 。
*   [按递增顺序排列向量 V](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)。
*   排序后，[将所有元素插回列表](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)、 **L1** 。

下面是上述方法的一个实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Linked list node
class Node {
public:
    int data;
    Node* next;
};

// Utility function to append key at
// end of linked list
void insertNode(Node** head, int x)
{
    Node* ptr = new Node;
    ptr->data = x;
    ptr->next = NULL;
    if (*head == NULL) {
        *head = ptr;
    }
    else {
        Node* temp;
        temp = *head;
        while (temp->next != NULL) {
            temp = temp->next;
        }
        temp->next = ptr;
    }
}

// Utility function to print linkedlist
void display(Node** head)
{
    Node* temp;
    temp = *head;
    if (temp == NULL) {
        cout << "NULL \n";
    }
    else {
        while (temp != NULL) {
            cout << temp->data;
            if (temp->next != NULL)
                cout << "->";
            temp = temp->next;
        }
    }
}

// Function to merge two linked lists
void MergeLinkedlist(Node** head1, Node** head2)
{
    Node* ptr;
    ptr = *head1;
    while (ptr->next != NULL) {
        ptr = ptr->next;
    }

    // Join linked list by placing address of
    // first node of L2 in the last node of L1
    ptr->next = *head2;
}

// Function to merge two unsorted linked
// lists to get a sorted list
void sortLinkedList(Node** head, Node** head1)
{
    // Function call to merge the two lists
    MergeLinkedlist(head, head1);

    // Declare a vector
    vector<int> V;
    Node* ptr = *head;

    // Push all elements into vector
    while (ptr != NULL) {
        V.push_back(ptr->data);
        ptr = ptr->next;
    }

    // Sort the vector
    sort(V.begin(), V.end());
    int index = 0;
    ptr = *head;

    // Insert elements in the linked
    // list from the vector
    while (ptr != NULL) {
        ptr->data = V[index];
        index++;
        ptr = ptr->next;
    }

    // Display the sorted and
    // merged linked list
    display(head);
}

// Driver Code
int main()
{
    // Given linked list, L1
    Node* head1 = NULL;
    insertNode(&head1, 3);
    insertNode(&head1, 5);
    insertNode(&head1, 1);

    // Given linked list, L2
    Node* head2 = NULL;
    insertNode(&head2, 6);
    insertNode(&head2, 2);
    insertNode(&head2, 4);
    insertNode(&head2, 9);

    // Function Call
    sortLinkedList(&head1, &head2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Linked list node
    static class Node {
        int data;
        Node next;
    };
    static Node head1, head2;

    // Utility function to append key at
    // end of linked list
    static Node insertNode(Node head, int x)
    {
        Node ptr = new Node();
        ptr.data = x;
        ptr.next = null;
        if (head == null) {
            head = ptr;
        }
        else {
            Node temp;
            temp = head;
            while (temp.next != null) {
                temp = temp.next;
            }
            temp.next = ptr;
        }

        return head;
    }

    // Utility function to print linkedlist
    static void display(Node head)
    {
        Node temp;
        temp = head;
        if (temp == null) {
            System.out.print("null \n");
        }
        else {
            while (temp != null) {
                System.out.print(temp.data);
                if (temp.next != null)
                    System.out.print("->");
                temp = temp.next;
            }
        }
    }

    // Function to merge two linked lists
    static Node MergeLinkedlist()
    {
        Node ptr;
        ptr = head1;
        while (ptr.next != null) {
            ptr = ptr.next;
        }

        // Join linked list by placing address of
        // first node of L2 in the last node of L1
        ptr.next = head2;

        return head1;
    }

    // Function to merge two unsorted linked
    // lists to get a sorted list
    static void sortLinkedList()
    {
        // Function call to merge the two lists
        Node head = MergeLinkedlist();

        // Declare a vector
        Vector<Integer> V = new Vector<>();
        Node ptr = head;

        // Push all elements into vector
        while (ptr != null) {
            V.add(ptr.data);
            ptr = ptr.next;
        }
        Collections.sort(V);
        // Sort the vector
        ;
        int index = 0;
        ptr = head;

        // Insert elements in the linked
        // list from the vector
        while (ptr != null) {
            ptr.data = V.get(index);
            index++;
            ptr = ptr.next;
        }

        // Display the sorted and
        // merged linked list
        display(head);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given linked list, L1

        head1 = insertNode(head1, 3);
        head1 = insertNode(head1, 5);
        head1 = insertNode(head1, 1);

        // Given linked list, L2
        head2 = null;
        head2 = insertNode(head2, 6);
        head2 = insertNode(head2, 2);
        head2 = insertNode(head2, 4);
        head2 = insertNode(head2, 9);

        // Function Call
        sortLinkedList();
    }
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Py program for the above approach

# Linked list node
class Node:
    def __init__(self, d):
        self.data = d
        self.next = None

# Utility function to append key at
# end of linked list
def insertNode(head, x):
    ptr = Node(x)
    if (head == None):
        head = ptr
    else:
        temp = head
        while (temp.next != None):
            temp = temp.next
        temp.next = ptr
    return head

# Utility function to print linkedlist
def display(head):
    temp = head
    if (temp == None):
        print ("None")
    else:
        while (temp.next != None):
            print (temp.data,end="->")
            if (temp.next != None):
                print ("",end="")
            temp = temp.next
        print(temp.data)

# Function to merge two linked lists
def MergeLinkedlist(head1, head2):
    ptr = head1
    while (ptr.next != None):
        ptr = ptr.next

    # Join linked list by placing address of
    # first node of L2 in the last node of L1
    ptr.next = head2

    return head1

# Function to merge two unsorted linked
# lists to get a sorted list
def sortLinkedList(head1, head2):
    # Function call to merge the two lists
    head1 = MergeLinkedlist(head1, head2)

    # Declare a vector
    V = []
    ptr = head1

    # Push all elements into vector
    while (ptr != None):
        V.append(ptr.data)
        ptr = ptr.next

    # Sort the vector
    V = sorted(V)
    index = 0
    ptr = head1

    # Insert elements in the linked
    # list from the vector
    while (ptr != None):
        ptr.data = V[index]
        index += 1
        ptr = ptr.next

    # Display the sorted and
    # merged linked list
    display(head1)

# Driver Code
if __name__ == '__main__':
    # Given linked list, L1
    head1 = None
    head1 = insertNode(head1, 3)
    head1 = insertNode(head1, 5)
    head1 = insertNode(head1, 1)

    # Given linked list, L2
    head2 = None
    head2 = insertNode(head2, 6)
    head2 = insertNode(head2, 2)
    head2 = insertNode(head2, 4)
    head2 = insertNode(head2, 9)

    # Function Call
    sortLinkedList(head1, head2)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Linked list node
public    class Node {
    public    int data;
    public    Node next;
    };

    static Node head1, head2;

    // Utility function to append key at
    // end of linked list
    static Node insertNode(Node head, int x) {
        Node ptr = new Node();
        ptr.data = x;
        ptr.next = null;
        if (head == null) {
            head = ptr;
        } else {
            Node temp;
            temp = head;
            while (temp.next != null) {
                temp = temp.next;
            }
            temp.next = ptr;
        }

        return head;
    }

    // Utility function to print linkedlist
    static void display(Node head) {
        Node temp;
        temp = head;
        if (temp == null) {
            Console.Write("null \n");
        } else {
            while (temp != null) {
                Console.Write(temp.data);
                if (temp.next != null)
                    Console.Write("->");
                temp = temp.next;
            }
        }
    }

    // Function to merge two linked lists
    static Node MergeLinkedlist() {
        Node ptr;
        ptr = head1;
        while (ptr.next != null) {
            ptr = ptr.next;
        }

        // Join linked list by placing address of
        // first node of L2 in the last node of L1
        ptr.next = head2;

        return head1;
    }

    // Function to merge two unsorted linked
    // lists to get a sorted list
    static void sortList()
    {

        // Function call to merge the two lists
        Node head = MergeLinkedlist();

        // Declare a vector
        List<int> V = new List<int>();
        Node ptr = head;

        // Push all elements into vector
        while (ptr != null) {
            V.Add(ptr.data);
            ptr = ptr.next;
        }
        V.Sort();
        // Sort the vector
        ;
        int index = 0;
        ptr = head;

        // Insert elements in the linked
        // list from the vector
        while (ptr != null) {
            ptr.data = V[index];
            index++;
            ptr = ptr.next;
        }

        // Display the sorted and
        // merged linked list
        display(head);
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given linked list, L1

        head1 = insertNode(head1, 3);
        head1 = insertNode(head1, 5);
        head1 = insertNode(head1, 1);

        // Given linked list, L2
        head2 = null;
        head2 = insertNode(head2, 6);
        head2 = insertNode(head2, 2);
        head2 = insertNode(head2, 4);
        head2 = insertNode(head2, 9);

        // Function Call
        sortList();
    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
// Javascript program for the above approach

// Linked list node
class Node {
    constructor(d) {
        this.data = d
        this.next = null
    }
}

// Utility function to append key at
// end of linked list
function insertNode(head, x) {
    ptr = new Node(x)
    if (head == null) {
        head = ptr
    } else {
        temp = head
        while (temp.next != null) {
            temp = temp.next
        }
        temp.next = ptr
    }
    return head
}

// Utility function to print linkedlist
function display(head) {
    let temp = head
    if (temp == null) {
        document.write("null")
    }
    else {
        while (temp.next != null) {
            document.write(temp.data, end = "->")
            if (temp.next != null)
                document.write("", end = "")
            temp = temp.next
        }
        document.write(temp.data)
    }
}

// Function to merge two linked lists
function MergeLinkedlist(head1, head2) {
    let ptr = head1
    while (ptr.next != null)
        ptr = ptr.next

    // Join linked list by placing address of
    // first node of L2 in the last node of L1
    ptr.next = head2

    return head1
}

// Function to merge two unsorted linked
// lists to get a sorted list
function sortLinkedList(head1, head2) {
    // Function call to merge the two lists
    head1 = MergeLinkedlist(head1, head2)

    // Declare a vector
    let V = []
    let ptr = head1

    // Push all elements into vector
    while (ptr != null) {
        V.push(ptr.data)
        ptr = ptr.next
    }

    // Sort the vector
    V = V.sort((a, b) => a - b)
    index = 0
    ptr = head1

    // Insert elements in the linked
    // list from the vector
    while (ptr != null) {
        ptr.data = V[index]
        index += 1
        ptr = ptr.next
    }

    // Display the sorted and
    // merged linked list
    display(head1)
}

// Driver Code

// Given linked list, L1
let head1 = null;
head1 = insertNode(head1, 3)
head1 = insertNode(head1, 5)
head1 = insertNode(head1, 1)

// Given linked list, L2
let head2 = null
head2 = insertNode(head2, 6)
head2 = insertNode(head2, 2)
head2 = insertNode(head2, 4)
head2 = insertNode(head2, 9)

// Function Call
sortLinkedList(head1, head2)

// This code is contributed by gfgking
```

**Output**

```
1->2->3->4->5->6->9
```

***时间复杂度:**O((N+M)* log(N+M))*
***辅助空间:** O(N+M)*