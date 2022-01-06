# 可购买糖果的最大数量

> 原文:[https://www . geeksforgeeks . org/最多可购买糖果数量/](https://www.geeksforgeeks.org/maximum-number-of-candies-that-can-be-bought/)

给定一个大小为 **n** 的数组 **arr[]** ，其中 **arr[i]** 是类型 **i** 的糖果数量。你有无限的钱。任务是购买尽可能多的满足以下条件的糖果:
如果您购买的是 **i** 类型的 **x(i)** 糖果(很明显，0 ≤ x(i) ≤ arr[i])，那么对于所有的 **j** (1 ≤ j ≤ i)必须至少持有以下其中一种:

1.  **x(j) < x(i)** (你买的 j 型糖果比 I 型少)
2.  **x(j) = 0** (你买了 0 颗 j 型糖果)

**例:**

> **输入:** arr[] = {1，2，1，3，6}
> **输出:** 10
> x[] = {0，0，1，3，6}其中 x[i]是购买的 I 型糖果数量
> **输入:** arr[] = {3，2，5，4，10}
> **输出:** 20
> **输入:** arr[] = {1，1

**进场:**我们可以用一种贪婪的进场方式，从数组末尾开始。如果我们已经服用了 **x** 类型的 **i + 1** 糖果，那么我们只能服用 **min(arr[i]，x–1)**类型的 **i** 糖果。如果这个值是负数，我们就不能购买当前类型的糖果。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum candies
// that can be bought
int maxCandies(int arr[], int n)
{

    // Buy all the candies of the last type
    int prevBought = arr[n - 1];
    int candies = prevBought;

    // Starting from second last
    for (int i = n - 2; i >= 0; i--) {

        // Amount of candies of the current
        // type that can be bought
        int x = min(prevBought - 1, arr[i]);

        if (x >= 0) {

            // Add candies of current type
            // that can be bought
            candies += x;

            // Update the previous bought amount
            prevBought = x;
        }
    }

    return candies;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 3, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxCandies(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum candies
// that can be bought
static int maxCandies(int arr[], int n)
{

    // Buy all the candies of the last type
    int prevBought = arr[n - 1];
    int candies = prevBought;

    // Starting from second last
    for (int i = n - 2; i >= 0; i--)
    {

        // Amount of candies of the current
        // type that can be bought
        int x = Math.min(prevBought - 1, arr[i]);

        if (x >= 0)
        {

            // Add candies of current type
            // that can be bought
            candies += x;

            // Update the previous bought amount
            prevBought = x;
        }
    }

    return candies;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 1, 3, 6 };
    int n = arr.length;
    System.out.println(maxCandies(arr, n));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum candies
# that can be bought
def maxCandies(arr, n) :

    # Buy all the candies of the last type
    prevBought = arr[n - 1];
    candies = prevBought;

    # Starting from second last
    for i in range(n - 2, -1, -1) :

        # Amount of candies of the current
        # type that can be bought
        x = min(prevBought - 1, arr[i]);
        if (x >= 0) :

            # Add candies of current type
            # that can be bought
            candies += x;

            # Update the previous bought amount
            prevBought = x;

    return candies;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 1, 3, 6 ];
    n = len(arr)
    print(maxCandies(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum candies
// that can be bought
static int maxCandies(int[] arr, int n)
{

    // Buy all the candies of the last type
    int prevBought = arr[n - 1];
    int candies = prevBought;

    // Starting from second last
    for (int i = n - 2; i >= 0; i--)
    {

        // Amount of candies of the current
        // type that can be bought
        int x = Math.Min(prevBought - 1, arr[i]);

        if (x >= 0)
        {

            // Add candies of current type
            // that can be bought
            candies += x;

            // Update the previous bought amount
            prevBought = x;
        }
    }

    return candies;
}

// Driver code
public static void Main()
{
    int[] arr= { 1, 2, 1, 3, 6 };
    int n = arr.Length;
    Console.WriteLine(maxCandies(arr, n));
}
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum candies
// that can be bought
function maxCandies($arr, $n)
{

    // Buy all the candies of the last type
    $prevBought = $arr[$n - 1];
    $candies = $prevBought;

    // Starting from second last
    for ($i = $n - 2; $i >= 0; $i--)
    {

        // Amount of candies of the current
        // type that can be bought
        $x = min($prevBought - 1, $arr[$i]);

        if ($x >= 0)
        {

            // Add candies of current type
            // that can be bought
            $candies += $x;

            // Update the previous bought amount
            $prevBought = $x;
        }
    }

    return $candies;
}

// Driver code
$arr = array(1, 2, 1, 3, 6 );
$n = sizeof($arr);
echo(maxCandies($arr, $n));

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum candies
// that can be bought
function maxCandies(arr, n)
{

    // Buy all the candies of the last type
    let prevBought = arr[n - 1];
    let candies = prevBought;

    // Starting from second last
    for (let i = n - 2; i >= 0; i--)
    {

        // Amount of candies of the current
        // type that can be bought
        let x = Math.min(prevBought - 1, arr[i]);

        if (x >= 0)
        {

            // Add candies of current type
            // that can be bought
            candies += x;

            // Update the previous bought amount
            prevBought = x;
        }
    }

    return candies;
} 

// Driver Code

      let arr = [ 1, 2, 1, 3, 6 ];
    let n = arr.length;
    document.write(maxCandies(arr, n));

</script>
```

**Output:** 

```
10
```