# 计算大于数组右侧任意元素的元素数量

> 原文:[https://www . geesforgeks . org/count-数组右侧大于任意元素的元素数/](https://www.geeksforgeeks.org/count-the-number-of-elements-which-are-greater-than-any-of-element-on-right-side-of-an-array/)

给定一个数组 **Arr[]** 。任务是计算给定数组中元素 **Arr[i]** 的数量，使得一个或多个较小的元素出现在数组中元素 **Arr[i]** 的右侧。

**示例:**

> **输入:** Arr[] = { 3，9，4，6，7，5 }
> **输出:** 3
> 计数的数字为:9，6，7
> **9**–由于 9 之后出现的所有数字都小于 9，
> **6**–5 之后出现的元素较小，
> **7**–5 之后出现的元素较小。
> 
> **输入:** Arr[] = { 3，2，1，2，3，4，5 }
> T3】输出: 2

**方法:**
从数组的最后一个元素到第一个元素开始遍历数组。遍历时，保持一个 **min** 变量和一个计数器变量，该变量存储到目前为止的最小元素。将最小变量与当前元素进行比较。如果 **min** 变量小于电流元件 **Arr[i]** ，则增加计数器，如果 **min** 大于 **Arr[i]** ，则更新 **min** 。

下面是上述方法的实现:

## C++

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

// function to return the count
int count_greater(int arr[], int n)
{
    int min = INT_MAX;
    int counter = 0;

    // Comparing the given element
    // with minimum element till
    // occurred till now.
    for (int i = n - 1; i >= 0; i--) {
        if (arr[i] > min) {
            counter++;
        }

        // Updating the min variable
        if (arr[i] <= min) {
            min = arr[i];
        }
    }

    return counter;
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(int);

    cout << count_greater(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// function to return the count
static int count_greater(int arr[], int n)
{
    int min = Integer.MAX_VALUE;
    int counter = 0;

    // Comparing the given element
    // with minimum element till
    // occurred till now.
    for (int i = n - 1; i >= 0; i--)
    {
        if (arr[i] > min)
        {
            counter++;
        }

        // Updating the min variable
        if (arr[i] <= min)
        {
            min = arr[i];
        }
    }
    return counter;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 1, 2, 3, 4, 5 };
    int n = arr.length;

    System.out.println(count_greater(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation for the above approach
import sys

# function to return the count
def count_greater(arr, n) :

    min = sys.maxsize;
    counter = 0;

    # Comparing the given element
    # with minimum element till
    # occurred till now.
    for i in range(n - 1, -1, -1) :
        if (arr[i] > min) :
            counter += 1;

        # Updating the min variable
        if (arr[i] <= min) :
            min = arr[i];

    return counter;

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 2, 1, 2, 3, 4, 5 ];
    n = len(arr);

    print(count_greater(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// function to return the count
static int count_greater(int []arr, int n)
{
    int min = int.MaxValue;
    int counter = 0;

    // Comparing the given element
    // with minimum element till
    // occurred till now.
    for (int i = n - 1; i >= 0; i--)
    {
        if (arr[i] > min)
        {
            counter++;
        }

        // Updating the min variable
        if (arr[i] <= min)
        {
            min = arr[i];
        }
    }
    return counter;
}

// Driver code
static public void Main ()
{
    int []arr = { 3, 2, 1, 2, 3, 4, 5 };
    int n = arr.Length;

    Console.Write(count_greater(arr, n));
}
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>

// Javascript implementation

// Function to return the count
function count_greater(arr, n)
{
    let min = Number.MAX_VALUE;
    let counter = 0;

    // Comparing the given element
    // with minimum element till
    // occurred till now.
    for(let i = n - 1; i >= 0; i--)
    {
        if (arr[i] > min)
        {
            counter++;
        }

        // Updating the min variable
        if (arr[i] <= min)
        {
            min = arr[i];
        }
    }
    return counter;
}

// Driver code
let arr = [ 3, 2, 1, 2, 3, 4, 5 ];
let n = arr.length;

document.write(count_greater(arr, n) + "<br>");

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)