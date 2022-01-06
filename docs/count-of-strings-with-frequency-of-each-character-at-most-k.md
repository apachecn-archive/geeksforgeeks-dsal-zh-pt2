# 每个字符频率最多为 K 的字符串数

> 原文:[https://www . geeksforgeeks . org/最多每个字符出现频率为 k 的字符串计数/](https://www.geeksforgeeks.org/count-of-strings-with-frequency-of-each-character-at-most-k/)

给定一个包含**N**T6】字符串和一个整数 **K** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)的个数，每个字符的出现频率最多为 **K**

**示例:**

> **输入:**arr[]= {“abab”、“derdee”、“erre”}，K = 2
> **输出:** 2
> **说明:**字符频率最多为 2 的字符串为“abab”、“erre”。因此计数为 2
> 
> **输入:**arr[]= {“ag”、“ka”、“nanna”}，K = 3
> **输出:** 1

**方法:**想法是遍历字符串数组，为每个字符串创建一个[字符频率图](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)。任何字符的频率大于 **K** 的地方，跳过当前字符串。否则，如果没有字符的频率超过 **K** ，则增加**回答**的次数。遍历所有字符串时，打印存储在**答案**中的计数。按照以下步骤解决问题:

*   定义一个函数**为子程序(字符串 s，int K)** ，并执行以下任务:
    *   [用值 **0 初始化矢量**](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **频率【26】**。
    *   使用变量 **c** 遍历字符串 **s** ，并执行以下任务:
        *   将**频率**的计数增加 **1。**
    *   [迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0。26)** 使用变量 **i** 并执行以下任务:
        *   如果 **freq[i]** 大于 **K** ，则返回 **false。**
    *   执行上述步骤后，返回**真**作为答案。
*   将变量**和**初始化为 **0** 来存储答案。
*   使用变量 **x** 遍历数组 **arr[]** ，并执行以下任务:
    *   调用函数**为程序(x，K)** ，如果函数返回**真**，则将 **ans** 的计数增加 **1。**
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if a string
// is an duogram or not
bool isDuogram(string s, int K)
{

    // Array to store the frequency
    // of characters
    vector<int> freq(26, 0);

    // Count the frequency
    for (char c : s) {
        freq++;
    }

    // Check if the frequency is greater
    // than K or not
    for (int i = 0; i < 26; i++)
        if (freq[i] > K)
            return false;

    return true;
}

// Function to check if array arr contains
// all duograms or not
int countDuograms(vector<string>& arr, int K)
{

    // Store the answer
    int ans = 0;

    // Traverse the strings
    for (string x : arr) {

        // Check the condition
        if (isDuogram(x, K)) {
            ans++;
        }
    }

    return ans;
}

// Driver Code
int main()
{
    vector<string> arr = { "abab", "derdee", "erre" };
    int K = 2;

    cout << countDuograms(arr, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check if a String
// is an duogram or not
static boolean isDuogram(String s, int K)
{

    // Array to store the frequency
    // of characters
   int []freq = new int[26];

    // Count the frequency
    for (char c : s.toCharArray()) {
        freq++;
    }

    // Check if the frequency is greater
    // than K or not
    for (int i = 0; i < 26; i++)
        if (freq[i] > K)
            return false;

    return true;
}

// Function to check if array arr contains
// all duograms or not
static int countDuograms(String[] arr, int K)
{

    // Store the answer
    int ans = 0;

    // Traverse the Strings
    for (String x : arr) {

        // Check the condition
        if (isDuogram(x, K)) {
            ans++;
        }
    }

    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String []arr = { "abab", "derdee", "erre" };
    int K = 2;

    System.out.print(countDuograms(arr, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to check if a string
# is an duogram or not
def isDuogram (s, K) :
    # Array to store the frequency
    # of characters
    freq = [0] * 26

    # Count the frequency
    for c in s:
        freq[ord(c) - ord("a")] += 1

    # Check if the frequency is greater
    # than K or not
    for i in range(26):
        if (freq[i] > K):
            return False
    return True

# Function to check if array arr contains
# all duograms or not
def countDuograms  (arr, K) :

    # Store the answer
    ans = 0
    # Traverse the strings
    for x in arr:
        # Check the condition
        if (isDuogram(x, K)):
            ans += 1
    return ans

# Driver Code
arr = ["abab", "derdee", "erre"]
K = 2

print(countDuograms(arr, K))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to check if a String
    // is an duogram or not
    static bool isDuogram(String s, int K)
    {

        // Array to store the frequency
        // of characters
        int[] freq = new int[26];

        // Count the frequency
        foreach (char c in s.ToCharArray())
        {
            freq[(int)c - (int)'a']++;
        }

        // Check if the frequency is greater
        // than K or not
        for (int i = 0; i < 26; i++)
            if (freq[i] > K)
                return false;

        return true;
    }

    // Function to check if array arr contains
    // all duograms or not
    static int countDuograms(String[] arr, int K)
    {

        // Store the answer
        int ans = 0;

        // Traverse the Strings
        foreach (String x in arr)
        {

            // Check the condition
            if (isDuogram(x, K))
            {
                ans++;
            }
        }

        return ans;
    }

    // Driver Code
    public static void Main()
    {
        String[] arr = { "abab", "derdee", "erre" };
        int K = 2;

        Console.Write(countDuograms(arr, K));
    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to check if a string
    // is an duogram or not
    const isDuogram = (s, K) => {

        // Array to store the frequency
        // of characters
        let freq = new Array(26).fill(0);

        // Count the frequency
        for (let c in s) {
            freq[s.charCodeAt(c) - "a".charCodeAt(0)]++;
        }

        // Check if the frequency is greater
        // than K or not
        for (let i = 0; i < 26; i++)
            if (freq[i] > K)
                return false;

        return true;
    }

    // Function to check if array arr contains
    // all duograms or not
    const countDuograms = (arr, K) => {

        // Store the answer
        let ans = 0;

        // Traverse the strings
        for (let x in arr) {

            // Check the condition
            if (isDuogram(arr[x], K)) {
                ans++;
            }
        }

        return ans;
    }

    // Driver Code
    let arr = ["abab", "derdee", "erre"];
    let K = 2;

    document.write(countDuograms(arr, K));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
2
```

***时间复杂度:** O(N*M)，其中 N 是数组的大小，M 是最长字符串的大小*
***辅助空间:** O(1)*