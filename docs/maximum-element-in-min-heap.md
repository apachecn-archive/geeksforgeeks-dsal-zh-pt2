# 最小堆中的最大元素

> 原文:[https://www.geeksforgeeks.org/maximum-element-in-min-heap/](https://www.geeksforgeeks.org/maximum-element-in-min-heap/)

给定一个[最小堆](https://www.geeksforgeeks.org/binary-heap/)，找到堆中存在的最大元素。
**例:**

```
Input :      10 
           /    \ 
          25     23 
         /  \    / \
       45   30  50  40
Output : 50

Input :     20
           /   \ 
          40    28
Output : 40
```

**蛮力方法:**
我们可以检查最小堆中的所有节点来获得最大元素。请注意，这种方法适用于任何二叉树，并且不使用最小堆的任何属性。它具有 O(n)的时间和空间复杂性。由于 min-heap 是一个完整的二叉树，我们通常使用数组来存储它们，所以我们可以通过简单地遍历数组来检查所有的节点。如果堆是使用指针存储的，那么我们可以使用递归来检查所有的节点。
以下是上述办法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// maximum element in a
// min heap
int findMaximumElement(int heap[], int n)
{
    int maximumElement = heap[0];

    for (int i = 1; i < n; ++i)
        maximumElement = max(maximumElement, heap[i]);

    return maximumElement;
}

// Driver code
int main()
{
    // Number of nodes
    int n = 10;

    // heap represents the following min heap:
    //     10
    //    / \
    //  25     23
    //  / \   / \
    // 45 50 30 35
    // / \ /
    // 63 65 81
    int heap[] = { 10, 25, 23, 45, 50, 30, 35, 63, 65, 81 };

    cout << findMaximumElement(heap, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG {
// Function to find the maximum element
// in a min heap

    static int findMaximumElement(int[] heap, int n) {
        int maximumElement = heap[0];

        for (int i = 1; i < n; ++i) {
            maximumElement = Math.max(maximumElement,
                    heap[i]);
        }

        return maximumElement;
    }

// Driver code
    public static void main(String[] args) {
        // Number of nodes
        int n = 10;

        // heap represents the following min heap:
        // 10
        // / \
        // 25 23
        // / \ / \
        // 45 50 30 35
        // / \ /
        //63 65 81
        int[] heap = {10, 25, 23, 45, 50,
            30, 35, 63, 65, 81};

        System.out.print(findMaximumElement(heap, n));
    }
}
// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find the maximum element
# in a min heap
def findMaximumElement(heap, n):

    maximumElement = heap[0];

    for i in range(1, n):
            maximumElement = max(maximumElement, heap[i]);

    return maximumElement;

# Driver code
if __name__ == '__main__':

    # Number of nodes
    n = 10;

    # heap represents the following min heap:
    # 10
    # / \
    # 25     23
    # / \ / \
    # 45 50 30 35
    # / \ /
    #63 65 81
    heap = [ 10, 25, 23, 45, 50,
             30, 35, 63, 65, 81 ];

    print(findMaximumElement(heap, n));

# This code is contributed by Princi Singh
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
// Function to find the maximum element
// in a min heap
static int findMaximumElement(int[] heap, int n)
{
    int maximumElement = heap[0];

    for (int i = 1; i < n; ++i)
        maximumElement = Math.Max(maximumElement,
                                        heap[i]);

    return maximumElement;
}

// Driver code
public static void Main()
{
    // Number of nodes
    int n = 10;

    // heap represents the following min heap:
    // 10
    // / \
    // 25 23
    // / \ / \
    // 45 50 30 35
    // / \ /
    //63 65 81
    int[] heap = { 10, 25, 23, 45, 50,
                   30, 35, 63, 65, 81 };

    Console.Write(findMaximumElement(heap, n));
}
}

// This code is contributed by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to find the maximum element
// in a min heap

    function findMaximumElement(heap , n) {
        var maximumElement = heap[0];

        for (i = 1; i < n; ++i) {
            maximumElement = Math.max(maximumElement,
                    heap[i]);
        }

        return maximumElement;
    }

// Driver code

        // Number of nodes
        var n = 10;

        // heap represents the following min heap:
        // 10
        // / \
        // 25 23
        // / \ / \
        // 45 50 30 35
        // / \ /
        //63 65 81
        var heap = [10, 25, 23, 45, 50,
            30, 35, 63, 65, 81];

        document.write(findMaximumElement(heap, n));

// This code contributed by aashish1995

</script>
```

**输出:**

```
81
```

**有效方法:**
最小堆属性要求父节点小于其子节点。因此，我们可以得出结论，非叶节点不能是最大元素，因为它的子节点具有更高的值。因此，我们可以将搜索空间缩小到只有叶节点。在具有 n 个元素的最小堆中，存在 ceil(n/2)个叶节点。时间和空间复杂度保持为 0(n)，因为 1/2 的常数因子不影响渐近复杂度。
以下是上述办法的实施:

## C++14

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// maximumelement in a
// max heap
int findMaximumElement(int heap[], int n)
{
    int maximumElement = heap[n / 2];

    for (int i = 1 + n / 2; i < n; ++i)
        maximumElement = max(maximumElement, heap[i]);

    return maximumElement;
}

// Driver code
int main()
{
    // Number of nodes
    int n = 10;

    // heap represents the following min heap:
    //     10
    //    / \
    //  25     23
    //  / \   / \
    // 45 50 30 35
    // / \ /
    //63 65 81
    int heap[] = { 10, 25, 23, 45, 50, 30, 35, 63, 65, 81 };

    cout << findMaximumElement(heap, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{

// Function to find the
// maximumelement in a
// max heap
static int findMaximumElement(int heap[], int n)
{
    int maximumElement = heap[n / 2];

    for (int i = 1 + n / 2; i < n; ++i)
        maximumElement = Math.max(maximumElement, heap[i]);

    return maximumElement;
}

// Driver code
public static void main(String args[])
{
    // Number of nodes
    int n = 10;

    // heap represents the following min heap:
    //     10
    //    / \
    //  25     23
    //  / \   / \
    // 45 50 30 35
    // / \ /
    //63 65 81
    int heap[] = { 10, 25, 23, 45, 50, 30, 35, 63, 65, 81 };

    System.out.println(findMaximumElement(heap, n));

}
}
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

# Function to find the maximum
# element in a max heap
def findMaximumElement(heap, n):

    maximumElement = heap[n // 2]

    for i in range(1 + n // 2, n):
        maximumElement = max(maximumElement,
                             heap[i])
    return maximumElement

# Driver Code
n = 10 # Numbers Of Node

# heap represents the following min heap:
#            10
#          /    \
#       25        23
#     /    \     /  \
#   45      50  30   35
#  /  \    /
# 63  65  81

heap = [10, 25, 23, 45, 50,
        30, 35, 63, 65, 81]
print(findMaximumElement(heap, n))

# This code is contributed by Yogesh Joshi
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to find the
// maximumelement in a
// max heap
static int findMaximumElement(int[] heap,
                              int n)
{
    int maximumElement = heap[n / 2];

    for (int i = 1 + n / 2; i < n; ++i)
        maximumElement = Math.Max(maximumElement,
                                        heap[i]);

    return maximumElement;
}

// Driver code
public static void Main()
{
    // Number of nodes
    int n = 10;

    // heap represents the following min heap:
    // 10
    // / \
    // 25 23
    // / \ / \
    // 45 50 30 35
    // / \ /
    //63 65 81
    int[] heap = { 10, 25, 23, 45, 50,
                   30, 35, 63, 65, 81 };

    Console.WriteLine(findMaximumElement(heap, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>
// javascript implementation of above approach
    // Function to find the
    // maximumelement in a
    // max heap
    function findMaximumElement(heap , n) {
        var maximumElement = heap[n / 2];

        for (i = 1 + n / 2; i < n; ++i)
            maximumElement = Math.max(maximumElement, heap[i]);

        return maximumElement;
    }

    // Driver code

        // Number of nodes
        var n = 10;

        // heap represents the following min heap:
        // 10
        // / \
        // 25 23
        // / \ / \
        // 45 50 30 35
        // / \ /
        // 63 65 81
        var heap = [ 10, 25, 23, 45, 50, 30, 35, 63, 65, 81 ];

        document.write(findMaximumElement(heap, n));

// This code contributed by aashish1995
</script>
```

**输出:**

```
81 
```