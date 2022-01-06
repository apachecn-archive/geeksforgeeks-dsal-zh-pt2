# 使所有数组元素相等所需的每对元素的最小增量和减量 K

> 原文:[https://www . geeksforgeeks . org/每对元素的最小增量和减量乘以 k-要求使所有数组元素相等/](https://www.geeksforgeeks.org/minimum-increment-and-decrement-by-k-of-each-pair-elements-required-to-make-all-array-elements-equal/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过反复选择三元组( **i** 、 **j** 、 **k** )来检查是否有可能使所有**数组**元素相等，其中 **i** 和 **j** 不同，从**arr【I】**中减去 **k** 并加上 **k**

**示例:**

> **输入:** arr[] = {1，5，6，4}
> **输出:**是
> **解释:**
> 执行的操作:
> 选择 **i = 2，j = 0，k = 2** 并执行给定的操作。数组 **arr[]** 修改为 **{3，5，4，4}** 。
> 选择 **i = 1，j = 0，k = 1** 并执行给定的操作。数组 **arr[]** 修改为 **{4，4，4，4}** 。
> 现在，所有数组元素都是**等于**。因此，打印**是**。
> 
> **输入:** arr[] = {2，5，3，2，2}
> **输出:**否

**天真法:** 最简单的方法是基于这样的观察:修改后数组的**和**将等于初始数组的和。按照以下步骤解决此问题:

*   考虑 **Y** 为所有数组元素相等后所有数组元素的值。因此， **Y * N** ( *其中 **N** 为数组大小*)必须等于给定数组的[之和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   迭代到数组中的 ma [最大值，并检查 **Y** 的可能值。如果发现满足给定条件，打印“**是”**。否则，打印“**否”**。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

**证明:**

> *   Select some **I** **J** and **K** at any one step.
> *   Assume that the sum of array elements is equal to the sum of .
> *   The sum of array elements excluding **arr [I]** and **arr [j]** is **sum–arr [I]–arr [j]** .
> *   Now, adding **arr [I]–k** and **arr [j]+k** to the array will change the sum of the array to **sum–arr [I]–arr [j]+arr [I]–k+arr [j]+.**

***时间复杂度:**O(max(arr[I])*
***辅助空间:** O(1)*

**有效方法:**最佳思路是检查给定数组的[和是否为 **N** 的](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)[因子。按照以下步骤解决问题:](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)

*   假设所有数组元素相等后，数组元素修改为 **X** ， **X** 应该是一个整数，这样数组的和可以被 **N** 整除。
*   如果和不能被 **N** 整除，那么 **X** 就不是整数，也不可能让所有数组元素相等。如果没有发现是整数，打印“**否**”。否则，打印“**是”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if its possible to
// make all array elements equal or not
void arrayElementEqual(int arr[], int N)
{
    // Stores the sum of the array
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        sum += arr[i];
    }

    // If sum is divisible by N
    if (sum % N == 0) {
        cout << "Yes";
    }

    // Otherwise, not possible to make
    // all array elements equal
    else {
        cout << "No" << endl;
    }
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 5, 6, 4 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    arrayElementEqual(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to check if its possible to
// make all array elements equal or not
static void arrayElementEqual(int arr[], int N)
{

    // Stores the sum of the array
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // If sum is divisible by N
    if (sum % N == 0)
    {
        System.out.print("Yes");
    }

    // Otherwise, not possible to make
    // all array elements equal
    else
    {
        System.out.print("No" +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given array
    int arr[] = { 1, 5, 6, 4 };

    // Size of the array
    int N = arr.length;
    arrayElementEqual(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if its possible to
# make all array elements equal or not
def arrayElementEqual(arr, N):

    # Stores the sum of the array
    sum = 0

    # Traverse the array
    for i in range(N):
        sum += arr[i]

    # If sum is divisible by N
    if (sum % N == 0):
        print('Yes')

    # Otherwise, not possible to make
    # all array elements equal
    else:
        print("No")

# Driver Code
# Given array
arr = [ 1, 5, 6, 4 ]

# Size of the array
N = len(arr)
arrayElementEqual(arr, N)

# This code is contributed by rohitsingh07052
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

// Function to check if its possible to
// make all array elements equal or not
static void arrayElementEqual(int[] arr, int N)
{

    // Stores the sum of the array
    int sum = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {
        sum += arr[i];
    }

    // If sum is divisible by N
    if (sum % N == 0)
    {
        Console.WriteLine("Yes");
    }

    // Otherwise, not possible to make
    // all array elements equal
    else
    {
        Console.Write("No" +"\n");
    }
}

// Driver Code
static public void Main()
{

    // Given array
    int[] arr = { 1, 5, 6, 4 };

    // Size of the array
    int N = arr.Length;
    arrayElementEqual(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to check if its possible to
    // make all array elements equal or not
    function arrayElementEqual(arr , N)
    {

        // Stores the sum of the array
        var sum = 0;

        // Traverse the array
        for (i = 0; i < N; i++) {
            sum += arr[i];
        }

        // If sum is divisible by N
        if (sum % N == 0) {
            document.write("Yes");
        }

        // Otherwise, not possible to make
        // all array elements equal
        else {
            document.write("No" + "\n");
        }
    }

    // Driver Code

        // Given array
        var arr = [ 1, 5, 6, 4 ];

        // Size of the array
        var N = arr.length;
        arrayElementEqual(arr, N);

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)