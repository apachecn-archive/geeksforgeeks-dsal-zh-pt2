# 对需要清空所有平衡括号子序列的配对进行计数删除

> 原文:[https://www . geesforgeks . org/count-移除配对-要求为空-所有平衡-括号-子序列/](https://www.geeksforgeeks.org/count-removal-of-pairs-required-to-be-empty-all-balanced-parenthesis-subsequences/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是找到需要删除的平衡括号的最大对数**(字符串[i]，字符串[j])** ，使得该字符串不包含任何平衡括号的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/):

**示例:**

> **输入:**str = {(})”
> **输出:** 2
> **解释:**
> 移除一对有效括号 **(0，2)** 将 str 修改为“()”
> 移除一对有效括号 **(0，1)** 将 str 修改为“”。
> 现在，字符串不包含任何有效括号。所需输出为 2。
> 
> **输入:**str =)}(}”
> T3】输出: 0

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化三个变量，比如 **cntSqr** 、 **cntCurly** 和 **cntSml** ，分别存储“【有效括号】的个数、“{}”有效括号的个数和小有效括号的个数。
*   初始化一个变量，比如 **cntPairs** ，以存储需要删除的平衡括号对的计数，这样字符串就不包含任何平衡括号的子序列。
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符，检查以下条件:
    *   如果 **str[i] == '('** )，则将 **cntSml** 的值增加 **1** 。
    *   如果 **str[i] = '{'** ，那么将**的数值增加 **1** 。**
    *   如果 **str[i] = '['** ，则将 **cntSqr** 的值增加 **1** 。
    *   如果 **str[i] = ']'** ，则检查 **cntSqr** 是否大于 **0** 。如果发现为真，则将 **cntSqr** 的值递减 **1** ，将 **cntPairs** 的值递增 **1** 。
    *   如果 **str[i] = '}'** ，则检查**是否大于 **0** 。如果发现为真，则将**CNT curry**的值递减 **1** ，将 **cntPairs** 的值递增 **1** 。**
    *   如果 **str[i] = ')'** ，则检查 **cntSml** 是否大于 **0** 。如果发现为真，则将 **cntSml** 的值减少 **1** ，将**CNTs pairs**的值增加 **1** 。
*   最后，打印 **cntPairs** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to find the maximum count of pairs
// required to be removed such that subsequence
// of string does not contain any valid parenthesis
void cntBalancedParenthesis(string s, int N)
{

    // Stores count of pairs
    // of balanced parenthesis
    int cntPairs = 0;

    // Stores count of curly
    // balanced parenthesis
    int cntCurly = 0;

    // Stores count of small
    // balanced parenthesis
    int cntSml = 0;

    // Stores count of square
    // balanced parenthesis
    int cntSqr = 0;

    // Iterate over characters
    // of the string
    for (int i = 0; i < N; i++) {
        if (s[i] == '{') {

            // Update cntCurly
            cntCurly++;
        }

        else if (s[i] == '(') {

            // Update cntSml
            cntSml++;
        }

        else if (s[i] == '[') {

            // Update cntSqr
            cntSqr++;
        }

        else if (s[i] == '}' && cntCurly > 0) {

            // Update cntCurly
            cntCurly--;

            // Update cntPairs
            cntPairs++;
        }

        else if (s[i] == ')' && cntSml > 0) {

            // Update cntSml
            cntSml--;

            // Update cntPairs
            cntPairs++;
        }

        else if (s[i] == ']' && cntSqr > 0) {

            // Update cntSml
            cntSqr--;

            // Update cntPairs
            cntPairs++;
        }
    }

    cout << cntPairs;
}

// Driver Code
int main()
{
    // Given String
    string s = "{(})";
    int N = s.length();

    // Function call
    cntBalancedParenthesis(s, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
class GFG
{

  // Function to find the maximum count of pairs
  // required to be removed such that subsequence
  // of string does not contain any valid parenthesis
  static void cntBalancedParenthesis(String s, int N)
  {

    // Stores count of pairs
    // of balanced parenthesis
    int cntPairs = 0;

    // Stores count of curly
    // balanced parenthesis
    int cntCurly = 0;

    // Stores count of small
    // balanced parenthesis
    int cntSml = 0;

    // Stores count of square
    // balanced parenthesis
    int cntSqr = 0;

    // Iterate over characters
    // of the string
    for (int i = 0; i < N; i++) {
      if (s.charAt(i) == '{')
      {

        // Update cntCurly
        cntCurly++;
      }

      else if (s.charAt(i) == '(')
      {

        // Update cntSml
        cntSml++;
      }

      else if (s.charAt(i) == '[')
      {

        // Update cntSqr
        cntSqr++;
      }

      else if (s.charAt(i) == '}' && cntCurly > 0)
      {

        // Update cntCurly
        cntCurly--;

        // Update cntPairs
        cntPairs++;
      }

      else if (s.charAt(i) == ')' && cntSml > 0)
      {

        // Update cntSml
        cntSml--;

        // Update cntPairs
        cntPairs++;
      }

      else if (s.charAt(i) == ']' && cntSqr > 0)
      {

        // Update cntSml
        cntSqr--;

        // Update cntPairs
        cntPairs++;
      }
    }
    System.out.println(cntPairs);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given String
    String s = "{(})";
    int N = s.length();

    // Function call
    cntBalancedParenthesis(s, N);
  }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the maximum count of pairs
# required to be removed such that subsequence
# of string does not contain any valid parenthesis
def cntBalancedParenthesis(s, N):

    # Stores count of pairs
    # of balanced parenthesis
    cntPairs = 0;

    # Stores count of curly
    # balanced parenthesis
    cntCurly = 0;

    # Stores count of small
    # balanced parenthesis
    cntSml = 0;

    # Stores count of square
    # balanced parenthesis
    cntSqr = 0;

    # Iterate over characters
    # of the string
    for i in range(N):
        if (ord(s[i]) == ord('{')):

            # Update cntCurly
            cntCurly += 1;
        elif (ord(s[i]) == ord('(')):

            # Update cntSml
            cntSml += 1;
        elif (ord(s[i]) == ord('[')):

            # Update cntSqr
            cntSqr += 1;
        elif (ord(s[i]) == ord('}') and cntCurly > 0):

            # Update cntCurly
            cntCurly -=1;

            # Update cntPairs
            cntPairs += 1;
        elif (ord(s[i]) == ord(')') and cntSml > 0):

            # Update cntSml
            cntSml -=1;

            # Update cntPairs
            cntPairs += 1;
        elif (ord(s[i]) == ord(']') and cntSqr > 0):

            # Update cntSml
            cntSqr -=1;

            # Update cntPairs
            cntPairs += 1;
    print(cntPairs);

# Driver Code
if __name__ == '__main__':

    # Given String
    s = "{(})";
    N = len(s);

    # Function call
    cntBalancedParenthesis(s, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

  // Function to find the maximum count of pairs
  // required to be removed such that subsequence
  // of string does not contain any valid parenthesis
  static void cntBalancedParenthesis(String s, int N)
  {

    // Stores count of pairs
    // of balanced parenthesis
    int cntPairs = 0;

    // Stores count of curly
    // balanced parenthesis
    int cntCurly = 0;

    // Stores count of small
    // balanced parenthesis
    int cntSml = 0;

    // Stores count of square
    // balanced parenthesis
    int cntSqr = 0;

    // Iterate over characters
    // of the string
    for (int i = 0; i < N; i++) {
      if (s[i] == '{') {

        // Update cntCurly
        cntCurly++;
      }

      else if (s[i] == '(') {

        // Update cntSml
        cntSml++;
      }

      else if (s[i] == '[') {

        // Update cntSqr
        cntSqr++;
      }

      else if (s[i] == '}' && cntCurly > 0) {

        // Update cntCurly
        cntCurly--;

        // Update cntPairs
        cntPairs++;
      }

      else if (s[i] == ')' && cntSml > 0) {

        // Update cntSml
        cntSml--;

        // Update cntPairs
        cntPairs++;
      }

      else if (s[i] == ']' && cntSqr > 0) {

        // Update cntSml
        cntSqr--;

        // Update cntPairs
        cntPairs++;
      }
    }

    Console.WriteLine(cntPairs);
  }

  // Driver Code
  static public void Main()
  {

    // Given String
    String s = "{(})";
    int N = s.Length;

    // Function call
    cntBalancedParenthesis(s, N);
  }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to find the maximum count of pairs
    // required to be removed such that subsequence
    // of string does not contain any valid parenthesis

    function cntBalancedParenthesis( s , N)
    {

        // Stores count of pairs
        // of balanced parenthesis
        var cntPairs = 0;

        // Stores count of curly
        // balanced parenthesis
        var cntCurly = 0;

        // Stores count of small
        // balanced parenthesis
        var cntSml = 0;

        // Stores count of square
        // balanced parenthesis
        var cntSqr = 0;

        // Iterate over characters
        // of the string
        for (i = 0; i < N; i++) {
            if (s.charAt(i) == '{')
            {

                // Update cntCurly
                cntCurly++;
            }

            else if (s.charAt(i) == '(')
            {

                // Update cntSml
                cntSml++;
            }

            else if (s.charAt(i) == '[')
            {

                // Update cntSqr
                cntSqr++;
            }

            else if (s.charAt(i) == '}' && cntCurly > 0)
            {

                // Update cntCurly
                cntCurly--;

                // Update cntPairs
                cntPairs++;
            }

            else if (s.charAt(i) == ')' && cntSml > 0)
            {

                // Update cntSml
                cntSml--;

                // Update cntPairs
                cntPairs++;
            }

            else if (s.charAt(i) == ']' && cntSqr > 0)
            {

                // Update cntSml
                cntSqr--;

                // Update cntPairs
                cntPairs++;
            }
        }
        document.write(cntPairs);
    }

    // Driver Code

        // Given String
        var s = "{(})";
        var N = s.length;

        // Function call
        cntBalancedParenthesis(s, N);

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)