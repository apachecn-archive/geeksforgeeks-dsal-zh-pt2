# 计算给定阵列中的团块数量

> 原文:[https://www . geeksforgeeks . org/count-给定阵列中的簇数/](https://www.geeksforgeeks.org/count-the-number-of-clumps-in-the-given-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算给定数组中的块数。

> 丛被定义为具有相同值的两个或更多相邻元素的系列。

**例:**

> **输入:** arr[] = { 13，15，66，66，37，8，8，11，52 }；
> **输出:** 2
> **说明:**
> 给定数组{66，66}和{8，8}中有两个丛。
> **输入:** arr[] = {1，2，1，4，3，2}
> **输出:** 0
> **解释:**
> 给定数组中没有团块。

**进场:**为了解决问题，我们需要按照以下步骤:

1.  遍历数组并检查相同元素在两个连续索引上的任何出现。
2.  对于任何这种情况，循环直到出现不同的数字。
3.  只有在执行第 2 步后，才能将**团块**的计数增加 1。如果尚未遍历整个数组，请对以下元素重复上述步骤。
4.  打印整个数组遍历后**块**的最终计数。

以下是上述方法的实现:

## C++

```
// C++ program to calculate
// the number of clumps in
// an array
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// clumps in the given array arr[]
int countClumps(int arr[], int N)
{

    // Initialise count of clumps as 0
    int clumps = 0;

    // Traverse the arr[]
    for (int i = 0; i < N - 1; i++) {

        int flag = 0;
        // Whenever a sequence of same
        // value is encountered
        while (arr[i] == arr[i + 1]) {
            flag = 1;
            i++;
        }

        if (flag)
            clumps++;
    }

    // Return the count of clumps
    return clumps;
}
// Driver Code
int main()
{

    // Given array
    int arr[] = { 13, 15, 66, 66, 66, 37, 37,
                  8, 8, 11, 11 };

    // length of the given array arr[]
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << countClumps(arr, N) << '\n';
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class Test {

    // Given array arr[]
    static int arr[] = { 13, 15, 66, 66, 66,
                         37, 37, 8, 8, 11, 11 };

    // Function to count the number of
    // clumps in the given array arr[]
    static int countClumps()
    {
        int l = arr.length;

        // Initialise count of clumps as 0
        int clumps = 0;

        // Traverse the arr[]
        for (int i = 0; i < l - 1; i++) {

            int flag = 0;
            // Whenever a sequence of same
            // value is encountered
            while (i < l - 1
                   && arr[i] == arr[i + 1]) {
                flag = 1;
                i++;
            }

            if (flag == 1)
                clumps++;
        }

        // Return the count of clumps
        return clumps;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Function Call
        System.out.println(countClumps());
    }
}
```

## 蟒蛇 3

```
# Python3 program to calculate
# the number of clumps in
# an array

# Function to count the number of
# clumps in the given array arr[]
def countClumps(arr, N):

    # Initialise count of clumps as 0
    clumps = 0

    # Traverse the arr[]
    i = 0
    while(i < N - 1):

        flag = 0

        # Whenever a sequence of same
        # value is encountered
        while (i + 1 < N and
               arr[i] == arr[i + 1]):
            flag = 1
            i += 1

        if (flag):
            clumps += 1

        i += 1

    # Return the count of clumps
    return clumps

# Driver Code

# Given array
arr = [ 13, 15, 66, 66, 66,
        37, 37, 8, 8, 11, 11 ]

# length of the given array arr[]
N = len(arr)

# Function Call
print(countClumps(arr, N))

# This code is contributed by yatin
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Given array arr[]
static int []arr = { 13, 15, 66, 66, 66,
                     37, 37, 8, 8, 11, 11 };

// Function to count the number of
// clumps in the given array arr[]
static int countClumps()
{
    int l = arr.Length;

    // Initialise count of clumps as 0
    int clumps = 0;

    // Traverse the arr[]
    for (int i = 0; i < l - 1; i++)
    {
        int flag = 0;

        // Whenever a sequence of same
        // value is encountered
        while (i < l - 1 && arr[i] == arr[i + 1])
        {
            flag = 1;
            i++;
        }

        if (flag == 1)
            clumps++;
    }

    // Return the count of clumps
    return clumps;
}

// Driver Code
public static void Main()
{

    // Function Call
    Console.WriteLine(countClumps());
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program to calculate
    // the number of clumps in
    // an array 

    // Function to count the number of
    // clumps in the given array arr[]
    function countClumps(arr, N)
    {

        // Initialise count of clumps as 0
        let clumps = 0;

        // Traverse the arr[]
        for (let i = 0; i < N - 1; i++) {

            let flag = 0;
            // Whenever a sequence of same
            // value is encountered
            while (arr[i] == arr[i + 1]) {
                flag = 1;
                i++;
            }

            if (flag)
                clumps++;
        }

        // Return the count of clumps
        return clumps;
    }

    // Given array
    let arr = [ 13, 15, 66, 66, 66, 37, 37, 8, 8, 11, 11 ];

    // length of the given array arr[]
    let N = arr.length;

    // Function Call
    document.write(countClumps(arr, N));

</script>
```

**Output:** 

```
4
```

**时间复杂度:** *O(N)* ，其中 **N** 是给定数组中元素的个数。
**辅助空间:** *O(1)*