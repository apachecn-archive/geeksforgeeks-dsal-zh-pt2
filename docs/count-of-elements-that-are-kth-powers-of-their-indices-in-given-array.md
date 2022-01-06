# 给定数组中索引的第 k 次幂的元素计数

> 原文:[https://www . geeksforgeeks . org/给定数组中元素个数的 k 次方指数/](https://www.geeksforgeeks.org/count-of-elements-that-are-kth-powers-of-their-indices-in-given-array/)

给定一个带有非负整数的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】****N**，任务是找出其指数的 K 次幂的元素数，其中 K 是非负数。

> **arr[i] = i <sup>K</sup>**

**示例:**

> **输入:** arr = [1，1，4，3，16，125，1]，K = 0
> **输出:** 3
> **解释:** 3 个元素是其指数的 K 次幂:
> 0 <sup>0</sup> 是 1，1 <sup>0</sup> 是 1，6 <sup>0</sup> 是 1
> 
> **输入:** arr = [0，1，4，3]，K = 2
> **输出:** 2
> **说明:** 0 <sup>2</sup> 为 0，1 <sup>2</sup> 为 1，2 <sup>2</sup> 为 4

**方法:**给定的问题可以通过找到每个索引的第 k 次[幂](https://www.geeksforgeeks.org/powers-2-required-sum/)并检查它们是否等于该索引中存在的元素来解决。按照以下步骤解决问题:

*   将变量 **res** 初始化为 0，以存储答案
*   如果 K 的值为 0:
    *   如果数组中的第一个元素 **arr** 存在并且等于 1，那么将 **res** 增加 1
*   否则，如果 K 的值大于 0:
    *   如果数组中的第一个元素 **arr** 存在并且等于 0，那么将 **res** 增加 1
*   如果数组中的第二个元素 **arr** 存在并且等于 1，那么将 **res** 增加 1
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** 从索引 2 到结束，在每个索引:
    *   将变量 **indPow** 初始化为当前索引 **i** ，并将其乘以 **i，k-1** 次
    *   如果 **indPow** 的值等于当前元素**arr【I】**那么将 **res** 增加 1
*   返回 **res** 作为我们的答案

以下是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of elements which
// are a non-negative power of their indices
int indPowEqualsEle(vector<int> arr, int K)
{

    // Length of the array
    int len = arr.size();

    // Initialize variable res for
    // calculating the answer
    int res = 0;

    // If the value of K is 0
    if (K == 0)
    {

        // If the first element is 1
        // then the condition is sattisfied
        if (len > 0 && arr[0] == 1)
            res++;
    }

    // If the value of K > 0
    if (K > 0)
    {

        // If the first is 0 increment res
        if (len > 0 && arr[0] == 1)
            res++;
    }

    // If the second element is 1
    // then increment res
    if (len > 1 && arr[1] == 1)
        res++;

    // Iterate the array arr from index 2
    for (int i = 2; i < len; i++)
    {

        // Initialize a variable
        // to index which is to be
        // multiplied K-1 times
        long indPow = i;

        for (int j = 2; j < K; j++)
        {

            // Multiply current value
            // with index K - 1 times
            indPow *= i;
        }

        // If index power K is equal to
        // the element then increment res
        if (indPow == arr[i])
            res++;
    }

    // return the result
    return res;
}

// Driver function
int main()
{

    // Initialize an array
    vector<int> arr = {1, 1, 4, 3, 16, 125, 1};

    // Initialize power
    int K = 0;

    // Call the function
    // and print the answer
    cout << (indPowEqualsEle(arr, K));
    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to find count of elements which
    // are a non-negative power of their indices
    public static int
    indPowEqualsEle(int[] arr, int K)
    {

        // Length of the array
        int len = arr.length;

        // Initialize variable res for
        // calculating the answer
        int res = 0;

        // If the value of K is 0
        if (K == 0) {

            // If the first element is 1
            // then the condition is sattisfied
            if (len > 0 && arr[0] == 1)
                res++;
        }

        // If the value of K > 0
        if (K > 0) {

            // If the first is 0 increment res
            if (len > 0 && arr[0] == 1)
                res++;
        }

        // If the second element is 1
        // then increment res
        if (len > 1 && arr[1] == 1)
            res++;

        // Iterate the array arr from index 2
        for (int i = 2; i < len; i++) {

            // Initialize a variable
            // to index which is to be
            // multiplied K-1 times
            long indPow = i;

            for (int j = 2; j < K; j++) {

                // Multiply current value
                // with index K - 1 times
                indPow *= i;
            }

            // If index power K is equal to
            // the element then increment res
            if (indPow == arr[i])
                res++;
        }

        // return the result
        return res;
    }
    // Driver function
    public static void main(String[] args)
    {

        // Initialize an array
        int[] arr = { 1, 1, 4, 3, 16, 125, 1 };

        // Initialize power
        int K = 0;

        // Call the function
        // and print the answer
        System.out.println(
            indPowEqualsEle(arr, K));
    }
}
```

## 蟒蛇 3

```
# python code for the above approach

# Function to find count of elements which
# are a non-negative power of their indices
def indPowEqualsEle(arr, K):

    # Length of the array
    le = len(arr)

    # Initialize variable res for
    # calculating the answer
    res = 0

    # If the value of K is 0
    if (K == 0):

        # If the first element is 1
        # then the condition is sattisfied
        if (le > 0 and arr[0] == 1):
            res += 1

    # If the value of K > 0
    if (K > 0):

        # If the first is 0 increment res
        if (le > 0 and arr[0] == 1):
            res += 1

    # If the second element is 1
    # then increment res
    if (le > 1 and arr[1] == 1):
        res += 1

    # Iterate the array arr from index 2
    for i in range(2, le):

        # Initialize a variable
        # to index which is to be
        # multiplied K-1 times
        indPow = i

        for j in range(2, K):

            # Multiply current value
            # with index K - 1 times
            indPow *= i

        # If index power K is equal to
        # the element then increment res
        if (indPow == arr[i]):
            res += 1

    # return the result
    return res

# Driver function
if __name__ == "__main__":

    # Initialize an array
    arr = [1, 1, 4, 3, 16, 125, 1]

    # Initialize power
    K = 0

    # Call the function
    # and print the answer
    print(indPowEqualsEle(arr, K))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

class GFG
{

// Function to find count of elements which
// are a non-negative power of their indices
static int indPowEqualsEle(int []arr, int K)
{

    // Length of the array
    int len = arr.Length;

    // Initialize variable res for
    // calculating the answer
    int res = 0;

    // If the value of K is 0
    if (K == 0)
    {
        // If the first element is 1
        // then the condition is sattisfied
        if (len > 0 && arr[0] == 1)
            res++;
    }

    // If the value of K > 0
    if (K > 0)
    {
        // If the first is 0 increment res
        if (len > 0 && arr[0] == 1)
            res++;
    }

    // If the second element is 1
    // then increment res
    if (len > 1 && arr[1] == 1)
        res++;

    // Iterate the array arr from index 2
    for (int i = 2; i < len; i++)
    {

        // Initialize a variable
        // to index which is to be
        // multiplied K-1 times
        long indPow = i;

        for (int j = 2; j < K; j++)
        {

            // Multiply current value
            // with index K - 1 times
            indPow *= i;
        }

        // If index power K is equal to
        // the element then increment res
        if (indPow == arr[i])
            res++;
    }

    // return the result
    return res;
}

// Driver Code
public static void Main()
{

    // Initialize an array
    int []arr = {1, 1, 4, 3, 16, 125, 1};

    // Initialize power
    int K = 0;

    // Call the function
    // and print the answer
    Console.Write(indPowEqualsEle(arr, K));
}
}

// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
//<script>
// Javascript program for the above approach

// Function to find count of elements which
// are a non-negative power of their indices
function indPowEqualsEle(arr, K)
{

    // Length of the array
    let len = arr.length;

    // Initialize variable res for
    // calculating the answer
    let res = 0;

    // If the value of K is 0
    if (K == 0)
    {

        // If the first element is 1
        // then the condition is sattisfied
        if (len > 0 && arr[0] == 1)
            res++;
    }

    // If the value of K > 0
    if (K > 0)
    {

        // If the first is 0 increment res
        if (len > 0 && arr[0] == 1)
            res++;
    }

    // If the second element is 1
    // then increment res
    if (len > 1 && arr[1] == 1)
        res++;

    // Iterate the array arr from index 2
    for (let i = 2; i < len; i++)
    {

        // Initialize a variable
        // to index which is to be
        // multiplied K-1 times
        let indPow = i;

        for (let j = 2; j < K; j++)
        {

            // Multiply current value
            // with index K - 1 times
            indPow *= i;
        }

        // If index power K is equal to
        // the element then increment res
        if (indPow == arr[i])
            res++;
    }

    // return the result
    return res;
}

// Driver Code
// Initialize an array
let arr = [ 1, 1, 4, 3, 16, 125, 1 ];

// Initialize power
let K = 0;

// Call the function
// and print the answer
document.write(indPowEqualsEle(arr, K));

// This code is contributed by Samim Hossain Mondal
</script>
```

**Output**

```
3
```

**时间复杂度:**O(N * K)
T3】辅助空间: O(1)