# 向链表表示的数字加 1 的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-用于将 1 添加到数字表示为链表的程序/](https://www.geeksforgeeks.org/cpp-program-for-adding-1-to-a-number-represented-as-linked-list/)

数字在链表中表示，每个数字对应链表中的一个节点。再加 1。例如，1999 被表示为(1-> 9-> 9 -> 9)，将 1 添加到它应该会将其更改为(2->0->0->0)

以下是步骤:

1.  反转给定的链表。例如，1-> 9-> 9 -> 9 被转换为 9-> 9-> 9-> 9-> 1。
2.  从最左边的节点开始遍历链表，并向其中添加 1。如果有进位，移到下一个节点。当有进位时，继续移动到下一个节点。
3.  反向修改链表和返回头。

下面是以上步骤的实现。

## C++

```
// C++ program to add 1 to a 
// linked list 
#include <bits/stdc++.h>
using namespace std;

// Linked list node 
class Node 
{ 
    public:
    int data; 
    Node* next; 
}; 

/* Function to create a new node 
   with given data */
Node *newNode(int data) 
{ 
    Node *new_node = new Node; 
    new_node->data = data; 
    new_node->next = NULL; 
    return new_node; 
} 

// Function to reverse the linked list 
Node *reverse(Node *head) 
{ 
    Node * prev = NULL; 
    Node * current = head; 
    Node * next; 
    while (current != NULL) 
    { 
        next = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    } 
    return prev; 
} 

/* Adds one to a linked lists and 
   return the head node of resultant 
   list */
Node *addOneUtil(Node *head) 
{ 
    // res is head node of the 
    // resultant list 
    Node* res = head; 
    Node *temp, *prev = NULL; 

    int carry = 1, sum; 

    // while both lists exist 
    while (head != NULL) 
    { 
        // Calculate value of next digit 
        // in resultant list. The next digit 
        // is sum of following things 
        // (i) Carry 
        // (ii) Next digit of head list (if 
        // there is a next digit) 
        sum = carry + head->data; 

        // Update carry for next calculation 
        carry = (sum >= 10)? 1 : 0; 

        // Update sum if it is greater 
        // than 10 
        sum = sum % 10; 

        // Create a new node with sum 
        // as data 
        head->data = sum; 

        // Move head and second pointers 
        // to next nodes 
        temp = head; 
        head = head->next; 
    } 

    // If some carry is still there, add 
    // a new node to result list. 
    if (carry > 0) 
        temp->next = newNode(carry); 

    // return head of the resultant list 
    return res; 
} 

// This function mainly uses addOneUtil(). 
Node* addOne(Node *head) 
{ 
    // Reverse linked list 
    head = reverse(head); 

    // Add one from left to right of 
    // reversed list 
    head = addOneUtil(head); 

    // Reverse the modified list 
    return reverse(head); 
} 

// A utility function to print a 
// linked list 
void printList(Node *node) 
{ 
    while (node != NULL) 
    { 
        cout << node->data; 
        node = node->next; 
    } 
    cout<<endl;
} 

// Driver code
int main(void) 
{ 
    Node *head = newNode(1); 
    head->next = newNode(9); 
    head->next->next = newNode(9); 
    head->next->next->next = newNode(9); 

    cout << "List is "; 
    printList(head); 

    head = addOne(head); 

    cout << "Resultant list is "; 
    printList(head); 

    return 0; 
} 
// This is code is contributed by rathbhupendra
```

**输出:**

```
List is 1999
Resultant list is 2000
```

**递归实现:**
我们可以递归到达最后一个节点，并结转到之前的节点。递归解决方案不需要链表的反转。我们也可以用堆栈代替递归来临时保存节点。

下面是递归解决方案的实现。

## C++

```
// Recursive C++ program to add 1 to 
// a linked list
#include <bits/stdc++.h>

// Linked list node 
struct Node 
{
    int data;
    Node* next;
};

/* Function to create a new 
   node with given data */
Node* newNode(int data)
{
    Node* new_node = new Node;
    new_node->data = data;
    new_node->next = NULL;
    return new_node;
}

// Recursively add 1 from end to 
// beginning and returns carry 
// after all nodes are processed.
int addWithCarry(Node* head)
{
    // If linked list is empty, 
    // then return carry
    if (head == NULL)
        return 1;

    // Add carry returned be next 
    // node call
    int res = head->data + addWithCarry(head->next);

    // Update data and return new carry
    head->data = (res) % 10;
    return (res) / 10;
}

// This function mainly uses addWithCarry().
Node* addOne(Node* head)
{
    // Add 1 to linked list from end 
    // to beginning
    int carry = addWithCarry(head);

    // If there is carry after processing 
    // all nodes, then we need to add a 
    // new node to linked list
    if (carry) 
    {
        Node* newNode = new Node;
        newNode->data = carry;
        newNode->next = head;

        // New node becomes head now
        return newNode; 
    }

    return head;
}

// A utility function to print 
// a linked list
void printList(Node* node)
{
    while (node != NULL) 
    {
        printf("%d", node->data);
        node = node->next;
    }
    printf("");
}

// Driver code 
int main(void)
{
    Node* head = newNode(1);
    head->next = newNode(9);
    head->next->next = newNode(9);
    head->next->next->next = newNode(9);

    printf("List is ");
    printList(head);

    head = addOne(head);

    printf("Resultant list is ");
    printList(head);

    return 0;
}
```

**输出:**

```
List is 1999
Resultant list is 2000
```

**简单的方法和容易的实现:**想法是存储最后一个非 9 位数的指针，这样如果最后一个指针为零，我们就可以将存储节点之后的所有节点(包含 9 之前最后一位数字的位置)替换为 0，并将存储节点的值加 1

## C++

```
// Recursive C++ program to add 1 to 
// a linked list
#include <bits/stdc++.h>

// Linked list node 
struct Node 
{
    int data;
    Node* next;
};

/* Function to create a new 
   node with given data */
Node* newNode(int data)
{
    Node* new_node = new Node;
    new_node->data = data;
    new_node->next = NULL;
    return new_node;
}

Node* addOne(Node* head)
{
    // Your Code here
    // return head of list after 
    // adding one
    Node* ln = head;
    if (head->next == NULL) 
    {
        head->data += 1;
        return head;
    }
    Node* t = head;
    int prev;
    while (t->next) 
    {
        if (t->data != 9) 
        {
            ln = t;
        }
        t = t->next;
    }
    if (t->data == 9 && 
        ln != NULL) 
    {
        if (ln->data == 9 && 
            ln == head) 
        {
            Node* temp = newNode(1);
            temp->next = head;
            head = temp;
            t = ln;
        }
        else 
        {
            t = ln;
            t->data += 1;
            t = t->next;
        }
        while (t) 
       {
            t->data = 0;
            t = t->next;
        }
    }
    else 
    {
        t->data += 1;
    }
    return head;
}

// A utility function to print 
// a linked list
void printList(Node* node)
{
    while (node != NULL) 
    {
        printf("%d->", 
                node->data);
        node = node->next;
    }
    printf("NULL");
    printf("");
}

// Driver code 
int main(void)
{
    Node* head = newNode(1);
    head->next = newNode(9);
    head->next->next = newNode(9);
    head->next->next->next = newNode(9);

    printf("List is ");
    printList(head);

    head = addOne(head);

    printf("Resultant list is ");
    printList(head);

    return 0;
}
// This code is contribute bu maddler
```

**输出:**

```
List is 1999
Resultant list is 2000
```

更多详情请参考[上的完整文章将 1 添加到表示为链表](https://www.geeksforgeeks.org/add-1-number-represented-linked-list/)的数字中！