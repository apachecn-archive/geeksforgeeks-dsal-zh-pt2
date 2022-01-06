# 尽量减少为使一个字符串的所有字符相同所需的上一个或下一个字母的替换

> 原文:[https://www . geeksforgeeks . org/最小化-按上一个或下一个字母替换-要求字符串中的所有字符相同/](https://www.geeksforgeeks.org/minimize-replacements-by-previous-or-next-alphabet-required-to-make-all-characters-of-a-string-the-same/)

给定一个由小写字母组成的长度为 **N** 的字符串 **S** ，任务是找到使字符串 **S** 的所有字符相同所需的最小操作数。在每个操作中，选择任意字符并用它的下一个或上一个字母替换它。

> **注意:**字母被认为是循环的，即 **z** 的下一个字符被认为是 **a** ，而 **a** 的前一个字符被认为是 **z** 。

**示例:**

> **输入:** S = "abc"
> **输出:** 2
> **解释:**
> 为尽量减少操作次数，将字符串的所有字符改为‘b’。
> 操作 1:变 a 为 b。
> 操作 2:变 c 为 b。
> 
> **输入:** S = "zzza"
> **输出:** 1
> **解释:**
> 为尽量减少操作次数，将字符串的所有字符改为‘z’。
> 操作 1:将 a 改为 z。

**方法:**解决问题的思路是计算使所有字符等于每个字母的成本，**‘a’**到**‘z’**，逐一计算，并打印任何转换所需的最小成本。按照以下步骤解决问题:

*   用存储最小答案的大值初始化变量 **min** 。
*   遍历范围**【0，25】**，其中 **i** 代表 **(i + 1) <sup>第</sup>个字母**从 **'a'** 到 **'z'** 并执行以下步骤:
    *   初始化变量 **cnt** 初始化为 **0** ，它将存储将字符串的所有字符转换为相同的答案。
    *   从 **j = 0** 到**(N–1)**遍历给定的字符串，并将**min(ABS(I+' a '–S[j])、26–ABS(I+' a '–S[j])**添加到 **cnt** 中。
    *   完成上述步骤后，将**分钟**更新为最小**分钟**和**分钟**。
*   遍历每个字符的字符串后，打印 **min** 的值作为最小操作数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum count
// of operations to make all characters
// of the string same
int minCost(string s, int n)
{

    // Set min to some large value
    int minValue = 100000000;

    // Find minimum operations for
    // each character
    for (int i = 0; i <= 25; i++) {

        // Initialize cnt
        int cnt = 0;

        for (int j = 0; j < n; j++) {

            // Add the value to cnt
            cnt += min(abs(i - (s[j] - 'a')),
                       26 - abs(i - (s[j] - 'a')));
        }

        // Update minValue
        minValue = min(minValue, cnt);
    }

    // Return minValue
    return minValue;
}

// Driver Code
int main()
{
    // Given string str
    string str = "geeksforgeeks";

    int N = str.length();

    // Function Call
    cout << minCost(str, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the minimum count
// of operations to make all characters
// of the String same
static int minCost(String s, int n)
{

    // Set min to some large value
    int minValue = 100000000;

    // Find minimum operations for
    // each character
    for(int i = 0; i <= 25; i++)
    {

        // Initialize cnt
        int cnt = 0;

        for(int j = 0; j < n; j++)
        {

            // Add the value to cnt
            cnt += Math.min(Math.abs(i - (s.charAt(j) - 'a')),
                       26 - Math.abs(i - (s.charAt(j) - 'a')));
        }

        // Update minValue
        minValue = Math.min(minValue, cnt);
    }

    // Return minValue
    return minValue;
}

// Driver Code
public static void main (String[] args)
{

    // Given String str
    String str = "geeksforgeeks";

    int N = str.length();

    // Function call
    System.out.println(minCost(str, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to find the minimum
# count of operations to make
# all characters of the string same
def minCost(s, n):

    # Set min to some
    # large value
    minValue = 100000000

    # Find minimum operations
    # for each character
    for i in range(26):

        # Initialize cnt
        cnt = 0

        for j in range(n):

            # Add the value to cnt
            cnt += min(abs(i - (ord(s[j]) -
                                ord('a'))),
                       26 - abs(i - (ord(s[j]) -
                                     ord('a'))))

        # Update minValue
        minValue = min(minValue, cnt)

    # Return minValue
    return minValue

# Driver Code
if __name__ == "__main__":

    # Given string str
    st = "geeksforgeeks"

    N = len(st)

    # Function Call
    print(minCost(st, N))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum count
// of operations to make all characters
// of the String same
static int minCost(string s, int n)
{

    // Set min to some large value
    int minValue = 100000000;

    // Find minimum operations for
    // each character
    for(int i = 0; i <= 25; i++)
    {

        // Initialize cnt
        int cnt = 0;

        for(int j = 0; j < n; j++)
        {

            // Add the value to cnt
            cnt += Math.Min(Math.Abs(i - (s[j] - 'a')),
                       26 - Math.Abs(i - (s[j] - 'a')));
        }

        // Update minValue
        minValue = Math.Min(minValue, cnt);
    }

    // Return minValue
    return minValue;
}

// Driver code
public static void Main()
{

    // Given String str
    string str = "geeksforgeeks";

    int N = str.Length;

    // Function call
    Console.WriteLine(minCost(str, N));
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to find the minimum count
      // of operations to make all characters
      // of the string same
      function minCost(s, n) {
        // Set min to some large value
        var minValue = 100000000;

        // Find minimum operations for
        // each character
        for (var i = 0; i <= 25; i++) {
          // Initialize cnt
          var cnt = 0;
          for (var j = 0; j < n; j++) {
            // Add the value to cnt
            cnt += Math.min(
              Math.abs(i - (s[j].charCodeAt(0) -
              "a".charCodeAt(0))),
              26 - Math.abs(i - (s[j].charCodeAt(0) -
              "a".charCodeAt(0)))
            );
          }

          // Update minValue
          minValue = Math.min(minValue, cnt);
        }

        // Return minValue
        return minValue;
      }

      // Driver Code

      // Given string str
      var str = "geeksforgeeks";
      var N = str.length;

      // Function Call
      document.write(minCost(str, N));

</script>
```

**Output**

```
60
```

***时间复杂度:** O(N * 26)*
***辅助空间:** O(N)*