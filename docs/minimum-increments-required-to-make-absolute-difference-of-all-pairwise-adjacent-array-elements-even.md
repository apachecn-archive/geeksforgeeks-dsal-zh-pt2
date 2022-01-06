# 使所有成对相邻数组元素的绝对差值相等所需的最小增量

> 原文:[https://www . geeksforgeeks . org/最小增量-要求对所有成对相邻数组元素进行绝对差值-偶数/](https://www.geeksforgeeks.org/minimum-increments-required-to-make-absolute-difference-of-all-pairwise-adjacent-array-elements-even/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到需要递增的最小数组元素数，以使所有成对连续元素之间的[绝对差为偶数。](https://www.geeksforgeeks.org/absolute-difference-of-all-pairwise-consecutive-elements-in-an-array/)

**示例:**

> **输入:** arr[] = {2，4，3，1，8}
> **输出:** 2
> **解释:**
> **操作 1:** 递增数组元素 arr[2](= 3)将数组修改为{2，4，4，1，8}。
> **操作 2:** 递增数组元素 arr[3](= 1)会将数组修改为{2，4，4，2，8}。
> 因此，所有成对相邻数组元素之间的差异为偶数。
> 
> **输入:** arr[] = {1，3，5，2}
> **输出:** 1

**方法:**利用两个数之差为偶数的情况下可以解决给定的问题，如果两个数都为奇数或偶数则只有[。因此，想法是增加所有奇数或偶数。两个数字都是偶数，对于增量的最小计数，打印奇数的最小](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)[计数或偶数的计数是](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of increments of array elements
// required to make difference between
// all pairwise adjacent elements even
int minOperations(int arr[], int n)
{
    // Stores the count of
    // odd and even elements
    int oddcount = 0, evencount = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Increment odd count
        if (arr[i] % 2 == 1)
            oddcount++;

        // Increment even count
        else
            evencount++;
    }

    // Return the minimum number
    // of operations required
    return min(oddcount, evencount);
}

// Driver Code
int main()
{
    int arr[] = { 2, 4, 3, 1, 8 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << minOperations(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the minimum number
// of increments of array elements
// required to make difference between
// all pairwise adjacent elements even
static int minOperations(int arr[], int n)
{

    // Stores the count of
    // odd and even elements
    int oddcount = 0, evencount = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Increment odd count
        if (arr[i] % 2 == 1)
            oddcount++;

        // Increment even count
        else
            evencount++;
    }

    // Return the minimum number
    // of operations required
    return Math.min(oddcount, evencount);
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 2, 4, 3, 1, 8 };
    int N = arr.length;

    System.out.println(minOperations(arr, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of increments of array elements
# required to make difference between
# all pairwise adjacent elements even
def minOperations(arr, n):

    # Stores the count of
    # odd and even elements
    oddcount, evencount = 0, 0

    # Traverse the array
    for i in range(n):

        # Increment odd count
        if (arr[i] % 2 == 1):
            oddcount += 1

        # Increment even count
        else:
            evencount += 1

    # Return the minimum number
    # of operations required
    return min(oddcount, evencount)

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 4, 3, 1, 8 ]
    N = len(arr)

    print (minOperations(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the minimum number
    // of increments of array elements
    // required to make difference between
    // all pairwise adjacent elements even
    static int minOperations(int[] arr, int n)
    {
        // Stores the count of
        // odd and even elements
        int oddcount = 0, evencount = 0;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // Increment odd count
            if (arr[i] % 2 == 1)
                oddcount++;

            // Increment even count
            else
                evencount++;
        }

        // Return the minimum number
        // of operations required
        return Math.Min(oddcount, evencount);
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, 4, 3, 1, 8 };
        int N = (arr.Length);
        Console.WriteLine(minOperations(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum number
// of increments of array elements
// required to make difference between
// all pairwise adjacent elements even
function minOperations(arr, n)
{

    // Stores the count of
    // odd and even elements
    var oddcount = 0, evencount = 0;

    // Traverse the array
    for(var i = 0; i < n; i++)
    {

        // Increment odd count
        if (arr[i] % 2 == 1)
            oddcount++;

        // Increment even count
        else
            evencount++;
    }

    // Return the minimum number
    // of operations required
    return Math.min(oddcount, evencount);
}

// Driver code
var arr = [ 2, 4, 3, 1, 8 ];
var N = arr.length;

document.write(minOperations(arr, N));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)