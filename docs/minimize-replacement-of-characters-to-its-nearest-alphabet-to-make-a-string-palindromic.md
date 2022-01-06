# 尽量减少将字符替换为最接近的字母，以形成字符串回文

> 原文:[https://www . geeksforgeeks . org/最小化字符替换到最接近字母的字符串回文/](https://www.geeksforgeeks.org/minimize-replacement-of-characters-to-its-nearest-alphabet-to-make-a-string-palindromic/)

给定一个由小写字母组成的长度为 **N** 的字符串 **S** ，任务是找到将给定字符串转换为[回文](https://www.geeksforgeeks.org/tag/palindrome/)的最小操作数。在一个操作中，选择任意字符并用它的下一个或上一个字母替换它。

> **注意:**字母是循环的，即如果 **z** 递增，则变成 **a** ，如果 **a** 递减，则变成 **z** 。

**示例:**

> **输入:** S = "arcehesmz"
> **输出:** 16
> **解释:**
> 给定最小运算次数的可能变换是:
> 
> *   将第一个字符**‘a’**减 1，得到**‘z’**。操作计数= 1
> *   将第三个字符**‘c’**减少 10，得到**‘T3’。操作计数= 1 + 10 = 11**
> *   将第 8 个字符**‘m’**增加 5，得到**‘r’**。操作计数= 11 + 5 = 16。
> 
> 因此，操作总数为 16。
> 
> **输入:**S = " abcdb "
> **输出:** 3
> **解释:**
> 给定最小运算次数的可能变换是:
> 
> *   将第一个字符**‘a’**增加 1，得到**‘b’**。操作计数= 1
> *   将第二个字符**【b】**增加 2，得到**【d】**。操作计数= 1 + 2 = 3。

**天真方法:**最简单的方法是[生成所有可能长度的字符串**N**T5。然后](https://www.geeksforgeeks.org/print-all-combinations-of-given-length/)[检查每个字符串，如果它是回文](https://www.geeksforgeeks.org/python-program-check-string-palindrome-not/)。如果发现任何字符串是回文，那么计算将给定字符串转换为该字符串所需的操作成本。对所有生成的字符串重复上述步骤，并打印所有成本中计算出的最小成本。

***时间复杂度:**O(26<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，其思想是遍历给定的字符串，并独立地找到每个位置的变化。按照以下步骤解决问题:

1.  [在范围**【0，(N/2)–1】**内遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)。
2.  对于索引 **i** 处的每个字符，找出索引 **i** 和**(N–I–1)**处的字符之间的绝对差异。
3.  可能存在两种可能的差异，即 **i** 处的字符在索引**(N–I–1)**处递增为字符时的差异，以及在该索引处递减时的差异。
4.  取两者中的最小值，并将其添加到结果中。
5.  完成上述步骤后，打印计算出的最小成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations required to convert
// th given string into palindrome
int minOperations(string s)
{
    int len = s.length();
    int result = 0;

    // Iterate till half of the string
    for (int i = 0; i < len / 2; i++) {

        // Find the absolute difference
        // between the characters
        int D1 = max(s[i], s[len - 1 - i])
                - min(s[i], s[len - 1 - i]);

        int D2 = 26 - D1;

        // Adding the minimum difference
        // of the two result
        result += min(D1, D2);
    }

    // Return the result
    return result;
}

// Driver Code
int main()
{
    // Given string
    string s = "abccdb";

    // Function Call
    cout << minOperations(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the minimum number
// of operations required to convert
// th given string into palindrome
public static int minOperations(String s)
{
    int len = s.length();
    int result = 0;

    // Iterate till half of the string
    for(int i = 0; i < len / 2; i++)
    {

        // Find the absolute difference
        // between the characters
        int D1 = Math.max(s.charAt(i),
                          s.charAt(len - 1 - i)) -
                 Math.min(s.charAt(i),
                          s.charAt(len - 1 - i));

        int D2 = 26 - D1;

        // Adding the minimum difference
        // of the two result
        result += Math.min(D1, D2);
    }

    // Return the result
    return result;
}

// Driver code
public static void main(String[] args)
{

    // Given string
    String s = "abccdb";

    // Function call
    System.out.println(minOperations(s));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of operations required to convert
# th given string into palindrome
def minOperations(s):

    length = len(s)
    result = 0

    # Iterate till half of the string
    for i in range(length // 2):

        # Find the absolute difference
        # between the characters
        D1 = (ord(max(s[i], s[length - 1 - i])) -
              ord(min(s[i], s[length - 1 - i])))

        D2 = 26 - D1

        # Adding the minimum difference
        # of the two result
        result += min(D1, D2)

    # Return the result
    return result

# Driver Code

# Given string
s = "abccdb"

# Function call
print(minOperations(s))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// of operations required to convert
// th given string into palindrome
public static int minOperations(String s)
{
    int len = s.Length;
    int result = 0;

    // Iterate till half of the string
    for(int i = 0; i < len / 2; i++)
    {

        // Find the absolute difference
        // between the characters
        int D1 = Math.Max(s[i],
                          s[len - 1 - i]) -
                 Math.Min(s[i],
                          s[len - 1 - i]);

        int D2 = 26 - D1;

        // Adding the minimum difference
        // of the two result
        result += Math.Min(D1, D2);
    }

    // Return the result
    return result;
}

// Driver code
public static void Main(String[] args)
{

    // Given string
    String s = "abccdb";

    // Function call
    Console.WriteLine(minOperations(s));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to find the minimum number
      // of operations required to convert
      // th given string into palindrome
      function minOperations(s)
      {
        var len = s.length;
        var result = 0;

        // Iterate till half of the string
        for (var i = 0; i < len / 2; i++)
        {

          // Find the absolute difference
          // between the characters
          var D1 =
            Math.max(s[i].charCodeAt(0), s[len - 1 - i].charCodeAt(0)) -
            Math.min(s[i].charCodeAt(0), s[len - 1 - i].charCodeAt(0));

          var D2 = 26 - D1;

          // Adding the minimum difference
          // of the two result
          result += Math.min(D1, D2);
        }

        // Return the result
        return result;
      }

      // Driver Code

      // Given string
      var s = "abccdb";

      // Function Call
      document.write(minOperations(s));

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)