# 进行平衡顺序所需的最小操作

> 原文:[https://www . geeksforgeeks . org/制作平衡序列所需的最小操作数/](https://www.geeksforgeeks.org/minimum-operation-required-to-make-a-balanced-sequence/)

平衡序列被定义为一个字符串，其中每个左括号都有两个连续的右括号。因此， **{}、{{}}}、{ } } { } } }**是平衡的，而**} {、{}** 是不平衡的。
现在给定一个括号序列(“{”和“}”)，您只能对该序列执行一个操作，即在任意位置插入左括号或右括号。你必须说出使给定序列平衡所需的最小操作数。

> **输入:**str =“{ } }”
> T3】输出: 0
> 序列已经平衡。
> **输入:**str =“{ } { } }”
> **输出:** 3
> 更新后的序列将为“{ }**}**{ }**{ }**}”。

**进场:**为了做出均衡的顺序，每一个开口括号需要两个连续的闭合括号。可能有 3 种情况:

1.  **当** **当前字符为左括号时:**如果前一个字符不是右括号，那么只需插入左括号进行堆叠，否则需要一个需要一次操作的右括号。
2.  **如果堆栈为空，并且当前字符是结束括号:**在这种情况下，需要一个开始括号，这将花费一次操作，并将该开始括号插入堆栈。
3.  **如果栈不是空的，但是** **当前字符是右括号:**这里只需要右括号的个数。如果是 2，则从堆栈中移除一个左括号，否则增加右括号的计数。

在字符串的末尾，如果堆栈不为空，则所需的结束括号数将为((2 *堆栈大小)–当前结束括号数)。
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum operations required
int minOperations(string s, int len)
{
    int operationCnt = 0;
    stack<char> st;
    int cntClosing = 0;
    for (int i = 0; i < len; i++) {

        // Condition where we got only one closing
        // bracket instead of 2, here we have to
        // add one more closing bracket to
        // make the sequence balanced
        if (s[i] == '{') {
            if (cntClosing > 0) {

                // Add closing bracket that
                // costs us one operation
                operationCnt++;

                // Remove the top opening bracket because
                // we got the 1 opening and 2
                // continuous closing brackets
                st.pop();
            }

            // Inserting the opening bracket to stack
            st.push(s[i]);

            // After making the sequence balanced
            // closing is now set to 0
            cntClosing = 0;
        }
        else if (st.empty()) {

            // Case when there is no opening bracket
            // the sequence starts with a closing bracket
            // and one opening bracket is required
            // Now we have one opening and one closing bracket
            st.push('{');

            // Add opening bracket that
            // costs us one operation
            operationCnt++;

            // Assigning 1 to cntClosing because
            // we have one closing bracket
            cntClosing = 1;
        }
        else {
            cntClosing = (cntClosing + 1) % 2;

            // Case where we got two continuous closing brackets
            // Need to pop one opening bracket from stack top
            if (cntClosing == 0) {
                st.pop();
            }
        }
    }

    // Condition where stack is not empty
    // This is the case where we have
    // only opening brackets
    // (st.size() * 2) will give us the total
    // closing bracket needed
    // cntClosing is the count of closing
    // bracket that we already have
    operationCnt += st.size() * 2 - cntClosing;
    return operationCnt;
}

// Driver code
int main()
{
    string str = "}}{";
    int len = str.length();

    cout << minOperations(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// Function to return the
// minimum operations required
static int minOperations(String s, int len)
{
    int operationCnt = 0;
    Stack<Character> st = new Stack<Character>();
    int cntClosing = 0;

    for(int i = 0; i < len; i++)
    {

       // Condition where we got only one
       // closing bracket instead of 2,
       // here we have to add one more
       // closing bracket to make the
       // sequence balanced
       if (s.charAt(i) == '{')
       {
           if (cntClosing > 0)
           {

               // Add closing bracket that
               // costs us one operation
               operationCnt++;

               // Remove the top opening bracket
               // because we got the 1 opening
               // and 2 continuous closing brackets
               st.pop();
           }

           // Inserting the opening bracket to stack
           st.add(s.charAt(i));

           // After making the sequence balanced
           // closing is now set to 0
           cntClosing = 0;
       }
       else if (st.isEmpty())
       {

           // Case when there is no opening
           // bracket the sequence starts
           // with a closing bracket and
           // one opening bracket is required
           // Now we have one opening and one
           // closing bracket
           st.add('{');

           // Add opening bracket that
           // costs us one operation
           operationCnt++;

           // Assigning 1 to cntClosing because
           // we have one closing bracket
            cntClosing = 1;
       }
       else
       {
           cntClosing = (cntClosing + 1) % 2;

           // Case where we got two continuous
           // closing brackets need to pop one
           // opening bracket from stack top
           if (cntClosing == 0)
           {
               st.pop();
           }
       }
    }

    // Condition where stack is not empty
    // This is the case where we have only
    // opening brackets (st.size() * 2)
    // will give us the total closing
    // bracket needed cntClosing is the
    // count of closing bracket that
    // we already have
    operationCnt += st.size() * 2 - cntClosing;

    return operationCnt;
}

// Driver code
public static void main(String[] args)
{
    String str = "}}{";
    int len = str.length();

    System.out.print(minOperations(str, len));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation
# of the approach
from queue import LifoQueue 

# Function to return the
# minimum operations required
def minOperations(s, len):

    operationCnt = 0;
    st = LifoQueue();
    cntClosing = 0;

    for i in range(0, len):

        # Condition where we got only one
        # closing bracket instead of 2,
        # here we have to add one more
        # closing bracket to make the
        # sequence balanced
        if (s[i] == '{'):

            if (cntClosing > 0):

                # Add closing bracket that
                # costs us one operation
                operationCnt += 1;

                # Remove the top opening bracket
                # because we got the 1 opening
                # and 2 continuous closing brackets
                st.pop();           

            # Inserting the opening bracket to stack
            st.put(s[i]);

            # After making the sequence balanced
            # closing is now set to 0
            cntClosing = 0;

        elif(st.empty()):

                # Case when there is no opening
                # bracket the sequence starts
                # with a closing bracket and
                # one opening bracket is required
                # Now we have one opening and one
                # closing bracket
                st.put('{');

                # Add opening bracket that
                # costs us one operation
                operationCnt += 1;

                # Assigning 1 to cntClosing because
                # we have one closing bracket
                cntClosing = 1;
        else:
            cntClosing = (cntClosing + 1) % 2;

            # Case where we got two continuous
            # closing brackets need to pop one
            # opening bracket from stack top
            if (cntClosing == 0):
                st.pop();   

    # Condition where stack is not empty
    # This is the case where we have only
    # opening brackets (st.size() * 2)
    # will give us the total closing
    # bracket needed cntClosing is the
    # count of closing bracket that
    # we already have
    operationCnt += st.qsize() * 2 - cntClosing + 1;

    return operationCnt;

# Driver code
if __name__ == '__main__':
    str = "{";
    print(minOperations(str, 1));

# This code is contributed by gauravrajput1
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to return the
// minimum operations required
static int minOperations(String s,
                         int len)
{
  int operationCnt = 0;
  Stack<char> st = new Stack<char>();
  int cntClosing = 0;

  for(int i = 0; i < len; i++)
  {       
    // Condition where we got only one
    // closing bracket instead of 2,
    // here we have to add one more
    // closing bracket to make the
    // sequence balanced
    if (s[i] == '{')
    {
      if (cntClosing > 0)
      {              
        // Add closing bracket that
        // costs us one operation
        operationCnt++;

        // Remove the top opening bracket
        // because we got the 1 opening
        // and 2 continuous closing brackets
        st.Pop();
      }

      // Inserting the opening bracket to stack
      st.Push(s[i]);

      // After making the sequence balanced
      // closing is now set to 0
      cntClosing = 0;
    }
    else if (st.Count != 0)
    {          
      // Case when there is no opening
      // bracket the sequence starts
      // with a closing bracket and
      // one opening bracket is required
      // Now we have one opening and one
      // closing bracket
      st.Push('{');

      // Add opening bracket that
      // costs us one operation
      operationCnt++;

      // Assigning 1 to cntClosing because
      // we have one closing bracket
      cntClosing = 1;
    }
    else
    {
      cntClosing = (cntClosing + 1) % 2;

      // Case where we got two continuous
      // closing brackets need to pop one
      // opening bracket from stack top
      if (cntClosing == 0 &&
          st.Count != 0)
      {
        st.Pop();
      }
    }
  }

  // Condition where stack is not empty
  // This is the case where we have only
  // opening brackets (st.Count * 2)
  // will give us the total closing
  // bracket needed cntClosing is the
  // count of closing bracket that
  // we already have
  operationCnt += st.Count * 2 -
                  cntClosing + 1;

  return operationCnt;
}

// Driver code
public static void Main(String[] args)
{
  String str = "}}{";
  int len = str.Length;
  Console.Write(minOperations(str,
                              len));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum operations required
function minOperations(s, len)
{
    var operationCnt = 0;
    var st = [];
    var cntClosing = 0;
    for (var i = 0; i < len; i++) {

        // Condition where we got only one closing
        // bracket instead of 2, here we have to
        // add one more closing bracket to
        // make the sequence balanced
        if (s[i] == '{') {
            if (cntClosing > 0) {

                // Add closing bracket that
                // costs us one operation
                operationCnt++;

                // Remove the top opening bracket because
                // we got the 1 opening and 2
                // continuous closing brackets
                st.pop();
            }

            // Inserting the opening bracket to stack
            st.push(s[i]);

            // After making the sequence balanced
            // closing is now set to 0
            cntClosing = 0;
        }
        else if (st.length==0) {

            // Case when there is no opening bracket
            // the sequence starts with a closing bracket
            // and one opening bracket is required
            // Now we have one opening and one closing bracket
            st.push('{');

            // Add opening bracket that
            // costs us one operation
            operationCnt++;

            // Assigning 1 to cntClosing because
            // we have one closing bracket
            cntClosing = 1;
        }
        else {
            cntClosing = (cntClosing + 1) % 2;

            // Case where we got two continuous closing brackets
            // Need to pop one opening bracket from stack top
            if (cntClosing == 0) {
                st.pop();
            }
        }
    }

    // Condition where stack is not empty
    // This is the case where we have
    // only opening brackets
    // (st.size() * 2) will give us the total
    // closing bracket needed
    // cntClosing is the count of closing
    // bracket that we already have
    operationCnt += st.length * 2 - cntClosing;
    return operationCnt;
}

// Driver code
var str = "}}{";
var len = str.length;
document.write( minOperations(str, len));

</script>
```

**Output:** 

```
3
```