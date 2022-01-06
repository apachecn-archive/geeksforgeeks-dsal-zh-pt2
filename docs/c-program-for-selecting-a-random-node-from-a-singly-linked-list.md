# 从单链表中选择随机节点的 C 程序

> 原文:[https://www . geesforgeks . org/c-从单链表中选择随机节点的程序/](https://www.geeksforgeeks.org/c-program-for-selecting-a-random-node-from-a-singly-linked-list/)

给定一个单链表，从链表中选择一个随机节点(如果链表中有 N 个节点，选择一个节点的概率应该是 1/N)。给你一个随机数生成器。
下面是一个简单的解决方案:

1.  通过遍历列表来计算节点数。
2.  再次遍历列表，以概率 1/N 选择每个节点，可以通过为第 I 个节点生成一个从 0 到 N-i 的随机数，并且只有当生成的数等于 0(或从 0 到 N-i 的任何其他固定数)时才选择第 I 个节点来完成选择。

我们得到了上述方案的一致概率。

```
i = 1, probability of selecting first node = 1/N
i = 2, probability of selecting second node =
                   [probability that first node is not selected] * 
                   [probability that second node is selected]
                  = ((N-1)/N)* 1/(N-1)
                  = 1/N  
```

同样，其他选择其他节点的概率为 1/N
上述解决方案需要链表的两次遍历。

**如何选择只允许一次遍历的随机节点？**
想法是用[水库采样](https://www.geeksforgeeks.org/reservoir-sampling/)。以下是步骤。这是[油藏取样](https://www.geeksforgeeks.org/reservoir-sampling/)的一个更简单的版本，因为我们只需要选择一个键，而不是 k 键。

```
(1) Initialize result as first node
    result = head->key 
(2) Initialize n = 2
(3) Now one by one consider all nodes from 2nd node onward.
    (a) Generate a random number from 0 to n-1\. 
        Let the generated random number is j.
    (b) If j is equal to 0 (we could choose other fixed numbers 
        between 0 to n-1), then replace result with the current node.
    (c) n = n+1
    (d) current = current->next
```

下面是上述算法的实现。

## C

```
/* C program to randomly select a node 
   from a singly linked list */
#include<stdio.h>
#include<stdlib.h>
#include <time.h>

// Linked list node 
struct Node
{
    int key;
    struct Node* next;
};

// A reservoir sampling-based function 
// to print a random node from a 
// linked list
void printRandom(struct Node *head)
{
    // If list is empty
    if (head == NULL)
       return;

    // Use a different seed value so 
    // that we don't get same result 
    // each time we run this program
    srand(time(NULL));

    // Initialize result as first node
    int result = head->key;

    // Iterate from the (k+1)th element 
    // to nth element
    struct Node *current = head;
    int n;
    for (n = 2; current != NULL; n++)
    {
        // Change result with probability 
        // 1/n
        if (rand() % n == 0)
           result = current->key;

        // Move to next node
        current = current->next;
    }

    printf("Randomly selected key is %d", 
            result);
}

/* A utility function to create 
   a new node */
struct Node *newNode(int new_key)
{
    // Allocate node 
    struct Node* new_node =
           (struct Node*) malloc(sizeof(struct Node));

    // Put in the key 
    new_node->key  = new_key;
    new_node->next =  NULL;

    return new_node;
}

/* A utility function to insert a node 
   at the beginning of linked list */
void push(struct Node** head_ref, 
          int new_key)
{
    // Allocate node 
    struct Node* new_node = new Node;

    // Put in the key  
    new_node->key  = new_key;

    // Link the old list off the 
    // new node 
    new_node->next = (*head_ref);

    // Move the head to point to 
    // the new node 
    (*head_ref)    = new_node;
}

// Driver code
int main()
{
    struct Node *head = NULL;
    push(&head, 5);
    push(&head, 20);
    push(&head, 4);
    push(&head, 3);
    push(&head, 30);

    printRandom(head);
    return 0;
}
```

请注意，上述程序基于随机函数的结果，可能会产生不同的输出。
**这是怎么工作的？**
让列表中总共有 N 个节点。从最后一个节点更容易理解。
最后一个节点是结果的概率只是 1/N【对于最后一个或第 N 个节点，我们生成一个 0 到 N-1 之间的随机数，如果生成的数是 0(或任何其他固定的数)，那么最后一个节点就是结果】
第二个最后一个节点是结果的概率也应该是 1/N

```
The probability that the second last node is the result 
          = [Probability that the second last node replaces result] X 
            [Probability that the last node doesn't replace the result] 
          = [1 / (N-1)] * [(N-1)/N]
          = 1/N
```

同样，我们可以显示 3 <sup>rd</sup> 最后一个节点和其他节点的概率。
详情请参考[从单链表中选择一个随机节点](https://www.geeksforgeeks.org/select-a-random-node-from-a-singly-linked-list/)的完整文章！