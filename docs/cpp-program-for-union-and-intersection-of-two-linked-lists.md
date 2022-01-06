# 两个链表并集和交集的 C++程序

> 原文:[https://www . geesforgeks . org/CPP-两个链表的并集和交集程序/](https://www.geeksforgeeks.org/cpp-program-for-union-and-intersection-of-two-linked-lists/)

给定两个链接列表，创建包含给定列表中元素的并集和交集的并集和交集列表。输出列表中元素的顺序并不重要。
**例:**

```
Input:
List1: 10->15->4->20
List2:  8->4->2->10
Output:
Intersection List: 4->10
Union List: 2->8->20->4->15->10
```

**方法 1(简单):**
下面是分别获取并集和交集列表的简单算法。
**1。交集(列表 1、列表 2):**
将结果列表初始化为空。遍历列表 1，查找列表 2 中的每个元素，如果列表 2 中有该元素，则将该元素添加到结果中。
**2。联合(列表 1，列表 2):**
将结果列表初始化为空。遍历列表 1，并将其所有元素添加到结果中。
导线列表 2。如果结果中已经存在 list2 的元素，则不要将其插入到结果中，否则插入。
该方法假设给定列表中没有重复项。
感谢蛇湖提出这个方法。下面是这个方法的 C 和 Java 实现。

## C++

```
// C++ program to find union
// and intersection of two unsorted
// linked lists
#include <iostream>
using namespace std;

// Link list node 
struct Node 
{
    int data;
    struct Node* next;
};

/* A utility function to insert a 
   node at the beginning ofa linked list*/
void push(struct Node** head_ref, 
          int new_data);

/* A utility function to check if 
   given data is present in a list */
bool isPresent(struct Node* head, 
               int data);

/* Function to get union of two 
   linked lists head1 and head2 */
struct Node* getUnion(struct Node* head1,
                      struct Node* head2)
{
    struct Node* result = NULL;
    struct Node *t1 = head1, *t2 = head2;

    // Insert all elements of
    // list1 to the result list
    while (t1 != NULL) 
    {
        push(&result, t1->data);
        t1 = t1->next;
    }

    // Insert those elements of list2
    // which are not present in result list
    while (t2 != NULL) 
    {
        if (!isPresent(result, t2->data))
            push(&result, t2->data);
        t2 = t2->next;
    }
    return result;
}

/* Function to get intersection of 
   two linked lists head1 and head2 */
struct Node* getIntersection(struct Node* head1,
                             struct Node* head2)
{
    struct Node* result = NULL;
    struct Node* t1 = head1;

    // Traverse list1 and search each element 
    // of it in list2\. If the element is present 
    // in list 2, then insert the element to result
    while (t1 != NULL) 
    {
        if (isPresent(head2, t1->data))
            push(&result, t1->data);
        t1 = t1->next;
    }
    return result;
}

/* A utility function to insert a 
   node at the beginning of a linked list*/
void push(struct Node** head_ref, 
          int new_data)
{

    // Allocate node 
    struct Node* new_node = 
    (struct Node*)malloc(
     sizeof(struct Node));

    // Put in the data 
    new_node->data = new_data;

    /* Link the old list off the 
       new node */
    new_node->next = (*head_ref);

    /* Move the head to point to the 
       new node */
    (*head_ref) = new_node;
}

/* A utility function to print a 
   linked list*/
void printList(struct Node* node)
{
    while (node != NULL) 
    {
        cout << " " << node->data;
        node = node->next;
    }
}

/* A utility function that returns true 
   if data is present in linked list 
   else return false */
bool isPresent(struct Node* head, 
               int data)
{
    struct Node* t = head;
    while (t != NULL) 
    {
        if (t->data == data)
            return 1;
        t = t->next;
    }
    return 0;
}

// Driver code
int main()
{  
    // Start with the empty list 
    struct Node* head1 = NULL;
    struct Node* head2 = NULL;
    struct Node* intersecn = NULL;
    struct Node* unin = NULL;

    // Create a linked lits 10->15->5->20 
    push(&head1, 20);
    push(&head1, 4);
    push(&head1, 15);
    push(&head1, 10);

    // Create a linked lits 8->4->2->10 
    push(&head2, 10);
    push(&head2, 2);
    push(&head2, 4);
    push(&head2, 8);
    intersecn = 
    getIntersection(head1, head2);
    unin = getUnion(head1, head2);
    cout << "First list is " << endl;
    printList(head1);
    cout << "Second list is " << endl;
    printList(head2);
    cout << "Intersection list is " << endl;
    printList(intersecn);
    cout << "Union list is " << endl;
    printList(unin);
    return 0;
}
// This code is contributed by shivanisingh2110
```

**输出**

```
 First list is 
10 15 4 20 
Second list is 
8 4 2 10 
Intersection list is 
4 10 
Union list is 
2 8 20 4 15 10
```

**复杂度分析:**

*   **时间复杂度:** O(m*n)。
    这里的‘m’和‘n’分别是第一和第二列表中的元素数量。
    **对于联合:**对于列表-2 中的每个元素，我们检查该元素是否已经存在于使用列表-1 生成的结果列表中。
    **对于交集:**对于列表-1 中的每个元素，我们检查该元素是否也存在于列表-2 中。
*   **辅助空间:** O(1)。
    不使用任何数据结构来存储值。

**方法 2(使用合并排序):**
在该方法中，并集和交集的算法非常相似。首先，我们对给定的列表进行排序，然后遍历排序后的列表以获得并集和交集。
以下是获取并集和交集列表应遵循的步骤。

1.  使用合并排序对第一个链接列表进行排序。这一步需要 O(mLogm)时间。该步骤详见[本帖](https://www.geeksforgeeks.org/archives/7740)。
2.  使用合并排序对第二个链接列表进行排序。这一步需要 0(nLogn)时间。该步骤详见[本帖](https://www.geeksforgeeks.org/archives/7740)。
3.  线性扫描两个排序列表以获得并集和交集。这一步需要 O(m + n)个时间。这个步骤可以使用与这里讨论的排序数组算法相同的算法来实现。

该方法的时间复杂度为 O(mLogm + nLogn)，优于方法 1 的时间复杂度。
详情请参考[两链表的并集和交集](https://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/)整篇文章！