# 从绝对差值不小于数组中最小元素的数组中计数对

> 原文:[https://www . geeksforgeeks . org/从绝对差不小于对中最小元素的数组中计数对/](https://www.geeksforgeeks.org/count-pairs-from-an-array-with-absolute-difference-not-less-than-the-minimum-element-in-the-pair/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到对 **(arr[i]，arr[j])** 的数量，使得两个元素之间的绝对差至少等于对中的最小元素。

**示例:**

> **输入:** arr[] = {1，2，2，3}
> **输出:** 3
> **解释:**
> 满足给定标准的配对如下:
> 
> 1.  (arr[0]，arr[1]):两者的绝对差为 ABS(1–2)= 1，这至少是两者的最小值，即 min(1。2) = 1.
> 2.  (arr[0]，arr[2]):两者的绝对差为 ABS(1–2)= 1，这至少是两者的最小值，即 min(1。2) = 1.
> 3.  (arr[0]，arr[3]):两者的绝对差为 ABS(1–2)= 1，这至少是两者的最小值，即 min(1。2) = 1.
> 
> 因此，这种对的总数是 3。
> 
> **输入:** arr[] = {2，3，6 }
> T3】输出: 2

**天真方法:**解决给定问题的简单方法是[从数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并对满足给定条件的对进行计数。检查所有对后，打印获得的总计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过[对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，然后迭代两个嵌套循环，使得第一个循环迭代到 **N** 为止，第二个循环从**arr[I]–(I % arr[I])**开始迭代，以 **j** 为增量 **j += arr[i]** 直到 **N** 为止，并对满足给定条件的那些对进行计数。按照以下步骤解决问题:

*   初始化变量，说**计数**为 **0** ，存储结果对的计数。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【arr[I]–(I % arr[I])，N】**，增量 **j** 为 **j += arr[i]** ，如果 **i** 小于 **j** 和**ABS(arr[I]–arr[j])**至少是 **arr[i]的最小值**
*   执行上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of pairs
// (i, j) such that abs(a[i]-a[j]) is
// at least the minimum of (a[i], a[j])
int getPairsCount(int arr[], int n)
{
    // Stores the resultant count of pairs
    int count = 0;

    // Iterate over the range [0, n]
    for (int i = 0; i < n; i++) {

        // Iterate from arr[i] - (i%arr[i])
        // till n with an increment
        // of arr[i]
        for (int j = arr[i] - (i % arr[i]);
             j < n; j += arr[i]) {

            // Count the possible pairs
            if (i < j
                && abs(arr[i] - arr[j])
                       >= min(arr[i], arr[j])) {
                count++;
            }
        }
    }

    // Return the total count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << getPairsCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find the number of pairs
    // (i, j) such that abs(a[i]-a[j]) is
    // at least the minimum of (a[i], a[j])
    static int getPairsCount(int arr[], int n)
    {

        // Stores the resultant count of pairs
        int count = 0;

        // Iterate over the range [0, n]
        for (int i = 0; i < n; i++) {

            // Iterate from arr[i] - (i%arr[i])
            // till n with an increment
            // of arr[i]
            for (int j = arr[i] - (i % arr[i]); j < n;
                 j += arr[i]) {

                // Count the possible pairs
                if (i < j
                    && Math.abs(arr[i] - arr[j])
                           >= Math.min(arr[i], arr[j])) {
                    count++;
                }
            }
        }

        // Return the total count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 2, 3 };
        int N = arr.length;

        System.out.println(getPairsCount(arr, N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the number of pairs
# (i, j) such that abs(a[i]-a[j]) is
# at least the minimum of (a[i], a[j])
def getPairsCount(arr, n):

    # Stores the resultant count of pairs
    count = 0

    # Iterate over the range [0, n]
    for i in range(n):

        # Iterate from arr[i] - (i%arr[i])
        # till n with an increment
        # of arr[i]
        for j in range(arr[i] - (i % arr[i]),n,arr[i]):

            # Count the possible pairs
            if (i < j and abs(arr[i] - arr[j]) >= min(arr[i], arr[j])):
                count += 1

    # Return the total count
    return count

# Driver Code
if __name__ == '__main__':
    arr = [1, 2, 2, 3]
    N = len(arr)
    print(getPairsCount(arr, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for above approach
using System;

class GFG{

    // Function to find the number of pairs
    // (i, j) such that abs(a[i]-a[j]) is
    // at least the minimum of (a[i], a[j])
    static int getPairsCount(int[] arr, int n)
    {

        // Stores the resultant count of pairs
        int count = 0;

        // Iterate over the range [0, n]
        for (int i = 0; i < n; i++) {

            // Iterate from arr[i] - (i%arr[i])
            // till n with an increment
            // of arr[i]
            for (int j = arr[i] - (i % arr[i]); j < n;
                 j += arr[i]) {

                // Count the possible pairs
                if (i < j
                    && Math.Abs(arr[i] - arr[j])
                           >= Math.Min(arr[i], arr[j])) {
                    count++;
                }
            }
        }

        // Return the total count
        return count;
    }

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 1, 2, 2, 3 };
    int N = arr.Length;

    Console.Write(getPairsCount(arr, N));

}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the number of pairs
// (i, j) such that abs(a[i]-a[j]) is
// at least the minimum of (a[i], a[j])
function getPairsCount(arr, n)
{

    // Stores the resultant count of pairs
    let count = 0;

    // Iterate over the range [0, n]
    for(let i = 0; i < n; i++)
    {

        // Iterate from arr[i] - (i%arr[i])
        // till n with an increment
        // of arr[i]
        for(let j = arr[i] - (i % arr[i]);
                j < n; j += arr[i])
        {

            // Count the possible pairs
            if (i < j && Math.abs(arr[i] - arr[j]) >=
                         Math.min(arr[i], arr[j]))
            {
                count++;
            }
        }
    }

    // Return the total count
    return count;
}

// Driver Code
let arr = [ 1, 2, 2, 3 ];
let N = arr.length;

document.write(getPairsCount(arr, N));

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*