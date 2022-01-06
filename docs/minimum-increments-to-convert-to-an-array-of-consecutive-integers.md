# 转换为连续整数数组的最小增量

> 原文:[https://www . geeksforgeeks . org/最小增量转换为连续整数数组/](https://www.geeksforgeeks.org/minimum-increments-to-convert-to-an-array-of-consecutive-integers/)

给定一个带有 **N** 元素的数组**arr【】**，任务是找到所需的最小运算次数，从而实现带有数组元素的算术级数，其公共差为 1。在单个操作中，任何元素都可以增加 1。
**例:**

> **输入:** arr[] = {4，4，5，5，7}
> **输出:** 5
> 期望的数组是{4，5，6，7，8}，
> 可以通过最少的操作实现。
> **输入:** arr[] = {11，2，5，6}
> **输出:** 26
> 由于只允许做增量，我们
> 将数组改为{11，12，13，14}

**进场:**

*   我们可以利用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来解决这个问题。
*   我们将使用固定的最后一个元素构建所需的数组，如果解决方案无效，该元素将增加，如果有效，该元素将减少，就像在二分搜索法一样。
*   检查所需数组的所有元素是否大于或等于输入数组，以便对元素执行操作，使它们等于所需元素。计算运算次数。
*   找到满足所需数组中所有元素条件的最后一个元素的最小可能值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that return true if the
// required array can be generated
// with m as the last element
bool check(int m, int n, int arr[])
{
    // Build the desired array
    int desired[n];
    for (int i = n - 1; i >= 0; i--) {
        desired[i] = m;
        m--;
    }

    // Check if the given array can
    // be converted to the desired array
    // with the given operation
    for (int i = 0; i < n; i++) {
        if (arr[i] > desired[i] || desired[i] < 1) {
            return false;
        }
    }

    return true;
}

// Function to return the minimum number
// of operations required to convert the
// given array to an increasing AP series
// with common difference as 1
int minOperations(int arr[], int n)
{
    int start = (int)arr[n - 1];
    int end = *(max_element(arr, arr + n)) + n;
    int max_arr = 0;

    // Apply Binary Search
    while (start <= end) {
        int mid = (start + end) / 2;

        // If array can be generated with
        // mid as the last element
        if (check(mid, n, arr)) {

            // Current ans is mid
            max_arr = mid;

            // Check whether the same can be
            // achieved with even less operations
            end = mid - 1;
        }
        else {
            start = mid + 1;
        }
    }

    // Build the desired array
    int desired[n];
    for (int i = n - 1; i >= 0; i--) {
        desired[i] = max_arr;
        max_arr--;
    }

    // Calculate the number of
    // operations required
    int operations = 0;
    for (int i = 0; i < n; i++) {
        operations += (desired[i] - arr[i]);
    }

    // Return the number of
    // operations required
    return operations;
}

// Driver code
int main()
{
    int arr[] = { 4, 4, 5, 5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minOperations(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

    // Function that return true if the
    // required array can be generated
    // with m as the last element
    static boolean check(int m, int n, int arr[])
    {
        // Build the desired array
        int[] desired = new int[n];
        for (int i = n - 1; i >= 0; i--)
        {
            desired[i] = m;
            m--;
        }

        // Check if the given array can
        // be converted to the desired array
        // with the given operation
        for (int i = 0; i < n; i++)
        {
            if (arr[i] > desired[i] || desired[i] < 1)
            {
                return false;
            }
        }

        return true;
    }

    // Function to return the minimum number
    // of operations required to convert the
    // given array to an increasing AP series
    // with common difference as 1
    static int minOperations(int arr[], int n)
    {
        int start = (int) arr[n - 1];
        int end = Arrays.stream(arr).max().getAsInt() + n;
        int max_arr = 0;

        // Apply Binary Search
        while (start <= end)
        {
            int mid = (start + end) / 2;

            // If array can be generated with
            // mid as the last element
            if (check(mid, n, arr))
            {

                // Current ans is mid
                max_arr = mid;

                // Check whether the same can be
                // achieved with even less operations
                end = mid - 1;
            }
            else
            {
                start = mid + 1;
            }
        }

        // Build the desired array
        int[] desired = new int[n];
        for (int i = n - 1; i >= 0; i--)
        {
            desired[i] = max_arr;
            max_arr--;
        }

        // Calculate the number of
        // operations required
        int operations = 0;
        for (int i = 0; i < n; i++)
        {
            operations += (desired[i] - arr[i]);
        }

        // Return the number of
        // operations required
        return operations;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {4, 4, 5, 5, 7};
        int n = arr.length;

        System.out.println(minOperations(arr, n));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that return true if the
# required array can be generated
# with m as the last element
def check( m, n, arr) :

    # Build the desired array
    desired = [0]*n;
    for i in range(n-1,-1,-1) :
        desired[i] = m;
        m -= 1;

    # Check if the given array can
    # be converted to the desired array
    # with the given operation
    for i in range(n) :
        if (arr[i] > desired[i] or desired[i] < 1) :
            return False;

    return True

# Function to return the minimum number
# of operations required to convert the
# given array to an increasing AP series
# with common difference as 1
def minOperations(arr, n) :

    start = arr[n - 1];
    end = max(arr) + n;
    max_arr = 0;

    # Apply Binary Search
    while (start <= end) :
        mid = (start + end) // 2;

        # If array can be generated with
        # mid as the last element
        if (check(mid, n, arr)) :

            # Current ans is mid
            max_arr = mid;

            # Check whether the same can be
            # achieved with even less operations
            end = mid - 1;

        else :
            start = mid + 1;

    # Build the desired array
    desired = [0]* n;
    for i in range(n-1, -1,-1) :
        desired[i] = max_arr;
        max_arr -= 1;

    # Calculate the number of
    # operations required
    operations = 0;
    for i in range(n) :
        operations += (desired[i] - arr[i]);

    # Return the number of
    # operations required
    return operations;

# Driver code
if __name__ == "__main__" :

    arr = [ 4, 4, 5, 5, 7 ];
    n = len(arr);

    print(minOperations(arr, n));

    # This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;    
using System.Linq;

class GFG
{

    // Function that return true if the
    // required array can be generated
    // with m as the last element
    static Boolean check(int m, int n, int []arr)
    {
        // Build the desired array
        int[] desired = new int[n];
        for (int i = n - 1; i >= 0; i--)
        {
            desired[i] = m;
            m--;
        }

        // Check if the given array can
        // be converted to the desired array
        // with the given operation
        for (int i = 0; i < n; i++)
        {
            if (arr[i] > desired[i] || desired[i] < 1)
            {
                return false;
            }
        }

        return true;
    }

    // Function to return the minimum number
    // of operations required to convert the
    // given array to an increasing AP series
    // with common difference as 1
    static int minOperations(int []arr, int n)
    {
        int start = (int) arr[n - 1];
        int end = arr.Max() + n;
        int max_arr = 0;

        // Apply Binary Search
        while (start <= end)
        {
            int mid = (start + end) / 2;

            // If array can be generated with
            // mid as the last element
            if (check(mid, n, arr))
            {

                // Current ans is mid
                max_arr = mid;

                // Check whether the same can be
                // achieved with even less operations
                end = mid - 1;
            }
            else
            {
                start = mid + 1;
            }
        }

        // Build the desired array
        int[] desired = new int[n];
        for (int i = n - 1; i >= 0; i--)
        {
            desired[i] = max_arr;
            max_arr--;
        }

        // Calculate the number of
        // operations required
        int operations = 0;
        for (int i = 0; i < n; i++)
        {
            operations += (desired[i] - arr[i]);
        }

        // Return the number of
        // operations required
        return operations;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {4, 4, 5, 5, 7};
        int n = arr.Length;

        Console.WriteLine(minOperations(arr, n));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that return true if the
// required array can be generated
// with m as the last element
function check(m, n, arr)
{
    // Build the desired array
    var desired = Array(n);
    for (var i = n - 1; i >= 0; i--) {
        desired[i] = m;
        m--;
    }

    // Check if the given array can
    // be converted to the desired array
    // with the given operation
    for (var i = 0; i < n; i++) {
        if (arr[i] > desired[i] || desired[i] < 1) {
            return false;
        }
    }

    return true;
}

// Function to return the minimum number
// of operations required to convert the
// given array to an increasing AP series
// with common difference as 1
function minOperations(arr, n)
{
    var start = arr[n - 1];
    var end = arr.reduce((a,b)=> Math.max(a,b)) + n;
    var max_arr = 0;

    // Apply Binary Search
    while (start <= end) {
        var mid = parseInt((start + end) / 2);

        // If array can be generated with
        // mid as the last element
        if (check(mid, n, arr)) {

            // Current ans is mid
            max_arr = mid;

            // Check whether the same can be
            // achieved with even less operations
            end = mid - 1;
        }
        else {
            start = mid + 1;
        }
    }

    // Build the desired array
    var desired = Array(n);
    for (var i = n - 1; i >= 0; i--) {
        desired[i] = max_arr;
        max_arr--;
    }

    // Calculate the number of
    // operations required
    var operations = 0;
    for (var i = 0; i < n; i++) {
        operations += (desired[i] - arr[i]);
    }

    // Return the number of
    // operations required
    return operations;
}

// Driver code
var arr = [4, 4, 5, 5, 7 ];
var n = arr.length;
document.write( minOperations(arr, n));

</script>
```

**Output:** 

```
5
```