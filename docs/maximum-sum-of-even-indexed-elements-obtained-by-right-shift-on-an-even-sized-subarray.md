# 在偶数大小的子阵列上通过右移获得的偶数索引元素的最大和

> 原文:[https://www . geeksforgeeks . org/偶数索引元素的最大和-通过在偶数大小的子数组上右移获得/](https://www.geeksforgeeks.org/maximum-sum-of-even-indexed-elements-obtained-by-right-shift-on-an-even-sized-subarray/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，我们需要找到偶数索引元素的最大和，通过对任意偶数长度的子数组执行 1 的右移位操作可以获得该元素的最大和。
**例:**

> **输入:** arr[] = {5，1，3，4，5，6}
> **输出:** 15
> **解释:**
> 我们可以对索引 2 到 5 执行右移，然后得到的数组是:
> arr[] = {5，1，6，3，4，5}
> 偶数索引处的元素之和= 5 + 6 + 4 = 15
> **输入:** arr[] = {7，9，1 12}
> **输出:** 39
> **解释:**
> 我们可以对索引 0 到 7 执行右移，然后得到的数组是:
> arr[] = {12，7，9，1，8，3，10，4}
> 偶数索引处的元素之和= 12 + 9 + 8 + 10 = 39

**朴素方法:**朴素方法是将每一个可能的偶数长度的子阵列右移 1，并为每一个可能的子阵列移位后形成的所有阵列找到偶数索引处的元素之和。所有数组中的最大和就是所需的结果。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效方法:**为了优化上述幼稚方法，我们可以观察到，在对任何偶数子阵列执行右移 1 之后，奇数索引值被偶数索引值替换，反之亦然。如果我们在移位前找到偶数索引处元素的和(比如 **sum** )，那么移位后的和会被偶数和奇数索引处元素之间的连续差之和所改变。
**例如:**

> arr[] = {1，2，3，4}
> 上述数组中偶数索引处的 sum 元素= 1 + 3 = 4
> 右移数组 1，我们有
> arr1[] = {4，1，2，3}
> 上述数组中偶数索引处的 Sum 元素= 4 + 2 = 6
> 因此，上述两个数组中的 Sum 元素相差 2，等于 arr[]中连续差的总和，为((2–1)+(4–3)= 2。

我们将使用上述概念来解决这个问题。以下是步骤:

1.  创建两个数组(比如 **arr1[]** 和 **arr2[]** )，使得 **arr1[]** 将数组 **arr[]** 中元素的连续差存储为:

```
{(a[1] – a[0]), (a[3] – a[2]), . . ., (a[n]-a[n-1])}
```

1.  **arr2[]** 将数组中元素的连续差 **arr[]** 存储为:

```
{(a[1] – a[2]), (a[3] – a[4]), . . ., (a[n-1]-a[n])}
```

2.  然后在上面形成的两个阵列中使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)找到最大子阵列和。
3.  现在最大和是原始数组中偶数索引处元素的和( **arr[]** ) +两个数组 **arr1[]** 和 **arr2[]** 的最大子数组和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Kadane's Algorithm to find
// the maximum sum sub array
int kadane(vector<int> v)
{
    int maxSoFar = 0;
    int maxEndingHere = 0;

    // Iterate array v
    for (int i = 0; i < v.size(); i++) {

        maxEndingHere += v[i];

        // Update the maximum
        maxSoFar = max(maxEndingHere,
                    maxSoFar);

        // Update maxEndingHere to 0 if it
        // is less than 0
        maxEndingHere
            = max(maxEndingHere, 0);
    }

    // Return maximum sum
    return maxSoFar;
}

// Function to find the sum
// of even indexed elements
// after modification in array.
int sumOfElements(int* arr, int n)
{
    int sum = 0;

    // Find initial sum of
    // even indexed elements
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0)
            sum += arr[i];
    }

    // Create two vectors to store
    // the consecutive differences
    // of elements
    vector<int> v1;
    vector<int> v2;

    for (int i = 1; i < n; i += 2) {

        v1.push_back(arr[i]
                    - arr[i - 1]);

        if (i + 1 < n) {
            v2.push_back(arr[i]
                        - arr[i + 1]);
        }
    }

    // Find the maximum sum subarray
    int option1 = kadane(v1);
    int option2 = kadane(v2);

    // Add the maximum value
    // to initial sum
    int ans = sum + max(option1,
                        option2);

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 5, 1, 3, 4, 5, 6 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << sumOfElements(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Kadane's Algorithm to find
// the maximum sum sub array
static int kadane(Vector<Integer> v)
{
    int maxSoFar = 0;
    int maxEndingHere = 0;

    // Iterate array v
    for(int i = 0; i < v.size(); i++)
    {
    maxEndingHere += v.get(i);

    // Update the maximum
    maxSoFar = Math.max(maxEndingHere,
                        maxSoFar);

    // Update maxEndingHere to 0 if it
    // is less than 0
    maxEndingHere = Math.max(maxEndingHere, 0);
    }

    // Return maximum sum
    return maxSoFar;
}

// Function to find the sum
// of even indexed elements
// after modification in array.
static int sumOfElements(int []arr, int n)
{
    int sum = 0;

    // Find initial sum of
    // even indexed elements
    for(int i = 0; i < n; i++)
    {
    if (i % 2 == 0)
        sum += arr[i];
    }

    // Create two vectors to store
    // the consecutive differences
    // of elements
    Vector<Integer> v1 = new Vector<Integer>();
    Vector<Integer> v2 = new Vector<Integer>();

    for(int i = 1; i < n; i += 2)
    {
    v1.add(arr[i] - arr[i - 1]);

    if (i + 1 < n)
    {
        v2.add(arr[i] - arr[i + 1]);
    }
    }

    // Find the maximum sum subarray
    int option1 = kadane(v1);
    int option2 = kadane(v2);

    // Add the maximum value
    // to initial sum
    int ans = sum + Math.max(option1,
                            option2);

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 5, 1, 3, 4, 5, 6 };

    int N = arr.length;

    // Function Call
    System.out.print(sumOfElements(arr, N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Kadane's Algorithm to find
# the maximum sum sub array
def kadane(v):

    maxSoFar = 0;
    maxEndingHere = 0;

    # Iterate array v
    for i in range(len(v)):
        maxEndingHere += v[i];

        # Update the maximum
        maxSoFar = max(maxEndingHere,
                    maxSoFar);

        # Update maxEndingHere to 0
        # if it is less than 0
        maxEndingHere = max(maxEndingHere, 0);

    # Return maximum sum
    return maxSoFar;

# Function to find the sum
# of even indexed elements
# after modification in array.
def sumOfElements(arr, n):

    sum = 0;

    # Find initial sum of
    # even indexed elements
    for i in range(n):
        if (i % 2 == 0):
            sum += arr[i];

    # Create two vectors to store
    # the consecutive differences
    # of elements
    v1 = [];
    v2 = [];

    for i in range(1, n, 2):
        v1.append(arr[i] - arr[i - 1]);

        if (i + 1 < n):
            v2.append(arr[i] - arr[i + 1]);

    # Find the maximum sum subarray
    option1 = kadane(v1);
    option2 = kadane(v2);

    # Add the maximum value
    # to initial sum
    ans = sum + max(option1, option2);

    # Return the answer
    return ans;

# Driver Code
if __name__ == "__main__" :

    # Given array arr[]
    arr = [ 5, 1, 3, 4, 5, 6 ];

    N = len(arr);

    # Function call
    print(sumOfElements(arr, N));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Kadane's Algorithm to find
// the maximum sum sub array
static int kadane(List<int> v)
{
    int maxSoFar = 0;
    int maxEndingHere = 0;

    // Iterate array v
    for(int i = 0; i < v.Count; i++)
    {
        maxEndingHere += v[i];

        // Update the maximum
        maxSoFar = Math.Max(maxEndingHere,
                            maxSoFar);

        // Update maxEndingHere to 0 if it
        // is less than 0
        maxEndingHere = Math.Max(maxEndingHere, 0);
    }

    // Return maximum sum
    return maxSoFar;
}

// Function to find the sum
// of even indexed elements
// after modification in array.
static int sumOfElements(int []arr, int n)
{
    int sum = 0;

    // Find initial sum of
    // even indexed elements
    for(int i = 0; i < n; i++)
    {
        if (i % 2 == 0)
            sum += arr[i];
    }

    // Create two vectors to store
    // the consecutive differences
    // of elements
    List<int> v1 = new List<int>();
    List<int> v2 = new List<int>();

    for(int i = 1; i < n; i += 2)
    {
        v1.Add(arr[i] - arr[i - 1]);

        if (i + 1 < n)
        {
            v2.Add(arr[i] - arr[i + 1]);
        }
    }

    // Find the maximum sum subarray
    int option1 = kadane(v1);
    int option2 = kadane(v2);

    // Add the maximum value
    // to initial sum
    int ans = sum + Math.Max(option1,
                             option2);

    // Return the answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 5, 1, 3, 4, 5, 6 };

    int N = arr.Length;

    // Function call
    Console.Write(sumOfElements(arr, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Kadane's Algorithm to find
// the maximum sum sub array
function kadane(v)
{
    var maxSoFar = 0;
    var maxEndingHere = 0;

    // Iterate array v
    for (var i = 0; i < v.length; i++) {

        maxEndingHere += v[i];

        // Update the maximum
        maxSoFar = Math.max(maxEndingHere,maxSoFar);

        // Update maxEndingHere to 0 if it
        // is less than 0
        maxEndingHere = Math.max(maxEndingHere, 0);
    }

    // Return maximum sum
    return maxSoFar;
}

// Function to find the sum
// of even indexed elements
// after modification in array.
function sumOfElements(arr, n)
{
    var sum = 0;

    // Find initial sum of
    // even indexed elements
    for (var i = 0; i < n; i++) {
        if (i % 2 == 0)
            sum += arr[i];
    }

    // Create two vectors to store
    // the consecutive differences
    // of elements
    var v1 = [];
    var v2 = [];

    for (var i = 1; i < n; i += 2) {

        v1.push(arr[i] - arr[i - 1]);

        if (i + 1 < n) {
            v2.push(arr[i] - arr[i + 1]);
        }
    }

    // Find the maximum sum subarray
    var option1 = kadane(v1);
    var option2 = kadane(v2);

    // Add the maximum value
    // to initial sum
    var ans = sum + Math.max(option1,
                        option2);

    // Return the answer
    return ans;
}

var arr = [ 5, 1, 3, 4, 5, 6 ];

    var N = arr.length;

    // Function Call
    document.write(sumOfElements(arr, N));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
15
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*