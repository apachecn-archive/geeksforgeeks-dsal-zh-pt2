# 没有连续相同字母的最长子串的长度

> 原文:[https://www . geesforgeks . org/无连续相同字母的最长子串长度/](https://www.geeksforgeeks.org/length-of-the-longest-substring-with-no-consecutive-same-letters/)

给定一个字符串 **str** ，任务是找到最长的子字符串的长度，该子字符串没有任何一对连续的相同字符。
**例:**

> **输入:**str = " abcded "
> **输出:**4
> 【ABCD】最长
> **输入:**str = " ccccccdeedff "
> **输出:**5
> 【ededf】最长

**方法:**可以按照以下步骤解决上述问题:

*   最初将 **cnt** 和 **maxi** 初始化为 **1** ，因为这是最长答案长度的最小答案。
*   迭代从 **1** 到**n–1**的字符串，如果 **str[i]！= str[I–1]**。
*   如果**str[I]= = str[I–1]**，则将 **cnt** 重新初始化为 **1** 和 **maxi** 至 **max(maxi，cnt)** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the length
// of the required sub-string
int longestSubstring(string s)
{
    int cnt = 1;
    int maxi = 1;

    // Get the length of the string
    int n = s.length();

    // Iterate in the string
    for (int i = 1; i < n; i++) {

        // Check for not consecutive
        if (s[i] != s[i - 1])
            cnt++;
        else {

            // If cnt greater than maxi
            maxi = max(cnt, maxi);

            // Re-initialize
            cnt = 1;
        }
    }

    // Check after iteration
    // is complete
    maxi = max(cnt, maxi);

    return maxi;
}

// Driver code
int main()
{
    string s = "ccccdeededff";
    cout << longestSubstring(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.lang.Math;

class GfG
{

    // Function to return the length
    // of the required sub-string
    static int longestSubstring(String s)
    {
        int cnt = 1, maxi = 1;

        // Get the length of the string
        int n = s.length();

        // Iterate in the string
        for (int i = 1; i < n; i++)
        {

            // Check for not consecutive
            if (s.charAt(i) != s.charAt(i-1))
                cnt++;
            else
            {

                // If cnt greater than maxi
                maxi = Math.max(cnt, maxi);

                // Re-initialize
                cnt = 1;
            }
        }

        // Check after iteration is complete
        maxi = Math.max(cnt, maxi);

        return maxi;
    }

    // Driver code
    public static void main(String []args)
    {

        String s = "ccccdeededff";
        System.out.println(longestSubstring(s));
    }
}

// This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to return the length
    // of the required sub-string
    static int longestSubstring(string s)
    {
        int cnt = 1, maxi = 1;

        // Get the length of the string
        int n = s.Length;

        // Iterate in the string
        for (int i = 1; i < n; i++)
        {

            // Check for not consecutive
            if (s[i] != s[i - 1])
                cnt++;
            else
            {

                // If cnt greater than maxi
                maxi = Math.Max(cnt, maxi);

                // Re-initialize
                cnt = 1;
            }
        }

        // Check after iteration is complete
        maxi = Math.Max(cnt, maxi);

        return maxi;
    }

    // Driver code
    static void Main()
    {

        string s = "ccccdeededff";
        Console.WriteLine(longestSubstring(s));
    }
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the length
# of the required sub-string
def longestSubstring(s) :

    cnt = 1;
    maxi = 1;

    # Get the length of the string
    n = len(s);

    # Iterate in the string
    for i in range(1, n) :

        # Check for not consecutive
        if (s[i] != s[i - 1]) :
            cnt += 1;

        else :

            # If cnt greater than maxi
            maxi = max(cnt, maxi);

            # Re-initialize
            cnt = 1;

    # Check after iteration
    # is complete
    maxi = max(cnt, maxi);

    return maxi;

# Driver code
if __name__ == "__main__" :

    s = "ccccdeededff";
    print(longestSubstring(s));

# This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the length
// of the required sub-string
function longestSubstring($s)
{
    $cnt = 1;
    $maxi = 1;

    // Get the length of the string
    $n = strlen($s);

    // Iterate in the string
    for ($i = 1; $i < $n; $i++)
    {

        // Check for not consecutive
        if ($s[$i] != $s[$i - 1])
            $cnt++;
        else
        {

            // If cnt greater than maxi
            $maxi = max($cnt, $maxi);

            // Re-initialize
            $cnt = 1;
        }
    }

    // Check after iteration
    // is complete
    $maxi = max($cnt, $maxi);

    return $maxi;
}

// Driver code
$s = "ccccdeededff";
echo longestSubstring($s);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach class GfG

// Function to return the length
// of the required sub-string
function longestSubstring(s)
{
    var cnt = 1, maxi = 1;

    // Get the length of the string
    var n = s.length;

    // Iterate in the string
    for (i = 1; i < n; i++)
    {

        // Check for not consecutive
        if (s.charAt(i) != s.charAt(i-1))
            cnt++;
        else
        {

            // If cnt greater than maxi
            maxi = Math.max(cnt, maxi);

            // Re-initialize
            cnt = 1;
        }
    }

    // Check after iteration is complete
    maxi = Math.max(cnt, maxi);

    return maxi;
}

// Driver code
var s = "ccccdeededff";
document.write(longestSubstring(s));

// This code contributed by shikhasingrajput
</script>
```

**Output:** 

```
5
```