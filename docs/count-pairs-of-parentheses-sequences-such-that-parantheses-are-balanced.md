# 计数成对的括号序列，使括号平衡

> 原文:[https://www . geeksforgeeks . org/count-对括号-序列-这样-参数-是平衡的/](https://www.geeksforgeeks.org/count-pairs-of-parentheses-sequences-such-that-parantheses-are-balanced/)

给定 N 个括号序列，任务是通过连接找到成对的[括号序列](https://www.geeksforgeeks.org/check-balanced-parentheses-expression-o1-space/)的数量，这可以作为一个整体获得一个平衡的括号序列。括号序列只能是一对中的一部分。

**示例:**

```
Input: { ")())", ")", "((", "((", "(", ")", ")"}
Output:  2 
Bracket sequence {1, 3} and {5, 6} 

Input: {"()", "(())", "(())", "()"}
Output: 2 
Since all brackets are balanced, hence we can form 2 pairs with 4\. 
```

**方法:**可以按照以下步骤解决上述问题:

*   计算个人所需的左括号和右括号。
*   如果所需的结束括号> 0，并且开始括号为 0，则散列括号所需的结束数字。
*   类似地，如果要求左括号> 0，右括号为 0，则散列括号的所需左括号号。
*   计算平衡括号序列。
*   将(平衡括号序列数/2)加到对数上。
*   对于每个需要相同数量的左括号的序列，min(hash[open]，hash[close])将被添加到对的数量中

以下是上述方法的实现:

## C++

```
// C++ program to count the number of pairs
// of balanced parentheses
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of pairs
int countPairs(string bracks[], int num)
{

    // Hashing function to count the
    // opening and closing brackets
    unordered_map<int, int> open, close;

    int cnt = 0;

    // Traverse for all bracket sequences
    for (int i = 0; i < num; i++) {

        // Get the string
        string s = bracks[i];

        int l = s.length();

        // Counts the opening and closing required
        int op = 0, cl = 0;

        // Traverse in the string
        for (int j = 0; j < l; j++) {

            // If it is a opening bracket
            if (s[j] == '(')
                op++;
            else // Closing bracket
            {

                // If openings are there, then close it
                if (op)
                    op--;
                else // Else increase count of closing
                    cl++;
            }
        }

        // If requirements of openings
        // are there and no closing
        if (op && !cl)
            open[op]++;

        // If requirements of closing
        // are there and no opening
        if (cl && !op)
            close[cl]++;

        // Perfect
        if (!op && !cl)
            cnt++;
    }

    // Divide by two since two
    // perfect makes one pair
    cnt = cnt / 2;

    // Traverse in the open and find
    // corresponding minimum
    for (auto it : open)
        cnt += min(it.second, close[it.first]);

    return cnt;
}

// Driver Code
int main()
{
    string bracks[] = { ")())", ")", "((", "((", "(", ")", ")" };
    int num = sizeof(bracks) / sizeof(bracks[0]);

    cout << countPairs(bracks, num);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of pairs
// of balanced parentheses
import java.util.HashMap;

class GFG
{

// Function to count the number of pairs
static int countPairs(String[] bracks, int num)
{

    // Hashing function to count the
    // opening and closing brackets
    HashMap<Integer, Integer> open = new HashMap<>();
    HashMap<Integer, Integer> close = new HashMap<>();

    int cnt = 0;

    // Traverse for all bracket sequences
    for (int i = 0; i < num; i++)
    {

        // Get the string
        String s = bracks[i];
        int l = s.length();

        // Counts the opening and closing required
        int op = 0, cl = 0;

        // Traverse in the string
        for (int j = 0; j < l; j++)
        {

            // If it is a opening bracket
            if (s.charAt(j) == '(')
                op++;

            // Closing bracket
            else
            {

                // If openings are there, then close it
                if (op != 0)
                    op--;

                // Else increase count of closing
                else
                    cl++;
            }
        }

        // If requirements of openings
        // are there and no closing
        if (op != 0 && cl == 0)
            open.put(op, open.get(op) == null ?
                     1 : open.get(op) + 1);

        // If requirements of closing
        // are there and no opening
        if (cl != 0 && op == 0)
            close.put(cl, close.get(cl) == null ?
                      1 : close.get(cl) + 1);

        // Perfect
        if (op == 0 && cl == 0)
            cnt++;
    }

    // Divide by two since two
    // perfect makes one pair
    cnt /= 2;

    // Traverse in the open and find
    // corresponding minimum
    for (HashMap.Entry<Integer,
                       Integer> it : open.entrySet())
        cnt += Math.min(it.getValue(),
              close.get(it.getKey()));

    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    String[] bracks = { ")())", ")", "((",
                        "((", "(", ")", ")" };
    int num = bracks.length;

    System.out.println(countPairs(bracks, num));
}
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to count the number of pairs
# of balanced parentheses
import math as mt

# Function to count the number of pairs
def countPairs(bracks, num):

    # Hashing function to count the
    # opening and closing brackets
    openn=dict()
    close=dict()

    cnt = 0

    # Traverse for all bracket sequences
    for i in range(num):

        # Get the string
        s = bracks[i]

        l = len(s)

        # Counts the opening and closing required
        op,cl = 0,0

        # Traverse in the string
        for j in range(l):
            # If it is a opening bracket
            if (s[j] == '('):
                op+=1
            else: # Closing bracket

                # If openings are there, then close it
                if (op):
                    op-=1
                else: # Else increase count of closing
                    cl+=1

        # If requirements of openings
        # are there and no closing
        if (op and cl==0):
            if op in openn.keys():
                openn[op]+=1
            else:
                openn[op]=1

        # If requirements of closing
        # are there and no opening
        if (cl and op==0):
            if cl in openn.keys():
                close[cl]+=1
            else:
                close[cl]=1

        # Perfect
        if (op==0 and cl==0):
            cnt+=1

    # Divide by two since two
    # perfect makes one pair
    cnt = cnt //2

    # Traverse in the open and find
    # corresponding minimum
    for it in openn:
        cnt += min(openn[it], close[it])

    return cnt

# Driver Code
bracks= [")())", ")", "((", "((", "(", ")", ")" ]
num = len(bracks)

print(countPairs(bracks, num))

#This code is contributed by Mohit kumar 29
```

## C#

```
// C# program to count the number of pairs
// of balanced parentheses
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of pairs
static int countPairs(string[] bracks, int num)
{

    // Hashing function to count the
    // opening and closing brackets
    Dictionary<int,
               int> open = new Dictionary<int,
                                          int>();
    Dictionary<int,
               int> close = new Dictionary<int,
                                           int>();

    int cnt = 0;

    // Traverse for all bracket sequences
    for(int i = 0; i < num; i++)
    {

        // Get the string
        string s = bracks[i];
        int l = s.Length;

        // Counts the opening and closing required
        int op = 0, cl = 0;

        // Traverse in the string
        for(int j = 0; j < l; j++)
        {

            // If it is a opening bracket
            if (s[j] == '(')
                op++;

            // Closing bracket
            else
            {

                // If openings are there, then close it
                if (op != 0)
                    op--;

                // Else increase count of closing
                else
                    cl++;
            }
        }

        // If requirements of openings
        // are there and no closing
        if (op != 0 && cl == 0)
        {
            if (open.ContainsKey(op))
            {
                open[op]++;
            }
            else
            {
                open[op] = 1;
            }
        }

        // If requirements of closing
        // are there and no opening
        if (cl != 0 && op == 0)
        {
            if (close.ContainsKey(cl))
            {
                close[cl]++;
            }
            else
            {
                close[cl] = 1;
            }
        }

        // Perfect
        if (op == 0 && cl == 0)
            cnt++;
    }

    // Divide by two since two
    // perfect makes one pair
    cnt /= 2;

    // Traverse in the open and find
    // corresponding minimum
    foreach(KeyValuePair<int, int> it in open)
    {
        cnt += Math.Min(it.Value, close[it.Value]);
    }
    return cnt;
}

// Driver Code
public static void Main(string[] args)
{
    string[] bracks = { ")())", ")", "((",
                        "((", "(", ")", ")" };

    int num = bracks.Length;

    Console.Write(countPairs(bracks, num));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript program to count the number of pairs
// of balanced parentheses

// Function to count the number of pairs
function countPairs( bracks,num)
{

    // Hashing function to count the
    // opening and closing brackets
    let open = new Map();
    let close = new Map();
    let cnt = 0;

    // Traverse for all bracket sequences
    for (let i = 0; i < num; i++)
    {

        // Get the string
        let s = bracks[i];
        let l = s.length;

        // Counts the opening and closing required
        let op = 0, cl = 0;

        // Traverse in the string
        for (let j = 0; j < l; j++)
        {

            // If it is a opening bracket
            if (s[j] == '(')
                op++;

            // Closing bracket
            else
            {

                // If openings are there, then close it
                if (op != 0)
                    op--;

                // Else increase count of closing
                else
                    cl++;
            }
        }

        // If requirements of openings
        // are there and no closing
        if (op != 0 && cl == 0)
            open.set(op, open.get(op) == null ?
                     1 : open.get(op) + 1);

        // If requirements of closing
        // are there and no opening
        if (cl != 0 && op == 0)
            close.set(cl, close.get(cl) == null ?
                      1 : close.get(cl) + 1);

        // Perfect
        if (op == 0 && cl == 0)
            cnt++;
    }

    // Divide by two since two
    // perfect makes one pair
    cnt /= 2;

    // Traverse in the open and find
    // corresponding minimum
    for (let [key, value] of open.entries())
        cnt += Math.min(value,
              close.get(value));

    return cnt;
}

// Driver Code
let bracks=[")())", ")", "((",
                        "((", "(", ")", ")"];

let num = bracks.length;
document.write(countPairs(bracks, num));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2
```