# 计数乘积等于给定素数的幂的子阵列

> 原文:[https://www . geesforgeks . org/count-subarrays-具有等于给定素数幂的乘积/](https://www.geeksforgeeks.org/count-subarrays-having-product-equal-to-the-power-of-a-given-prime-number/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **M** ，任务是计算[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的数量，其元素的乘积等于 **M** 的幂，其中 **M** 是一个[素数](https://www.geeksforgeeks.org/prime-numbers/)。

**示例:**

> **输入:** arr[] = {2，2，2，2}，M = 2
> **输出:** 10
> **解释:**乘积等于 M = (4 * (4 + 1)) / 2 = 10 的所有可能的非空子阵
> 
> **输入:** arr[] = {1，1，1，3}，M = 3
> T3】输出: 10

**天真方法:**最简单的方法是[生成阵列**arr【】**的所有可能的子阵列](https://www.geeksforgeeks.org/sum-of-products-of-all-possible-subarrays/)，对于每个子阵列，检查它们的乘积是否为 **M** 的[次方。如果发现为真，那么将这些子阵列的计数增加 1。最后，打印获得的计数。](https://www.geeksforgeeks.org/java-program-to-calculate-power-of-a-number/)

***时间复杂度:**T3】O(N<sup>3</sup>)
*T8】辅助空间: O(1)**

**有效方法:**最优思想是基于这样一个事实:任何[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的乘积要等于 **M** 的幂，子阵列中的所有元素也必须是 **M** 的幂，因为 [**M** 是素数](https://www.geeksforgeeks.org/fermats-little-theorem/)。按照以下步骤解决给定的问题:

*   初始化变量，比如**和**，以存储所需的[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的计数
*   初始化一个变量，比如说 **cnt** ，来存储连续数字的计数，这些数字是**M**T5 的[次方。](https://www.geeksforgeeks.org/java-program-to-calculate-power-of-a-number/)
*   [使用一个变量遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)的索引范围**【0，N–1】**，说 **i** ，并执行以下操作:
    *   如果**arr【I】**是[的**M**T5】的幂。将 **cnt** 增加 1。更新**ans = ans+(CNT *(CNT–1))/2**](https://www.geeksforgeeks.org/java-program-to-calculate-power-of-a-number/)
    *   否则，更新 **cnt = 0。**
*   完成以上步骤后，打印 **cnt** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if y
// is a power of m or not
bool isPower(int m, int y)
{
    // Calculate log y base m and store
    // it in a variable with integer datatype
    int res1 = log(y) / log(m);

    // Calculate log y base m and store
    // it in a variable with double datatype
    double res2 = log(y) / log(m);

    // If res1 and res2 are equal, return
    // True. Otherwise, return false
    return (res1 == res2);
}

// Function to count the number of subarrays
// having product of elements equal to a
// power of m, where m is a prime number
int numSub(int arr[], int n, int m)
{
    // Stores the count of
    // subarrays required
    int ans = 0;

    // Stores current sequence of
    // consecutive array elements
    // which are a multiple of m
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If arr[i] is a power of M
        if (isPower(m, arr[i])) {

            // Increment cnt
            cnt++;

            // Update ans
            ans += (cnt * (cnt - 1)) / 2;
        }
        else {

            // Update cnt
            cnt = 0;
        }
    }

    // Return the count
    // of subarrays
    return ans;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 1, 1, 1, 3 };
    int m = 3;
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << numSub(arr, n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code of above approach
import java.util.*;
class GFG
{

// Function to check if y
// is a power of m or not
static boolean isPower(int m, int y)
{

    // Calculate log y base m and store
    // it in a variable with integer datatype
    int res1 = (int)Math.log(y) / (int)Math.log(m);

    // Calculate log y base m and store
    // it in a variable with double datatype
    double res2 = (int)Math.log(y) / (int)Math.log(m);

    // If res1 and res2 are equal, return
    // True. Otherwise, return false
    return (res1 == res2);
}

// Function to count the number of subarrays
// having product of elements equal to a
// power of m, where m is a prime number
static int numSub(int arr[], int n, int m)
{

    // Stores the count of
    // subarrays required
    int ans = 0;

    // Stores current sequence of
    // consecutive array elements
    // which are a multiple of m
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If arr[i] is a power of M
        if (isPower(m, arr[i])) {

            // Increment cnt
            cnt++;

            // Update ans
            ans += (cnt * (cnt - 1)) / 2;
        }
        else {

            // Update cnt
            cnt = 0;
        }
    }

    // Return the count
    // of subarrays
    return ans;
}

    // Driver code
   public static void main(String[] args)
    {

     // Input
    int arr[] = { 1, 1, 1, 3 };
    int m = 3;
    int n = arr.length;

   System.out.println(numSub(arr, n, m));
    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python 3 program for the above approach
from math import log

# Function to check if y
# is a power of m or not
def isPower(m, y):

    # Calculate log y base m and store
    # it in a variable with integer datatype
    res1 = log(y) // log(m)

    # Calculate log y base m and store
    # it in a variable with double datatype
    res2 = log(y) // log(m)

    # If res1 and res2 are equal, return
    # True. Otherwise, return false
    return (res1 == res2)

# Function to count the number of subarrays
# having product of elements equal to a
# power of m, where m is a prime number
def numSub(arr, n, m):

    # Stores the count of
    # subarrays required
    ans = 0

    # Stores current sequence of
    # consecutive array elements
    # which are a multiple of m
    cnt = 0

    # Traverse the array
    for i in range(n):

        # If arr[i] is a power of M
        if (isPower(m, arr[i])):

            # Increment cnt
            cnt += 1

            # Update ans
            ans += (cnt * (cnt - 1)) // 2

        else:
            # Update cnt
            cnt = 0

    # Return the count
    # of subarrays
    return ans

# Driver Code
if __name__ == '__main__':

    # Input
    arr =  [1, 1, 1, 3]
    m = 3
    n = len(arr)
    print(numSub(arr, n, m))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if y
// is a power of m or not
static bool isPower(int m, int y)
{

    // Calculate log y base m and store
    // it in a variable with integer datatype
    int res1 = (int)Math.Log(y) / (int)Math.Log(m);

    // Calculate log y base m and store
    // it in a variable with double datatype
    double res2 = (int)Math.Log(y) / (int)Math.Log(m);

    // If res1 and res2 are equal, return
    // True. Otherwise, return false
    return (res1 == res2);
}

// Function to count the number of subarrays
// having product of elements equal to a
// power of m, where m is a prime number
static int numSub(int[] arr, int n, int m)
{

    // Stores the count of
    // subarrays required
    int ans = 0;

    // Stores current sequence of
    // consecutive array elements
    // which are a multiple of m
    int cnt = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If arr[i] is a power of M
        if (isPower(m, arr[i]))
        {

            // Increment cnt
            cnt++;

            // Update ans
            ans += (cnt * (cnt - 1)) / 2;
        }
        else
        {

            // Update cnt
            cnt = 0;
        }
    }

    // Return the count
    // of subarrays
    return ans;
}

// Driver code
public static void Main()
{

    // Input
    int[] arr = { 1, 1, 1, 3 };
    int m = 3;
    int n = arr.Length;

    Console.Write(numSub(arr, n, m));
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if y
// is a power of m or not
function isPower(m, y)
{

    // Calculate log y base m and store
    // it in a variable with integer datatype
    let res1 = parseInt(Math.log(y) / Math.log(m));

    // Calculate log y base m and store
    // it in a variable with double datatype
    let res2 = Math.log(y) / Math.log(m);

    // If res1 and res2 are equal, return
    // True. Otherwise, return false
    return (res1 == res2);
}

// Function to count the number of subarrays
// having product of elements equal to a
// power of m, where m is a prime number
function numSub(arr, n, m)
{
    // Stores the count of
    // subarrays required
    let ans = 0;

    // Stores current sequence of
    // consecutive array elements
    // which are a multiple of m
    let cnt = 0;

    // Traverse the array
    for (let i = 0; i < n; i++) {

        // If arr[i] is a power of M
        if (isPower(m, arr[i])) {

            // Increment cnt
            cnt++;

            // Update ans
            ans += parseInt((cnt * (cnt - 1)) / 2);
        }
        else {

            // Update cnt
            cnt = 0;
        }
    }

    // Return the count
    // of subarrays
    return ans;
}

// Driver Code
    // Input
    let arr = [ 1, 1, 1, 3 ];
    let m = 3;
    let n = arr.length;

    document.write(numSub(arr, n, m));

  // This code is contributed by subhammahato348.
</script>
```

**Output:** 

```
10
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)