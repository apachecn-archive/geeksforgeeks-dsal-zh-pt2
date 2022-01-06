# 长度为 K 的子序列的最大位与值

> 原文:[https://www . geeksforgeeks . org/长度为 k 的子序列的最大位和值/](https://www.geeksforgeeks.org/maximum-bitwise-and-value-of-subsequence-of-length-k/)

给定一个数组**一个大小为 **N** 的**和一个整数 **K** 。任务是找到长度为 **K** 的任意子序列元素的最大[位和](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值。
**注**:a【I】<= 10<sup>9</sup>
**例:**

> **输入:** a[] = {10，20，15，4，14}，K = 4
> **输出:** 4
> {20，15，4，14}是值最高的子序列'&'。
> **输入:** a[] = {255，127，31，5，24，37，15}，K = 5
> **输出:** 8

**天真方法**:天真的方法是递归寻找所有长度子序列 **K** 的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值，其中最大值就是答案。
**有效方法**:一种有效方法是使用[位属性](https://www.geeksforgeeks.org/bitwise-hacks-for-competitive-programming/)求解。下面是解决问题的步骤:

*   从左开始迭代(最初**左= 31** 作为**2<sup>32</sup>T12】10<sup>9</sup>**)直到我们在第 I 位被设置的向量 temp(最初 **temp = arr** )中找到 **> K** 个数字。将新的数字集更新为临时数组
*   如果我们没有得到 **> K** 的数字，temp 数组中任何 **K** 元素的 **&** 值将是最大的 **&** 值。
*   重复**步骤-1** ，左侧重新初始化为**第一位+ 1** 。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of
// the addition of all possible subsets.
#include <bits/stdc++.h>
using namespace std;

// Function to perform step-1
vector<int> findSubset(vector<int>& temp, int& last, int k)
{
    vector<int> ans;

    // Iterate from left till 0
    // till we get a bit set of K numbers
    for (int i = last; i >= 0; i--) {
        int cnt = 0;

        // Count the numbers whose
        // i-th bit is set
        for (auto it : temp) {
            int bit = it & (1 << i);
            if (bit > 0)
                cnt++;
        }

        // If the array has numbers>=k
        // whose i-th bit is set
        if (cnt >= k) {
            for (auto it : temp) {
                int bit = it & (1 << i);
                if (bit > 0)
                    ans.push_back(it);
            }

            // Update last
            last = i - 1;

            // Return the new set of numbers
            return ans;
        }
    }

    return ans;
}

// Function to find the maximum '&' value
// of K elements in subsequence
int findMaxiumAnd(int a[], int n, int k)
{
    int last = 31;
    // Temporary arrays
    vector<int> temp1, temp2;

    // Initially temp = arr
    for (int i = 0; i < n; i++) {
        temp2.push_back(a[i]);
    }

    // Iterate till we have >=K elements
    while ((int)temp2.size() >= k) {

        // Temp array
        temp1 = temp2;

        // Find new temp array if
        // K elements are there
        temp2 = findSubset(temp2, last, k);
    }

    // Find the & value
    int ans = temp1[0];
    for (int i = 0; i < k; i++)
        ans = ans & temp1[i];

    return ans;
}

// Driver Code
int main()
{
    int a[] = { 255, 127, 31, 5, 24, 37, 15 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 4;

    cout << findMaxiumAnd(a, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of
// the addition of all possible subsets.
import java.util.*;
class GFG
{
static int last;

// Function to perform step-1
static Vector<Integer>
       findSubset(Vector<Integer> temp, int k)
{
    Vector<Integer> ans = new Vector<Integer>();

    // Iterate from left till 0
    // till we get a bit set of K numbers
    for (int i = last; i >= 0; i--)
    {
        int cnt = 0;

        // Count the numbers whose
        // i-th bit is set
        for (Integer it : temp)
        {
            int bit = it & (1 << i);
            if (bit > 0)
                cnt++;
        }

        // If the array has numbers>=k
        // whose i-th bit is set
        if (cnt >= k)
        {
            for (Integer it : temp)
            {
                int bit = it & (1 << i);
                if (bit > 0)
                    ans.add(it);
            }

            // Update last
            last = i - 1;

            // Return the new set of numbers
            return ans;
        }
    }
    return ans;
}

// Function to find the maximum '&' value
// of K elements in subsequence
static int findMaxiumAnd(int a[], int n, int k)
{
    last = 31;

    // Temporary arrays
    Vector<Integer> temp1 = new Vector<Integer>();
    Vector<Integer> temp2 = new Vector<Integer>();;

    // Initially temp = arr
    for (int i = 0; i < n; i++)
    {
        temp2.add(a[i]);
    }

    // Iterate till we have >=K elements
    while ((int)temp2.size() >= k)
    {

        // Temp array
        temp1 = temp2;

        // Find new temp array if
        // K elements are there
        temp2 = findSubset(temp2, k);
    }

    // Find the & value
    int ans = temp1.get(0);
    for (int i = 0; i < k; i++)
        ans = ans & temp1.get(i);

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 255, 127, 31, 5, 24, 37, 15 };
    int n = a.length;
    int k = 4;

    System.out.println(findMaxiumAnd(a, n, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the sum of
# the addition of all possible subsets.
last = 31

# Function to perform step-1
def findSubset(temp, k):
    global last
    ans = []

    # Iterate from left till 0
    # till we get a bit set of K numbers
    for i in range(last, -1, -1):
        cnt = 0

        # Count the numbers whose
        # i-th bit is set
        for it in temp:
            bit = it & (1 << i)
            if (bit > 0):
                cnt += 1

        # If the array has numbers>=k
        # whose i-th bit is set
        if (cnt >= k):
            for it in temp:
                bit = it & (1 << i)
                if (bit > 0):
                    ans.append(it)

            # Update last
            last = i - 1

            # Return the new set of numbers
            return ans

    return ans

# Function to find the maximum '&' value
# of K elements in subsequence
def findMaxiumAnd(a, n, k):
    global last

    # Temporary arrays
    temp1, temp2, = [], []

    # Initially temp = arr
    for i in range(n):
        temp2.append(a[i])

    # Iterate till we have >=K elements
    while len(temp2) >= k:

        # Temp array
        temp1 = temp2

        # Find new temp array if
        # K elements are there
        temp2 = findSubset(temp2, k)

    # Find the & value
    ans = temp1[0]
    for i in range(k):
        ans = ans & temp1[i]

    return ans

# Driver Code
a = [255, 127, 31, 5, 24, 37, 15]
n = len(a)
k = 4

print(findMaxiumAnd(a, n, k))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to find the sum of
// the addition of all possible subsets.
using System;
using System.Collections.Generic;

class GFG
{
static int last;

// Function to perform step-1
static List<int>findSubset(List<int> temp, int k)
{
    List<int> ans = new List<int>();

    // Iterate from left till 0
    // till we get a bit set of K numbers
    for (int i = last; i >= 0; i--)
    {
        int cnt = 0;

        // Count the numbers whose
        // i-th bit is set
        foreach (int it in temp)
        {
            int bit = it & (1 << i);
            if (bit > 0)
                cnt++;
        }

        // If the array has numbers>=k
        // whose i-th bit is set
        if (cnt >= k)
        {
            foreach (int it in temp)
            {
                int bit = it & (1 << i);
                if (bit > 0)
                    ans.Add(it);
            }

            // Update last
            last = i - 1;

            // Return the new set of numbers
            return ans;
        }
    }
    return ans;
}

// Function to find the maximum '&' value
// of K elements in subsequence
static int findMaxiumAnd(int []a, int n, int k)
{
    last = 31;

    // Temporary arrays
    List<int> temp1 = new List<int>();
    List<int> temp2 = new List<int>();;

    // Initially temp = arr
    for (int i = 0; i < n; i++)
    {
        temp2.Add(a[i]);
    }

    // Iterate till we have >=K elements
    while ((int)temp2.Count >= k)
    {

        // Temp array
        temp1 = temp2;

        // Find new temp array if
        // K elements are there
        temp2 = findSubset(temp2, k);
    }

    // Find the & value
    int ans = temp1[0];
    for (int i = 0; i < k; i++)
        ans = ans & temp1[i];

    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 255, 127, 31, 5, 24, 37, 15 };
    int n = a.Length;
    int k = 4;

    Console.WriteLine(findMaxiumAnd(a, n, k));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find the sum of
// the addition of all possible subsets.

// Function to perform step-1
function findSubset(temp,k)
{
    let ans = [];

    // Iterate from left till 0
    // till we get a bit set of K numbers
    for (let i = last; i >= 0; i--)
    {
        let cnt = 0;

        // Count the numbers whose
        // i-th bit is set
        for (let it=0;it< temp.length;it++)
        {
            let bit = temp[it] & (1 << i);
            if (bit > 0)
                cnt++;
        }

        // If the array has numbers>=k
        // whose i-th bit is set
        if (cnt >= k)
        {
            for (let it=0;it< temp.length;it++)
            {
                let bit = temp[it] & (1 << i);
                if (bit > 0)
                    ans.push(temp[it]);
            }

            // Update last
            last = i - 1;

            // Return the new set of numbers
            return ans;
        }
    }
    return ans;
}

// Function to find the maximum '&' value
// of K elements in subsequence
function findMaxiumAnd(a,n,k)
{
    last = 31;

    // Temporary arrays
    let temp1 = [];
    let temp2 = [];

    // Initially temp = arr
    for (let i = 0; i < n; i++)
    {
        temp2.push(a[i]);
    }

    // Iterate till we have >=K elements
    while (temp2.length >= k)
    {

        // Temp array
        temp1 = temp2;

        // Find new temp array if
        // K elements are there
        temp2 = findSubset(temp2, k);
    }

    // Find the & value
    let ans = temp1[0];
    for (let i = 0; i < k; i++)
        ans = ans & temp1[i];

    return ans;
}

// Driver Code
let a=[255, 127, 31, 5, 24, 37, 15 ];
let n = a.length;
let k = 4;
document.write(findMaxiumAnd(a, n, k));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
24
```