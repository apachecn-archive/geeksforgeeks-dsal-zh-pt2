# 以最小代价使所有数组元素相等

> 原文:[https://www . geesforgeks . org/make-array-elements-equal-mini-cost/](https://www.geeksforgeeks.org/make-array-elements-equal-minimum-cost/)

给定一个包含整数值的数组，我们需要使这个数组的所有值等于某个具有最小代价的整数值，其中将数组值 x 改为 y 的代价是 abs(x-y)。

**示例:**

```
Input  : arr[] = [1, 100, 101]
Output : 100
We can change all its values to 100 with minimum cost,
|1 - 100| + |100 - 100| + |101 - 100| = 100

Input  : arr[] = [4, 6]
Output : 2
We can change all its values to 5 with minimum cost,
|4 - 5| + |5 - 6| = 2
```

这个问题可以通过在改变目标等价值的同时观察成本来解决，即当目标等价值改变时，我们会看到成本的变化。可以观察到，当我们增加目标等价值时，总成本降低到极限，然后开始增加，即相对于目标等价值的成本图为 U 形，并且当成本图为 U 形时，[三元搜索](https://en.wikipedia.org/wiki/Ternary_search)可以应用于该搜索空间，并且我们的目标是获得代表最小成本的曲线的最底部点。我们将使数组的最小和最大值作为我们搜索空间的极限，然后我们将继续跳过搜索空间的 1/3 部分，直到我们到达 U 形曲线的最底部点。

请参见下面的代码，以便更好地理解。

## C++

```
// C++ program to find minimum cost to
// make all elements equal
#include <bits/stdc++.h>
using namespace std;

// Utility method to compute cost, when
// all values of array are made equal to X
int computeCost(int arr[], int N, int X)
{
    int cost = 0;
    for (int i = 0; i < N; i++)
        cost += abs(arr[i] - X);
    return cost;
}

// Method to find minimum cost to make all
// elements equal
int minCostToMakeElementEqual(int arr[], int N)
{
    int low, high;
    low = high = arr[0];

    // setting limits for ternary search by
    // smallest and largest element
    for (int i = 0; i < N; i++) {
        if (low > arr[i])
            low = arr[i];
        if (high < arr[i])
            high = arr[i];
    }

    /* loop until difference between low and high
       become less than 3, because after that
       mid1 and mid2 will start repeating
    */
    while ((high - low) > 2) {

        // mid1 and mid2 are representative array
        // equal values of search space
        int mid1 = low + (high - low) / 3;
        int mid2 = high - (high - low) / 3;

        int cost1 = computeCost(arr, N, mid1);
        int cost2 = computeCost(arr, N, mid2);

        // if mid2 point gives more total cost,
        // skip third part
        if (cost1 < cost2)
            high = mid2;

        // if mid1 point gives more total cost,
        // skip first part
        else
            low = mid1;
    }

    // computeCost gets optimum cost by sending
    // average of low and high as X
    return computeCost(arr, N, (low + high) / 2);
}

// Driver code to test above method
int main()
{
    int arr[] = { 1, 100, 101 };
    int N = sizeof(arr) / sizeof(int);
    cout << minCostToMakeElementEqual(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Make all array elements
// equal with minimum cost
class GFG {

    // Utility method to compute cost, when
    // all values of array are made equal to X
    public static int computeCost(int arr[], int N,
                                  int X)
    {
        int cost = 0;
        for (int i = 0; i < N; i++)
            cost += Math.abs(arr[i] - X);
        return cost;
    }

    // Method to find minimum cost to make all
    // elements equal
    public static int minCostToMakeElementEqual(int arr[],
                                                int N)
    {
        int low, high;
        low = high = arr[0];

        // setting limits for ternary search by
        // smallest and largest element
        for (int i = 0; i < N; i++) {
            if (low > arr[i])
                low = arr[i];
            if (high < arr[i])
                high = arr[i];
        }

        /* loop until difference between low and high
           become less than 3, because after that
           mid1 and mid2 will start repeating
        */
        while ((high - low) > 2) {
            // mid1 and mid2 are representative array
            // equal values of search space
            int mid1 = low + (high - low) / 3;
            int mid2 = high - (high - low) / 3;

            int cost1 = computeCost(arr, N, mid1);
            int cost2 = computeCost(arr, N, mid2);

            // if mid2 point gives more total cost,
            // skip third part
            if (cost1 < cost2)
                high = mid2;

            // if mid1 point gives more total cost,
            // skip first part
            else
                low = mid1;
        }

        // computeCost gets optimum cost by sending
        // average of low and high as X
        return computeCost(arr, N, (low + high) / 2);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = { 1, 100, 101 };
        int N = arr.length;
        System.out.println(minCostToMakeElementEqual(arr, N));
    }
}
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to find minimum 
# cost to make all elements equal

# Utility method to compute cost, when
# all values of array are made equal to X
def computeCost(arr, N, X):

    cost = 0
    for i in range(N):
        cost += abs(arr[i] - X)
    return cost

# Method to find minimum cost to
# make all elements equal
def minCostToMakeElementEqual(arr, N):

    low = high = arr[0]

    # Setting limits for ternary search
    # by smallest and largest element
    for i in range(N):

        if (low > arr[i]): low = arr[i]
        if (high < arr[i]): high = arr[i]

    # loop until difference between low and
    # high become less than 3, because after
    # that mid1 and mid2 will start repeating
    while ((high - low) > 2):

        # mid1 and mid2 are representative
        # array equal values of search space
        mid1 = low + (high - low) // 3
        mid2 = high - (high - low) // 3

        cost1 = computeCost(arr, N, mid1)
        cost2 = computeCost(arr, N, mid2)

        # if mid2 point gives more total
        # cost, skip third part
        if (cost1 < cost2):
            high = mid2

        # if mid1 point gives more total
        # cost, skip first part
        else:
            low = mid1

    # computeCost gets optimum cost by
    # sending average of low and high as X
    return computeCost(arr, N, (low + high) // 2)

# Driver code
arr = [1, 100, 101]
N = len(arr)
print(minCostToMakeElementEqual(arr, N))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# Code to Make all array elements
// equal with minimum cost
using System;

class GFG {

    // Utility method to compute cost, when
    // all values of array are made equal to X
    public static int computeCost(int[] arr, int N,
                                             int X)
    {
        int cost = 0;
        for (int i = 0; i < N; i++)
            cost += Math.Abs(arr[i] - X);
        return cost;
    }

    // Method to find minimum cost to
    // make all elements equal
    public static int minCostToMakeElementEqual(int[] arr,
                                                    int N)
    {
        int low, high;
        low = high = arr[0];

        // setting limits for ternary search by
        // smallest and largest element
        for (int i = 0; i < N; i++) {
            if (low > arr[i])
                low = arr[i];
            if (high < arr[i])
                high = arr[i];
        }

        /* loop until difference between low and high
        become less than 3, because after that
        mid1 and mid2 will start repeating
        */
        while ((high - low) > 2) {

            // mid1 and mid2 are representative array
            // equal values of search space
            int mid1 = low + (high - low) / 3;
            int mid2 = high - (high - low) / 3;

            int cost1 = computeCost(arr, N, mid1);
            int cost2 = computeCost(arr, N, mid2);

            // if mid2 point gives more total cost,
            // skip third part
            if (cost1 < cost2)
                high = mid2;

            // if mid1 point gives more total cost,
            // skip first part
            else
                low = mid1;
        }

        // computeCost gets optimum cost by sending
        // average of low and high as X
        return computeCost(arr, N, (low + high) / 2);
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int[] arr = { 1, 100, 101 };
        int N = arr.Length;
        Console.Write(minCostToMakeElementEqual(arr, N));
    }
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum cost
// to make all elements equal

// Utility method to compute cost,
// when all values of array are
// made equal to X
function computeCost($arr, $N, $X)
{
    $cost = 0;
    for ($i = 0; $i < $N; $i++)
        $cost += abs($arr[$i] - $X);
    return $cost;
}

// Method to find minimum cost
// to make all elements equal
function minCostToMakeElementEqual($arr, $N)
{
    $low; $high;
    $low = $high = $arr[0];

    // setting limits for ternary
    // search by smallest and
    // largest element
    for ($i = 0; $i < $N; $i++)
    {
        if ($low > $arr[$i])
            $low = $arr[$i];
        if ($high < $arr[$i])
            $high = $arr[$i];
    }

    /* loop until difference between
    low and high become less than 3,
    because after that mid1 and mid2
    will start repeating */
    while (($high - $low) > 2)
    {
        // mid1 and mid2 are representative
        // array equal values of search space
        $mid1 = $low + (floor($high - $low) / 3);
        $mid2 = $high - ($high - $low) / 3;

        $cost1 = computeCost($arr, $N, $mid1);
        $cost2 = computeCost($arr, $N, $mid2);

        // if mid2 point gives more total
        // cost, skip third part
        if ($cost1 < $cost2)
            $high = $mid2;

        // if mid1 point gives more
        // total cost, skip first part
        else
            $low = $mid1;
    }

    // computeCost gets optimum cost by
    // sending average of low and high as X
    return computeCost($arr, $N, ($low +
                                  $high) / 2);
}

// Driver Code
$arr = array( 1, 100, 101 );
$N = sizeof($arr) / sizeof($arr[0]);
echo minCostToMakeElementEqual($arr, $N);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum cost to
// make all elements equal

    // Utility method to compute cost, when
    // all values of array are made equal to X
    function computeCost(arr, N, X)
    {
        let cost = 0;
        for (let i = 0; i < N; i++)
            cost += Math.abs(arr[i] - X);
        return cost;
    }

    // Method to find minimum cost to make all
    // elements equal
    function minCostToMakeElementEqual(arr, N)
    {
        let low, high;
        low = high = arr[0];

        // setting limits for ternary search by
        // smallest and largest element
        for (let i = 0; i < N; i++) {
            if (low > arr[i])
                low = arr[i];
            if (high < arr[i])
                high = arr[i];
        }

        /* loop until difference between low and high
           become less than 3, because after that
           mid1 and mid2 will start repeating
        */
        while ((high - low) > 2) {
            // mid1 and mid2 are representative array
            // equal values of search space
            let mid1 = low + (high - low) / 3;
            let mid2 = high - (high - low) / 3;

            let cost1 = computeCost(arr, N, mid1);
            let cost2 = computeCost(arr, N, mid2);

            // if mid2 point gives more total cost,
            // skip third part
            if (cost1 < cost2)
                high = mid2;

            // if mid1 point gives more total cost,
            // skip first part
            else
                low = mid1;
        }

        // computeCost gets optimum cost by sending
        // average of low and high as X
        return Math.round(computeCost(arr, N, (low + high) / 2));
    }

// Driver Code

    let arr = [ 1, 100, 101 ];
    let N = arr.length;
    document.write(minCostToMakeElementEqual(arr, N));

</script>
```

**Output:** 

```
100
```

**交替解**
用几何方法思考。假设数组元素在 x 轴上是坐标。该问题简化为寻找另一个坐标，使得该选择和其他坐标之间的距离总和最小。
注意:如果坐标数是奇数，那么 y =中间元素。如果 y 是中间 2 个坐标之间的任何数。假设输入= [a，b，c，d]。输出是 b 和 c 之间的任意数字，包括两者。因此，成本是总和，现在我们已经为所有 I 选择了 y. sum|(y-ai)|可以很容易地计算出来。

编码真的很容易。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// This function assumes that a[] is
// sorted. If a[] is not sorted, we need
// to sort it first.
int minCostToMakeElementEqual(int a[], int n)
{

    // If there are odd elements, we choose
    // middle element
    int y;
    if (n % 2 == 1)
        y = a[n / 2];

    // If there are even elements, then we choose
    // the average of middle two.
    else
        y = (a[n / 2] + a[(n - 2) / 2]) / 2;

    // After deciding the final value, find the
    // result.
    int s = 0;
    for(int i = 0; i < n; i++)
        s += abs(a[i] - y);

    return s;
}

// Driver code
int main()
{
    int a[] = { 1, 100, 101 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << (minCostToMakeElementEqual(a, n));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;

class GFG{

// This function assumes that a[] is
// sorted. If a[] is not sorted, we need
// to sort it first.   
public static int minCostToMakeElementEqual(int a[],
                                            int n)
{

    // If there are odd elements, we choose
    // middle element
    int y;

    if (n % 2 == 1)
        y = a[n / 2];

    // If there are even elements, then we
    // choose the average of middle two.
    else
        y = (a[n / 2] + a[(n - 2) / 2]) / 2;

    // After deciding the final value,
    // find the result.
    int s = 0;

    for(int i = 0; i < n; i++)
        s += Math.abs(a[i] - y);

    return s;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 1, 100, 101 };
    int n = a.length;

    System.out.println(minCostToMakeElementEqual(a, n));
}
}

// This code is contributed by parascoding
```

## 蟒蛇 3

```
# This function assumes that a[] is
# sorted. If a[] is not sorted, we need
# to sort it first.
def minCostToMakeElementEqual(a):
    l = len(a)

    # If there are odd elements, we choose
    # middle element
    if (l%2 == 1):
        y = a[l//2]

    # If there are even elements, then we choose
    # the average of middle two.
    else:
        y = (a[l//2] + a[(l-2)//2])//2

    # After deciding the final value, find the
    # result.
    s = 0
    for i in range(l):
        s += abs(a[i]-y)
    return s

# Driver code
a = [1, 100, 101]
print(minCostToMakeElementEqual(a))
```

## C#

```
using System;
using System.Collections.Generic;

class GFG{

// This function assumes that a[] is
// sorted. If a[] is not sorted, we need
// to sort it first.   
static int minCostToMakeElementEqual(int[] a,
                                     int n)
{

    // If there are odd elements, we choose
    // middle element
    int y;

    if (n % 2 == 1)
        y = a[n / 2];

    // If there are even elements, then we
    // choose the average of middle two.
    else
        y = (a[n / 2] + a[(n - 2) / 2]) / 2;

    // After deciding the final value,
    // find the result.
    int s = 0;

    for(int i = 0; i < n; i++)
        s += Math.Abs(a[i] - y);

    return s;
}

// Driver code
static void Main()
{
    int[] a = { 1, 100, 101 };
    int n = a.Length;

    Console.WriteLine(
        minCostToMakeElementEqual(a, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// This function assumes that a[] is
// sorted. If a[] is not sorted, we need
// to sort it first.
function minCostToMakeElementEqual( a, n)
{

    // If there are odd elements, we choose
    // middle element
    let y;
    if (n % 2 == 1)
        y = a[Math.trunc(n / 2)];

    // If there are even elements, then we choose
    // the average of middle two.
    else
        y = Math.trunc((a[n / 2] + a[(n - 2) / 2]) / 2);

    // After deciding the final value, find the
    // result.
    let s = 0;
    for(let i = 0; i < n; i++)
        s += Math.abs(a[i] - y);

    return s;
}

    // Driver program

    let a = [ 1, 100, 101 ];
    let n = a.length;

    document.write(minCostToMakeElementEqual(a, n));

</script>
```

**Output**

```
100
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。