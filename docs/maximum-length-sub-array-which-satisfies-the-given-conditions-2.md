# 满足给定条件的最大长度子阵列

> 原文:[https://www . geesforgeks . org/最大长度-满足给定条件的子数组-2/](https://www.geeksforgeeks.org/maximum-length-sub-array-which-satisfies-the-given-conditions-2/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出满足给定条件之一的 **arr[]** 的任意子数组的最大长度:

1.  子阵列正在严格增加。
2.  子阵列正在严格减少。
3.  子阵列首先严格增加，然后严格减少。

**示例:**

> **输入:** arr[] = {1，2，2，1，3}
> **输出:** 2
> {1，2}、{2，1}和{1，3}是有效的子阵。
> 
> **输入:** arr[] = {5，4，3，2，1，2，3，4}
> **输出:** 5
> {5，4，3，2，1}为所需子阵。

**方法:**创建一个数组**激励[]** ，其中**激励[i]** 将存储给定数组中最大的递增子数组的长度，以索引 **i** 结束。同样，创建另一个数组 **decStarting[]** ，其中 **decStarting[i]** 将存储从索引 **i** 开始的给定数组的最大递减子数组的长度。现在开始遍历原始数组，对于每个元素，假设它是所需子数组的中间，那么最大的所需子数组的长度，其在索引 **i** 处的中间将是**激励【I】+decStarting【I】–1**。**注意**减去 **1** ，因为**arr【I】**将对递增和递减子阵列进行两次计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the largest
// required sub-array
int largestSubArr(int arr[], int n)
{

    // incEnding[i] will store the length
    // of the largest increasing subarray
    // ending at arr[i]
    int incEnding[n] = { 0 };
    incEnding[0] = 1;
    for (int i = 1; i < n; i++) {

        // If current element is greater than
        // the previous element then it
        // can be a part of the previous
        // increasing subarray
        if (arr[i - 1] < arr[i])
            incEnding[i] = incEnding[i - 1] + 1;
        else
            incEnding[i] = 1;
    }

    // decStarting[i] will store the length
    // of the largest decreasing subarray
    // starting at arr[i]
    int decStarting[n] = { 0 };
    decStarting[n - 1] = 1;
    for (int i = n - 2; i >= 0; i--) {

        // If current element is greater than
        // the next element then it can be a part
        // of the decreasing subarray
        // with the next element
        if (arr[i + 1] < arr[i])
            decStarting[i] = decStarting[i + 1] + 1;
        else
            decStarting[i] = 1;
    }

    // To store the length of the
    // maximum required subarray
    int maxSubArr = 0;

    // Assume every element to be the mid
    // point of the required array
    for (int i = 0; i < n; i++) {

        // 1 has to be subtracted because the
        // current element will be counted for
        // both the increasing and
        // the decreasing subarray
        maxSubArr = max(maxSubArr, incEnding[i]
                                       + decStarting[i] - 1);
    }

    return maxSubArr;
}

// Driver code
int main()
{

    int arr[] = { 1, 2, 2, 1, 3 };
    int n = sizeof(arr) / sizeof(int);

    cout << largestSubArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

    // Function to return the largest
    // required sub-array
    static int largestSubArr(int arr[], int n)
    {

        // incEnding[i] will store the length
        // of the largest increasing subarray
        // ending at arr[i]
        int incEnding[] = new int[n];

        int i;
        for(i = 0; i < n ; i++)
            incEnding[i] = 0;

        incEnding[0] = 1;

        for (i = 1; i < n; i++)
        {

            // If current element is greater than
            // the previous element then it
            // can be a part of the previous
            // increasing subarray
            if (arr[i - 1] < arr[i])
                incEnding[i] = incEnding[i - 1] + 1;
            else
                incEnding[i] = 1;
        }

        // decStarting[i] will store the length
        // of the largest decreasing subarray
        // starting at arr[i]
        int decStarting[] = new int[n];

        for(i = 0; i < n ; i++)
            decStarting[i] = 0;

        decStarting[n - 1] = 1;

        for (i = n - 2; i >= 0; i--)
        {

            // If current element is greater than
            // the next element then it can be a part
            // of the decreasing subarray
            // with the next element
            if (arr[i + 1] < arr[i])
                decStarting[i] = decStarting[i + 1] + 1;
            else
                decStarting[i] = 1;
        }

        // To store the length of the
        // maximum required subarray
        int maxSubArr = 0;

        // Assume every element to be the mid
        // point of the required array
        for (i = 0; i < n; i++)
        {

            // 1 has to be subtracted because the
            // current element will be counted for
            // both the increasing and
            // the decreasing subarray
            maxSubArr = Math.max(maxSubArr, incEnding[i] +
                                            decStarting[i] - 1);
        }
        return maxSubArr;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 2, 1, 3 };
        int n = arr.length;

        System.out.println(largestSubArr(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the largest
# required sub-array
def largestSubArr(arr, n) :

    # incEnding[i] will store the length
    # of the largest increasing subarray
    # ending at arr[i]
    incEnding = [0] * n
    incEnding[0] = 1
    for i in range(1, n) :

        # If current element is greater than
        # the previous element then it
        # can be a part of the previous
        # increasing subarray
        if (arr[i - 1] < arr[i]) :
            incEnding[i] = incEnding[i - 1] + 1
        else :
            incEnding[i] = 1

    # decStarting[i] will store the length
    # of the largest decreasing subarray
    # starting at arr[i]
    decStarting = [0] * n
    decStarting[n - 1] = 1
    for i in range(n - 2, -1, -1):

        # If current element is greater than
        # the next element then it can be a part
        # of the decreasing subarray
        # with the next element
        if (arr[i + 1] < arr[i]) :
            decStarting[i] = decStarting[i + 1] + 1
        else :
            decStarting[i] = 1

    # To store the length of the
    # maximum required subarray
    maxSubArr = 0

    # Assume every element to be the mid
    # point of the required array
    for i in range(n):

        # 1 has to be subtracted because the
        # current element will be counted for
        # both the increasing and
        # the decreasing subarray
        maxSubArr = max(maxSubArr, incEnding[i] +
                                 decStarting[i] - 1)

    return maxSubArr

# Driver code
arr = [ 1, 2, 2, 1, 3 ]
n = len(arr)

print(largestSubArr(arr, n))

# This code is contributed by
# divyamohan123
```

## C#

```
// C# implementation of the above approach
using System;        

class GFG
{

    // Function to return the largest
    // required sub-array
    static int largestSubArr(int []arr, int n)
    {

        // incEnding[i] will store the length
        // of the largest increasing subarray
        // ending at arr[i]
        int []incEnding = new int[n];

        int i;
        for(i = 0; i < n ; i++)
            incEnding[i] = 0;

        incEnding[0] = 1;

        for (i = 1; i < n; i++)
        {

            // If current element is greater than
            // the previous element then it
            // can be a part of the previous
            // increasing subarray
            if (arr[i - 1] < arr[i])
                incEnding[i] = incEnding[i - 1] + 1;
            else
                incEnding[i] = 1;
        }

        // decStarting[i] will store the length
        // of the largest decreasing subarray
        // starting at arr[i]
        int []decStarting = new int[n];

        for(i = 0; i < n ; i++)
            decStarting[i] = 0;

        decStarting[n - 1] = 1;

        for (i = n - 2; i >= 0; i--)
        {

            // If current element is greater than
            // the next element then it can be a part
            // of the decreasing subarray
            // with the next element
            if (arr[i + 1] < arr[i])
                decStarting[i] = decStarting[i + 1] + 1;
            else
                decStarting[i] = 1;
        }

        // To store the length of the
        // maximum required subarray
        int maxSubArr = 0;

        // Assume every element to be the mid
        // point of the required array
        for (i = 0; i < n; i++)
        {

            // 1 has to be subtracted because the
            // current element will be counted for
            // both the increasing and
            // the decreasing subarray
            maxSubArr = Math.Max(maxSubArr, incEnding[i] +
                                            decStarting[i] - 1);
        }
        return maxSubArr;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 1, 2, 2, 1, 3 };
        int n = arr.Length;

        Console.WriteLine(largestSubArr(arr, n));
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the largest
// required sub-array
function largestSubArr(arr, n)
{

    // incEnding[i] will store the length
    // of the largest increasing subarray
    // ending at arr[i]
    var incEnding = Array(n).fill(0);
    incEnding[0] = 1;

    for(var i = 1; i < n; i++)
    {

        // If current element is greater than
        // the previous element then it
        // can be a part of the previous
        // increasing subarray
        if (arr[i - 1] < arr[i])
            incEnding[i] = incEnding[i - 1] + 1;
        else
            incEnding[i] = 1;
    }

    // decStarting[i] will store the length
    // of the largest decreasing subarray
    // starting at arr[i]
    var decStarting = Array(n).fill(0);
    decStarting[n - 1] = 1;

    for(var i = n - 2; i >= 0; i--)
    {

        // If current element is greater than
        // the next element then it can be a part
        // of the decreasing subarray
        // with the next element
        if (arr[i + 1] < arr[i])
            decStarting[i] = decStarting[i + 1] + 1;
        else
            decStarting[i] = 1;
    }

    // To store the length of the
    // maximum required subarray
    var maxSubArr = 0;

    // Assume every element to be the mid
    // point of the required array
    for(var i = 0; i < n; i++)
    {

        // 1 has to be subtracted because the
        // current element will be counted for
        // both the increasing and
        // the decreasing subarray
        maxSubArr = Math.max(maxSubArr,
                             incEnding[i] +
                             decStarting[i] - 1);
    }
    return maxSubArr;
}

// Driver code
var arr = [ 1, 2, 2, 1, 3 ];
var n = arr.length;

document.write(largestSubArr(arr, n));

// This code is contributed by itsok

</script>
```

**Output:** 

```
2
```