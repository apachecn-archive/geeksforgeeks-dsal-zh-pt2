# 从链表的开始和结束删除第 k 个节点

> 原文:[https://www . geeksforgeeks . org/delete-kth-nodes-from-the-from-a-end-a-link-list/](https://www.geeksforgeeks.org/delete-kth-nodes-from-the-beginning-and-end-of-a-linked-list/)

给定一个[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)和一个表示链表位置的整数 **K** ，任务是从[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)的**开始**和**结束**删除 **K <sup>第</sup>个**节点。

**示例:**

> ***输入:**1→2→**<u>3</u>**→**<u>4</u>**→5→6，K = 3*
> ***输出**:1→2→5→6*
> ***说明:**删除节点:3、4*
> 
> ***输入:****<u>1</u>**→2→3→4→5→**<u>6</u>**，K = 1*
> ***输出:** 2 → 3 → 4 → 5*
> 
> ***输入:**1→2→**<u>3</u>**→**<u>4</u>**→5→6，K = 4*
> ***输出:** 1 → 2 → 5 → 6*

**方法:**按照步骤解决问题

1.  初始化两个指针**快速**和**慢速**，以[遍历链表](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)。
2.  将两个节点指向[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)的**头**。
3.  使用**快速**指针进行迭代，直到**快速**从开始指向**(K–1)**<sup>第</sup>个节点。
4.  遍历时，保持**第一个前一个**来存储**快速**指针的前一个节点。
5.  现在，在每次迭代中将**慢速**和**快速**指针增加一个节点，直到**快速- >下一个**变得等于**空**。
6.  遍历时，保持**秒前一**存储**慢**指针的前一个节点。
7.  [使用**第一个上一个**和**第二个上一个**指针，删除链表的两个节点](https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/)。
8.  [打印更新后的链表。](https://www.geeksforgeeks.org/print-nodes-of-linked-list-at-given-indexes/)

下面是上述方法的实现:

## C++14

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Structure of a
// Linked list Node
struct Node {
    int data;
    struct Node* next;
};

// Function to insert a new node
// at the front of the Linked List
void push(struct Node** head_ref, int new_data)
{
    struct Node* new_node
        = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = new_data;
    new_node->next = (*head_ref);
    (*head_ref) = new_node;
}

// Function to print the Linked List
void printList(struct Node* node)
{
    // while node is not NULL
    while (node != NULL) {
        cout << node->data << " ";
        node = node->next;
    }
    cout << endl;
}

// Function to delete nodes from
// both ends of a Linked List
Node* DeleteNodesfromBothEnds(struct Node** head_ref, int k)
{
    // Empty List
    if (head_ref == NULL)
        return *head_ref;

    // Represent nodes that remove
    // the next node of each
    Node* firstPrev = NULL;
    Node* secondPrev = NULL;

    Node* fast = *head_ref;

    // copy of head_ref
    Node* head = *head_ref;

    // Move fast to (k - 1)
    // nodes ahead of slow
    for (int i = 0; i < k - 1; ++i) {
        firstPrev = fast;
        fast = fast->next;
    }

    Node* slow = *head_ref;

    // Iterate until fast reaches
    // end of the Linked List
    while (fast != NULL && fast->next != NULL) {
        secondPrev = slow;
        slow = slow->next;
        fast = fast->next;
    }

    // Remove first node
    if (firstPrev == secondPrev) {

        if (firstPrev == NULL) {

            // Remove the head node
            head = head->next;
        }
        else {

            // Remove the middle Node
            firstPrev->next = firstPrev->next->next;
        }
    }
    else if (firstPrev != NULL && secondPrev != NULL
             && (firstPrev->next == secondPrev
                 || secondPrev->next == firstPrev)) {

        // If firstPrev comes first
        if (firstPrev->next == secondPrev)
            firstPrev->next = secondPrev->next->next;

        // If secondPrev comes first
        else
            secondPrev->next = firstPrev->next->next;
    }
    else {

        // Remove the head node
        if (firstPrev == NULL) {
            head = head->next;
        }
        else {

            // Removethe first Node
            firstPrev->next = firstPrev->next->next;
        }

        // Remove the head node
        if (secondPrev == NULL) {
            head = head->next;
        }
        else {

            // Remove the second Node
            secondPrev->next = secondPrev->next->next;
        }
    }
    return head;
}

// Driver code
int main()
{

    // Given Linked List
    struct Node* head = NULL;
    push(&head, 6);
    push(&head, 5);
    push(&head, 4);
    push(&head, 3);
    push(&head, 2);
    push(&head, 1);

    // Given position
    int K = 3;

    printList(head);

    // Function call to delete nodes
    // from both ends of Linked List
    head = DeleteNodesfromBothEnds(&head, K);

    // Print the updated Linked List
    printList(head);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

public class Simple {

    // Stores the head and tail
    // of the Linked List
    Node head = null;
    Node tail = null;

    // Structure of a
    // Linked list Node
    class Node {
        int data;
        Node next;

        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    // Function to delete nodes from
    // both ends of a Linked List
    Node DeleteNodesfromBothEnds(int k)
    {
        // Empty List
        if (head == null)
            return head;

        // Represent nodes that remove
        // the next node of each
        Node firstPrev = null, secondPrev = null;

        Node fast = head;

        // Move fast to (k - 1)
        // nodes ahead of slow
        for (int i = 0; i < k - 1; ++i) {
            firstPrev = fast;
            fast = fast.next;
        }

        Node slow = head;

        // Iterate until fast reaches
        // end of the Linked List
        while (fast != null
               && fast.next != null) {
            secondPrev = slow;
            slow = slow.next;
            fast = fast.next;
        }

        // Remove first node
        if (firstPrev == secondPrev) {

            if (firstPrev == null) {

                // Remove the head node
                head = head.next;
            }
            else {

                // Remove the middle Node
                firstPrev.next
                    = firstPrev.next.next;
            }
        }
        else if (firstPrev != null && secondPrev != null
                 && (firstPrev.next == secondPrev
                     || secondPrev.next == firstPrev)) {

            // If firstPrev comes first
            if (firstPrev.next == secondPrev)
                firstPrev.next
                    = secondPrev.next.next;

            // If secondPrev comes first
            else
                secondPrev.next
                    = firstPrev.next.next;
        }
        else {

            // Remove the head node
            if (firstPrev == null) {
                head = head.next;
            }
            else {

                // Removethe first Node
                firstPrev.next
                    = firstPrev.next.next;
            }

            // Remove the head node
            if (secondPrev == null) {
                head = head.next;
            }
            else {

                // Remove the second Node
                secondPrev.next
                    = secondPrev.next.next;
            }
        }

        return head;
    }

    // Function to insert a new node
    // at the end of the Linked List
    public void push(int new_data)
    {
        Node new_node = new Node(new_data);

        if (head == null) {
            head = new_node;
            tail = new_node;
        }
        else {
            tail.next = new_node;
            tail = new_node;
        }
    }

    // Function to print the Linked List
    public void printList()
    {
        Node tnode = head;

        // while tnode is not NULL
        while (tnode != null) {
            System.out.print(tnode.data + " ");
            tnode = tnode.next;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Linked List
        Simple llist = new Simple();
        llist.push(1);
        llist.push(2);
        llist.push(3);
        llist.push(4);
        llist.push(5);
        llist.push(6);

        // Given position
        int K = 3;

        // Function call to delete nodes
        // from both ends of Linked List
        llist.DeleteNodesfromBothEnds(K);

        // Print the updated Linked List
        llist.printList();
    }
}
```

## C#

```
// C# implementation of the approach
using System;

public class Simple {

  // Stores the head and tail
  // of the Linked List
  public Node head = null;
  public Node tail = null;

  // Structure of a
  // Linked list Node
  public class Node {
    public int data;
    public Node next;

    public Node(int d)
    {
      data = d;
      next = null;
    }
  }

  // Function to delete nodes from
  // both ends of a Linked List
  public Node DeleteNodesfromBothEnds(int k)
  {
    // Empty List
    if (head == null)
      return head;

    // Represent nodes that remove
    // the next node of each
    Node firstPrev = null, secondPrev = null;

    Node fast = head;

    // Move fast to (k - 1)
    // nodes ahead of slow
    for (int i = 0; i < k - 1; ++i) {
      firstPrev = fast;
      fast = fast.next;
    }

    Node slow = head;

    // Iterate until fast reaches
    // end of the Linked List
    while (fast != null
           && fast.next != null) {
      secondPrev = slow;
      slow = slow.next;
      fast = fast.next;
    }

    // Remove first node
    if (firstPrev == secondPrev) {

      if (firstPrev == null) {

        // Remove the head node
        head = head.next;
      }
      else {

        // Remove the middle Node
        firstPrev.next
          = firstPrev.next.next;
      }
    }
    else if (firstPrev != null && secondPrev != null
             && (firstPrev.next == secondPrev
                 || secondPrev.next == firstPrev)) {

      // If firstPrev comes first
      if (firstPrev.next == secondPrev)
        firstPrev.next
        = secondPrev.next.next;

      // If secondPrev comes first
      else
        secondPrev.next
        = firstPrev.next.next;
    }
    else {

      // Remove the head node
      if (firstPrev == null) {
        head = head.next;
      }
      else {

        // Removethe first Node
        firstPrev.next
          = firstPrev.next.next;
      }

      // Remove the head node
      if (secondPrev == null) {
        head = head.next;
      }
      else {

        // Remove the second Node
        secondPrev.next
          = secondPrev.next.next;
      }
    }

    return head;
  }

  // Function to insert a new node
  // at the end of the Linked List
  public void push(int new_data)
  {
    Node new_node = new Node(new_data);

    if (head == null) {
      head = new_node;
      tail = new_node;
    }
    else {
      tail.next = new_node;
      tail = new_node;
    }
  }

  // Function to print the Linked List
  public void printList()
  {
    Node tnode = head;

    // while tnode is not NULL
    while (tnode != null) {
      Console.Write(tnode.data + " ");
      tnode = tnode.next;
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given Linked List
    Simple llist = new Simple();
    llist.push(1);
    llist.push(2);
    llist.push(3);
    llist.push(4);
    llist.push(5);
    llist.push(6);

    // Given position
    int K = 3;

    // Function call to delete nodes
    // from both ends of Linked List
    llist.DeleteNodesfromBothEnds(K);

    // Print the updated Linked List
    llist.printList();
  }
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Structure of a
// Linked list Node
class Node {

    constructor()
    {
        this.data = 0;
        this.next = null;
    }
};

// Function to insert a new node
// at the front of the Linked List
function push(head_ref, new_data)
{
    var new_node = new Node();
    new_node.data = new_data;
    new_node.next = (head_ref);
    (head_ref) = new_node;
    return head_ref;
}

// Function to print the Linked List
function printList(node)
{
    // while node is not null
    while (node != null) {
        document.write( node.data + " ");
        node = node.next;
    }
    document.write("<br>");
}

// Function to delete nodes from
// both ends of a Linked List
function DeleteNodesfromBothEnds(head_ref, k)
{
    // Empty List
    if (head_ref == null)
        return head_ref;

    // Represent nodes that remove
    // the next node of each
    var firstPrev = null;
    var secondPrev = null;

    var fast = head_ref;

    // copy of head_ref
    var head = head_ref;

    // Move fast to (k - 1)
    // nodes ahead of slow
    for (var i = 0; i < k - 1; ++i) {
        firstPrev = fast;
        fast = fast.next;
    }

    var slow = head_ref;

    // Iterate until fast reaches
    // end of the Linked List
    while (fast != null && fast.next != null) {
        secondPrev = slow;
        slow = slow.next;
        fast = fast.next;
    }

    // Remove first node
    if (firstPrev == secondPrev) {

        if (firstPrev == null) {

            // Remove the head node
            head = head.next;
        }
        else {

            // Remove the middle Node
            firstPrev.next = firstPrev.next.next;
        }
    }
    else if (firstPrev != null && secondPrev != null
             && (firstPrev.next == secondPrev
                 || secondPrev.next == firstPrev)) {

        // If firstPrev comes first
        if (firstPrev.next == secondPrev)
            firstPrev.next = secondPrev.next.next;

        // If secondPrev comes first
        else
            secondPrev.next = firstPrev.next.next;
    }
    else {

        // Remove the head node
        if (firstPrev == null) {
            head = head.next;
        }
        else {

            // Removethe first Node
            firstPrev.next = firstPrev.next.next;
        }

        // Remove the head node
        if (secondPrev == null) {
            head = head.next;
        }
        else {

            // Remove the second Node
            secondPrev.next = secondPrev.next.next;
        }
    }
    return head;
}

// Driver code
// Given Linked List
var head = null;
head = push(head, 6);
head = push(head, 5);
head = push(head, 4);
head = push(head, 3);
head = push(head, 2);
head = push(head, 1);
// Given position
var K = 3;
printList(head);
// Function call to delete nodes
// from both ends of Linked List
head = DeleteNodesfromBothEnds(head, K);
// Print the updated Linked List
printList(head);

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
1 2 3 4 5 6 
1 2 5 6 
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*