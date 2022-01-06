# 排序输入的高效霍夫曼编码|贪婪算法-4

> 原文:[https://www . geesforgeks . org/efficient-Huffman-coding-for-sorted-input-greedy-algo-4/](https://www.geeksforgeeks.org/efficient-huffman-coding-for-sorted-input-greedy-algo-4/)

我们建议阅读以下文章作为先决条件。
[贪婪算法|集合 3(霍夫曼编码)](https://www.geeksforgeeks.org/huffman-coding-greedy-algo-3/)

上文中讨论的算法时间复杂度为 O(nLogn)。如果我们知道给定的数组是排序的(按照频率的非递减顺序)，我们可以在 O(n)时间内生成霍夫曼码。下面是排序输入的 O(n)算法。
**1。**创建两个空队列。
T4【2】。为每个唯一字符创建一个叶节点，并按频率的非递减顺序将其排入第一个队列。最初第二个队列是空的。
**3。**通过检查两个队列的前端，以最小的频率将两个节点出列。重复以下步骤两次
1。如果第二个队列为空，则从第一个队列出列。
2。如果第一个队列为空，则从第二个队列出列。
3。否则，比较两个队列的前面，并使最小队列出列。
**4。**新建一个内部节点，频率等于两个节点频率之和。将第一个出队节点作为其左子节点，将第二个出队节点作为右子节点。将此节点排入第二个队列。
**5。**当队列中有多个节点时，重复步骤#3 和#4。剩下的节点是根节点，树是完整的。

## C++

```
// C++ Program for Efficient Huffman Coding for Sorted input
#include <bits/stdc++.h>
using namespace std;

// This constant can be avoided by explicitly
// calculating height of Huffman Tree
#define MAX_TREE_HT 100

// A node of huffman tree
class QueueNode {
public:
    char data;
    unsigned freq;
    QueueNode *left, *right;
};

// Structure for Queue: collection
// of Huffman Tree nodes (or QueueNodes)
class Queue {
public:
    int front, rear;
    int capacity;
    QueueNode** array;
};

// A utility function to create a new Queuenode
QueueNode* newNode(char data, unsigned freq)
{
    QueueNode* temp = new QueueNode[(sizeof(QueueNode))];
    temp->left = temp->right = NULL;
    temp->data = data;
    temp->freq = freq;
    return temp;
}

// A utility function to create a Queue of given capacity
Queue* createQueue(int capacity)
{
    Queue* queue = new Queue[(sizeof(Queue))];
    queue->front = queue->rear = -1;
    queue->capacity = capacity;
    queue->array = new QueueNode*[(queue->capacity
                                   * sizeof(QueueNode*))];
    return queue;
}

// A utility function to check if size of given queue is 1
int isSizeOne(Queue* queue)
{
    return queue->front == queue->rear
           && queue->front != -1;
}

// A utility function to check if given queue is empty
int isEmpty(Queue* queue) { return queue->front == -1; }

// A utility function to check if given queue is full
int isFull(Queue* queue)
{
    return queue->rear == queue->capacity - 1;
}

// A utility function to add an item to queue
void enQueue(Queue* queue, QueueNode* item)
{
    if (isFull(queue))
        return;
    queue->array[++queue->rear] = item;
    if (queue->front == -1)
        ++queue->front;
}

// A utility function to remove an item from queue
QueueNode* deQueue(Queue* queue)
{
    if (isEmpty(queue))
        return NULL;
    QueueNode* temp = queue->array[queue->front];
    if (queue->front
        == queue
               ->rear) // If there is only one item in queue
        queue->front = queue->rear = -1;
    else
        ++queue->front;
    return temp;
}

// A utility function to get from of queue
QueueNode* getFront(Queue* queue)
{
    if (isEmpty(queue))
        return NULL;
    return queue->array[queue->front];
}

/* A function to get minimum item from two queues */
QueueNode* findMin(Queue* firstQueue, Queue* secondQueue)
{
    // Step 3.a: If first queue is empty, dequeue from
    // second queue
    if (isEmpty(firstQueue))
        return deQueue(secondQueue);

    // Step 3.b: If second queue is empty, dequeue from
    // first queue
    if (isEmpty(secondQueue))
        return deQueue(firstQueue);

    // Step 3.c: Else, compare the front of two queues and
    // dequeue minimum
    if (getFront(firstQueue)->freq
        < getFront(secondQueue)->freq)
        return deQueue(firstQueue);

    return deQueue(secondQueue);
}

// Utility function to check if this node is leaf
int isLeaf(QueueNode* root)
{
    return !(root->left) && !(root->right);
}

// A utility function to print an array of size n
void printArr(int arr[], int n)
{
    int i;
    for (i = 0; i < n; ++i)
        cout << arr[i];
    cout << endl;
}

// The main function that builds Huffman tree
QueueNode* buildHuffmanTree(char data[], int freq[],
                            int size)
{
    QueueNode *left, *right, *top;

    // Step 1: Create two empty queues
    Queue* firstQueue = createQueue(size);
    Queue* secondQueue = createQueue(size);

    // Step 2:Create a leaf node for each unique character
    // and Enqueue it to the first queue in non-decreasing
    // order of frequency. Initially second queue is empty
    for (int i = 0; i < size; ++i)
        enQueue(firstQueue, newNode(data[i], freq[i]));

    // Run while Queues contain more than one node. Finally,
    // first queue will be empty and second queue will
    // contain only one node
    while (
        !(isEmpty(firstQueue) && isSizeOne(secondQueue))) {
        // Step 3: Dequeue two nodes with the minimum
        // frequency by examining the front of both queues
        left = findMin(firstQueue, secondQueue);
        right = findMin(firstQueue, secondQueue);

        // Step 4: Create a new internal node with frequency
        // equal to the sum of the two nodes frequencies.
        // Enqueue this node to second queue.
        top = newNode('{content}apos;, left->freq + right->freq);
        top->left = left;
        top->right = right;
        enQueue(secondQueue, top);
    }

    return deQueue(secondQueue);
}

// Prints huffman codes from the root of Huffman Tree. It
// uses arr[] to store codes
void printCodes(QueueNode* root, int arr[], int top)
{
    // Assign 0 to left edge and recur
    if (root->left) {
        arr[top] = 0;
        printCodes(root->left, arr, top + 1);
    }

    // Assign 1 to right edge and recur
    if (root->right) {
        arr[top] = 1;
        printCodes(root->right, arr, top + 1);
    }

    // If this is a leaf node, then it contains one of the
    // input characters, print the character and its code
    // from arr[]
    if (isLeaf(root)) {
        cout << root->data << ": ";
        printArr(arr, top);
    }
}

// The main function that builds a Huffman Tree and print
// codes by traversing the built Huffman Tree
void HuffmanCodes(char data[], int freq[], int size)
{
    // Construct Huffman Tree
    QueueNode* root = buildHuffmanTree(data, freq, size);

    // Print Huffman codes using the Huffman tree built
    // above
    int arr[MAX_TREE_HT], top = 0;
    printCodes(root, arr, top);
}

// Driver code
int main()
{
    char arr[] = { 'a', 'b', 'c', 'd', 'e', 'f' };
    int freq[] = { 5, 9, 12, 13, 16, 45 };
    int size = sizeof(arr) / sizeof(arr[0]);
    HuffmanCodes(arr, freq, size);
    return 0;
}

// This code is contributed by rathbhupendra
```

## C

```
// C Program for Efficient Huffman Coding for Sorted input
#include <stdio.h>
#include <stdlib.h>

// This constant can be avoided by explicitly calculating
// height of Huffman Tree
#define MAX_TREE_HT 100

// A node of huffman tree
struct QueueNode {
    char data;
    unsigned freq;
    struct QueueNode *left, *right;
};

// Structure for Queue: collection of Huffman Tree nodes (or
// QueueNodes)
struct Queue {
    int front, rear;
    int capacity;
    struct QueueNode** array;
};

// A utility function to create a new Queuenode
struct QueueNode* newNode(char data, unsigned freq)
{
    struct QueueNode* temp = (struct QueueNode*)malloc(
        sizeof(struct QueueNode));
    temp->left = temp->right = NULL;
    temp->data = data;
    temp->freq = freq;
    return temp;
}

// A utility function to create a Queue of given capacity
struct Queue* createQueue(int capacity)
{
    struct Queue* queue
        = (struct Queue*)malloc(sizeof(struct Queue));
    queue->front = queue->rear = -1;
    queue->capacity = capacity;
    queue->array = (struct QueueNode**)malloc(
        queue->capacity * sizeof(struct QueueNode*));
    return queue;
}

// A utility function to check if size of given queue is 1
int isSizeOne(struct Queue* queue)
{
    return queue->front == queue->rear
           && queue->front != -1;
}

// A utility function to check if given queue is empty
int isEmpty(struct Queue* queue)
{
    return queue->front == -1;
}

// A utility function to check if given queue is full
int isFull(struct Queue* queue)
{
    return queue->rear == queue->capacity - 1;
}

// A utility function to add an item to queue
void enQueue(struct Queue* queue, struct QueueNode* item)
{
    if (isFull(queue))
        return;
    queue->array[++queue->rear] = item;
    if (queue->front == -1)
        ++queue->front;
}

// A utility function to remove an item from queue
struct QueueNode* deQueue(struct Queue* queue)
{
    if (isEmpty(queue))
        return NULL;
    struct QueueNode* temp = queue->array[queue->front];
    if (queue->front
        == queue
               ->rear) // If there is only one item in queue
        queue->front = queue->rear = -1;
    else
        ++queue->front;
    return temp;
}

// A utility function to get from of queue
struct QueueNode* getFront(struct Queue* queue)
{
    if (isEmpty(queue))
        return NULL;
    return queue->array[queue->front];
}

/* A function to get minimum item from two queues */
struct QueueNode* findMin(struct Queue* firstQueue,
                          struct Queue* secondQueue)
{
    // Step 3.a: If first queue is empty, dequeue from
    // second queue
    if (isEmpty(firstQueue))
        return deQueue(secondQueue);

    // Step 3.b: If second queue is empty, dequeue from
    // first queue
    if (isEmpty(secondQueue))
        return deQueue(firstQueue);

    // Step 3.c:  Else, compare the front of two queues and
    // dequeue minimum
    if (getFront(firstQueue)->freq
        < getFront(secondQueue)->freq)
        return deQueue(firstQueue);

    return deQueue(secondQueue);
}

// Utility function to check if this node is leaf
int isLeaf(struct QueueNode* root)
{
    return !(root->left) && !(root->right);
}

// A utility function to print an array of size n
void printArr(int arr[], int n)
{
    int i;
    for (i = 0; i < n; ++i)
        printf("%d", arr[i]);
    printf("\n");
}

// The main function that builds Huffman tree
struct QueueNode* buildHuffmanTree(char data[], int freq[],
                                   int size)
{
    struct QueueNode *left, *right, *top;

    // Step 1: Create two empty queues
    struct Queue* firstQueue = createQueue(size);
    struct Queue* secondQueue = createQueue(size);

    // Step 2:Create a leaf node for each unique character
    // and Enqueue it to the first queue in non-decreasing
    // order of frequency. Initially second queue is empty
    for (int i = 0; i < size; ++i)
        enQueue(firstQueue, newNode(data[i], freq[i]));

    // Run while Queues contain more than one node. Finally,
    // first queue will be empty and second queue will
    // contain only one node
    while (
        !(isEmpty(firstQueue) && isSizeOne(secondQueue))) {
        // Step 3: Dequeue two nodes with the minimum
        // frequency by examining the front of both queues
        left = findMin(firstQueue, secondQueue);
        right = findMin(firstQueue, secondQueue);

        // Step 4: Create a new internal node with frequency
        // equal to the sum of the two nodes frequencies.
        // Enqueue this node to second queue.
        top = newNode('{content}apos;, left->freq + right->freq);
        top->left = left;
        top->right = right;
        enQueue(secondQueue, top);
    }

    return deQueue(secondQueue);
}

// Prints huffman codes from the root of Huffman Tree.  It
// uses arr[] to store codes
void printCodes(struct QueueNode* root, int arr[], int top)
{
    // Assign 0 to left edge and recur
    if (root->left) {
        arr[top] = 0;
        printCodes(root->left, arr, top + 1);
    }

    // Assign 1 to right edge and recur
    if (root->right) {
        arr[top] = 1;
        printCodes(root->right, arr, top + 1);
    }

    // If this is a leaf node, then it contains one of the
    // input characters, print the character and its code
    // from arr[]
    if (isLeaf(root)) {
        printf("%c: ", root->data);
        printArr(arr, top);
    }
}

// The main function that builds a Huffman Tree and print
// codes by traversing the built Huffman Tree
void HuffmanCodes(char data[], int freq[], int size)
{
    //  Construct Huffman Tree
    struct QueueNode* root
        = buildHuffmanTree(data, freq, size);

    // Print Huffman codes using the Huffman tree built
    // above
    int arr[MAX_TREE_HT], top = 0;
    printCodes(root, arr, top);
}

// Driver program to test above functions
int main()
{
    char arr[] = { 'a', 'b', 'c', 'd', 'e', 'f' };
    int freq[] = { 5, 9, 12, 13, 16, 45 };
    int size = sizeof(arr) / sizeof(arr[0]);
    HuffmanCodes(arr, freq, size);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program for Efficient Huffman Coding
# for Sorted input

# Class for the nodes of the Huffman tree
class QueueNode:

    def __init__(self, data = None, freq = None,
                 left = None, right = None):
        self.data = data
        self.freq = freq
        self.left = left
        self.right = right

    # Function to check if the following
    # node is a leaf node
    def isLeaf(self):
        return (self.left == None and
                self.right == None)

# Class for the two Queues
class Queue:

    def __init__(self):
        self.queue = []

    # Function for checking if the
    # queue has only 1 node
    def isSizeOne(self):
        return len(self.queue) == 1

    # Function for checking if
    # the queue is empty
    def isEmpty(self):
        return self.queue == []

    # Function to add item to the queue
    def enqueue(self, x):
        self.queue.append(x)

    # Function to remove item from the queue
    def dequeue(self):
        return self.queue.pop(0)

# Function to get minimum item from two queues
def findMin(firstQueue, secondQueue):

    # Step 3.1: If second queue is empty,
    # dequeue from first queue
    if secondQueue.isEmpty():
        return firstQueue.dequeue()

    # Step 3.2: If first queue is empty,
    # dequeue from second queue
    if firstQueue.isEmpty():
        return secondQueue.dequeue()

    # Step 3.3:  Else, compare the front of
    # two queues and dequeue minimum
    if (firstQueue.queue[0].freq <
        secondQueue.queue[0].freq):
        return firstQueue.dequeue()

    return secondQueue.dequeue()

# The main function that builds Huffman tree
def buildHuffmanTree(data, freq, size):

    # Step 1: Create two empty queues
    firstQueue = Queue()
    secondQueue = Queue()

    # Step 2: Create a leaf node for each unique
    # character and Enqueue it to the first queue
    # in non-decreasing order of frequency.
    # Initially second queue is empty.
    for i in range(size):
        firstQueue.enqueue(QueueNode(data[i], freq[i]))

    # Run while Queues contain more than one node.
    # Finally, first queue will be empty and
    # second queue will contain only one node
    while not (firstQueue.isEmpty() and
               secondQueue.isSizeOne()):

        # Step 3: Dequeue two nodes with the minimum
        # frequency by examining the front of both queues
        left = findMin(firstQueue, secondQueue)
        right = findMin(firstQueue, secondQueue)

        # Step 4: Create a new internal node with
        # frequency equal to the sum of the two
        # nodes frequencies. Enqueue this node
        # to second queue.
        top = QueueNode("{content}quot;, left.freq + right.freq,
                        left, right)
        secondQueue.enqueue(top)

    return secondQueue.dequeue()

# Prints huffman codes from the root of
# Huffman tree. It uses arr[] to store codes
def printCodes(root, arr):

    # Assign 0 to left edge and recur
    if root.left:
        arr.append(0)
        printCodes(root.left, arr)
        arr.pop(-1)

    # Assign 1 to right edge and recur
    if root.right:
        arr.append(1)
        printCodes(root.right, arr)
        arr.pop(-1)

    # If this is a leaf node, then it contains
    # one of the input characters, print the
    # character and its code from arr[]
    if root.isLeaf():
        print(f"{root.data}: ", end = "")
        for i in arr:
            print(i, end = "")

        print()

# The main function that builds a Huffman
# tree and print codes by traversing the
# built Huffman tree
def HuffmanCodes(data, freq, size):

    # Construct Huffman Tree
    root = buildHuffmanTree(data, freq, size)

    # Print Huffman codes using the Huffman
    # tree built above
    arr = []
    printCodes(root, arr)

# Driver code
arr = ["a", "b", "c", "d", "e", "f"]
freq = [5, 9, 12, 13, 16, 45]
size = len(arr)

HuffmanCodes(arr, freq, size)

# This code is contributed by Kevin Joshi
```

**输出:**

```
f: 0
c: 100
d: 101
a: 1100
b: 1101
e: 111
```

**时间复杂度:** O(n)
如果输入没有排序，需要先排序后才能用上述算法处理。排序可以使用堆排序或合并排序来完成，这两种方式都在 Theta(nlogn)中运行。因此，对于未排序的输入，整体时间复杂度变为 0(nlogn)。

**参考:**
[【http://en.wikipedia.org/wiki/Huffman_coding】](http://en.wikipedia.org/wiki/Huffman_coding)
本文由[aashis Barnwal](https://www.facebook.com/barnwal.aashish)整理，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。