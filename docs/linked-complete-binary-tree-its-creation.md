# 链接完整二叉树&其创建

> 原文:[https://www . geesforgeks . org/link-complete-二叉树-its-creation/](https://www.geeksforgeeks.org/linked-complete-binary-tree-its-creation/)

完整的二叉树是这样的二叉树，其中除了最后一级之外的每一级‘l’都具有 2^l 节点，并且最后一级的节点都是左对齐的。完全二叉树主要用于基于堆的数据结构。
完整二叉树中的节点一次从左向右插入一级。如果某个级别已满，则该节点会插入新的级别。
下面是一些完整的二叉树。

```
       1
      / \
     2   3

        1
       / \
      2   3
     / \  / 
    4  5 6

```

以下二叉树不完整:

```
     1
    / \
   2   3
  /    /
  4   5

       1
      / \
     2   3
    / \  /
   4  5 6
  /
 7

```

完整的二叉树通常用数组表示。数组表示更好，因为它不包含任何空槽。给定父索引 I，它的左子由 2 * i + 1 给出，它的右子由 2 * i + 2 给出。因此不会浪费额外的空间，并且节省了存储左右指针的空间。然而，使用链接表示创建完整的二叉树可能是一个有趣的编程问题。这里的“链接”指的是非数组表示，其中左指针和右指针(或引用)分别用于引用左子对象和右子对象。如何编写一个总是在最后一级和最左边的可用位置添加新节点的 insert 函数？
为了创建一个链接的完整二叉树，我们需要以级别顺序的方式跟踪节点，使得下一个要插入的节点位于最左边的位置。队列数据结构可用于跟踪插入的节点。
以下是在完全二叉树中插入新节点的步骤。
T3】1。如果树是空的，用新节点初始化根。
**2。**否则，获取队列的前节点。
……。如果该前节点的左子节点不存在，则将左子节点设置为新节点。
……。否则，如果该前端节点的右子节点不存在，则将右子节点设置为新节点。
**3。**如果前节点同时有左子节点和右子节点，将其出列()。
**4。**将新节点入队()。
下面是实现:

## C

```
// Program for linked implementation of complete binary tree
#include <stdio.h>
#include <stdlib.h>

// For Queue Size
#define SIZE 50

// A tree node
struct node
{
    int data;
    struct node *right,*left;
};

// A queue node
struct Queue
{
    int front, rear;
    int size;
    struct node* *array;
};

// A utility function to create a new tree node
struct node* newNode(int data)
{
    struct node* temp = (struct node*) malloc(sizeof( struct node ));
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to create a new Queue
struct Queue* createQueue(int size)
{
    struct Queue* queue = (struct Queue*) malloc(sizeof( struct Queue ));

    queue->front = queue->rear = -1;
    queue->size = size;

    queue->array = (struct node**) malloc
                   (queue->size * sizeof( struct node* ));

    int i;
    for (i = 0; i < size; ++i)
        queue->array[i] = NULL;

    return queue;
}

// Standard Queue Functions
int isEmpty(struct Queue* queue)
{
    return queue->front == -1;
}

int isFull(struct Queue* queue)
{  return queue->rear == queue->size - 1; }

int hasOnlyOneItem(struct Queue* queue)
{  return queue->front == queue->rear;  }

void Enqueue(struct node *root, struct Queue* queue)
{
    if (isFull(queue))
        return;

    queue->array[++queue->rear] = root;

    if (isEmpty(queue))
        ++queue->front;
}

struct node* Dequeue(struct Queue* queue)
{
    if (isEmpty(queue))
        return NULL;

    struct node* temp = queue->array[queue->front];

    if (hasOnlyOneItem(queue))
        queue->front = queue->rear = -1;
    else
        ++queue->front;

    return temp;
}

struct node* getFront(struct Queue* queue)
{  return queue->array[queue->front]; }

// A utility function to check if a tree node
// has both left and right children
int hasBothChild(struct node* temp)
{
    return temp && temp->left && temp->right;
}

// Function to insert a new node in complete binary tree
void insert(struct node **root, int data, struct Queue* queue)
{
    // Create a new node for given data
    struct node *temp = newNode(data);

    // If the tree is empty, initialize the root with new node.
    if (!*root)
        *root = temp;

    else
    {
        // get the front node of the queue.
        struct node* front = getFront(queue);

        // If the left child of this front node doesn’t exist, set the
        // left child as the new node
        if (!front->left)
            front->left = temp;

        // If the right child of this front node doesn’t exist, set the
        // right child as the new node
        else if (!front->right)
            front->right = temp;

        // If the front node has both the left child and right child,
        // Dequeue() it.
        if (hasBothChild(front))
            Dequeue(queue);
    }

    // Enqueue() the new node for later insertions
    Enqueue(temp, queue);
}

// Standard level order traversal to test above function
void levelOrder(struct node* root)
{
    struct Queue* queue = createQueue(SIZE);

    Enqueue(root, queue);

    while (!isEmpty(queue))
    {
        struct node* temp = Dequeue(queue);

        printf("%d ", temp->data);

        if (temp->left)
            Enqueue(temp->left, queue);

        if (temp->right)
            Enqueue(temp->right, queue);
    }
}

// Driver program to test above functions
int main()
{
    struct node* root = NULL;
    struct Queue* queue = createQueue(SIZE);
    int i;

    for(i = 1; i <= 12; ++i)
        insert(&root, i, queue);

    levelOrder(root);

    return 0;
}
```

## C++

```
// Program for linked implementation of complete binary tree
#include <bits/stdc++.h>
using namespace std;

// For Queue Size
#define SIZE 50

// A tree node
class node
{
    public:
    int data;
    node *right,*left;
};

// A queue node
class Queue
{
    public:
    int front, rear;
    int size;
    node**array;
};

// A utility function to create a new tree node
node* newNode(int data)
{
    node* temp = new node();
    temp->data = data;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to create a new Queue
Queue* createQueue(int size)
{
    Queue* queue = new Queue();

    queue->front = queue->rear = -1;
    queue->size = size;

    queue->array = new node*[queue->size * sizeof( node* )];

    int i;
    for (i = 0; i < size; ++i)
        queue->array[i] = NULL;

    return queue;
}

// Standard Queue Functions
int isEmpty(Queue* queue)
{
    return queue->front == -1;
}

int isFull(Queue* queue)
{ return queue->rear == queue->size - 1; }

int hasOnlyOneItem(Queue* queue)
{ return queue->front == queue->rear; }

void Enqueue(node *root, Queue* queue)
{
    if (isFull(queue))
        return;

    queue->array[++queue->rear] = root;

    if (isEmpty(queue))
        ++queue->front;
}

node* Dequeue(Queue* queue)
{
    if (isEmpty(queue))
        return NULL;

    node* temp = queue->array[queue->front];

    if (hasOnlyOneItem(queue))
        queue->front = queue->rear = -1;
    else
        ++queue->front;

    return temp;
}

node* getFront(Queue* queue)
{ return queue->array[queue->front]; }

// A utility function to check if a tree node
// has both left and right children
int hasBothChild(node* temp)
{
    return temp && temp->left && temp->right;
}

// Function to insert a new node in complete binary tree
void insert(node **root, int data, Queue* queue)
{
    // Create a new node for given data
    node *temp = newNode(data);

    // If the tree is empty, initialize the root with new node.
    if (!*root)
        *root = temp;

    else
    {
        // get the front node of the queue.
        node* front = getFront(queue);

        // If the left child of this front node doesn’t exist, set the
        // left child as the new node
        if (!front->left)
            front->left = temp;

        // If the right child of this front node doesn’t exist, set the
        // right child as the new node
        else if (!front->right)
            front->right = temp;

        // If the front node has both the left child and right child,
        // Dequeue() it.
        if (hasBothChild(front))
            Dequeue(queue);
    }

    // Enqueue() the new node for later insertions
    Enqueue(temp, queue);
}

// Standard level order traversal to test above function
void levelOrder(node* root)
{
    Queue* queue = createQueue(SIZE);

    Enqueue(root, queue);

    while (!isEmpty(queue))
    {
        node* temp = Dequeue(queue);

        cout<<temp->data<<" ";

        if (temp->left)
            Enqueue(temp->left, queue);

        if (temp->right)
            Enqueue(temp->right, queue);
    }
}

// Driver program to test above functions
int main()
{
    node* root = NULL;
    Queue* queue = createQueue(SIZE);
    int i;

    for(i = 1; i <= 12; ++i)
        insert(&root, i, queue);

    levelOrder(root);

    return 0;
}

//This code is contributed by rathbhupendra
```

## 蟒蛇 3

```
# Program for linked implementation
# of complete binary tree

# For Queue Size
SIZE = 50

# A tree node
class node:

    def __init__(self, data):

        self.data = data
        self.right = None
        self.left = None

# A queue node
class Queue:

    def __init__(self):

        self.front = None
        self.rear = None
        self.size = 0
        self.array = []

# A utility function to
# create a new tree node
def newNode(data):

    temp = node(data)
    return temp

# A utility function to
# create a new Queue
def createQueue(size):

    global queue   
    queue = Queue();
    queue.front = queue.rear = -1;
    queue.size = size;
    queue.array = [None for i in range(size)]
    return queue;

# Standard Queue Functions
def isEmpty(queue):

    return queue.front == -1

def isFull(queue):

    return queue.rear == queue.size - 1;

def hasOnlyOneItem(queue):

    return queue.front == queue.rear;

def Enqueue(root):

    if (isFull(queue)):
        return;

    queue.rear+=1
    queue.array[queue.rear] = root;

    if (isEmpty(queue)):
        queue.front+=1;

def Dequeue():

    if (isEmpty(queue)):
        return None;

    temp = queue.array[queue.front];

    if(hasOnlyOneItem(queue)):
        queue.front = queue.rear = -1;
    else:
        queue.front+=1

    return temp;

def getFront(queue):

    return queue.array[queue.front];

# A utility function to check
# if a tree node has both left
# and right children
def hasBothChild(temp):

    return (temp and temp.left and
            temp.right);

# Function to insert a new
# node in complete binary tree
def insert(root, data, queue):

    # Create a new node for
    # given data
    temp = newNode(data);

    # If the tree is empty,
    # initialize the root
    # with new node.
    if not root:
        root = temp;
    else:

        # get the front node of
        # the queue.
        front = getFront(queue);

        # If the left child of this
        # front node doesn’t exist,
        # set the left child as the
        # new node
        if (not front.left):
            front.left = temp;

        # If the right child of this
        # front node doesn’t exist, set
        # the right child as the new node
        elif (not front.right):
            front.right = temp;

        # If the front node has both the
        # left child and right child,
        # Dequeue() it.
        if (hasBothChild(front)):
            Dequeue();

    # Enqueue() the new node for
    # later insertions
    Enqueue(temp);
    return root

# Standard level order
# traversal to test above
# function
def levelOrder(root):

    queue = createQueue(SIZE);
    Enqueue(root);

    while (not isEmpty(queue)):   
        temp = Dequeue();        
        print(temp.data, end = ' ')
        if (temp.left):
            Enqueue(temp.left);
        if (temp.right):
            Enqueue(temp.right);

# Driver code 
if __name__ == "__main__":

    root = None
    queue = createQueue(SIZE);

    for i in range(1, 13):
        root=insert(root, i,
                    queue);

    levelOrder(root);

# This code is contributed by Rutvik_56
```

**Output:** 

```
1 2 3 4 5 6 7 8 9 10 11 12

```

本文由 [**【阿施·巴恩瓦尔】**](https://www.facebook.com/barnwal.aashish) 编辑，GeeksforGeeks 团队审核。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。