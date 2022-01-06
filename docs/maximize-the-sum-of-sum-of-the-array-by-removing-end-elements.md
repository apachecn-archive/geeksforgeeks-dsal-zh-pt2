# 通过移除末端元素

最大化数组总和

> 原文:[https://www . geesforgeks . org/通过移除结束元素来最大化数组的总和/](https://www.geeksforgeeks.org/maximize-the-sum-of-sum-of-the-array-by-removing-end-elements/)

给定一个大小为 **N** 的数组 **arr** ，任务是通过移除结束元素来最大化数组中剩余元素的和。
**例:**

> **输入:** arr[] = {2，3}
> **输出:** 3
> **解释:**
> 首先我们会删除 2，然后剩余元素之和= 3。然后删除 3。因此和之和= 3 + 0 = 3。
> 我们也可以先删除 3 再删除 2，但是在这种情况下，sum = 2 + 0 = 2 的和
> 但是由于 3 比较大，因此输出为 3。
> **输入:** arr[] = {3，1，7，2，1}
> **输出:** 39
> **解释** :
> 首先我们将从最后一个中删除 1，然后剩余元素的总和
> 将为 13。
> 那么从最后删除 2，那么剩余元素的和就是 11。
> 那么从开头删除 3，那么剩余元素的和就是 8。
> 然后我们删除 1，剩下的和是 7 然后删除 7。
> 因此所有剩余和的和为 13 + 11 + 8 + 7 = 39，这是最大情况。

**方法:**思路是用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决这个问题。

1.  首先要计算数组的总和。
2.  然后比较两端的元素，从总和中减去两者之间的最小值。这将使剩余金额最大。
3.  然后，将剩余的总和加到结果中。
4.  重复以上步骤，直到所有元素都从数组中移除。然后打印结果总和。

以下是上述方法的实现:

## C++

```
// C++ program to maximize the sum
// of sum of the Array by
// removing end elements

#include <iostream>
using namespace std;

// Function to find
// the maximum sum of sum
int maxRemainingSum(int arr[], int n)
{
    int sum = 0;

    // compute the sum of whole array
    for (int i = 0; i < n; i++)
        sum += arr[i];

    int i = 0;
    int j = n - 1;

    int result = 0;

    // Traverse and remove the
    // minimum value from an end
    // to maximum the sum value
    while (i < j) {

        // If the left end element
        // is smaller than right end
        if (arr[i] < arr[j]) {

            // remove the left end element
            sum -= arr[i];

            i++;
        }

        // If the right end element
        // is smaller than left end
        else {

            // remove the right end element
            sum -= arr[j];
            j--;
        }

        // Add the remaining element
        // sum in the result
        result += sum;
    }

    // Return the maximum
    // sum of sum
    return result;
}

// Driver code
int main()
{
    int arr[] = { 3, 1, 7, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << maxRemainingSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximize the sum
// of sum of the Array by removing
// end elements
import java.util.*;

class GFG{

// Function to find
// the maximum sum of sum
static int maxRemainingSum(int arr[], int n)
{
    int sum = 0;

    // Compute the sum of whole array
    for(int i = 0; i < n; i++)
        sum += arr[i];

    int i = 0;
    int j = n - 1;
    int result = 0;

    // Traverse and remove the
    // minimum value from an end
    // to maximum the sum value
    while (i < j)
    {

        // If the left end element
        // is smaller than right end
        if (arr[i] < arr[j])
        {

            // Remove the left end element
            sum -= arr[i];
            i++;
        }

        // If the right end element
        // is smaller than left end
        else
        {

            // Remove the right end element
            sum -= arr[j];
            j--;
        }

        // Add the remaining element
        // sum in the result
        result += sum;
    }

    // Return the maximum
    // sum of sum
    return result;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 3, 1, 7, 2, 1 };
    int N = arr.length;

    System.out.println(maxRemainingSum(arr, N));
}
}

// This code is contributed by ankitkumar34
```

## 蟒蛇 3

```
# Python3 program to maximize the
# sum of sum of the Array by
# removing end elements

# Function to find the maximum
# sum of sum
def maxRemainingSum(arr, n):

    sum = 0

    # Compute the sum of whole array
    for i in range(n):
        sum += arr[i]

    i = 0
    j = n - 1

    result = 0

    # Traverse and remove the
    # minimum value from an end
    # to maximum the sum value
    while (i < j):

        # If the left end element
        # is smaller than right end
        if (arr[i] < arr[j]):

            # Remove the left end element
            sum -= arr[i]
            i += 1

        # If the right end element
        # is smaller than left end
        else:

            # Remove the right end element
            sum -= arr[j]
            j -= 1

        # Add the remaining element
        # sum in the result
        result += sum;

    # Return the maximum
    # sum of sum
    return result

# Driver code
arr = [ 3, 1, 7, 2, 1 ]
N = len(arr)

print(maxRemainingSum(arr, N))

# This code is contributed by ankitkumar34
```

## C#

```
// C# program to maximize the sum
// of sum of the Array by removing
// end elements
using System;

class GFG{

// Function to find
// the maximum sum of sum
static int maxRemainingSum(int[] arr, int n)
{
    int i, sum = 0;

    // Compute the sum of whole array
    for(i = 0; i < n; i++)
        sum += arr[i];

    i = 0;
    int j = n - 1;
    int result = 0;

    // Traverse and remove the
    // minimum value from an end
    // to maximum the sum value
    while (i < j)
    {

        // If the left end element
        // is smaller than right end
        if (arr[i] < arr[j])
        {

            // Remove the left end element
            sum -= arr[i];
            i++;
        }

        // If the right end element
        // is smaller than left end
        else
        {

            // Remove the right end element
            sum -= arr[j];
            j--;
        }

        // Add the remaining element
        // sum in the result
        result += sum;
    }

    // Return the maximum
    // sum of sum
    return result;
}

// Driver code
public static void Main()
{
    int[] arr = { 3, 1, 7, 2, 1 };
    int N = arr.Length;

    Console.Write(maxRemainingSum(arr, N));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript program to maximize the sum
// of sum of the Array by
// removing end elements

// Function to find
// the maximum sum of sum
function maxRemainingSum(arr, n)
{
    var sum = 0;

    // compute the sum of whole array
    for (var i = 0; i < n; i++)
        sum += arr[i];

    var i = 0;
    var j = n - 1;

    var result = 0;

    // Traverse and remove the
    // minimum value from an end
    // to maximum the sum value
    while (i < j) {

        // If the left end element
        // is smaller than right end
        if (arr[i] < arr[j]) {

            // remove the left end element
            sum -= arr[i];

            i++;
        }

        // If the right end element
        // is smaller than left end
        else {

            // remove the right end element
            sum -= arr[j];
            j--;
        }

        // Add the remaining element
        // sum in the result
        result += sum;
    }

    // Return the maximum
    // sum of sum
    return result;
}

// Driver code
var arr = [ 3, 1, 7, 2, 1 ];
var N = arr.length;
document.write( maxRemainingSum(arr, N));

</script>
```

**Output:** 

```
39
```

***时间复杂度:**O(N)*T4】