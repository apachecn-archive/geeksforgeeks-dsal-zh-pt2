# 尽量减少删除使给定字符串为空所需的不相等的相邻字符

> 原文:[https://www . geeksforgeeks . org/minimum-移除不相等的相邻字符-需要使给定字符串为空/](https://www.geeksforgeeks.org/minimize-removal-of-non-equal-adjacent-characters-required-to-make-a-given-string-empty/)

给定一个由**(“**”和**)“**组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过重复删除一对不相等的相邻字符来找到使该字符串成为空字符串所需的最小括号反转次数。如果无法清空字符串，则打印 **-1** 。

**示例:**

> **输入:**S =))(((
> **输出:** 0
> **解释:**
> 从 S 中移除(S[2]，S[3])将 S 修饰为)()()。
> 从 S 中移除(S[1]，S[2])会将 S 修改为“(”。
> 从 S 中移除(S[0]，S[1])会将 S 修改为“”。
> 因为不需要空翻就能让 S 变空。
> 因此，要求输出为 0。
> 
> **输入:**S =)(
> **输出:** -1

**方法:**按照以下步骤解决问题:

*   将两个整数变量 **cnt1** 和 **cnt2** 初始化为 **0** 。
*   如果字符串的[长度为奇数**或只有一种类型的字符，则打印**-1”**。**](https://www.geeksforgeeks.org/5-different-methods-find-length-string-c/)
*   否则，[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，如果当前字符是**(“**)，则将 **cnt1** 递增 1。否则，将 **cnt2** 增加 **1** 。
*   完成上述步骤后，打印**ABS(CNT 1–CNT 2)/2**的值作为所需的最小反转次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum count of steps
// required ot make string S an empty string
void canReduceString(string S, int N)
{

    // Stores count of occurences '('
    int count_1 = 0;

    // Stores count of occurences ')'
    int count_2 = 0;

    // Traverse the string, str
    for (int i = 0; i < N; i++) {

        // If current character is '('
        if (S[i] == '(') {

            // Update count_1
            count_1++;
        }
        else {

            // Update count_2
            count_2++;
        }
    }

    // If all the characters are
    // same, then print -1
    if (count_1 == 0 || count_2 == 0) {
        cout << "-1" << endl;
    }

    // If the count of occurence of ')'
    // and '(' are same then print 0
    else if (count_1 == count_2) {
        cout << "0" << endl;
    }

    // If length of string is Odd
    else if (N % 2 != 0) {
        cout << "-1";
    }

    else {
        cout << abs(count_1 - count_2) / 2;
    }
}

// Driver Code
int main()
{

    // Given string
    string S = ")))(((";

    // Size of the string
    int N = S.length();

    // Function Call
    canReduceString(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find minimum count of steps
// required ot make String S an empty String
static void canReduceString(String S, int N)
{

    // Stores count of occurences '('
    int count_1 = 0;

    // Stores count of occurences ')'
    int count_2 = 0;

    // Traverse the String, str
    for(int i = 0; i < N; i++)
    {

        // If current character is '('
        if (S.charAt(i) == '(')
        {

            // Update count_1
            count_1++;
        }
        else
        {

            // Update count_2
            count_2++;
        }
    }

    // If all the characters are
    // same, then print -1
    if (count_1 == 0 || count_2 == 0)
    {
        System.out.print("-1" + "\n");
    }

    // If the count of occurence of ')'
    // and '(' are same then print 0
    else if (count_1 == count_2)
    {
        System.out.print("0" + "\n");
    }

    // If length of String is Odd
    else if (N % 2 != 0)
    {
        System.out.print("-1");
    }

    else
    {
        System.out.print(Math.abs(
            count_1 - count_2) / 2);
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    String S = ")))(((";

    // Size of the String
    int N = S.length();

    // Function Call
    canReduceString(S, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
#Python3 program for the above approach

# Function to find minimum count of steps
# required ot make string S an empty string
def canReduceString(S, N):

    # Stores count of occurences '('
    count_1 = 0

    # Stores count of occurences ')'
    count_2 = 0

    # Traverse the string, str
    for i in range(N):

        # If current character is '('
        if (S[i] == '('):

            # Update count_1
            count_1 += 1
        else:

            #Update count_2
            count_2 += 1

    # If all the characters are
    # same, then pr-1
    if (count_1 == 0 or count_2 == 0):
        print("-1")

    # If the count of occurence of ')'
    # and '(' are same then pr0
    elif (count_1 == count_2):
        print("0")

    # If length of string is Odd
    elif (N % 2 != 0):
        print("-1")
    else:
        print (abs(count_1 - count_2) // 2)

# Driver Code
if __name__ == '__main__':

    # Given string
    S = ")))((("

    # Size of the string
    N = len(S)

    # Function Call
    canReduceString(S, N)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find minimum count of steps
// required ot make String S an empty String
static void canReduceString(String S, int N)
{

    // Stores count of occurences '('
    int count_1 = 0;

    // Stores count of occurences ')'
    int count_2 = 0;

    // Traverse the String, str
    for(int i = 0; i < N; i++)
    {

        // If current character is '('
        if (S[i] == '(')
        {

            // Update count_1
            count_1++;
        }
        else
        {

            // Update count_2
            count_2++;
        }
    }

    // If all the characters are
    // same, then print -1
    if (count_1 == 0 || count_2 == 0)
    {
        Console.Write("-1" + "\n");
    }

    // If the count of occurence of ')'
    // and '(' are same then print 0
    else if (count_1 == count_2)
    {
        Console.Write("0" + "\n");
    }

    // If length of String is Odd
    else if (N % 2 != 0)
    {
        Console.Write("-1");
    }

    else
    {
        Console.Write(Math.Abs(
            count_1 - count_2) / 2);
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    String S = ")))(((";

    // Size of the String
    int N = S.Length;

    // Function Call
    canReduceString(S, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach

      // Function to find minimum count of steps
      // required ot make string S an empty string
      function canReduceString(S, N) {
        // Stores count of occurences '('
        var count_1 = 0;

        // Stores count of occurences ')'
        var count_2 = 0;

        // Traverse the string, str
        for (var i = 0; i < N; i++) {
          // If current character is '('
          if (S[i] === "(") {
            // Update count_1
            count_1++;
          } else {
            // Update count_2
            count_2++;
          }
        }

        // If all the characters are
        // same, then print -1
        if (count_1 === 0 || count_2 === 0) {
          document.write("-1" + "<br>");
        }

        // If the count of occurence of ')'
        // and '(' are same then print 0
        else if (count_1 === count_2) {
          document.write("0" + "<br>");
        }

        // If length of string is Odd
        else if (N % 2 !== 0) {
          document.write("-1");
        } else {
          document.write(Math.abs(count_1 - count_2) / 2);
        }
      }

      // Driver Code
      // Given string
      var S = ")))(((";

      // Size of the string
      var N = S.length;

      // Function Call
      canReduceString(S, N);
    </script>
```

**Output:** 

```
0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)