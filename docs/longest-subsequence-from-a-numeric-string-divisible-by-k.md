# 可被 K 整除的数字串中最长的子序列

> 原文:[https://www . geeksforgeeks . org/最长子序列-从-数字-字符串-可被-k 整除/](https://www.geeksforgeeks.org/longest-subsequence-from-a-numeric-string-divisible-by-k/)

给定一个整数 **K** 和一个数字字符串 **str** ，任务是从给定的字符串中找到最长的[子序列](https://www.geeksforgeeks.org/tag/subsequence/)，该序列可以被 **K** 整除。

**示例:**

> **输入:** str = "121400 "，K = 8
> **输出:** 121400
> **解释:**
> 由于整串可以被 8 整除，所以整串就是答案。
> 
> **输入:**字符串:“7675437”，K = 64
> **输出:** 64
> **解释:**
> 可被 64 整除的字符串中最长的子序列是“64”本身。

**方法:**思路是[找到给定字符串](https://www.geeksforgeeks.org/print-subsequences-string/)的所有子序列，对于每个子序列，检查其整数表示是否能被 **K** 整除。按照以下步骤解决问题:

*   [穿越弦](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)。每遇到一个角色，都有两种可能。
*   要么考虑子序列中的当前字符，要么不考虑。对于这两种情况，继续到字符串的下一个字符，并找到可被 **K** 整除的最长子序列。
*   将上面获得的最长子序列与最长子序列的当前最大长度进行比较，并进行相应的更新。
*   对字符串的每个字符重复上述步骤，最后，打印获得的最大长度。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to if the integer representation
// of the current string is divisible by K
bool isdivisible(string& newstr, long long K)
{
    // Stores the integer
    // representation of the string
    long long num = 0;

    for (int i = 0; i < newstr.size(); i++) {
        num = num * 10 + newstr[i] - '0';
    }

    // Check if the num is
    // divisible by K
    if (num % K == 0)
        return true;

    else
        return false;
}

// Function to find the longest subsequence
// which is divisible by K
void findLargestNo(string& str, string& newstr,
                string& ans, int index,
                long long K)
{

    if (index == (int)str.length()) {

        // If the number is divisible by K
        if (isdivisible(newstr, K)) {

            // If current number is the
            // maximum obtained so far
            if ((ans < newstr
                && ans.length() == newstr.length())
                || newstr.length() > ans.length()) {
                ans = newstr;
            }
        }

        return;
    }

    string x = newstr + str[index];

    // Include the digit at current index
    findLargestNo(str, x, ans, index + 1, K);

    // Exclude the digit at current index
    findLargestNo(str, newstr, ans, index + 1, K);
}

// Driver Code
int main()
{

    string str = "121400";

    string ans = "", newstr = "";

    long long K = 8;

    findLargestNo(str, newstr, ans, 0, K);

    // Printing the largest number
    // which is divisible by K
    if (ans != "")
        cout << ans << endl;

    // If no number is found
    // to be divisible by K
    else
        cout << -1 << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to if the integer representation
// of the current string is divisible by K
static boolean isdivisible(StringBuilder newstr,
                           long K)
{

    // Stores the integer
    // representation of the string
    long num = 0;

    for(int i = 0; i < newstr.length(); i++)
    {
        num = num * 10 + newstr.charAt(i) - '0';
    }

    // Check if the num is
    // divisible by K
    if (num % K == 0)
        return true;
    else
        return false;
}

// Function to find the longest
// subsequence which is divisible
// by K
static void findLargestNo(String str, StringBuilder newstr,
                          StringBuilder ans, int index,
                          long K)
{
    if (index == str.length())
    {

        // If the number is divisible by K
        if (isdivisible(newstr, K))
        {

            // If current number is the
            // maximum obtained so far
            if ((newstr.toString().compareTo(ans.toString()) > 0 &&
                ans.length() == newstr.length()) ||
                newstr.length() > ans.length())
            {
                ans.setLength(0);
                ans.append(newstr);
            }
        }
        return;
    }

    StringBuilder x = new StringBuilder(
        newstr.toString() + str.charAt(index));

    // Include the digit at current index
    findLargestNo(str, x, ans, index + 1, K);

    // Exclude the digit at current index
    findLargestNo(str, newstr, ans, index + 1, K);
} 

// Driver code
public static void main (String[] args)
{
    String str = "121400";

    StringBuilder ans = new StringBuilder(),
               newstr = new StringBuilder();

     long K = 8;

    findLargestNo(str, newstr, ans, 0, K);

    // Printing the largest number
    // which is divisible by K
    if (ans.toString() != "")
        System.out.println(ans);

    // If no number is found
    // to be divisible by K
    else
        System.out.println(-1);
}
}

// This code is contributed by offbeat
```

## C#

```
// C# program for the above approach
using System;
using System.Text;

class GFG{

// Function to if the integer representation
// of the current string is divisible by K
static bool isdivisible(StringBuilder newstr,
                        long K)
{

    // Stores the integer representation
    // of the string
    long num = 0;

    for(int i = 0; i < newstr.Length; i++)
    {
        num = num * 10 + newstr[i] - '0';
    }

    // Check if the num is
    // divisible by K
    if (num % K == 0)
        return true;
    else
        return false;
}

// Function to find the longest
// subsequence which is divisible
// by K
static void findLargestNo(String str, StringBuilder newstr,
                          StringBuilder ans, int index,
                          long K)
{
    if (index == str.Length)
    {

        // If the number is divisible by K
        if (isdivisible(newstr, K))
        {

            // If current number is the
            // maximum obtained so far
            if ((newstr.ToString().CompareTo(ans.ToString()) > 0 &&
                ans.Length == newstr.Length) ||
                newstr.Length > ans.Length)
            {
                ans.EnsureCapacity(0);//.SetLength(0);
                ans.Append(newstr);
            }
        }
        return;
    }

    StringBuilder x = new StringBuilder(
        newstr.ToString() + str[index]);

    // Include the digit at current index
    findLargestNo(str, x, ans, index + 1, K);

    // Exclude the digit at current index
    findLargestNo(str, newstr, ans, index + 1, K);
} 

// Driver code
public static void Main(String[] args)
{
    String str = "121400";

    StringBuilder ans = new StringBuilder(),
               newstr = new StringBuilder();

     long K = 8;

    findLargestNo(str, newstr, ans, 0, K);

    // Printing the largest number
    // which is divisible by K
    if (ans.ToString() != "")
        Console.WriteLine(ans);

    // If no number is found
    // to be divisible by K
    else
        Console.WriteLine(-1);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to if the integer representation
// of the current string is divisible by K
function isdivisible(newstr, K)
{

    // Stores the integer
    // representation of the string
    var num = 0;

    for(var i = 0; i < newstr.length; i++)
    {
        num = num * 10 + newstr[i].charCodeAt(0) -
                               '0'.charCodeAt(0);
    }

    // Check if the num is
    // divisible by K
    if (num % K == 0)
        return true;
    else
        return false;
}

// Function to find the longest subsequence
// which is divisible by K
function findLargestNo(str, newstr, ans, index, K)
{
    if (index == str.length)
    {

        // If the number is divisible by K
        if (isdivisible(newstr, K))
        {

            // If current number is the
            // maximum obtained so far
            if ((ans < newstr &&
                 ans.length == newstr.length) ||
                 newstr.length > ans.length)
            {
                ans = newstr;
            }
        }
        return ans;
    }

    var x = newstr + str[index];

    // Include the digit at current index
    ans = findLargestNo(str, x, ans,
                        index + 1, K);

    // Exclude the digit at current index
    ans = findLargestNo(str, newstr, ans,
                        index + 1, K);

    return ans;
}

// Driver Code
var str = "121400";
var ans = "", newstr = "";
var K = 8;
ans = findLargestNo(str, newstr, ans, 0, K);

// Printing the largest number
// which is divisible by K
if (ans != "")
    document.write(ans)

// If no number is found
// to be divisible by K
else
    document.write( -1)

// This code is contributed by itsok

</script>
```

**Output:** 

```
121400
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(1)*