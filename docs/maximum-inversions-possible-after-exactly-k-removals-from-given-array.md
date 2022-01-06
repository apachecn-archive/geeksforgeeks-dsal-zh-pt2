# 从给定数组中精确移除 K 个元素后可能出现的最大反转

> 原文:[https://www . geeksforgeeks . org/maximum-inversion-从给定数组中精确 k 次移除后可能出现的情况/](https://www.geeksforgeeks.org/maximum-inversions-possible-after-exactly-k-removals-from-given-array/)

给定一个由 **N** 整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】】**，任务是在移除 **K** [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)元素后，找到给定数组可能的最大[反转次数。](https://www.geeksforgeeks.org/counting-inversions/)

**示例:**

> **输入:** arr[] = {2，3，4，1}，K = 2
> **输出:** 1
> **解释:**移除 1 <sup>st</sup> 和 2 <sup>nd</sup> 数组元素将数组修改为{4，1}。因此，最大反转次数为 1。
> 
> **输入:** arr[] = {4，3，2，1}，K = 3
> **输出:** 0
> **解释:**由于 K 次移除后的数组只剩下 1 个元素，因此最大反转次数为 0。

**方法:**按照以下步骤解决问题:

*   从数组 **arr[]** 中移除 **K** 元素后，初始化变量 **res** 以存储最大反转次数。
*   初始化一个长度为 **N** 的二进制字符串 **S** ，以存储要从数组**arr【】**中考虑哪些**(N–K)**元素。
*   将 **0** 存储在**【0，K–1】**位置，表示 **K** 已移除的元素，将 1 存储在**【K，N–1】**位置，表示字符串 **S** 中的**(N–K)**所选元素。
*   [生成字符串](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/) **S** 的所有排列，并执行以下操作:
    *   初始化一个数组 **v** 按照字符串 **S** 存储从**arr【】**中选择的**(N–K)**元素。
    *   [统计数组](https://www.geeksforgeeks.org/counting-inversions/) **v** 中的逆序数，存储在 **cnt** 中。
    *   将 **res** 更新为最大 **res** 和 **cnt** 。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of inversions after K removals
void maximizeInversions(int a[], int n,
                        int k)
{
    // Initialize a binary string
    string s;

    // Iterate over range [0, K]
    for (int i = 0; i < k; i++)
    {

        // Append 0 to the string
        s += "0";
    }

    for (int i = k; i < n; i++)
    {

        // Append 1 to the string
        s += "1";
    }

    // Stores the maximum number of
    // inversions after K removals
    int res = 0;

    // Generate all permutations
    // of string s
    do
    {

        // Stores the current array
        vector<int> v;

        // Stores number of inversions
        // of the current array
        int cnt = 0;

        for (int i = 0; i < n; i++)
        {
            if (s[i] == '1')
                v.push_back(a[i]);
        }

        // Find the number of inversions
        // in the array v
        for (int i = 0;
             i < v.size() - 1; i++)
        {

            for (int j = i + 1;
                 j < v.size(); j++)
            {

                // Condition to check if the
                // number of pairs satisfy
                // required condition
                if (v[i] >= v[j])

                    // Increment the count
                    cnt++;
            }
        }

        // Update res
        res = max(res, cnt);

    }
  while (next_permutation(s.begin(),
                              s.end()));

    // Print the result
    cout << res;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    // Function Call
    maximizeInversions(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find the maximum number
// of inversions after K removals
static void maximizeInversions(int a[], int n,
                                int k)
{
    // Initialize a binary String
    String s="";

    // Iterate over range [0, K]
    for (int i = 0; i < k; i++)
    {

        // Append 0 to the String
        s += "0";
    }

    for (int i = k; i < n; i++)
    {

        // Append 1 to the String
        s += "1";
    }

    // Stores the maximum number of
    // inversions after K removals
    int res = 0;

    // Generate all permutations
    // of String s
    do
    {

        // Stores the current array
        Vector<Integer> v = new Vector<>();

        // Stores number of inversions
        // of the current array
        int cnt = 0;

        for (int i = 0; i < n; i++)
        {
            if (s.charAt(i) == '1')
                v.add(a[i]);
        }

        // Find the number of inversions
        // in the array v
        for (int i = 0;
             i < v.size() - 1; i++)
        {

            for (int j = i + 1;
                 j < v.size(); j++)
            {

                // Condition to check if the
                // number of pairs satisfy
                // required condition
                if (v.get(i) >= v.get(j))

                    // Increment the count
                    cnt++;
            }
        }

        // Update res
        res = Math.max(res, cnt);

    }
  while (next_permutation(s));

    // Print the result
    System.out.print(res);
}

static boolean next_permutation(String str)
{
    char []p = str.toCharArray();
      for (int a = p.length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
          for (int b = p.length - 1;; --b)
            if (p[b] > p[a])
            {
              char t = p[a];
              p[a] = p[b];
              p[b] = t;
              for (++a, b = p.length - 1;
                   a < b; ++a, --b)
              {
                t = p[a];
                p[a] = p[b];
                p[b] = t;
              }
              return false;
            }
      return true;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 4, 1 };
    int N = arr.length;
    int K = 2;

    // Function Call
    maximizeInversions(arr, N, K);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
def next_permutation(Str):

    p = list(Str)

    for a in range(len(p) - 2, -1, -1):
        if p[a] < p[a + 1]:
            b = len(p) - 1

            while True:
                if p[b] > p[a]:
                    t = p[a]
                    p[a] = p[b]
                    p[b] = t
                    a += 1
                    b = len(p) - 1

                    while a < b:
                        t = p[a]
                        p[a] = p[b]
                        p[b] = t
                        a += 1
                        b -= 1

                    return False

                b -= 1

    return True

# Function to find the maximum number
# of inversions after K removals
def maximizeInversions(a, n, k):

    # Initialize a binary string
    s = ""

    # Iterate over range [0, K]
    for i in range(k):

        # Append 0 to the string
        s += "0"

    for i in range(k, n):

        # Append 1 to the string
        s += "1"

    # Stores the maximum number of
    # inversions after K removals
    res = 0

    # Generate all permutations
    # of string s
    while (True):

        # Stores the current array
        v = []

        # Stores number of inversions
        # of the current array
        cnt = 0

        for i in range(n):
            if (s[i] == '1'):
                v.append(a[i])

        # Find the number of inversions
        # in the array v
        for i in range(len(v) - 1):
            for j in range(i + 1, len(v)):

                # Condition to check if the
                # number of pairs satisfy
                # required condition
                if (v[i] >= v[j]):

                    # Increment the count
                    cnt += 1

        # Update res
        res = max(res, cnt)

        if (not next_permutation(s)):
            break

    # Print the result
    print(res)

# Driver Code
arr = [ 2, 3, 4, 1 ]
N = len(arr)
K = 2

# Function Call
maximizeInversions(arr, N, K)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the maximum number
// of inversions after K removals
static void maximizeInversions(int []a, int n,
                                int k)
{
    // Initialize a binary String
    String s="";

    // Iterate over range [0, K]
    for (int i = 0; i < k; i++)
    {

        // Append 0 to the String
        s += "0";
    }

    for (int i = k; i < n; i++)
    {

        // Append 1 to the String
        s += "1";
    }

    // Stores the maximum number of
    // inversions after K removals
    int res = 0;

    // Generate all permutations
    // of String s
    do
    {

        // Stores the current array
        List<int> v = new List<int>();

        // Stores number of inversions
        // of the current array
        int cnt = 0;

        for (int i = 0; i < n; i++)
        {
            if (s[i] == '1')
                v.Add(a[i]);
        }

        // Find the number of inversions
        // in the array v
        for (int i = 0;
             i < v.Count - 1; i++)
        {

            for (int j = i + 1;
                 j < v.Count; j++)
            {

                // Condition to check if the
                // number of pairs satisfy
                // required condition
                if (v[i] >= v[j])

                    // Increment the count
                    cnt++;
            }
        }

        // Update res
        res = Math.Max(res, cnt);

    }
  while (next_permutation(s));

    // Print the result
    Console.Write(res);
}

static bool next_permutation(String str)
{
    char []p = str.ToCharArray();
      for (int a = p.Length - 2; a >= 0; --a)
        if (p[a] < p[a + 1])
          for (int b = p.Length - 1;; --b)
            if (p[b] > p[a])
            {
              char t = p[a];
              p[a] = p[b];
              p[b] = t;
              for (++a, b = p.Length - 1;
                   a < b; ++a, --b)
              {
                t = p[a];
                p[a] = p[b];
                p[b] = t;
              }
              return false;
            }
      return true;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 4, 1 };
    int N = arr.Length;
    int K = 2;

    // Function Call
    maximizeInversions(arr, N, K);
}
}

// This code contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum number
// of inversions after K removals
function maximizeInversions(a, n, k)
{
    // Initialize a binary String
    let s="";

    // Iterate over range [0, K]
    for (let i = 0; i < k; i++)
    {

        // Append 0 to the String
        s += "0";
    }

    for (let i = k; i < n; i++)
    {

        // Append 1 to the String
        s += "1";
    }

    // Stores the maximum number of
    // inversions after K removals
    let res = 0;

    // Generate all permutations
    // of String s
    do
    {

        // Stores the current array
        let v = [];

        // Stores number of inversions
        // of the current array
        let cnt = 0;

        for (let i = 0; i < n; i++)
        {
            if (s[i] == '1')
                v.push(a[i]);
        }

        // Find the number of inversions
        // in the array v
        for (let i = 0;
             i < v.length - 1; i++)
        {

            for (let j = i + 1;
                 j < v.length; j++)
            {

                // Condition to check if the
                // number of pairs satisfy
                // required condition
                if (v[i] >= v[j])

                    // Increment the count
                    cnt++;
            }
        }

        // Update res
        res = Math.max(res, cnt);

    }
    while (next_permutation(s));

    // Print the result
    document.write(res);
}

function next_permutation(str)
{
      for (let a = str.length - 2; a >= 0; --a)
        if (str[a] < str[a + 1])
          for (let b = str.length - 1;; --b)
            if (str[b] > str[a])
            {
              let t = str[a];
              str[a] = str[b];
              str[b] = t;
              for (++a, b = str.length - 1;
                   a < b; ++a, --b)
              {
                t = str[a];
                str[a] = str[b];
                str[b] = t;
              }
              return false;
            }
      return true;
}

// Driver Code

    let arr = [ 2, 3, 4, 1 ];
    let N = arr.length;
    let K = 2;

    // Function Call
    maximizeInversions(arr, N, K);

    // This code is contributed by Dharanendra L V.

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O((N！)*(N–K)<sup>2</sup>)*
***辅助空间:** O(N)*