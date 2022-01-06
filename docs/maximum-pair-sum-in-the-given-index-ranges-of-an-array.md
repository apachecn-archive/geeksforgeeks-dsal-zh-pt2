# 给定数组索引范围内的最大对和

> 原文:[https://www . geeksforgeeks . org/给定数组索引范围中的最大对和/](https://www.geeksforgeeks.org/maximum-pair-sum-in-the-given-index-ranges-of-an-array/)

给定一个包含正整数 **N** 和查询数 **Q** 的数组 **arr** ，对于每个查询任务，在给定的索引范围**【L，R】**内寻找最大对和，其中 **L** 和 **R** 分别是**低**和**高**索引。

**示例:**

> **输入:** arr = {3，4，5，6，7，8}，Q[][2] = [[0，3]，[3，5]]
> **输出:**
> 11
> 15
> **解释:**
> 对于第一个查询，子阵列为[3，4，5，6]
> 所有对为(3，4)，(3，5)，(3，6)，(4，5)，(4，6)，(5，6) 8]
> 子阵列的所有对都是(6，7)，(6，8)，(7，8)
> 因此最大对和= (7 + 8) = 15

**简单方法:**对于每个查询范围，执行以下操作

1.  查找给定查询范围内的最大值和第二个最大值。
2.  最大值和第二个最大值之和将是给定范围的最大对和。

以下是上述方法的实现:

## C++

```
// C++ program to find maximum
// pair sum in the given
// index range of an Array
#include <bits/stdc++.h>
using namespace std;

// Node structure to store a query
struct node {
    int f;
    int s;
};

// Function to find the required sum
void findSum(int* arr, int n,
             int Q, node* query)
{

    // Run a loop to iterate
    // over query array
    for (int i = 0; i < Q; i++) {

        // declare first 'f'
        // and second 's' variables
        int f, s;

        // Initialise them with 0
        f = s = 0;

        // Iterate over the
        // given array from
        // range query[i].f to query[i].s
        for (int j = query[i].f;
             j <= query[i].s;
             j++) {

            // If the array element
            // value is greater than
            // current f, store
            // current f in s and
            // array element value in f
            if (arr[j] >= f) {
                s = f;

                f = arr[j];
            }
            // else if element
            // is greater than s,
            // update s with
            // array element value
            else if (arr[j] > s)
                s = arr[j];
        }

        // print the sum of f and s
        cout << (f + s) << endl;
    }
}

// Driver code
int main()
{
    // Given array and number of queries
    int arr[] = { 3, 4, 5, 6, 7, 8 }, Q = 2;
    int n = sizeof(arr) / sizeof(arr[0]);

    // Declare and define queries
    node query[Q];
    query[0] = { 0, 3 };
    query[1] = { 3, 5 };

    findSum(arr, n, Q, query);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// pair sum in the given
// index range of an Array
class GFG{

// Node structure to store a query
static class node {
    int f;
    int s;
    public node(int f, int s) {
        this.f = f;
        this.s = s;
    }

};

// Function to find the required sum
static void findSum(int []arr, int n,
             int Q, node []query)
{

    // Run a loop to iterate
    // over query array
    for (int i = 0; i < Q; i++) {

        // declare first 'f'
        // and second 's' variables
        int f, s;

        // Initialise them with 0
        f = s = 0;

        // Iterate over the
        // given array from
        // range query[i].f to query[i].s
        for (int j = query[i].f;
             j <= query[i].s;
             j++) {

            // If the array element
            // value is greater than
            // current f, store
            // current f in s and
            // array element value in f
            if (arr[j] >= f) {
                s = f;

                f = arr[j];
            }
            // else if element
            // is greater than s,
            // update s with
            // array element value
            else if (arr[j] > s)
                s = arr[j];
        }

        // print the sum of f and s
        System.out.print((f + s) +"\n");
    }
}

// Driver code
public static void main(String[] args)
{
    // Given array and number of queries
    int arr[] = { 3, 4, 5, 6, 7, 8 }, Q = 2;
    int n = arr.length;

    // Declare and define queries
    node []query = new node[2];
    query[0] = new node( 0, 3 );
    query[1] =  new node(3, 5 );

    findSum(arr, n, Q, query);
}
}

// This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find maximum
// pair sum in the given
// index range of an Array
using System;

class GFG{

// Node structure to store a query
class node {
    public int f;
    public int s;
    public node(int f, int s) {
        this.f = f;
        this.s = s;
    }

};

// Function to find the required sum
static void findSum(int []arr, int n,
             int Q, node []query)
{

    // Run a loop to iterate
    // over query array
    for (int i = 0; i < Q; i++) {

        // declare first 'f'
        // and second 's' variables
        int f, s;

        // Initialise them with 0
        f = s = 0;

        // Iterate over the
        // given array from
        // range query[i].f to query[i].s
        for (int j = query[i].f;
             j <= query[i].s;
             j++) {

            // If the array element
            // value is greater than
            // current f, store
            // current f in s and
            // array element value in f
            if (arr[j] >= f) {
                s = f;

                f = arr[j];
            }
            // else if element
            // is greater than s,
            // update s with
            // array element value
            else if (arr[j] > s)
                s = arr[j];
        }

        // print the sum of f and s
        Console.Write((f + s) +"\n");
    }
}

// Driver code
public static void Main(String[] args)
{
    // Given array and number of queries
    int []arr = { 3, 4, 5, 6, 7, 8 };
    int Q = 2;
    int n = arr.Length;

    // Declare and define queries
    node []query = new node[2];
    query[0] = new node( 0, 3 );
    query[1] =  new node(3, 5 );

    findSum(arr, n, Q, query);
}
}

// This code is contributed by PrinciRaj1992
```

**Output:**

```
11
15

```

**性能分析:**

*   **时间复杂度:**在上面的方法中，对于每一个 **Q** 查询，我们都是长度数组 **N** 的活套。因此，时间复杂度将是 **O(N*Q)** 。
*   **辅助空间:**在上面的方法中，没有使用额外的空间，因此辅助空间的复杂性将是 **O(1)** 。

**高效方法:**想法是使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，其中段树的每个节点存储两个值:

*   下面给定子树的最大值
*   下面给定子树的第二个最大值

    **构建所需线段树的算法**

    > 1.  If the size of the array is 1, then we only need to store the first max=arr[start] and the second max=0, where start is the index of the array.
    > 2.  其他
    >     *   Recursively determine the first maximum value `(l1)` and the second maximum value `(l2)` of the left half of the array.
    >     *   Recursively determine the first maximum value `(r1)` and the second maximum value `(r2)` of the right half of the array.
    >     
    > 3.  We now determine the first and second max of the current node as
    >     `firstMax=max(l1, r1)` and `secondMax=max(min(l1, r1), max(l2, r2))`

    **查询寻找给定范围最大对和的算法**

    > 1.  If the range of nodes is within L and R, the value of the current
    >     node is returned.
    > 2.  Otherwise, if the range of the node is completely outside L and R, it returns 0.
    > 3.  Otherwise, find `first max(l1)` and `second max(l2)` recursively from the left half of
    >     , and find `firstMax(r1)` and `secondMax(r2)` recursively from the right half of
    >     .

    *   return the `max(l1, r1) and max(min(l1, r1), max(l2, r2)).`

        下面是上述方法的实现:

        ## 卡片打印处理机（Card Print Processor 的缩写）

        ```
        // C++ program to find maximum
        // pair sum in the given
        // index range of an Array

        #include <bits/stdc++.h>
        using namespace std;

        // Node structure to store a query
        struct node {
            int f;
            int s;
        };

        // Function to build the tree
        void build(
            int arr[], node tree[],
            int start, int end,
            int index)
        {
            // If there is just one element
            // in the array range,
            // set maximum as that element,
            // and second maximum as zero
            if (start == end) {
                tree[index].f = arr[start];

                tree[index].s = 0;

                return;
            }

            // Calculate the mid value
            int mid = start + (end - start) / 2;

            // Recursively build the tree
            // for the range [start, mid]
            // and store the value
            // at index (2 * index + 1)
            build(
                arr, tree, start,
                mid, 2 * index + 1);

            // Recursively build the tree
            // for the range [mid + 1, end]
            // and store the value
            // at index (2 * index + 2)
            build(
                arr, tree, mid + 1,
                end, 2 * index + 2);

            // Get the maximum and
            // second maximum from
            // both left and right subtrees
            int l1 = tree[2 * index + 1].f;
            int l2 = tree[2 * index + 1].s;
            int r1 = tree[2 * index + 2].f;
            int r2 = tree[2 * index + 2].s;

            // Set the maximum for this node as
            // maximum of l1 and r1
            tree[index].f = max(l1, r1);

            // Set the second maximum for this
            // node as maximum of
            // min(l1, r1) & max(l2, r2)
            tree[index].s
                = max(min(l1, r1),
                      max(l2, r2));
        }

        // Function to execute a
        // query on the segment tree
        node runQuery(
            node tree[], int start,
            int end, int index,
            int L, int R)
        {
            // If the range of
            // the node is completely
            // outside l and r then return 0
            if (R < start or L > end) {
                return { 0, 0 };
            }

            // If the range of the
            // node is within l and r
            // then return the value
            // of the present node
            if (L <= start and R >= end) {
                return tree[index];
            }

            // calculate mid value
            int mid = start + (end - start) / 2;

            // Recursively find first
            // max and second max from
            // the left half
            node Left
                = runQuery(
                    tree, start,
                    mid, 2 * index + 1,
                    L, R);

            // Recursively find first
            // max and second max from
            // the right half
            node Right
                = runQuery(
                    tree, mid + 1,
                    end, 2 * index + 2,
                    L, R);

            // Get the values
            // of l1, l2, r1, r2
            int l1 = Left.f;
            int l2 = Left.s;
            int r1 = Right.f;
            int r2 = Right.s;

            // return the maximum
            // as max(l1, r1), and
            // second maximum as
            // max(min(l1, r1), max(l2, r2))
            return { max(l1, r1),
                     max(min(l1, r1),
                         max(l2, r2)) };
        }

        // Function to find the required sum
        void findSum(int* arr, int n,
                     int Q, node* query)
        {

            // Declare an array of
            // length '4 * n + 1' and
            // build the tree
            node tree[4 * n + 1];
            build(arr, tree, 0, n - 1, 0);

            // Run a loop to iterate
            // over each query
            for (int i = 0; i < Q; i++) {

                // Call the query function
                // with given range
                node temp
                    = runQuery(
                        tree, 0,
                        n - 1, 0,
                        query[i].f,
                        query[i].s);

                // Store maximum and second
                // maximum in variables
                int f = temp.f;
                int s = temp.s;

                // Return sum of the maximum
                // and second maximum
                cout << (f + s) << endl;
            }
        }

        // Driver code
        int main()
        {
            // Given array and number of queries
            int arr[] = { 3, 4, 5, 6, 7, 8 }, Q = 2;

            int n = sizeof(arr) / sizeof(arr[0]);

            // Declare and define queries
            node query[Q];
            query[0] = { 0, 3 };
            query[1] = { 3, 5 };

            findSum(arr, n, Q, query);
        }
        ```

        ## Java 语言(一种计算机语言，尤用于创建网站)

        ```
        // Java program to find maximum
        // pair sum in the given
        // index range of an Array
        class GFG{

        // Node structure to store a query
        static class node {
            int f;
            int s;
            public node(int f, int s) {
                this.f = f;
                this.s = s;
            }
            public node() {
                // TODO Auto-generated constructor stub
            }

        };

        // Function to build the tree
        static void build(
            int arr[], node tree[],
            int start, int end,
            int index)
        {
            // If there is just one element
            // in the array range,
            // set maximum as that element,
            // and second maximum as zero
            if (start == end ) {
                tree[index].f = arr[start];

                tree[index].s = 0;

                return;
            }

            // Calculate the mid value
            int mid = start + (end - start) / 2;

            // Recursively build the tree
            // for the range [start, mid]
            // and store the value
            // at index (2 * index + 1)
            build(
                arr, tree, start,
                mid, 2 * index + 1);

            // Recursively build the tree
            // for the range [mid + 1, end]
            // and store the value
            // at index (2 * index + 2)
            build(
                arr, tree, mid + 1,
                end, 2 * index + 2);

            // Get the maximum and
            // second maximum from
            // both left and right subtrees
            int l1 = tree[2 * index + 1].f;
            int l2 = tree[2 * index + 1].s;
            int r1 = tree[2 * index + 2].f;
            int r2 = tree[2 * index + 2].s;

            // Set the maximum for this node as
            // maximum of l1 and r1
            tree[index].f = Math.max(l1, r1);

            // Set the second maximum for this
            // node as maximum of
            // Math.min(l1, r1) & Math.max(l2, r2)
            tree[index].s
                = Math.max(Math.min(l1, r1),
                      Math.max(l2, r2));
        }

        // Function to execute a
        // query on the segment tree
        static node runQuery(
            node tree[], int start,
            int end, int index,
            int L, int R)
        {
            // If the range of
            // the node is completely
            // outside l and r then return 0
            if (R < start || L > end) {
                return new node( 0, 0 );
            }

            // If the range of the
            // node is within l and r
            // then return the value
            // of the present node
            if (L <= start && R >= end) {
                return tree[index];
            }

            // calculate mid value
            int mid = start + (end - start) / 2;

            // Recursively find first
            // max and second max from
            // the left half
            node Left
                = runQuery(
                    tree, start,
                    mid, 2 * index + 1,
                    L, R);

            // Recursively find first
            // max and second max from
            // the right half
            node Right
                = runQuery(
                    tree, mid + 1,
                    end, 2 * index + 2,
                    L, R);

            // Get the values
            // of l1, l2, r1, r2
            int l1 = Left.f;
            int l2 = Left.s;
            int r1 = Right.f;
            int r2 = Right.s;

            // return the maximum
            // as Math.max(l1, r1), and
            // second maximum as
            // Math.max(Math.min(l1, r1), Math.max(l2, r2))
            return new node( Math.max(l1, r1),
                     Math.max(Math.min(l1, r1),
                         Math.max(l2, r2)) );
        }

        // Function to find the required sum
        static void findSum(int []arr, int n,
                     int Q, node []query)
        {

            // Declare an array of
            // length '4 * n + 1' and
            // build the tree
            node []tree = new node[4 * n + 1];
            for(int i=0;i<4 * n + 1;i++) {
                tree[i] = new node();
            }
            build(arr, tree, 0, n - 1, 0);

            // Run a loop to iterate
            // over each query
            for (int i = 0; i < Q; i++) {

                // Call the query function
                // with given range
                node temp
                    = runQuery(
                        tree, 0,
                        n - 1, 0,
                        query[i].f,
                        query[i].s);

                // Store maximum and second
                // maximum in variables
                int f = temp.f;
                int s = temp.s;

                // Return sum of the maximum
                // and second maximum
                System.out.print((f + s) +"\n");
            }
        }

        // Driver code
        public static void main(String[] args)
        {
            // Given array and number of queries
            int arr[] = { 3, 4, 5, 6, 7, 8 }, Q = 2;

            int n = arr.length;

            // Declare and define queries
            node []query = new node[Q];
            query[0] = new node( 0, 3 );
            query[1] = new node( 3, 5 );

            findSum(arr, n, Q, query);
        }
        }

        // This code is contributed by Princi Singh
        ```

        ## C#

        ```
        // C# program to find maximum
        // pair sum in the given
        // index range of an Array
        using System;

        class GFG{

        // Node structure to store a query
        class node {
            public int f;
            public int s;
            public node(int f, int s) {
                this.f = f;
                this.s = s;
            }
            public node() {
                // TODO Auto-generated constructor stub
            }

        };

        // Function to build the tree
        static void build(
            int []arr, node []tree,
            int start, int end,
            int index)
        {
            // If there is just one element
            // in the array range,
            // set maximum as that element,
            // and second maximum as zero
            if (start == end ) {
                tree[index].f = arr[start];

                tree[index].s = 0;

                return;
            }

            // Calculate the mid value
            int mid = start + (end - start) / 2;

            // Recursively build the tree
            // for the range [start, mid]
            // and store the value
            // at index (2 * index + 1)
            build(
                arr, tree, start,
                mid, 2 * index + 1);

            // Recursively build the tree
            // for the range [mid + 1, end]
            // and store the value
            // at index (2 * index + 2)
            build(
                arr, tree, mid + 1,
                end, 2 * index + 2);

            // Get the maximum and
            // second maximum from
            // both left and right subtrees
            int l1 = tree[2 * index + 1].f;
            int l2 = tree[2 * index + 1].s;
            int r1 = tree[2 * index + 2].f;
            int r2 = tree[2 * index + 2].s;

            // Set the maximum for this node as
            // maximum of l1 and r1
            tree[index].f = Math.Max(l1, r1);

            // Set the second maximum for this
            // node as maximum of
            // Math.Min(l1, r1) & Math.Max(l2, r2)
            tree[index].s
                = Math.Max(Math.Min(l1, r1),
                      Math.Max(l2, r2));
        }

        // Function to execute a
        // query on the segment tree
        static node runQuery(
            node []tree, int start,
            int end, int index,
            int L, int R)
        {
            // If the range of
            // the node is completely
            // outside l and r then return 0
            if (R < start || L > end) {
                return new node( 0, 0 );
            }

            // If the range of the
            // node is within l and r
            // then return the value
            // of the present node
            if (L <= start && R >= end) {
                return tree[index];
            }

            // calculate mid value
            int mid = start + (end - start) / 2;

            // Recursively find first
            // max and second max from
            // the left half
            node Left
                = runQuery(
                    tree, start,
                    mid, 2 * index + 1,
                    L, R);

            // Recursively find first
            // max and second max from
            // the right half
            node Right
                = runQuery(
                    tree, mid + 1,
                    end, 2 * index + 2,
                    L, R);

            // Get the values
            // of l1, l2, r1, r2
            int l1 = Left.f;
            int l2 = Left.s;
            int r1 = Right.f;
            int r2 = Right.s;

            // return the maximum
            // as Math.Max(l1, r1), and
            // second maximum as
            // Math.Max(Math.Min(l1, r1), Math.Max(l2, r2))
            return new node( Math.Max(l1, r1),
                     Math.Max(Math.Min(l1, r1),
                         Math.Max(l2, r2)) );
        }

        // Function to find the required sum
        static void findSum(int []arr, int n,
                     int Q, node []query)
        {

            // Declare an array of
            // length '4 * n + 1' and
            // build the tree
            node []tree = new node[4 * n + 1];
            for(int i=0;i<4 * n + 1;i++) {
                tree[i] = new node();
            }
            build(arr, tree, 0, n - 1, 0);

            // Run a loop to iterate
            // over each query
            for (int i = 0; i < Q; i++) {

                // Call the query function
                // with given range
                node temp
                    = runQuery(
                        tree, 0,
                        n - 1, 0,
                        query[i].f,
                        query[i].s);

                // Store maximum and second
                // maximum in variables
                int f = temp.f;
                int s = temp.s;

                // Return sum of the maximum
                // and second maximum
                Console.Write((f + s) +"\n");
            }
        }

        // Driver code
        public static void Main(String[] args)
        {
            // Given array and number of queries
            int []arr = { 3, 4, 5, 6, 7, 8 };
            int Q = 2;

            int n = arr.Length;

            // Declare and define queries
            node []query = new node[Q];
            query[0] = new node( 0, 3 );
            query[1] = new node( 3, 5 );

            findSum(arr, n, Q, query);
        }
        }

        // This code is contributed by Rajput-Ji
        ```

        **Output:**

        ```
        11
        15

        ```

        **性能分析:**

        *   **时间复杂度:**在上面的方法中，我们正在构建一个时间复杂度为 **O(N)** 的段树，然后对于每个 **Q** 查询，我们在 **O(logN)** 时间内找到解决方案。所以整体时间复杂度是 **O(N+Q*logN)**
        *   **辅助空间复杂度:**在上面的方法中，我们使用额外的空间来存储正在占用(4 * N + 1)空间的段树。所以辅助空间复杂度是 **O(N)**