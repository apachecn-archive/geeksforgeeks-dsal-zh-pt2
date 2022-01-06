# 具有作为完美立方体的和的子阵列的计数

> 原文:[https://www . geeksforgeeks . org/子阵列计数-拥有作为完美立方体的总和/](https://www.geeksforgeeks.org/count-of-subarrays-having-sum-as-a-perfect-cube/)

给定一个数组 **arr[]** ，任务是将具有和的子数组计数为一个完美立方体。
**例:**

> **输入:** arr[] = {6，10，9，2，1，113}
> **输出:** 3
> **解释:**
> 可能的子阵有–
> { { 1}、{6，10，9，2，1 }、{9，2，1，113}}
> **输入:** arr[] = {1}
> **输出:** 1 【T16

**方法:**想法是找到数组的前缀和，这样任何子数组的和都可以在 O(1)中计算出来。然后迭代每一个可能的子阵列，并检查子阵列的和是否是一个完美的立方体，如果是，则将计数增加 1。
以下是上述办法的实施情况:

## C++

```
// C++ implementationn to count
// subarrays having sum
// as  a perfect cube

#include <bits/stdc++.h>
using namespace std;
#define int long long

// Function to check for
// perfect cube or not
bool isCubicSquare(int x)
{
    int curoot = round(pow(x, 1.0 / 3.0));

    if (curoot * curoot * curoot == x)
        return true;
    return false;
}

// Function to count the subarray
// whose sum is a perfect cube
int count(int arr[], int n)
{
    int pre[n + 1];

    pre[0] = 0;

    // Loop to find the prefix sum
    // of the array
    for (int i = 1; i <= n; i++) {
        pre[i] = pre[i - 1] + arr[i - 1];
    }

    int ans = 0;

    // Loop to take every
    // possible subarrays
    for (int i = 0; i <= n; i++) {
        for (int j = i + 1; j <= n; j++) {

            // check for every
            // possible subarrays
            if (isCubicSquare((double)
                   (pre[j] - pre[i]))) {
                ans++;
            }
        }
    }

    return ans;
}

// Driver Code
int32_t main()
{
    int arr[6] = { 6, 10, 9, 2, 1, 113 };

    cout << count(arr, 6);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementationn to count subarrays 
// having sum as a perfect cube
import java.lang.Math;
class GFG{

// Function to check for
// perfect cube or not
public static boolean isCubicSquare(int x)
{
    double curoot = Math.round(
                    Math.pow(x, 1.0 / 3.0));

    if (curoot * curoot * curoot == x)
        return true;
    return false;
}

// Function to count the subarray
// whose sum is a perfect cube
public static int count(int arr[], int n)
{
    int[] pre = new int[n + 1];
    pre[0] = 0;

    // Loop to find the prefix sum
    // of the array
    for(int i = 1; i <= n; i++)
    {
       pre[i] = pre[i - 1] + arr[i - 1];
    }

    int ans = 0;

    // Loop to take every
    // possible subarrays
    for(int i = 0; i <= n; i++)
    {
       for(int j = i + 1; j <= n; j++)
       {

          // Check for every
          // possible subarrays
          if (isCubicSquare((pre[j] - pre[i])))
          {
              ans++;
          }
       }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 6, 10, 9, 2, 1, 113 };

    System.out.print(count(arr, 6));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementationn to count
# subarrays having sum
# as  a perfect cube

# Function to check for
# perfect cube or not
def isCubicSquare(x):

    curoot = round(pow(x,
                   1.0 / 3.0))

    if (curoot * curoot *
        curoot == x):
        return True
    return False

# Function to count the subarray
# whose sum is a perfect cube
def count(arr, n):

    pre = [0] * (n + 1)
    pre[0] = 0

    # Loop to find the prefix
    # sum of the array
    for  i in range (1, n + 1):
        pre[i] = pre[i - 1] + arr[i - 1]

    ans = 0

    # Loop to take every
    # possible subarrays
    for i in range (n + 1):
        for j in range (i + 1, n + 1):

            # Check for every
            # possible subarrays
            if (isCubicSquare((pre[j] -
                               pre[i]))):
                ans += 1

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [6, 10, 9, 2, 1, 113]
    print (count(arr, 6))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementationn to count subarrays
// having sum as a perfect cube
using System;
class GFG{

// Function to check for
// perfect cube or not
public static bool isCubicSquare(int x)
{
    double curoot = Math.Round(
                    Math.Pow(x, 1.0 / 3.0));

    if (curoot * curoot * curoot == x)
        return true;
    return false;
}

// Function to count the subarray
// whose sum is a perfect cube
public static int count(int []arr, int n)
{
    int[] pre = new int[n + 1];
    pre[0] = 0;

    // Loop to find the prefix sum
    // of the array
    for(int i = 1; i <= n; i++)
    {
       pre[i] = pre[i - 1] + arr[i - 1];
    }

    int ans = 0;

    // Loop to take every
    // possible subarrays
    for(int i = 0; i <= n; i++)
    {
       for(int j = i + 1; j <= n; j++)
       {

          // Check for every
          // possible subarrays
          if (isCubicSquare((pre[j] - pre[i])))
          {
              ans++;
          }
       }
    }
    return ans;
}

// Driver code
public static void Main()
{
    int []arr = { 6, 10, 9, 2, 1, 113 };

    Console.Write(count(arr, 6));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript implementationn to count
// subarrays having sum
// as  a perfect cube

// Function to check for
// perfect cube or not
function isCubicSquare( x)
{
    var curoot = Math.round(Math.pow(x, 1.0 / 3.0));

    if (curoot * curoot * curoot == x)
        return true;
    return false;
}

// Function to count the subarray
// whose sum is a perfect cube
function count(arr, n)
{
    var pre = Array(n+1);

    pre[0] = 0;

    // Loop to find the prefix sum
    // of the array
    for (var i = 1; i <= n; i++) {
        pre[i] = pre[i - 1] + arr[i - 1];
    }

    var ans = 0;

    // Loop to take every
    // possible subarrays
    for (var i = 0; i <= n; i++) {
        for (var j = i + 1; j <= n; j++) {

            // check for every
            // possible subarrays
            if (isCubicSquare(
                   (pre[j] - pre[i]))) {
                ans++;
            }
        }
    }

    return ans;
}

// Driver Code
var arr = [6, 10, 9, 2, 1, 113 ];
document.write( count(arr, 6));

// This code is contributed by itsok.
</script>
```

**Output:** 

```
3
```

**性能分析:**

*   **时间复杂度:** O(N <sup>2</sup> )
*   **辅助空间:** O(N)