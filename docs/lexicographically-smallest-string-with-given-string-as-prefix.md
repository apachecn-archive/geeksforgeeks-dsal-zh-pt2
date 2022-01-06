# 以给定字符串为前缀的字典最小字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序以给定字符串作为前缀的最小字符串/](https://www.geeksforgeeks.org/lexicographically-smallest-string-with-given-string-as-prefix/)

给定一个由 **N** [字符串](https://www.geeksforgeeks.org/string-data-structure/)和一个字符串 **S** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，如果大小为 **M** ，那么任务是找到由字符串 **S** 作为前缀组成的字典上最小的字符串。如果不存在任何以前缀 **S** 开头的字符串，则打印 **"-1"** 。

**示例:**

> **输入:**arr[]= {“apple”、“appe”、“apl”、“aapl”、“appax”}，S =“app”
> **输出:** appax
> **解释:**
> 以“app”为子串的字符串的字典顺序为{“Aapl”、“APL”、“appax”、“appe”、“apple”}。包含的最小词典字符串是“appax”。
> 
> **输入:**arr[]= {“can”、“man”、“va”}，S = " van "
> T3】输出: -1

**方法:**给定的问题可以通过[排序给定的字符串数组](https://www.geeksforgeeks.org/sort-the-array-of-strings-according-to-alphabetical-order-defined-by-another-string/) **arr[]** 来解决，这样所有以前缀 **S** 开始的字符串都连续出现。现在遍历给定的字符串数组 **arr[]** ，当第一个字符串的前缀与 **S** 匹配时，打印该字符串，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the whether the
// string temp starts with str or not
bool is_prefix(string temp, string str)
{
    // Base Case
    if (temp.length() < str.length())
        return 0;
    else {

        // Check for the corresponding
        // characters in temp & str
        for (int i = 0;
             i < str.length(); i++) {

            if (str[i] != temp[i])
                return 0;
        }
        return 1;
    }
}

// Function to find lexicographic smallest
// string consisting of the string str
// as prefix
string lexicographicallyString(
    string input[], int n, string str)
{
    // Sort the given array string arr[]
    sort(input, input + n);

    for (int i = 0; i < n; i++) {
        string temp = input[i];

        // If the i-th string contains
        // given string as a prefix,
        // then print the result
        if (is_prefix(temp, str)) {
            return temp;
        }
    }

    // If no string exists then
    // return "-1"
    return "-1";
}

// Driver Code
int main()
{
    string arr[] = { "apple", "appe", "apl",
                     "aapl", "appax" };
    string S = "app";
    int N = 5;

    cout << lexicographicallyString(
        arr, N, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.Arrays;  

class GFG {

    // Function to find the whether the
    // string temp starts with str or not
    static boolean is_prefix(String temp, String str)
    {
        // Base Case
        if (temp.length() < str.length())
            return false;
        else {

            // Check for the corresponding
            // characters in temp & str
            for (int i = 0; i < str.length(); i++) {

                if (str.charAt(i) != temp.charAt(i))
                    return false;
            }
            return true;
        }
    }

    // Function to find lexicographic smallest
    // string consisting of the string str
    // as prefix
    static String lexicographicallyString(String[] input,
                                          int n, String str)
    {
        // Sort the given array string arr[]
        Arrays.sort(input);

        for (int i = 0; i < n; i++) {
            String temp = input[i];

            // If the i-th string contains
            // given string as a prefix,
            // then print the result
            if (is_prefix(temp, str)) {
                return temp;
            }
        }

        // If no string exists then
        // return "-1"
        return "-1";
    }

    // Driver Code
    public static void main(String args[])
    {
        String[] arr = { "apple", "appe", "apl", "aapl", "appax" };
        String S = "app";
        int N = 5;

        System.out.println(
            lexicographicallyString(arr, N, S));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the whether the
# string temp starts with str or not
def is_prefix(temp, str):

    # Base Case
    if (len(temp) < len(str)):
        return 0
    else:

        # Check for the corresponding
        # characters in temp & str
        for i in range(len(str)):
            if (str[i] != temp[i]):
                return 0
        return 1

# Function to find lexicographic smallest
# string consisting of the string str
# as prefix
def lexicographicallyString(input, n, str):

    # Sort the given array string arr[]
    input.sort()

    for i in range(n):
        temp = input[i]

        # If the i-th string contains
        # given string as a prefix,
        # then print the result
        if (is_prefix(temp, str)):
            return temp

    # If no string exists then
    # return "-1"
    return "-1"

# Driver Code
if __name__ == '__main__':
    arr = ["apple", "appe", "apl", "aapl", "appax"]
    S = "app"
    N = 5

    print(lexicographicallyString(arr, N, S))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the whether the
    // string temp starts with str or not
    static bool is_prefix(string temp, string str)
    {
        // Base Case
        if (temp.Length < str.Length)
            return false;
        else {

            // Check for the corresponding
            // characters in temp & str
            for (int i = 0; i < str.Length; i++) {

                if (str[i] != temp[i])
                    return false;
            }
            return true;
        }
    }

    // Function to find lexicographic smallest
    // string consisting of the string str
    // as prefix
    static string lexicographicallyString(string[] input,
                                          int n, string str)
    {
        // Sort the given array string arr[]
        Array.Sort(input);

        for (int i = 0; i < n; i++) {
            string temp = input[i];

            // If the i-th string contains
            // given string as a prefix,
            // then print the result
            if (is_prefix(temp, str)) {
                return temp;
            }
        }

        // If no string exists then
        // return "-1"
        return "-1";
    }

    // Driver Code
    public static void Main()
    {
        string[] arr
            = { "apple", "appe", "apl", "aapl", "appax" };
        string S = "app";
        int N = 5;

        Console.WriteLine(
            lexicographicallyString(arr, N, S));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the whether the
        // string temp starts with str or not
        function is_prefix(temp, str)
        {

            // Base Case
            if (temp.length < str.length)
                return 0;
            else {

                // Check for the corresponding
                // characters in temp & str
                for (let i = 0;
                    i < str.length; i++) {

                    if (str[i] != temp[i])
                        return 0;
                }
                return 1;
            }
        }

        // Function to find lexicographic smallest
        // string consisting of the string str
        // as prefix
        function lexicographicallyString(
            input, n, str)
       {

            // Sort the given array string arr[]
            input = Array.from(input).sort();
            for (let i = 0; i < n; i++) {
                let temp = input[i];

                // If the i-th string contains
                // given string as a prefix,
                // then print the result
                if (is_prefix(temp, str)) {
                    return temp;
                }
            }

            // If no string exists then
            // return "-1"
            return "-1";
        }

        // Driver Code
        let arr = ["apple", "appe", "apl",
            "aapl", "appax"];
        let S = "app";
        let N = 5;

        document.write(lexicographicallyString(
            arr, N, S));

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
appax
```

***时间复杂度:** O(M*K*N*log N)，其中 K 是数组**arr【】**中字符串* *的最大* [*长度。*
***辅助空间:** O(N)*](https://www.geeksforgeeks.org/program-for-length-of-a-string-using-recursion/)

**另一种方法:**上述方法也可以通过使用 [Trie 数据结构](https://www.geeksforgeeks.org/trie-insert-and-search/)进行优化，方法是[在 Trie 中插入所有给定的字符串](https://www.geeksforgeeks.org/insertion-in-a-trie-recursively/)，然后检查前缀为 **S** 的 Trie 中是否存在第一个字符串。

***时间复杂度:** O(M*N)*
***辅助空间:** O(N)*