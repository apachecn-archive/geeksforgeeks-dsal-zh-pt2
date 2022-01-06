# 使用给定的运算最大化数组的除法结果

> 原文:[https://www . geeksforgeeks . org/最大化使用给定运算的数组除法结果/](https://www.geeksforgeeks.org/maximize-the-division-result-of-array-using-given-operations/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是通过重复以下两个步骤来找到数组中可能剩余的最大值:

*   移除任意两个数组元素。
*   将除法的商插入数组。

***注意:**我们可以改变元素的顺序。*

**示例:**

> **输入:** arr[] = {100，1000，10，2 }
> T3】输出:200
> T6】解释:
> 
> *   从阵列中移除 100 和 10。将 10 (= 100/10)插回到数组中。
> *   从阵列中移除 10 和 2。在数组中插入 5。
> *   从阵列中移除 1000 和 5。将 200 插入阵列
> 
> 因此，最大结果是 200。
> 
> **输入:** arr[] = {2，100，1 }
> T3】输出: 50

**方法:**
为了解决上述问题，我们可以观察到，当元素按降序排序，除法运算按顺序**arr[0]/(arr[1]/arr[2]/arr[3]…..反向排序数组的 arr[n-1])** 。因此，对数组进行相应的排序，并计算适当的结果。

下面的代码是上述方法的实现:

## C++

```
// C++ implementation to maximize the
// result of division of the given
// array elements
#include <bits/stdc++.h>
using namespace std;

// Function to find the max result
float maxDivision(int arr[], int n)
{

    // Sort the array in descending order
    sort(arr, arr + n, greater<int>());

    float mxdiv = arr[1];

    // loop to divide in this order
    // arr[0] / ( arr[1] / arr[2] / ....
    // arr[n-2] / arr[n-1])
    for (int i = 2; i < n; ++i)
        mxdiv = mxdiv / arr[i];

    // return the final result
    return arr[0] / mxdiv;
}

// Driver code
int main()
{

    int arr[] = { 100, 1000, 10, 2 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxDivision(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to maximize the
// result of division of the given
// array elements
import java.util.*;

class GFG{

// Function to find the max result
static float maxDivision(Integer arr[], int n)
{

    // Sort the array in descending order
    Arrays.sort(arr, Collections.reverseOrder());

    float mxdiv = arr[1];

    // Loop to divide in this order
    // arr[0] / ( arr[1] / arr[2] / ....
    // arr[n-2] / arr[n-1])
    for(int i = 2; i < n; ++i)
       mxdiv = mxdiv / arr[i];

    // Return the final result
    return arr[0] / mxdiv;
}

// Driver code
public static void main(String[] args)
{

    Integer arr[] = { 100, 1000, 10, 2 };
    int n = arr.length;

    System.out.print((int)maxDivision(arr, n));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to maximize
# the result of division of the
# given array elements

# Function to find the max result
def maxDivision(arr, n):

    # Sort the array in descending order
    arr.sort(reverse = True)
    mxdiv = arr[1]

    # Loop to divide in this order
    # arr[0] / ( arr[1] / arr[2] / ....
    # arr[n-2] / arr[n-1])
    for i in range(2, n):
        mxdiv = mxdiv / arr[i]

    # Return the final result
    return arr[0] / mxdiv

# Driver code
arr = [ 100, 1000, 10, 2 ]
n = len(arr)

print(maxDivision(arr, n))

# This code is contributed by ishayadav181
```

## C#

```
// C# implementation to maximize the
// result of division of the given
// array elements
using System;

class GFG{

// Function to find the max result
static float maxDivision(int []arr, int n)
{

    // Sort the array in descending order
    Array.Sort(arr);
    Array.Reverse(arr);

    float mxdiv = arr[1];

    // Loop to divide in this order
    // arr[0] / ( arr[1] / arr[2] / ....
    // arr[n-2] / arr[n-1])
    for(int i = 2; i < n; ++i)
       mxdiv = mxdiv / arr[i];

    // Return the readonly result
    return arr[0] / mxdiv;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 100, 1000, 10, 2 };
    int n = arr.Length;

    Console.Write((int)maxDivision(arr, n));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation to maximize
// the result of division of the given
// array elements

// Function to find the max result
function maxDivision(arr, n)
{

    // Sort the array in descending order
    arr.sort((a, b) => b - a);

    let mxdiv = arr[1];

    // Loop to divide in this order
    // arr[0] / ( arr[1] / arr[2] / ....
    // arr[n-2] / arr[n-1])
    for(let i = 2; i < n; ++i)
        mxdiv = mxdiv / arr[i];

    // Return the final result
    return arr[0] / mxdiv;
}

// Driver Code
let arr = [ 100, 1000, 10, 2 ];
let n = arr.length;

document.write(maxDivision(arr, n));

// This code is contributed by susmitakundugoaldanga

</script>
```

**Output:** 

```
200
```

**时间复杂度:**T2【O(N logN)T4】