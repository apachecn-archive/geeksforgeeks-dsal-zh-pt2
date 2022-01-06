# 最大堆中的最小元素

> 原文:[https://www . geesforgeks . org/max-heap 中的最小元素/](https://www.geeksforgeeks.org/minimum-element-in-a-max-heap/)

给定最大堆，找出堆中存在的最小元素。

**示例:**

```
Input :     100
           /    \ 
          75     50 
         /  \    / \
       55   10  2  40
Output : 2

Input :     20
           /   \ 
          4    18
Output : 4
```

**蛮力逼近** :
我们可以检查最大堆中的所有节点，得到最小元素。请注意，这种方法适用于任何二叉树，并且不使用最大堆的任何属性。它具有 O(n)的时间和空间复杂性。由于 max heap 是一个完整的二叉树，我们一般使用数组来存储它们，所以我们可以通过简单地遍历数组来检查所有的节点。如果堆是使用指针存储的，那么我们可以使用递归来检查所有的节点。

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// minimum element in a
// max heap
int findMinimumElement(int heap[], int n)
{
    int minimumElement = heap[0];

    for (int i = 1; i < n; ++i)
        minimumElement = min(minimumElement, heap[i]);

    return minimumElement;
}

// Driver code
int main()
{
    // Number of nodes
    int n = 10;
    // heap represents the following max heap:
    //         20
    //       /    \
    //      18     10
    //   /    \    /  \
    //   12     9  9   3
    //  /  \   /
    // 5    6 8
    int heap[] = { 20, 18, 10, 12, 9, 9, 3, 5, 6, 8 };

    cout << findMinimumElement(heap, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

public class Improve {

    // Function to find the
    // minimum element in a
    // max heap
    static int findMinimumElement(int heap[], int n)
    {
        int minimumElement = heap[0];

        for (int i = 1; i < n; ++i)
            minimumElement
                = Math.min(minimumElement, heap[i]);

        return minimumElement;
    }

    // Driver code
    public static void main(String args[])
    {
        // Number of nodes
        int n = 10;
        // heap represents the following max heap:
        //         20
        //       /    \
        //      18     10
        //   /    \    /  \
        //   12     9  9   3
        //  /  \   /
        // 5    6 8
        int heap[] = { 20, 18, 10, 12, 9, 9, 3, 5, 6, 8 };

        System.out.println(findMinimumElement(heap, n));
    }
    // This Code is contributed by ANKITRAI1
}
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to find the minimum
# element in a max heap

def findMiniumumElement(heap, n):

    minimumElement = heap[0]

    for i in range(1, n):
        minimumElement = min(minimumElement, heap[i])

    return minimumElement

# Driver Code
n = 10  # Numbers Of Node

# heap represents the following max heap:
#         20
#         / \
#         18 10
#     / \ / \
#     12 9 9 3
#     / \ /
#     5 6 8
#

heap = [20, 18, 10, 12, 8,
        9, 3, 5, 6, 8]

print(findMiniumumElement(heap, n))

# This code is contributed by SANKAR
```

## C#

```
// C# implementation of above approach
using System;
class GFG {

    // Function to find the
    // minimum element in a
    // max heap
    static int findMinimumElement(int[] heap, int n)
    {
        int minimumElement = heap[0];

        for (int i = 1; i < n; ++i)
            minimumElement
                = Math.Min(minimumElement, heap[i]);

        return minimumElement;
    }

    // Driver code
    public static void Main()
    {
        // Number of nodes
        int n = 10;

        // heap represents the following max heap:
        //             20
        //           /     \
    //          18     10
        //       /  \    / \
    //      12   9  9   3
        //     /  \ /
        //    5   6 8
        int[] heap = { 20, 18, 10, 12, 9, 9, 3, 5, 6, 8 };

        Console.Write(findMinimumElement(heap, n));
    }
}

// This code is contributed by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the
// minimum element in a
// max heap
function findMinimumElement(&$heap, $n)
{
    $minimumElement = $heap[0];

    for ($i = 1; $i < $n; ++$i)
        $minimumElement = min($minimumElement,
                              $heap[$i]);

    return $minimumElement;
}

// Driver code

// Number of nodes
$n = 10;

// heap represents the following
// max heap:
//         20
//       /    \
//     18     10
//    /  \   /  \
// 12   9  9   3
// / \ /
// 5 6 8
$heap = array(20, 18, 10, 12, 9,
               9, 3, 5, 6, 8 );

echo findMinimumElement($heap, $n);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

    // Javascript implementation of above approach

    // Function to find the
    // minimum element in a
    // max heap
    function findMinimumElement(heap, n)
    {
        let minimumElement = heap[0];

        for (let i = 1; i < n; ++i)
            minimumElement = Math.min(minimumElement, heap[i]);

        return minimumElement;
    }

    // Number of nodes
    let n = 10;

    // heap represents the following max heap:
    //             20
    //           /     \
    //          18     10
    //       /  \    / \
    //      12   9  9   3
    //     /  \ /
    //    5   6 8
    let heap = [ 20, 18, 10, 12, 9, 9, 3, 5, 6, 8 ];

    document.write(findMinimumElement(heap, n));

</script>
```

**Output**

```
3
```

**高效方法** :
最大堆属性要求父节点大于其子节点。因此，我们可以得出结论，非叶节点不能是最小元素，因为它的子节点具有较低的值。因此，我们可以将搜索空间缩小到只有叶节点。在具有 n 个元素的最大堆中，有 ceil(n/2)个叶节点。时间和空间复杂度保持为 0(n)，因为 1/2 的常数因子不影响渐近复杂度。

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// minimum element in a
// max heap
int findMinimumElement(int heap[], int n)
{
    int minimumElement = heap[n / 2];

    for (int i = 1 + n / 2; i < n; ++i)
        minimumElement = min(minimumElement, heap[i]);

    return minimumElement;
}

// Driver code
int main()
{
    // Number of nodes
    int n = 10;
    // heap represents the following max heap:
    //        20
    //       /    \
    //     18     10
    //   /    \    /  \
    //   12     9  9   3
    //  /  \   /
    // 5    6 8
    int heap[] = { 20, 18, 10, 12, 9, 9, 3, 5, 6, 8 };

    cout << findMinimumElement(heap, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;
import java.lang.*;

class GFG {

    // Function to find the
    // minimum element in a
    // max heap
    static int findMinimumElement(int heap[], int n)
    {
        int minimumElement = heap[n / 2];

        for (int i = 1 + n / 2; i < n; ++i)
            minimumElement
                = Math.min(minimumElement, heap[i]);

        return minimumElement;
    }

    // Driver code
    public static void main(String args[])
    {
        // Number of nodes
        int n = 10;
        // heap represents the following max heap:
        //     20
        //     / \
        //     18     10
        // / \ / \
        // 12     9 9 3
        // / \ /
        // 5 6 8
        int heap[] = new int[] { 20, 18, 10, 12, 9,
                                 9,  3,  5,  6,  8 };

        System.out.println(findMinimumElement(heap, n));
    }
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 蟒蛇 3

```
# Python 3 implementation of
# above approach

# Function to find the minimum
# element in a max heap

def findMiniumumElement(heap, n):

    # // -->Floor Division Arithmetic Operator
    minimumElement = heap[n // 2]

    for i in range(1 + n // 2, n):
        minimumElement = min(minimumElement,
                             heap[i])

    return minimumElement

# Driver Code
n = 10  # Numbers Of Node

# heap represents the
# following max heap:
# 20
# / \
# 18 10
# / \ / \
# 12 9 9 3
# / \ \
# 5 6 8
#

heap = [20, 18, 10, 12, 9,
        9, 3, 5, 6, 8]

print(findMiniumumElement(heap, n))

# This code is contributed by SANKAR
```

## C#

```
// C# implementation of above approach
using System;

class GFG {

    // Function to find the minimum element
    // in a max heap
    static int findMinimumElement(int[] heap, int n)
    {
        int minimumElement = heap[n / 2];

        for (int i = 1 + n / 2; i < n; ++i)
            minimumElement
                = Math.Min(minimumElement, heap[i]);

        return minimumElement;
    }

    // Driver code
    static public void Main()
    {

        // Number of nodes
        int n = 10;

        // heap represents the following
        // max heap:
        // 20
        // / \
    // 18 10
        // / \ / \
    // 12 9 9 3
        // / \ /
        // 5 6 8
        int[] heap = new int[] { 20, 18, 10, 12, 9,
                                 9,  3,  5,  6,  8 };

        Console.WriteLine(findMinimumElement(heap, n));
    }
}

// This code is contributed
// by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Function to find the
// minimum element in a
// max heap
function findMinimumElement($heap, $n)
{
    $minimumElement = $heap[$n/2];

    for ($i = 1 + $n / 2; $i < $n; ++$i)
        $minimumElement = min($minimumElement, $heap[$i]);

    return $minimumElement;
}

    // Driver code
    // Number of nodes
    $n = 10;
    // heap represents the following max heap:
    //     20
    //     / \
    //     18     10
    // / \ / \
    // 12     9 9 3
    // / \ /
    // 5 6 8
    $heap = Array(20, 18, 10, 12, 9, 9, 3, 5, 6, 8 );

    echo(findMinimumElement($heap, $n));

//  This code is contributed to Rajput-Ji
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Function to find the minimum element
    // in a max heap
    function findMinimumElement(heap, n)
    {
        let minimumElement = heap[parseInt(n / 2, 10)];

        for (let i = 1 + parseInt(n / 2, 10); i < n; ++i)
            minimumElement
                = Math.min(minimumElement, heap[i]);

        return minimumElement;
    }

    // Number of nodes
    let n = 10;

    // heap represents the following
    // max heap:
    // 20
    // / \
    // 18 10
    // / \ / \
    // 12 9 9 3
    // / \ /
    // 5 6 8
    let heap = [ 20, 18, 10, 12, 9, 9,  3,  5,  6,  8 ];

    document.write(findMinimumElement(heap, n));

</script>
```

**Output:** 

```
3
```