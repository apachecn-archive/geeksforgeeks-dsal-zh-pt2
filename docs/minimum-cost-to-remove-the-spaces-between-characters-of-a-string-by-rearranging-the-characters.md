# 通过重新排列字符来删除字符串字符之间的空格的最小成本

> 原文:[https://www . geeksforgeeks . org/通过重新排列字符来删除字符串字符之间的空格的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-remove-the-spaces-between-characters-of-a-string-by-rearranging-the-characters/)

给定一个由字符和空格组成的字符串 **str** ，任务是找到最小的代价来减少字符串字符之间的空格数。

> 将索引 **i** 的字符移动到索引 **j** 的成本定义为:**| I–j |**

**示例:**

> **输入:**str = " @ { content } # x201；
> **输出:** 4
> **解释:**
> 由于字符位于索引[2，7](只有两个)，要么将第一个字符移动到最近的第二个字符，要么相反。所需成本为|2-6| = 4 或|6-2| = 4。
> 因此，最低成本为 4。
> 
> **输入:** str = " A "
> **输出:** 0
> **解释:**
> 由于字符串只有一个字符，所以不需要修改。因此，最小成本为 0。

**方法:**思路是将所有字符移动到最靠近字符串中间的位置，这样整体代价最小。以下是步骤:

1.  用 0 初始化总成本。
2.  横向移动字符串，计算两个字符之间的间距。
3.  将两个角色放在一起，并将成本加到总成本中。
4.  对所有字符重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ program to gather characters
// of a string in minimum cost
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the
// minimum cost
int min_cost(string S)
{

    // Stores the minimum cost
    int cost = 0;

    // Stores the count of
    // characters found
    int F = 0;

    // Stores the count of
    // blank spaces found
    int B = 0;

    int count = 0;

    for(char c : S)
        if(c == ' ')
           count++;

    // Stores the count of
    // total characters
    int n = S.size() - count;

    // If the count of characters
    // is equal to 1
    if (n == 1)
        return cost;

    // Iterate over the string
    for(char in : S)
    {

        // Consider the previous character
        // together with current character
        if (in != ' ')
        {
            // If not together already
            if (B != 0)
            {

                // Add the cost to group
                // them together
                cost += min(n - F, F) * B;
                B = 0;
            }

            // Increase count of
            // characters found
            F += 1;
        }

        // Otherwise
        else
        {

            // Increase count of
            // spaces found
            B += 1;
        }
    }

    // Return the total
    // cost obtained
    return cost;
}

// Driver Code
int main ()
{
    string S = " @    {content}quot;;

    cout << min_cost(S);
    return 0;
}

// This code is contributed by Amit Katiyar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to gather characters
// of a string in minimum cost
import java.util.*;
import java.lang.*;

class GFG{

// Function to calculate the
// minimum cost
static int min_cost(String S)
{

    // Stores the minimum cost
    int cost = 0;

    // Stores the count of
    // characters found
    int F = 0;

    // Stores the count of
    // blank spaces found
    int B = 0;

    int count = 0;

    for(char c : S.toCharArray())
        if(c == ' ')
           count++;

    // Stores the count of
    // total characters
    int n = S.length() - count;

    // If the count of characters
    // is equal to 1
    if (n == 1)
        return cost;

    // Iterate over the string
    for(char in : S.toCharArray())
    {

        // Consider the previous character
        // together with current character
        if (in != ' ')
        {
            // If not together already
            if (B != 0)
            {

                // Add the cost to group
                // them together
                cost += Math.min(n - F, F) * B;
                B = 0;
            }

            // Increase count of
            // characters found
            F += 1;
        }

        // Otherwise
        else
        {

            // Increase count of
            // spaces found
            B += 1;
        }
    }

    // Return the total
    // cost obtained
    return cost;
}

// Driver Code
public static void main (String[] args)
{
    String S = " @    {content}quot;;

    System.out.println(min_cost(S));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to gather characters
# of a string in minimum cost

# Function to calculate the
# minimum cost
def min_cost(S):

    # Stores the minimum cost
    cost = 0

    # Stores the count of
    # characters found
    F = 0

    # Stores the count of
    # blank spaces found
    B = 0

    # Stores the count of
    # total characters
    n = len(S)-S.count(' ')

    # If the count of characters
    # is equal to 1
    if n == 1:
        return cost

    # Iterate over the string
    for char in S:

        # Consider the previous character
        # together with current character
        if char != ' ':

            # If not together already
            if B != 0:

                # Add the cost to group
                # them together
                cost += min(n - F, F) * B
                B = 0

            # Increase count of
            # characters found
            F += 1

        # Otherwise
        else:

            # Increase count of
            # spaces found
            B += 1

    # Return the total
    # cost obtained
    return cost

# Driver Code
S = " @    {content}quot;
print(min_cost(S))
```

## C#

```
// C# program to gather characters
// of a string in minimum cost
using System;

class GFG{

// Function to calculate the
// minimum cost
static int min_cost(String S)
{

    // Stores the minimum cost
    int cost = 0;

    // Stores the count of
    // characters found
    int F = 0;

    // Stores the count of
    // blank spaces found
    int B = 0;

    int count = 0;

    foreach(char c in S.ToCharArray())
        if(c == ' ')
           count++;

    // Stores the count of
    // total characters
    int n = S.Length - count;

    // If the count of characters
    // is equal to 1
    if (n == 1)
        return cost;

    // Iterate over the string
    foreach(char inn in S.ToCharArray())
    {

        // Consider the previous character
        // together with current character
        if (inn != ' ')
        {

            // If not together already
            if (B != 0)
            {

                // Add the cost to group
                // them together
                cost += Math.Min(n - F, F) * B;
                B = 0;
            }

            // Increase count of
            // characters found
            F += 1;
        }

        // Otherwise
        else
        {

            // Increase count of
            // spaces found
            B += 1;
        }
    }

    // Return the total
    // cost obtained
    return cost;
}

// Driver Code
public static void Main(String[] args)
{
    String S = " @    {content}quot;;

    Console.WriteLine(min_cost(S));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to gather characters
// of a string in minimum cost

// Function to calculate the
// minimum cost
function min_cost(S)
{

    // Stores the minimum cost
    let cost = 0;

    // Stores the count of
    // characters found
    let F = 0;

    // Stores the count of
    // blank spaces found
    let B = 0;

    let count = 0;

    for(let i in S)
        if(S[i] == ' ')
           count++;

    // Stores the count of
    // total characters
    let n = S.length - count;

    // If the count of characters
    // is equal to 1
    if (n == 1)
        return cost;

    // Iterate over the string
    for(let i in S)
    {

        // Consider the previous character
        // together with current character
        if (S[i] != ' ')
        {
            // If not together already
            if (B != 0)
            {

                // Add the cost to group
                // them together
                cost += Math.min(n - F, F) * B;
                B = 0;
            }

            // Increase count of
            // characters found
            F += 1;
        }

        // Otherwise
        else
        {

            // Increase count of
            // spaces found
            B += 1;
        }
    }

    // Return the total
    // cost obtained
    return cost;
}

// Driver Code

     let S = " @    {content}quot;;

    document.write(min_cost(S.split('')));

</script>
```

**输出:**

```
4
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*