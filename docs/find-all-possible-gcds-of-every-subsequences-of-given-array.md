# 找出给定数组的每个子序列的所有可能的 GCDs】

> 原文:[https://www . geeksforgeeks . org/find-all-可能性-给定数组的每个子序列的 gcds/](https://www.geeksforgeeks.org/find-all-possible-gcds-of-every-subsequences-of-given-array/)

给定一个由正整数 **N** 组成的数组 **arr[]** ，任务是在数组 **arr[]** 的所有非空[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中找到所有可能的相异 [**最大公约数(GCDs)**](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 。

**示例:**

> **输入:** arr[] = {3，4，8}
> **输出:** 1 3 4 8
> **解释:**
> 可能的非空子序列是{3}、{4}、{8}、{3，4}、{4，8}、{3，8}、{3，4，8}以及它们对应的 GCDs 是 3，4，8，1，4，1。
> 因此，将所有 gcd 打印为{1，3，4，8}。
> 
> **输入:** arr[] = {3，8，9，4，13，45，6}
> **输出:** 1 2 3 4 6 8 9 13 45

**天真方法:**解决给定问题的最简单方法是[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能子序列，并将子序列的所有 gcd 存储在一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。检查所有子序列后，将集合中的元素存储打印为所有可能形成的 gcd。

***时间复杂度:** O(log M*2 <sup>N</sup> ，其中 M 为* [*数组的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*

**有效方法:**通过观察任何子序列的 GCD 位于范围**【1，M】**内的事实，上述方法也可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)进行优化，其中 **M** 是数组的最大元素。因此，想法是[迭代然后范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，M】**并且如果范围中的任何元素是数组元素的[因子](https://www.geeksforgeeks.org/find-largest-prime-factor-number/)，则打印当前元素作为结果之一 **GCD** 。按照以下步骤解决问题:

*   将所有数组元素存储在 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 中，比如 **s** 。
*   使用变量 **i** 迭代范围**【1，M】**，并执行以下步骤:
    *   遍历 **i** 的所有倍数，如果 HashSet 中存在任何倍数，则打印当前元素 **i** 作为可能的 GCD 之一。

下面是上述方法的一个实现:

// C++程序的上述方法

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the different GCDs of
// the subsequence of the given array
void findGCDsSubsequence(vector<int> arr)
{

    // Stores all the possible GCDs
    vector<int> ans;

    // Stores all array element in set
    set<int> s;
    for(int i : arr)
        s.insert(i);

    int M = *max_element(arr.begin(), arr.end());

    // Iterate over the range [1, M]
    for(int i = 1; i <= M; i++)
    {
        int gcd = 0;

        // Check if i can be the GCD of
        // any subsequence
        for(int j = i; j < M + 1; j += i)
        {
            if (s.find(j) != s.end())
                gcd = __gcd(gcd, j);
        }
        if (gcd == i)
            ans.push_back(i);
    }
    for(int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";
}

// Driver Code
int main()
{
    int N = 7;
    vector<int> arr = { 3, 4, 8 };

    // Function Call
    findGCDsSubsequence(arr);
    return 0;
}

// This code is contributed by parthagarwal1962000
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG {
static int gcd1(int a, int b)
{
    return b == 0 ? a : gcd1(b, a % b);
}

// Function to find the different GCDs of
// the subsequence of the given array
static void findGCDsSubsequence(ArrayList<Integer> arr)
{

    // Stores all the possible GCDs
    ArrayList<Integer> ans = new ArrayList<Integer>();

    // Stores all array element in set
    HashSet<Integer> s = new HashSet<Integer>();
    for(int i : arr)
        s.add(i);

    int M = Integer.MIN_VALUE;
    for(int i : arr)
    {
        if (i > M)
            M = i;
    }

    // Iterate over the range [1, M]
    for(int i = 1; i <= M; i++)
    {
        int gcd = 0;

        // Check if i can be the GCD of
        // any subsequence
        for(int j = i; j < M + 1; j += i)
        {
            if (s.contains(j))
                gcd = gcd1(gcd, j);
        }
        if (gcd == i)
            ans.add(i);
    }
    for(int i = 0; i < ans.size(); i++)
       System.out.print(ans.get(i) + " ");
}

// Driver Code
 public static void main(String args[])
{
    ArrayList<Integer> arr = new ArrayList<Integer>();
    arr.add(3);
    arr.add(4);
    arr.add(8);

    // Function Call
    findGCDsSubsequence(arr);
}
}
// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to find the different GCDs of
# the subsequence of the given array
def findGCDsSubsequence(nums):

        # Stores all the possible GCDs
    Ans = []

    # Stores all array element in set
    s = set(nums)

    # Find the maximum array element
    M = max(nums)

    # Iterate over the range [1, M]
    for i in range(1, M + 1):

          # Stores the GCD of subsequence
        gcd = 0

        # Check if i can be the GCD of
        # any subsequence
        for j in range(i, M + 1, i):
            if j in s:
                gcd = math.gcd(gcd, j)

        # Store the value i in Ans[]
        # if it can be the GCD
        if gcd == i:
            Ans += [i]

    # Print all possible GCDs stored
    print(*Ans)

# Driver Code
N = 7
arr = [3, 4, 8]

# Function Call
findGCDsSubsequence(arr)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int gcd1(int a, int b)
{
    return b == 0 ? a : gcd1(b, a % b);
}

// Function to find the different GCDs of
// the subsequence of the given array
static void findGCDsSubsequence(List<int> arr)
{

    // Stores all the possible GCDs
    List<int> ans = new List<int>();

    // Stores all array element in set
    HashSet<int> s = new HashSet<int>();
    foreach(int i in arr)
        s.Add(i);

    int M = Int32.MinValue;
    foreach(int i in arr)
    {
        if (i > M)
            M = i;
    }

    // Iterate over the range [1, M]
    for(int i = 1; i <= M; i++)
    {
        int gcd = 0;

        // Check if i can be the GCD of
        // any subsequence
        for(int j = i; j < M + 1; j += i)
        {
            if (s.Contains(j))
                gcd = gcd1(gcd, j);
        }
        if (gcd == i)
            ans.Add(i);
    }
    for(int i = 0; i < ans.Count; i++)
        Console.Write(ans[i] + " ");
}

// Driver Code
public static void Main()
{
    List<int> arr = new List<int>(){ 3, 4, 8 };

    // Function Call
    findGCDsSubsequence(arr);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

function __gcd(a, b) {
    if (b == 0)
    return a;
    return __gcd(b, a % b);
 }

// Function to find the different GCDs of
// the subsequence of the given array
function findGCDsSubsequence(arr) {

    // Stores all the possible GCDs
    let ans = [];

    // Stores all array element in set
    let s = new Set();
    for (let i of arr)
        s.add(i);

    let M = [...arr].sort((a, b) => b - a)[0]

    // Iterate over the range [1, M]
    for (let i = 1; i <= M; i++) {
        let gcd = 0;

        // Check if i can be the GCD of
        // any subsequence
        for (let j = i; j < M + 1; j += i) {
            if (s.has(j))
                gcd = __gcd(gcd, j);
        }
        if (gcd == i)
            ans.push(i);
    }
    for (let i = 0; i < ans.length; i++)
        document.write(ans[i] + " ");
}

// Driver Code

let N = 7;
let arr = [3, 4, 8];

// Function Call
findGCDsSubsequence(arr);

// This code is contributed by gfgking

</script>
```

**Output**

```
1 3 4 8
```

***时间复杂度:** O(M*log M)，其中 M 为* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(N)*