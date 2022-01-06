# 计算使每个数组元素为 0 所需的 4 秒和/或 5 秒的组合

> 原文:[https://www . geesforgeks . org/count-4s 和-or-5s 的组合-制作每个数组元素所需的-0/](https://www.geeksforgeeks.org/count-the-combination-of-4s-and-or-5s-required-to-make-each-array-element-0/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是检查每个数组元素是否可以用数字 **4** 和 **5** 表示。如果可能，则打印每个数组元素所需的 **4** 和 **5** 的总数。否则，打印 **-1。**

**示例:**

> **输入:** arr[] = {12，11，9}
> **输出:** 3 -1 2
> **解释:**
> 
> 1.  arr[0]( =12):打印 3，因为它可以用 3 个 4 来表示，即 4 + 4 + 4 = 12。
> 2.  arr[1](= 11): Print -1，因为它不能用 4 和 5 的任何组合来表示。
> 3.  arr[2](= 9):打印 2，因为它可以用一个 4 和一个 5 来表示，即 4 + 5 = 9。
> 
> **输入:** arr[] = {7，15，17，22}
> **输出:** -1 3 4 5

**方法:**问题可以用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)和一点数学来解决。按照以下步骤解决问题:

*   [初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)称 **ans，**为 **{-1}** ，其中**ans【I】**存储数组 **arr[]的值**arr【I】**的可能答案的答案。**
*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**，并执行以下步骤:
    *   如果**arr【I】**小于 **4、**，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   初始化两个变量，说**求和**为 **INT_MAX** 存储 **4** 和 **5** 需要形成**arr【I】**和 **cnt** 为 **0** 保持 **4 当前因子的计数。**
    *   [使用变量 **j** 迭代一个范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，arr[I]】**，并执行以下步骤:
        *   如果**(arr[I]–j)**可被 **5、**整除，则将**和**的值设置为**和**以及**的最小值(CNT+(arr[I]–j)/5)。**
        *   通过 **1** 增加 **cnt** 的值，通过 **4** 增加 **j** 的值。
    *   如果**和**不等于 **INT_MAX，**，则将[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中**ans【I】**的值设置为**和。**
*   最后，完成以上步骤后，打印[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)T2 ans 中的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the count of the
// combination of 4 or 5 required to
// make the arr[i] for each 0 < i < N
void sumOfCombinationOf4OR5(vector<int> arr, int N)
{

    // Vector to store the answer
    vector<int> ans(N, -1);

    // Iterate in the range[0, N-1]
    for (int i = 0; i < N; i++) {

        if (arr[i] < 4) {
            continue;
        }

        // Initialize sum to store the count
        // of numbers and cnt for the current
        // factor of 4
        int sum = INT_MAX, cnt = 0;

        // Iterate in the range[0, arr[i]] with
        // increment of 4
        for (int j = 0; j <= arr[i]; j += 4) {

            // Check if arr[i] - j(the current factor
            // of 4) is divisible by 5 or not
            if ((arr[i] - j) % 5 == 0) {
                sum = min(sum, cnt + (arr[i] - j) / 5);
            }

            cnt++;
        }

        // If sum is not maximum
        // then answer is found
        if (sum != INT_MAX)
            ans[i] = sum;
    }

    // Finally, print the required answer
    for (auto num : ans)
        cout << num << " ";
}

// Driver Code
int main()
{

    // Given Input
    vector<int> arr = { 7, 15, 17, 22 };
    int N = arr.size();

    // Function Call
    sumOfCombinationOf4OR5(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;

class GFG
{

    // Function to print the count of the
    // combination of 4 or 5 required to
    // make the arr[i] for each 0 < i < N
    static void sumOfCombinationOf4OR5(int[] arr, int N)
    {

        // Vector to store the answer
        int[] ans = new int[N];
        Arrays.fill(ans, -1);
        // Iterate in the range[0, N-1]
        for (int i = 0; i < N; i++) {

            if (arr[i] < 4) {
                continue;
            }

            // Initialize sum to store the count
            // of numbers and cnt for the current
            // factor of 4
            int sum = Integer.MAX_VALUE;
            int cnt = 0;

            // Iterate in the range[0, arr[i]] with
            // increment of 4
            for (int j = 0; j <= arr[i]; j += 4) {

                // Check if arr[i] - j(the current factor
                // of 4) is divisible by 5 or not
                if ((arr[i] - j) % 5 == 0) {
                    sum = Math.min(sum,
                                   cnt + (arr[i] - j) / 5);
                }

                cnt++;
            }

            // If sum is not maximum
            // then answer is found
            if (sum != Integer.MAX_VALUE)
                ans[i] = sum;
        }

        // Finally, print the required answer
        for (int num : ans)
            System.out.printf(num + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int[] arr = { 7, 15, 17, 22 };
        int N = arr.length;

        // Function Call
        sumOfCombinationOf4OR5(arr, N);
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print the count of the
# combination of 4 or 5 required to
# make the arr[i] for each 0 < i < N
def sumOfCombinationOf4OR5(arr, N):

    # Vector to store the answer
    ans = [-1 for i in range(N)]

    # Iterate in the range[0, N-1]
    for i in range(N):

        if (arr[i] < 4):
            continue

        # Initialize sum to store the count
        # of numbers and cnt for the current
        # factor of 4
        sum = 10**9
        cnt = 0

        # Iterate in the range[0, arr[i]] with
        # increment of 4
        for j in range(0, arr[i] + 1, 4):

            # Check if arr[i] - j(the current factor
            # of 4) is divisible by 5 or not
            if ((arr[i] - j) % 5 == 0):
                sum = min(sum, cnt + (arr[i] - j) // 5)

            cnt += 1

        # If sum is not maximum
        # then answer is found
        if (sum != 10**9):
            ans[i] = sum

    # Finally, print the required answer
    for num in ans:
        print(num, end = " ")

# Driver Code

# Given Input
arr = [ 7, 15, 17, 22 ]
N = len(arr)

# Function Call
sumOfCombinationOf4OR5(arr, N)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the count of the
// combination of 4 or 5 required to
// make the arr[i] for each 0 < i < N
static void sumOfCombinationOf4OR5(int []arr, int N)
{

    // Vector to store the answer
    int []ans = new int[N];
    for(int i = 0; i < N; i++)
       ans[i] = -1;

    // Iterate in the range[0, N-1]
    for (int i = 0; i < N; i++) {

        if (arr[i] < 4) {
            continue;
        }

        // Initialize sum to store the count
        // of numbers and cnt for the current
        // factor of 4
        int sum = Int32.MaxValue, cnt = 0;

        // Iterate in the range[0, arr[i]] with
        // increment of 4
        for (int j = 0; j <= arr[i]; j += 4) {

            // Check if arr[i] - j(the current factor
            // of 4) is divisible by 5 or not
            if ((arr[i] - j) % 5 == 0) {
                sum = Math.Min(sum, cnt + (int)(arr[i] - j) / 5);
            }

            cnt++;
        }

        // If sum is not maximum
        // then answer is found
        if (sum != Int32.MaxValue)
            ans[i] = sum;
    }

    // Finally, print the required answer
    foreach(int num in ans)
        Console.Write(num + " ");
}

// Driver Code
public static void Main()
{

    // Given Input
    int []arr = {7, 15, 17, 22 };
    int N = arr.Length;

    // Function Call
    sumOfCombinationOf4OR5(arr, N);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to print the count of the
// combination of 4 or 5 required to
// make the arr[i] for each 0 < i < N
function sumOfCombinationOf4OR5(arr, N) {

    // Vector to store the answer
    let ans = new Array(N).fill(-1);

    // Iterate in the range[0, N-1]
    for (let i = 0; i < N; i++) {

        if (arr[i] < 4) {
            continue;
        }

        // Initialize sum to store the count
        // of numbers and cnt for the current
        // factor of 4
        let sum = Number.MAX_SAFE_INTEGER, cnt = 0;

        // Iterate in the range[0, arr[i]] with
        // increment of 4
        for (let j = 0; j <= arr[i]; j += 4) {

            // Check if arr[i] - j(the current factor
            // of 4) is divisible by 5 or not
            if ((arr[i] - j) % 5 == 0) {
                sum = Math.min(sum, cnt + Math.floor((arr[i] - j) / 5));
            }

            cnt++;
        }

        // If sum is not maximum
        // then answer is found
        if (sum != Number.MAX_SAFE_INTEGER)
            ans[i] = sum;
    }

    // Finally, print the required answer
    for (let num of ans)
        document.write(num + " ");
}

// Driver Code

// Given Input
let arr = [7, 15, 17, 22];
let N = arr.length;

// Function Call
sumOfCombinationOf4OR5(arr, N);
</script>

// This code is contributed by _saurabh_jaiswal.
```

**Output**

```
-1 3 4 5 
```

***时间复杂度:** O(N*M)其中 **M** 是数组 **arr[]的最大元素。***
***辅助空间:** O(N)*

***注:**上述方法可以在空间复杂度方面进一步优化，因为在上述方法中，打印前存储结果是可选的。此后，空间复杂度将优化为 O(1)。*