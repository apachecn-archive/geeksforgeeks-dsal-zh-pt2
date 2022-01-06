# 查找字符串中嵌套括号的最大深度

> 原文:[https://www . geesforgeks . org/find-最大深度-嵌套-括号-string/](https://www.geeksforgeeks.org/find-maximum-depth-nested-parenthesis-string/)

给我们一个字符串，其括号如下
”(((X))((Y))))“
我们需要找到平衡括号的最大深度，如上例中的 4。因为“Y”被 4 个平衡括号包围。
如果括号不平衡，则返回-1。

**示例:**

```
Input : S = "( a(b) (c) (d(e(f)g)h) I (j(k)l)m)";
Output : 4

Input : S = "( p((q)) ((s)t) )";
Output : 3

Input : S = "";
Output : 0

Input : S = "b) (c) ()";
Output : -1 

Input : S = "(b) ((c) ()"
Output : -1 
```

**方法 1(使用堆栈)**
一个简单的解决方案是使用堆栈来跟踪当前的开括号。

```
1) Create a stack. 
2) Traverse the string, do following for every character
     a) If current character is ‘(’ push it to the stack .
     b) If character is ‘)’, pop an element.
     c) Maintain maximum count during the traversal. 
```

时间复杂度:O(n)
辅助空间:O(n)

**方法 2 ( O(1)辅助空间)**
这个也可以不用叠加完成。

```
1) Take two variables max and current_max, initialize both of them as 0.
2) Traverse the string, do following for every character
    a) If current character is ‘(’, increment current_max and 
       update max value if required.
    b) If character is ‘)’. Check if current_max is positive or
       not (this condition ensure that parenthesis are balanced). 
       If positive that means we previously had a ‘(’ character 
       so decrement current_max without worry. 
       If not positive then the parenthesis are not balanced. 
       Thus return -1\. 
3) If current_max is not 0, then return -1 to ensure that the parenthesis
   are balanced. Else return max
```

下面是上述算法的实现。

## C++

```
// A C++ program to find the maximum depth of nested
// parenthesis in a given expression
#include <iostream>
using namespace std;

// function takes a string and returns the
// maximum depth nested parenthesis
int maxDepth(string S)
{
    int current_max = 0; // current count
    int max = 0; // overall maximum count
    int n = S.length();

    // Traverse the input string
    for (int i = 0; i < n; i++)
    {
        if (S[i] == '(')
        {
            current_max++;

            // update max if required
            if (current_max > max)
                max = current_max;
        }
        else if (S[i] == ')')
        {
            if (current_max > 0)
                current_max--;
            else
                return -1;
        }
    }

    // finally check for unbalanced string
    if (current_max != 0)
        return -1;

    return max;
}

// Driver program
int main()
{
    string s = "( ((X)) (((Y))) )";
    cout << maxDepth(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to find the maximum depth of nested
// parenthesis in a given expression

class GFG {
// function takes a string and returns the
// maximum depth nested parenthesis

    static int maxDepth(String S) {
        int current_max = 0; // current count
        int max = 0; // overall maximum count
        int n = S.length();

        // Traverse the input string
        for (int i = 0; i < n; i++) {
            if (S.charAt(i) == '(') {
                current_max++;

                // update max if required
                if (current_max > max) {
                    max = current_max;
                }
            } else if (S.charAt(i) == ')') {
                if (current_max > 0) {
                    current_max--;
                } else {
                    return -1;
                }
            }
        }

        // finally check for unbalanced string
        if (current_max != 0) {
            return -1;
        }

        return max;
    }

// Driver program
    public static void main(String[] args) {
        String s = "( ((X)) (((Y))) )";
        System.out.println(maxDepth(s));
    }
}
```

## 计算机编程语言

```
# A Python program to find the maximum depth of nested
# parenthesis in a given expression

# function takes a string and returns the
# maximum depth nested parenthesis
def maxDepth(S):
    current_max = 0
    max = 0
    n = len(S)

    # Traverse the input string
    for i in range(n):
        if S[i] == '(':
            current_max += 1

            if current_max > max:
                max = current_max
        elif S[i] == ')':
            if current_max > 0:
                current_max -= 1
            else:
                return -1

    # finally check for unbalanced string
    if current_max != 0:
        return -1

    return max

# Driver program
s = "( ((X)) (((Y))) )"
print (maxDepth(s))

# This code is contributed by BHAVYA JAIN
```

## C#

```
// C# program to find the
// maximum depth of nested
// parenthesis in a given expression
using System;
class GFG {

// function takes a string
// and returns the maximum
// depth nested parenthesis

static int maxDepth(string S)
{
  // current count
  int current_max = 0;

  // overall maximum count
  int max = 0;

  int n = S.Length;

  // Traverse the input string
  for (int i = 0; i < n; i++)
  {
    if (S[i] == '(')
    {
      current_max++;

      // update max if required
      if (current_max > max)
      {
        max = current_max;
      }
    }
    else if (S[i] == ')')
    {
      if (current_max > 0)
      {
        current_max--;
      }
      else
      {
        return -1;
      }
    }
  }

  // finally check for unbalanced string
  if (current_max != 0)
  {
    return -1;
  }

  return max;
}

// Driver program
public static void Main()
{
  string s = "(((X)) (((Y))))";
  Console.Write(maxDepth(s));
}
}

// This code is contributed by Chitranayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to find the
// maximum depth of nested
// parenthesis in a given
// expression

// function takes a string 
// and returns the maximum
// depth nested parenthesis
function maxDepth($S)
{
    // current count
    $current_max = 0;

    // overall maximum count
    $max = 0;
    $n = strlen($S);

    // Traverse the input string
    for ($i = 0; $i < $n; $i++)
    {
        if ($S[$i] == '(')
        {
            $current_max++;

            // update max if required
            if ($current_max> $max)
                $max = $current_max;
        }

        else if ($S[$i] == ')')
        {
            if ($current_max>0)
                $current_max--;
            else
                return -1;
        }
    }

    // finally check for
    // unbalanced string
    if ($current_max != 0)
        return -1;

    return $max;
}

// Driver Code
$s = "( ((X)) (((Y))) )";
echo maxDepth($s);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript program to find the
// maximum depth of nested parenthesis
// in a given expression

// Function takes a string and returns the
// maximum depth nested parenthesis
function maxDepth(S)
{

    // Current count
    let current_max = 0;

    // Overall maximum count
    let max = 0;
    let n = S.length;

    // Traverse the input string    
    for(let i = 0; i < n; i++)
    {
        if (S[i] == '(')
        {
            current_max++;

            // Update max if required
            if (current_max > max)
            {
                max = current_max;
            }
        }
        else if (S[i] == ')')
        {
             if (current_max > 0)
             {
                current_max--;
            } else
            {
                return -1;
            }
        }
    }

    // Finally check for unbalanced string
    if (current_max != 0)
    {
        return -1;
    }

    return max;
}

// Driver code
let s = "( ((X)) (((Y))) )";

document.write(maxDepth(s));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
 4 
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

？list = plqm 7 alhxfysf 7 lap-wi 5 qlad 8 oebx 9 rmv

本文由**高拉夫·夏尔马**供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。