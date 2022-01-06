# 外部排序

> 原文:[https://www.geeksforgeeks.org/external-sorting/](https://www.geeksforgeeks.org/external-sorting/)

外部排序是一类能够处理大量数据的排序算法的术语。当被排序的数据不适合计算设备的主存储器(通常是随机存取存储器)时，需要外部排序，相反，它们必须驻留在较慢的外部存储器(通常是硬盘)中。外部排序通常使用混合排序合并策略。在排序阶段，读取、排序足够小的数据块，并将其写入一个临时文件。在合并阶段，排序后的子文件被合并成一个更大的文件。
外部排序的一个例子是外部合并排序算法，它对每个适合 RAM 的块进行排序，然后将排序后的块合并在一起。我们首先将文件分成**个运行**，这样一个运行的大小就足够小，可以放入主内存。然后使用合并排序算法对主存中的每个运行进行排序。最后，将生成的运行合并到连续更大的运行中，直到文件被排序。

算法/代码的先决条件:
[【合并排序】](http://geeksquiz.com/merge-sort/):用于对单个运行进行排序(运行是文件的一部分，足够小，可以放入主内存)
[:合并 K 个排序数组](https://www.geeksforgeeks.org/merge-k-sorted-arrays/):用于合并排序的运行。
下面是 C++实现中使用的步骤。
**输入:**

```
input_file  : Name of input file. input.txt
output_file : Name of output file, output.txt
run_size : Size of a run (can fit in RAM)
num_ways : Number of runs to be merged
```

**<u>解决方案:</u>**
思路很简单，由于尺寸很大，所有元素不能一次排序。因此，数据被分成块，然后使用合并排序进行排序。然后将排序后的数据转储到文件中。因为如此庞大的数据量无法完全处理。现在在对单个块进行排序之后。利用合并 k 个排序数组的思想对整个数组进行排序。
**算法:**

1.  读取 input_file，以便一次最多读取“run_size”元素。对数组中的每次运行读取执行以下操作。
2.  使用[合并排序](http://geeksquiz.com/merge-sort/)对运行进行排序。
3.  将排序后的数组存储在文件中。让我们对我的档案说“我”。
4.  使用所讨论的方法合并排序的文件[合并 k 个排序的数组](https://www.geeksforgeeks.org/merge-k-sorted-arrays/)

下面是上述步骤的 C++实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to implement
// external sorting using
// merge sort
#include <bits/stdc++.h>
using namespace std;

struct MinHeapNode {
    // The element to be stored
    int element;

    // index of the array from which
    // the element is taken
    int i;
};

// Prototype of a utility function
// to swap two min heap nodes
void swap(MinHeapNode* x, MinHeapNode* y);

// A class for Min Heap
class MinHeap {
    // pointer to array of elements in heap
    MinHeapNode* harr;

    // size of min heap
    int heap_size;

public:
    // Constructor: creates a min
    // heap of given size
    MinHeap(MinHeapNode a[], int size);

    // to heapify a subtree with
    // root at given index
    void MinHeapify(int);

    // to get index of left child
    // of node at index i
    int left(int i) { return (2 * i + 1); }

    // to get index of right child
    // of node at index i
    int right(int i) { return (2 * i + 2); }

    // to get the root
    MinHeapNode getMin() { return harr[0]; }

    // to replace root with new node
    // x and heapify() new root
    void replaceMin(MinHeapNode x)
    {
        harr[0] = x;
        MinHeapify(0);
    }
};

// Constructor: Builds a heap from
// a given array a[] of given size
MinHeap::MinHeap(MinHeapNode a[], int size)
{
    heap_size = size;
    harr = a; // store address of array
    int i = (heap_size - 1) / 2;
    while (i >= 0) {
        MinHeapify(i);
        i--;
    }
}

// A recursive method to heapify
// a subtree with root
// at given index. This method
// assumes that the
// subtrees are already heapified
void MinHeap::MinHeapify(int i)
{
    int l = left(i);
    int r = right(i);
    int smallest = i;
    if (l < heap_size && harr[l].element < harr[i].element)
        smallest = l;
    if (r < heap_size && harr[r].element < harr[smallest].element)
        smallest = r;
    if (smallest != i) {
        swap(&harr[i], &harr[smallest]);
        MinHeapify(smallest);
    }
}

// A utility function to swap two elements
void swap(MinHeapNode* x, MinHeapNode* y)
{
    MinHeapNode temp = *x;
    *x = *y;
    *y = temp;
}

// Merges two subarrays of arr[].
// First subarray is arr[l..m]
// Second subarray is arr[m+1..r]
void merge(int arr[], int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 = r - m;

    /* create temp arrays */
    int L[n1], R[n2];

    /* Copy data to temp arrays L[] and R[] */
    for (i = 0; i < n1; i++)
        L[i] = arr[l + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[m + 1 + j];

    /* Merge the temp arrays back into arr[l..r]*/
    // Initial index of first subarray
    i = 0;

    // Initial index of second subarray
    j = 0;

    // Initial index of merged subarray
    k = l;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j])
            arr[k++] = L[i++];
        else
            arr[k++] = R[j++];
    }

    /* Copy the remaining elements of L[],
        if there are any */
    while (i < n1)
        arr[k++] = L[i++];

    /* Copy the remaining elements of R[],
        if there are any */
    while (j < n2)
        arr[k++] = R[j++];
}

/* l is for left index and r is right index of the
   sub-array of arr to be sorted */
void mergeSort(int arr[], int l, int r)
{
    if (l < r) {
        // Same as (l+r)/2, but avoids overflow for
        // large l and h
        int m = l + (r - l) / 2;

        // Sort first and second halves
        mergeSort(arr, l, m);
        mergeSort(arr, m + 1, r);

        merge(arr, l, m, r);
    }
}

FILE* openFile(char* fileName, char* mode)
{
    FILE* fp = fopen(fileName, mode);
    if (fp == NULL) {
        perror("Error while opening the file.\n");
        exit(EXIT_FAILURE);
    }
    return fp;
}

// Merges k sorted files. Names of files are assumed
// to be 1, 2, 3, ... k
void mergeFiles(char* output_file, int n, int k)
{
    FILE* in[k];
    for (int i = 0; i < k; i++) {
        char fileName[2];

        // convert i to string
        snprintf(fileName, sizeof(fileName),
                 "%d", i);

        // Open output files in read mode.
        in[i] = openFile(fileName, "r");
    }

    // FINAL OUTPUT FILE
    FILE* out = openFile(output_file, "w");

    // Create a min heap with k heap
    // nodes. Every heap node
    // has first element of scratch
    // output file
    MinHeapNode* harr = new MinHeapNode[k];
    int i;
    for (i = 0; i < k; i++) {
        // break if no output file is empty and
        // index i will be no. of input files
        if (fscanf(in[i], "%d ", &harr[i].element) != 1)
            break;

        // Index of scratch output file
        harr[i].i = i;
    }
    // Create the heap
    MinHeap hp(harr, i);

    int count = 0;

    // Now one by one get the
    // minimum element from min
    // heap and replace it with
    // next element.
    // run till all filled input
    // files reach EOF
    while (count != i) {
        // Get the minimum element
        // and store it in output file
        MinHeapNode root = hp.getMin();
        fprintf(out, "%d ", root.element);

        // Find the next element that
        // will replace current
        // root of heap. The next element
        // belongs to same
        // input file as the current min element.
        if (fscanf(in[root.i], "%d ",
                   &root.element)
            != 1) {
            root.element = INT_MAX;
            count++;
        }

        // Replace root with next
        // element of input file
        hp.replaceMin(root);
    }

    // close input and output files
    for (int i = 0; i < k; i++)
        fclose(in[i]);

    fclose(out);
}

// Using a merge-sort algorithm,
// create the initial runs
// and divide them evenly among
// the output files
void createInitialRuns(
    char* input_file, int run_size,
    int num_ways)
{
    // For big input file
    FILE* in = openFile(input_file, "r");

    // output scratch files
    FILE* out[num_ways];
    char fileName[2];
    for (int i = 0; i < num_ways; i++) {
        // convert i to string
        snprintf(fileName, sizeof(fileName),
                 "%d", i);

        // Open output files in write mode.
        out[i] = openFile(fileName, "w");
    }

    // allocate a dynamic array large enough
    // to accommodate runs of size run_size
    int* arr = (int*)malloc(
        run_size * sizeof(int));

    bool more_input = true;
    int next_output_file = 0;

    int i;
    while (more_input) {
        // write run_size elements
        // into arr from input file
        for (i = 0; i < run_size; i++) {
            if (fscanf(in, "%d ", &arr[i]) != 1) {
                more_input = false;
                break;
            }
        }

        // sort array using merge sort
        mergeSort(arr, 0, i - 1);

        // write the records to the
        // appropriate scratch output file
        // can't assume that the loop
        // runs to run_size
        // since the last run's length
        // may be less than run_size
        for (int j = 0; j < i; j++)
            fprintf(out[next_output_file],
                    "%d ", arr[j]);

        next_output_file++;
    }

    // close input and output files
    for (int i = 0; i < num_ways; i++)
        fclose(out[i]);

    fclose(in);
}

// For sorting data stored on disk
void externalSort(
    char* input_file, char* output_file,
    int num_ways, int run_size)
{
    // read the input file,
    // create the initial runs,
    // and assign the runs to
    // the scratch output files
    createInitialRuns(input_file,
                      run_size, num_ways);

    // Merge the runs using
    // the K-way merging
    mergeFiles(output_file, run_size, num_ways);
}

// Driver program to test above
int main()
{
    // No. of Partitions of input file.
    int num_ways = 10;

    // The size of each partition
    int run_size = 1000;

    char input_file[] = "input.txt";
    char output_file[] = "output.txt";

    FILE* in = openFile(input_file, "w");

    srand(time(NULL));

    // generate input
    for (int i = 0; i < num_ways * run_size; i++)
        fprintf(in, "%d ", rand());

    fclose(in);

    externalSort(input_file, output_file, num_ways,
                 run_size);

    return 0;
}
```

**复杂度分析:**

*   **时间复杂度:** O(n * log n)。
    合并排序所用时间为 0(游程*游程 _ 大小*日志游程 _ 大小)，等于 0(n 个日志游程 _ 大小)。为了合并排序后的数组，时间复杂度为 0(n * log runs)。因此，整体时间复杂度为 O(n * log run_size + n * log runs)。由于 log run _ size+log runs = log run _ size * runs = log n，结果时间复杂度将为 O(n * log n)。
*   **辅助空间:** O(run_size)。
    run_size 是存储数组所需的空间。

**注意:**该代码在在线编译器上无法工作，因为它需要文件创建权限。当运行本地机器时，它产生具有 10000 个随机数的样本输入文件“input.txt”。它对数字进行排序，并将排序后的数字放入文件“output.txt”中。它还生成名称为 1、2，..存储已排序的运行。
**参考文献:**

*   [https://en.wikipedia.org/wiki/External_sorting](https://en.wikipedia.org/wiki/External_sorting)
*   [http://web . eecs . utk . edu/~ leparker/Courses/CS302-fall 06/Notes/external-sort 2 . html](http://web.eecs.utk.edu/~leparker/Courses/CS302-Fall06/Notes/external-sorting2.html)

本文由**阿迪蒂亚·戈尔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息