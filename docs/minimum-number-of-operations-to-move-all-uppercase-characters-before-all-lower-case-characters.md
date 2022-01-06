# 将所有大写字符移到所有小写字符之前的最小操作次数

> 原文:[https://www . geeksforgeeks . org/最小操作数-在所有小写字符之前移动所有大写字符/](https://www.geeksforgeeks.org/minimum-number-of-operations-to-move-all-uppercase-characters-before-all-lower-case-characters/)

给定一个字符串**字符串**，包含大写和小写字符。在单个操作中，任何小写字符都可以转换为大写字符，反之亦然。任务是打印所需的最小数量的此类操作，以便结果字符串由零个或多个大写字符后跟零个或多个小写字符组成。
**例:**

> **输入:** str = "geEks"
> **输出:** 1
> 前 2 个字符可以转换为大写字符，即“geEks”进行 2 次操作。
> 或者第三个字符可以一次操作转换成小写字符即“极客”。
> **输入:** str = "geek"
> **输出:** 0
> 字符串已经是指定的格式。

**方法:**有两种可能的情况:

*   查找字符串中最后一个大写字符的索引，并将出现在它前面的所有小写字符转换为大写字符。
*   或者，找到字符串中第一个小写字符的索引，并将其后出现的所有大写字符转换为小写字符。

选择所需操作最少的情况。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the minimum
// number of operations required
int minOperations(string str, int n)
{

    // To store the indices of the last uppercase
    // and the first lowercase character
    int i, lastUpper = -1, firstLower = -1;

    // Find the last uppercase character
    for (i = n - 1; i >= 0; i--)
    {
        if (isupper(str[i]))
        {
            lastUpper = i;
            break;
        }
    }

    // Find the first lowercase character
    for (i = 0; i < n; i++)
    {
        if (islower(str[i]))
        {
            firstLower = i;
            break;
        }
    }

    // If all the characters are either
    // uppercase or lowercase
    if (lastUpper == -1 || firstLower == -1)
        return 0;

    // Count of uppercase characters that appear
    // after the first lowercase character
    int countUpper = 0;
    for (i = firstLower; i < n; i++)
    {
        if (isupper(str[i]))
        {
            countUpper++;
        }
    }

    // Count of lowercase characters that appear
    // before the last uppercase character
    int countLower = 0;
    for (i = 0; i < lastUpper; i++)
    {
        if (islower(str[i]))
        {
            countLower++;
        }
    }

    // Return the minimum operations required
    return min(countLower, countUpper);
}

// Driver Code
int main()
{
    string str = "geEksFOrGEekS";
    int n = str.length();
    cout << minOperations(str, n) << endl;
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the minimum
    // number of operations required
    static int minOperations(String str, int n)
    {

        // To store the indices of the last uppercase
        // and the first lowercase character
        int i, lastUpper = -1, firstLower = -1;

        // Find the last uppercase character
        for (i = n - 1; i >= 0; i--) {
            if (Character.isUpperCase(str.charAt(i))) {
                lastUpper = i;
                break;
            }
        }

        // Find the first lowercase character
        for (i = 0; i < n; i++) {
            if (Character.isLowerCase(str.charAt(i))) {
                firstLower = i;
                break;
            }
        }

        // If all the characters are either
        // uppercase or lowercase
        if (lastUpper == -1 || firstLower == -1)
            return 0;

        // Count of uppercase characters that appear
        // after the first lowercase character
        int countUpper = 0;
        for (i = firstLower; i < n; i++) {
            if (Character.isUpperCase(str.charAt(i))) {
                countUpper++;
            }
        }

        // Count of lowercase characters that appear
        // before the last uppercase character
        int countLower = 0;
        for (i = 0; i < lastUpper; i++) {
            if (Character.isLowerCase(str.charAt(i))) {
                countLower++;
            }
        }

        // Return the minimum operations required
        return Math.min(countLower, countUpper);
    }

    // Driver Code
    public static void main(String args[])
    {
        String str = "geEksFOrGEekS";
        int n = str.length();
        System.out.println(minOperations(str, n));
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum
# number of operations required
def minOperations(str, n):

    # To store the indices of the last uppercase
    # and the first lowercase character
    lastUpper = -1
    firstLower = -1

    # Find the last uppercase character
    for i in range( n - 1, -1, -1):
        if (str[i].isupper()):
            lastUpper = i
            break

    # Find the first lowercase character
    for i in range(n):
        if (str[i].islower()):
            firstLower = i
            break

    # If all the characters are either
    # uppercase or lowercase
    if (lastUpper == -1 or firstLower == -1):
        return 0

    # Count of uppercase characters that appear
    # after the first lowercase character
    countUpper = 0
    for i in range( firstLower,n):
        if (str[i].isupper()):
            countUpper += 1

    # Count of lowercase characters that appear
    # before the last uppercase character
    countLower = 0
    for i in range(lastUpper):
        if (str[i].islower()):
            countLower += 1

    # Return the minimum operations required
    return min(countLower, countUpper)

# Driver Code
if __name__ == "__main__":

    str = "geEksFOrGEekS"
    n = len(str)
    print(minOperations(str, n))

# This code is contributed by Ita_c.
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum
    // number of operations required
    static int minOperations(string str, int n)
    {

        // To store the indices of the last uppercase
        // and the first lowercase character
        int i, lastUpper = -1, firstLower = -1;

        // Find the last uppercase character
        for (i = n - 1; i >= 0; i--)
        {
            if (Char.IsUpper(str[i]))
            {
                lastUpper = i;
                break;
            }
        }

        // Find the first lowercase character
        for (i = 0; i < n; i++)
        {
            if (Char.IsLower(str[i]))
            {
                firstLower = i;
                break;
            }
        }

        // If all the characters are either
        // uppercase or lowercase
        if (lastUpper == -1 || firstLower == -1)
            return 0;

        // Count of uppercase characters that appear
        // after the first lowercase character
        int countUpper = 0;
        for (i = firstLower; i < n; i++)
        {
            if (Char.IsUpper(str[i]))
            {
                countUpper++;
            }
        }

        // Count of lowercase characters that appear
        // before the last uppercase character
        int countLower = 0;
        for (i = 0; i < lastUpper; i++)
        {
            if (Char.IsLower(str[i]))
            {
                countLower++;
            }
        }

        // Return the minimum operations required
        return Math.Min(countLower, countUpper);
    }

    // Driver Code
    public static void Main()
    {
        string str = "geEksFOrGEekS";
        int n = str.Length;
        Console.WriteLine(minOperations(str, n));
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// number of operations required
function minOperations($str, $n)
{

    // To store the indices of the last uppercase
    // and the first lowercase character
    $i; $lastUpper = -1; $firstLower = -1;

    // Find the last uppercase character
    for ($i = $n - 1; $i >= 0; $i--)
    {
        if (ctype_upper($str[$i]))
        {
            $lastUpper = $i;
            break;
        }
    }

    // Find the first lowercase character
    for ($i = 0; $i < $n; $i++)
    {
        if (ctype_lower($str[$i]))
        {
            $firstLower = $i;
            break;
        }
    }

    // If all the characters are either
    // uppercase or lowercase
    if ($lastUpper == -1 || $firstLower == -1)
        return 0;

    // Count of uppercase characters that appear
    // after the first lowercase character
    $countUpper = 0;
    for ($i = $firstLower; $i < $n; $i++)
    {
        if (ctype_upper($str[$i]))
        {
            $countUpper++;
        }
    }

    // Count of lowercase characters that appear
    // before the last uppercase character
    $countLower = 0;
    for ($i = 0; $i < $lastUpper; $i++)
    {
        if (ctype_lower($str[$i]))
        {
            $countLower++;
        }
    }

    // Return the minimum operations required
    return min($countLower, $countUpper);
    }

    // Driver Code
    {
        $str = "geEksFOrGEekS";
        $n = strlen($str);
        echo(minOperations($str, $n));
    }

// This code is contributed by Code_Mech
?>
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      //Check UpperCase
      function isupper(str) {
        return str === str.toUpperCase();
      }
      //Check UpperCase
      function islower(str) {
        return str === str.toLowerCase();
      }

      // Function to return the minimum
      // number of operations required
      function minOperations(str, n) {
        // To store the indices of the last uppercase
        // and the first lowercase character
        var i,
          lastUpper = -1,
          firstLower = -1;

        // Find the last uppercase character
        for (i = n - 1; i >= 0; i--) {
          if (isupper(str[i])) {
            lastUpper = i;
            break;
          }
        }

        // Find the first lowercase character
        for (i = 0; i < n; i++) {
          if (islower(str[i])) {
            firstLower = i;
            break;
          }
        }

        // If all the characters are either
        // uppercase or lowercase
        if (lastUpper === -1 || firstLower === -1) return 0;

        // Count of uppercase characters that appear
        // after the first lowercase character
        var countUpper = 0;
        for (i = firstLower; i < n; i++) {
          if (isupper(str[i])) {
            countUpper++;
          }
        }

        // Count of lowercase characters that appear
        // before the last uppercase character
        var countLower = 0;
        for (i = 0; i < lastUpper; i++) {
          if (islower(str[i])) {
            countLower++;
          }
        }

        // Return the minimum operations required
        return Math.min(countLower, countUpper);
      }

      // Driver Code
      var str = "geEksFOrGEekS";
      var n = str.length;
      document.write(minOperations(str, n) + "<br>");
    </script>
```

**Output:** 

```
6
```

**时间复杂度:** O(N)，其中 N 是字符串的长度。
**辅助空间:** O(1)