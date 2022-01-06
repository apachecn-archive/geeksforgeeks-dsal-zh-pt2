# 最多 K 个替换的字典上最大的字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最多 k 个可能的最大字符串替换/](https://www.geeksforgeeks.org/lexicographically-largest-string-possible-by-at-most-k-replacements/)

给定一个由小写字母组成的长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过替换给定字符串中最多 K 个字符来找到字典上最长的字符串。

**示例:**

> **输入:**S =“dbza”，K = 1
> **输出:** zbza
> **说明:**将 S[0] (= 'd ')替换为' z '，得到字典上最大的字符串。
> 
> **输入:** S = "zzzz "，K = 2
> T3】输出: zzzz

**方法:**给定的问题可以用 [<u>贪婪方法</u>](https://www.geeksforgeeks.org/greedy-algorithms/) 解决。思路是从左到右遍历数组，将所有非 **z** 字符替换为 **z** 。按照以下步骤解决问题:

*   将 **i = 0** 循环至字符串长度:
    *   如果当前字符不等于 **z** ，且 **K** 不等于 **0:**
        *   然后，用 **z** 替换当前字符。
        *   **K = K–1。**
*   最后，返回修改后的字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach

#include <bits/stdc++.h>
using namespace std;

string largestString(string s, int k)
{
    // Traverse each element of the string
    for (int i = 0; i < s.size(); i++) {

        // If the current character
        // can be replaced with 'z'
        if (s[i] != 'z' && k > 0) {

            s[i] = 'z';
            k--;
        }
    }

    // Return the modified string
    return s;
}

// Driver code
int main()
{
    string s = "dbza";
    int k = 1;

    cout << largestString(s, k) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

static String largestString(String s, int k)
{

    // Traverse each element of the string
    for(int i = 0; i < s.length(); i++)
    {

        // If the current character
        // can be replaced with 'z'
        if (s.charAt(i) != 'z' && k > 0)
        {
            s = s.replace(s.charAt(i),'z');
            k--;
        }
    }

    // Return the modified string
    return s;
}

// Driver code
public static void main(String args[])
{
    String s = "dbza";
    int k = 1;

    System.out.println(largestString(s, k));
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
def largestString(s, k):

    # Traverse each element of the string
    for i in range(len(s)):

        # If the current character
        # can be replaced with 'z'
        if (s[i] != 'z' and k > 0):
            s[i] = 'z'
            k -= 1

    # Return the modified string
    return "".join(s)

# Driver code
if __name__ == '__main__':

    s = "dbza"
    k = 1

    print (largestString([i for i in s], k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;

class GFG{

static string largestString(string s, int k)
{

    // Traverse each element of the string
    for(int i = 0; i < s.Length; i++)
    {

        // If the current character
        // can be replaced with 'z'
        if (s[i] != 'z' && k > 0)
        {
            s = s.Replace(s[i],'z');
            k--;
        }
    }

    // Return the modified string
    return s;
}

// Driver code
public static void Main()
{
    string s = "dbza";
    int k = 1;

    Console.Write(largestString(s, k));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
        // JavaScript implementation of
        // the above approach

        function largestString(s, k)
        {

            // Traverse each element of the string
            for (let i = 0; i < s.length; i++) {

                // If the current character
                // can be replaced with 'z'
                if (s[i] != 'z' && k > 0) {
                    s = s.substring(0, i) + 'z' + s.substring(i + 1);
                    k--;
                }
            }

            // Return the modified string
            return s;
        }

        // Driver code

        var s = "dbza";
        var k = 1;

        document.write(largestString(s, k));

  // This code is contributed by Potta Lokesh
  </script>
```

**Output:** 

```
zbza
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)