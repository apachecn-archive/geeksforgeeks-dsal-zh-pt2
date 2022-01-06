# 计算数组中不同字符小于或等于 M 的字符串数

> 原文:[https://www . geeksforgeeks . org/count-数组中不同字符小于等于 m 的字符串数/](https://www.geeksforgeeks.org/count-the-number-of-strings-in-an-array-whose-distinct-characters-are-less-than-equal-to-m/)

给定一个字符串数组 **arr[]** 和一个整数 **M** ，任务是对不同字符数小于 **M** 的字符串进行计数。

**示例:**

> **输入:**arr[]= {“ADAM”、“JOHNSON”、“COOL”}，M = 3
> **输出:** 2
> **解释:**
> 有两个这样的字符串，其不同字符的计数小于 M。
> 不同字符的计数(“ADAM”)= 3
> 不同字符的计数(“COOL”)= 3
> 
> **输入:** arr[] = {“草食动物”、“飞机”、“GEEKSFORGEEKS”}，M = 7
> **输出:** 2
> **解释:**
> 有两个这样的字符串，其不同字符的计数小于 M。
> 不同字符的计数(“飞机”)= 7
> 不同字符的计数(“GEEKSFORGEEKS”)= 7

**方法:**思想是迭代所有字符串，[找到字符串的不同字符](https://www.geeksforgeeks.org/print-all-distinct-characters-of-a-string-in-order-3-methods/)，如果字符串中不同字符的计数小于或等于 M 的给定值，那么将计数增加 1。
以下是上述办法的实施情况:

## C++

```
// C++ implementation to count
// the number of strings in the
// array whose distinct characters
// is less than or equal to M
#include <bits/stdc++.h>
#include <set>
using namespace std;

// Function to count the strings
// whose distinct characters
// count is less than M
void distinct(string S[], int M, int n)
{
    int count = 0;

    // Loop to iterate over all
    // the strings of the array
    for(int i = 0; i < n; i++)
    {

        // Distinct characters in the
        // String with the help of set
        set<char> set1;
        for(int j = 0; j < S[i].length(); j++)
        {
            if (set1.find(S[i][j]) == set1.end())
                set1.insert(S[i][j]);
        }
        int c = set1.size();

        // Checking if its less
        // than or equal to M
        if (c <= M)
            count += 1;
    }
    cout << (count);
}

// Driver Code
int main()
{
    string S[] = { "HERBIVORES", "AEROPLANE",
                   "GEEKSFORGEEKS" };
    int M = 7;
    int n = sizeof(S) / sizeof(S[0]);

    distinct(S, M, n);

    return 0;
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count
// the number of strings in the
// array whose distinct characters
// is less than or equal to M
import java.util.*;

class GFG{

// Function to count the strings
// whose distinct characters
// count is less than M
public static void distinct(String[] S, int M)
{
    int count = 0;

    // Loop to iterate over all
    // the strings of the array
    for(int i = 0; i < S.length; i++)
    {

    // Distinct characters in the
    // String with the help of set
    Set<Character> set = new HashSet<>();
    for(int j = 0; j < S[i].length(); j++)
    {
        if (!set.contains(S[i].charAt(j)))
            set.add(S[i].charAt(j));
    }
    int c = set.size();

    // Checking if its less
    // than or equal to M
    if (c <= M)
        count += 1;
    }
    System.out.println(count);
}

// Driver Code
public static void main(String[] args)
{
    String S[] = { "HERBIVORES", "AEROPLANE",
                "GEEKSFORGEEKS" };
    int M = 7;

    distinct(S, M);
}
}

// This code is contributed by jrishabh99
```

## 蟒蛇 3

```
# Python3 implementation to count
# the number of strings in the
# array whose distinct characters
# is less than or equal to M

# Function to count the strings
# whose distinct characters
# count is less than M
def distinct(S, M):
    count = 0

    # Loop to iterate over all
    # the strings of the array
    for i in range (len(S)):

        # Distinct characters in the
        # String with the help of set
        c = len(set([d for d in S[i]]))

        # Checking if its less
        # than or equal to M
        if (c <= M):
            count += 1
    print(count)

# Driver Code
if __name__== '__main__':

    S = ["HERBIVORES", "AEROPLANE",
        "GEEKSFORGEEKS"]
    M = 7

    distinct(S, M)
```

## C#

```
// C# implementation to count
// the number of strings in the
// array whose distinct characters
// is less than or equal to M
using System;
using System.Collections.Generic;

class GFG{

// Function to count the strings
// whose distinct characters
// count is less than M
public static void distinct(string[] S, int M)
{
    int count = 0;

    // Loop to iterate over all
    // the strings of the array
    for(int i = 0; i < S.Length; i++)
    {

        // Distinct characters in the
        // String with the help of set
        HashSet<char> set = new HashSet<char>();
        for(int j = 0; j < S[i].Length; j++)
        {
            if (!set.Contains(S[i][j]))
                set.Add(S[i][j]);
        }
        int c = set.Count;

        // Checking if its less
        // than or equal to M
        if (c <= M)
            count += 1;
    }
    Console.Write(count);
}

// Driver Code
public static void Main(string[] args)
{
    string []S = { "HERBIVORES", "AEROPLANE",
                   "GEEKSFORGEEKS" };
    int M = 7;

    distinct(S, M);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript implementation to count
// the number of strings in the
// array whose distinct characters
// is less than or equal to M

// Function to count the strings
// whose distinct characters
// count is less than M
function distinct(S, M, n) {
    let count = 0;

    // Loop to iterate over all
    // the strings of the array
    for (let i = 0; i < n; i++) {

        // Distinct characters in the
        // String with the help of set
        let set1 = new Set();
        for (let j = 0; j < S[i].length; j++) {
            if (!set1.has(S[i][j]))
                set1.add(S[i][j]);
        }
        let c = set1.size;

        // Checking if its less
        // than or equal to M
        if (c <= M)
            count += 1;
    }
    document.write(count);
}

// Driver Code

let S = ["HERBIVORES", "AEROPLANE",
    "GEEKSFORGEEKS"];
let M = 7;
let n = S.length;

distinct(S, M, n);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
2
```

**性能分析:**

*   **时间复杂度:** O(N * M)，其中 M 为字符串的最大长度。
*   **辅助空间:** O(1)