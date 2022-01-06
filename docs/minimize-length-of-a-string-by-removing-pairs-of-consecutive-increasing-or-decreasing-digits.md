# 通过移除成对的连续递增或递减的数字来最小化字符串的长度

> 原文:[https://www . geesforgeks . org/通过移除成对的连续递增或递减数字来最小化字符串长度/](https://www.geeksforgeeks.org/minimize-length-of-a-string-by-removing-pairs-of-consecutive-increasing-or-decreasing-digits/)

给定一个由 **N** 个数字组成的数字[串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到串的个最小[长度，该长度可以通过重复去除以递增或递减顺序排列的相邻连续字符对而形成。](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)

**示例:**

> **输入:** S = "12213"
> **输出:** 1
> **说明:**
> 通过以下方式去除元素可以得到的字符串 S 的最小长度:
> 
> 1.  删除子字符串{S[0]，S[1]}。字符串 S 修改为“213”
> 2.  删除子字符串{S[0]，S[1]}。字符串 S 修改为“3”
> 
> 因此，字符串 S 的长度为 1，这是可能的最小长度。
> 
> **输入:**S = " 1350 "
> T3】输出: 4

**方法:**给定的问题可以使用[堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)来解决。按照以下步骤解决问题:

*   初始化一个[栈](https://www.geeksforgeeks.org/stack-data-structure/)，比如说 **St** ，存储给定字符串的字符。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   如果[堆叠 **St** 为空](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)，则按下堆叠 **St** 中的字符**S【I】**。
    *   如果堆叠的[顶部，即 **St.top()** 和 **S[i]** 处的字符的绝对值为 **1** ，则](https://www.geeksforgeeks.org/stack-top-c-stl/)[从堆叠](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)中弹出该元素。否则，按下堆栈 **St** 中的字符 **S[i]** 。
*   完成以上步骤后，打印[堆栈的大小](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/) **St** 作为结果。

下面是该方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum length
// of the string possible after removing
// pairs of consecutive digits
int minLength(string S)
{
    // Initialize the stack st
    stack<char> st;

    // Traverse the string S
    for (auto ch : S) {

        // If the stack is empty
        if (st.empty())
            st.push(ch);

        // Otherwise
        else {

            // Get the top character
            // of the stack
            char top = st.top();

            // If cha and top are
            // consecutive digits
            if (abs(ch - top) == 1)
                st.pop();

            // Otherwise, push the
            // character ch
            else {
                st.push(ch);
            }
        }
    }

    // Print the size of the stack
    return st.size();
}

// Driver Code
int main()
{
    string S = "12213";
    cout << minLength(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to find the minimum length
    // of the string possible after removing
    // pairs of consecutive digits
    static int minLength(String S)
    {
        // Initialize the stack st
        Stack<Character> st = new Stack<>();

        // Traverse the string S
        for (char ch : S.toCharArray()) {

            // If the stack is empty
            if (st.isEmpty())
                st.push(ch);

            // Otherwise
            else {

                // Get the top character
                // of the stack
                char top = st.peek();

                // If cha and top are
                // consecutive digits
                if (Math.abs(ch - top) == 1)
                    st.pop();

                // Otherwise, push the
                // character ch
                else {
                    st.push(ch);
                }
            }
        }

        // Print the size of the stack
        return st.size();
    }

    // Driver Code
    public static void main(String[] args)
    {

        String S = "12213";
        System.out.println(minLength(S));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum length
# of the string possible after removing
# pairs of consecutive digits
def minLength(S):

    # Initialize the stack st
    st = []

    # Traverse the string S
    for ch in S:

        # If the stack is empty
        if (len(st) == 0):
            st.append(ch)

        # Otherwise
        else:

            # Get the top character
            # of the stack
            top = st[-1]

            # If cha and top are
            # consecutive digits
            if (abs(ord(ch) - ord(top)) == 1):
                st.pop()

            # Otherwise, push the
            # character ch
            else:
                st.append(ch)

    # Print the size of the stack
    return len(st)

# Driver Code
if __name__ == "__main__":

    S = "12213"
    print(minLength(S))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum length
// of the string possible after removing
// pairs of consecutive digits
static int minLength(String S)
{

    // Initialize the stack st
    Stack<char> st = new Stack<char>();

    // Traverse the string S
    foreach (char ch in S.ToCharArray())
    {

        // If the stack is empty
        if (st.Count == 0)
            st.Push(ch);

        // Otherwise
        else
        {

            // Get the top character
            // of the stack
            char top = st.Peek();

            // If cha and top are
            // consecutive digits
            if (Math.Abs(ch - top) == 1)
                st.Pop();

            // Otherwise, push the
            // character ch
            else
            {
                st.Push(ch);
            }
        }
    }

    // Print the size of the stack
    return st.Count;
}

// Driver Code
public static void Main(String[] args)
{
    String S = "12213";
    Console.WriteLine(minLength(S));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum length
// of the string possible after removing
// pairs of consecutive digits
function minLength(S)
{
    // Initialize the stack st
    var st = [];

    // Traverse the string S
    S.split('').forEach(ch => {

        // If the stack is empty
        if (st.length==0)
            st.push(ch);

        // Otherwise
        else {

            // Get the top character
            // of the stack
            var top =st[st.length-1];

            // If cha and top are
            // consecutive digits
            if (Math.abs(ch - top) == 1)
                st.pop();

            // Otherwise, push the
            // character ch
            else {
                st.push(ch);
            }
        }
    });

    // Print the size of the stack
    return st.length;
}

// Driver Code
var S = "12213";
document.write( minLength(S));

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)