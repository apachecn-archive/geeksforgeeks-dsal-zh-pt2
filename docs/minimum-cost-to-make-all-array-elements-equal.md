# 使所有数组元素相等的最小成本

> 原文:[https://www . geesforgeks . org/最小成本-使所有数组元素相等/](https://www.geeksforgeeks.org/minimum-cost-to-make-all-array-elements-equal/)

给定一个由 **N** 个正整数组成的数组 **arr[]** ，任务是在执行任何次数(可能为零)的运算后，使该数组的所有值等于某个最小成本的整数值。

1.  将数组元素减少 2 或增加 2，成本为零。
2.  用单位成本将数组元素减少 1 或增加 1。

**例:**

> **输入:** arr[] = {2，4，3，1，5}
> **输出:** 2
> 我们可以将第三个元素更改为 5，产生 0 成本。
> 我们可以将第 4 个元素更改为 5 ( 1 - > 3 - > 5)，产生 0 成本。
> 现在数组是，2 4 5 5 5
> 我们可以将第一个元素改为 5 (2 - > 4 - > 5)，产生单位成本。
> 我们可以将第二个元素改为 5，产生单位成本。
> 最终数组为，5 5 5 5 5
> 总成本= 1 + 1 = 2
> **输入:** arr[] = {2，2，2，3}
> **输出:** 1
> 我们只能将最后一个元素减少 1，从而产生单位成本。

**方法:**基本思路是统计数组中出现的偶数元素和奇数元素的个数，打印出这两者的最小值作为答案。这种方法是可行的，因为我们可以使所有偶数元素相等，所有奇数元素相等，而不会产生任何成本(操作 1)。执行这些操作后更新的数组将只包含元素 x 和 x + 1，其中一个是奇数，另一个是偶数。这两种类型的元素可以转换成单位成本为 1 的另一种类型，为了使成本最小化，结果将是最小值(频率(x)，频率(x + 1))。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cost
// to make each array element equal
int minCost(int arr[], int n)
{
    // To store the count of even numbers
    // present in the array
    int count_even = 0;

    // To store the count of odd numbers
    // present in the array
    int count_odd = 0;

    // Iterate through the array and
    // find the count of even numbers
    // and odd numbers
    for (int i = 0; i < n; i++) {
        if (arr[i] % 2 == 0)
            count_even++;
        else
            count_odd++;
    }

    return min(count_even, count_odd);
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 3, 1, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minCost(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum cost
// to make each array element equal
static int minCost(int arr[], int n)
{
    // To store the count of even numbers
    // present in the array
    int count_even = 0;

    // To store the count of odd numbers
    // present in the array
    int count_odd = 0;

    // Iterate through the array and
    // find the count of even numbers
    // and odd numbers
    for (int i = 0; i < n; i++)
    {
        if (arr[i] % 2 == 0)
            count_even++;
        else
            count_odd++;
    }

    return Math.min(count_even, count_odd);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 4, 3, 1, 5 };
    int n = arr.length;

    System.out.println(minCost(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum cost
# to make each array element equal
def minCost(arr, n):

    # To store the count of even numbers
    # present in the array
    count_even = 0

    # To store the count of odd numbers
    # present in the array
    count_odd = 0

    # Iterate through the array and
    # find the count of even numbers
    # and odd numbers
    for i in range(n):
        if (arr[i] % 2 == 0):
            count_even += 1
        else:
            count_odd += 1

    return min(count_even, count_odd)

# Driver code
arr = [2, 4, 3, 1, 5]
n = len(arr)

print(minCost(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum cost
// to make each array element equal
static int minCost(int []arr, int n)
{
    // To store the count of even numbers
    // present in the array
    int count_even = 0;

    // To store the count of odd numbers
    // present in the array
    int count_odd = 0;

    // Iterate through the array and
    // find the count of even numbers
    // and odd numbers
    for (int i = 0; i < n; i++)
    {
        if (arr[i] % 2 == 0)
            count_even++;
        else
            count_odd++;
    }

    return Math.Min(count_even, count_odd);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 2, 4, 3, 1, 5 };
    int n = arr.Length;

    Console.WriteLine(minCost(arr, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the minimum cost
    // to make each array element equal
    function minCost(arr, n)
    {

        // To store the count of even numbers
        // present in the array
        var count_even = 0;

        // To store the count of odd numbers
        // present in the array
        var count_odd = 0;

        // Iterate through the array and
        // find the count of even numbers
        // and odd numbers
        for (i = 0; i < n; i++)
        {
            if (arr[i] % 2 == 0)
                count_even++;
            else
                count_odd++;
        }
        return Math.min(count_even, count_odd);
    }

    // Driver code
        var arr = [ 2, 4, 3, 1, 5 ];
        var n = arr.length;
        document.write(minCost(arr, n));

// This code is contributed by Rajput-Ji.
</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)