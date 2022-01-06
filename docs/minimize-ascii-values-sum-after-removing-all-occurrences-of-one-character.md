# 在删除一个字符的所有出现后，最小化 ASCII 值的总和

> 原文:[https://www . geesforgeks . org/minimum-ascii-values-移除一个字符的所有出现次数后的总和/](https://www.geeksforgeeks.org/minimize-ascii-values-sum-after-removing-all-occurrences-of-one-character/)

给定字符串 **str** ，任务是在删除特定字符的每次出现后，最小化 **str** 的每个字符的 ASCII 值之和。

**示例:**

> **输入:** str = "geeksforgeeks"
> **输出:**977
> “g”出现两次->2 * 103 = 206
> “e”出现 4 次->4 * 101 = 404
> “k”出现两次->2 * 107 = 214
> s 出现两次->2 * 115 = 230
> “f” 111 = 111
> “r”出现一次- > 1 * 114 = 114
> 总和= 1381
> 为了最小化总和，从字符串
> 中删除所有出现的“e”，新的总和变为 1381–404 = 977
> **输入:**str =“ABCD”
> **输出:** 294

**进场:**

1.  取给定字符串中所有 ASCII 值的总和。
2.  另外，存储字符串中每个字符的出现次数。
3.  删除对总和贡献最大值的字符的每次出现，即其**出现次数* ASCII** 最大。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimized sum
int getMinimizedSum(string str, int len)
{
    int i, maxVal = INT_MIN, sum = 0;

    // To store the occurrences of
    // each character of the string
    int occurrences[26] = { 0 };
    for (i = 0; i < len; i++) {

        // Update the occurrence
        occurrences[str[i] - 'a']++;

        // Calculate the sum
        sum += (int)str[i];
    }

    // Get the character which is contributing
    // the maximum value to the sum
    for (i = 0; i < 26; i++)

        // Count of occurrence of the character
        // multiplied by its ASCII value
        maxVal = max(maxVal, occurrences[i] * (i + 'a'));

    // Return the minimized sum
    return (sum - maxVal);
}

// Driver code
int main()
{
    string str = "geeksforgeeks";
    int len = str.length();
    cout << getMinimizedSum(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
import java.lang.Math;

class GfG
{

    // Function to return the minimized sum
    static int getMinimizedSum(String str, int len)
    {
        int i, maxVal = Integer.MIN_VALUE, sum = 0;

        // To store the occurrences of
        // each character of the string
        int occurrences[] = new int[26];
        Arrays.fill(occurrences, 0);

        for (i = 0; i < len; i++)
        {

            // Update the occurrence
            occurrences[str.charAt(i) - 'a']++;

            // Calculate the sum
            sum += (int)str.charAt(i);
        }

        // Get the character which is contributing
        // the maximum value to the sum
        for (i = 0; i < 26; i++)

            // Count of occurrence of the character
            // multiplied by its ASCII value
            maxVal = Math.max(maxVal, occurrences[i] * (i + 'a'));

        // Return the minimized sum
        return (sum - maxVal);
    }

    // Driver code
    public static void main(String []args){

        String str = "geeksforgeeks";
        int len = str.length();
        System.out.println(getMinimizedSum(str, len));
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to return the minimized sum
def getMinimizedSum(string, length) :

    maxVal = -(sys.maxsize - 1)
    sum = 0;

    # To store the occurrences of
    # each character of the string
    occurrences = [0] * 26;

    for i in range(length) :

        # Update the occurrence
        occurrences[ord(string[i]) -
                    ord('a')] += 1;

        # Calculate the sum
        sum += ord(string[i]);

    # Get the character which is contributing
    # the maximum value to the sum
    for i in range(26) :

        # Count of occurrence of the character
        # multiplied by its ASCII value
        count = occurrences[i] * (i + ord('a'))
        maxVal = max(maxVal, count);

    # Return the minimized sum
    return (sum - maxVal);

# Driver code
if __name__ == "__main__" :

    string = "geeksforgeeks";
    length = len(string);

    print(getMinimizedSum(string, length));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to return the minimized sum
    static int getMinimizedSum(string str, int len)
    {
        int i, maxVal = Int32.MinValue, sum = 0;

        // To store the occurrences of
        // each character of the string
        int [] occurrences = new int[26];

        for (i = 0; i < len; i++)
        {

            // Update the occurrence
            occurrences[str[i] - 'a']++;

            // Calculate the sum
            sum += (int)str[i];
        }

        // Get the character which is contributing
        // the maximum value to the sum
        for (i = 0; i < 26; i++)

            // Count of occurrence of the character
            // multiplied by its ASCII value
            maxVal = Math.Max(maxVal, occurrences[i] * (i + 'a'));

        // Return the minimized sum
        return (sum - maxVal);
    }

    // Driver code
    public static void Main()
    {
        string str = "geeksforgeeks";
        int len = str.Length;
        Console.WriteLine(getMinimizedSum(str, len));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the minimized sum
      function getMinimizedSum(str, len) {
        var i,
          maxVal = -2147483648,
          sum = 0;

        // To store the occurrences of
        // each character of the string
        var occurrences = new Array(26).fill(0);

        for (i = 0; i < len; i++) {
          // Update the occurrence
          occurrences[str[i].charCodeAt(0) - "a".charCodeAt(0)]++;

          // Calculate the sum
          sum += str[i].charCodeAt(0);
        }

        // Get the character which is contributing
        // the maximum value to the sum
        for (i = 0; i < 26; i++) {
          // Count of occurrence of the character
          // multiplied by its ASCII value
          maxVal = Math.max(maxVal, occurrences[i] * (i + "a".charCodeAt(0)));
        }
        // Return the minimized sum
        return sum - maxVal;
      }

      // Driver code
      var str = "geeksforgeeks";
      var len = str.length;
      document.write(getMinimizedSum(str, len));
    </script>
```

**Output:** 

```
977
```