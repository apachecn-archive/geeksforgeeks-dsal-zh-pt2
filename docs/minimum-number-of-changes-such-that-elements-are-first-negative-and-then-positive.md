# 元素先负后正的最小变化次数

> 原文:[https://www . geesforgeks . org/最小变化数-这样-元素先负后正/](https://www.geeksforgeeks.org/minimum-number-of-changes-such-that-elements-are-first-negative-and-then-positive/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是找到转换数组所需的最小更改次数，以便对于任何索引 **0 ≤ k < N** ，数组中直到第 k 个索引的元素将小于零，并且在第 k 个索引之后将大于零。
即:

> **arr[0] < 0，arr[1] < 0，…，arr[k] < 0** 和 **arr[k + 1] > 0，arr[k + 2] > 0，…，arr[N–1]>0**。

**例:**

> **输入:** arr[] = { -1，1，2，-1}
> **输出:** 1
> 用任意正整数替换最后的-1。
> **输入:** arr[] = { -1，0，1，2 }
> **输出:** 1
> 将 0 替换为任意负整数。

**方法:**首先，对于每个有效的 **k** ，求其左边的非负整数个数和右边的非正整数个数。现在，对每一个有效的 **k** (0 ≤ k < n)运行一个循环，求其左边的非负整数个数和右边的非正整数个数的和，每一个 **k** 的这些值的最小值就是我们需要的答案。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of minimum operations required
int Minimum_Operations(int a[], int n)
{

    // To store the count of negative integers
    // on the right of the current index (inclusive)
    int np[n + 1];
    np[n] = 0;

    // Find the count of negative integers
    // on the right
    for (int i = n - 1; i >= 0; i--) {
        np[i] = np[i + 1];

        // If current element is negative
        if (a[i] <= 0)
            np[i]++;
    }

    // To store the count of positive elements
    int pos = 0;
    int ans = n;

    // Find the positive integers
    // on the left
    for (int i = 0; i < n - 1; i++) {

        // If current element is positive
        if (a[i] >= 0)
            pos++;

        // Update the answer
        ans = min(ans, pos + np[i + 1]);
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int a[] = { -1, 0, 1, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << Minimum_Operations(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of minimum operations required
static int Minimum_Operations(int []a, int n)
{

    // To store the count of negative integers
    // on the right of the current index (inclusive)
    int[] np = new int[n + 1];
    np[n] = 0;

    // Find the count of negative integers
    // on the right
    for (int i = n - 1; i >= 0; i--)
    {
        np[i] = np[i + 1];

        // If current element is negative
        if (a[i] <= 0)
            np[i]++;
    }

    // To store the count of positive elements
    int pos = 0;
    int ans = n;

    // Find the positive integers
    // on the left
    for (int i = 0; i < n - 1; i++)
    {

        // If current element is positive
        if (a[i] >= 0)
            pos++;

        // Update the answer
        ans = Math.min(ans, pos + np[i + 1]);
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void main(String args[])
{
    int []a = { -1, 0, 1, 2 };
    int n = a.length;
    System.out.print(Minimum_Operations(a, n));
}
}

// This code is contributed by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of minimum operations required
def Minimum_Operations(a, n):

    # To store the count of negative integers
    # on the right of the current index (inclusive)
    np = [0 for i in range(n + 1)]

    # Find the count of negative integers
    # on the right
    for i in range(n - 1, -1, -1):
        np[i] = np[i + 1]

        # If current element is negative
        if (a[i] <= 0):
            np[i] += 1

    # To store the count of positive elements
    pos = 0
    ans = n

    # Find the positive integers
    # on the left
    for i in range(n - 1):

        # If current element is positive
        if (a[i] >= 0):
            pos += 1

        # Update the answer
        ans = min(ans, pos + np[i + 1])

    # Return the required answer
    return ans

# Driver code
a = [-1, 0, 1, 2]
n = len(a)
print(Minimum_Operations(a, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of minimum operations required
static int Minimum_Operations(int []a, int n)
{

    // To store the count of negative integers
    // on the right of the current index (inclusive)
    int[] np = new int[n + 1];
    np[n] = 0;

    // Find the count of negative integers
    // on the right
    for (int i = n - 1; i >= 0; i--)
    {
        np[i] = np[i + 1];

        // If current element is negative
        if (a[i] <= 0)
            np[i]++;
    }

    // To store the count of positive elements
    int pos = 0;
    int ans = n;

    // Find the positive integers
    // on the left
    for (int i = 0; i < n - 1; i++)
    {

        // If current element is positive
        if (a[i] >= 0)
            pos++;

        // Update the answer
        ans = Math.Min(ans, pos + np[i + 1]);
    }

    // Return the required answer
    return ans;
}

// Driver code
static void Main()
{
    int []a = { -1, 0, 1, 2 };
    int n = a.Length;
    Console.WriteLine(Minimum_Operations(a, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of minimum operations required
function Minimum_Operations($a, $n)
{

    // To store the count of negative
    // integers on the right of the
    // current index (inclusive)
    $np = array();
    $np[$n] = 0;

    // Find the count of negative
    // integers on the right
    for ($i = $n - 1; $i >= 0; $i--)
    {
        $np[$i] = $np[$i + 1];

        // If current element is negative
        if ($a[$i] <= 0)
            $np[$i]++;
    }

    // To store the count of positive elements
    $pos = 0;
    $ans = $n;

    // Find the positive integers
    // on the left
    for ($i = 0; $i < $n - 1; $i++)
    {

        // If current element is positive
        if ($a[$i] >= 0)
            $pos++;

        // Update the answer
        $ans = min($ans, $pos + $np[$i + 1]);
    }

    // Return the required answer
    return $ans;
}

// Driver code
$a = array( -1, 0, 1, 2 );
$n = count($a) ;

echo Minimum_Operations($a, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count
// of minimum operations required
function Minimum_Operations(a, n)
{

    // To store the count of negative integers
    // on the right of the current index (inclusive)
    let np = Array(n+1).fill(0);
    np[n] = 0;

    // Find the count of negative integers
    // on the right
    for (let i = n - 1; i >= 0; i--)
    {
        np[i] = np[i + 1];

        // If current element is negative
        if (a[i] <= 0)
            np[i]++;
    }

    // To store the count of positive elements
    let pos = 0;
    let ans = n;

    // Find the positive integers
    // on the left
    for (let i = 0; i < n - 1; i++)
    {

        // If current element is positive
        if (a[i] >= 0)
            pos++;

        // Update the answer
        ans = Math.min(ans, pos + np[i + 1]);
    }

    // Return the required answer
    return ans;
}

// Driver Code

    let a = [ -1, 0, 1, 2 ];
    let n = a.length;
    document.write(Minimum_Operations(a, n));

</script>
```

**Output:** 

```
1
```