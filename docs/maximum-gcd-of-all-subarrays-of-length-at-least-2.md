# 长度至少为 2 的所有子阵列的最大 GCD

> 原文:[https://www . geesforgeks . org/maximum-gcd-of-all-subarles-length-at-2/](https://www.geeksforgeeks.org/maximum-gcd-of-all-subarrays-of-length-at-least-2/)

给定一个由 **N** 个数字组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找到所有尺寸大于 1 的子阵列的最大 [GCD。
**举例:**](https://www.geeksforgeeks.org/calculate-the-sum-of-gcd-over-all-subarrays/) 

> **输入:** arr[] = { 3，18，9，9，5，15，8，7，6，9 }
> **输出:** 9
> **说明:**
> 子阵{18，9，9 }的 GCD 最大，为 9。
> **输入:** arr[] = { 4，8，12，16，20，24 }
> **输出:** 4
> **说明:**
> 子阵列{ 4，18，12，16，20，24 }的 GCD 最大，为 4。

**天真的做法:**想法是[生成所有尺寸大于 1 的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，然后找到形成的所有子阵的 gcd 的最大值。
***时间复杂度:** O(N <sup>2</sup> )*
**高效途径:**让两个数的 [GCD](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) 为 **g** 。如果我们把 **g** 的 gcd 和第三个数字 **c** 相加，那么 gcd 会减少或保持不变，但永远不会增加。
思路是在**arr【】**中找到每一个连续对的 gcd，所有形成对的 gcd 的最大值就是期望的结果。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find GCD
int gcd(int a, int b)
{
    if (b == 0) {
        return a;
    }
    return gcd(b, a % b);
}

void findMaxGCD(int arr[], int n)
{

    // To store the maximum GCD
    int maxGCD = 0;

    // Traverse the array
    for (int i = 0; i < n - 1; i++) {

        // Find GCD of the consecutive
        // element
        int val = gcd(arr[i], arr[i + 1]);

        // If calculated GCD > maxGCD
        // then update it
        if (val > maxGCD) {
            maxGCD = val;
        }
    }

    // Print the maximum GCD
    cout << maxGCD << endl;
}

// Driver Code
int main()
{
    int arr[] = { 3, 18, 9, 9, 5,
                  15, 8, 7, 6, 9 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findMaxGCD(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find GCD
static int gcd(int a, int b)
{
    if (b == 0)
    {
        return a;
    }
    return gcd(b, a % b);
}

static void findMaxGCD(int arr[], int n)
{

    // To store the maximum GCD
    int maxGCD = 0;

    // Traverse the array
    for(int i = 0; i < n - 1; i++)
    {

       // Find GCD of the consecutive
       // element
       int val = gcd(arr[i], arr[i + 1]);

       // If calculated GCD > maxGCD
       // then update it
       if (val > maxGCD)
       {
           maxGCD = val;
       }
    }

    // Print the maximum GCD
    System.out.print(maxGCD + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 18, 9, 9, 5,
                  15, 8, 7, 6, 9 };
    int n = arr.length;

    // Function call
    findMaxGCD(arr, n);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find GCD
def gcd(a, b):

    if (b == 0):
        return a;
    return gcd(b, a % b);

def findMaxGCD(arr, n):

    # To store the maximum GCD
    maxGCD = 0;

    # Traverse the array
    for i in range(0, n - 1):

        # Find GCD of the consecutive
        # element
        val = gcd(arr[i], arr[i + 1]);

        # If calculated GCD > maxGCD
        # then update it
        if (val > maxGCD):
            maxGCD = val;

    # Print the maximum GCD
    print(maxGCD);

# Driver Code
if __name__ == '__main__':

    arr = [ 3, 18, 9, 9, 5,
            15, 8, 7, 6, 9 ];
    n = len(arr);

    # Function call
    findMaxGCD(arr, n);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find GCD
static int gcd(int a, int b)
{
    if (b == 0)
    {
        return a;
    }
    return gcd(b, a % b);
}

static void findMaxGCD(int []arr, int n)
{

    // To store the maximum GCD
    int maxGCD = 0;

    // Traverse the array
    for(int i = 0; i < n - 1; i++)
    {

        // Find GCD of the consecutive
        // element
        int val = gcd(arr[i], arr[i + 1]);

        // If calculated GCD > maxGCD
        // then update it
        if (val > maxGCD)
        {
            maxGCD = val;
        }
    }

    // Print the maximum GCD
    Console.Write(maxGCD + "\n");
}

// Driver Code
public static void Main()
{
    int []arr = { 3, 18, 9, 9, 5,
                 15, 8, 7, 6, 9 };
    int n = arr.Length;

    // Function call
    findMaxGCD(arr, n);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find GCD
function gcd(a, b)
{
    if (b == 0) {
        return a;
    }
    return gcd(b, a % b);
}

function findMaxGCD(arr, n)
{

    // To store the maximum GCD
    let maxGCD = 0;

    // Traverse the array
    for (let i = 0; i < n - 1; i++) {

        // Find GCD of the consecutive
        // element
        let val = gcd(arr[i], arr[i + 1]);

        // If calculated GCD > maxGCD
        // then update it
        if (val > maxGCD) {
            maxGCD = val;
        }
    }

    // Print the maximum GCD
    document.write(maxGCD + "<br>");
}

// Driver Code

    let arr = [ 3, 18, 9, 9, 5,
                15, 8, 7, 6, 9 ];

    let n = arr.length;

    // Function Call
    findMaxGCD(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N)* ，其中 N 为数组长度。

***辅助空间:** O(log(max(a，b)))*