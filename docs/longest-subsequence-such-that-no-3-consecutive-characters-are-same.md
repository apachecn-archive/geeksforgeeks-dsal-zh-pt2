# 最长的子序列，因此没有 3 个连续的字符相同

> 原文:[https://www . geesforgeks . org/最长子序列-这样-没有-3 个连续字符是相同的/](https://www.geeksforgeeks.org/longest-subsequence-such-that-no-3-consecutive-characters-are-same/)

给定一串小写字符 **S** ，任务是找到不含 3 个连续相同字符的字符串的最长子序列。
**例**:

> **输入:**S = " eedaaad "
> T3】输出:eedaad
> T6】说明:删除字母 a 的一次出现。
> 
> **输入:** xxxtxxx
> **输出:** xxtxx

**逼近**:检查每一个大小为 3 的窗口就可以解决任务。如果 3 个字符中的任何一个不匹配，将其附加到结果字符串中，否则继续。最后，打印结果字符串。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// longest subsequence
string filterString(string s1)
{
    string sb1 = "";

    // Append the first character
    sb1 += s1[0];

    // Append the second character
    sb1 += (s1[1]);

    // Loop for i=2 to n
    for (int i = 2; i < s1.length(); ++i)
    {

        // If consecutive three element
        // are not equal then append
        if (s1[i] != s1[i - 1] || s1[i] != s1[i - 2])
        {
            sb1 += s1[i];
        }
    }
    return sb1;
}

// Driver Code
int main()
{
    string s = "eedaaad";
    string res = filterString(s);
    cout << (res);
    return 0;
}
// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class Solution {

    // Function to find the
    // longest subsequence
    public static String
    filterString(String s1)
    {
        StringBuilder sb1 = new StringBuilder();

        // Append the first character
        sb1.append(s1.charAt(0));

        // Append the second character
        sb1.append(s1.charAt(1));

        // Loop for i=2 to n
        for (int i = 2; i < s1.length();
             ++i) {

            // If consecutive three element
            // are not equal then append
            if (s1.charAt(i) != s1.charAt(i - 1)
                || s1.charAt(i) != s1.charAt(i - 2)) {
                sb1.append(s1.charAt(i));
            }
        }
        return sb1.toString();
    }

    // Driver Code
    public static void main(String[] args)
    {
        String s = "eedaaad";
        String res = filterString(s);
        System.out.println(res);
    }
}
```

## 蟒蛇 3

```
# Python 3 code for the above approach

# Function to find the
# longest subsequence
def filterString(s1):

    sb1 = ""

    # Append the first character
    sb1 += s1[0]

    # Append the second character
    sb1 += (s1[1])

    # Loop for i=2 to n
    for i in range(2, len(s1)):

        # If consecutive three element
        # are not equal then append
        if (s1[i] != s1[i - 1] or s1[i] != s1[i - 2]):

            sb1 += s1[i]

    return sb1

# Driver Code
if __name__ == "__main__":

    s = "eedaaad"
    res = filterString(s)
    print(res)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Text;
class Solution
{

    // Function to find the
    // longest subsequence
    public static string filterstring(string s1)
    {
        StringBuilder sb1 = new StringBuilder();

        // Append the first character
        sb1.Append(s1[0]);

        // Append the second character
        sb1.Append(s1[1]);

        // Loop for i=2 to n
        for (int i = 2; i < s1.Length; ++i)
        {

            // If consecutive three element
            // are not equal then append
            if (s1[i] != s1[i - 1]
                || s1[i] != s1[i - 2])
            {
                sb1.Append(s1[i]);
            }
        }
        return sb1.ToString();
    }

    // Driver Code
    public static void Main()
    {
        string s = "eedaaad";
        string res = filterstring(s);
        Console.Write(res);
    }
}

// This code is contributed by gfgking.
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach
    // Function to find the
    // longest subsequence
    const filterString = (s1) => {
        let sb1 = "";

        // Append the first character
        sb1 += s1[0];

        // Append the second character
        sb1 += (s1[1]);

        // Loop for i=2 to n
        for (let i = 2; i < s1.length; ++i) {

            // If consecutive three element
            // are not equal then append
            if (s1[i] != s1[i - 1] || s1[i] != s1[i - 2]) {
                sb1 += s1[i];
            }
        }
        return sb1;
    }

    // Driver Code
    let s = "eedaaad";
    let res = filterString(s);
    document.write(res);

    // This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
eedaad
```

***时间复杂度*** : O(N)，其中 N 为弦的长度
***辅助空间*** : O(1)