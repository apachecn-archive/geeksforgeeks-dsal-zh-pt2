# 由每个字符具有偶数频率的连接形成的字符串的最大长度

> 原文:[https://www . geesforgeks . org/每个字符具有偶数频率的最大字符串长度/](https://www.geeksforgeeks.org/maximum-length-of-string-formed-by-concatenation-having-even-frequency-of-each-character/)

给定 **N** [字符串](https://www.geeksforgeeks.org/python-strings/)，打印该字符串的最大长度以及由任意 **N** 字符串串联而成的字符串，使得该字符串中的每个字母出现偶数次

**示例:**

> **输入:** N = 5，str =[“ABAB”、“ABF”、“CDA”、“AD”、“CCC”]
> **输出:** : ABABCDAADCCC 12
> **说明:**串接形成的字符串为 ABABCDAADCCC。字符串中的每个字母出现偶数次
> 
> **输入:** N = 3，str =[“AB”、“BC”、“CA”]
> **输出:** ABBCCA 6
> **说明:**所有 3 个字符串串联形成的字符串为 ABBCCA

**逼近**:给定的问题可以通过[递归](https://www.geeksforgeeks.org/recursion/)和[回溯](https://www.geeksforgeeks.org/backtracking-algorithms/)来解决。其思想是要么在每次迭代中包含字符串，要么排除字符串。包含一个字符串后，将计算串联字符串中所有字符的频率。如果所有字符的频率是偶数，我们更新最大长度 **max。**可以按照以下步骤解决问题:

*   将变量 **max** 初始化为 0，以计算所有字符频率均为偶数的串联字符串的最大长度
*   初始化[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **ans1** 以存储最大长度的串联字符串，所有字符具有偶数频率
*   递归调用的基本情况是返回，如果**索引**等于输入字符串列表的大小
*   每次递归调用时，我们都会执行以下操作:
    *   包括字符串，并检查串联字符串的字符频率是否均匀
        *   如果频率均匀，更新 **max** 和 **ans1**
        *   递增索引并进行下一次递归调用
    *   排除字符串，增加索引并进行下一次递归调用

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;
int maxi = 0;
string ans1 = "";

// Function to check the string
void calculate(string ans)
{

    int dp[26] = { 0 };
    for (int i = 0; i < ans.length(); ++i) {

        // Count the frequency
        // of the string
        dp[ans[i] - 'A']++;
    }

    // Check the frequency of the string
    for (int i = 0; i < 26; ++i) {
        if (dp[i] % 2 == 1) {
            return;
        }
    }
    if (maxi < ans.length()) {

        // Store the length
        // of the new String
        maxi = ans.length();
        ans1 = ans;
    }
}

// Function to find the longest
// concatenated string having
// every character of even frequency
void longestString(vector<string> arr, int index,
                   string str)
{

    // Checking the string
    if (index == arr.size()) {
        return;
    }

    // Dont Include the string
    longestString(arr, index + 1, str);

    // Include the string
    str += arr[index];

    calculate(str);
    longestString(arr, index + 1, str);
}

// Driver code
int main()
{
    vector<string> A
        = { "ABAB", "ABF", "CDA", "AD", "CCC" };

    // Call the function
    longestString(A, 0, "");

    // Print the answer
    cout << ans1 << " " << ans1.length();

    return 0;
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of the above approach

import java.io.*;
import java.util.*;

public class index {
    static int max = 0;
    static String ans1 = "";

    // Function to check the string
    static void calculate(String ans)
    {

        int dp[] = new int[26];
        for (int i = 0; i < ans.length(); ++i) {

            // Count the frequency
            // of the string
            dp[ans.charAt(i) - 'A']++;
        }

        // Check the frequency of the string
        for (int i = 0; i < dp.length; ++i) {
            if (dp[i] % 2 == 1) {
                return;
            }
        }
        if (max < ans.length()) {

            // Store the length
            // of the new String
            max = ans.length();
            ans1 = ans;
        }
    }

    // Function to find the longest
    // concatenated string having
    // every character of even frequency
    static void longestString(
        List<String> arr, int index, String str)
    {

        // Checking the string
        if (index == arr.size()) {
            return;
        }

        // Dont Include the string
        longestString(arr, index + 1, str);

        // Include the string
        str += arr.get(index);

        calculate(str);
        longestString(arr, index + 1, str);
    }

    // Driver code
    public static void main(String[] args)
    {
        ArrayList<String> A = new ArrayList<>();
        A.add("ABAB");
        A.add("ABF");
        A.add("CDA");
        A.add("AD");
        A.add("CCC");

        // Call the function
        longestString(A, 0, "");

        // Print the answer
        System.out.println(ans1 + " "
                           + ans1.length());
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach
maxi = 0;
ans1 = "";

# Function to check the string
def calculate(ans) :

    global maxi,ans1;

    dp = [ 0 ] * 26;
    for i in range(len(ans)) :

        # Count the frequency
        # of the string
        dp[ord(ans[i]) - ord('A')] += 1;

    # Check the frequency of the string
    for i in range(26) :
        if (dp[i] % 2 == 1) :
            return;

    if (maxi < len(ans)) :

        # Store the length
        # of the new String
        maxi = len(ans);
        ans1 = ans;

# Function to find the longest
# concatenated string having
# every character of even frequency
def longestString( arr,  index, string) :

    # Checking the string
    if (index == len(arr)) :
        return;

    # Dont Include the string
    longestString(arr, index + 1, string);

    # Include the string
    string += arr[index];

    calculate(string);
    longestString(arr, index + 1, string);

# Driver code
if __name__ == "__main__" :

    A = [ "ABAB", "ABF", "CDA", "AD", "CCC" ];

    # Call the function
    longestString(A, 0, "");

    # Print the answer
    print(ans1, len(ans1));

    # This code is contributed by AnkThon
```

## C#

```
// C# Implementation of the above approach
using System;

public class index {
    static int max = 0;
    static String ans1 = "";

    // Function to check the string
    static void calculate(String ans)
    {

        int[] dp = new int[26];
        for (int i = 0; i < ans.Length; ++i) {

            // Count the frequency
            // of the string
            dp[(int)ans[i] - (int)'A']++;
        }

        // Check the frequency of the string
        for (int i = 0; i < dp.Length; ++i) {
            if (dp[i] % 2 == 1) {
                return;
            }
        }
        if (max < ans.Length) {

            // Store the Length
            // of the new String
            max = ans.Length;
            ans1 = ans;
        }
    }

    // Function to find the longest
    // concatenated string having
    // every character of even frequency
    static void longestString(String[] arr, int index, String str)
    {

        // Checking the string
        if (index == arr.Length) {
            return;
        }

        // Dont Include the string
        longestString(arr, index + 1, str);

        // Include the string
        str += arr[index];

        calculate(str);
        longestString(arr, index + 1, str);
    }

    // Driver code
    public static void Main()
    {
        String[] A = {"ABAB", "ABF", "CDA", "AD", "CCC"};

        // Call the function
        longestString(A, 0, "");

        // Print the answer
        Console.WriteLine(ans1 + " " + ans1.Length);
    }
}

// This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

let maxi = 0;
let ans1 = "";

// Function to check the string
function calculate(ans) {
  let dp = new Array(26).fill(0);
  for (let i = 0; i < ans.length; ++i) {
    // Count the frequency
    // of the string
    dp[ans[i].charCodeAt(0) - "A".charCodeAt(0)]++;
  }

  // Check the frequency of the string
  for (let i = 0; i < 26; ++i) {
    if (dp[i] % 2 == 1) {
      return;
    }
  }
  if (maxi < ans.length) {
    // Store the length
    // of the new String
    maxi = ans.length;
    ans1 = ans;
  }
}

// Function to find the longest
// concatenated string having
// every character of even frequency
function longestString(arr, index, str) {
  // Checking the string
  if (index == arr.length) {
    return;
  }

  // Dont Include the string
  longestString(arr, index + 1, str);

  // Include the string
  str += arr[index];

  calculate(str);
  longestString(arr, index + 1, str);
}

// Driver code

let A = ["ABAB", "ABF", "CDA", "AD", "CCC"];

// Call the function
longestString(A, 0, "");

// Print the answer
document.write(ans1 + " " + ans1.length);

// This code is contributed by gfgking

</script>
```

**Output**

```
ABABCDAADCCC 12
```

**时间复杂度:** O(M*N* (2^N))，其中 n 为字符串数，m 为最长字符串的长度
T3】辅助空间: O(N)

**另一种方法:**通过预先计算每个字符串的字符频率，并在每个字符串串联后更新频率数组，可以进一步优化上述方法。