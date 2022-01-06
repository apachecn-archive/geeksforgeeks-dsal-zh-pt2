# 最大化移除所有子串“ab”和“ba”的成本

> 原文:[https://www . geeksforgeeks . org/最大化移除所有子字符串出现的成本-ab-and-ba/](https://www.geeksforgeeks.org/maximize-cost-of-removing-all-occurrences-of-substrings-ab-and-ba/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 和整数 **P** 和 **Q** ，分别表示从 **S** 中移除子字符串**【ab】**和**【ba】**的成本，任务是找出移除所有子字符串**【ab】**和**【ba】**的**最大成本**。

**示例:**

> **输入:**S =“cbbabbaab”，P = 6，Q = 4
> **输出:** 22
> **解释:**
> 从“cbba **ab** baab”中去掉子串“ab”，得到的字符串为“cbbabaab”。成本= 6。
> 从“cbb **ab** aab”中去掉子串“ab”，得到的字符串为“cbbaab”。成本= 6。
> 从“cb **ba** ab”中去掉子串“ba”，得到的字符串为“cbab”。成本= 4。
> 从“cb **ab** 中去掉子串“ab”，得到的字符串为“cb”。成本= 6。
> 总成本= 6 + 6 + 4 + 6 = **22**
> 
> **输入:**S =“bbaanaybabd”，P = 3，Q = 5
> **输出:** 15
> **解释:**
> 从“b **ba** anaybbabd”中去掉子串“ba”，得到的字符串为“banaybbabd”。成本= 5。
> 去掉子串“ba”，得到的字符串是“**ba**naybabd”，得到的字符串是“naybabd”。成本= 5。
> 从“nayb **ba** bd”中去掉子串“ba”，得到的字符串为“naybd”。成本= 5。
> 总成本= 5 + 5 + 5 = **15**

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并删除一种类型的子字符串。这可以通过使用**贪婪方法**来完成，如下所示:
    *   如果 **P > = Q** ，删除所有出现的“ab”子串，然后删除所有出现的“ba”子串。
    *   否则，删除所有出现的“ba”子串，然后删除所有出现的“ab”子串。
*   [堆栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)可以使用
*   根据大小为 2 的字符数组 **P 和 Q** 作为字符数组**maxstr【】**和**minstr【】**将我们的**高成本**和**低成本**字符串初始化为**“ab”或“ba”**，将最大成本和最小成本分别初始化为 **maxp** 和 **minp** 。
*   初始化变量，比如**成本**，存储最大成本
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并执行以下步骤:
    *   如果 [**栈不为空**](https://www.geeksforgeeks.org/stack-empty-method-in-java/) 和[栈顶](https://www.geeksforgeeks.org/stack-top-c-stl/)且当前字符形成**maxstr【】**，则[弹出](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)栈顶并将 **maxp** 加入成本。
    *   否则，将当前字符添加到堆栈中。
*   遍历剩余的字符串。
    *   如果 [**栈不为空**](https://www.geeksforgeeks.org/stack-empty-method-in-java/)[栈顶](https://www.geeksforgeeks.org/stack-top-c-stl/)且当前角色形成 minstr[]，则弹出栈顶并添加 **minp** 到成本。
    *   否则，将当前字符添加到堆栈中。
*   打印**成本**作为最大成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach:
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum cost of
// removing substrings "ab" and "ba" from S
int MaxCollection(string S, int P, int Q)
{
    // MaxStr is the substring char
    // array with larger cost
    char maxstr[2];
    string x = (P >= Q ? "ab" : "ba");
    strcpy(maxstr, x.c_str());

    // MinStr is the substring char
    // array with smaller cost;
    char minstr[2];
    x = (P >= Q ? "ba" : "ab");
    strcpy(minstr, x.c_str());

    // Denotes larger point
    int maxp = max(P, Q);

    // Denotes smaller point
    int minp = min(P, Q);

    // Stores cost scored
    int cost = 0;

    // Removing all occurrences of
    // maxstr from the S

    // Stack to keep track of characters
    stack<char> stack1;
    char s[S.length()];
    strcpy(s, S.c_str());

    // Traverse the string
    for (auto &ch : s) {

        // If the substring is maxstr

        if (!stack1.empty()
            && (stack1.top() == maxstr[0]
                && ch == maxstr[1])) {

            // Pop from the stack
            stack1.pop();

            // Add maxp to cost
            cost += maxp;
        }

        // Push the character to the stack
        else {

            stack1.push(ch);
        }
    }

    // Remaining string after removing maxstr
    string sb = "";

    // Find remaining string
    while (stack1.size() > 0)
    {
        sb = sb + stack1.top();
        stack1.pop();
    }

    // Reversing the string
    // retrieved from the stack
    reverse(sb.begin(), sb.end());

    // Removing all occurences of minstr
    for (auto &ch : sb) {

        // If the substring is minstr
        if (!stack1.empty()
            && (stack1.top() == minstr[0]
                && ch == minstr[1])) {

            // Pop from the stack
            stack1.pop();

            // Add minp to the cost
            cost += minp;
        }

        // Otherwise
        else {
            stack1.push(ch);
        }
    }

    // Return the maximum cost
    return cost;
}

int main()
{
    // Input String
    string S = "cbbaabbaab";

    // Costs
    int P = 6;
    int Q = 4;

    cout << MaxCollection(S, P, Q);

    return 0;
}

// This code is contributed by decode2207.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach:

import java.util.*;

class GFG {

    // Function to find the maximum cost of
    // removing substrings "ab" and "ba" from S
    public static int MaxCollection(
        String S, int P, int Q)
    {
        // MaxStr is the substring char
        // array with larger cost
        char maxstr[]
            = (P >= Q ? "ab" : "ba").toCharArray();

        // MinStr is the substring char
        // array with smaller cost;
        char minstr[]
            = (P >= Q ? "ba" : "ab").toCharArray();

        // Denotes larger point
        int maxp = Math.max(P, Q);

        // Denotes smaller point
        int minp = Math.min(P, Q);

        // Stores cost scored
        int cost = 0;

        // Removing all occurrences of
        // maxstr from the S

        // Stack to keep track of characters
        Stack<Character> stack1 = new Stack<>();
        char[] s = S.toCharArray();

        // Traverse the string
        for (char ch : s) {

            // If the substring is maxstr

            if (!stack1.isEmpty()
                && (stack1.peek() == maxstr[0]
                    && ch == maxstr[1])) {

                // Pop from the stack
                stack1.pop();

                // Add maxp to cost
                cost += maxp;
            }

            // Push the character to the stack
            else {

                stack1.push(ch);
            }
        }

        // Remaining string after removing maxstr
        StringBuilder sb = new StringBuilder();

        // Find remaining string
        while (!stack1.isEmpty())
            sb.append(stack1.pop());

        // Reversing the string
        // retrieved from the stack
        sb = sb.reverse();
        String remstr = sb.toString();

        // Removing all occurences of minstr
        for (char ch : remstr.toCharArray()) {

            // If the substring is minstr
            if (!stack1.isEmpty()
                && (stack1.peek() == minstr[0]
                    && ch == minstr[1])) {

                // Pop from the stack
                stack1.pop();

                // Add minp to the cost
                cost += minp;
            }

            // Otherwise
            else {
                stack1.push(ch);
            }
        }

        // Return the maximum cost
        return cost;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Input String
        String S = "cbbaabbaab";

        // Costs
        int P = 6;
        int Q = 4;

        System.out.println(MaxCollection(S, P, Q));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach:

# Function to find the maximum cost of
# removing substrings "ab" and "ba" from S
def MaxCollection(S, P, Q):

    # MaxStr is the substring char
    # array with larger cost
    maxstr = [i for i in ("ab" if P >= Q else "ba")]

    # MinStr is the substring char
    # array with smaller cost;
    minstr = [i for i in ("ba" if P >= Q else "ab")]

    # Denotes larger point
    maxp = max(P, Q)

    # Denotes smaller point
    minp = min(P, Q)

    # Stores cost scored
    cost = 0

    # Removing all occurrences of
    # maxstr from the S

    # Stack to keep track of characters
    stack1 = []
    s = [i for i in S]
    # Traverse the string
    for ch in s:

        # If the substring is maxstr

        if (len(stack1)>0 and (stack1[-1] == maxstr[0] and ch == maxstr[1])):

            # Pop from the stack
            del stack1[-1]

            # Add maxp to cost
            cost += maxp

        # Push the character to the stack
        else:
            stack1.append(ch)

    # Remaining string after removing maxstr
    sb = ""

    # Find remaining string
    while (len(stack1) > 0):
        sb += stack1[-1]
        del stack1[-1]

    # Reversing the string
    # retrieved from the stack
    sb = sb[::-1]
    remstr = sb

    # Removing all occurences of minstr
    for ch in remstr:

        # If the substring is minstr
        if (len(stack1) > 0 and (stack1[-1] == minstr[0] and ch == minstr[1])):

            #  Pop from the stack
            del stack1[-1]

            # Add minp to the cost
            cost += minp

        # Otherwise
        else:
            stack1.append(ch)

    # Return the maximum cost
    return cost

# Driver Code
if __name__ == '__main__':

    # Input String
    S = "cbbaabbaab"

    # Costs
    P = 6;
    Q = 4;

    print(MaxCollection(S, P, Q));

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach:
using System;
using System.Collections;
class GFG {

    // Function to find the maximum cost of
    // removing substrings "ab" and "ba" from S
    static int MaxCollection(string S, int P, int Q)
    {

        // MaxStr is the substring char
        // array with larger cost
        char[] maxstr = (P >= Q ? "ab" : "ba").ToCharArray();

        // MinStr is the substring char
        // array with smaller cost;
        char[] minstr = (P >= Q ? "ba" : "ab").ToCharArray();

        // Denotes larger point
        int maxp = Math.Max(P, Q);

        // Denotes smaller point
        int minp = Math.Min(P, Q);

        // Stores cost scored
        int cost = 0;

        // Removing all occurrences of
        // maxstr from the S

        // Stack to keep track of characters
        Stack stack1 = new Stack();
        char[] s = S.ToCharArray();

        // Traverse the string
        foreach(char ch in s) {

            // If the substring is maxstr

            if (stack1.Count > 0 && ((char)stack1.Peek() == maxstr[0] && ch == maxstr[1])) {

                // Pop from the stack
                stack1.Pop();

                // Add maxp to cost
                cost += maxp;
            }

            // Push the character to the stack
            else {

                stack1.Push(ch);
            }
        }

        // Remaining string after removing maxstr
        string sb = "";

        // Find remaining string
        while (stack1.Count > 0)
        {
            sb = sb + stack1.Peek();
            stack1.Pop();
        }

        // Reversing the string
        // retrieved from the stack
        char[] chars = sb.ToCharArray();
        Array.Reverse(chars);
        string remstr = new string(chars);

        // Removing all occurences of minstr
        foreach(char ch in remstr.ToCharArray()) {

            // If the substring is minstr
            if (stack1.Count > 0 && ((char)stack1.Peek() == minstr[0] && ch == minstr[1])) {

                // Pop from the stack
                stack1.Pop();

                // Add minp to the cost
                cost += minp;
            }

            // Otherwise
            else {
                stack1.Push(ch);
            }
        }

        // Return the maximum cost
        return cost;
    }

  static void Main()
  {
    // Input String
    string S = "cbbaabbaab";

    // Costs
    int P = 6;
    int Q = 4;

    Console.Write(MaxCollection(S, P, Q));
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach:

// Function to find the maximum cost of
    // removing substrings "ab" and "ba" from S
function MaxCollection(S,P,Q)
{
    // MaxStr is the substring char
        // array with larger cost
        let maxstr
            = (P >= Q ? "ab" : "ba").split("");

        // MinStr is the substring char
        // array with smaller cost;
        let minstr
            = (P >= Q ? "ba" : "ab").split("");

        // Denotes larger point
        let maxp = Math.max(P, Q);

        // Denotes smaller point
        let minp = Math.min(P, Q);

        // Stores cost scored
        let cost = 0;

        // Removing all occurrences of
        // maxstr from the S

        // Stack to keep track of characters
        let stack1 = [];
        let s = S.split("");

        // Traverse the string
        for (let ch=0;ch< s.length;ch++) {

            // If the substring is maxstr

            if (stack1.length!=0
                && (stack1[stack1.length-1] == maxstr[0]
                    && s[ch] == maxstr[1])) {

                // Pop from the stack
                stack1.pop();

                // Add maxp to cost
                cost += maxp;
            }

            // Push the character to the stack
            else {

                stack1.push(s[ch]);
            }
        }

        // Remaining string after removing maxstr
        let sb = [];

        // Find remaining string
        while (stack1.length!=0)
            sb.push(stack1.pop());

        // Reversing the string
        // retrieved from the stack
        sb = sb.reverse();
        let remstr = sb.join("");

        // Removing all occurences of minstr
        for (let ch =0;ch<remstr.length;ch++) {

            // If the substring is minstr
            if (stack1.length!=0
                && (stack1[stack1.length-1] == minstr[0]
                    && remstr[ch] == minstr[1])) {

                // Pop from the stack
                stack1.pop();

                // Add minp to the cost
                cost += minp;
            }

            // Otherwise
            else {
                stack1.push(remstr[ch]);
            }
        }

        // Return the maximum cost
        return cost;
}

// Driver Code
// Input String
        let S = "cbbaabbaab";

        // Costs
        let P = 6;
        let Q = 4;

        document.write(MaxCollection(S, P, Q));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
22
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)