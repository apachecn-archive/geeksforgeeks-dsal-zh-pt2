# 生成平衡支架序列所需的最小成本

> 原文:[https://www . geeksforgeeks . org/生成平衡括号序列所需的最低成本/](https://www.geeksforgeeks.org/minimum-cost-required-to-generate-a-balanced-bracket-sequence/)

给定长度为 **N** 的字符串**和两个整数 **A** 和 **B** ，任务是通过执行以下类型的任意数量的移动(*可能为零*)来从**字符串**中找到获得常规括号序列所需的最小成本:**

*   花费 **A** 从字符串中删除一个字符。
*   从字符串中删除一个字符，并在字符串末尾追加一个费用 **B** 。

> 平衡括号序列可以是以下类型:
> 
> *   空字符串
> *   由对应于每个左括号的右括号组成的字符串。

**示例:**

> **输入:** str = ")()"，A = 1，B = 2
> **输出:** 1
> **解释:**
> 移除 **0 <sup>第</sup>个字符**，即 **')'** ，花费 1，生成一个平衡字符串”()"。因此，最小成本为 1。
> 
> **输入:** str = ")("，A = 3，B = 9
> **输出:** 6
> **解释:**
> 删除 **0 <sup>第</sup>个字符**并追加在字符串末尾会生成一个平衡字符串”()"。
> 因此，成本= 9。
> 删除这两个字符会生成一个空字符串，代价为 6。
> 因此，生成平衡字符串的最小成本为 6。

**方法:**按照以下步骤解决问题:

*   统计给定字符串中打开 **'('** )和关闭 **')'** 括号的频率，并存储两者中较高的频率。
*   最小成本至少为**a *(ABS(open–count))**，因为需要移除这些支架以平衡管柱。
*   计算字符串中不平衡的左括号和右括号的数量。如果空括号是**多余**，那么将 ***不平衡空括号*** 的计数减少 ***多余空括号*** 的计数。同样，如果结束括号过多，减少 ***不平衡结束括号*** 的数量。
*   现在，计算移除所有不平衡开放和不平衡封闭支架的**成本，以及移除不平衡封闭支架并将其添加到最后**的**成本。比较并在答案中加上两个成本的最小值。**
*   因此，生成平衡括号序列所需的最小成本由以下等式给出:

> 生成平衡字符串的最小成本= **a * (abs(开–关))+ min( a*(非平衡开+非平衡闭)，b*(非平衡闭括号))**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum cost
// required to generate a balanced bracket
// sequence
void minCost(string str, int a, int b)
{
    // Stores the count of
    // unbalanced open brackets
    int openUnbalanced = 0;

    // Stores the count of
    // unbalanced closed brackets
    int closedUnbalanced = 0;

    // Stores the count of
    // open brackets
    int openCount = 0;

    // Stores the count of
    // closed brackets
    int closedCount = 0;

    for (int i = 0; str[i] != '\0'; i++) {

        // If open brace is encountered
        if (str[i] == '(') {
            openUnbalanced++;
            openCount++;
        }

        // Otherwise
        else {

            // If no unbalanced open
            // brackets are present
            if (openUnbalanced == 0)

                // Increase count of
                // unbalanced closed brackets
                closedUnbalanced++;

            // Otherwise
            else

                // Reduce count of
                // unbalanced open brackets
                openUnbalanced--;

            // Increase count of
            // closed brackets
            closedCount++;
        }
    }

    // Calculate lower bound of minimum cost
    int result = a * (abs(openCount
                          - closedCount));

    // Reduce excess open or closed brackets
    // to prevent counting them twice
    if (closedCount > openCount)
        closedUnbalanced
            -= (closedCount - openCount);

    if (openCount > closedCount)
        openUnbalanced
            -= (openCount - closedCount);

    // Update answer by adding minimum of
    // removing both unbalanced open and
    // closed brackets or inserting closed
    // unbalanced brackets to end of string
    result += min(a * (openUnbalanced
                       + closedUnbalanced),
                  b * closedUnbalanced);

    // Print the result
    cout << result << endl;
}

// Driver Code
int main()
{
    string str = "))()(()()(";
    int A = 1, B = 3;
    minCost(str, A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to calculate the minimum cost
// required to generate a balanced bracket
// sequence
static void minCost(String str, int a, int b)
{

    // Stores the count of
    // unbalanced open brackets
    int openUnbalanced = 0;

    // Stores the count of
    // unbalanced closed brackets
    int closedUnbalanced = 0;

    // Stores the count of
    // open brackets
    int openCount = 0;

    // Stores the count of
    // closed brackets
    int closedCount = 0;

    for(int i = 0; i < str.length(); i++)
    {

        // If open brace is encountered
        if (str.charAt(i) == '(')
        {
            openUnbalanced++;
            openCount++;
        }

        // Otherwise
        else
        {

            // If no unbalanced open
            // brackets are present
            if (openUnbalanced == 0)

                // Increase count of
                // unbalanced closed brackets
                closedUnbalanced++;

            // Otherwise
            else

                // Reduce count of
                // unbalanced open brackets
                openUnbalanced--;

            // Increase count of
            // closed brackets
            closedCount++;
        }
    }

    // Calculate lower bound of minimum cost
    int result = a * (Math.abs(openCount -
                             closedCount));

    // Reduce excess open or closed brackets
    // to prevent counting them twice
    if (closedCount > openCount)
        closedUnbalanced -= (closedCount - 
                               openCount);

    if (openCount > closedCount)
        openUnbalanced -= (openCount -
                         closedCount);

    // Update answer by adding minimum of
    // removing both unbalanced open and
    // closed brackets or inserting closed
    // unbalanced brackets to end of String
    result += Math.min(a * (openUnbalanced +
                            closedUnbalanced),
                        b * closedUnbalanced);

    // Print the result
    System.out.print(result + "\n");
}

// Driver Code
public static void main(String[] args)
{
    String str = "))()(()()(";
    int A = 1, B = 3;

    minCost(str, A, B);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the minimum cost
# required to generate a balanced bracket
# sequence
def minCost(str, a, b):

    # Stores the count of
    # unbalanced open brackets
    openUnbalanced = 0;

    # Stores the count of
    # unbalanced closed brackets
    closedUnbalanced = 0;

    # Stores the count of
    # open brackets
    openCount = 0;

    # Stores the count of
    # closed brackets
    closedCount = 0;

    for i in range(len(str)):

        # If open brace is encountered
        if (str[i] == '('):
            openUnbalanced += 1;
            openCount += 1;

        # Otherwise
        else:

            # If no unbalanced open
            # brackets are present
            if (openUnbalanced == 0):

                # Increase count of
                # unbalanced closed brackets
                closedUnbalanced += 1;

            # Otherwise
            else:

                # Reduce count of
                # unbalanced open brackets
                openUnbalanced -= 1;

            # Increase count of
            # closed brackets
            closedCount += 1;

    # Calculate lower bound of minimum cost
    result = a * (abs(openCount - closedCount));

    # Reduce excess open or closed brackets
    # to prevent counting them twice
    if (closedCount > openCount):
        closedUnbalanced -= (closedCount - openCount);

    if (openCount > closedCount):
        openUnbalanced -= (openCount - closedCount);

    # Update answer by adding minimum of
    # removing both unbalanced open and
    # closed brackets or inserting closed
    # unbalanced brackets to end of String
    result += min(a * (openUnbalanced +
                       closedUnbalanced),
                   b * closedUnbalanced);

    # Print the result
    print(result);

# Driver Code
if __name__ == '__main__':
    str = "))()(()()(";
    A = 1; B = 3;

    minCost(str, A, B);

# This code is contributed by Rohit_ranjan
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to calculate the minimum cost
// required to generate a balanced bracket
// sequence
static void minCost(String str, int a, int b)
{

    // Stores the count of
    // unbalanced open brackets
    int openUnbalanced = 0;

    // Stores the count of
    // unbalanced closed brackets
    int closedUnbalanced = 0;

    // Stores the count of
    // open brackets
    int openCount = 0;

    // Stores the count of
    // closed brackets
    int closedCount = 0;

    for(int i = 0; i < str.Length; i++)
    {

        // If open brace is encountered
        if (str[i] == '(')
        {
            openUnbalanced++;
            openCount++;
        }

        // Otherwise
        else
        {

            // If no unbalanced open
            // brackets are present
            if (openUnbalanced == 0)

                // Increase count of
                // unbalanced closed brackets
                closedUnbalanced++;

            // Otherwise
            else

                // Reduce count of
                // unbalanced open brackets
                openUnbalanced--;

            // Increase count of
            // closed brackets
            closedCount++;
        }
    }

    // Calculate lower bound of minimum cost
    int result = a * (Math.Abs(openCount -
                               closedCount));

    // Reduce excess open or closed brackets
    // to prevent counting them twice
    if (closedCount > openCount)
        closedUnbalanced -= (closedCount - 
                             openCount);

    if (openCount > closedCount)
        openUnbalanced -= (openCount -
                           closedCount);

    // Update answer by adding minimum of
    // removing both unbalanced open and
    // closed brackets or inserting closed
    // unbalanced brackets to end of String
    result += Math.Min(a * (openUnbalanced +
                           closedUnbalanced),
                       b * closedUnbalanced);

    // Print the result
    Console.Write(result + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    String str = "))()(()()(";
    int A = 1, B = 3;

    minCost(str, A, B);
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// JavaScript program for the
// above approach

// Function to calculate the minimum cost
// required to generate a balanced bracket
// sequence
function minCost(str, a, b)
{

    // Stores the count of
    // unbalanced open brackets
    let openUnbalanced = 0;

    // Stores the count of
    // unbalanced closed brackets
    let closedUnbalanced = 0;

    // Stores the count of
    // open brackets
    let openCount = 0;

    // Stores the count of
    // closed brackets
    let closedCount = 0;

    for(let i = 0; i < str.length; i++)
    {

        // If open brace is encountered
        if (str[i] == '(')
        {
            openUnbalanced++;
            openCount++;
        }

        // Otherwise
        else
        {

            // If no unbalanced open
            // brackets are present
            if (openUnbalanced == 0)

                // Increase count of
                // unbalanced closed brackets
                closedUnbalanced++;

            // Otherwise
            else

                // Reduce count of
                // unbalanced open brackets
                openUnbalanced--;

            // Increase count of
            // closed brackets
            closedCount++;
        }
    }

    // Calculate lower bound of minimum cost
    let result = a * (Math.abs(openCount -
                             closedCount));

    // Reduce excess open or closed brackets
    // to prevent counting them twice
    if (closedCount > openCount)
        closedUnbalanced -= (closedCount -
                               openCount);

    if (openCount > closedCount)
        openUnbalanced -= (openCount -
                         closedCount);

    // Update answer by adding minimum of
    // removing both unbalanced open and
    // closed brackets or inserting closed
    // unbalanced brackets to end of String
    result += Math.min(a * (openUnbalanced +
                            closedUnbalanced),
                        b * closedUnbalanced);

    // Prlet the result
    document.write(result + "\n");
}

// Driver Code

    let str = "))()(()()(";
    let A = 1, B = 3;

    minCost(str, A, B);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)