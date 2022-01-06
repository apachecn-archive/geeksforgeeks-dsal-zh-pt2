# 二进制数组中不同的相邻元素

> 原文:[https://www . geeksforgeeks . org/distinct-二进制数组中的相邻元素/](https://www.geeksforgeeks.org/distinct-adjacent-elements-in-a-binary-array/)

给定一个长度为 1 和 0 的二进制数组**arr[]****N**。任务是找出相对于其邻居而言不同的元素数量。
**注:**至少要有一个邻居是截然不同的。
**示例:**

> **输入:** N = 4，arr=[1，0，1，1]
> **输出:** 3
> arr[0]=1 不同，因为它的邻居 arr[1]=0 不同。
> arr[1]=0 也是不同的，因为它有两个不同的邻居，即 arr[2]=1 & arr[0]=1。
> arr[2]=1 在 arr[3]=1 中具有相同邻居，但在 arr[1]=0 中具有不同邻居。所以很明显。
> 但是 arr[3]=1 并不明显，因为它的邻居 arr[2]=1 是相同的。
> 因此不同元素的总数为 1+1+1+0=3
> **输入:** N = 2，arr=[1，1]
> **输出:** 0

**进场:**

*   对列表中的所有元素运行一个循环，并将每个元素与其前一个和下一个邻居进行比较。如果元素不同，将计数增加 1。
*   第一个元素只能与其下一个邻居进行比较，同样，最后一个元素只能与其前一个元素进行比较。
*   其余元素有两个邻居。如果两个邻居中的任何一个不同，那么它就被认为是不同的。

以下是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>

using namespace std;

int distinct(int arr[], int n)
{
    int count = 0;

    // if array has only one element, return 1
    if (n == 1)
        return 1;

    for ( int i = 0; i < n - 1; i++)
    {

        // For first element compare
        // with only next element
        if(i == 0)
        {
            if(arr[i] != arr[i + 1])
                count += 1;
        }

        // For remaining elements compare with
        // both prev and next elements
        else
        {
            if(arr[i] != arr[i + 1] ||
               arr[i] != arr[i - 1])
                count += 1;
        }
    }

    // For last element compare
    // with only prev element
    if(arr[n - 1] != arr[n - 2])
        count += 1;

    return count;
}

// Driver code
int main()
{
    int arr[] = {0, 0, 0, 0, 0, 1, 0};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << distinct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
class GFG
{
static int distinct(int []arr, int n)
{
    int count = 0;

    // if array has only one element,
    // return 1
    if (n == 1)
        return 1;

    for (int i = 0; i < n - 1; i++)
    {

        // For first element compare
        // with only next element
        if(i == 0)
        {
            if(arr[i] != arr[i + 1])
                count += 1;
        }

        // For remaining elements compare with
        // both prev and next elements
        else
        {
            if(arr[i] != arr[i + 1] ||
               arr[i] != arr[i - 1])
                count += 1;
        }
    }

    // For last element compare
    // with only prev element
    if(arr[n - 1] != arr[n - 2])
        count += 1;

    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {0, 0, 0, 0, 0, 1, 0};
    int n = arr.length;
    System.out.println(distinct(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
def distinct(arr):
    count = 0

    # if array has only one element, return 1
    if len(arr) == 1:
        return 1

    for i in range(0, len(arr) - 1):

        # For first element compare
        # with only next element
        if(i == 0):
            if(arr[i] != arr[i + 1]):
                count += 1

        # For remaining elements compare with
        # both prev and next elements
        elif(i > 0 & i < len(arr) - 1):
            if(arr[i] != arr[i + 1] or
               arr[i] != arr[i - 1]):
                count += 1

    # For last element compare
    # with only prev element
    if(arr[len(arr) - 1] != arr[len(arr) - 2]):
        count += 1
    return count

# Driver code
arr = [0, 0, 0, 0, 0, 1, 0]

print(distinct(arr))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of
// the above approach
using System;

class GFG
{
static int distinct(int []arr, int n)
{
    int count = 0;

    // if array has only one element,
    // return 1
    if (n == 1)
        return 1;

    for (int i = 0; i < n - 1; i++)
    {

        // For first element compare
        // with only next element
        if(i == 0)
        {
            if(arr[i] != arr[i + 1])
                count += 1;
        }

        // For remaining elements compare with
        // both prev and next elements
        else
        {
            if(arr[i] != arr[i + 1] ||
               arr[i] != arr[i - 1])
                count += 1;
        }
    }

    // For last element compare
    // with only prev element
    if(arr[n - 1] != arr[n - 2])
        count += 1;

    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = {0, 0, 0, 0, 0, 1, 0};
    int n = arr.Length;
    Console.WriteLine(distinct(arr, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript implementation of
// the above approach

function distinct(arr, n)
{
    let count = 0;

    // if array has only one element, return 1
    if (n == 1)
        return 1;

    for ( let i = 0; i < n - 1; i++)
    {

        // For first element compare
        // with only next element
        if(i == 0)
        {
            if(arr[i] != arr[i + 1])
                count += 1;
        }

        // For remaining elements compare with
        // both prev and next elements
        else
        {
            if(arr[i] != arr[i + 1] ||
               arr[i] != arr[i - 1])
                count += 1;
        }
    }

    // For last element compare
    // with only prev element
    if(arr[n - 1] != arr[n - 2])
        count += 1;

    return count;
}

// Driver code
    let arr = [0, 0, 0, 0, 0, 1, 0];
    let n = arr.length;
    document.write(distinct(arr, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)