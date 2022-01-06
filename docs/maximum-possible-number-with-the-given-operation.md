# 给定操作的最大可能数量

> 原文:[https://www . geesforgeks . org/给定操作的最大可能数量/](https://www.geeksforgeeks.org/maximum-possible-number-with-the-given-operation/)

给定一个正整数 **N** ，任务是通过改变数字将这个整数转换成最大可能的整数，而不用前导零。一个数字 **X** 只有在 **X + Y = 9** 的情况下才能变成一个数字 **Y** 。
**举例:**

> **输入:**N = 42
> T3】输出: 57
> 变化 4 - > 5 和 2 - > 7。
> **输入:** N = 1
> **输出:** 8

**方法:**只有大于等于 5 的数字需要更改，因为更改小于 5 的数字会导致数字变大。更新所有必需的数字后，检查结果数字是否有前导零，如果有，则将其更改为 9。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum possible
// integer that can be obtained from the
// given integer after performing
// the given operations
string maxInt(string str)
{
    // For every digit
    for (int i = 0; i < str.length(); i++) {

        // Digits greater than or equal to 5
        // need not to be changed as changing
        // them will lead to a smaller number
        if (str[i] < '5') {
            str[i] = ('9' - str[i]) + '0';
        }
    }

    // The resulting integer
    // cannot have leading zero
    if (str[0] == '0')
        str[0] = '9';

    return str;
}

// Driver code
int main()
{
    string str = "42";

    cout << maxInt(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function to return the maximum possible
    // integer that can be obtained from the
    // given integer after performing
    // the given operations
    static String maxInt(char str[])
    {
        // For every digit
        for (int i = 0; i < str.length; i++)
        {

            // Digits greater than or equal to 5
            // need not to be changed as changing
            // them will lead to a smaller number
            if (str[i] < '5')
            {
                str[i] = (char)(('9' - str[i]) + '0');
            }
        }

        // The resulting integer
        // cannot have leading zero
        if (str[0] == '0')
            str[0] = '9';

        String str2 = new String(str);
        return str2;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "42";

        System.out.println(maxInt(str.toCharArray()));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum possible
# integer that can be obtained from the
# given integer after performing
# the given operations
def maxInt(string):
    string2 = ""

    # For every digit
    for i in range(0, len(string)):

        # Digits greater than or equal to 5
        # need not to be changed as changing
        # them will lead to a smaller number
        if (string[i] < '5'):
            string2 += str((ord('9') - ord(string[i])))
        else:
            string2 += str(string[i])

    # The resulting integer
    # cannot have leading zero
    if (string2[0] == '0'):
        string2[0] = '9'

    return string2

# Driver code
if __name__ == '__main__':

    string = "42"
    print(maxInt(string))

# This code is contributed by ashutosh450
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum possible
    // integer that can be obtained from the
    // given integer after performing
    // the given operations
    static String maxInt(char []str)
    {
        // For every digit
        for (int i = 0; i < str.Length; i++)
        {

            // Digits greater than or equal to 5
            // need not to be changed as changing
            // them will lead to a smaller number
            if (str[i] < '5')
            {
                str[i] = (char)(('9' - str[i]) + '0');
            }
        }

        // The resulting integer
        // cannot have leading zero
        if (str[0] == '0')
            str[0] = '9';

        String str2 = new String(str);
        return str2;
    }

    // Driver code
    public static void Main (String []args)
    {
        String str = "42";

        Console.WriteLine(maxInt(str.ToCharArray()));
    }
}

// This code is contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Function to return the maximum possible
// integer that can be obtained from the
// given integer after performing
// the given operations
function maxInt(str)
{
    // For every digit
    var str2 = "";
    for (var i = 0; i < str.length; i++) {

        // Digits greater than or equal to 5
        // need not to be changed as changing
        // them will lead to a smaller number
        if (str[i] < '5') {
            var l = ('9'.charCodeAt(0) - str[i].charCodeAt(0)) + '0'.charCodeAt(0);
            str2 = str2.concat(String.fromCharCode(l));
        }
    }

    // The resulting integer
    // cannot have leading zero
    if (str2[0] == '0')
        str2[0] = '9';

    return str2;
}

// Driver code
var str = "42";
document.write(maxInt(str))

// This code is contributed by ShubhamSingh10
</script>
```

**Output:** 

```
57
```