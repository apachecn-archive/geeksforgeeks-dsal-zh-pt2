# 长度至少为 K 的给定字符串数组中的等值线字符串的计数

> 原文:[https://www . geeksforgeeks . org/给定长度至少为-k 的字符串数组中的等值字符串计数/](https://www.geeksforgeeks.org/count-of-isogram-strings-in-given-array-of-strings-with-length-at-least-k/)

给定一个包含 **N** 字符串和一个整数 **K** 的数组**arr【】**，任务是找出长度为[等值线](https://www.geeksforgeeks.org/check-if-all-given-strings-are-isograms-or-not/)和至少长度为 **K** 的字符串数量。

**示例:**

> **输入:**arr[]= {“abcd”、“der”、“erty”}，K = 4
> **输出:** 2
> **解释:**所有给定的字符串都是等长图，但只有“ABCD”和“erty”的长度至少为 K，因此计数为 2
> 
> **输入:**arr[]= {“ag”、“bka”、“lkmn”、“asdfg”}，K = 2
> **输出:** 4
> **说明:**所有字符串都是等长图，每个字符串都是长度> =K，因此计数为 4。

**方法:**这个问题可以通过存储所有字符的频率或者使用[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)数据结构来解决。如果一个字符串中没有字母出现不止一次，那么这个字符串就是一个[等值线图](https://www.geeksforgeeks.org/check-if-all-given-strings-are-isograms-or-not/)。按照以下步骤解决给定的问题。

*   遍历字符串数组 **arr[]** ，对于每个字符串
*   创建字符的频率图。
*   如果任何字符的频率大于 **1** ，或者如果字符串的长度小于 **K** ，则跳过当前字符串。
*   否则，如果没有字符的频率大于 **1** ，并且字符串的长度小于 **K** ，则递增答案的**计数**。
*   遍历所有字符串时，打印答案中存储的**计数**。

下面是上述方法的实现。

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a string
// is an isogram or not
bool isIsogram(string s)
{
    // To store the frequencies
    vector<int> freq(26, 0);

    for (char c : s) {
        freq++;

        if (freq > 1) {
            return false;
        }
    }

    return true;
}

// Function to check if array arr contains
// all isograms or not
int allIsograms(vector<string>& arr, int K)
{
    int ans = 0;
    for (string x : arr) {
        if (isIsogram(x) && x.length() >= K) {
            ans++;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    vector<string> arr = { "abcd", "der", "erty" };
    int K = 4;

    // Function call and printing the answer
    cout << allIsograms(arr, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG {

    // Function to check if a string
    // is an isogram or not
    static boolean isIsogram(String s)
    {
        // To store the frequencies
        int[] freq = new int[26];

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            freq++;

            if (freq > 1) {
                return false;
            }
        }

        return true;
    }

    // Function to check if array arr contains
    // all isograms or not
    static int allIsograms(String[] arr, int K)
    {
        int ans = 0;
        for (String x : arr) {
            if (isIsogram(x) && x.length() >= K) {
                ans++;
            }
        }

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String arr[] = { "abcd", "der", "erty" };
        int K = 4;

        // Function call and printing the answer

        System.out.println(allIsograms(arr, K));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to check if a string
# is an isogram or not
def isIsogram (s):

    # To store the frequencies
    freq = [0] * 26

    for c in s:
        freq[ord(c) - ord("a")] += 1

        if (freq[s.index(c)] > 1):
            return False

    return True

# Function to check if array arr contains
# all isograms or not
def allIsograms (arr, K):
    ans = 0
    for x in arr:
        if isIsogram(x) and len(x) >= K:
            ans += 1

    return ans

# Driver Code
arr = ["abcd", "der", "erty"]
K = 4

# Function call and printing the answer
print(allIsograms(arr, K))

# This code is contributed by Saurabh jaiswal
```

## C#

```
// C# code for the above approach
using System;

class GFG{

// Function to check if a string
// is an isogram or not
static bool isIsogram(string s)
{

    // To store the frequencies
    int[] freq = new int[26];

    for(int i = 0; i < s.Length; i++)
    {
        char c = s[i];
        freq++;

        if (freq > 1)
        {
            return false;
        }
    }
    return true;
}

// Function to check if array arr contains
// all isograms or not
static int allIsograms(string[] arr, int K)
{
    int ans = 0;
    foreach(string x in arr)
    {
        if (isIsogram(x) && x.Length >= K)
        {
            ans++;
        }
    }
    return ans;
}

// Driver Code
public static void Main(string[] args)
{
    string[] arr = { "abcd", "der", "erty" };
    int K = 4;

    // Function call and printing the answer
    Console.WriteLine(allIsograms(arr, K));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach

    // Function to check if a string
    // is an isogram or not
    const isIsogram = (s) => {

        // To store the frequencies
        let freq = new Array(26).fill(0);

        for (let c in s) {
            freq[s.charCodeAt(c) - "a".charCodeAt(0)]++;

            if (freq > 1) {
                return false;
            }
        }

        return true;
    }

    // Function to check if array arr contains
    // all isograms or not
    const allIsograms = (arr, K) => {
        let ans = 0;
        for (let x in arr) {
            if (isIsogram(x) && arr[x].length >= K) {
                ans++;
            }
        }

        return ans;
    }

    // Driver Code
    let arr = ["abcd", "der", "erty"];
    let K = 4;

    // Function call and printing the answer
    document.write(allIsograms(arr, K));

    // This code is contributed by rakeshsahni
</script>
```

**Output**

```
2
```

**时间复杂度:** O(N*M)，其中 **N** 为阵的大小， **M** 为最长弦的大小。

**辅助空间:** O(1)。