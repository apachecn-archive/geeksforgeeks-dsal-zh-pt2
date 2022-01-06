# 尽量减少替换或交换相同的索引字符，以使两个给定的字符串回文

> 原文:[https://www . geeksforgeeks . org/最小化-替换-或-交换-相同的索引字符-需要生成两个给定的字符串-回文/](https://www.geeksforgeeks.org/minimize-replacements-or-swapping-of-same-indexed-characters-required-to-make-two-given-strings-palindromic/)

给定由 **N** 小写字母组成的两个[字符串](https://www.geeksforgeeks.org/string-data-structure/)、 **str1** 和 **str2** ，任务是找到以下两种类型的最小操作数，使两个字符串[回文字符串](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。

*   将字符串中的任何字符替换为任何其他字符(**[a–z]**)。
*   [交换两个字符串中同一索引处的任意两个字符。](https://www.geeksforgeeks.org/swap-in-cpp/)

**示例:**

> **输入:**str1 =“abbd”，str2 =“dbca”
> **输出:** 2
> **解释:**
> 交换(str1[0]，str2[0])将字符串 str 1 修改为“dbbd”，str2 修改为“abca”
> 将 str2[1]替换为“c”将字符串 str 2 修改为“acca”。
> 因此，经过上述 2 次操作后，字符串 str1 和 str2 成为回文。
> 
> **输入:**str 1 =“geeksforgeeks”，str 2 =“geeksforgeeks”
> T3】输出: 10

**方法:**按照以下步骤解决问题:

*   初始化两个变量，比如说 **i = 0** 和 **j = 0** 分别存储两个字符串的左指针和右指针的索引。
*   初始化一个变量，比如说 **cntOp** 来存储生成两个字符串[回文字符串](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)所需的最小操作数。
*   [遍历两个字符串](https://www.geeksforgeeks.org/strings-in-c-and-how-to-create-them/)并检查以下条件:
    *   如果 **str1[i] == str1[j]** 和 **str2[i]！= str2[j]** 然后将 **str2[i]** 的值替换为 **str2[j]** ，并将 **cntOp** 的值增加 **1** 。
    *   如果 **str1[i]！= str1[j]** 和 **str2[i] == str2[j]** 然后将 **str1[i]** 的值替换为 **str1[j]** ，并将 **cntOp** 的值增加 **1** 。
    *   如果 **str1[i]！= str1[j]** 和 **str2[i]！= str2[j]** 然后检查 **(str1[i] == str2[j]** 和 **str2[i] == str1[j])** 的值是否等于真。如果发现为真，则[交换(str1[i]，str2[j])](https://www.geeksforgeeks.org/swap-in-cpp/) ，并将 **cntOp** 的值增加 **1** 。
    *   否则，将 **str1[i]** 替换为 **str1[j]** 、 **str2[i]** 替换为 **str2[j]** ，并将 **cntOp** 的值增加 **2** 。
*   最后，打印 **cntOp** 的值。

**以下是上述方法的实现:**

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum operations
// to make both the strings palindromic
int MincntBothPalin(string str1,
                    string str2, int N)
{

    // Stores index of
    // the left pointer
    int i = 0;

    // Stores index of
    // the right pointer
    int j = N - 1;

    // Stores count of minimum operations to
    // make both the strings palindromic
    int cntOp = 0;

    while (i < j) {

        // if str1[i] equal to str1[j]
        // and str2[i] not equal to str2[j]
        if (str1[i] == str1[j]
            && str2[i] != str2[j]) {

            // Update cntOp
            cntOp += 1;
        }

        // If str1[i] not equal to str1[j]
        // and str2[i] equal to str2[j]
        else if (str1[i] != str1[j]
                 && str2[i] == str2[j]) {

            // Update cntOp
            cntOp += 1;
        }

        // If str1[i] is not equal to str1[j]
        // and str2[i] is not equal to str2[j]
        else if (str1[i] != str1[j]
                 && str2[i] != str2[j]) {

            // If str1[i] is equal to str2[j]
            // and str2[i] is equal to str1[j]
            if (str1[i] == str2[j]
                && str2[i] == str1[j]) {

                // Update cntOp
                cntOp += 1;
            }
            else {

                // Update cntOp
                cntOp += 2;
            }
        }

        // Update i and j
        i += 1;
        j -= 1;
    }

    return cntOp;
}

// Driver Code
int main()
{
    string str1 = "dbba";
    string str2 = "abcd";

    // Stores length of str1
    int N = str1.length();
    cout << MincntBothPalin(
        str1, str2, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find minimum operations
// to make both the Strings palindromic
static int MincntBothPalin(char[] str1,
                           char[] str2, int N)
{

    // Stores index of
    // the left pointer
    int i = 0;

    // Stores index of
    // the right pointer
    int j = N - 1;

    // Stores count of minimum operations to
    // make both the Strings palindromic
    int cntOp = 0;

    while (i < j)
    {

        // If str1[i] equal to str1[j]
        // and str2[i] not equal to str2[j]
        if (str1[i] == str1[j] &&
            str2[i] != str2[j])
        {

            // Update cntOp
            cntOp += 1;
        }

        // If str1[i] not equal to str1[j]
        // and str2[i] equal to str2[j]
        else if (str1[i] != str1[j] &&
                 str2[i] == str2[j])
        {

            // Update cntOp
            cntOp += 1;
        }

        // If str1[i] is not equal to str1[j]
        // and str2[i] is not equal to str2[j]
        else if (str1[i] != str1[j] &&
                 str2[i] != str2[j])
        {

            // If str1[i] is equal to str2[j]
            // and str2[i] is equal to str1[j]
            if (str1[i] == str2[j] &&
                str2[i] == str1[j])
            {

                // Update cntOp
                cntOp += 1;
            }
            else
            {

                // Update cntOp
                cntOp += 2;
            }
        }

        // Update i and j
        i += 1;
        j -= 1;
    }
    return cntOp;
}

// Driver Code
public static void main(String[] args)
{
    String str1 = "dbba";
    String str2 = "abcd";

    // Stores length of str1
    int N = str1.length();

    System.out.print(MincntBothPalin(
        str1.toCharArray(), str2.toCharArray(), N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find minimum
# operations to make both
# the strings palindromic
def MincntBothPalin(str1,
                    str2, N):

    # Stores index of
    # the left pointer
    i = 0

    # Stores index of
    # the right pointer
    j = N - 1

    # Stores count of minimum
    # operations to make both
    # the strings palindromic
    cntOp = 0

    while (i < j):

        # if str1[i] equal to
        # str1[j] and str2[i]
        # not equal to str2[j]
        if (str1[i] == str1[j] and
            str2[i] != str2[j]):

            # Update cntOp
            cntOp += 1

        # If str1[i] not equal
        # to str1[j] and str2[i]
        # equal to str2[j]
        elif (str1[i] != str1[j] and
              str2[i] == str2[j]):

            # Update cntOp
            cntOp += 1

        # If str1[i] is not equal
        # to str1[j] and str2[i]
        # is not equal to str2[j]
        elif (str1[i] != str1[j] and
              str2[i] != str2[j]):

            # If str1[i] is equal to
            # str2[j] and str2[i] is
            # equal to str1[j]
            if (str1[i] == str2[j] and
                str2[i] == str1[j]):

                # Update cntOp
                cntOp += 1

            else:

                # Update cntOp
                cntOp += 2

        # Update i and j
        i += 1
        j -= 1

    return cntOp

# Driver Code
if __name__ == "__main__":

    str1 = "dbba"
    str2 = "abcd"

    # Stores length of str1
    N = len(str1)
    print(MincntBothPalin(str1,
                          str2, N))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find minimum operations
// to make both the strings palindromic
static int MincntBothPalin(string str1,
                           string str2, int N)
{   
  // Stores index of
  // the left pointer
  int i = 0;

  // Stores index of
  // the right pointer
  int j = N - 1;

  // Stores count of minimum
  // operations to make both
  // the strings palindromic
  int cntOp = 0;

  while (i < j)
  {
    // If str1[i] equal to
    // str1[j] and str2[i]
    // not equal to str2[j]
    if (str1[i] == str1[j] &&
        str2[i] != str2[j])
    {
      // Update cntOp
      cntOp += 1;
    }

    // If str1[i] not equal
    // to str1[j] and str2[i]
    // equal to str2[j]
    else if (str1[i] != str1[j] &&
             str2[i] == str2[j])
    {
      // Update cntOp
      cntOp += 1;
    }

    // If str1[i] is not equal
    // to str1[j] and str2[i]
    // is not equal to str2[j]
    else if (str1[i] != str1[j] &&
             str2[i] != str2[j])
    {
      // If str1[i] is equal
      // to str2[j] and str2[i]
      // is equal to str1[j]
      if (str1[i] == str2[j] &&
          str2[i] == str1[j])
      {
        // Update cntOp
        cntOp += 1;
      }
      else
      {
        // Update cntOp
        cntOp += 2;
      }
    }

    // Update i and j
    i += 1;
    j -= 1;
  }
  return cntOp;
}

// Driver Code
public static void Main()
{
  string str1 = "dbba";
  string str2 = "abcd";

  // Stores length of str1
  int N = str1.Length;

  Console.WriteLine(
  MincntBothPalin(str1,
                  str2, N));
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

      // JavaScript program to implement
      // the above approach

      // Function to find minimum operations
      // to make both the strings palindromic
      function MincntBothPalin(str1, str2, N)
      {
        // Stores index of
        // the left pointer
        var i = 0;

        // Stores index of
        // the right pointer
        var j = N - 1;

        // Stores count of minimum operations to
        // make both the strings palindromic
        var cntOp = 0;

        while (i < j) {
          // if str1[i] equal to str1[j]
          // and str2[i] not equal to str2[j]
          if (str1[i] === str1[j] &&
          str2[i] !== str2[j]) {
            // Update cntOp
            cntOp += 1;
          }

          // If str1[i] not equal to str1[j]
          // and str2[i] equal to str2[j]
          else if (str1[i] !== str1[j] &&
          str2[i] === str2[j]) {
            // Update cntOp
            cntOp += 1;
          }

          // If str1[i] is not equal to str1[j]
          // and str2[i] is not equal to str2[j]
          else if (str1[i] !== str1[j] &&
          str2[i] !== str2[j])
          {
            // If str1[i] is equal to str2[j]
            // and str2[i] is equal to str1[j]
            if (str1[i] === str2[j] &&
            str2[i] === str1[j]) {
              // Update cntOp
              cntOp += 1;
            } else {
              // Update cntOp
              cntOp += 2;
            }
          }

          // Update i and j
          i += 1;
          j -= 1;
        }

        return cntOp;
      }

      // Driver Code
      var str1 = "dbba";
      var str2 = "abcd";

      // Stores length of str1
      var N = str1.length;
      document.write(MincntBothPalin(str1, str2, N));

    </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)