# 位“与”为 2 的幂的对的计数

> 原文:[https://www . geeksforgeeks . org/对计数-其位与是 2 的幂/](https://www.geeksforgeeks.org/count-of-pairs-whose-bitwise-and-is-a-power-of-2/)

给定一个 **N** 正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找出[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值为 2 的幂的对的数量。
**举例:**

> **输入:** arr[] = {2，1，3，4}
> **输出:** 2
> **解释:**
> 此数组中有 2 对(2，3)和(1，3)，它们的按位与值为:
> 1。(2&3)= 1 =(2<sup>0</sup>)
> 2。(1 & 3) = 1 = (2 <sup>0</sup> )。
> **输入:** arr[] = {6，4，2，3}
> **输出:** 4
> **解释:**
> 有 4 对(6，4)、(6，2)、(6，3)、(2，3)的按位 and 是 2 的幂。

**方法:**对于给定数组中的每个可能对，检查每对元素的**位与**是否为 2 的**完美幂**的想法。如果**“是”**则计数该对，否则检查下一对。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if x is power of 2
bool check(int x)
{
    // Returns true if x is a power of 2
    return x && (!(x & (x - 1)));
}

// Function to return the
// number of valid pairs
int count(int arr[], int n)
{
    int cnt = 0;

    // Iterate for all possible pairs
    for (int i = 0; i < n - 1; i++) {

        for (int j = i + 1; j < n; j++) {

            // Bitwise and value of
            // the pair is passed
            if (check(arr[i]
                      & arr[j]))
                cnt++;
        }
    }

    // Return the final count
    return cnt;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 6, 4, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << count(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Method to check if x is power of 2
static boolean check(int x)
{

    // First x in the below expression
    // is for the case when x is 0
    return x != 0 && ((x & (x - 1)) == 0);
}

// Function to return the
// number of valid pairs
static int count(int arr[], int n)
{
    int cnt = 0;

    // Iterate for all possible pairs
    for(int i = 0; i < n - 1; i++)
    {
       for(int j = i + 1; j < n; j++)
       {

          // Bitwise and value of
          // the pair is passed
          if (check(arr[i] & arr[j]))
              cnt++;
       }
    }

    // Return the final count
    return cnt;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = new int[]{ 6, 4, 2, 3 };

    int n = arr.length;

    // Function call
    System.out.print(count(arr, n));
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if x is power of 2
def check(x):

    # Returns true if x is a power of 2
    return x and (not(x & (x - 1)))

# Function to return the
# number of valid pairs
def count(arr, n):

    cnt = 0

    # Iterate for all possible pairs
    for i in range(n - 1):
        for j in range(i + 1, n):

            # Bitwise and value of
            # the pair is passed
            if check(arr[i] & arr[j]):
                cnt = cnt + 1

    # Return the final count
    return cnt

# Given array
arr = [ 6, 4, 2, 3 ]
n = len(arr)

# Function Call
print(count(arr, n))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Method to check if x is power of 2
static bool check(int x)
{

    // First x in the below expression
    // is for the case when x is 0
    return x != 0 && ((x & (x - 1)) == 0);
}

// Function to return the
// number of valid pairs
static int count(int []arr, int n)
{
    int cnt = 0;

    // Iterate for all possible pairs
    for(int i = 0; i < n - 1; i++)
    {
       for(int j = i + 1; j < n; j++)
       {

          // Bitwise and value of
          // the pair is passed
          if (check(arr[i] & arr[j]))
              cnt++;
       }
    }

    // Return the final count
    return cnt;
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int []arr = new int[]{ 6, 4, 2, 3 };

    int n = arr.Length;

    // Function call
    Console.Write(count(arr, n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Method to check if x is power of 2
function check(x)
{

    // First x in the below expression
    // is for the case when x is 0
    return x != 0 && ((x & (x - 1)) == 0);
}

// Function to return the
// number of valid pairs
function count(arr, n)
{
    let cnt = 0;

    // Iterate for all possible pairs
    for(let i = 0; i < n - 1; i++)
    {
       for(let j = i + 1; j < n; j++)
       {

          // Bitwise and value of
          // the pair is passed
          if (check(arr[i] & arr[j]))
              cnt++;
       }
    }

    // Return the final count
    return cnt;
}

// Driver code
    // Given array arr[]
    let arr = [ 6, 4, 2, 3 ];

    let n = arr.length;

    // Function call
    document.write(count(arr, n));

// This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*