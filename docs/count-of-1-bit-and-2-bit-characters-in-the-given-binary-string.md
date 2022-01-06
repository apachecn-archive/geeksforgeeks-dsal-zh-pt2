# 给定二进制字符串中 1 位和 2 位字符的计数

> 原文:[https://www . geesforgeks . org/给定二进制字符串中 1 位和 2 位字符的计数/](https://www.geeksforgeeks.org/count-of-1-bit-and-2-bit-characters-in-the-given-binary-string/)

给定两个特殊字符，第一个字符可以用一个 0 位表示，第二个字符可以用两个位表示 **10** 或 **11** 。现在给定一个由几个位表示的字符串。任务是返回它所代表的字符数。**注意**给定的字符串始终有效。
**举例:**

> **输入:** str = "11100"
> **输出:**3
> “11”“10”“0”为必输字符。
> **输入:** str = "100"
> **输出:** 2

**方法:**解决问题的方法是，如果当前字符是 0，那么它代表 1 位的单个字符，但是如果当前字符是 1，那么它之后的下一位必须包含在由两位组成的字符中，因为没有以 1 开头的单个位字符。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of required characters
int countChars(string str, int n)
{

    int i = 0, cnt = 0;

    // While there are characters left
    while (i < n) {

        // Single bit character
        if (str[i] == '0')
            i++;

        // Two-bit character
        else
            i += 2;

        // Update the count
        cnt++;
    }

    return cnt;
}

// Driver code
int main()
{
    string str = "11010";
    int n = str.length();

    cout << countChars(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG {

    // Function to return the count
    // of required characters
    static int countChars(String str, int n)
    {

        int i = 0, cnt = 0;

        // While there are characters left
        while (i < n) {

            // Single bit character
            if (str.charAt(i) == '0')
                i += 1;

            // Two-bit character
            else
                i += 2;

            // Update the count
            cnt += 1;
        }

        return cnt;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "11010";
        int n = str.length();

        System.out.println(countChars(str, n));
    }
    // This code is contributed by AnkitRai01
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of required characters
def countChars(string, n) :

    i = 0; cnt = 0;

    # While there are characters left
    while (i < n) :

        # Single bit character
        if (string[i] == '0'):
            i += 1;

        # Two-bit character
        else :
            i += 2;

        # Update the count
        cnt += 1;

    return cnt;

# Driver code
if __name__ == "__main__" :

    string = "11010";
    n = len(string);

    print(countChars(string, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the count
    // of required characters
    static int countChars(string str, int n)
    {

        int i = 0, cnt = 0;

        // While there are characters left
        while (i < n)
        {

            // Single bit character
            if (str[i] == '0')
                i += 1;

            // Two-bit character
            else
                i += 2;

            // Update the count
            cnt += 1;
        }

        return cnt;
    }

    // Driver code
    public static void Main ()
    {
        string str = "11010";
        int n = str.Length;

        Console.WriteLine(countChars(str, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

    // JavaScript implementation of the above approach

    // Function to return the count
    // of required characters
    function countChars(str, n)
    {

        let i = 0, cnt = 0;

        // While there are characters left
        while (i < n)
        {

            // Single bit character
            if (str[i] == '0')
                i += 1;

            // Two-bit character
            else
                i += 2;

            // Update the count
            cnt += 1;
        }

        return cnt;
    }

    let str = "11010";
    let n = str.length;

    document.write(countChars(str, n));

</script>
```

**Output:** 

```
3
```