# 给定二进制字符串中 0 和 1 的比率相等的子字符串的计数，直到第一个索引

> 原文:[https://www . geeksforgeeks . org/给定二进制字符串中具有 0 和 1 等比率的子字符串计数/third-with-index/](https://www.geeksforgeeks.org/count-of-substrings-with-equal-ratios-of-0s-and-1s-till-ith-index-in-given-binary-string/)

给定一个二进制字符串 **S** ，任务是打印**子串**的**最大**个数，其 **0s** 和 **1s** 的比例相等，直到从开始的**带有**索引。

**示例:**

> **输入:** S = "110001"
> **输出:** {1，2，1，1，2}
> **解释:**给定的字符串可以划分为以下相等的子字符串:
> 
> *   到索引 0:“1”的有效子字符串，可能的子字符串数量= 1
> *   到索引 1 的有效子字符串:“1”、“B”，可能的子字符串数量= 2
> *   截至索引 2 的有效子字符串:“110”，可能的子字符串数量= 1
> *   截至索引 3 的有效子字符串:“1100”，可能的子字符串数量= 1
> *   截至索引 4 的有效子字符串:“11000”，可能的子字符串数量= 1
> *   截至索引 5 的有效子字符串:“1100”、“01”，可能的子字符串数量= 2
>     
> 
> **输入:** S = "010100001"
> **输出:** {1，1，1，2，1，2，1，1，1，3}

**方法:**可以使用[数学概念](https://www.geeksforgeeks.org/math-in-competitive-programming/) & [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 存储配对的**频率**来解决任务，按照以下步骤解决问题:

1.  为出现的 **0s** 和 **1s** 分别创建两个 **pre0[]** 和 **pre1[]** 前缀数组。
2.  对于每个前缀，用一对(a，b)标记，其中 a =该前缀中 **'0'** 的频率，b =**' 1 '**的频率。将 a 和 b 除以 [gcd(a，b)](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) 得到最简单的形式。
3.  迭代所有**前缀**，并将前缀的答案存储为该对**出现的当前次数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to retuan a prefix array of
// equal partitions of the given string
// consisting of 0s and 1s
void equalSubstrings(string s)
{
    // Length of the string
    int n = s.size();

    // Prefix arrays for 0s and 1s
    int pre0[n] = { 0 }, pre1[n] = { 0 };

    // If character at index 0 is 0
    if (s[0] == '0') {
        pre0[0] = 1;
    }

    // If character at index 0 is 1
    else {
        pre1[0] = 1;
    }

    // Filling the prefix arrays
    for (int i = 1; i < n; i++) {
        if (s[i] == '0') {
            pre0[i] = pre0[i - 1] + 1;
            pre1[i] = pre1[i - 1];
        }
        else {
            pre0[i] = pre0[i - 1];
            pre1[i] = pre1[i - 1] + 1;
        }
    }

    // Vector to store the answer
    vector<int> ans;

    // Map to store the ratio
    map<pair<int, int>, int> mp;

    for (int i = 0; i < n; i++) {
        // Find the gcd of pre0[i] and pre1[i]
        int x = __gcd(pre0[i], pre1[i]);

        // Converting the elements in
        // simplest form
        int l = pre0[i] / x, r = pre1[i] / x;

        // Update the value in map
        mp[{ l, r }]++;

        // Store this in ans
        ans.push_back(mp[{ l, r }]);
    }
    // Return the ans vector
    for (auto i : ans)
        cout << i << " ";
}

// Driver Code
int main()
{
    string s = "001110";
    equalSubstrings(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;

class GFG
{

    // Function to retuan a prefix array of
    // equal partitions of the given string
    // consisting of 0s and 1s
    public static void equalSubstrings(String s)
    {

        // Length of the string
        int n = s.length();

        // Prefix arrays for 0s and 1s
        int[] pre0 = new int[n];
        int[] pre1 = new int[n];

        Arrays.fill(pre0, 0);
        Arrays.fill(pre1, 0);

        // If character at index 0 is 0
        if (s.charAt(0) == '0') {
            pre0[0] = 1;
        }

        // If character at index 0 is 1
        else {
            pre1[0] = 1;
        }

        // Filling the prefix arrays
        for (int i = 1; i < n; i++) {
            if (s.charAt(i) == '0') {
                pre0[i] = pre0[i - 1] + 1;
                pre1[i] = pre1[i - 1];
            } else {
                pre0[i] = pre0[i - 1];
                pre1[i] = pre1[i - 1] + 1;
            }
        }

        // Vector to store the answer
        ArrayList<Integer> ans = new ArrayList<Integer>();

        // Map to store the ratio
        HashMap<String, Integer> mp = new HashMap<String, Integer>();

        for (int i = 0; i < n; i++)
        {

            // Find the gcd of pre0[i] and pre1[i]
            int x = __gcd(pre0[i], pre1[i]);

            // Converting the elements in
            // simplest form
            int l = pre0[i] / x, r = pre1[i] / x;

            String key = l + "," + r;

            // Update the value in map
            if (mp.containsKey(key))
                mp.put(key, mp.get(key) + 1);
            else
                mp.put(key, 1);

            // Store this in ans
            ans.add(mp.get(key));
        }

        // Return the ans vector
        for (int i : ans)
            System.out.print(i + " ");
    }

    public static int __gcd(int a, int b) {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Driver Code
    public static void main(String args[]) {
        String s = "001110";
        equalSubstrings(s);

    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python program for the above approach
def __gcd(a, b):
    if (b == 0):
        return a
    return __gcd(b, a % b)

# Function to retuan a prefix array of
# equal partitions of the given string
# consisting of 0s and 1s
def equalSubstrings(s):

    # Length of the string
    n = len(s)

    # Prefix arrays for 0s and 1s
    pre0 = [0] * n
    pre1 = [0] * n

    # If character at index 0 is 0
    if (s[0] == '0'):
        pre0[0] = 1

    # If character at index 0 is 1
    else:
        pre1[0] = 1

    # Filling the prefix arrays
    for i in range(1, n):
        if (s[i] == '0'):
            pre0[i] = pre0[i - 1] + 1
            pre1[i] = pre1[i - 1]
        else:
            pre0[i] = pre0[i - 1]
            pre1[i] = pre1[i - 1] + 1

    # Vector to store the answer
    ans = []

    # Map to store the ratio
    mp = {}

    for i in range(n):
        # Find the gcd of pre0[i] and pre1[i]
        x = __gcd(pre0[i], pre1[i])

        # Converting the elements in
        # simplest form
        l = pre0[i] // x
        r = pre1[i] // x

        # Update the value in map
        if (f'[{l}, {r}]' in mp):
            mp[f'[{l}, {r}]'] += 1
        else:
            mp[f'[{l}, {r}]'] = 1

        # Store this in ans
        ans.append(mp[f'[{l}, {r}]'])

    # Return the ans vector
    for i in ans:
        print(i, end=" ")

# Driver Code
s = "001110"
equalSubstrings(s)

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to retuan a prefix array of
    // equal partitions of the given string
    // consisting of 0s and 1s
    public static void equalSubstrings(string s)
    {

        // Length of the string
        int n = s.Length;

        // Prefix arrays for 0s and 1s
        int[] pre0 = new int[n];
        int[] pre1 = new int[n];

        // Arrays.fill(pre0, 0);
        // Arrays.fill(pre1, 0);

        // If character at index 0 is 0
        if (s[0] == '0') {
            pre0[0] = 1;
        }

        // If character at index 0 is 1
        else {
            pre1[0] = 1;
        }

        // Filling the prefix arrays
        for (int i = 1; i < n; i++) {
            if (s[i] == '0') {
                pre0[i] = pre0[i - 1] + 1;
                pre1[i] = pre1[i - 1];
            }
            else {
                pre0[i] = pre0[i - 1];
                pre1[i] = pre1[i - 1] + 1;
            }
        }

        // Vector to store the answer
        List<int> ans = new List<int>();

        // Map to store the ratio
        Dictionary<string, int> mp
            = new Dictionary<string, int>();

        for (int i = 0; i < n; i++) {

            // Find the gcd of pre0[i] and pre1[i]
            int x = __gcd(pre0[i], pre1[i]);

            // Converting the elements in
            // simplest form
            int l = pre0[i] / x, r = pre1[i] / x;

            string key = l + "," + r;

            // Update the value in map
            if (mp.ContainsKey(key))
                mp[key] += 1;
            else
                mp[key] = 1;

            // Store this in ans
            ans.Add(mp[key]);
        }

        // Return the ans vector
        foreach(int i in ans) Console.Write(i + " ");
    }

    public static int __gcd(int a, int b)
    {
        if (b == 0)
            return a;
        return __gcd(b, a % b);
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string s = "001110";
        equalSubstrings(s);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach
    const __gcd = (a, b) => {
        if (b == 0) return a;
        return __gcd(b, a % b)
    }

    // Function to retuan a prefix array of
    // equal partitions of the given string
    // consisting of 0s and 1s

    const equalSubstrings = (s) => {
        // Length of the string
        let n = s.length;

        // Prefix arrays for 0s and 1s
        let pre0 = new Array(n).fill(0);
        let pre1 = new Array(n).fill(0);

        // If character at index 0 is 0
        if (s[0] == '0') {
            pre0[0] = 1;
        }

        // If character at index 0 is 1
        else {
            pre1[0] = 1;
        }

        // Filling the prefix arrays
        for (let i = 1; i < n; i++) {
            if (s[i] == '0') {
                pre0[i] = pre0[i - 1] + 1;
                pre1[i] = pre1[i - 1];
            }
            else {
                pre0[i] = pre0[i - 1];
                pre1[i] = pre1[i - 1] + 1;
            }
        }

        // Vector to store the answer
        ans = [];

        // Map to store the ratio
        mp = {};

        for (let i = 0; i < n; i++) {
            // Find the gcd of pre0[i] and pre1[i]
            let x = __gcd(pre0[i], pre1[i]);

            // Converting the elements in
            // simplest form
            let l = pre0[i] / x, r = pre1[i] / x;

            // Update the value in map
            if ([l, r] in mp) mp[[l, r]] += 1
            else mp[[l, r]] = 1

            // Store this in ans
            ans.push(mp[[l, r]]);
        }
        // Return the ans vector
        for (let i in ans)
            document.write(`${ans[i]} `);
    }

    // Driver Code

    let s = "001110";
    equalSubstrings(s);

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
1 2 1 1 1 2 
```

***时间复杂度:**T3】O(nlogn)
T5】T6】辅助空间:T8】O(n)*