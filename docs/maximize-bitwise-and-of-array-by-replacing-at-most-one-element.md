# 通过最多替换一个元素来最大化数组的按位与

> 原文:[https://www . geeksforgeeks . org/通过最多替换一个元素来最大化按位数组/](https://www.geeksforgeeks.org/maximize-bitwise-and-of-array-by-replacing-at-most-one-element/)

给定一个包含正整数 **N** 的数组 **arr[]** ，任务是通过最多选取 **arr[]** 的一个元素并将其递增或递减任意值来最大化 **arr[]** 的位**和**。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 2
> **解释:**以下是为最大化 arr[]
> 的按位与而执行的操作最初按位与{1，2，3} = 0
> 将 arr[0]递增 1 会更新 arr[] = {2，2，3}。
> 现在{2，2，3}的按位“与”是 2，这是最大可能值。
> 所以，答案是 2。
> 
> **输入:** arr[] = {10，10}
> **输出:** 10
> **说明:**不要执行任何最佳操作。

**方法:**这个问题的问题陈述说通过替换**arr【】**中几乎一个元素来最大化**arr【】**的 AND。解决这个问题的蛮力方法是对**arr【】**中除一次一个之外的所有元素进行**位“与”**，并为每次 arr【】的整个位“与”中贡献不相加的那个元素找到合适的替换。对**arr【】**中的所有元素都这样做，找到最佳结果。

下面是上述方法的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum AND by
// Replacing atmost one element by any value
int maxAnd(int n, vector<int> a)
{
    // To Calculate answer
    int ans = 0;

    // Iterating through the array
    for (int i = 0; i < n; i++) {
        int max_and = 0XFFFFFFFF;

        // Checking and for element and
        // Leaving only jth element
        for (int j = 0; j < n; j++) {
            if (i != j) {
                max_and = max_and & a[j];
            }
        }

        // Comapring previous answers
        // and max answers
        ans = max(ans, max_and);
    }
    return ans;
}

// Driver Code
int main()
{
    int N = 3;
    vector<int> arr = { 1, 2, 3 };

    // Function Call
    cout << maxAnd(N, arr) << "\n";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG{

// Function to find maximum AND by
// Replacing atmost one element by any value
static int maxAnd(int n,int[] a)
{

    // To Calculate answer
    int ans = 0;

    // Iterating through the array
    for(int i = 0; i < n; i++)
    {
        int max_and = 0XFFFFFFFF;

        // Checking and for element and
        // Leaving only jth element
        for(int j = 0; j < n; j++)
        {
            if (i != j)
            {
                max_and = max_and & a[j];
            }
        }

        // Comapring previous answers
        // and max answers
        ans = Math.max(ans, max_and);
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;
    int[] arr = { 1, 2, 3 };

    // Function Call
    System.out.println( maxAnd(N, arr) );
}
}

// This code is contributed by Potta Lokesh
```

## 计算机编程语言

```
# Function to find maximum AND by
# Replacing atmost one element by any value
def maxAnd(n, a):

    # To Calculate answer
    ans = 0

    # Iterating through the array
    for i in range(0, n):
        max_and = 0XFFFFFFFF

        # Checking and for element and
        # Leaving only jth element
        for j in range(0, n):
            if (i != j):
                max_and = max_and & a[j]

        # Comapring previous answers
        # and max answers
        ans = max(ans, max_and)

    return ans

# Driver Code
if __name__ == '__main__':

    N = 3
    arr = [ 1, 2, 3 ]

    print(maxAnd(N, arr))

    # This code is contributed by Samim Hossain Mondal.
```

## C#

```
using System;

class GFG{

// Function to find maximum AND by
// Replacing atmost one element by any value
static int maxAnd(int n,int[] a)
{

    // To Calculate answer
    int ans = 0;

    // Iterating through the array
    for(int i = 0; i < n; i++)
    {
        uint max_and = 0XFFFFFFFF;

        // Checking and for element and
        // Leaving only jth element
        for(int j = 0; j < n; j++)
        {
            if (i != j)
            {
                max_and = Convert.ToUInt32(max_and & a[j]);
            }
        }

        // Comapring previous answers
        // and max answers
        ans = Math.Max(ans, (int)max_and);
    }
    return ans;
}

// Driver Code
public static void Main()
{
    int N = 3;
    int[] arr = { 1, 2, 3 };

    // Function Call
    Console.Write( maxAnd(N, arr) );
}
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>

// Function to find maximum AND by
// Replacing atmost one element by any value
const maxAnd = (n, a) => {

    // To Calculate answer
    let ans = 0;

    // Iterating through the array
    for(let i = 0; i < n; i++)
    {
        let max_and = 0XFFFFFFFF;

        // Checking and for element and
        // Leaving only jth element
        for(let j = 0; j < n; j++)
        {
            if (i != j)
            {
                max_and = max_and & a[j];
            }
        }

        // Comapring previous answers
        // and max answers
        ans = Math.max(ans, max_and);
    }
    return ans;
}

// Driver Code
let N = 3;
let arr = [ 1, 2, 3 ];

// Function Call
document.write(maxAnd(N, arr));

// This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
2
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(1)