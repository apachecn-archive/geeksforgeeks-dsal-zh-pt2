# 在 K 次循环移位后，将给定的数组分成两半后，使用按位“或”来求数组和

> 原文:[https://www . geeksforgeeks . org/find-array-sum-use-bitwise-or-after-split-给定-array-in-two-half-after-k-circular-shift/](https://www.geeksforgeeks.org/find-array-sum-using-bitwise-or-after-splitting-given-array-in-two-halves-after-k-circular-shifts/)

给定一个长度为 **N** 的**数组 A[]** ，其中 N 是偶数，任务是回答 **Q** 独立的查询，其中每个查询由一个正整数 **K** 组成，代表对该数组执行的循环移位的次数，并通过对划分的数组执行按位或运算来找到元素的和。
***注意:**每个查询都从原始数组开始。*
**示例:**

> **输入:** A[] = {12，23，4，21，22，76}，Q = 1，K = 2
> **输出:** 117
> **说明:**
> 既然 K 是 2，修改数组 A[]={22，76，12，23，4，21}。
> 数组前半部分的按位 OR =(22 | 76 | 12)= 94
> 数组后半部分的按位 OR =(21 | 23 | 4)= 23
> OR 值之和为 94 + 23 = 117
> **输入:** A[] = {7，44，19，86，65，39，75，101}，Q = 1，K = 4
> **输出:
> 
> 数组前半部分的按位或= 111
> 数组后半部分的按位或= 127
> 或值之和为 111 + 127 = 238**

**天真方法:**
要解决上面提到的问题，最简单的方法是将数组的每个元素移动 **K % (N / 2)** ，然后遍历数组来计算每个查询的两部分的或。但是这种方法效率不高，因此可以进一步优化。
**高效方法:**
为了优化上述方法，我们可以借助[段树](https://www.geeksforgeeks.org/segment-tree-efficient-implementation/)数据结构。

> **观察:**
> 
> *   我们可以观察到，在恰好 **N / 2** 右循环移位之后，数组的两半变得与原始数组中的相同。这有效地将旋转次数减少到 **K % (N / 2)** 。
> *   执行右循环移位基本上是将数组的最后一个元素移到前面。所以对于任意正整数 **X** 执行 **X** 右循环移位等于将数组的最后 X 个元素移到前面。

以下是解决问题的步骤:

*   为原始数组 **A[]** 构造一个段树，并分配一个变量，比如说 **i = K % (N / 2)** 。
*   然后对于每个查询，我们使用段树来查找按位“或”；也就是从第一个**(N/2)–I–1**元素的末尾**或**开始的 I 元素的按位或。
*   然后计算**[(N/2)–I，N–I–1]**范围内元素的按位或。
*   将这两个结果相加，得到 ith 查询的答案。
    下面是上述方法的实现:

## C++

```
// C++ Program to find Bitwise OR of two
// equal halves of an array after performing
// K right circular shifts
#include <bits/stdc++.h>
const int MAX = 100005;
using namespace std;

// Array for storing
// the segment tree
int seg[4 * MAX];

// Function to build the segment tree
void build(int node, int l, int r, int a[])
{
    if (l == r)
        seg[node] = a[l];

    else {
        int mid = (l + r) / 2;

        build(2 * node, l, mid, a);
        build(2 * node + 1, mid + 1, r, a);

        seg[node] = (seg[2 * node]
                     | seg[2 * node + 1]);
    }
}

// Function to return the OR
// of elements in the range [l, r]
int query(int node, int l, int r,
          int start, int end, int a[])
{
    // Check for out of bound condition
    if (l > end or r < start)
        return 0;

    if (start <= l and r <= end)
        return seg[node];

    // Find middle of the range
    int mid = (l + r) / 2;

    // Recurse for all the elements in array
    return ((query(2 * node, l, mid,
                   start, end, a))
            | (query(2 * node + 1, mid + 1,
                     r, start, end, a)));
}

// Function to find the OR sum
void orsum(int a[], int n, int q, int k[])
{
    // Function to build the segment Tree
    build(1, 0, n - 1, a);

    // Loop to handle q queries
    for (int j = 0; j < q; j++) {
        // Effective number of
        // right circular shifts
        int i = k[j] % (n / 2);

        // Calculating the OR of
        // the two halves of the
        // array from the segment tree

        // OR of second half of the
        // array [n/2-i, n-1-i]
        int sec = query(1, 0, n - 1,
                        n / 2 - i, n - i - 1, a);

        // OR of first half of the array
        // [n-i, n-1]OR[0, n/2-1-i]
        int first = (query(1, 0, n - 1, 0,
                           n / 2 - 1 - i, a)
                     | query(1, 0, n - 1,
                             n - i, n - 1, a));

        int temp = sec + first;

        // Print final answer to the query
        cout << temp << endl;
    }
}

// Driver Code
int main()
{

    int a[] = { 7, 44, 19, 86, 65, 39, 75, 101 };
    int n = sizeof(a) / sizeof(a[0]);

    int q = 2;

    int k[q] = { 4, 2 };

    orsum(a, n, q, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Bitwise OR of two
// equal halves of an array after performing
// K right circular shifts
import java.util.*;

class GFG{

static int MAX = 100005;

// Array for storing
// the segment tree
static int []seg = new int[4 * MAX];

// Function to build the segment tree
static void build(int node, int l,
                  int r, int a[])
{
    if (l == r)
        seg[node] = a[l];

    else
    {
        int mid = (l + r) / 2;

        build(2 * node, l, mid, a);
        build(2 * node + 1, mid + 1, r, a);

        seg[node] = (seg[2 * node] |
                     seg[2 * node + 1]);
    }
}

// Function to return the OR
// of elements in the range [l, r]
static int query(int node, int l, int r,
                 int start, int end, int a[])
{

    // Check for out of bound condition
    if (l > end || r < start)
        return 0;

    if (start <= l && r <= end)
        return seg[node];

    // Find middle of the range
    int mid = (l + r) / 2;

    // Recurse for all the elements in array
    return ((query(2 * node, l, mid,
                   start, end, a)) |
            (query(2 * node + 1, mid + 1,
                   r, start, end, a)));
}

// Function to find the OR sum
static void orsum(int a[], int n,
                  int q, int k[])
{

    // Function to build the segment Tree
    build(1, 0, n - 1, a);

    // Loop to handle q queries
    for(int j = 0; j < q; j++)
    {

        // Effective number of
        // right circular shifts
        int i = k[j] % (n / 2);

        // Calculating the OR of
        // the two halves of the
        // array from the segment tree

        // OR of second half of the
        // array [n/2-i, n-1-i]
        int sec = query(1, 0, n - 1,
                        n / 2 - i,
                        n - i - 1, a);

        // OR of first half of the array
        // [n-i, n-1]OR[0, n/2-1-i]
        int first = (query(1, 0, n - 1, 0,
                           n / 2 - 1 - i, a) |
                     query(1, 0, n - 1,
                           n - i, n - 1, a));

        int temp = sec + first;

        // Print final answer to the query
        System.out.print(temp + "\n");
    }
}

// Driver Code
public static void main(String[] args)
{

    int a[] = { 7, 44, 19, 86, 65, 39, 75, 101 };
    int n = a.length;
    int q = 2;

    int k[] = { 4, 2 };

    orsum(a, n, q, k);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find Bitwise OR of two
# equal halves of an array after performing
# K right circular shifts
MAX = 100005

# Array for storing
# the segment tree
seg = [0] * (4 * MAX)

# Function to build the segment tree
def build(node, l, r, a):

    if (l == r):
        seg[node] = a[l]

    else:
        mid = (l + r) // 2

        build(2 * node, l, mid, a)
        build(2 * node + 1, mid + 1, r, a)

        seg[node] = (seg[2 * node] |
                     seg[2 * node + 1])

# Function to return the OR
# of elements in the range [l, r]
def query(node, l, r, start, end, a):

    # Check for out of bound condition
    if (l > end or r < start):
        return 0

    if (start <= l and r <= end):
        return seg[node]

    # Find middle of the range
    mid = (l + r) // 2

    # Recurse for all the elements in array
    return ((query(2 * node, l, mid,
                       start, end, a)) |
            (query(2 * node + 1, mid + 1,
                       r, start, end, a)))

# Function to find the OR sum
def orsum(a, n, q, k):

    # Function to build the segment Tree
    build(1, 0, n - 1, a)

    # Loop to handle q queries
    for j in range(q):

        # Effective number of
        # right circular shifts
        i = k[j] % (n // 2)

        # Calculating the OR of
        # the two halves of the
        # array from the segment tree

        # OR of second half of the
        # array [n/2-i, n-1-i]
        sec = query(1, 0, n - 1, n // 2 - i,
                          n - i - 1, a)

        # OR of first half of the array
        # [n-i, n-1]OR[0, n/2-1-i]
        first = (query(1, 0, n - 1, 0,
                             n // 2 -
                             1 - i, a) |
                 query(1, 0, n - 1,
                             n - i,
                             n - 1, a))

        temp = sec + first

        # Print final answer to the query
        print(temp)

# Driver Code
if __name__ == "__main__":

    a = [ 7, 44, 19, 86, 65, 39, 75, 101 ]
    n = len(a)

    q = 2
    k = [ 4, 2 ]

    orsum(a, n, q, k)

# This code is contributed by chitranayal
```

## C#

```
// C# program to find Bitwise OR of two
// equal halves of an array after performing
// K right circular shifts
using System;
class GFG{

static int MAX = 100005;

// Array for storing
// the segment tree
static int []seg = new int[4 * MAX];

// Function to build the segment tree
static void build(int node, int l,
                  int r, int []a)
{
    if (l == r)
        seg[node] = a[l];

    else
    {
        int mid = (l + r) / 2;

        build(2 * node, l, mid, a);
        build(2 * node + 1, mid + 1, r, a);

        seg[node] = (seg[2 * node] |
                     seg[2 * node + 1]);
    }
}

// Function to return the OR
// of elements in the range [l, r]
static int query(int node, int l, int r,
                 int start, int end, int []a)
{

    // Check for out of bound condition
    if (l > end || r < start)
        return 0;

    if (start <= l && r <= end)
        return seg[node];

    // Find middle of the range
    int mid = (l + r) / 2;

    // Recurse for all the elements in array
    return ((query(2 * node, l, mid,
                      start, end, a)) |
            (query(2 * node + 1, mid + 1,
                   r, start, end, a)));
}

// Function to find the OR sum
static void orsum(int []a, int n,
                  int q, int []k)
{

    // Function to build the segment Tree
    build(1, 0, n - 1, a);

    // Loop to handle q queries
    for(int j = 0; j < q; j++)
    {

        // Effective number of
        // right circular shifts
        int i = k[j] % (n / 2);

        // Calculating the OR of
        // the two halves of the
        // array from the segment tree

        // OR of second half of the
        // array [n/2-i, n-1-i]
        int sec = query(1, 0, n - 1,
                        n / 2 - i,
                        n - i - 1, a);

        // OR of first half of the array
        // [n-i, n-1]OR[0, n/2-1-i]
        int first = (query(1, 0, n - 1, 0,
                         n / 2 - 1 - i, a) |
                    query(1, 0, n - 1,
                          n - i, n - 1, a));

        int temp = sec + first;

        // Print readonly answer to the query
        Console.Write(temp + "\n");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 7, 44, 19, 86, 65, 39, 75, 101 };
    int n = a.Length;
    int q = 2;

    int []k = { 4, 2 };

    orsum(a, n, q, k);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program to find Bitwise OR of two
// equal halves of an array after performing
// K right circular shifts
    const MAX = 100005;

    // Array for storing
    // the segment tree
    var seg = Array(4 * MAX).fill(0);

    // Function to build the segment tree
    function build(node , l , r , a) {
        if (l == r)
            seg[node] = a[l];

        else {
            var mid = parseInt((l + r) / 2);

            build(2 * node, l, mid, a);
            build(2 * node + 1, mid + 1, r, a);

            seg[node] = (seg[2 * node] | seg[2 * node + 1]);
        }
    }

    // Function to return the OR
    // of elements in the range [l, r]
    function query(node , l , r , start , end , a) {

        // Check for out of bound condition
        if (l > end || r < start)
            return 0;

        if (start <= l && r <= end)
            return seg[node];

        // Find middle of the range
        var mid = parseInt((l + r) / 2);

        // Recurse for all the elements in array
        return ((query(2 * node, l, mid, start, end, a)) | (query(2 * node + 1, mid + 1, r, start, end, a)));
    }

    // Function to find the OR sum
    function orsum(a , n , q , k) {

        // Function to build the segment Tree
        build(1, 0, n - 1, a);

        // Loop to handle q queries
        for (j = 0; j < q; j++) {

            // Effective number of
            // right circular shifts
            var i = k[j] % (n / 2);

            // Calculating the OR of
            // the two halves of the
            // array from the segment tree

            // OR of second half of the
            // array [n/2-i, n-1-i]
            var sec = query(1, 0, n - 1, n / 2 - i, n - i - 1, a);

            // OR of first half of the array
            // [n-i, n-1]OR[0, n/2-1-i]
            var first = (query(1, 0, n - 1, 0, n / 2 - 1 - i, a) | query(1, 0, n - 1, n - i, n - 1, a));

            var temp = sec + first;

            // Print final answer to the query
            document.write(temp + "<br/>");
        }
    }

    // Driver Code
        var a = [ 7, 44, 19, 86, 65, 39, 75, 101 ];
        var n = a.length;
        var q = 2;

        var k = [ 4, 2 ];

        orsum(a, n, q, k);

// This code is contributed by Rajput-Ji.
</script>
```

**Output:** 

```
238
230
```