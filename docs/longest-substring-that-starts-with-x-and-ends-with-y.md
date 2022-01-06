# 以 X 开头、以 Y 结尾的最长子串

> 原文:[https://www . geeksforgeeks . org/以-x 开头、以-y 结尾的最长子串/](https://www.geeksforgeeks.org/longest-substring-that-starts-with-x-and-ends-with-y/)

给定一个字符串**字符串**，两个字符 **X** 和 **Y** 。任务是找出以 **X** 开始，以 **Y** 结束的最长子串的长度。给定始终存在一个以 **X** 开头，以 **Y** 结尾的子串。
**举例:**

> **输入:** str = "QWERTYASDFZXCV "，X = 'A '，Y = 'Z'
> **输出:** 5
> **解释:**
> 以 **'A'** 开头，以 **'Z'** 结尾的最大子串= "ASDFZ "。
> 子串的大小= 5。
> **输入:** str = "ZABCZ "，X = 'Z '，Y = 'Z'
> **输出:** 3
> **解释:**
> 以 **'Z'** 开头，以 **'Z'** = "ZABCZ "结尾的最大子串。
> 子串的大小= 5。

**朴素方法:**朴素方法是从给定字符串中找出所有子字符串，找出最大的子字符串，以 **X** 开始，以 **Y** 结束。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效途径:**要优化上述途径， **X** 和 **Y** 之间的字符数应该最大。因此，使用指针**开始**和**结束**遍历字符串，从起始索引中找到第一个出现的 **X** ，从结束索引中找到最后一个出现的 **Y** 。以下是步骤:

1.  初始化**开始= 0** 和**结束=字符串长度–1**。
2.  从头开始遍历字符串，找到第一个出现的字符 **X** 。让它在索引 **xPos** 处。
3.  从头开始遍历字符串，找到最后出现的字符 **Y** 。让它在索引 **yPos** 处。
4.  最长子串的长度由**(yPos–xPos+1)**给出。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function returns length of longest
// substring starting with X and
// ending with Y
int longestSubstring(string str,
                    char X, char Y)
{
    // Length of string
    int N = str.length();
    int start = 0;
    int end = N - 1;
    int xPos = 0;
    int yPos = 0;

    // Find the length of the string
    // starting with X from the beginning
    while (true) {

        if (str[start] == X) {
            xPos = start;
            break;
        }
        start++;
    }

    // Find the length of the string
    // ending with Y from the end
    while (true) {

        if (str[end] == Y) {
            yPos = end;
            break;
        }
        end--;
    }

    // Longest substring
    int length = (yPos - xPos) + 1;

    // Print the length
    cout << length;
}

// Driver Code
int main()
{
    // Given string str
    string str = "HASFJGHOGAKZZFEGA";

    // Starting and Ending characters
    char X = 'A', Y = 'Z';

    // Function Call
    longestSubstring(str, X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function returns length of longest
// substring starting with X and
// ending with Y
public static void longestSubstring(String str,
                                    char X, char Y)
{

    // Length of string
    int N = str.length();
    int start = 0;
    int end = N - 1;
    int xPos = 0;
    int yPos = 0;

    // Find the length of the string
    // starting with X from the beginning
    while (true)
    {
        if (str.charAt(start) == X)
        {
            xPos = start;
            break;
        }
        start++;
    }

    // Find the length of the string
    // ending with Y from the end
    while (true)
    {
        if (str.charAt(end) == Y)
        {
            yPos = end;
            break;
        }
        end--;
    }

    // Longest substring
    int length = (yPos - xPos) + 1;

    // Print the length
    System.out.print(length);
}

// Driver code
public static void main(String[] args)
{

    // Given string str
    String str = "HASFJGHOGAKZZFEGA";

    // Starting and Ending characters
    char X = 'A', Y = 'Z';

    // Function Call
    longestSubstring(str, X, Y);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function returns length of longest
# substring starting with X and
# ending with Y
def longestSubstring(str, X, Y):

    # Length of string
    N = len(str)

    start = 0
    end = N - 1
    xPos = 0
    yPos = 0

    # Find the length of the string
    # starting with X from the beginning
    while (True):
        if (str[start] == X):
            xPos = start
            break

        start += 1

    # Find the length of the string
    # ending with Y from the end
    while (True):
        if (str[end] == Y):
            yPos = end
            break

        end -= 1

    # Longest substring
    length = (yPos - xPos) + 1

    # Print the length
    print(length)

# Driver Code
if __name__ == "__main__":

    # Given string str
    str = "HASFJGHOGAKZZFEGA"

    # Starting and Ending characters
    X = 'A'
    Y = 'Z'

    # Function Call
    longestSubstring(str, X, Y)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Function returns length of longest
// substring starting with X and
// ending with Y
static void longestSubstring(string str,
                             char X, char Y)
{

    // Length of string
    int N = str.Length;
    int start = 0;
    int end = N - 1;
    int xPos = 0;
    int yPos = 0;

    // Find the length of the string
    // starting with X from the beginning
    while (true)
    {
        if (str[start] == X)
        {
            xPos = start;
            break;
        }
        start++;
    }

    // Find the length of the string
    // ending with Y from the end
    while (true)
    {
        if (str[end] == Y)
        {
            yPos = end;
            break;
        }
        end--;
    }

    // Longest substring
    int length = (yPos - xPos) + 1;

    // Print the length
    Console.Write(length);
}

// Driver code
public static void Main()
{

    // Given string str
    string str = "HASFJGHOGAKZZFEGA";

    // Starting and Ending characters
    char X = 'A', Y = 'Z';

    // Function call
    longestSubstring(str, X, Y);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function returns length of longest
      // substring starting with X and
      // ending with Y
      function longestSubstring(str, X, Y) {
        // Length of string
        var N = str.length;
        var start = 0;
        var end = N - 1;
        var xPos = 0;
        var yPos = 0;

        // Find the length of the string
        // starting with X from the beginning
        while (true) {
          if (str[start] === X) {
            xPos = start;
            break;
          }
          start++;
        }

        // Find the length of the string
        // ending with Y from the end
        while (true) {
          if (str[end] === Y) {
            yPos = end;
            break;
          }
          end--;
        }

        // Longest substring
        var length = yPos - xPos + 1;

        // Print the length
        document.write(length);
      }

      // Driver code
      // Given string str
      var str = "HASFJGHOGAKZZFEGA";

      // Starting and Ending characters
      var X = "A",
        Y = "Z";
      // Function call
      longestSubstring(str, X, Y);
    </script>
```

**Output:** 

```
12
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*