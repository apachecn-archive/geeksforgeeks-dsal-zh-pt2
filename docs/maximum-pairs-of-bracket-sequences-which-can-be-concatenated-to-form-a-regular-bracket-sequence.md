# 最多成对的括号序列，可以连接起来形成一个规则的括号序列

> 原文:[https://www . geeksforgeeks . org/最大括号序列对-哪些可以被连接以形成规则的括号序列/](https://www.geeksforgeeks.org/maximum-pairs-of-bracket-sequences-which-can-be-concatenated-to-form-a-regular-bracket-sequence/)

给定一个由 **N** [个字符串](https://www.geeksforgeeks.org/string-data-structure/)组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，使得每个字符串由字符**(**和**)**组成，任务是找到最大数量的字符串对，使得两个字符串的连接是一个**正则括号序列**。

> A **正则括号序列**是由括号**'(**和**')**组成的字符串，这样从字符串开头开始的每个前缀的**'(**大于或等于**')**的计数和**'(**和**')**的计数在整个字符串中是相等的。例如:“(())”、“()((())”、…，等等

**示例:**

> **输入:** arr[] = {“))”、“”、“(”、“(”、“(”、“(”、“”、“”)”}
> T3】输出:2
> T6】解释:T8】以下为一对字符串:
> 
> 1.  **(2，1):** 索引处的字符串为**”((**和**)“**。现在，这些字符串的连接是**”(()())“**，这是一个常规的括号序列。
> 2.  **(4，5):** 指标处的字符串为**(**、**)**。现在，这些字符串的连接是**“()”**，这是一个常规的括号序列。
> 
> 因此，规则括号序列对的总数是 2。
> 
> **输入:** arr[] = { "(())"、"()" }
> **输出:** 1

**简单方法:**解决给定问题的最简单方法是[从给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的字符串对，并计算那些串联后得到**正则括号序列**的字符串对。检查所有可能的配对后，打印获得的总计数。

***时间复杂度:** O(L*N <sup>2</sup> ，其中 L 为弦的最大长度。*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过用一对 **(A，B)** 来描述每个字符串来优化，其中 **A** 和 **B** 是最小值，使得在字符串左侧添加 **A** 开括号**”(**和字符串右侧添加 **B** 闭括号**“**后，它成为一个规则的括号序列。要连接两个括号序列(例如，**I<sup>th</sup>T19】和 **j <sup>th</sup>** )以产生正确的括号序列，第 I 个序列中左括号的超出部分必须等于第 j <sup>th</sup> 序列中右括号的超出部分；即**b<sub>I</sub>= a<sub>j</sub>**。按照以下步骤解决问题:**

*   初始化两个[数组](https://www.geeksforgeeks.org/array-data-structure/)，说**开[]** 和**关[]** 到 **0** 。此外，初始化一个整数变量**和**到 **0** ，存储结果对的计数。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下步骤:
    *   使用[这篇](https://www.geeksforgeeks.org/convert-an-unbalanced-bracket-sequence-to-a-balanced-sequence/?ref=rp)文章中讨论的方法，找出需要分别添加到 **arr[i]** 左右的左圆括号和右圆括号的数量，使 **arr[i]** 成为一个规则的括号序列。取值分别为 **a** 和 **b** 。
    *   如果**一个！=0 和 b！=0** 然后**arr【I】**将要求其两侧都有括号，因此**不可能将其与任何其他字符串连接起来。**
    *   如果 **a==0 和 b==0** ，那么这个特定的字符串已经是一个规则的括号序列，并且可以与其他规则的括号序列的字符串配对。
    *   否则，如果 **a** 等于 **0** ，则通过 **1** 增加**关闭**，否则通过 **1** 增加**打开**。
*   将**(关[0]/2)** 的 [**楼层**](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) 的值加到 **ans** 的值上。
*   [遍历数组**打开[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，将**打开**和**关闭**的最小值加到变量**和**上。
*   完成上述步骤后，打印**和**的值作为结果。

以下是上述方法的实施情况

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to count the number of
    // pairs whose concatenation results
    // in the regular bracket sequence
    static void countPairs(
        int N, ArrayList<String> arr)
    {
        // Stores the count of opening
        // and closing parenthesis for
        // each string arr[i]
        int open[] = new int[100];
        int close[] = new int[100];

        // Stores maximum count of pairs
        int ans = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            char c[] = arr.get(i).toCharArray();
            int d = 0;
            int min = 0;

            // Traverse the string c[]
            for (int j = 0; j < c.length; j++) {

                // Opening Bracket
                if (c[j] == '(') {
                    d++;
                }

                // Otherwise, Closing
                // Bracket
                else {
                    d--;
                    if (d < min)
                        min = d;
                }
            }

            // Count of closing brackets
            // needed to balance string
            if (d >= 0) {
                if (min == 0)
                    close[d]++;
            }

            // Count of opening brackets
            // needed to balance string
            else if (d < 0) {
                if (min == d)
                    open[-d]++;
            }
        }

        // Add the count of balanced
        // sequences
        ans += close[0] / 2;

        // Traverse the array
        for (int i = 1; i < 100; i++) {
            ans += Math.min(
                open[i], close[i]);
        }

        // Print the resultant count
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 7;
        ArrayList<String> list = new ArrayList<String>();
        list.add(")())");
        list.add(")");
        list.add("((");
        list.add("((");
        list.add("(");
        list.add(")");
        list.add(")");

        countPairs(N, list);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# pairs whose concatenation results
# in the regular bracket sequence
def countPairs(N, arr):

    # Stores the count of opening
    # and closing parenthesis for
    # each string arr[i]
    open = [0] * 100
    close = [0] * 100

    # Stores maximum count of pairs
    ans = 0

    # Traverse the array arr[]
    for i in range(N):
        c = [i for i in arr[i]]
        d = 0
        minm = 0

        # Traverse the string c[]
        for j in range(len(c)):

            # Opening Bracket
            if (c[j] == '('):
                d += 1

            # Otherwise, Closing
            # Bracket
            else:
                d -= 1
                if (d < minm):
                    minm = d

        # Count of closing brackets
        # needed to balance string
        if (d >= 0):
            if (minm == 0):
                close[d] += 1

        # Count of opening brackets
        # needed to balance string
        elif (d < 0):
            if (minm == d):
                open[-d] += 1

    # Add the count of balanced
    # sequences
    ans += close[0] // 2

    # Traverse the array
    for i in range(1, 100):
        ans +=min(open[i], close[i])

    # Print the resultant count
    print(ans)

# Driver Code
if __name__ == '__main__':

    N = 7
    list = []
    list.append(")())")
    list.append(")")
    list.append("((")
    list.append("((")
    list.append("(")
    list.append(")")
    list.append(")")

    countPairs(N, list)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of
// pairs whose concatenation results
// in the regular bracket sequence
static void countPairs(int N, List<string> arr)
{

    // Stores the count of opening
    // and closing parenthesis for
    // each string arr[i]
    int[] open = new int[100];
    int[] close = new int[100];

    // Stores maximum count of pairs
    int ans = 0;

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {
        char[] c = arr[i].ToCharArray();
        int d = 0;
        int min = 0;

        // Traverse the string c[]
        for(int j = 0; j < c.Length; j++)
        {

            // Opening Bracket
            if (c[j] == '(')
            {
                d++;
            }

            // Otherwise, Closing
            // Bracket
            else
            {
                d--;
                if (d < min)
                    min = d;
            }
        }

        // Count of closing brackets
        // needed to balance string
        if (d >= 0)
        {
            if (min == 0)
                close[d]++;
        }

        // Count of opening brackets
        // needed to balance string
        else if (d < 0)
        {
            if (min == d)
                open[-d]++;
        }
    }

    // Add the count of balanced
    // sequences
    ans += close[0] / 2;

    // Traverse the array
    for(int i = 1; i < 100; i++)
    {
        ans += Math.Min(open[i], close[i]);
    }

    // Print the resultant count
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(string[] args)
{
    int N = 7;
    List<string> list = new List<string>();
    list.Add(")())");
    list.Add(")");
    list.Add("((");
    list.Add("((");
    list.Add("(");
    list.Add(")");
    list.Add(")");

    countPairs(N, list);
}
}

// This code is contributed by ukasp
```

**Output:** 

```
2
```

***时间复杂度:** O(L*N)，其中 N 为字符串* *的最大* [*长度。*
***辅助空间:** O(L)*](https://www.geeksforgeeks.org/c-program-to-find-the-length-of-a-string/)