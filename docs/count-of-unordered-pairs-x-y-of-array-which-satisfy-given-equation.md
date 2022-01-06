# 满足给定等式的数组的无序对(x，y)的计数

> 原文:[https://www . geesforgeks . org/无序对计数-满足给定等式的数组的 x-y/](https://www.geeksforgeeks.org/count-of-unordered-pairs-x-y-of-array-which-satisfy-given-equation/)

给定一个正负整数的**数组 arr[]****N**，我们的任务是找出满足给定等式的无序对(x，y)的数量:

*   **| x |>= min(| x–y |，| x + y|)**
*   **| y |<= max(| x–y |，| x + y|)**

**示例:**

> **输入:**arr[]=【2，5，-3】
> **输出:** 2
> **解释:**
> 可能的无序对是(5，-3)和(2，-3)。(2，5)不算，因为它不满足条件。
> 
> **输入:**arr[]=【3，6】
> **输出:** 1
> **说明:**
> 对【3，6】满足条件。因此，输出为 1。

**天真方法:**
解决上述问题的天真方法是遍历所有可能的对，并计算满足这些条件的无序对的数量。但是这种方法成本高，耗时长，可以进一步优化。

***时间复杂度:**O(N<sup>2</sup>)*
*T8】辅助空间 : O(1)*

**高效方法:**
优化上述方法的主要思路是**对数组**进行排序，然后应用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找出数组中每个索引的正确边界。我们必须观察到，如果我们将 **x 更改为–x**，则|x|和|y|的值保持不变，而| x–y |和|x + y|将交换值。这意味着当且仅当{-x，y}起作用时，对{x，y}起作用。同样，我们可以切换 y 的符号，这意味着我们可以**用 x 和 y 的绝对值**替换 x 和 y，当且仅当新的对起作用时，原来的对才起作用。

> 如果 x > = 0，y > = 0，则条件变为**| x–y |<= x，y < = x + y** 。上限始终成立，而下限相当于 x < = 2 * y 和 y < = 2 * x

所以问题简化为**用|x| < = 2|y|和|y| < = 2|x|** 计算对{x，y}的数量。为了解决这个问题，我们取所有 A[i]的绝对值，用 l < r 和 a[r] < = 2 * a[l]对数组进行排序。对于每个固定的 l，我们计算满足这个条件的最大 r，然后把它和答案相加。

下面是上述方法的实现:

## C++

```
// C++ Program to find the number of
// unordered pairs (x, y) which satisfy
// the given equation for the array

#include <bits/stdc++.h>
using namespace std;

// Return the number of unordered
// pairs satisfying the conditions
int numPairs(int a[], int n)

{
    int ans, i, index;

    // ans stores the number
    // of unordered pairs
    ans = 0;

    // Making each value of
    // array to positive
    for (i = 0; i < n; i++)
        a[i] = abs(a[i]);

    // Sort the array
    sort(a, a + n);

    // For each index calculating
    // the right boundary for
    // the unordered pairs
    for (i = 0; i < n; i++) {

        index = upper_bound(
                    a,
                    a + n,
                    2 * a[i])
                - a;
        ans += index - i - 1;
    }

    // Return the final result
    return ans;
}

// Driver code
int main()
{
    int a[] = { 3, 6 };
    int n = sizeof(a)
            / sizeof(a[0]);

    cout << numPairs(a, n)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the number of
// unordered pairs (x, y) which satisfy
// the given equation for the array
import java.util.Arrays;
class GFG{

// Return the number of unordered
// pairs satisfying the conditions
static int numPairs(int a[], int n)
{
    int ans, i, index;

    // ans stores the number
    // of unordered pairs
    ans = 0;

    // Making each value of
    // array to positive
    for (i = 0; i < n; i++)
        a[i] = Math.abs(a[i]);

    // Sort the array
    Arrays.sort(a);

    // For each index calculating
    // the right boundary for
    // the unordered pairs
    for (i = 0; i < n; i++)
    {
        index = 2;
        ans += index - i - 1;
    }

    // Return the final result
    return ans;
}

// Driver code
public static void main(String []args)
{
    int a[] = new int[]{ 3, 6 };
    int n = a.length;

    System.out.println(numPairs(a, n));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to find the number of
# unordered pairs (x, y) which satisfy
# the given equation for the array

# Return the number of unordered
# pairs satisfying the conditions
def numPairs(a, n):

    # ans stores the number
    # of unordered pairs
    ans = 0

    # Making each value of array
    # to positive
    for i in range(n):
        a[i] = abs(a[i])

    # Sort the array
    a.sort()

    # For each index calculating
    # the right boundary for
    # the unordered pairs
    for i in range(n):
        index = 0

        for j in range(i + 1, n):
            if (2 * a[i] >= a[j - 1] and
                2 * a[i] < a[j]):
                index = j

        if index == 0:
            index = n

        ans += index - i - 1

    # Return the final result
    return ans

# Driver code
a = [ 3, 6 ]
n = len(a)

print(numPairs(a, n))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# Program to find the number of
// unordered pairs (x, y) which satisfy
// the given equation for the array
using System;
class GFG{

// Return the number of unordered
// pairs satisfying the conditions
static int numPairs(int []a, int n)
{
    int ans, i, index;

    // ans stores the number
    // of unordered pairs
    ans = 0;

    // Making each value of
    // array to positive
    for (i = 0; i < n; i++)
        a[i] = Math.Abs(a[i]);

    // Sort the array
    Array.Sort(a);

    // For each index calculating
    // the right boundary for
    // the unordered pairs
    for (i = 0; i < n; i++)
    {
        index = 2;
        ans += index - i - 1;
    }

    // Return the final result
    return ans;
}

// Driver code
public static void Main()
{
    int []a = new int[]{ 3, 6 };
    int n = a.Length;

    Console.Write(numPairs(a, n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
    // Javascript Program to find the number of
    // unordered pairs (x, y) which satisfy
    // the given equation for the array

    // Return the number of unordered
    // pairs satisfying the conditions
    function numPairs(a, n)
    {
        let ans, i, index;

        // ans stores the number
        // of unordered pairs
        ans = 0;

        // Making each value of
        // array to positive
        for (i = 0; i < n; i++)
            a[i] = Math.abs(a[i]);

        // Sort the array
        a.sort();

        // For each index calculating
        // the right boundary for
        // the unordered pairs
        for (i = 0; i < n; i++)
        {
            index = 2;
            ans += index - i - 1;
        }

        // Return the final result
        return ans;
    }

    let a = [ 3, 6 ];
    let n = a.length;

    document.write(numPairs(a, n));

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(n * log n)*
***辅助空间:** O(1)*