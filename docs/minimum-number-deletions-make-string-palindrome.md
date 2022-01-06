# 组成字符串回文的最小删除次数

> 原文:[https://www . geesforgeks . org/最小数量-删除-制作-字符串-回文/](https://www.geeksforgeeks.org/minimum-number-deletions-make-string-palindrome/)

给定大小为“n”的字符串。任务是从字符串中移除或删除最少数量的字符，以使结果字符串成为回文。

注意:应该保持字符的顺序。

**示例:**

```
Input : aebcbda
Output : 2
Remove characters 'e' and 'd'
Resultant string will be 'abcba'
which is a palindromic string

Input : geeksforgeeks
Output : 8
```

一个**简单的解决方法**就是把所有的子序列一个个去掉，检查剩下的字符串是不是回文。这个解的时间复杂度是指数级的。

一种**有效的方法**使用[的概念来寻找给定序列的最长回文子序列](https://www.geeksforgeeks.org/dynamic-programming-set-12-longest-palindromic-subsequence/)的长度。

**算法:**

1.**字符串**是给定的字符串。

2. **n** 长度**弦**

3. **len** 是**串**的最长
回文子序列的长度

4.最小删除次数
**分钟**= n–len

下面是上述方法的实现:

## C++

```
// C++ implementation to find
// minimum number of deletions
// to make a string palindromic
#include <bits/stdc++.h>
using namespace std;

// Returns the length of
// the longest palindromic
// subsequence in 'str'
int lps(string str)
{
    int n = str.size();

    // Create a table to store
    // results of subproblems
    int L[n][n];

    // Strings of length 1
    // are palindrome of length 1
    for (int i = 0; i < n; i++)
        L[i][i] = 1;

    // Build the table. Note that
    // the lower diagonal values
    // of table are useless and
    // not filled in the process.
    // c1 is length of substring
    for (int cl = 2; cl <= n; cl++)
    {
        for (int i = 0;
                 i < n - cl + 1; i++)
        {
            int j = i + cl - 1;
            if (str[i] == str[j] &&
                        cl == 2)
                L[i][j] = 2;
            else if (str[i] == str[j])
                L[i][j] = L[i + 1][j - 1] + 2;
            else
                L[i][j] = max(L[i][j - 1],
                            L[i + 1][j]);
        }
    }

    // length of longest
    // palindromic subseq
    return L[0][n - 1];
}

// function to calculate
// minimum number of deletions
int minimumNumberOfDeletions(string str)
{
    int n = str.size();

    // Find longest palindromic
    // subsequence
    int len = lps(str);

    // After removing characters
    // other than the lps, we
    // get palindrome.
    return (n - len);
}

// Driver Code
int main()
{
    string str = "geeksforgeeks";
    cout << "Minimum number of deletions = "
         << minimumNumberOfDeletions(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// find minimum number of
// deletions to make a
// string palindromic
class GFG
{
    // Returns the length of
    // the longest palindromic
    // subsequence in 'str'
    static int lps(String str)
    {
        int n = str.length();

        // Create a table to store
        // results of subproblems
        int L[][] = new int[n][n];

        // Strings of length 1
        // are palindrome of length 1
        for (int i = 0; i < n; i++)
            L[i][i] = 1;

        // Build the table. Note
        // that the lower diagonal
        // values of table are useless
        // and not filled in the process.
        // c1 is length of substring
        for (int cl = 2; cl <= n; cl++)
        {
            for (int i = 0; i < n - cl + 1; i++)
            {
                int j = i + cl - 1;
                if (str.charAt(i) ==
                        str.charAt(j) && cl == 2)
                    L[i][j] = 2;
                else if (str.charAt(i) ==
                              str.charAt(j))
                    L[i][j] = L[i + 1][j - 1] + 2;
                else
                    L[i][j] = Integer.max(L[i][j - 1],
                                         L[i + 1][j]);
            }
        }

        // length of longest
        // palindromic subsequence
        return L[0][n - 1];
    }

    // function to calculate minimum
    // number of deletions
    static int minimumNumberOfDeletions(String str)
    {
        int n = str.length();

        // Find longest palindromic
        // subsequence
        int len = lps(str);

        // After removing characters
        // other than the lps, we get
        // palindrome.
        return (n - len);
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "geeksforgeeks";
        System.out.println("Minimum number " +
                            "of deletions = "+
               minimumNumberOfDeletions(str));
    }
}

// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 implementation to find
# minimum number of deletions
# to make a string palindromic

# Returns the length of
# the longest palindromic
# subsequence in 'str'
def lps(str):
    n = len(str)

    # Create a table to store
    # results of subproblems
    L = [[0 for x in range(n)]for y in range(n)]

    # Strings of length 1
    # are palindrome of length 1
    for i in range(n):
        L[i][i] = 1

    # Build the table. Note that
    # the lower diagonal values
    # of table are useless and
    # not filled in the process.
    # c1 is length of substring
    for cl in range( 2, n+1):
        for i in range(n - cl + 1):
            j = i + cl - 1
            if (str[i] == str[j] and cl == 2):
                L[i][j] = 2
            elif (str[i] == str[j]):
                L[i][j] = L[i + 1][j - 1] + 2
            else:
                L[i][j] = max(L[i][j - 1],L[i + 1][j])

    # length of longest
    # palindromic subseq
    return L[0][n - 1]

# function to calculate
# minimum number of deletions
def minimumNumberOfDeletions( str):

    n = len(str)

    # Find longest palindromic
    # subsequence
    l = lps(str)

    # After removing characters
    # other than the lps, we
    # get palindrome.
    return (n - l)

# Driver Code
if __name__ == "__main__":

    str = "geeksforgeeks"
    print( "Minimum number of deletions = "
         , minimumNumberOfDeletions(str))
```

## C#

```
// C# implementation to find
// minimum number of deletions
// to make a string palindromic
using System;

class GFG
{
    // Returns the length of
    // the longest palindromic
    // subsequence in 'str'
    static int lps(String str)
    {
        int n = str.Length;

        // Create a table to store
        // results of subproblems
        int [,]L = new int[n, n];

        // Strings of length 1
        // are palindrome of length 1
        for (int i = 0; i < n; i++)
            L[i, i] = 1;

        // Build the table. Note
        // that the lower diagonal
        // values of table are useless
        // and not filled in the process.
        // c1 is length of substring
        for (int cl = 2; cl <= n; cl++)
        {
            for (int i = 0; i < n - cl + 1; i++)
            {
                int j = i + cl - 1;
                if (str[i] == str[j] && cl == 2)
                    L[i, j] = 2;
                else if (str[i] == str[j])
                    L[i, j] = L[i + 1, j - 1] + 2;
                else
                    L[i, j] = Math.Max(L[i, j - 1],
                                      L[i + 1, j]);
            }
        }

        // length of longest
        // palindromic subsequence
        return L[0, n - 1];
    }

    // function to calculate minimum
    // number of deletions
    static int minimumNumberOfDeletions(string str)
    {
        int n = str.Length;

        // Find longest palindromic
        // subsequence
        int len = lps(str);

        // After removing characters
        // other than the lps, we get
        // palindrome.
        return (n - len);
    }

    // Driver Code
    public static void Main()
    {
        string str = "geeksforgeeks";
        Console.Write("Minimum number of" +
                          " deletions = " +
            minimumNumberOfDeletions(str));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// minimum number of deletions
// to make a string palindromic

// Returns the length of
// the longest palindromic
// subsequence in 'str'
function lps($str)
{
    $n = strlen($str);

    // Create a table to store
    // results of subproblems
    $L;

    // Strings of length 1
    // are palindrome of length 1
    for ($i = 0; $i < $n; $i++)
        $L[$i][$i] = 1;

    // Build the table. Note that
    // the lower diagonal values
    // of table are useless and
    // not filled in the process.
    // c1 is length of substring
    for ($cl = 2; $cl <= $n; $cl++)
    {
        for ( $i = 0;
              $i < $n -$cl + 1;
              $i++)
        {
            $j = $i + $cl - 1;
            if ($str[$i] == $str[$j] &&
                            $cl == 2)
                $L[$i][$j] = 2;
            else if ($str[$i] == $str[$j])
                $L[$i][$j] =
                        $L[$i + 1][$j - 1] + 2;

            else
                $L[$i][$j] = max($L[$i][$j - 1],
                                $L[$i + 1][$j]);
        }
    }

    // length of longest
    // palindromic subseq
    return $L[0][$n - 1];
}

// function to calculate minimum
// number of deletions
function minimumNumberOfDeletions($str)
{
    $n = strlen($str);

    // Find longest
    // palindromic subsequence
    $len = lps($str);

    // After removing characters
    // other than the lps, we get
    // palindrome.
    return ($n - $len);
}

// Driver Code
{
    $str = "geeksforgeeks";
    echo "Minimum number of deletions = ",
           minimumNumberOfDeletions($str);
    return 0;
}

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

  // JavaScript implementation to
  // find minimum number of
  // deletions to make a
  // string palindromic

  // Returns the length of
  // the longest palindromic
  // subsequence in 'str'
  function lps(str)
  {
      let n = str.length;

      // Create a table to store
      // results of subproblems
      let L = new Array(n);
      for (let i = 0; i < n; i++)
      {
        L[i] = new Array(n);
        for (let j = 0; j < n; j++)
        {
          L[i][j] = 0;
        }
      }

      // Strings of length 1
      // are palindrome of length 1
      for (let i = 0; i < n; i++)
          L[i][i] = 1;

      // Build the table. Note
      // that the lower diagonal
      // values of table are useless
      // and not filled in the process.
      // c1 is length of substring
      for (let cl = 2; cl <= n; cl++)
      {
          for (let i = 0; i < n - cl + 1; i++)
          {
              let j = i + cl - 1;
              if (str[i] == str[j] && cl == 2)
                  L[i][j] = 2;
              else if (str[i] == str[j])
                  L[i][j] = L[i + 1][j - 1] + 2;
              else
                  L[i][j] = Math.max(L[i][j - 1], L[i + 1][j]);
          }
      }

      // length of longest
      // palindromic subsequence
      return L[0][n - 1];
  }

  // function to calculate minimum
  // number of deletions
  function minimumNumberOfDeletions(str)
  {
      let n = str.length;

      // Find longest palindromic
      // subsequence
      let len = lps(str);

      // After removing characters
      // other than the lps, we get
      // palindrome.
      return (n - len);
  }

  let str = "geeksforgeeks";
  document.write("Minimum number " + "of deletions = "+
  minimumNumberOfDeletions(str));

</script>
```

**Output**

```
Minimum number of deletions = 8
```