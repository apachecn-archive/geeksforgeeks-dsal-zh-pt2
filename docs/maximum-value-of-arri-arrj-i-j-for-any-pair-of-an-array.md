# 数组任意一对的 arr[I]+arr[j]+I–j 的最大值

> 原文:[https://www . geeksforgeeks . org/arri-arrj-I-j-for-any-pair-of-a-array/](https://www.geeksforgeeks.org/maximum-value-of-arri-arrj-i-j-for-any-pair-of-an-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是为给定数组的任何可能的对 **(i，j)** 找到**(arr[I]+arr[j]+I-j)**的最大值。

**示例:**

> **输入:** arr[] = {1，9，3，6，5}
> **输出:** 13
> **解释:**
> 数组中最大值为(arr[I]+arr[j]+I-j)的对为(1，3)。该值为(arr[1]+arr[3]+1–3)=(9+6+1–3)= 13。
> 
> **输入:** arr[] = {6，2，5，6}
> **输出:** 10

**天真方法:**解决给定问题最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)的所有可能对(I，j)，并在所有可能对中找到表达式的最大值。

下面是上述方法的实现:

## C++

```
// C++ program to for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value of
// arr[i] + arr[j] + i - j over all pairs
void maximumValue(int arr[], int n)
{
    // Stores the required result
    int ans = 0;

    // Traverse over all the pairs (i, j)
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Calculate the value of the
            // expression and update the
            // overall maximum value
            ans = max(ans, arr[i] + arr[j]
                               + i - j);
        }
    }

    // Print the result
    cout << ans;
}

// Driven Code
int main()
{
    int arr[] = { 1, 9, 3, 6, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    maximumValue(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the maximum value of
// arr[i] + arr[j] + i - j over all pairs
static void maximumValue(int arr[], int n)
{

    // Stores the required result
    int ans = 0;

    // Traverse over all the pairs (i, j)
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Calculate the value of the
            // expression and update the
            // overall maximum value
            ans = Math.max(ans,
                           arr[i] + arr[j] + i - j);
        }
    }

    // Print the result
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 9, 3, 6, 5 };
    int N = arr.length;

    maximumValue(arr, N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum value of
# arr[i] + arr[j] + i - j over all pairs
def maximumValue(arr, n):

    # Stores the required result
    ans = 0

    # Traverse over all the pairs (i, j)
    for i in range(n):
        for j in range(i + 1, n):

            # Calculate the value of the
            # expression and update the
            # overall maximum value
            ans = max(ans, arr[i] + arr[j] + i - j)

    print(ans)

# Driver Code
arr = [ 1, 9, 3, 6, 5 ]
N = len(arr)

maximumValue(arr, N)

# This code is contributed by abhinavjain194
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum value of
// arr[i] + arr[j] + i - j over all pairs
static void maximumValue(int[] arr, int n)
{

    // Stores the required result
    int ans = 0;

    // Traverse over all the pairs (i, j)
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Calculate the value of the
            // expression and update the
            // overall maximum value
            ans = Math.Max(ans, arr[i] + arr[j] + i - j);
        }
    }

    // Print the result
    Console.Write(ans);
}

// Driver code
static void Main()
{
    int[]  arr = { 1, 9, 3, 6, 5 };
    int N = arr.Length;

    maximumValue(arr, N);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// Javascript program to for the above approach
var arr = [ 1, 9, 3, 6, 5 ];

// Function to find the maximum value of
// arr[i] + arr[j] + i - j over all pairs
function maximumValue(arr, n)
{
    // Stores the required result
    var ans = 0;

    // Traversing over all the pairs (i, j)
    for(i = 0; i < n; i++)
    {
        for(j = i + 1; j < n; j++)
        {

            // Calculate the value of the
            // expression and update the
            // overall maximum value
            ans = Math.max(ans, arr[i] + arr[j] + i - j);

         }
    }

    // Print the result
    document.write(ans);
}

// Driver code
n = arr.length
maximumValue(arr, n);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
13
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过将表达式**(arr[I]+arr[j]+I–j)**分成两部分来优化: **(arr[i] + i)** 和**(arr[j]–j)**然后将 **(arr[i] + i)** 的最大值与**(arr[I]–I)**的所有可能值之和最大化。按照以下步骤解决问题 [:](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)

*   初始化两个变量，**用 **0** 重置**以存储所需的总和，**用**重置**以跟踪 **(arr[i] + i)** 的最大值。**
*   [使用变量 **i** 在范围**【1，N–1】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   将表达式的值存储在 **X** 中作为**(最大值+arr[I]–I)**。
    *   如果 **X** 的值大于 **res** ，则将 **res** 的值更新为 **X** 。
    *   如果 **arr[i] + i** 的值大于**最大值**，则更新**最大值**为 **(arr[i] + i)** 。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value
// of (arr[i] + arr[j] + i - j)
// possible for a pair in the array
void maximumValue(int arr[], int n)
{
    // Stores the maximum value
    // of(arr[i] + i)
    int maxvalue = arr[0];

    // Stores the required result
    int result = 0;

    // Traverse the array arr[]
    for (int i = 1; i < n; i++) {

        // Calculate for current pair
        // and update maximum value
        result = max(result,
                     maxvalue + arr[i] - i);

        // Update maxValue if (arr[i] + I)
        // is greater than maxValue
        maxvalue = max(maxvalue, arr[i] + i);
    }

    // Print the result
    cout << result;
}

// Driven Code
int main()
{
    int arr[] = { 1, 9, 3, 6, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    maximumValue(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the maximum value
// of (arr[i] + arr[j] + i - j)
// possible for a pair in the array
static void maximumValue(int arr[], int n)
{

    // Stores the maximum value
    // of(arr[i] + i)
    int maxvalue = arr[0];

    // Stores the required result
    int result = 0;

    // Traverse the array arr[]
    for(int i = 1; i < n; i++)
    {

        // Calculate for current pair
        // and update maximum value
        result = Math.max(result,
                          maxvalue + arr[i] - i);

        // Update maxValue if (arr[i] + I)
        // is greater than maxValue
        maxvalue = Math.max(maxvalue, arr[i] + i);
    }

    // Print the result
    System.out.println(result);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 9, 3, 6, 5 };
    int N = arr.length;

    maximumValue(arr, N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum value
# of (arr[i] + arr[j] + i - j)
# possible for a pair in the array
def maximumValue(arr, n):

     # Stores the maximum value
    # of(arr[i] + i)
    maxvalue = arr[0]

    # Stores the required result
    result = 0

    # Traverse the array arr[]
    for  i in range(1, n):

        # Calculate for current pair
        # and update maximum value
        result = max(result, maxvalue + arr[i] - i)

        # Update maxValue if (arr[i] + I)
        # is greater than maxValue
        maxvalue = max(maxvalue, arr[i] + i)

    print(result)

# Driver code      
arr = [ 1, 9, 3, 6, 5 ]
N = len(arr)

maximumValue(arr, N)

# This code is contributed by abhinavjain194
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum value of
// arr[i] + arr[j] + i - j over all pairs
static void maximumValue(int[] arr, int n)
{

    // Stores the maximum value
    // of(arr[i] + i)
    int maxvalue = arr[0];

    // Stores the required result
    int result = 0;

    // Traverse the array arr[]
    for(int i = 1; i < n; i++)
    {

        // Calculate for current pair
        // and update maximum value
        result = Math.Max(result,
                          maxvalue + arr[i] - i);

        // Update maxValue if (arr[i] + I)
        // is greater than maxValue
        maxvalue = Math.Max(maxvalue, arr[i] + i);
    }

    // Print the result
    Console.Write(result);
}

// Driver code
static void Main()
{
    int[] arr = { 1, 9, 3, 6, 5 };
    int N = arr.Length;

    maximumValue(arr, N);
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

// Javascript program for the above approach   

// Function to find the maximum value
    // of (arr[i] + arr[j] + i - j)
    // possible for a pair in the array
    function maximumValue(arr , n)
    {

        // Stores the maximum value
        // of(arr[i] + i)
        var maxvalue = arr[0];

        // Stores the required result
        var result = 0;

        // Traverse the array arr
        for (i = 1; i < n; i++) {

            // Calculate for current pair
            // and update maximum value
            result = Math.max(result, maxvalue + arr[i] - i);

            // Update maxValue if (arr[i] + I)
            // is greater than maxValue
            maxvalue = Math.max(maxvalue, arr[i] + i);
        }

        // Print the result
        document.write(result);
    }

    // Driver Code

        var arr = [ 1, 9, 3, 6, 5 ];
        var N = arr.length;

        maximumValue(arr, N);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
13
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)