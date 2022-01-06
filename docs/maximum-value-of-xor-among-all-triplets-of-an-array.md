# 数组所有三元组中异或的最大值

> 原文:[https://www . geeksforgeeks . org/数组三元组的最大异或值/](https://www.geeksforgeeks.org/maximum-value-of-xor-among-all-triplets-of-an-array/)

给定一个整数数组“arr”，任务是在所有可能的三元组对中找到任何三元组对的最大异或值。
**注意:**一个阵元可以多次使用。
**示例:**

> **输入:** arr[] = {3，4，5，6}
> **输出:** 7
> 异或值最大的三元组为{4，5，6}。
> **输入:** arr[] = {1，3，8，15}
> **输出:** 15

**进场:**

*   将数组中所有可能的二元对之间的所有可能的异或值存储在一个集合中。
*   集合数据结构用于避免异或值的重复。
*   现在，在每个集合元素和数组元素之间进行异或运算，以获得任何三元组对的最大值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// function to count maximum
// XOR value for a triplet
void Maximum_xor_Triplet(int n, int a[])
{
    // set is used to avoid repetitions
    set<int> s;

    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {

            // store all possible unique
            // XOR value of pairs
            s.insert(a[i] ^ a[j]);
        }
    }

    int ans = 0;

    for (auto i : s) {
        for (int j = 0; j < n; j++) {

            // store maximum value
            ans = max(ans, i ^ a[j]);
        }
    }

    cout << ans << "\n";
}

// Driver code
int main()
{
    int a[] = { 1, 3, 8, 15 };
    int n = sizeof(a) / sizeof(a[0]);
    Maximum_xor_Triplet(n, a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.util.HashSet;

class GFG
{

    // function to count maximum
    // XOR value for a triplet
    static void Maximum_xor_Triplet(int n, int a[])
    {
        // set is used to avoid repetitions
        HashSet<Integer> s = new HashSet<Integer>();

        for (int i = 0; i < n; i++)
        {
            for (int j = i; j < n; j++)
            {

                // store all possible unique
                // XOR value of pairs
                s.add(a[i] ^ a[j]);
            }
        }

        int ans = 0;
        for (Integer i : s)
        {
            for (int j = 0; j < n; j++)
            {

                // store maximum value
                ans = Math.max(ans, i ^ a[j]);
            }
        }
        System.out.println(ans);
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = {1, 3, 8, 15};
        int n = a.length;
        Maximum_xor_Triplet(n, a);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# function to count maximum
# XOR value for a triplet
def Maximum_xor_Triplet(n, a):

    # set is used to avoid repetitions
    s = set()

    for i in range(0, n):
        for j in range(i, n):

            # store all possible unique
            # XOR value of pairs
            s.add(a[i] ^ a[j])

    ans = 0
    for i in s:
        for j in range(0, n):

            # store maximum value
            ans = max(ans, i ^ a[j])

    print(ans)

# Driver code
if __name__ == "__main__":

    a = [1, 3, 8, 15]
    n = len(a)
    Maximum_xor_Triplet(n, a)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // function to count maximum
    // XOR value for a triplet
    static void Maximum_xor_Triplet(int n, int []a)
    {
        // set is used to avoid repetitions
        HashSet<int> s = new HashSet<int>();

        for (int i = 0; i < n; i++)
        {
            for (int j = i; j < n; j++)
            {

                // store all possible unique
                // XOR value of pairs
                s.Add(a[i] ^ a[j]);
            }
        }

        int ans = 0;
        foreach (int i in s)
        {
            for (int j = 0; j < n; j++)
            {

                // store maximum value
                ans = Math.Max(ans, i ^ a[j]);
            }
        }
        Console.WriteLine(ans);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []a = {1, 3, 8, 15};
        int n = a.Length;
        Maximum_xor_Triplet(n, a);
    }
}

/* This code has been contributed
by PrinciRaj1992*/
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
// function to count maximum
// XOR value for a triplet
function Maximum_xor_Triplet(n, a)
{
    // set is used to avoid repetitions
    let s = new Set();

    for (let i = 0; i < n; i++) {
        for (let j = i; j < n; j++) {

            // store all possible unique
            // XOR value of pairs
            s.add(a[i] ^ a[j]);
        }
    }

    let ans = 0;

    for (let i of s.values()) {
        for (let j = 0; j < n; j++) {

            // store maximum value
            ans = Math.max(ans, i ^ a[j]);
        }
    }

    document.write( ans, "<br>");
}

// Driver code
let a = [ 1, 3, 8, 15 ];
let n = a.length;
    Maximum_xor_Triplet(n, a);

</script>
```

**Output:** 

```
15
```