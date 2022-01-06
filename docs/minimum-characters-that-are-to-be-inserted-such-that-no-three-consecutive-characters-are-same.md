# 要插入的最少字符，使得没有三个连续字符相同

> 原文:[https://www . geeksforgeeks . org/待插入的最少字符数-没有-三个连续字符相同/](https://www.geeksforgeeks.org/minimum-characters-that-are-to-be-inserted-such-that-no-three-consecutive-characters-are-same/)

给定一个字符串 **str** ，任务是修改该字符串，使得没有三个连续的字符相同。在一次操作中，可以在字符串的任何位置插入任何字符。找到所需的此类操作的最小数量。
**例:**

> **输入:** str = "aabbbcc"
> **输出:**1
> “AABB**d**bcc”为修改后的字符串。
> **输入:**str = " geeks forgeeks "
> **输出:** 0

**方法:**对于每三个相同的连续字符，必须在它们之间插入一个字符，以使任何三个连续字符不同。但是操作的次数需要最小化，所以字符必须插入到第二个字符之后。例如，如果字符串是“bbbb ”,那么如果字符插入在第二个位置，即“babbb ”,那么仍然有三个连续的相同字符，并且需要另一个操作来解决这个问题，但是如果字符插入在第三个位置，即“bbabb ”,那么只需要一个操作。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of characters
// that are to be inserted in str such that no
// three consecutive characters are same
int getCount(string str, int n)
{

    // To store the count of
    // operations required
    int cnt = 0;

    int i = 0;
    while (i < n - 2) {

        // A character needs to be
        // inserted after str[i + 1]
        if (str[i] == str[i + 1]
            && str[i] == str[i + 2]) {
            cnt++;
            i = i + 2;
        }

        // Current three consecutive
        // characters are not same
        else
            i++;
    }

    return cnt;
}

// Driver code
int main()
{
    string str = "aabbbcc";
    int n = str.length();

    cout << getCount(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the count of characters
    // that are to be inserted in str such that no
    // three consecutive characters are same
    static int getCount(char[] str, int n)
    {

        // To store the count of
        // operations required
        int cnt = 0;

        int i = 0;
        while (i < n - 2)
        {

            // A character needs to be
            // inserted after str[i + 1]
            if (str[i] == str[i + 1] &&
                str[i] == str[i + 2])
            {
                cnt++;
                i = i + 2;
            }

            // Current three consecutive
            // characters are not same
            else
            {
                i++;
            }
        }
        return cnt;
    }

    // Driver code
    static public void main(String[] arg)
    {
        String str = "aabbbcc";
        int n = str.length();

        System.out.println(getCount(str.toCharArray(), n));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of characters
# that are to be inserted in str1 such that no
# three consecutive characters are same
def getCount(str1, n):

    # To store the count of
    # operations required
    cnt = 0;

    i = 0;
    while (i < n - 2):

        # A character needs to be
        # inserted after str1[i + 1]
        if (str1[i] == str1[i + 1] and
            str1[i] == str1[i + 2]):
            cnt += 1
            i = i + 2

        # Current three consecutive
        # characters are not same
        else:
            i += 1

    return cnt

# Driver code
str1 = "aabbbcc"
n = len(str1)

print(getCount(str1, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the count of characters
    // that are to be inserted in str such that no
    // three consecutive characters are same
    static int getCount(string str, int n)
    {

        // To store the count of
        // operations required
        int cnt = 0;

        int i = 0;
        while (i < n - 2)
        {

            // A character needs to be
            // inserted after str[i + 1]
            if (str[i] == str[i + 1] &&
                str[i] == str[i + 2])
            {
                cnt++;
                i = i + 2;
            }

            // Current three consecutive
            // characters are not same
            else
            {
                i++;
            }
        }
        return cnt;
    }

    // Driver code
    static public void Main ()
    {
        string str = "aabbbcc";
        int n = str.Length;

        Console.WriteLine(getCount(str, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
      // JavaScript implementation of the above approach
      // Function to return the count of characters
      // that are to be inserted in str such that no
      // three consecutive characters are same
      function getCount(str, n) {
        // To store the count of
        // operations required
        var cnt = 0;

        var i = 0;
        while (i < n - 2) {
          // A character needs to be
          // inserted after str[i + 1]
          if (str[i] === str[i + 1] && str[i] === str[i + 2]) {
            cnt++;
            i = i + 2;
          }

          // Current three consecutive
          // characters are not same
          else {
            i++;
          }
        }
        return cnt;
      }

      // Driver code
      var str = "aabbbcc";
      var n = str.length;

      document.write(getCount(str, n));
    </script>
```

**Output:** 

```
1
```