# 给定二进制字符串中连续 1 组的计数

> 原文:[https://www . geesforgeks . org/给定二进制字符串中连续 1 的组数/](https://www.geeksforgeeks.org/count-of-groups-of-consecutive-1s-in-a-given-binary-string/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是只在字符串 **S** 中找到 **1** s 的组数。

**示例:**

> **输入:** S = "100110111 "，N = 9
> **输出:** 3
> **说明:**
> 以下各组仅为 1s:
> 
> 1.  在等于“1”的[0，0]范围内分组。
> 2.  在等于“11”的范围[3，4]上分组。
> 3.  在等于“111”的范围[6，8]上分组。
> 
> 因此，总共只有 3 组 1。
> 
> **输入:**S = " 0101 "
> T3】输出: 2

**方法:**这个问题可以通过[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符来解决。按照以下步骤解决问题:

*   初始化一个变量，比如**计数**为 **0** ，它将 **1** s 的子串数存储在 **S** 中。
*   初始化一个[栈](https://www.geeksforgeeks.org/stack-in-cpp-stl/)说 **st** 只在 **1** s 的索引前存储子串。
*   [使用变量 **i** 迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 的字符，并执行以下操作:
    *   如果当前角色为 **1** ，将 **1** 推入堆叠 **st** 。
    *   否则，如果 **st** 不为空，则按 **1** 递增**计数**。否则[清除](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/) **st** 。
*   如果 **st** 不为空，则按 **1、**递增**计数**，即如果有 **1s 的后缀。**
*   最后，打印得到的总计**计数**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of the
// groups of 1s only in the binary
// string
int groupsOfOnes(string S, int N)
{
    // Stores number of groups of 1s
    int count = 0;

    // Initialization of the stack
    stack<int> st;

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If S[i] is '1'
        if (S[i] == '1')
            st.push(1);
        // Otherwise
        else {
            // If st is empty
            if (!st.empty()) {
                count++;
                while (!st.empty()) {
                    st.pop();
                }
            }
        }
    }
    // If st is not empty
    if (!st.empty())
        count++;

    // Return answer
    return count;
}
// Driver code
int main()
{
    // Input
    string S = "100110111";
    int N = S.length();

    // Function call
    cout << groupsOfOnes(S, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Stack;

class GFG{

// Function to find the number of the
// groups of 1s only in the binary
// string
static int groupsOfOnes(String S, int N)
{

    // Stores number of groups of 1s
    int count = 0;

    // Initialization of the stack
    Stack<Integer> st = new Stack<>();

    // Traverse the string S
    for(int i = 0; i < N; i++)
    {

        // If S[i] is '1'
        if (S.charAt(i) == '1')
            st.push(1);

        // Otherwise
        else
        {

            // If st is empty
            if (!st.empty())
            {
                count++;
                while (!st.empty())
                {
                    st.pop();
                }
            }
        }
    }

    // If st is not empty
    if (!st.empty())
        count++;

    // Return answer
    return count;
}

// Driver code
public static void main(String[] args)
{

    // Input
    String S = "100110111";
    int N = S.length();

    // Function call
    System.out.println(groupsOfOnes(S, N));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of the
# groups of 1s only in the binary
# string
def groupsOfOnes(S, N):

    # Stores number of groups of 1s
    count = 0

    # Initialization of the stack
    st = []

    # Traverse the string S
    for i in range(N):

        # If S[i] is '1'
        if (S[i] == '1'):
            st.append(1)

        # Otherwise
        else:

            # If st is empty
            if (len(st) > 0):
                count += 1
                while (len(st) > 0):
                    del st[-1]

    # If st is not empty
    if (len(st)):
        count += 1

    # Return answer
    return count

# Driver code
if __name__ == '__main__':

    # Input
    S = "100110111"
    N = len(S)

    # Function call
    print(groupsOfOnes(S, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the number of the
// groups of 1s only in the binary
// string
static int groupsOfOnes(string S, int N)
{

    // Stores number of groups of 1s
    int count = 0;

    // Initialization of the stack
    Stack<int> st = new Stack<int>();

    // Traverse the string S
    for (int i = 0; i < N; i++) {

        // If S[i] is '1'
        if (S[i] == '1')
            st.Push(1);
        // Otherwise
        else {
            // If st is empty
            if (st.Count > 0) {
                count++;
                while (st.Count > 0) {
                    st.Pop();
                }
            }
        }
    }

    // If st is not empty
    if (st.Count > 0)
        count++;

    // Return answer
    return count;
}

// Driver code
public static void Main()
{
    // Input
    string S = "100110111";
    int N = S.Length;

    // Function call
    Console.Write(groupsOfOnes(S, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the number of the
        // groups of 1s only in the binary
        // string
        function groupsOfOnes(S, N) {
            // Stores number of groups of 1s
            let count = 0;

            // Initialization of the stack
            var st = [];

            // Traverse the string S
            for (let i = 0; i < N; i++) {

                // If S[i] is '1'
                if (S[i] == '1')
                    st.push(1);
                // Otherwise
                else {
                    // If st is empty
                    if (st.length != 0) {
                        count++;
                        while (st.length != 0) {
                            st.pop();
                        }
                    }
                }
            }
            // If st is not empty
            if (st.length != 0)
                count++;

            // Return answer
            return count;
        }
        // Driver code

        // Input
        var S = "100110111";
        let N = S.length;

        // Function call
        document.write(groupsOfOnes(S, N));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)