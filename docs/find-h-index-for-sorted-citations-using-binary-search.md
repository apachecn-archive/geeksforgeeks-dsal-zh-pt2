# 使用二分搜索法

找到分类引文的 H 索引

> 原文:[https://www . geesforgeks . org/find-h-index-for-sorted-引文-使用-binary-search/](https://www.geeksforgeeks.org/find-h-index-for-sorted-citations-using-binary-search/)

给定由非递增顺序的 N 个整数组成的数组引用 **[]** ，代表引用，任务是找到 H-index。

> **H 指数**通常被分配给研究者，以论文数量和引用次数来表示所做的贡献。H 指数(H)是指研究者至少有 H 篇论文被引用至少 H 次的最大值。

**示例:**

> **输入:**引文[] = {5，3，3，0，0}
> **输出:** 3
> **解释:**
> 至少有 3 篇论文(5，3，3)至少有 3 篇引文
> **输入:**引文[] = {5，4，2，1，1}
> **输出:** 2
> **解释:**
> 至少有 2 篇论文(5

**天真方法:**一个简单的解决方法是从左到右迭代论文，当引文 <sub>i</sub> 大于或等于索引时，增加 H-index。

**时间复杂度:** O(N)

**高效途径:**思路是利用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)对上述途径进行优化。H 指数可以在从 **0** 到 **N** 的范围内。检查给定值是否可能，检查**引用【值】**是否大于或等于**值**。

*   将二分搜索法的搜索范围初始化为 **0 到 N** 。
*   找到范围的中间元素。
*   检查引文的中间元素是否小于索引。如果是，那么将左边的范围更新为中间的元素。
*   否则，检查引文的中间元素是否大于索引。如果是这样，那么更新中间元素的正确范围。
*   否则，给定的索引就是引用的 H 索引。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the H-index
int hIndex(vector<int> citations,
           int n)
{

    int hindex = 0;

    // Set the range for binary search
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = (low + high) / 2;

        // Check if current citations is
        // possible
        if (citations[mid] >= (mid + 1)) {

            // Check to the right of mid
            low = mid + 1;

            // Update h-index
            hindex = mid + 1;
        }
        else {

            // Since current value is not
            // possible, check to the left
            // of mid
            high = mid - 1;
        }
    }

    // Print the h-index
    cout << hindex << endl;

    return hindex;
}

// Driver Code
int main()
{

    // citations
    int n = 5;
    vector<int> citations = { 5, 3, 3, 2, 2 };

    hIndex(citations, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.io.*;

class GFG{

// Function to find the H-index
static int hIndex(int[] citations, int n)
{
    int hindex = 0;

    // Set the range for binary search
    int low = 0, high = n - 1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        // Check if current citations is
        // possible
        if (citations[mid] >= (mid + 1))
        {

            // Check to the right of mid
            low = mid + 1;

            // Update h-index
            hindex = mid + 1;
        }
        else
        {

            // Since current value is not
            // possible, check to the left
            // of mid
            high = mid - 1;
        }
    }

    // Print the h-index
    System.out.println(hindex);

    return hindex;
}

// Driver Code
public static void main (String[] args)
{

    // citations
    int n = 5;
    int[] citations = { 5, 3, 3, 2, 2 };

    hIndex(citations, n);
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to find the H-index
def hIndex(citations, n):

    hindex = 0

    # Set the range for binary search
    low = 0
    high = n - 1

    while (low <= high):
        mid = (low + high) // 2

        # Check if current citations is
        # possible
        if (citations[mid] >= (mid + 1)):

            # Check to the right of mid
            low = mid + 1

            # Update h-index
            hindex = mid + 1

        else:

            # Since current value is not
            # possible, check to the left
            # of mid
            high = mid - 1

    # Print the h-index
    print(hindex)

    return hindex

# Driver Code

# citations
n = 5
citations = [ 5, 3, 3, 2, 2 ]

# Function Call
hIndex(citations, n)

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

// Function to find the H-index
static int hIndex(int[] citations, int n)
{
    int hindex = 0;

    // Set the range for binary search
    int low = 0, high = n - 1;

    while (low <= high)
    {
        int mid = (low + high) / 2;

        // Check if current citations is
        // possible
        if (citations[mid] >= (mid + 1))
        {

            // Check to the right of mid
            low = mid + 1;

            // Update h-index
            hindex = mid + 1;
        }
        else
        {

            // Since current value is not
            // possible, check to the left
            // of mid
            high = mid - 1;
        }
    }

    // Print the h-index
    Console.WriteLine(hindex);

    return hindex;
}

// Driver Code
public static void Main ()
{

    // citations
    int n = 5;
    int[] citations = { 5, 3, 3, 2, 2 };

    hIndex(citations, n);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

 // Function to find the H-index
function hIndex(citations, n)
{
    let hindex = 0;

    // Set the range for binary search
    let low = 0, high = n - 1;

    while (low <= high)
    {
        let mid = (low + high) / 2;

        // Check if current citations is
        // possible
        if (citations[mid] >= (mid + 1))
        {

            // Check to the right of mid
            low = mid + 1;

            // Update h-index
            hindex = mid + 1;
        }
        else
        {

            // Since current value is not
            // possible, check to the left
            // of mid
            high = mid - 1;
        }
    }

    // Prlet the h-index
    document.write(hindex);

    return hindex;
}

// Driver code

    // citations
    let n = 5;
    let citations = [ 5, 3, 3, 2, 2 ];

    hIndex(citations, n)

// This code is contributed by target_2.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(logN)*
***辅助空间:** O(1)*