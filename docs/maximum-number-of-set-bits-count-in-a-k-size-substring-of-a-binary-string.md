# 二进制字符串的 K 大小子串中的最大设置位数

> 原文:[https://www . geesforgeks . org/最大集位数-k 大小-二进制字符串的子字符串计数/](https://www.geeksforgeeks.org/maximum-number-of-set-bits-count-in-a-k-size-substring-of-a-binary-string/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和一个整数 **K** 。任务是找到大小为 k 的子串中出现的最大设置位数。

**示例:**

> **输入:**S =“100111010”，K = 3
> **输出:** 3
> **解释:**
> 子串“111”包含 3 个设置位。
> 
> **输入:**S =“0000000”，K = 4
> **输出:** 0
> **说明:** S 里面没有设置位，所以 ans 为 0。

**天真方法:**

1.  [生成大小为 K 的所有子串](https://www.geeksforgeeks.org/python-extract-k-length-substrings/)。
2.  查找所有子串中设置位的最大计数。

***时间复杂度:** O( N <sup>2</sup> )。*
***辅助空间:** O(1)。*

**有效方法:**这个问题可以使用[滑动窗口技术来解决。](https://www.geeksforgeeks.org/window-sliding-technique/)

1.  取 ***【最大计数】*** 变量存储设置位的最大计数， ***计数*** 变量存储当前窗口的计数设置位。
2.  从 1 到 K 遍历字符串，计算设置位的 ***计数*** ，存储为 ***最大计数*** 。
3.  从 K + 1 到字符串长度遍历字符串。
4.  每次迭代时，如果设置了**(K–I)<sup>第</sup>** 位，则减少 ***计数*** 。如果设置了 **i <sup>th</sup>** 位，则增加 ***计数*** 。对比更新 ***maxcount*** 。
5.  完成数组遍历后，最后返回 ***maxcount。**T3】*

下面是上述方法的实现:

## C++

```
// C++ program to find the maximum
// set bits in a substring of size K
#include<bits/stdc++.h>
using namespace std;

// Function that find Maximum number
// of set bit appears in a substring
// of size K.
int maxSetBitCount(string s, int k)
{
    int maxCount = 0, n = s.length();
    int count = 0;

    // Traverse string 1 to k
    for(int i = 0; i < k; i++)
    {

       // Increment count if
       // character is set bit
       if (s[i] == '1')
           count++;
    }
    maxCount = count;

    // Traverse string k+1
    // to length of string
    for(int i = k; i < n; i++)
    {

       // Remove the contribution of the
       // (i - k)th character which is no
       // longer in the window
       if (s[i - k] == '1')
           count--;

       // Add the contribution of
       // the current character
       if (s[i] == '1')
           count++;

       // Update maxCount at for
       // each window of size k
       maxCount = max(maxCount, count);
    }

    // Return maxCount
    return maxCount;
}

// Driver code
int main()
{
    string s = "100111010";
    int k = 3;

    cout << (maxSetBitCount(s, k));
    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// set bits in a substring of size K
import java.util.*;

class GFG {

    // Function that find Maximum number
    // of set bit appears in a substring
    // of size K.
    static int maxSetBitCount(String s, int k)
    {

        int maxCount = 0, n = s.length();
        int count = 0;

        // Traverse string 1 to k
        for (int i = 0; i < k; i++) {
            // Increment count if
            // character is set bit
            if (s.charAt(i) == '1')
                count++;
        }

        maxCount = count;

        // Traverse string k+1
        // to length of string
        for (int i = k; i < n; i++) {

            // remove the contribution of the
            // (i - k)th character which is no
            // longer in the window
            if (s.charAt(i - k) == '1')
                count--;

            // add the contribution of
            // the current character
            if (s.charAt(i) == '1')
                count++;

            // update maxCount at for
            // each window of size k
            maxCount = Math.max(maxCount, count);
        }

        // return maxCount
        return maxCount;
    }
    // Driver Program
    public static void main(String[] args)
    {
        String s = "100111010";
        int k = 3;

        System.out.println(maxSetBitCount(s, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# set bits in a substring of size K

# Function that find Maximum number
# of set bit appears in a substring
# of size K.
def maxSetBitCount(s, k):

    maxCount = 0
    n = len(s)
    count = 0

    # Traverse string 1 to k
    for i in range(k):

        # Increment count if
        # character is set bit
        if (s[i] == '1'):
            count += 1

    maxCount = count

    # Traverse string k+1
    # to length of string
    for i in range(k, n):

        # Remove the contribution of the
        # (i - k)th character which is no
        # longer in the window
        if (s[i - k] == '1'):
            count -= 1

        # Add the contribution of
        # the current character
        if (s[i] == '1'):
            count += 1

        # Update maxCount at for
        # each window of size k
        maxCount = max(maxCount, count)

    # Return maxCount
    return maxCount

# Driver code
if __name__ == '__main__':

    s = "100111010"
    k = 3

    print(maxSetBitCount(s, k))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the maximum
// set bits in a substring of size K
using System;
class GFG {

// Function that find Maximum number
// of set bit appears in a substring
// of size K.
static int maxSetBitCount(string s, int k)
{

    int maxCount = 0, n = s.Length;
    int count = 0;

    // Traverse string 1 to k
    for (int i = 0; i < k; i++)
    {
        // Increment count if
        // character is set bit
        if (s[i] == '1')
            count++;
    }

    maxCount = count;

    // Traverse string k+1
    // to length of string
    for (int i = k; i < n; i++)
    {

        // remove the contribution of the
        // (i - k)th character which is no
        // longer in the window
        if (s[i - k] == '1')
            count--;

        // add the contribution of
        // the current character
        if (s[i] == '1')
            count++;

        // update maxCount at for
        // each window of size k
        maxCount = Math.Max(maxCount, count);
    }

    // return maxCount
    return maxCount;
}
// Driver Program
public static void Main()
{
    string s = "100111010";
    int k = 3;

    Console.Write(maxSetBitCount(s, k));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// set bits in a substring of size K

// Function that find Maximum number
// of set bit appears in a substring
// of size K.
function maxSetBitCount(s, k)
{
    var maxCount = 0, n = s.length;
    var count = 0;

    // Traverse string 1 to k
    for(var i = 0; i < k; i++)
    {

       // Increment count if
       // character is set bit
       if (s[i] == '1')
           count++;
    }
    maxCount = count;

    // Traverse string k+1
    // to length of string
    for(var i = k; i < n; i++)
    {

       // Remove the contribution of the
       // (i - k)th character which is no
       // longer in the window
       if (s[i - k] == '1')
           count--;

       // Add the contribution of
       // the current character
       if (s[i] == '1')
           count++;

       // Update maxCount at for
       // each window of size k
       maxCount = Math.max(maxCount, count);
    }

    // Return maxCount
    return maxCount;
}

// Driver code
var s = "100111010";
var k = 3;
document.write(maxSetBitCount(s, k));

// This code is contributed by famously.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N)。*
***辅助空间:** O(1)。*