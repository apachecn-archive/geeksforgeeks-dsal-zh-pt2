# 以 HH:MM 格式最大化给定时间内的缺失值

> 原文:[https://www . geeksforgeeks . org/最大化 hhmm 格式给定时间的缺失值/](https://www.geeksforgeeks.org/maximize-the-missing-values-in-given-time-in-hhmm-format/)

给定一个以 **24 小时格式****【HH:MM】**表示时间的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，使得一些数字用**“？”**，任务是更换**'？'**用任何可能的数字，使得结果时间是最大可能时间。

**示例:**

> **输入:** S =？4:5?"
> **输出:** 14:59
> **说明:**
> 替换第一个和第二个之后呢'使用数字 1 和 9，将给定时间修改为“14:59”，这是通过替换“？”可以得到的所有可能时间中的最大值。
> 
> **输入:**S =“0？:??"
> **输出:** 09:59

**方法:**给定的问题可以通过[遍历给定的字符串**S**T5】并替换**'？'来解决**字符 **':'** 前的子串位于**【0，23】**范围内， **':'** 后的子串最多必须为 **59** 并打印获得的最大时间。按照以下步骤解决给定的问题:](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)

*   如果索引 **0** 处的字符 **S** 的值是**“？”**索引 **1** 处的字符是**“3”**或**“？”**，然后将 **S[0]** 的值更新为**‘2’**。否则，将 **S[0]** 的值更新为**‘1’**。
*   如果索引 **1** 处的字符 **S** 的值是**“？”**且索引 **0** 处的字符不是**‘2’**，则将 **S[1]** 的值更新为**‘9’**。否则，将 **S[1]** 的值更新为**‘3’**。
*   如果索引 **3** 处的字符 **S** 的值是**“？”**，然后将**S【3】**的值更新为**‘5’**。
*   如果索引 **4** 处的字符 **S** 的值是**“？”**，然后将**S【4】**的值更新为**‘9’**。
*   完成上述步骤后，打印字符串 **S** 的值作为合成时间。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;
// Function to find the maximum time
// by replacing '?' by any digits
void maxTime(string s)
{
    // Convert the string to the
    // character array

    // If the 0th index is '?'
    if (s[0] == '?') {
        if (s[1] <= '3' || s[1] == '?')
            s[0] = '2';
        else
            s[0] = '1';
    }

    // If the 1st index is '?'
    if (s[1] == '?') {
        if (s[0] != '2') {
            s[1] = 9;
        }
        else
            s[1] = 3;
    }

    // If the 3rd index is '?'
    if (s[3] == '?')
        s[3] = '5';

    // If the 4th index is '?'
    if (s[4] == '?')
        s[4] = '9';

    // Return new string
    cout << s << endl;
}

// Driver Code
int main()
{
    string S = "?4:5?";
    maxTime(S);
    return 0;
}
// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class Main {

    // Function to find the maximum time
    // by replacing '?' by any digits
    public static void maxTime(String S)
    {

        // Convert the string to the
        // character array
        char[] s = S.toCharArray();

        // If the 0th index is '?'
        if (s[0] == '?') {
            if (s[1] <= '3' || s[1] == '?')
                s[0] = '2';
            else
                s[0] = '1';
        }

        // If the 1st index is '?'
        if (s[1] == '?') {
            if (s[0] != '2') {
                s[1] = 9;
            }
            else
                s[1] = 3;
        }

        // If the 3rd index is '?'
        if (s[3] == '?')
            s[3] = '5';

        // If the 4th index is '?'
        if (s[4] == '?')
            s[4] = '9';

        // Return new string
        System.out.println(
            new String(s));
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "?4:5?";
        maxTime(S);
    }
}

// This code is contributed by lokeshpotta20.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum time
# by replacing '?' by any digits
def maxTime(s):

    # Convert the string to the
    # character array

    # If the 0th index is '?'
    s = list(s)

    if (s[0] == '?'):
        if (s[1] <= '3' or s[1] == '?'):
            s[0] = '2'
        else:
            s[0] = '1'

    # If the 1st index is '?'
    if (s[1] == '?'):
        if (s[0] != '2'):
            s[1] = 9
        else:
            s[1] = 3

    # If the 3rd index is '?'
    if (s[3] == '?'):
        s[3] = '5'

    # If the 4th index is '?'
    if (s[4] == '?'):
        s[4] = '9'

    # Return new string
    print("".join(s))

# Driver Code
S = "?4:5?"
maxTime(S)

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class gfg {

    // Function to find the maximum time
    // by replacing '?' by any digits
    public static void maxTime(String S)
    {

        // Convert the string to the
        // character array
        char[] s = S.ToCharArray();

        // If the 0th index is '?'
        if (s[0] == '?') {
            if (s[1] <= '3' || s[1] == '?')
                s[0] = '2';
            else
                s[0] = '1';
        }

        // If the 1st index is '?'
        if (s[1] == '?') {
            if (s[0] != '2') {
                s[1] = '9';
            }
            else
                s[1] = '3';
        }

        // If the 3rd index is '?'
        if (s[3] == '?')
            s[3] = '5';

        // If the 4th index is '?'
        if (s[4] == '?')
            s[4] = '9';

        // Return new string
        Console.Write(new String(s));
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String S = "?4:5?";
        maxTime(S);
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum time
// by replacing '?' by any digits
function maxTime(s)
{

    // Convert the string to the
    // character array

    // If the 0th index is '?'
    s = s.split("")
    if (s[0] == '?') {
        if (s[1] <= '3' || s[1] == '?')
            s[0] = '2';
        else
            s[0] = '1';
    }

    // If the 1st index is '?'
    if (s[1] == '?') {
        if (s[0] != '2') {
            s[1] = 9;
        }
        else
            s[1] = 3;
    }

    // If the 3rd index is '?'
    if (s[3] == '?')
        s[3] = '5';

    // If the 4th index is '?'
    if (s[4] == '?')
        s[4] = '9';

    // Return new string
    document.write(s.join(""));
}

// Driver Code
let S = "?4:5?";
maxTime(S);

// This code is contributed by gfgking
</script>
```

**Output:** 

```
14:59
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)