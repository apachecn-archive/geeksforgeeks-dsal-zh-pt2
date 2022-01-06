# 将数组分成两个不包含任何和 K 对的数组

> 原文:[https://www . geeksforgeeks . org/将数组分成两个数组，其中不包含任何带 sum-k 的对/](https://www.geeksforgeeks.org/divide-array-into-two-arrays-which-does-not-contain-any-pair-with-sum-k/)

给定一个由 **N** 个非负不同整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是将该数组分布在两个数组中，使得两个数组都不包含一对和 **K** 。

**示例:**

> **输入:** arr[] = {1，0，2，3，4，7，8，9}，K = 4
> **输出:**
> 3，2，4，7，8，9
> 0，1
> **说明:给定数组中的**对(1，3)和(0，4)不能放在同一个数组中。因此，0，1 可以放在一个数组中，3，4 可以放在另一个数组中。剩余的数组元素可以放在两个数组中的任何一个中。
> 
> **输入:** arr[] = {0，1，2，4，5，6，7，8，9}，K = 7
> **输出:**
> 0，1，2，4
> 5，6，7，9，8

**方式:**思路是[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，将大于 **K / 2** 的数组元素放在一个数组中，其余元素放在另一个数组中。按照以下步骤解决问题:

*   初始化两个独立的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **第一个**和**第二个**来存储两个分布式数组。
*   由于所有的数组元素都是不同的，大于 **K/2** 的元素可以存储在一个数组中，剩余的元素可以存储在另一个数组中。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，检查**arr【I】**是否大于 **K/2** 。如果发现是真的，将该元素插入向量**第二个**。否则先插入向量**。**
*   **完成数组遍历后，打印两个向量中的元素。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split the given
// array into two separate arrays
// satisfying given condition
void splitArray(int a[], int n,
                int k)
{
    // Stores resultant arrays
    vector<int> first, second;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If a[i] is smaller than
        // or equal to k/2
        if (a[i] <= k / 2)
            first.push_back(a[i]);
        else
            second.push_back(a[i]);
    }

    // Print first array
    for (int i = 0; i < first.size();
         i++) {
        cout << first[i] << " ";
    }

    // Print second array
    cout << "\n";
    for (int i = 0; i < second.size();
         i++) {
        cout << second[i] << " ";
    }
}

// Driver Code
int main()
{

    // Given K
    int k = 5;

    // Given array
    int a[] = { 0, 1, 3, 2, 4, 5,
                6, 7, 8, 9, 10 };

    // Given size
    int n = sizeof(a)
            / sizeof(int);

    splitArray(a, n, k);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to split the given
// array into two separate arrays
// satisfying given condition
static void splitArray(int a[], int n,
                       int k)
{

    // Stores resultant arrays
    Vector<Integer> first = new Vector<>();
    Vector<Integer> second = new Vector<>();

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If a[i] is smaller than
        // or equal to k/2
        if (a[i] <= k / 2)
            first.add(a[i]);
        else
            second.add(a[i]);
    }

    // Print first array
    for(int i = 0; i < first.size(); i++)
    {
        System.out.print(first.get(i) + " ");
    }

    // Print second array
    System.out.println();
    for(int i = 0; i < second.size(); i++)
    {
        System.out.print(second.get(i) + " ");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given K
    int k = 5;

    // Given array
    int a[] = { 0, 1, 3, 2, 4, 5,
                6, 7, 8, 9, 10 };

    int n = a.length;

    splitArray(a, n, k);
}
}

// This code is contributed by code_hunt
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to split the given
# array into two separate arrays
# satisfying given condition
def splitArray(a, n, k):

    # Stores resultant arrays
    first = []
    second = []

    # Traverse the array
    for i in range(n):

        # If a[i] is smaller than
        # or equal to k/2
        if (a[i] <= k // 2):
            first.append(a[i])
        else:
            second.append(a[i])

    # Print first array
    for i in range(len(first)):
        print(first[i], end = " ")

    # Print second array
    print("\n", end = "")
    for i in range(len(second)):
        print(second[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given K
    k = 5

    # Given array
    a =  [ 0, 1, 3, 2, 4, 5,
           6, 7, 8, 9, 10 ]

    n =  len(a)

    splitArray(a, n, k)

# This code is contributed by bgangwar59
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to split the given
// array into two separate arrays
// satisfying given condition
static void splitArray(int[] a, int n,
                       int k)
{

    // Stores resultant arrays
    List<int> first = new List<int>();
    List<int> second = new List<int>();

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If a[i] is smaller than
        // or equal to k/2
        if (a[i] <= k / 2)
            first.Add(a[i]);
        else
            second.Add(a[i]);
    }

    // Print first array
    for(int i = 0; i < first.Count; i++)
    {
        Console.Write(first[i] + " ");
    }

    // Print second array
    Console.WriteLine();
    for(int i = 0; i < second.Count; i++)
    {
        Console.Write(second[i] + " ");
    }
}

// Driver Code
public static void Main()
{

    // Given K
    int k = 5;

    // Given array
    int[] a = { 0, 1, 3, 2, 4, 5,
                6, 7, 8, 9, 10 };

    int n = a.Length;

    splitArray(a, n, k);
}
}

// This code is contributed by susmitakundugoaldanga
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to split the given
// array into two separate arrays
// satisfying given condition
function splitArray(a, n, k)
{

    // Stores resultant arrays
    let first = [];
    let second = [];

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // If a[i] is smaller than
        // or equal to k/2
        if (a[i] <= parseInt(k / 2))
            first.push(a[i]);
        else
            second.push(a[i]);
    }

    // Print first array
    for (let i = 0; i < first.length;
         i++) {
        document.write(first[i] + " ");
    }

    // Print second array
    document.write("<br>");
    for (let i = 0; i < second.length;
         i++) {
        document.write(second[i] + " ");
    }
}

// Driver Code

// Given K
let k = 5;

// Given array
let a = [ 0, 1, 3, 2, 4, 5,
    6, 7, 8, 9, 10 ];

// Given size
let n = a.length;
splitArray(a, n, k);

    // This code is contributed by rishavmahato348.
</script>
```

****Output:** 

```
0 1 2 
3 4 5 6 7 8 9 10
```** 

*****时间复杂度:** O(N)，其中 **N** 是给定数组的大小。*
***辅助空间:** O(N)***