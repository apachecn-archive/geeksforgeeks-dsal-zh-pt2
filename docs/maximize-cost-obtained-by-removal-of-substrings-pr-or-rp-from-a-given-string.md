# 通过从给定字符串中移除子字符串“pr”或“rp”来最大化成本

> 原文:[https://www . geesforgeks . org/maximum-通过从给定字符串中移除子字符串获得的成本-pr-or-RP/](https://www.geeksforgeeks.org/maximize-cost-obtained-by-removal-of-substrings-pr-or-rp-from-a-given-string/)

给定一个字符串 **str** 和两个整数 **X** 和 **Y** ，任务是找到从给定字符串中移除所有子字符串“pr”和“rp”所需的最大成本，其中移除子字符串“rp”和“pr”分别需要 **X** 和 **Y** 。

**示例:**

> **输入:**str = " abppprr "，X = 5，Y = 4
> **输出:** 15
> **解释:**
> 执行以下操作:
> 【abpp】**pr**RR->【abpprr】，成本= 5
> ABP**pr**r->【abpr】，成本= 10
> ab**pr【T11**
> 
> **输入:**str = " prpr RP "，X = 7，Y = 10
> T3】输出: 37

**进场**:问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。这里的想法是如果 **X** 大于 **Y** 则移除**“pr”**，否则移除**“RP”**。按照以下步骤解决问题。

1.  **如果 X < Y:** 交换给定字符串中的 **X** 和 **Y** 的值，并将字符**‘p’**替换为**‘r’**，反之亦然。
2.  初始化两个变量 **countP** 和**count**分别存储字符串中**【p】**和**【r】**的计数。
3.  迭代数组 **arr[]** 并执行以下步骤:
    *   **如果 str[i] = 'p':** 将**计数**增加 1。
    *   **如果 str[i] = 'r':** 检查**计数**的值。如果**计数> 0** ，则将结果增加 **X** ，将**计数**的值减少 1。否则，将**count**的值增加 1。
    *   **If str[i]！= 'p '和 str[i]！='r':** 将结果增加**分钟(计数，国家)* Y** 。
4.  将结果增加**分钟(countP，count)* Y**。
5.  最后，删除所有需要的子字符串后，打印得到的结果。

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to maintain the case, X>=Y
bool swapXandY(string& str, int X, int Y)
{

    int N = str.length();

    // To maintain X>=Y
    swap(X, Y);

    for (int i = 0; i < N; i++) {

        // Replace 'p' to 'r'
        if (str[i] == 'p') {
            str[i] = 'r';
        }

        // Replace 'r' to 'p'.
        else if (str[i] == 'r') {
            str[i] = 'p';
        }
    }
}

// Function to return the maximum cost
int maxCost(string str, int X, int Y)
{
    // Stores the length of the string
    int N = str.length();

    // To maintain X>=Y.
    if (Y > X) {
        swapXandY(str, X, Y);
    }

    // Stores the maximum cost
    int res = 0;

    // Stores the count of 'p'
    // after removal of all "pr"
    // substrings up to str[i]
    int countP = 0;

    // Stores the count of 'r'
    // after removal of all "pr"
    // substrings up to str[i]
    int countR = 0;

    // Stack to maintain the order of
    // characters after removal of
    // substrings
    for (int i = 0; i < N; i++) {

        if (str[i] == 'p') {
            countP++;
        }
        else if (str[i] == 'r') {

            // If substring "pr"
            // is removed
            if (countP > 0) {
                countP--;

                // Increase cost by X
                res += X;
            }
            else
                countR++;
        }
        else {

            // If any substring "rp"
            // left in the Stack
            res += min(countP, countR) * Y;
            countP = 0;
            countR = 0;
        }
    }

    // If any substring "rp"
    // left in the Stack
    res += min(countP, countR) * Y;
    return res;
}

// Driver Code
int main()
{
    string str = "abppprrr";
    int X = 5, Y = 4;
    cout << maxCost(str, X, Y);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to maintain the case, X>=Y
static boolean swapXandY(char []str, int X, int Y)
{
    int N = str.length;

    // To maintain X>=Y
    X = X + Y;
    Y = X - Y;
    X = X - Y;

    for(int i = 0; i < N; i++)
    {

        // Replace 'p' to 'r'
        if (str[i] == 'p')
        {
            str[i] = 'r';
        }

        // Replace 'r' to 'p'.
        else if (str[i] == 'r')
        {
            str[i] = 'p';
        }
    }
    return true;
}

// Function to return the maximum cost
static int maxCost(String str, int X, int Y)
{

    // Stores the length of the String
    int N = str.length();

    // To maintain X>=Y.
    if (Y > X)
    {
        swapXandY(str.toCharArray(), X, Y);
    }

    // Stores the maximum cost
    int res = 0;

    // Stores the count of 'p'
    // after removal of all "pr"
    // subStrings up to str[i]
    int countP = 0;

    // Stores the count of 'r'
    // after removal of all "pr"
    // subStrings up to str[i]
    int countR = 0;

    // Stack to maintain the order of
    // characters after removal of
    // subStrings
    for(int i = 0; i < N; i++)
    {
        if (str.charAt(i) == 'p')
        {
            countP++;
        }
        else if (str.charAt(i) == 'r')
        {

            // If subString "pr"
            // is removed
            if (countP > 0)
            {
                countP--;

                // Increase cost by X
                res += X;
            }
            else
                countR++;
        }
        else
        {

            // If any subString "rp"
            // left in the Stack
            res += Math.min(countP, countR) * Y;
            countP = 0;
            countR = 0;
        }
    }

    // If any subString "rp"
    // left in the Stack
    res += Math.min(countP, countR) * Y;
    return res;
}

// Driver Code
public static void main(String[] args)
{
    String str = "abppprrr";
    int X = 5, Y = 4;

    System.out.print(maxCost(str, X, Y));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to maintain the case, X>=Y
def swapXandY(str, X, Y):

    N = len(str)

    # To maintain X>=Y
    X, Y = Y, X

    for i in range(N):

        # Replace 'p' to 'r'
        if(str[i] == 'p'):
            str[i] = 'r'

        # Replace 'r' to 'p'.
        elif(str[i] == 'r'):
            str[i] = 'p'

# Function to return the maximum cost
def maxCost(str, X, Y):

    # Stores the length of the string
    N = len(str)

    # To maintain X>=Y.
    if(Y > X):
        swapXandY(str, X, Y)

    # Stores the maximum cost
    res = 0

    # Stores the count of 'p'
    # after removal of all "pr"
    # substrings up to str[i]
    countP = 0

    # Stores the count of 'r'
    # after removal of all "pr"
    # substrings up to str[i]
    countR = 0

    # Stack to maintain the order of
    # characters after removal of
    # substrings
    for i in range(N):
        if(str[i] == 'p'):
            countP += 1

        elif(str[i] == 'r'):

            # If substring "pr"
            # is removed
            if(countP > 0):
                countP -= 1

                # Increase cost by X
                res += X

            else:
                countR += 1

        else:

            # If any substring "rp"
            # left in the Stack
            res += min(countP, countR) * Y
            countP = 0
            countR = 0

    # If any substring "rp"
    # left in the Stack
    res += min(countP, countR) * Y

    return res

# Driver Code
str = "abppprrr"
X = 5
Y = 4

# Function call
print(maxCost(str, X, Y))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to maintain the case, X>=Y
static bool swapXandY(char []str,
                      int X, int Y)
{
    int N = str.Length;

    // To maintain X>=Y
    X = X + Y;
    Y = X - Y;
    X = X - Y;

    for(int i = 0; i < N; i++)
    {
        // Replace 'p' to 'r'
        if (str[i] == 'p')
        {
            str[i] = 'r';
        }

        // Replace 'r' to 'p'.
        else if (str[i] == 'r')
        {
            str[i] = 'p';
        }
    }
    return true;
}

// Function to return the
// maximum cost
static int maxCost(String str,
                   int X, int Y)
{   
    // Stores the length of the String
    int N = str.Length;

    // To maintain X>=Y.
    if (Y > X)
    {
        swapXandY(str.ToCharArray(),
                  X, Y);
    }

    // Stores the maximum cost
    int res = 0;

    // Stores the count of 'p'
    // after removal of all "pr"
    // subStrings up to str[i]
    int countP = 0;

    // Stores the count of 'r'
    // after removal of all "pr"
    // subStrings up to str[i]
    int countR = 0;

    // Stack to maintain the order of
    // characters after removal of
    // subStrings
    for(int i = 0; i < N; i++)
    {
        if (str[i] == 'p')
        {
            countP++;
        }
        else if (str[i] == 'r')
        {           
            // If subString "pr"
            // is removed
            if (countP > 0)
            {
                countP--;

                // Increase cost by X
                res += X;
            }
            else
                countR++;
        }
        else
        {
            // If any subString "rp"
            // left in the Stack
            res += Math.Min(countP,
                            countR) * Y;
            countP = 0;
            countR = 0;
        }
    }

    // If any subString "rp"
    // left in the Stack
    res += Math.Min(countP,
                    countR) * Y;
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "abppprrr";
    int X = 5, Y = 4;   
    Console.Write(maxCost(str, X, Y));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to maintain the case, X>=Y
function swapXandY(str, X, Y)
{
    let N = str.length;

    // To maintain X>=Y
    X = X + Y;
    Y = X - Y;
    X = X - Y;

    for(let i = 0; i < N; i++)
    {

        // Replace 'p' to 'r'
        if (str[i] == 'p')
        {
            str[i] = 'r';
        }

        // Replace 'r' to 'p'.
        else if (str[i] == 'r')
        {
            str[i] = 'p';
        }
    }
    return true;
}

// Function to return the maximum cost
function maxCost(str, X, Y)
{

    // Stores the length of the String
    let N = str.length;

    // To maintain X>=Y.
    if (Y > X)
    {
        swapXandY(str.split(''), X, Y);
    }

    // Stores the maximum cost
    let res = 0;

    // Stores the count of 'p'
    // after removal of all "pr"
    // subStrings up to str[i]
    let countP = 0;

    // Stores the count of 'r'
    // after removal of all "pr"
    // subStrings up to str[i]
    let countR = 0;

    // Stack to maintain the order of
    // characters after removal of
    // subStrings
    for(let i = 0; i < N; i++)
    {
        if (str[i] == 'p')
        {
            countP++;
        }
        else if (str[i] == 'r')
        {

            // If subString "pr"
            // is removed
            if (countP > 0)
            {
                countP--;

                // Increase cost by X
                res += X;
            }
            else
                countR++;
        }
        else
        {

            // If any subString "rp"
            // left in the Stack
            res += Math.min(countP, countR) * Y;
            countP = 0;
            countR = 0;
        }
    }

    // If any subString "rp"
    // left in the Stack
    res += Math.min(countP, countR) * Y;
    return res;
}

// Driver Code

    let str = "abppprrr";
    let X = 5, Y = 4;

    document.write(maxCost(str, X, Y));

// This code is contributed by target_2.
</script>
```

**Output:** 

```
15
```

***时间复杂度:** O(N)，其中 N 表示弦的长度*
***辅助空间:** O(1)*