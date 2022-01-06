# 长度至少为 2 的所有子阵列的最小 LCM

> 原文:[https://www . geeksforgeeks . org/所有长度至少为 2 的子阵列中的最小值 LCM/](https://www.geeksforgeeks.org/minimum-lcm-of-all-subarrays-of-length-at-least-2/)

给定一个正整数数组**arr[]****N**。任务是找到所有尺寸大于 1 的子阵列的最小 [LCM。](https://www.geeksforgeeks.org/minimum-lcm-and-gcd-possible-among-all-possible-sub-arrays/)

**示例:**

> **输入:** arr[] = { 3，18，9，18，5，15，8，7，6，9 }
> **输出:** 15
> **说明:**
> 子阵{5，15}的 LCM 最小，为 15。
> 
> **输入:** arr[] = { 4，8，12，16，20，24 }
> **输出:** 8
> **说明:**
> 子阵{ 4，8}的 LCM 最小，为 8。

**天真方法:**想法是[生成所有可能的长度至少为 2 的](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)子阵，并找到所有形成的子阵的 LCM。打印所有子阵列中的最小 LCM。

**时间复杂度:***O(N<sup>3</sup>)*
**辅助空间:** *O(1)*

**有效方法:**为了优化上述方法，我们必须观察到，当且仅当必须计算 LCM 的元素数量最小时，两个或更多数量的 LCM 将更少。子阵列大小的最小可能值是 2。因此，想法是找到所有相邻对的 LCM，并打印它们的最小值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find LCM pf two numbers
int LCM(int a, int b)
{
    // Initialise lcm value
    int lcm = a > b ? a : b;

    while (true) {

        // Check for divisibility
        // of a and b by the lcm
        if (lcm % a == 0 && lcm % b == 0)
            break;
        else
            lcm++;
    }
    return lcm;
}

// Function to find the Minimum LCM of
// all subarrays of length greater than 1
void findMinLCM(int arr[], int n)
{

    // Store the minimum LCM
    int minLCM = INT_MAX;

    // Traverse the array
    for (int i = 0; i < n - 1; i++) {

        // Find LCM of consecutive element
        int val = LCM(arr[i], arr[i + 1]);

        // Check if the calculated LCM is
        // less than the minLCM then update it
        if (val < minLCM) {
            minLCM = val;
        }
    }

    // Print the minimum LCM
    cout << minLCM << endl;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 4, 8, 12, 16, 20, 24 };

    // Size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findMinLCM(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find LCM pf two numbers
static int LCM(int a, int b)
{

    // Initialise lcm value
    int lcm = a > b ? a : b;

    while (true)
    {

        // Check for divisibility
        // of a and b by the lcm
        if (lcm % a == 0 && lcm % b == 0)
            break;
        else
            lcm++;
    }
    return lcm;
}

// Function to find the Minimum LCM of
// all subarrays of length greater than 1
static void findMinLCM(int arr[], int n)
{

    // Store the minimum LCM
    int minLCM = Integer.MAX_VALUE;

    // Traverse the array
    for(int i = 0; i < n - 1; i++)
    {

        // Find LCM of consecutive element
        int val = LCM(arr[i], arr[i + 1]);

        // Check if the calculated LCM is
        // less than the minLCM then update it
        if (val < minLCM)
        {
            minLCM = val;
        }
    }

    // Print the minimum LCM
    System.out.print(minLCM + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 4, 8, 12, 16, 20, 24 };

    // Size of the array
    int n = arr.length;

    // Function call
    findMinLCM(arr, n);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find LCM pf two numbers
def LCM(a, b):

    # Initialise lcm value
    lcm = a if a > b else b

    while (True):

        # Check for divisibility
        # of a and b by the lcm
        if (lcm % a == 0 and lcm % b == 0):
            break
        else:
            lcm += 1

    return lcm

# Function to find the Minimum LCM of
# all subarrays of length greater than 1
def findMinLCM(arr, n):

    # Store the minimum LCM
    minLCM = sys.maxsize

    # Traverse the array
    for i in range(n - 1):

        # Find LCM of consecutive element
        val = LCM(arr[i], arr[i + 1])

        # Check if the calculated LCM is
        # less than the minLCM then update it
        if (val < minLCM):
            minLCM = val

    # Print the minimum LCM
    print(minLCM)

# Driver Code

# Given array arr[]
arr = [ 4, 8, 12, 16, 20, 24 ]

# Size of the array
n = len(arr)

# Function call
findMinLCM(arr, n)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find LCM pf two numbers
static int LCM(int a, int b)
{

    // Initialise lcm value
    int lcm = a > b ? a : b;

    while (true)
    {

        // Check for divisibility
        // of a and b by the lcm
        if (lcm % a == 0 && lcm % b == 0)
            break;
        else
            lcm++;
    }
    return lcm;
}

// Function to find the Minimum LCM of
// all subarrays of length greater than 1
static void findMinLCM(int []arr, int n)
{

    // Store the minimum LCM
    int minLCM = int.MaxValue;

    // Traverse the array
    for(int i = 0; i < n - 1; i++)
    {

        // Find LCM of consecutive element
        int val = LCM(arr[i], arr[i + 1]);

        // Check if the calculated LCM is
        // less than the minLCM then update it
        if (val < minLCM)
        {
            minLCM = val;
        }
    }

    // Print the minimum LCM
    Console.Write(minLCM + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 4, 8, 12, 16, 20, 24 };

    // Size of the array
    int n = arr.Length;

    // Function call
    findMinLCM(arr, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find LCM of two numbers
function LCM(a, b)
{
    // Initialise lcm value
    let lcm = a > b ? a : b;

    while (true) {

        // Check for divisibility
        // of a and b by the lcm
        if (lcm % a == 0 && lcm % b == 0)
            break;
        else
            lcm++;
    }
    return lcm;
}

// Function to find the Minimum LCM of
// all subarrays of length greater than 1
function findMinLCM(arr, n)
{

    // Store the minimum LCM
    let minLCM = Number.MAX_VALUE;

    // Traverse the array
    for (let i = 0; i < n - 1; i++) {

        // Find LCM of consecutive element
        let val = LCM(arr[i], arr[i + 1]);

        // Check if the calculated LCM is
        // less than the minLCM then update it
        if (val < minLCM) {
            minLCM = val;
        }
    }

    // Print the minimum LCM
    document.write(minLCM + "<br>");
}

// Driver Code

    // Given array arr[]
    let arr = [ 4, 8, 12, 16, 20, 24 ];

    // Size of the array
    let n = arr.length;

    // Function Call
    findMinLCM(arr, n);

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
8
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*