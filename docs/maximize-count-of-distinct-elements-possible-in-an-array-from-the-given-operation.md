# 从给定操作中最大化数组中可能的不同元素的数量

> 原文:[https://www . geeksforgeeks . org/从给定操作中最大化数组中可能的不同元素的数量/](https://www.geeksforgeeks.org/maximize-count-of-distinct-elements-possible-in-an-array-from-the-given-operation/)

给定一个大小为 **N** 的数组 **A[]** ，任务是通过插入现有数组元素的绝对差来最大化数组中不同元素的数量。

**示例:**

> **输入:** A[] = {1，2，3，5}
> **输出:** 5
> **解释:**
> 数组元素之间可能的绝对差异是:
> (2–1)= 1
> (5–3)= 2
> (5–2)= 3
> (5–1)= 4
> 因此，在数组中插入 4 可以最大化不同元素的数量。
> **输入:** A[] = {1，2，3，6}
> **输出:** 6

**天真方法:**
从数组中生成所有可能的对，并将它们的绝对差异存储在[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。将所有数组元素插入集合中。集合的最终大小表示数组在执行给定操作后可以拥有的最大不同元素。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*
**高效途径:**
按照以下步骤优化上述途径:

1.  找到数组的最大元素。任意两个元素的最大可能绝对差不超过数组的最大元素。

2.  计算数组的 [GCD，因为它是整个数组的公因数。](https://www.geeksforgeeks.org/gcd-two-array-numbers/) 
3.  用数组的 gcd 除最大元素，得到不同元素的计数。

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum
// possible distinct elements that
// can be obtained from the array
// by performing the given operations
#include <bits/stdc++.h>
using namespace std;

// Function to find the gcd
// of two numbers
int gcd(int x, int y)
{
    if (x == 0)
        return y;
    return gcd(y % x, x);
}

// Function to calculate and return
// the count of maximum possible
// distinct elements in the array
int findDistinct(int arr[], int n)
{
    // Find the maximum element
    int maximum = *max_element(arr,
                               arr + n);

    // Base Case
    if (n == 1)
        return 1;

    if (n == 2) {
        return (maximum / gcd(arr[0],
                              arr[1]));
    }

    // Finding the gcd of first
    // two element
    int k = gcd(arr[0], arr[1]);

    // Calculate Gcd of the array
    for (int i = 2; i < n; i++) {
        k = gcd(k, arr[i]);
    }

    // Return the total count
    // of distinct elements
    return (maximum / k);
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findDistinct(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// possible distinct elements that
// can be obtained from the array
// by performing the given operations
import java.util.*;

class GFG{

// Function to find the gcd
// of two numbers
static int gcd(int x, int y)
{
    if (x == 0)
        return y;
    return gcd(y % x, x);
}

// Function to calculate and return
// the count of maximum possible
// distinct elements in the array
static int findDistinct(int arr[], int n)
{

    // Find the maximum element
    int maximum = Arrays.stream(arr).max().getAsInt();

    // Base Case
    if (n == 1)
        return 1;

    if (n == 2)
    {
        return (maximum / gcd(arr[0],
                              arr[1]));
    }

    // Finding the gcd of first
    // two element
    int k = gcd(arr[0], arr[1]);

    // Calculate Gcd of the array
    for(int i = 2; i < n; i++)
    {
        k = gcd(k, arr[i]);
    }

    // Return the total count
    // of distinct elements
    return (maximum / k);
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 3, 5 };
    int n = arr.length;

    System.out.println(findDistinct(arr, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# possible distinct elements that
# can be obtained from the array
# by performing the given operations

# Function to find the gcd
# of two numbers
def gcd(x, y):

    if (x == 0):
        return y
    return gcd(y % x, x)

# Function to calculate and return
# the count of maximum possible
# distinct elements in the array
def findDistinct(arr, n):

    # Find the maximum element
    maximum = max(arr)

    # Base Case
    if (n == 1):
        return 1

    if (n == 2):
        return (maximum // gcd(arr[0],
                               arr[1]))

    # Finding the gcd of first
    # two element
    k = gcd(arr[0], arr[1])

    # Calculate Gcd of the array
    for i in range(2, n):
        k = gcd(k, arr[i])

    # Return the total count
    # of distinct elements
    return (maximum // k)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 5 ]
    n = len(arr)

    print(findDistinct(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the maximum
// possible distinct elements that
// can be obtained from the array
// by performing the given operations
using System;
using System.Linq;
class GFG{

// Function to find the gcd
// of two numbers
static int gcd(int x, int y)
{
    if (x == 0)
        return y;
    return gcd(y % x, x);
}

// Function to calculate and return
// the count of maximum possible
// distinct elements in the array
static int findDistinct(int []arr, int n)
{
    // Find the maximum element
    int maximum = arr.Max();

    // Base Case
    if (n == 1)
        return 1;

    if (n == 2)
    {
        return (maximum / gcd(arr[0],
                              arr[1]));
    }

    // Finding the gcd of first
    // two element
    int k = gcd(arr[0], arr[1]);

    // Calculate Gcd of the array
    for (int i = 2; i < n; i++)
    {
        k = gcd(k, arr[i]);
    }

    // Return the total count
    // of distinct elements
    return (maximum / k);
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 2, 3, 5 };
    int n = arr.Length;

    Console.Write(findDistinct(arr, n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// possible distinct elements that
// can be obtained from the array
// by performing the given operations

// Function to find the gcd
// of two numbers
function gcd(x, y)
{
    if (x == 0)
        return y;
    return gcd(y % x, x);
}

// Function to calculate and return
// the count of maximum possible
// distinct elements in the array
function findDistinct(arr, n)
{

    // Find the maximum element
    let maximum = Math.max(...arr);

    // Base Case
    if (n == 1)
        return 1;

    if (n == 2)
    {
        return (maximum / gcd(arr[0],
                              arr[1]));
    }

    // Finding the gcd of first
    // two element
    let k = gcd(arr[0], arr[1]);

    // Calculate Gcd of the array
    for(let i = 2; i < n; i++)
    {
        k = gcd(k, arr[i]);
    }

    // Return the total count
    // of distinct elements
    return (maximum / k);
}

// Driver Code

    let arr = [ 1, 2, 3, 5 ];
    let n = arr.length;

    document.write(findDistinct(arr, n));

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*