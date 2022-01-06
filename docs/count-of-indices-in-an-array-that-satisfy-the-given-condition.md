# 满足给定条件的数组中索引的计数

> 原文:[https://www . geesforgeks . org/满足给定条件的数组中的索引数/](https://www.geeksforgeeks.org/count-of-indices-in-an-array-that-satisfy-the-given-condition/)

给定一个由 **N** 正整数组成的数组 **arr[]** ，任务是找到索引 **i** 的计数，使得从 **arr[0]** 到**arr[I–1]**的所有元素都小于 **arr[i]** 。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 4
> 所有指标满足给定条件。
> **输入:** arr[] = {4，3，2，1}
> **输出:** 1
> 只有 i = 0 才是有效索引。

**方法:**想法是从左到右遍历数组并跟踪当前最大值，每当这个最大值改变时，那么当前索引就是一个有效的索引，所以递增结果计数器。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of indices that satisfy
// the given condition
int countIndices(int arr[], int n)
{

    // To store the result
    int cnt = 0;

    // To store the current maximum
    // Initialized to 0 since there are only
    // positive elements in the array
    int max = 0;
    for (int i = 0; i < n; i++) {

        // i is a valid index
        if (max < arr[i]) {

            // Update the maximum so far
            max = arr[i];

            // Increment the counter
            cnt++;
        }
    }

    return cnt;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int n = sizeof(arr) / sizeof(int);

    cout << countIndices(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of indices that satisfy
// the given condition
static int countIndices(int arr[], int n)
{

    // To store the result
    int cnt = 0;

    // To store the current maximum
    // Initialized to 0 since there are only
    // positive elements in the array
    int max = 0;
    for (int i = 0; i < n; i++)
    {

        // i is a valid index
        if (max < arr[i])
        {

            // Update the maximum so far
            max = arr[i];

            // Increment the counter
            cnt++;
        }
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4 };
    int n = arr.length;

    System.out.println(countIndices(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the count
# of indices that satisfy
# the given condition
def countIndices(arr, n):

    # To store the result
    cnt = 0;

    # To store the current maximum
    # Initialized to 0 since there are only
    # positive elements in the array
    max = 0;
    for i in range(n):
        # i is a valid index
        if (max < arr[i]):

            # Update the maximum so far
            max = arr[i];

            # Increment the counter
            cnt += 1;

    return cnt;

# Driver code
if __name__ == '__main__':
    arr = [ 1, 2, 3, 4 ];
    n = len(arr);

    print(countIndices(arr, n));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of indices that satisfy
// the given condition
static int countIndices(int []arr, int n)
{

    // To store the result
    int cnt = 0;

    // To store the current maximum
    // Initialized to 0 since there are only
    // positive elements in the array
    int max = 0;
    for (int i = 0; i < n; i++)
    {

        // i is a valid index
        if (max < arr[i])
        {

            // Update the maximum so far
            max = arr[i];

            // Increment the counter
            cnt++;
        }
    }
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4 };
    int n = arr.Length;

    Console.WriteLine(countIndices(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the count
    // of indices that satisfy
    // the given condition
    function countIndices(arr , n) {

        // To store the result
        var cnt = 0;

        // To store the current maximum
        // Initialized to 0 since there are only
        // positive elements in the array
        var max = 0;
        for (i = 0; i < n; i++) {

            // i is a valid index
            if (max < arr[i]) {

                // Update the maximum so far
                max = arr[i];

                // Increment the counter
                cnt++;
            }
        }
        return cnt;
    }

    // Driver code

        var arr = [ 1, 2, 3, 4 ];
        var n = arr.length;

        document.write(countIndices(arr, n));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
4
```