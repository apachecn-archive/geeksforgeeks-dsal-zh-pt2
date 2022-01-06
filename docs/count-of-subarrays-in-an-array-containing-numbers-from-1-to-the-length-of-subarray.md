# 包含从 1 到子阵列长度的数的阵列中的子阵列的计数

> 原文:[https://www . geesforgeks . org/包含从 1 到子阵列长度的数字的阵列中的子阵列计数/](https://www.geeksforgeeks.org/count-of-subarrays-in-an-array-containing-numbers-from-1-to-the-length-of-subarray/)

给定一个长度为 N 的数组**arr【】**包含从 1 到 N 的所有元素，任务是找到包含从 1 到 M 的数字的子数组的数量，其中 M 是子数组的长度。

**示例:**

> **输入:** arr[] = {4，1，3，2，5，6}
> **输出:** 5
> **解释:**
> 所需子数组= { {4，1，3，2}，{1}，{1，3，2}，{4，1，3，2，5}，{4，1，3，2，5，6}，}
> 计数(子数组)= 5
> 
> **输入:** arr[] = {3，2，4，1}
> **输出:** 2
> **解释:**
> 所需子数组= { {1}，{3，2，4，1} }
> 计数(子数组)= 2

**天真方法:** [生成阵列的所有子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并检查每个子阵列是否包含子阵列长度的每个元素 1。

**有效方法:**创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，该向量按照排序顺序映射数组的每个元素及其索引。现在[迭代这个向量](https://www.geeksforgeeks.org/vector-iterator-method-in-java-with-examples/)并且检查直到 i <sup>第</sup>个元素的最大和最小索引的差是否小于到现在为止迭代的元素数量，这是 I 本身的值。

下面是上述方法的实现

## C++

```
// C++ Implementation to Count the no. of
// Sub-arrays which contains all elements
// from 1 to length of subarray

#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// Sub-arrays which contains all elements
// 1 to length of subarray
int countOfSubarrays(int* arr, int n)
{
    int count = 0;
    vector<int> v(n + 1);

    // Map all elements of array with their index
    for (int i = 0; i < n; i++)
        v[arr[i]] = i;

    // Set the max and min index equal to the
    // min and max value of integer respectively.
    int maximum = INT_MIN;
    int minimum = INT_MAX;

    for (int i = 1; i <= n; i++) {

        // Update the value of maximum index
        maximum = max(maximum, v[i]);

        // Update the value of minimum index
        minimum = min(minimum, v[i]);

        // Increase the counter if difference of
        // max. and min. index is less than the
        // elements iterated till now
        if (maximum - minimum < i)
            count = count + 1;
    }

    return count;
}

// Driver Function
int main()
{
    int arr[] = { 4, 1, 3, 2, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countOfSubarrays(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation to Count the no. of
// Sub-arrays which contains all elements
// from 1 to length of subarray
class GFG
{

// Function to count the number
// Sub-arrays which contains all elements
// 1 to length of subarray
static int countOfSubarrays(int []arr, int n)
{
    int count = 0;
    int []v = new int[n + 1];

    // Map all elements of array with their index
    for (int i = 0; i < n; i++)
        v[arr[i]] = i;

    // Set the max and min index equal to the
    // min and max value of integer respectively.
    int maximum = Integer.MIN_VALUE;
    int minimum = Integer.MAX_VALUE;

    for (int i = 1; i <= n; i++)
    {

        // Update the value of maximum index
        maximum = Math.max(maximum, v[i]);

        // Update the value of minimum index
        minimum = Math.min(minimum, v[i]);

        // Increase the counter if difference of
        // max. and min. index is less than the
        // elements iterated till now
        if (maximum - minimum < i)
            count = count + 1;
    }

    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 4, 1, 3, 2, 5, 6 };
    int n = arr.length;
    System.out.print(countOfSubarrays(arr, n) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 Implementation to Count the no. of
# Sub-arrays which contains all elements
# from 1 to length of subarray
import sys

INT_MAX = sys.maxsize;
INT_MIN = -(sys.maxsize - 1);

# Function to count the number
# Sub-arrays which contains all elements
# 1 to length of subarray
def countOfSubarrays(arr, n) :

    count = 0;
    v = [0]*(n + 1);

    # Map all elements of array with their index
    for i in range(n) :
        v[arr[i]] = i;

    # Set the max and min index equal to the
    # min and max value of integer respectively.
    maximum = INT_MIN;
    minimum = INT_MAX;

    for i in range(1, n + 1) :

        # Update the value of maximum index
        maximum = max(maximum, v[i]);

        # Update the value of minimum index
        minimum = min(minimum, v[i]);

        # Increase the counter if difference of
        # max. and min. index is less than the
        # elements iterated till now
        if (maximum - minimum < i) :
            count = count + 1;

    return count;

# Driver code
if __name__ == "__main__" :

    arr = [ 4, 1, 3, 2, 5, 6 ];
    n = len(arr);
    print(countOfSubarrays(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# Implementation to Count the no. of
// Sub-arrays which contains all elements
// from 1 to length of subarray
using System;

class GFG
{

// Function to count the number
// Sub-arrays which contains all elements
// 1 to length of subarray
static int countOfSubarrays(int []arr, int n)
{
    int count = 0;
    int []v = new int[n + 1];

    // Map all elements of array with their index
    for (int i = 0; i < n; i++)
        v[arr[i]] = i;

    // Set the max and min index equal to the
    // min and max value of integer respectively.
    int maximum = int.MinValue;
    int minimum = int.MaxValue;

    for (int i = 1; i <= n; i++)
    {

        // Update the value of maximum index
        maximum = Math.Max(maximum, v[i]);

        // Update the value of minimum index
        minimum = Math.Min(minimum, v[i]);

        // Increase the counter if difference of
        // max. and min. index is less than the
        // elements iterated till now
        if (maximum - minimum < i)
            count = count + 1;
    }

    return count;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 4, 1, 3, 2, 5, 6 };
    int n = arr.Length;
    Console.Write(countOfSubarrays(arr, n) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript Implementation to Count the no. of
// Sub-arrays which contains all elements
// from 1 to length of subarray

// Function to count the number
// Sub-arrays which contains all elements
// 1 to length of subarray
function countOfSubarrays(arr, n)
{
    var count = 0;
    var v = Array(n + 1);

    // Map all elements of array with their index
    for (var i = 0; i < n; i++)
        v[arr[i]] = i;

    // Set the max and min index equal to the
    // min and max value of integer respectively.
    var maximum = -1000000000;
    var minimum = 10000000000;

    for (var i = 1; i <= n; i++) {

        // Update the value of maximum index
        maximum = Math.max(maximum, v[i]);

        // Update the value of minimum index
        minimum = Math.min(minimum, v[i]);

        // Increase the counter if difference of
        // max. and min. index is less than the
        // elements iterated till now
        if (maximum - minimum < i)
            count = count + 1;
    }

    return count;
}

// Driver Function
var arr = [4, 1, 3, 2, 5, 6 ];
var n = arr.length;
document.write( countOfSubarrays(arr, n) );

// This code is contributed by importantly.
</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(N)