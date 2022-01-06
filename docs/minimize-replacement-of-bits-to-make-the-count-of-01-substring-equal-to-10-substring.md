# 尽量减少位的替换，使 01 子串的计数等于 10 子串

> 原文:[https://www . geeksforgeeks . org/最小化-替换位-使 01 子串计数等于 10 子串/](https://www.geeksforgeeks.org/minimize-replacement-of-bits-to-make-the-count-of-01-substring-equal-to-10-substring/)

给定一个二进制字符串 **str** 。任务是将**“0”替换为“1”**或**“1”替换为“0”**的次数降至最低，以平衡二进制字符串。一个二进制字符串被说成是平衡的: ***“如果数“01”的子串=数“10”的子串”。***

***例:***

> **输入:** str = "101010"
> **输出:** 1
> **解释:**“01”= 2&“10”= 3。所以把最后一个字符改为“1”。修改后的字符串将是“101011”或“001010”。
> 
> **输入:** str = "0000100" // **平衡**、【01】= 1&【10】= 1
> T5】输出:0
> T8】说明:弦已经平衡了。

**方法:**可以注意到 ***“平衡的二进制字符串总是第一个字符等于字符串的最后一个字符。”***
只需要一步就能平衡，那就是 **s.back() = s.front()。**见下面提供的证明

> **证明:**
> 
> 上述方法可以用数学归纳法原理来证明。
> **注:**在下面的证明中，考虑了第一个字符等于最后一个字符的所有情况。
> 
> 对于 n = 0 —>空字符串" "//计数“10”= 0 &计数“01”= 0
> 对于 n = 1—>“0”或“1”//计数“10”= 0&计数“01”= 0
> 对于 n = 2—>“00”或“11”//计数“10”= 0&计数“01”= 0
> 对于 n = 3
> 
> —>“000”//计数“10”= 0 &计数“01”= 0
> 或“111”//计数“10”= 0&计数“01”= 0
> 或“010”//计数“10”= 1&计数“01”= 1
> 或“101”//计数“10”= 1&计数“01”= 1
> 
> 因此，根据数学归纳法的原理，每 n 个就有一个真实的**，其中 **n 是一个自然数**。**

下面是上述方法的实现。

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of replacements
int minimizeReplacements(string str)
{
    unordered_map<string, int> count;
    string temp;

    // Loop to count the minimum number
    // of replacements required
    for (int i = 0; i <
        str.length() - 1; i++) {
        temp = str.substr(i, 2);
        count[temp]++;
    }

    return abs(count["10"] - count["01"]);
}

// Driver code
int main()
{
    // Given string
    string str = "101010";
    cout << minimizeReplacements(str) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.HashMap;

class GFG{

// Function to count the minimum
// number of replacements
static int minimizeReplacements(String str)
{
    HashMap<String,
            Integer> count = new HashMap<String,
                                         Integer>();
    String temp;

    // Loop to count the minimum number
    // of replacements required
    for(int i = 0; i < str.length() - 1; i++)
    {
        temp = str.substring(i, i + 2);
        if (count.containsKey(temp))
            count.put(temp, count.get(temp) + 1);
        else
            count.put(temp, 1);
    }
    return Math.abs(count.get("10") - count.get("01"));
}

// Driver code
public static void main(String args[])
{

    // Given string
    String str = "101010";
    System.out.print(minimizeReplacements(str));
}
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to count the minimum
# number of replacements
def minimizeReplacements(str):
    count = {}
    temp = ""

   # Loop to count the minimum number
   # of replacements required
    for i in range(0, len(str)-1):
        temp = str[i: i+2]
        if temp in count:
            count[temp] = count[temp] + 1
        else:
            count[temp] = 1
    return abs(count["10"] - count["01"])

    # Driver code

    # Given string
str = "101010"
print(minimizeReplacements(str))

# This code is contributed by Potta Lokesh
```

## C#

```
// C# code to implement above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to count the minimum
    // number of replacements
    static int minimizeReplacements(string str)
    {
        Dictionary<string, int> count
            = new Dictionary<string, int>();
        string temp;

        // Loop to count the minimum number
        // of replacements required
        for (int i = 0; i < str.Length - 1; i++) {
            temp = str.Substring(i, 2);
            if (count.ContainsKey(temp))
                count[temp]++;
            else
                count[temp] = 1;
        }

        return Math.Abs(count["10"] - count["01"]);
    }

    // Driver code
    public static void Main()
    {
        // Given string
        string str = "101010";
        Console.WriteLine(minimizeReplacements(str));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // JavaScript code to implement above approach

    // Function to count the minimum
    // number of replacements
    const minimizeReplacements = (str) => {
        count = {};
        let temp = "";

        // Loop to count the minimum number
        // of replacements required
        for (let i = 0; i <
            str.length - 1; i++) {
            temp = str.substring(i, i + 2);
            if (temp in count) count[temp]++;
            else count[temp] = 1;
        }

        return Math.abs(count["10"] - count["01"]);
    }

    // Driver code

    // Given string
    let str = "101010";
    document.write(minimizeReplacements(str));

    //  This code is contributed by rakeshsahni

</script>
```

**Output**

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)