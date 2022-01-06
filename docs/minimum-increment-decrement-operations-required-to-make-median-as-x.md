# 使中位数为 X 所需的最小增量/减量操作

> 原文:[https://www . geesforgeks . org/minimum-increment-减量-operations-required-make-median-as-x/](https://www.geeksforgeeks.org/minimum-increment-decrement-operations-required-to-make-median-as-x/)

给定 n 个奇数的**数组 A[]** 和一个**整数 X** 。计算使数组的中值等于 X 所需的最小运算次数，其中，在一次运算中，我们可以将任何单个元素增加或减少一。

**示例:**

> **输入:** A[] = {6，5，8}，X = 8
> **输出:** 2
> **说明:**
> 这里 6 可以增加 2 倍。数组将变成 8，5，8，排序后变成 5，8，8，因此中位数等于 8。
> 
> **输入:** A[] = {1，4，7，12，3，5，9}，X = 5
> **输出:** 0
> **说明:**
> 排序后 5 处于中间位置，因此需要 0 步。

**方法:**改变数组中值的想法是[给定数组](https://www.geeksforgeeks.org/array-data-structure/array-sorting/)排序。然后排序后，最好的中值候选是**中间元素**，因为中间元素前的数字越小越好，中间元素后的数字越大越好。

下面是上述方法的实现:

## C++

```
// C++ implementation to determine the
// Minimum numbers of steps to make
// median of an array equal X

#include <bits/stdc++.h>
using namespace std;

// Function to count minimum
// required operations to
// make median X
int count(vector<int> a, int X)
{
    // Sorting the array a[]
    sort(a.begin(), a.end());
    int ans = 0;

    // Calculate the size of array
    int n = a.size();

    // Iterate over the array
    for (int i = 0; i < n; i++) {
        // For all elements
        // less than median
        if (i < n / 2)
            ans += max(0, a[i] - X);

        // For element equal
        // to median
        else if (i == n / 2)
            ans += abs(X - a[i]);

        // For all elements
        // greater than median
        else
            ans += max(0, X - a[i]);
    }

    // Return the answer
    return ans;
}

// Driver code
int main()
{
    vector<int> a = { 6, 5, 8 };
    int X = 8;
    cout << count(a, X) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to determine the
// Minimum numbers of steps to make
// median of an array equal X
import java.util.*;

class GFG{

// Function to count minimum
// required operations to
// make median X
static int count(int[] a, int X)
{

    // Sorting the array a[]
    Arrays.sort(a);
    int ans = 0;

    // Calculate the size of array
    int n = a.length;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {

       // For all elements
       // less than median
       if (i < n / 2)
           ans += Math.max(0, a[i] - X);

       // For element equal
       // to median
       else if (i == n / 2)
           ans += Math.abs(X - a[i]);

       // For all elements
       // greater than median
       else
           ans += Math.max(0, X - a[i]);
    }

    // Return the answer
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int []a = { 6, 5, 8 };
    int X = 8;

    System.out.print(count(a, X) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to determine the
# Minimum numbers of steps to make
# median of an array equal X

# Function to count minimum
# required operations to
# make median X
def count(a, X):

    # Sorting the array a[]
    a.sort()
    ans = 0

    # Calculate the size of array
    n = len(a)

    # Iterate over the array
    for i in range(n):

        # For all elements
        # less than median
        if (i < n // 2):
            ans += max(0, a[i] - X)

        # For element equal
        # to median
        elif (i == n // 2):
            ans += abs(X - a[i])

        # For all elements
        # greater than median
        else:
            ans += max(0, X - a[i]);

    # Return the answer
    return ans

# Driver code
a = [ 6, 5, 8 ]
X = 8

print(count(a, X))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to determine the
// Minimum numbers of steps to make
// median of an array equal X
using System;

class GFG{

// Function to count minimum
// required operations to
// make median X
static int count(int[] a, int X)
{

    // Sorting the array []a
    Array.Sort(a);
    int ans = 0;

    // Calculate the size of array
    int n = a.Length;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {

       // For all elements
       // less than median
       if (i < n / 2)
           ans += Math.Max(0, a[i] - X);

       // For element equal
       // to median
       else if (i == n / 2)
           ans += Math.Abs(X - a[i]);

       // For all elements
       // greater than median
       else
           ans += Math.Max(0, X - a[i]);
    }

    // Return the answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 6, 5, 8 };
    int X = 8;

    Console.Write(count(a, X) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript implementation to determine the
// Minimum numbers of steps to make
// median of an array equal X

// Creating the bblSort function
function bblSort(arr)
{
    for(var i = 0; i < arr.length; i++)
    {

        // Last i elements are already in place 
        for(var j = 0; j < (arr.length - i - 1); j++)
        {

            // Checking if the item at present
            // iteration is greater than the
            // next iteration
            if (arr[j] > arr[j+1])
            {

                // If the condition is true
                // then swap them
                var temp = arr[j]
                arr[j] = arr[j + 1]
                arr[j + 1] = temp
            }
        }
    }

    // Return the sorted array
    return (arr);
}

// Function to count minimum
// required operations to
// make median X
function count(a, X)
{

    // Sorting the array a
    a  = bblSort(a);
    var ans = 0;

    // Calculate the size of array
    var n = a.length;

    // Iterate over the array
    for(i = 0; i < n; i++)
    {

        // For all elements
        // less than median
        if (i < parseInt(n / 2))
            ans += Math.max(0, a[i] - X);

        // For element equal
        // to median
        else if (i == parseInt(n / 2))
            ans += Math.abs(X - a[i]);

        // For all elements
        // greater than median
        else
            ans += Math.max(0, X - a[i]);
    }

    // Return the answer
    return ans;
}

// Driver code
var a = [ 6, 5, 8 ];
var X = 8;

document.write(count(a, X));

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log N)*
***辅助空间复杂度:** O(1)*