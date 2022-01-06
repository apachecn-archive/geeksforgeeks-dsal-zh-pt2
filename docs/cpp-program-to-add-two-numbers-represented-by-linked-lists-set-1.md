# C++程序添加两个链表表示的数字-集合 1

> 原文:[https://www . geesforgeks . org/CPP-program-add-two-numbers-由链表表示-set-1/](https://www.geeksforgeeks.org/cpp-program-to-add-two-numbers-represented-by-linked-lists-set-1/)

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

**方法 1:**
**逼近**:遍历两个列表，逐个选择两个列表的节点，并添加值。如果总和大于 10，则进位为 1 并减少总和。如果一个列表中的元素比另一个列表中的多，则认为该列表的剩余值为 0。步骤如下:

1.  从头到尾遍历两个链表
2.  将相应链接列表中的两位数字相加。
3.  如果其中一个列表已到达末尾，则取 0 作为它的数字。
4.  继续下去，直到两个列表都结束。
5.  如果两位数之和大于 9，则将进位设置为 1，将当前数字设置为*和% 10*

下面是这个方法的实现。

## C++

```
// C++ program to add two numbers
// represented by linked list
#include <bits/stdc++.h>
using namespace std;

// Linked list node 
class Node 
{
    public:
    int data;
    Node* next;
};

/* Function to create a 
   new node with given data */
Node* newNode(int data)
{
    Node* new_node = new Node();
    new_node->data = data;
    new_node->next = NULL;
    return new_node;
}

/* Function to insert a node at the
   beginning of the Singly Linked List */
void push(Node** head_ref, int new_data)
{
    // Allocate node 
    Node* new_node = newNode(new_data);

    // link the old list off the 
    // new node 
    new_node->next = (*head_ref);

    // Move the head to point to the 
    // new node 
    (*head_ref) = new_node;
}

/* Adds contents of two linked lists and 
   return the head node of resultant list */
Node* addTwoLists(Node* first, 
                  Node* second)
{
    // res is head node of the resultant 
    // list
    Node* res = NULL;
    Node *temp, *prev = NULL;
    int carry = 0, sum;

    // while both lists exist
    while (first != NULL || 
           second != NULL) 
    {
        // Calculate value of next digit in 
        // resultant list. The next digit is 
        // sum of following things
        // (i) Carry
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
        // set it as head of the resultant list
        if (res == NULL)
            res = temp;

        // If this is not the first
        // node then connect it to the rest.
        else
            prev->next = temp;

        // Set prev for next insertion
        prev = temp;

        // Move first and second
        // pointers to next nodes
        if (first)
            first = first->next;
        if (second)
            second = second->next;
    }

    if (carry > 0)
        temp->next = newNode(carry);

    // return head of the resultant 
    // list
    return res;
}

// A utility function to print a 
// linked list
void printList(Node* node)
{
    while (node != NULL) 
    {
        cout << node->data << " ";
        node = node->next;
    }
    cout << endl;
}

// Driver code
int main(void)
{
    Node* res = NULL;
    Node* first = NULL;
    Node* second = NULL;

    // Create first list 
    // 7->5->9->4->6
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
    cout << "Second List is ";
    printList(second);

    // Add the two lists and see 
    // result
    res = addTwoLists(first, 
                      second);
    cout << "Resultant list is ";
    printList(res);
    return 0;
}
// This code is contributed by rathbhupendra
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

**方法 2(使用 STL):** 使用堆栈数据结构
**方法:**

```
1\. Create 3 stacks namely s1,s2,s3.
2\. Fill s1 with Nodes of list1 and fill s2 with nodes of list2.
3\. Fill s3 by creating new nodes and setting the data of new nodes to the 
   sum of s1.top(), s2.top() and carry until list1 and list2 are empty .
4\. If the sum >9, set carry 1
5\. Else set carry 0.
6\. Create a Node(say prev) that will contain the head of the sum List.
7\. Link all the elements of s3 from top to bottom.
8\. return prev.
```

## C++

```
// C++ program to add two numbers represented 
// by Linked Lists using Stack
#include <bits/stdc++.h>
using namespace std;
class Node 
{
    public:
    int data;
    Node* next;
};
Node* newnode(int data)
{
    Node* x = new Node();
    x->data = data;
    return x;
}
// Function that returns the sum of two 
// numbers represented by linked lists
Node* addTwoNumbers(Node* l1, Node* l2)
{
    Node* prev = NULL;

    // Create 3 stacks
    stack<Node*> s1, s2, s3;

    // Fill first stack with first 
    // List Elements
    while (l1 != NULL) 
    {
        s1.push(l1);
        l1 = l1->next;
    }

    // Fill second stack with second 
    // List Elements
    while (l2 != NULL) 
    {
        s2.push(l2);
        l2 = l2->next;
    }
    int carry = 0;
    // Fill the third stack with the 
    // sum of first and second stack
    while (!s1.empty() && !s2.empty()) 
    {
        int sum = (s1.top()->data + 
                   s2.top()->data + carry);
        Node* temp = newnode(sum % 10);
        s3.push(temp);
        if (sum > 9) 
        {
            carry = 1;
        }
        else 
        {
            carry = 0;
        }
        s1.pop();
        s2.pop();
    }
    while (!s1.empty()) 
   {
        int sum = carry + s1.top()->data;
        Node* temp = newnode(sum % 10);
        s3.push(temp);
        if (sum > 9) 
        {
            carry = 1;
        }
        else 
        {
            carry = 0;
        }
        s1.pop();
    }
    while (!s2.empty()) 
    {
        int sum = carry + s2.top()->data;
        Node* temp = newnode(sum % 10);
        s3.push(temp);
        if (sum > 9) 
        {
            carry = 1;
        }
        else 
        {
            carry = 0;
        }
        s2.pop();
    }
    // If carry is still present create a 
    // new node with value 1 and push it 
    // to the third stack
    if (carry == 1) 
    {
        Node* temp = newnode(1);
        s3.push(temp);
    }

    // Link all the elements inside 
    // third stack with each other
    if (!s3.empty())
        prev = s3.top();
    while (!s3.empty())
    {
        Node* temp = s3.top();
        s3.pop();
        if (s3.size() == 0) 
        {
            temp->next = NULL;
        }
        else 
        {
            temp->next = s3.top();
        }
    }
    return prev;
}

// Utility functions
// Function that displays the List
void Display(Node* head)
{
    if (head == NULL) 
    {
        return;
    }
    while (head->next != NULL) 
    {
        cout << head->data << " -> ";
        head = head->next;
    }
    cout << head->data << endl;
}

// Function that adds element at 
// the end of the Linked List
void push(Node** head_ref, int d)
{
    Node* new_node = newnode(d);
    new_node->next = NULL;
    if (*head_ref == NULL) 
    {
        new_node->next = *head_ref;
        *head_ref = new_node;
        return;
    }
    Node* last = *head_ref;
    while (last->next != NULL && 
           last != NULL) 
    {
        last = last->next;
    }
    last->next = new_node;
    return;
}

// Driver code
int main()
{
    // Creating two lists first list 
    // 9 -> 5 -> 0
    // second List = 6 -> 7
    Node* first = NULL;
    Node* second = NULL;
    Node* sum = NULL;
    push(&first, 9);
    push(&first, 5);
    push(&first, 0);
    push(&second, 6);
    push(&second, 7);
    cout << "First List : ";
    Display(first);
    cout << "Second List : ";
    Display(second);
    sum = addTwoNumbers(first, second);
    cout << "Sum List : ";
    Display(sum);
    return 0;
}
```

**输出:**

```
First List : 9 -> 5 -> 0
Second List : 6 -> 7
Sum List : 1 -> 0 -> 1 -> 7
```

**时间复杂度为 O(N)的另一种方法:**

给定的方法按照以下步骤工作:

1.  首先，我们分别计算链表的大小，大小 1 和大小 2。
2.  然后我们遍历更大的链表，如果有的话，递减直到两者的大小相同。
3.  现在我们遍历两个链表直到结束。
4.  现在回溯发生在执行加法的时候。
5.  最后，返回包含答案的链表的头节点。

## C++

```
// C++ program to implement 
// the above approach
#include <iostream>
using namespace std;

struct Node 
{
    int data;
    struct Node* next;
};

// Recursive function
Node* addition(Node* temp1, Node* temp2, 
               int size1, int size2)
{
    // Creating a new Node
    Node* newNode = 
    (struct Node*)malloc(sizeof(struct Node));

    // Base case
    if (temp1->next == NULL && 
        temp2->next == NULL) 
    {
        // Addition of current nodes which is 
        // the last nodes of both linked lists
        newNode->data = (temp1->data + 
                         temp2->data);

        // Set this current node's link null
        newNode->next = NULL;

        // Return the current node
        return newNode;
    }

    // Creating a node that contains sum 
    // of previously added number
    Node* returnedNode = 
    (struct Node*)malloc(sizeof(struct Node));

    // If sizes are same then we move in
    // both linked list
    if (size2 == size1) 
    {
        // Recursively call the function
        // move ahead in both linked list
        returnedNode = addition(temp1->next, temp2->next,
                                size1 - 1, size2 - 1);

        // Add the current nodes and append the carry
        newNode->data = (temp1->data + temp2->data) + 
                        ((returnedNode->data) / 10);
    }

    // Or else we just move in big linked 
    // list
    else 
    {
        // Recursively call the function
        // move ahead in big linked list
        returnedNode = addition(temp1, temp2->next, 
                                size1, size2 - 1);

        // Add the current node and carry
        newNode->data = 
        (temp2->data) + 
        ((returnedNode->data) / 10);
    }

    // This node contains previously added 
    // numbers so we need to set only 
    // rightmost digit of it
    returnedNode->data = (returnedNode->data) % 10;

    // Set the returned node to the 
    // current nod
    newNode->next = returnedNode;

    // return the current node
    return newNode;
}

// Function to add two numbers represented 
// by nexted list.
struct Node* addTwoLists(struct Node* head1,
                         struct Node* head2)
{
    struct Node *temp1, 
                *temp2, *ans = NULL;

    temp1 = head1;
    temp2 = head2;

    int size1 = 0, size2 = 0;

    // calculating the size of first 
    // linked list
    while (temp1 != NULL) 
    {
        temp1 = temp1->next;
        size1++;
    }

    // Calculating the size of second 
    // linked list
    while (temp2 != NULL) 
    {
        temp2 = temp2->next;
        size2++;
    }

    Node* returnedNode = 
    (struct Node*)malloc(sizeof(struct Node));

    // Traverse the bigger linked list
    if (size2 > size1) 
    {
        returnedNode = addition(head1, head2, 
                                size1, size2);
    }
    else 
    {
        returnedNode = addition(head2, head1, 
                                size2, size1);
    }

    // Creating new node if head node is >10
    if (returnedNode->data >= 10) 
    {
        ans = (struct Node*)malloc(sizeof(struct Node));
        ans->data = (returnedNode->data) / 10;
        returnedNode->data = returnedNode->data % 10;
        ans->next = returnedNode;
    }
    else
        ans = returnedNode;

    // Return the head node of linked list 
    // that contains answer
    return ans;
}

void Display(Node* head)
{
    if (head == NULL) 
    {
        return;
    }
    while (head->next != NULL) 
    {
        cout << head->data << " -> ";
        head = head->next;
    }
    cout << head->data << endl;
}

// Function that adds element at the 
// end of the Linked List
void push(Node** head_ref, int d)
{
    Node* new_node = 
    (struct Node*)malloc(sizeof(struct Node));
    new_node->data = d;
    new_node->next = NULL;
    if (*head_ref == NULL) 
    {
        new_node->next = *head_ref;
        *head_ref = new_node;
        return;
    }

    Node* last = *head_ref;
    while (last->next != NULL && 
           last != NULL) 
    {
        last = last->next;
    }
    last->next = new_node;
    return;
}

// Driver code
int main()
{
    // Creating two lists
    Node* first = NULL;
    Node* second = NULL;
    Node* sum = NULL;
    push(&first, 5);
    push(&first, 6);
    push(&first, 3);
    push(&second, 8);
    push(&second, 4);
    push(&second, 2);
    cout << "First List : ";
    Display(first);
    cout << "Second List : ";
    Display(second);
    sum = addTwoLists(first, second);
    cout << "Sum List : ";
    Display(sum);
    return 0;
}
// This code is contributed by Dharmik Parmar
```

**输出:**

```
First List : 5 -> 6 -> 3
Second List : 8 -> 4 -> 2
Sum List : 1 -> 4 -> 0 -> 5
```

相关文章:[添加两个链表表示的数字|集合 2](https://www.geeksforgeeks.org/sum-of-two-linked-lists/)

更多详情请参考[整篇文章添加两个链表表示的数字|集合 1](https://www.geeksforgeeks.org/add-two-numbers-represented-by-linked-lists/) ！