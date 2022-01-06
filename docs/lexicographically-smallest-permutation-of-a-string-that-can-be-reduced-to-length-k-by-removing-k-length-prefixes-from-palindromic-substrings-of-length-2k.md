# 通过从长度为 2K 的回文子串中移除 K 长度前缀，可以将字符串的字典最小排列缩减为长度为 K 的排列

> 原文:[https://www . geeksforgeeks . org/词典学上最小的字符串排列可以通过从长度为 2k 的回文子字符串中移除长度为 k 的前缀来缩减为长度为 k 的字符串/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-a-string-that-can-be-reduced-to-length-k-by-removing-k-length-prefixes-from-palindromic-substrings-of-length-2k/)

给定一个长度为 **N** 的[二进制串](https://www.geeksforgeeks.org/tag/binary-string/) **串**和一个整数 **K** ，任务是通过从长度为 **2K** 的回文[子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)中移除每一个 **K** 长度的前缀，找到该串**串**的字典最小排列。如果不存在这样的排列，打印“**不可能**”。

**示例:**

> **输入:** str = "0000100001100001 "，K = 4
> **输出:** 0001100000011000
> **说明:**在字符串“00011000000011000”中，每当去掉一个 K 长度前缀，每 2K 长度的子串就变成一个回文，直到字符串长度减少到 K
> 
> **输入:** str = "100111 "，K = 2
> **输出:**“不可能”

**方法:**按照以下步骤解决问题:

*   [统计 **0** 和 **1** 出现在](https://www.geeksforgeeks.org/find-number-zeroes/)串中的次数。如果 **0** s 或 **1** s 的计数是 **N / K、**的倍数，则 **K** 可以减少弦长。否则，打印**“不可能**”。
*   初始化一个字符串 **tempStr** 来存储最初形成的字典最小的 **2K** 长度的字符串。
*   初始化一个字符串 **finalStr** 来存储满足给定条件的结果字符串。
*   根据以下公式将 **0** s 分配成一段长度 **2K** :
    *   2K 长度子字符串中的零个数，N0 =((N 长度字符串中的零个数)/(字符串的总长度))*(2K)
    *   2K 长度子串中的 1 个数，N1 =(2 * K–2K 长度子串中的 0 个数)
*   将 0**N0/2**次和 1**N1/2 次**次以及 0**N0/2**次追加到 **tempStr** 中。
*   将 **tempStr (N/2K)** 次追加到 **finalStr** 中，并将 **tempStr** 的 **(N%2K)** 字符插入到 **finalStr** 的末尾。
*   打印**最终字符串**作为结果字符串。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// zeroes present in the string
int count_zeroes(int n, string str)
{
    int cnt = 0;

    // Traverse the string
    for (int i = 0; i < str.size(); i++) {
        if (str[i] == '0')
            cnt++;
    }

    // Return the count
    return cnt;
}

// Function to rearrange the string s.t
// the string can be reduced to a length
// K as per the given rules
string kReducingStringUtil(
    int n, int k, string str,
    int no_of_zeroes)
{

    // Distribute the count of 0s and
    // 1s in segment of length 2k
    int zeroes_in_2k = ((no_of_zeroes)
                        * (2 * k))
                       / n;

    int ones_in_2k = 2 * k - zeroes_in_2k;

    // Store string that are initially
    // have formed lexicographically
    // smallest 2k length substring
    string temp_str = "";

    for (int i = 0;
         i < (zeroes_in_2k) / 2; i++) {
        temp_str.push_back('0');
    }
    for (int i = 0; i < ones_in_2k; i++) {
        temp_str.push_back('1');
    }
    for (int i = 0;
         i < (zeroes_in_2k) / 2; i++) {
        temp_str.push_back('0');
    }

    // Store the lexicographically
    // smallest string of length n
    // that satisfy the condition
    string final_str = "";

    // Insert temp_str into final_str
    // (n/2k) times and add (n%2k)
    // characters of temp_str at end
    for (int i = 0;
         i < n / (2 * k); i++) {
        final_str += (temp_str);
    }

    for (int i = 0;
         i < n % (2 * k); i++) {
        final_str.push_back(temp_str[i]);
    }

    // Return the final string
    return final_str;
}

// Function to reduce the string to
// length K that follows the given
// conditions
string kReducingString(int n, int k,
                       string str)
{
    // If the string contains either
    // 0s or 1s then it always be
    // reduced into a K length string
    int no_of_zeroes = count_zeroes(n, str);

    int no_of_ones = n - no_of_zeroes;

    // If the string contains only 0s
    // 1s then it always reduces to
    // a K length string
    if (no_of_zeroes == 0
        || no_of_zeroes == n) {
        return str;
    }

    // If K = 1
    if (k == 1) {
        if (no_of_zeroes == 0
            || no_of_zeroes == n) {
            return str;
        }
        else {
            return "Not Possible";
        }
    }

    // Check whether the given string
    // is K reducing string or not
    bool check = 0;

    for (int i = (n / k);
         i < n; i += (n / k)) {

        if (no_of_zeroes == i
            || no_of_ones == i) {
            check = 1;
            break;
        }
    }

    if (check == 0) {
        return "Not Possible";
    }

    // Otherwise recursively find
    // the string
    return kReducingStringUtil(n, k,
                               str,
                               no_of_zeroes);
}

// Driver Code
int main()
{
    string str = "0000100001100001";
    int K = 4;
    int N = str.length();

    // Function Call
    cout << kReducingString(N, K, str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count the number of
// zeroes present in the string
static int count_zeroes(int n, String str)
{
    int cnt = 0;

    // Traverse the string
    for(int i = 0; i < str.length(); i++)
    {
        if (str.charAt(i) == '0')
            cnt++;
    }

    // Return the count
    return cnt;
}

// Function to rearrange the string s.t
// the string can be reduced to a length
// K as per the given rules
static String kReducingStringUtil(int n, int k,
                                  String str,
                                  int no_of_zeroes)
{

    // Distribute the count of 0s and
    // 1s in segment of length 2k
    int zeroes_in_2k = ((no_of_zeroes) *
                        (2 * k)) / n;

    int ones_in_2k = 2 * k - zeroes_in_2k;

    // Store string that are initially
    // have formed lexicographically
    // smallest 2k length substring
    String temp_str = "";

    for(int i = 0; i < (zeroes_in_2k) / 2; i++)
    {
        temp_str += '0';
    }
    for(int i = 0; i < ones_in_2k; i++)
    {
        temp_str += '1';
    }
    for(int i = 0; i < (zeroes_in_2k) / 2; i++)
    {
        temp_str += '0';
    }

    // Store the lexicographically
    // smallest string of length n
    // that satisfy the condition
    String final_str = "";

    // Insert temp_str into final_str
    // (n/2k) times and add (n%2k)
    // characters of temp_str at end
    for(int i = 0; i < n / (2 * k); i++)
    {
        final_str += (temp_str);
    }

    for(int i = 0; i < n % (2 * k); i++)
    {
        final_str += temp_str.charAt(i);
    }

    // Return the final string
    return final_str;
}

// Function to reduce the string to
// length K that follows the given
// conditions
static String kReducingString(int n, int k,
                              String str)
{

    // If the string contains either
    // 0s or 1s then it always be
    // reduced into a K length string
    int no_of_zeroes = count_zeroes(n, str);

    int no_of_ones = n - no_of_zeroes;

    // If the string contains only 0s
    // 1s then it always reduces to
    // a K length string
    if (no_of_zeroes == 0 ||
        no_of_zeroes == n)
    {
        return str;
    }

    // If K = 1
    if (k == 1)
    {
        if (no_of_zeroes == 0 ||
            no_of_zeroes == n)
        {
            return str;
        }
        else
        {
            return "Not Possible";
        }
    }

    // Check whether the given string
    // is K reducing string or not
    boolean check = false;

    for(int i = (n / k); i < n; i += (n / k))
    {
        if (no_of_zeroes == i ||
            no_of_ones == i)
        {
            check = true;
            break;
        }
    }

    if (check == false)
    {
        return "Not Possible";
    }

    // Otherwise recursively find
    // the string
    return kReducingStringUtil(n, k, str,
                               no_of_zeroes);
}

// Driver Code
public static void main(String[] args)
{
    String str = "0000100001100001";
    int K = 4;
    int N = str.length();

    // Function Call
    System.out.println(kReducingString(N, K, str));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# zeroes present in the string
def count_zeroes(n, str):

  cnt = 0

  # Traverse the string
  for i in range(0, len(str)):
    if (str[i] == '0'):
      cnt += 1

  # Return the count
  return cnt

# Function to rearrange the string s.t
# the string can be reduced to a length
# K as per the given rules
def kReducingStringUtil(n, k, str,
                        no_of_zeroes):

  # Distribute the count of 0s and
  # 1s in segment of length 2k
  zeroes_in_2k = (((no_of_zeroes) *
                   (2 * k)) // n)

  ones_in_2k = 2 * k - zeroes_in_2k

  # Store string that are initially
  # have formed lexicographically
  # smallest 2k length substring
  temp_str = ""

  for i in range(0, (zeroes_in_2k) // 2):
    temp_str += '0'

  for i in range(0, (ones_in_2k)):
    temp_str += '1'

  for i in range(0, (zeroes_in_2k) // 2):
    temp_str += '0'

  # Store the lexicographically
  # smallest string of length n
  # that satisfy the condition
  final_str = ""

  # Insert temp_str into final_str
  # (n/2k) times and add (n%2k)
  # characters of temp_str at end
  for i in range(0, n // (2 * k)):
    final_str += (temp_str)

  for i in range(0, n % (2 * k)):
    final_str += (temp_str[i])

  # Return the final string
  return final_str

# Function to reduce the string to
# length K that follows the given
# conditions
def kReducingString(n, k, str):

  # If the string contains either
  # 0s or 1s then it always be
  # reduced into a K length string
  no_of_zeroes = count_zeroes(n, str)

  no_of_ones = n - no_of_zeroes

  # If the string contains only 0s
  # 1s then it always reduces to
  # a K length string
  if (no_of_zeroes == 0 or
      no_of_zeroes == n):
    return str

  # If K = 1
  if (k == 1):
    if (no_of_zeroes == 0 or
        no_of_zeroes == n):
      return str
    else:
      return "Not Possible"

  # Check whether the given string
  # is K reducing string or not
  check = 0

  for i in range((n // k), n, (n // k)):
    if (no_of_zeroes == i or no_of_ones == i):
      check = 1
      break

  if (check == 0):
    return "Not Possible"

  # Otherwise recursively find
  # the string
  return kReducingStringUtil(n, k, str,
                             no_of_zeroes)

# Driver Code
if __name__ == '__main__':

  str = "0000100001100001"
  K = 4;
  N = len(str)

  # Function Call
  print(kReducingString(N, K, str))

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of
// zeroes present in the string
static int count_zeroes(int n, string str)
{
    int cnt = 0;

    // Traverse the string
    for(int i = 0; i < str.Length; i++)
    {
        if (str[i] == '0')
            cnt++;
    }

    // Return the count
    return cnt;
}

// Function to rearrange the string s.t
// the string can be reduced to a length
// K as per the given rules
static string kReducingStringUtil(int n, int k,
                                  string str,
                                  int no_of_zeroes)
{

    // Distribute the count of 0s and
    // 1s in segment of length 2k
    int zeroes_in_2k = ((no_of_zeroes) *
                        (2 * k)) / n;

    int ones_in_2k = 2 * k - zeroes_in_2k;

    // Store string that are initially
    // have formed lexicographically
    // smallest 2k length substring
    string temp_str = "";

    for(int i = 0; i < (zeroes_in_2k) / 2; i++)
    {
        temp_str += '0';
    }
    for(int i = 0; i < ones_in_2k; i++)
    {
        temp_str += '1';
    }
    for(int i = 0; i < (zeroes_in_2k) / 2; i++)
    {
        temp_str += '0';
    }

    // Store the lexicographically
    // smallest string of length n
    // that satisfy the condition
    string final_str = "";

    // Insert temp_str into final_str
    // (n/2k) times and add (n%2k)
    // characters of temp_str at end
    for(int i = 0; i < n / (2 * k); i++)
    {
        final_str += (temp_str);
    }

    for(int i = 0; i < n % (2 * k); i++)
    {
        final_str += temp_str[i];
    }

    // Return the final string
    return final_str;
}

// Function to reduce the string to
// length K that follows the given
// conditions
static string kReducingString(int n, int k,
                              string str)
{

    // If the string contains either
    // 0s or 1s then it always be
    // reduced into a K length string
    int no_of_zeroes = count_zeroes(n, str);

    int no_of_ones = n - no_of_zeroes;

    // If the string contains only 0s
    // 1s then it always reduces to
    // a K length string
    if (no_of_zeroes == 0 ||
        no_of_zeroes == n)
    {
        return str;
    }

    // If K = 1
    if (k == 1)
    {
        if (no_of_zeroes == 0 ||
            no_of_zeroes == n)
        {
            return str;
        }
        else
        {
            return "Not Possible";
        }
    }

    // Check whether the given string
    // is K reducing string or not
    bool check = false;

    for(int i = (n / k); i < n; i += (n / k))
    {
        if (no_of_zeroes == i ||
            no_of_ones == i)
        {
            check = true;
            break;
        }
    }

    if (check == false)
    {
        return "Not Possible";
    }

    // Otherwise recursively find
    // the string
    return kReducingStringUtil(n, k, str,
                               no_of_zeroes);
}

// Driver Code
public static void Main()
{
    string str = "0000100001100001";
    int K = 4;
    int N = str.Length;

    // Function Call
    Console.WriteLine(kReducingString(N, K, str));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach
      // Function to count the number of
      // zeroes present in the string
      function count_zeroes(n, str) {
        var cnt = 0;

        // Traverse the string
        for (var i = 0; i < str.length; i++)
        {
          if (str[i] === "0") cnt++;
        }

        // Return the count
        return cnt;
      }

      // Function to rearrange the string s.t
      // the string can be reduced to a length
      // K as per the given rules
      function kReducingStringUtil(n, k, str, no_of_zeroes)
      {
        // Distribute the count of 0s and
        // 1s in segment of length 2k
        var zeroes_in_2k =
        parseInt((no_of_zeroes * (2 * k)) / n);

        var ones_in_2k = 2 * k - zeroes_in_2k;

        // Store string that are initially
        // have formed lexicographically
        // smallest 2k length substring
        var temp_str = "";

        for (var i = 0; i < zeroes_in_2k / 2; i++)
        {
          temp_str += "0";
        }
        for (var i = 0; i < ones_in_2k; i++)
        {
          temp_str += "1";
        }
        for (var i = 0; i < zeroes_in_2k / 2; i++)
        {
          temp_str += "0";
        }

        // Store the lexicographically
        // smallest string of length n
        // that satisfy the condition
        var final_str = "";

        // Insert temp_str into final_str
        // (n/2k) times and add (n%2k)
        // characters of temp_str at end
        for (var i = 0; i < n / (2 * k); i++)
        {
          final_str += temp_str;
        }

        for (var i = 0; i < n % (2 * k); i++)
        {
          final_str += temp_str[i];
        }

        // Return the final string
        return final_str;
      }

      // Function to reduce the string to
      // length K that follows the given
      // conditions
      function kReducingString(n, k, str)
      {
        // If the string contains either
        // 0s or 1s then it always be
        // reduced into a K length string
        var no_of_zeroes = count_zeroes(n, str);

        var no_of_ones = n - no_of_zeroes;

        // If the string contains only 0s
        // 1s then it always reduces to
        // a K length string
        if (no_of_zeroes === 0 || no_of_zeroes === n)
        {
          return str;
        }

        // If K = 1
        if (k === 1) {
          if (no_of_zeroes === 0 || no_of_zeroes === n)
          {
            return str;
          } else {
            return "Not Possible";
          }
        }

        // Check whether the given string
        // is K reducing string or not
        var check = false;

        for (var i = n / k; i < n; i += n / k) {
          if (no_of_zeroes === i || no_of_ones === i)
          {
            check = true;
            break;
          }
        }

        if (check === false) {
          return "Not Possible";
        }

        // Otherwise recursively find
        // the string
        return kReducingStringUtil(n, k, str, no_of_zeroes);
      }

      // Driver Code
      var str = "0000100001100001";
      var K = 4;
      var N = str.length;

      // Function Call
      document.write(kReducingString(N, K, str));

</script>
```

**Output:** 

```
0001100000011000
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)