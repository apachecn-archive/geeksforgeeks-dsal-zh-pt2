# 通过在给定的 24 小时格式时间中替换“_”来最大化时间

> 原文:[https://www . geeksforgeeks . org/通过在给定的 24 小时格式中替换-时间来最大化时间/](https://www.geeksforgeeks.org/maximize-time-by-replacing-_-in-a-given-24-hour-format-time/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** 表示 [24 小时格式](https://en.wikipedia.org/wiki/24-hour_clock)中的时间，其中**“_”**位于某些数字的位置，任务是通过用任何数字替换字符**“_”**来找到可能的最大时间。

**示例:**

> **输入:**S =“0 _:4 _”
> T3】输出: 09:39
> **说明:**将字符 S[1]和 S[4]替换为‘9’将字符串修改为“09:49”，这是可能的最大时间。
> 
> **输入:**S =“_ _:_ _”
> T3】输出: 23:59

**方法:**给定的问题可以通过[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)为字符串中出现的每个 **'_'** 选择数字来解决。按照以下步骤解决问题:

*   如果字符 **S[0]** 等于 **'_'** ， **S[1]** 或者是 **'_'** 或者是小于 **4** ，那么将“ **2** ”赋给 **S[0]** 。否则，将**‘1’**分配给**S【0】**。
*   如果字符 **S[1]** 等于 **'_'** ， **S[0]** 为 **'2 '，**则将 **'3'** 分配给 **S[1]** 。否则，将“ **9** ”分配给**S【1】**。
*   如果字符 **S[3]** 等于 **'_'** ，则将 **'5'** 分配给 **S[3]** 。
*   如果字符 **S[4]** 等于**“_”**，那么将“ **9** ”分配给 **S[4]** 。
*   完成上述步骤后，打印修改后的字符串 **S** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// time possible by replacing
// each '_' with any digit
string maximumTime(string s)
{
    // If the first character is '_'
    if (s[0] == '_') {

        // If s[1] is '_' or
        // s[1] is less than 4
        if ((s[1] == '_')
            || (s[1] >= '0'
                && s[1] < '4')) {

            // Update s[0] as 2
            s[0] = '2';
        }

        // Otherwise, update s[0] = 1
        else {
            s[0] = '1';
        }
    }

    // If s[1] is equal to '_'
    if (s[1] == '_') {

        // If s[0] is equal to '2'
        if (s[0] == '2') {
            s[1] = '3';
        }

        // Otherwise
        else {
            s[1] = '9';
        }
    }

    // If S[3] is equal to '_'
    if (s[3] == '_') {
        s[3] = '5';
    }

    // If s[4] is equal to '_'
    if (s[4] == '_') {
        s[4] = '9';
    }

    // Return the modified string
    return s;
}

// Driver Code
int main()
{
    string S = "0_:4_";
    cout << maximumTime(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the maximum
// time possible by replacing
// each '_' with any digit
static void maximumTime(String str)
{
    char []s = str.toCharArray();

    // If the first character is '_'
    if (s[0] == '_')
    {

        // If s[1] is '_' or
        // s[1] is less than 4
        if ((s[1] == '_') ||
            (s[1] >= '0' && s[1] < '4'))
        {

            // Update s[0] as 2
            s[0] = '2';
        }

        // Otherwise, update s[0] = 1
        else
        {
            s[0] = '1';
        }
    }

    // If s[1] is equal to '_'
    if (s[1] == '_')
    {

        // If s[0] is equal to '2'
        if (s[0] == '2')
        {
            s[1] = '3';
        }

        // Otherwise
        else
        {
            s[1] = '9';
        }
    }

    // If S[3] is equal to '_'
    if (s[3] == '_')
    {
        s[3] = '5';
    }

    // If s[4] is equal to '_'
    if (s[4] == '_')
    {
        s[4] = '9';
    }

    // Print the modified string
    for(int i = 0; i < s.length; i++)
        System.out.print(s[i]);
}

// Driver Code
static public void main (String []args)
{
    String S = "0_:4_";

    maximumTime(S);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum
# time possible by replacing
# each '_' with any digit
def maximumTime(s):

    s = list(s)
    # If the first character is '_'
    if (s[0] == '_'):

        # If s[1] is '_' or
        # s[1] is less than 4
        if ((s[1] == '_') or (s[1] >= '0' and
                              s[1] < '4')):

            # Update s[0] as 2
            s[0] = '2'

        # Otherwise, update s[0] = 1
        else:
            s[0] = '1'

    # If s[1] is equal to '_'
    if (s[1] == '_'):

        # If s[0] is equal to '2'
        if (s[0] == '2'):
            s[1] = '3'

        # Otherwise
        else:
            s[1] = '9'

    # If S[3] is equal to '_'
    if (s[3] == '_'):
        s[3] = '5'

    # If s[4] is equal to '_'
    if (s[4] == '_'):
        s[4] = '9'

    # Return the modified string
    s = ''.join(s)
    return s

# Driver Code
if __name__ == '__main__':

    S = "0_:4_"

    print(maximumTime(S))

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum
// time possible by replacing
// each '_' with any digit
static void maximumTime(string str)
{
    char []s = str.ToCharArray();

    // If the first character is '_'
    if (s[0] == '_')
    {

        // If s[1] is '_' or
        // s[1] is less than 4
        if ((s[1] == '_') ||
            (s[1] >= '0' && s[1] < '4'))
        {

            // Update s[0] as 2
            s[0] = '2';
        }

        // Otherwise, update s[0] = 1
        else
        {
            s[0] = '1';
        }
    }

    // If s[1] is equal to '_'
    if (s[1] == '_')
    {

        // If s[0] is equal to '2'
        if (s[0] == '2')
        {
            s[1] = '3';
        }

        // Otherwise
        else
        {
            s[1] = '9';
        }
    }

    // If S[3] is equal to '_'
    if (s[3] == '_')
    {
        s[3] = '5';
    }

    // If s[4] is equal to '_'
    if (s[4] == '_')
    {
        s[4] = '9';
    }

    // Print the modified string
    for(int i = 0; i < s.Length; i++)
        Console.Write(s[i]);
}

// Driver Code
static public void Main ()
{
    string S = "0_:4_";

    maximumTime(S);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// javascript program for the above approach

// Function to find the maximum
// time possible by replacing
// each '_' with any digit

     function maximumTime(str)
{
     var s = str.split("");

    // If the first character is '_'
    if (s[0] == '_')
    {

        // If s[1] is '_' or
        // s[1] is less than 4
        if ((s[1] == '_') ||
            (s[1] >= '0' && s[1] < '4'))
        {

            // Update s[0] as 2
            s[0] = '2';
        }

        // Otherwise, update s[0] = 1
        else
        {
            s[0] = '1';
        }
    }

    // If s[1] is equal to '_'
    if (s[1] == '_')
    {

        // If s[0] is equal to '2'
        if (s[0] == '2')
        {
            s[1] = '3';
        }

        // Otherwise
        else
        {
            s[1] = '9';
        }
    }

    // If S[3] is equal to '_'
    if (s[3] == '_')
    {
        s[3] = '5';
    }

    // If s[4] is equal to '_'
    if (s[4] == '_')
    {
        s[4] = '9';
    }

    // Print the modified string
    for(var i = 0; i < s.length; i++)
        document.write(s[i]);
}

// Driver Code
    var S = "0_:4_";   
    maximumTime(S);

// This code is contributed by bunnyram19.
</script>
```

**Output:** 

```
09:49
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)