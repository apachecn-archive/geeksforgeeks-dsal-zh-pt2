# 如何在单个数组中高效实现 k 个队列？

> 原文:[https://www . geeksforgeeks . org/efficient-implement-k-queues-single-array/](https://www.geeksforgeeks.org/efficiently-implement-k-queues-single-array/)

我们已经讨论了[在一个数组](https://www.geeksforgeeks.org/efficiently-implement-k-stacks-single-array/)中 k 栈的有效实现。在这篇文章中，对队列也进行了讨论。以下是详细的问题陈述。
*创建代表 k 个队列的数据结构 kQueues。kQueues 的实现应该只使用一个数组，即 k 个队列应该使用相同的数组来存储元素。kQueues 必须支持以下功能。*
*入队(int x，int qn)–>将 x 添加到队列号‘qn’中，其中 qn 从 0 到 k-1*
*出队(int qn)–>从队列号‘qn’中删除一个元素，其中 qn 从 0 到 k-1*
**方法 1(将数组划分为大小为 n/k 的槽)**
实现 k 个队列的一个简单方法是将数组划分为 并且固定不同队列的槽，即，使用 arr[0]来为第一队列 arr[n/k-1]，并且使用 arr[n/k]来为队列 2 arr[2n/k-1]，其中 arr[]是用于实现两个队列的数组，并且数组的大小是 n。
该方法的问题是数组空间的低效使用。 即使 arr[]中有可用空间，排队操作也可能导致溢出。例如，考虑 k 为 2，数组大小 n 为 6。让我们将 3 个元素排在第一个队列中，不要将任何东西排在第二个队列中。当我们将第四个元素排入第一个队列时，即使数组中还有 3 个元素的空间，也会出现溢出。
**方法 2(一个空间高效的实现)**
这个思路类似于[栈帖](https://www.geeksforgeeks.org/efficiently-implement-k-stacks-single-array/)，这里我们需要使用三个额外的数组。在 stack post 中，我们需要两个额外的数组，还需要一个数组，因为在队列中，入队()和出队()操作是在不同的末端完成的。
以下是使用的三个额外数组:
1) **front[]** :大小为 k，存储所有队列中 front 元素的索引。
2) **后置[]** :大小为 k，存储所有队列中后置元素的索引。
2) **next[]** :大小为 n，存储数组 arr[]中所有项的下一项的索引。
这里 arr[]是存储 k 个栈的实际数组。
与 k 个队列一起，arr[]中的一堆空闲槽也被维护。这个堆栈的顶部存储在变量“free”中。
前面[]的所有条目都初始化为-1，表示所有队列都是空的。下一个[i]的所有条目都被初始化为 i+1，因为所有插槽最初都是空闲的，并指向下一个插槽。空闲堆栈的顶部，“空闲”被初始化为 0。
以下是上述思想的 C++实现。

## C++

```
// A C++ program to demonstrate implementation of k queues in a single
// array in time and space efficient way
#include<iostream>
#include<climits>
using namespace std;

// A C++ class to represent k queues in a single array of size n
class kQueues
{  
    // Array of size n to store actual content to be stored in queue
    int *arr;

    // Array of size k to store indexes of front elements of the queue 
    int *front;  

    // Array of size k to store indexes of rear elements of queue
    int *rear;

    // Array of size n to store next entry in all queues           
    int *next; 
    int n, k;

    int free; // To store the beginning index of the free list

public:
    //constructor to create k queue in an array of size n
    kQueues(int k, int n);

    // A utility function to check if there is space available
    bool isFull()   {  return (free == -1);  }

    // To enqueue an item in queue number 'qn' where qn is from 0 to k-1
    void enqueue(int item, int qn);

    // To dequeue an from queue number 'qn' where qn is from 0 to k-1
    int dequeue(int qn);

    // To check whether queue number 'qn' is empty or not
    bool isEmpty(int qn)  {  return (front[qn] == -1); }
};

// Constructor to create k queues in an array of size n
kQueues::kQueues(int k1, int n1)
{
    // Initialize n and k, and allocate memory for all arrays
    k = k1, n = n1;
    arr = new int[n];
    front = new int[k];
    rear = new int[k];
    next = new int[n];

    // Initialize all queues as empty
    for (int i = 0; i < k; i++)
        front[i] = -1;

    // Initialize all spaces as free
    free = 0;
    for (int i=0; i<n-1; i++)
        next[i] = i+1;
    next[n-1] = -1;  // -1 is used to indicate end of free list
}

// To enqueue an item in queue number 'qn' where qn is from 0 to k-1
void kQueues::enqueue(int item, int qn)
{
    // Overflow check
    if (isFull())
    {
        cout << "\nQueue Overflow\n";
        return;
    }

    int i = free;      // Store index of first free slot

    // Update index of free slot to index of next slot in free list
    free = next[i];

    if (isEmpty(qn))
        front[qn] = i;
    else
        next[rear[qn]] = i;

    next[i] = -1;

    // Update next of rear and then rear for queue number 'qn'
    rear[qn] = i;

    // Put the item in array
    arr[i] = item;
}

// To dequeue an from queue number 'qn' where qn is from 0 to k-1
int kQueues::dequeue(int qn)
{
    // Underflow checkSAS
    if (isEmpty(qn))
    {
         cout << "\nQueue Underflow\n";
         return INT_MAX;
    }

    // Find index of front item in queue number 'qn'
    int i = front[qn];

    front[qn] = next[i];  // Change top to store next of previous top

    // Attach the previous front to the beginning of free list
    next[i] = free;
    free = i;

    // Return the previous front item
    return arr[i];
}

/* Driver program to test kStacks class */
int main()
{
    // Let us create 3 queue in an array of size 10
    int k = 3, n = 10;
    kQueues ks(k, n);

    // Let us put some items in queue number 2
    ks.enqueue(15, 2);
    ks.enqueue(45, 2);

    // Let us put some items in queue number 1
    ks.enqueue(17, 1);
    ks.enqueue(49, 1);
    ks.enqueue(39, 1);

    // Let us put some items in queue number 0
    ks.enqueue(11, 0);
    ks.enqueue(9, 0);
    ks.enqueue(7, 0);

    cout << "Dequeued element from queue 2 is " << ks.dequeue(2) << endl;
    cout << "Dequeued element from queue 1 is " << ks.dequeue(1) << endl;
    cout << "Dequeued element from queue 0 is " << ks.dequeue(0) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to demonstrate implementation of k queues in a single
// array in time and space efficient way
public class KQueues {

    int k;
    int n;
    int[] arr;
    int[] front;
    int[] rear;
    int[] next;
    int free;

    KQueues(int k, int n){

        // Initialize n and k, and allocate memory for all arrays
        this.k = k;
        this.n = n;
        this.arr = new int[n];
        this.front = new int[k];
        this.rear = new int[k];
        this.next = new int[n];

        // Initialize all queues as empty
        for(int i= 0; i< k; i++) {
            front[i] = rear[i] = -1;
        }

        // Initialize all spaces as free
        free = 0;
        for(int i= 0; i< n-1; i++) {
            next[i] = i+1;
        }
        next[n-1] = -1;

    }

    public static void main(String[] args)
    {
        // Let us create 3 queue in an array of size 10
        int k = 3, n = 10;
        KQueues ks=  new KQueues(k, n);

        // Let us put some items in queue number 2
        ks.enqueue(15, 2);
        ks.enqueue(45, 2);

        // Let us put some items in queue number 1
        ks.enqueue(17, 1);
        ks.enqueue(49, 1);
        ks.enqueue(39, 1);

        // Let us put some items in queue number 0
        ks.enqueue(11, 0);
        ks.enqueue(9, 0);
        ks.enqueue(7, 0);

        System.out.println("Dequeued element from queue 2 is " +
                                ks.dequeue(2));
        System.out.println("Dequeued element from queue 1 is " +
                                ks.dequeue(1));
        System.out.println("Dequeued element from queue 0 is " +
                                ks.dequeue(0) );

    }

    // To check whether queue number 'i' is empty or not
    private boolean isEmpty(int i) {
        return front[i] == -1;
    }

    // To dequeue an from queue number 'i' where i is from 0 to k-1
    private boolean isFull(int i) {
        return free == -1;
    }

    // To enqueue an item in queue number 'j' where j is from 0 to k-1
    private void enqueue(int item, int j) {
        if(isFull(j)) {
            System.out.println("queue overflow");
            return;
        }

        int nextFree = next[free];

        if(isEmpty(j)) {
            rear[j] = front[j] = free;
        }else {
            // Update next of rear and then rear for queue number 'j'
            next[rear[j]] = free;
            rear[j] = free;
        }
        next[free] = -1;

        // Put the item in array
        arr[free] = item;

        // Update index of free slot to index of next slot in free list
        free = nextFree;
    }

    // To dequeue an from queue number 'i' where i is from 0 to k-1
    private int dequeue(int i) {
        // Underflow checkSAS
        if(isEmpty(i)) {
            System.out.println("Stack underflow");
            return Integer.MIN_VALUE;
        }

        // Find index of front item in queue number 'i'
        int frontIndex = front[i];

        // Change top to store next of previous top
        front[i] = next[frontIndex];

        // Attach the previous front to the beginning of free list
        next[frontIndex] = free;
        free = frontIndex;

        return arr[frontIndex];
    }

}
```

## 计算机编程语言

```
# A Python program to demonstrate implementation of k queues in a single
# array in time and space efficient way

class KQueues:
    def __init__(self, number_of_queues, array_length):
        self.number_of_queues = number_of_queues
        self.array_length = array_length
        self.array = [-1] * array_length
        self.front = [-1] * number_of_queues
        self.rear = [-1] * number_of_queues
        self.next_array = list(range(1, array_length))
        self.next_array.append(-1)
        self.free = 0

    # To check whether the current queue_number is empty or not
    def is_empty(self, queue_number):
        return True if self.front[queue_number] == -1 else False

    # To check whether the current queue_number is full or not
    def is_full(self, queue_number):
        return True if self.free == -1 else False

    # To enqueue the given item in the given queue_number where
    # queue_number is from 0 to number_of_queues-1
    def enqueue(self, item, queue_number):
        if self.is_full(queue_number):
            print("Queue FULL")
            return
        next_free = self.next_array[self.free]
        if self.is_empty(queue_number):
            self.front[queue_number] = self.rear[queue_number] = self.free
        else:
            self.next_array[self.rear[queue_number]] = self.free
            self.rear[queue_number] = self.free
        self.next_array[self.free] = -1
        self.array[self.free] = item
        self.free = next_free

    # To dequeue an item from the given queue_number where
    # queue_number is from 0 to number_of_queues-1
    def dequeue(self, queue_number):
        if self.is_empty(queue_number):
             print("Queue EMPTY")
             return

        front_index = self.front[queue_number]
        self.front[queue_number] = self.next_array[front_index]
        self.next_array[front_index] = self.free
        self.free = front_index
        return self.array[front_index]

if __name__ == "__main__":
    # Let us create 3 queue in an array of size 10 
    ks =  KQueues(3, 10)

    # Let us put some items in queue number 2 
    ks.enqueue(15, 2)
    ks.enqueue(45, 2)

    # Let us put some items in queue number 1 
    ks.enqueue(17, 1); 
    ks.enqueue(49, 1); 
    ks.enqueue(39, 1); 

    # Let us put some items in queue number 0 
    ks.enqueue(11, 0); 
    ks.enqueue(9, 0); 
    ks.enqueue(7, 0); 

    print("Dequeued element from queue 2 is {}".format(ks.dequeue(2)))
    print("Dequeued element from queue 1 is {}".format(ks.dequeue(1)))
    print("Dequeued element from queue 0 is {}".format(ks.dequeue(0)))
```

## C#

```
// A C# program to demonstrate implementation of k queues in a single
// array in time and space efficient way
using System;
public class KQueues
{
  int k;
  int n;
  int[] arr;
  int[] front;
  int[] rear;
  int[] next;
  int free;  
  KQueues(int k, int n)
  {

    // Initialize n and k, and
    // allocate memory for all arrays
    this.k = k;
    this.n = n;
    this.arr = new int[n];
    this.front = new int[k];
    this.rear = new int[k];
    this.next = new int[n];

    // Initialize all queues as empty
    for(int i = 0; i < k; i++)
    {
      front[i] = rear[i] = -1;
    }

    // Initialize all spaces as free
    free = 0;
    for(int i = 0; i < n - 1; i++)
    {
      next[i] = i + 1;
    }
    next[n - 1] = -1;       
  }

  public static void Main(String[] args)
  {

    // Let us create 3 queue in an array of size 10
    int k = 3, n = 10;
    KQueues ks = new KQueues(k, n);

    // Let us put some items in queue number 2
    ks.enqueue(15, 2);
    ks.enqueue(45, 2);

    // Let us put some items in queue number 1
    ks.enqueue(17, 1);
    ks.enqueue(49, 1);
    ks.enqueue(39, 1);

    // Let us put some items in queue number 0
    ks.enqueue(11, 0);
    ks.enqueue(9, 0);
    ks.enqueue(7, 0);

    Console.WriteLine("Dequeued element from queue 2 is " +
                      ks.dequeue(2));
    Console.WriteLine("Dequeued element from queue 1 is " +
                      ks.dequeue(1));
    Console.WriteLine("Dequeued element from queue 0 is " +
                      ks.dequeue(0) );

  }

  // To check whether queue number 'i' is empty or not
  private bool isEmpty(int i)
  {
    return front[i] == -1;
  }

  // To dequeue an from queue
  // number 'i' where i is from 0 to k-1
  private bool isFull(int i)
  {
    return free == -1;
  }

  // To enqueue an item in queue
  // number 'j' where j is from 0 to k-1
  private void enqueue(int item, int j)
  {
    if(isFull(j))
    {
      Console.WriteLine("queue overflow");
      return;
    }

    int nextFree = next[free];

    if(isEmpty(j))
    {
      rear[j] = front[j] = free;
    }
    else
    {
      // Update next of rear and then
      // rear for queue number 'j'
      next[rear[j]] = free;
      rear[j] = free;
    }
    next[free] = -1;

    // Put the item in array
    arr[free] = item;

    // Update index of free slot to
    // index of next slot in free list
    free = nextFree;
  }

  // To dequeue an from queue
  // number 'i' where i is from 0 to k-1
  private int dequeue(int i)
  {

    // Underflow checkSAS
    if(isEmpty(i))
    {
      Console.WriteLine("Stack underflow");
      return int.MinValue;
    }

    // Find index of front item in queue number 'i'
    int frontIndex = front[i];

    // Change top to store next of previous top
    front[i] = next[frontIndex];

    // Attach the previous front to the beginning of free list
    next[frontIndex] = free;
    free = frontIndex;       
    return arr[frontIndex];
  }   
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// A Javascript program to demonstrate implementation of k queues in a single
// array in time and space efficient way
class KQueues
{
    constructor(k,n)
    {
        // Initialize n and k, and allocate memory for all arrays
        this.k = k;
        this.n = n;
        this.arr = new Array(n);
        this.front = new Array(k);
        this.rear = new Array(k);
        this.next = new Array(n);

        // Initialize all queues as empty
        for(let i= 0; i< k; i++) {
            this.front[i] = this.rear[i] = -1;
        }

        // Initialize all spaces as free
        this.free = 0;
        for(let i= 0; i< n-1; i++) {
            this.next[i] = i+1;
        }
        this.next[n-1] = -1;
    }

    // To check whether queue number 'i' is empty or not
    isEmpty(i)
    {
        return this.front[i] == -1;
    }

    // To dequeue an from queue number 'i' where i is from 0 to k-1
    isFull(i)
    {
        return this.free == -1;
    }

    // To enqueue an item in queue number 'j' where j is from 0 to k-1
    enqueue(item,j)
    {
        if(this.isFull(j)) {
            document.write("queue overflow<br>");
            return;
        }

        let nextFree = this.next[this.free];

        if(this.isEmpty(j)) {
            this.rear[j] = this.front[j] = this.free;
        }else {
            // Update next of rear and then rear for queue number 'j'
            this.next[this.rear[j]] = this.free;
            this.rear[j] = this.free;
        }
        this.next[this.free] = -1;

        // Put the item in array
        this.arr[this.free] = item;

        // Update index of free slot to index of next slot in free list
        this.free = nextFree;
    }

    // To dequeue an from queue number 'i' where i is from 0 to k-1
    dequeue(i)
    {
        // Underflow checkSAS
        if(this.isEmpty(i)) {
            document.write("Stack underflow<br>");
            return Number.MIN_VALUE;
        }

        // Find index of front item in queue number 'i'
        let frontIndex = this.front[i];

        // Change top to store next of previous top
        this.front[i] = this.next[frontIndex];

        // Attach the previous front to the beginning of free list
        this.next[frontIndex] = this.free;
        this.free = frontIndex;

        return this.arr[frontIndex];
    }
}

// Let us create 3 queue in an array of size 10
        let k = 3, n = 10;
        let ks=  new KQueues(k, n);

        // Let us put some items in queue number 2
        ks.enqueue(15, 2);
        ks.enqueue(45, 2);

        // Let us put some items in queue number 1
        ks.enqueue(17, 1);
        ks.enqueue(49, 1);
        ks.enqueue(39, 1);

        // Let us put some items in queue number 0
        ks.enqueue(11, 0);
        ks.enqueue(9, 0);
        ks.enqueue(7, 0);

        document.write("Dequeued element from queue 2 is " +
                                ks.dequeue(2)+"<br>");
        document.write("Dequeued element from queue 1 is " +
                                ks.dequeue(1)+"<br>");
        document.write("Dequeued element from queue 0 is " +
                                ks.dequeue(0)+"<br>" );

// This code is contributed by avanitrachhadiya2155
</script>
```

输出:

```
Dequeued element from queue 2 is 15
Dequeued element from queue 1 is 17
Dequeued element from queue 0 is 11
```

入队()和出队()的时间复杂度为 O(1)。
上述实现的最佳部分是，如果队列中有可用的槽，则一个项目可以在任何队列中排队，即没有空间浪费。这种方法需要一些额外的空间。空间可能不是问题，因为队列项目通常很大，例如，员工、学生等的队列，其中每个项目都是数百字节。对于如此大的队列，使用的额外空间相对来说非常少，因为我们使用三个整数数组作为额外空间。
本文由**沙欣**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息