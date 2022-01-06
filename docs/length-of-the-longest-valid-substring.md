# 最长有效子串的长度

> 原文:[https://www . geesforgeks . org/最长有效子字符串长度/](https://www.geeksforgeeks.org/length-of-the-longest-valid-substring/)

给定由左括号和右括号组成的字符串，找到最长的有效括号子字符串的长度。

**示例:**

```
Input : ((()
Output : 2
Explanation : ()

Input: )()())
Output : 4
Explanation: ()() 

Input:  ()(()))))
Output: 6
Explanation:  ()(())
```

一种简单的方法是找到给定字符串的所有子串。对于每个字符串，检查它是否是有效的字符串。如果有效且长度超过最大长度，则更新最大长度。我们可以使用堆栈在线性时间内检查子串是否有效(详见[本](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-an-expression/))。该解决方案的时间复杂度为 0(n)<sup>2</sup>。

一个**高效解**可以在 O(n)时间内解决这个问题。其思想是将先前起始括号的索引存储在堆栈中。堆栈的第一个元素是一个特殊的元素，它在有效子字符串(下一个有效字符串的基)开始之前提供索引。

```
1) Create an empty stack and push -1 to it. 
   The first element of the stack is used 
   to provide a base for the next valid string. 

2) Initialize result as 0.

3) If the character is '(' i.e. str[i] == '('), 
   push index'i' to the stack. 

2) Else (if the character is ')')
   a) Pop an item from the stack (Most of the 
      time an opening bracket)
   b) If the stack is not empty, then find the
      length of current valid substring by taking 
      the difference between the current index and
      top of the stack. If current length is more 
      than the result, then update the result.
   c) If the stack is empty, push the current index
      as a base for the next valid substring.

3) Return result.
```

下面是上述算法的实现。

## C++

```
// C++ program to find length of the
// longest valid substring
#include <bits/stdc++.h>
using namespace std;

int findMaxLen(string str)
{
    int n = str.length();

    // Create a stack and push -1 as
    // initial index to it.
    stack<int> stk;
    stk.push(-1);

    // Initialize result
    int result = 0;

    // Traverse all characters of given string
    for (int i = 0; i < n; i++)
    {
        // If opening bracket, push index of it
        if (str[i] == '(')
            stk.push(i);

        // If closing bracket, i.e.,str[i] = ')'
        else
        {
            // Pop the previous opening
            // bracket's index
            if (!stk.empty())
            {
                stk.pop();
            }

            // Check if this length formed with base of
            // current valid substring is more than max
            // so far
            if (!stk.empty())
                result = max(result, i - stk.top());

            // If stack is empty. push current index as
            // base for next valid substring (if any)
            else
                stk.push(i);
        }
    }

    return result;
}

// Driver code
int main()
{
    string str = "((()()";

    // Function call
    cout << findMaxLen(str) << endl;

    str = "()(()))))";

    // Function call
    cout << findMaxLen(str) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of the longest valid
// substring

import java.util.Stack;

class Test
{
    // method to get length of the longest valid
    static int findMaxLen(String str)
    {
        int n = str.length();

        // Create a stack and push -1
        // as initial index to it.
        Stack<Integer> stk = new Stack<>();
        stk.push(-1);

        // Initialize result
        int result = 0;

        // Traverse all characters of given string
        for (int i = 0; i < n; i++)
        {
            // If opening bracket, push index of it
            if (str.charAt(i) == '(')
                stk.push(i);

            // // If closing bracket, i.e.,str[i] = ')'
            else
            {
                // Pop the previous
                // opening bracket's index
                if(!stk.empty())
                    stk.pop();

                // Check if this length
                // formed with base of
                // current valid substring
                // is more than max
                // so far
                if (!stk.empty())
                    result
                        = Math.max(result,
                                   i - stk.peek());

                // If stack is empty. push
                // current index as base
                // for next valid substring (if any)
                else
                    stk.push(i);
            }
        }

        return result;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "((()()";

        // Function call
        System.out.println(findMaxLen(str));

        str = "()(()))))";

        // Function call
        System.out.println(findMaxLen(str));
    }
}
```

## 计算机编程语言

```
# Python program to find length of the longest valid
# substring

def findMaxLen(string):
    n = len(string)

    # Create a stack and push -1
    # as initial index to it.
    stk = []
    stk.append(-1)

    # Initialize result
    result = 0

    # Traverse all characters of given string
    for i in xrange(n):

        # If opening bracket, push index of it
        if string[i] == '(':
            stk.append(i)

        # If closing bracket, i.e., str[i] = ')'
        else:  

            # Pop the previous opening bracket's index
            if len(stk) != 0:
               stk.pop()

            # Check if this length formed with base of
            # current valid substring is more than max
            # so far
            if len(stk) != 0:
                result = max(result,
                             i - stk[len(stk)-1])

            # If stack is empty. push current index as
            # base for next valid substring (if any)
            else:
                stk.append(i)

    return result

# Driver code
string = "((()()"

# Function call
print findMaxLen(string)

string = "()(()))))"

# Function call
print findMaxLen(string)

# This code is contributed by Bhavya Jain
```

## C#

```
// C# program to find length of
// the longest valid substring
using System;
using System.Collections.Generic;

class GFG {
    // method to get length of
    // the longest valid
    public static int findMaxLen(string str)
    {
        int n = str.Length;

        // Create a stack and push -1 as
        // initial index to it.
        Stack<int> stk = new Stack<int>();
        stk.Push(-1);

        // Initialize result
        int result = 0;

        // Traverse all characters of
        // given string
        for (int i = 0; i < n; i++)
        {
            // If opening bracket, push
            // index of it
            if (str[i] == '(') {
                stk.Push(i);
            }

            else // If closing bracket,
                 // i.e.,str[i] = ')'
            {
                // Pop the previous opening
                // bracket's index
                if (stk.Count > 0)
                    stk.Pop();

                // Check if this length formed
                // with base of current valid
                // substring is more than max
                // so far
                if (stk.Count > 0)
                {
                    result
                        = Math.Max(result,
                                   i - stk.Peek());
                }

                // If stack is empty. push current
                // index as base for next valid
                // substring (if any)
                else {
                    stk.Push(i);
                }
            }
        }

        return result;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string str = "((()()";

        // Function call
        Console.WriteLine(findMaxLen(str));

        str = "()(()))))";

        // Function call
        Console.WriteLine(findMaxLen(str));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>
       // JavaScript Program for the above approach
       function findMaxLen(str)
       {
           let n = str.length;

           // Create a stack and push -1 as
           // initial index to it.
           let stk = [];
           stk.push(-1);

           // Initialize result
           let result = 0;

           // Traverse all characters of given string
           for (let i = 0; i < n; i++)
           {
               // If opening bracket, push index of it
               if (str.charAt(i) == '(')
               {
                   stk.push(i);
               }

               // If closing bracket, i.e.,str[i] = ')'
               else
               {
                   // Pop the previous opening
                   // bracket's index
                   if (stk.length != 0) {
                       stk.pop();
                   }

                   // Check if this length formed with base of
                   // current valid substring is more than max
                   // so far
                   if (stk.length != 0) {
                       result = Math.max(result, i - stk[stk.length - 1]);
                   }

                   // If stack is empty. push current index as
                   // base for next valid substring (if any)
                   else {
                       stk.push(i);
                   }
               }
           }

           return result;
       }

       // Driver code
       let str = "((()()";

       // Function call
       document.write(findMaxLen(str) + "<br>");

       str = "()(()))))";

       // Function call
       document.write(findMaxLen(str) + "<br>");

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
4
6
```

**举例说明:**

```
Input: str = "(()()"

Initialize result as 0 and stack with one item -1.

For i = 0, str[0] = '(', we push 0 in stack

For i = 1, str[1] = '(', we push 1 in stack

For i = 2, str[2] = ')', currently stack has 
[-1, 0, 1], we pop from the stack and the stack
now is [-1, 0] and length of current valid substring 
becomes 2 (we get this 2 by subtracting stack top from 
current index).

Since the current length is more than the current result, 
we update the result.

For i = 3, str[3] = '(', we push again, stack is [-1, 0, 3].
For i = 4, str[4] = ')', we pop from the stack, stack 
becomes [-1, 0] and length of current valid substring 
becomes 4 (we get this 4 by subtracting stack top from 
current index). 
Since current length is more than current result,
we update result. 
```

另一种**高效方法**可以在 O(n)时间内解决问题。其思想是维护一个数组，该数组存储在该索引处结束的最长有效子字符串的长度。我们迭代数组并返回最大值。

```
1) Create an array longest of length n (size of the input
   string) initialized to zero.
   The array will store the length of the longest valid 
   substring ending at that index.

2) Initialize result as 0.

3) Iterate through the string from second character
   a) If the character is '(' set longest[i]=0 as no 
      valid sub-string will end with '('.
   b) Else
      i) if s[i-1] = '('
            set longest[i] = longest[i-2] + 2
      ii) else
            set longest[i] = longest[i-1] + 2 + 
            longest[i-longest[i-1]-2]

4) In each iteration update result as the maximum of 
   result and longest[i]

5) Return result.
```

下面是上述算法的实现。

## C++

```
// C++ program to find length of the longest valid
// substring
#include <bits/stdc++.h>
using namespace std;

int findMaxLen(string s)
{
    if (s.length() <= 1)
        return 0;

    // Initialize curMax to zero
    int curMax = 0;

    vector<int> longest(s.size(), 0);

    // Iterate over the string starting from second index
    for (int i = 1; i < s.length(); i++)
    {
        if (s[i] == ')' && i - longest[i - 1] - 1 >= 0
            && s[i - longest[i - 1] - 1] == '(')
        {
            longest[i]
                = longest[i - 1] + 2
                  + ((i - longest[i - 1] - 2 >= 0)
                  ? longest[i - longest[i - 1] - 2]
                  : 0);
            curMax = max(longest[i], curMax);
        }
    }
    return curMax;
}

// Driver code
int main()
{
    string str = "((()()";

    // Function call
    cout << findMaxLen(str) << endl;

    str = "()(()))))";

    // Function call
    cout << findMaxLen(str) << endl;

    return 0;
}
// This code is contributed by Vipul Lohani
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of the longest valid
// subString
import java.util.*;
class GFG
{

  static int findMaxLen(String s)
  {
    if (s.length() <= 1)
      return 0;

    // Initialize curMax to zero
    int curMax = 0;
    int[] longest = new int[s.length()];

    // Iterate over the String starting from second index
    for (int i = 1; i < s.length(); i++)
    {
      if (s.charAt(i) == ')' && i - longest[i - 1] - 1 >= 0
          && s.charAt(i - longest[i - 1] - 1) == '(')
      {
        longest[i]
          = longest[i - 1] + 2
          + ((i - longest[i - 1] - 2 >= 0)
             ? longest[i - longest[i - 1] - 2]
             : 0);
        curMax = Math.max(longest[i], curMax);
      }
    }
    return curMax;
  }

  // Driver code
  public static void main(String[] args)
  {
    String str = "((()()";

    // Function call
    System.out.print(findMaxLen(str) +"\n");

    str = "()(()))))";

    // Function call
    System.out.print(findMaxLen(str) +"\n");

  }
}

// This code is contributed by aashish1995
```

## 蟒蛇 3

```
# Python3 program to find length of
# the longest valid substring

def findMaxLen(s):
    if (len(s) <= 1):
        return 0

    # Initialize curMax to zero
    curMax = 0

    longest = [0] * (len(s))

    # Iterate over the string starting
    # from second index
    for i in range(1, len(s)):
        if ((s[i] == ')'
             and i - longest[i - 1] - 1 >= 0
             and s[i - longest[i - 1] - 1] == '(')):

            longest[i] = longest[i - 1] + 2
            if (i - longest[i - 1] - 2 >= 0):
                longest[i] += (longest[i -
                                       longest[i - 1] - 2])
            else:
                longest[i] += 0
            curMax = max(longest[i], curMax)
    return curMax

# Driver Code
if __name__ == '__main__':
    Str = "((()()"

    # Function call
    print(findMaxLen(Str))

    Str = "()(()))))"

    # Function call
    print(findMaxLen(Str))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find length of the longest valid
// subString
using System;

public class GFG {

    static int findMaxLen(String s) {
        if (s.Length <= 1)
            return 0;

        // Initialize curMax to zero
        int curMax = 0;
        int[] longest = new int[s.Length];

        // Iterate over the String starting from second index
        for (int i = 1; i < s.Length; i++) {
            if (s[i] == ')' && i - longest[i - 1] - 1 >= 0 && s[i - longest[i - 1] - 1] == '(') {
                longest[i] = longest[i - 1] + 2 + ((i - longest[i - 1] - 2 >= 0) ? longest[i - longest[i - 1] - 2] : 0);
                curMax = Math.Max(longest[i], curMax);
            }
        }
        return curMax;
    }

    // Driver code
    public static void Main(String[] args) {
        String str = "((()()";

        // Function call
        Console.Write(findMaxLen(str) + "\n");

        str = "()(()))))";

        // Function call
        Console.Write(findMaxLen(str) + "\n");
    }
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>
// javascript program to find length of the longest valid
// subString
    function findMaxLen( s) {
        if (s.length <= 1)
            return 0;

        // Initialize curMax to zero
        var curMax = 0;
        var longest = Array(s.length).fill(0);

        // Iterate over the String starting from second index
        for (var i = 1; i < s.length; i++) {
            if (s[i] == ')' && i - longest[i - 1] - 1 >= 0 && s[i - longest[i - 1] - 1] == '(') {
                longest[i] = longest[i - 1] + 2 + ((i - longest[i - 1] - 2 >= 0) ? longest[i - longest[i - 1] - 2] : 0);
                curMax = Math.max(longest[i], curMax);
            }
        }
        return curMax;
    }

    // Driver code
        var str = "((()()";

        // Function call
        document.write(findMaxLen(str) + "<br\>");

        str = "()(()))))";

        // Function call
        document.write(findMaxLen(str) + "<br\>");

// This code is contributed by umadevi9616
</script>
```

**Output**

```
4
6
```

感谢 Gaurav Ahirwar 和 [Ekta Goel](https://www.linkedin.com/pub/ekta-goel/75/12a/3a6) 对上述方法的建议。

**O(1)辅助空间和 O(N)时间复杂度的另一种方法:**

1.  解决这个问题的思路是，在两个计数器**左**和**右**的帮助下，遍历字符串，分别跟踪开括号和闭括号的计数。
2.  首先，字符串从左向右遍历，对于遇到的每一个“ **(** ”，**左计数器**增加 1，对于每一个“ **)** ”，**右计数器**增加 1。
3.  每当左边等于右边时，计算当前有效字符串的长度，如果它大于当前最长的子字符串，则所需最长子字符串的值用当前字符串长度更新。
4.  如果右边的计数器变得大于左边的计数器，那么括号组就变成了**无效的**，因此左边和右边的计数器被**设置为 0** 。
5.  在上述过程之后，类似地从右向左遍历字符串，并应用类似的过程。

下面是上述方法的实现:

## C++

```
// C++ program to implement the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the length of
// the longest valid substring
int solve(string s, int n)
{

    // Variables for left and right counter.
    // maxlength to store the maximum length found so far
    int left = 0, right = 0, maxlength = 0;

    // Iterating the string from left to right
    for (int i = 0; i < n; i++)
    {
        // If "(" is encountered,
        // then left counter is incremented
        // else right counter is incremented
        if (s[i] == '(')
            left++;
        else
            right++;

        // Whenever left is equal to right, it signifies
        // that the subsequence is valid and
        if (left == right)
            maxlength = max(maxlength, 2 * right);

        // Reseting the counters when the subsequence
        // becomes invalid
        else if (right > left)
            left = right = 0;
    }

    left = right = 0;

    // Iterating the string from right to left
    for (int i = n - 1; i >= 0; i--) {

        // If "(" is encountered,
        // then left counter is incremented
        // else right counter is incremented
        if (s[i] == '(')
            left++;
        else
            right++;

        // Whenever left is equal to right, it signifies
        // that the subsequence is valid and
        if (left == right)
            maxlength = max(maxlength, 2 * left);

        // Reseting the counters when the subsequence
        // becomes invalid
        else if (left > right)
            left = right = 0;
    }
    return maxlength;
}

//A much shorter and concise version of the above code
int solve2(string s, int n){
    int left=0,right=0,maxlength=0,t=2;
      while(t--){
        left=0;
        right=0;
        for(int i=0;i<n;i++){
            if(s[i]=='(')left++;
            else right++;

            if(left==right){
                maxlength=max(maxlength,2*left);
            }
            //when travelling from 0 to n-1   
            if(t%2==1 && right>left){
                left=0;
                right=0;
              }
              //when travelling from n-1 to 0
              if(t%2==0 && left>right){
                  left=0;
                  right=0;
              }
            }
              //now we need to do the same thing from the other side;
            reverse(s.begin(),s.end());
        }
        return maxlength;
}

// Driver code
int main()
{

    // Function call
    cout << solve("((()()()()(((())", 16);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
import java.util.Scanner;
import java.util.Arrays;

class GFG {

    // Function to return the length
    // of the longest valid substring
    public static int solve(String s, int n)
    {

        // Variables for left and right
        // counter maxlength to store
        // the maximum length found so far
        int left = 0, right = 0;
        int maxlength = 0;

        // Iterating the string from left to right
        for (int i = 0; i < n; i++) {

            // If "(" is encountered, then
            // left counter is incremented
            // else right counter is incremented
            if (s.charAt(i) == '(')
                left++;
            else
                right++;

            // Whenever left is equal to right,
            // it signifies that the subsequence
            // is valid and
            if (left == right)
                maxlength = Math.max(maxlength,
                                     2 * right);

            // Reseting the counters when the
            // subsequence becomes invalid
            else if (right > left)
                left = right = 0;
        }

        left = right = 0;

        // Iterating the string from right to left
        for (int i = n - 1; i >= 0; i--) {

            // If "(" is encountered, then
            // left counter is incremented
            // else right counter is incremented
            if (s.charAt(i) == '(')
                left++;
            else
                right++;

            // Whenever left is equal to right,
            // it signifies that the subsequence
            // is valid and
            if (left == right)
                maxlength = Math.max(maxlength,
                                     2 * left);

            // Reseting the counters when the
            // subsequence becomes invalid
            else if (left > right)
                left = right = 0;
        }
        return maxlength;
    }

    // Driver code
    public static void main(String args[])
    {
        // Function call
        System.out.print(solve("((()()()()(((())", 16));
    }
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program to implement the above approach

# Function to return the length of
# the longest valid substring

def solve(s, n):

    # Variables for left and right counter.
    # maxlength to store the maximum length found so far
    left = 0
    right = 0
    maxlength = 0

    # Iterating the string from left to right
    for i in range(n):

        # If "(" is encountered,
        # then left counter is incremented
        # else right counter is incremented
        if (s[i] == '('):
            left += 1
        else:
            right += 1

        # Whenever left is equal to right, it signifies
        # that the subsequence is valid and
        if (left == right):
            maxlength = max(maxlength, 2 * right)

        # Reseting the counters when the subsequence
        # becomes invalid
        elif (right > left):
            left = right = 0

    left = right = 0

    # Iterating the string from right to left
    for i in range(n - 1, -1, -1):

        # If "(" is encountered,
        # then left counter is incremented
        # else right counter is incremented
        if (s[i] == '('):
            left += 1
        else:
            right += 1

        # Whenever left is equal to right, it signifies
        # that the subsequence is valid and
        if (left == right):
            maxlength = max(maxlength, 2 * left)

        # Reseting the counters when the subsequence
        # becomes invalid
        elif (left > right):
            left = right = 0
    return maxlength

# Driver code
# Function call
print(solve("((()()()()(((())", 16))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to implement the above approach
using System;

public class GFG {

  // Function to return the length
  // of the longest valid substring
  public static int solve(String s, int n)
  {

    // Variables for left and right
    // counter maxlength to store
    // the maximum length found so far
    int left = 0, right = 0;
    int maxlength = 0;

    // Iterating the string from left to right
    for (int i = 0; i < n; i++) {

      // If "(" is encountered, then
      // left counter is incremented
      // else right counter is incremented
      if (s[i] == '(')
        left++;
      else
        right++;

      // Whenever left is equal to right,
      // it signifies that the subsequence
      // is valid and
      if (left == right)
        maxlength = Math.Max(maxlength,
                             2 * right);

      // Reseting the counters when the
      // subsequence becomes invalid
      else if (right > left)
        left = right = 0;
    }

    left = right = 0;

    // Iterating the string from right to left
    for (int i = n - 1; i >= 0; i--) {

      // If "(" is encountered, then
      // left counter is incremented
      // else right counter is incremented
      if (s[i] == '(')
        left++;
      else
        right++;

      // Whenever left is equal to right,
      // it signifies that the subsequence
      // is valid and
      if (left == right)
        maxlength = Math.Max(maxlength,
                             2 * left);

      // Reseting the counters when the
      // subsequence becomes invalid
      else if (left > right)
        left = right = 0;
    }
    return maxlength;
  }

  // Driver code
  public static void Main(String []args)
  {
    // Function call
    Console.Write(solve("((()()()()(((())", 16));
  }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to implement the above approach

// Function to return the length of
// the longest valid substring
function solve(s, n)
{

    // Variables for left and right counter.
    // maxlength to store the maximum length found so far
    let left = 0, right = 0, maxlength = 0;

    // Iterating the string from left to right
    for (let i = 0; i < n; i++)
    {
        // If "(" is encountered,
        // then left counter is incremented
        // else right counter is incremented
        if (s[i] == '(')
            left++;
        else
            right++;

        // Whenever left is equal to right, it signifies
        // that the subsequence is valid and
        if (left == right)
            maxlength = max(maxlength, 2 * right);

        // Reseting the counters when the subsequence
        // becomes invalid
        else if (right > left)
            left = right = 0;
    }

    left = right = 0;

    // Iterating the string from right to left
    for (let i = n - 1; i >= 0; i--) {

        // If "(" is encountered,
        // then left counter is incremented
        // else right counter is incremented
        if (s[i] == '(')
            left++;
        else
            right++;

        // Whenever left is equal to right, it signifies
        // that the subsequence is valid and
        if (left == right)
            maxlength = Math.max(maxlength, 2 * left);

        // Reseting the counters when the subsequence
        // becomes invalid
        else if (left > right)
            left = right = 0;
    }
    return maxlength;
}

// Driver code

    // Function call
    document.write( solve("((()()()()(((())", 16));

//This code is contributed by Manoj
</script>
```

**Output**

```
8
```

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。