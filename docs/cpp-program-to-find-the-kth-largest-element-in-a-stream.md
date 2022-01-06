# C++程序寻找一个流中第 K 大的元素

> 原文:[https://www . geesforgeks . org/CPP-program-to-find-the-kth-最大的流中元素/](https://www.geeksforgeeks.org/cpp-program-to-find-the-kth-largest-element-in-a-stream/)

给定一个无限长的整数流，在任意时间点找到第 k 个最大的元素。
**例:**

```
Input:
stream[] = {10, 20, 11, 70, 50, 40, 100, 5, ...}
k = 3

Output:    {_,   _, 10, 11, 20, 40, 50,  50, ...}
```

允许的额外空间为 0(k)。

在下面的文章中，我们讨论了寻找数组中第 k 大元素的不同方法。
[未排序数组中第 K 个最小/最大元素|集合 1](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array/)
[未排序数组中第 K 个最小/最大元素|集合 2(预期线性时间)](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-2-expected-linear-time/)
[未排序数组中第 K 个最小/最大元素|集合 3(最坏情况线性时间)](https://www.geeksforgeeks.org/kth-smallestlargest-element-unsorted-array-set-3-worst-case-linear-time/)
这里我们有一个流而不是整个数组，我们只允许存储 K 个元素。

一个**简单的解决方法**就是保持一个大小为 k 的数组，思路是保持数组的排序，这样在 O(1)时间内就可以找到第 k 个最大的元素(如果数组按递增顺序排序，我们只需要返回数组的第一个元素)
如何处理一个流的新元素？
对于流中的每个新元素，检查新元素是否小于当前第 k 个最大元素。如果是，那就忽略它。如果否，则从数组中移除最小的元素，并按排序顺序插入新元素。处理一个新元素的时间复杂度是 O(k)。

一个**更好的解决方案**是使用大小为 k 的自平衡二叉查找树。第 k 个最大的元素可以在 O(Logk)时间内找到。
如何加工新元素的流？
对于流中的每个新元素，检查新元素是否小于当前第 k 个最大元素。如果是，那就忽略它。如果没有，则从树中移除最小的元素并插入新元素。处理一个新元素的时间复杂度是 O(Logk)。

一个有效的解决方案是使用 k 大小的最小堆来存储 k 个最大的流元素。第 k 个最大的元素总是在根，可以在 O(1)时间找到。
如何加工新元素的流？
比较新元素与堆根。如果新元素较小，则忽略它。否则，用新元素替换根目录，并为修改后的堆的根目录调用 heapify。寻找第 k 大元素的时间复杂度是 O(Logk)。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// A C++ program to find k'th 
// smallest element in a stream
#include <climits>
#include <iostream>
using namespace std;

// Prototype of a utility function 
// to swap two integers
void swap(int* x, int* y);

// A class for Min Heap
class MinHeap {
    int* harr; // pointer to array of elements in heap
    int capacity; // maximum possible size of min heap
    int heap_size; // Current number of elements in min heap
public:
    MinHeap(int a[], int size); // Constructor
    void buildHeap();
    void MinHeapify(
        int i); // To minheapify subtree rooted with index i
    int parent(int i) { return (i - 1) / 2; }
    int left(int i) { return (2 * i + 1); }
    int right(int i) { return (2 * i + 2); }
    int extractMin(); // extracts root (minimum) element
    int getMin() { return harr[0]; }

    // to replace root with new node x and heapify() new
    // root
    void replaceMin(int x)
    {
        harr[0] = x;
        MinHeapify(0);
    }
};

MinHeap::MinHeap(int a[], int size)
{
    heap_size = size;
    harr = a; // store address of array
}

void MinHeap::buildHeap()
{
    int i = (heap_size - 1) / 2;
    while (i >= 0) {
        MinHeapify(i);
        i--;
    }
}

// Method to remove minimum element 
// (or root) from min heap
int MinHeap::extractMin()
{
    if (heap_size == 0)
        return INT_MAX;

    // Store the minimum vakue.
    int root = harr[0];

    // If there are more than 1 items, 
    // move the last item to
    // root and call heapify.
    if (heap_size > 1) {
        harr[0] = harr[heap_size - 1];
        MinHeapify(0);
    }
    heap_size--;

    return root;
}

// A recursive method to heapify a subtree with root at
// given index This method assumes that the subtrees are
// already heapified
void MinHeap::MinHeapify(int i)
{
    int l = left(i);
    int r = right(i);
    int smallest = i;
    if (l < heap_size && harr[l] < harr[i])
        smallest = l;
    if (r < heap_size && harr[r] < harr[smallest])
        smallest = r;
    if (smallest != i) {
        swap(&harr[i], &harr[smallest]);
        MinHeapify(smallest);
    }
}

// A utility function to swap two elements
void swap(int* x, int* y)
{
    int temp = *x;
    *x = *y;
    *y = temp;
}

// Function to return k'th largest element from input stream
void kthLargest(int k)
{
    // count is total no. of elements in stream seen so far
    int count = 0, x; // x is for new element

    // Create a min heap of size k
    int* arr = new int[k];
    MinHeap mh(arr, k);

    while (1) {
        // Take next element from stream
        cout << "Enter next element of stream ";
        cin >> x;

        // Nothing much to do for first k-1 elements
        if (count < k - 1) {
            arr[count] = x;
            count++;
        }

        else {
            // If this is k'th element, then store it
            // and build the heap created above
            if (count == k - 1) {
                arr[count] = x;
                mh.buildHeap();
            }

            else {
                // If next element is greater than
                // k'th largest, then replace the root
                if (x > mh.getMin())
                    mh.replaceMin(x); // replaceMin calls
                                      // heapify()
            }

            // Root of heap is k'th largest element
            cout << "K'th largest element is "
                 << mh.getMin() << endl;
            count++;
        }
    }
}

// Driver program to test above methods
int main()
{
    int k = 3;
    cout << "K is " << k << endl;
    kthLargest(k);
    return 0;
}
```

**输出:**

```
K is 3
Enter next element of stream 23
Enter next element of stream 10
Enter next element of stream 15
K'th largest element is 10
Enter next element of stream 70
K'th largest element is 15
Enter next element of stream 5
K'th largest element is 15
Enter next element of stream 80
K'th largest element is 23
Enter next element of stream 100
K'th largest element is 70
Enter next element of stream
CTRL + C pressed
```

**使用优先级队列的实现:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

vector<int> kthLargest(int k, int arr[], int n)
{
    vector<int> ans(n);

    // Creating a min-heap using priority queue
    priority_queue<int, vector<int>, greater<int> > pq;

    // Iterating through each element
    for (int i = 0; i < n; i++) {
        // If size of priority
        // queue is less than k
        if (pq.size() < k)
            pq.push(arr[i]);
        else {
            if (arr[i] > pq.top()) {
                pq.pop();
                pq.push(arr[i]);
            }
        }

        // If size is less than k
        if (pq.size() < k)
            ans[i] = -1;
        else
            ans[i] = pq.top();
    }

    return ans;
}

// Driver Code
int main()
{
    int n = 6;
    int arr[n] = { 1, 2, 3, 4, 5, 6 };
    int k = 4;

    // Function call
    vector<int> v = kthLargest(k, arr, n);
    for (auto it : v)
        cout << it << " ";
    return 0;
}
```

**Output**

```
-1 -1 -1 1 2 3 
```

详情请参考[流中第 K 大元素](https://www.geeksforgeeks.org/kth-largest-element-in-a-stream/)的完整文章！