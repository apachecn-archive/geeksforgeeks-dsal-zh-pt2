# 等于 1 和 0 的最长子串的长度

> 原文:[https://www . geesforgeks . org/最长子串长度等于 1 和 0/](https://www.geeksforgeeks.org/length-of-the-longest-substring-with-equal-1s-and-0s/)

给定一个二进制字符串。我们需要找到最长的平衡子串的长度。如果子串包含相等的 0 和 1，则它是平衡的。

**示例:**

```
Input : input = 110101010
Output : Length of longest balanced
         sub string = 8

Input : input = 0000
Output : Length of longest balanced
         sub string = 0
```

一个**简单的解决方案**是使用两个嵌套循环来生成每个子串。第三个循环计算当前子串中 0 和 1 的个数。时间复杂度为 0(T2 3)

下面是上述方法的实现:

## C++

```
// C++ program to find the length of
// the longest balanced substring
#include<bits/stdc++.h>
using namespace std;

// Function to check if a string contains
// equal number of one and zeros or not
bool isValid(string p)
{
    int n = p.length();
    int c1 = 0, c0 = 0;

    for(int i =0; i < n; i++)
    {
        if(p[i] == '0')
            c0++;
        if(p[i] == '1')
            c1++;
    }

    return (c0 == c1) ? true : false;
}

// Function to find the length of
// the longest balanced substring
int longestSub(string s)
{
    int max_len = 0;
    int n = s.length();

    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {
            if(isValid(s.substr(i, j - i + 1)) && max_len < j - i + 1)
                max_len = j - i + 1;
        }

    }
    return max_len;

}

// Driver code
int main()
{
    string s = "101001000";

    // Function call
    cout << longestSub(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of 
// the longest balanced substring
import java.io.*;
import java.util.*;
class GFG
{

  // Function to check if a string contains
  // equal number of one and zeros or not
  public static boolean isValid(String p)
  {
    int n = p.length();
    int c1 = 0, c0 = 0;
    for (int i = 0; i < n; i++)
    {
      if(p.charAt(i) == '0')
      {
        c0++;
      }
      if(p.charAt(i) == '1')
      {
        c1++;
      }
    }
    if(c0 == c1)
    {
      return true;
    }
    else
    {
      return false;
    }
  }
  // Function to find the length of 
  // the longest balanced substring
  public static int longestSub(String s)
  {
    int max_len = 0;
    int n = s.length();
    for(int i = 0; i < n; i++)
    {
      for(int j = i; j < n; j++)
      {
        if(isValid(s.substring(i, j + 1)) && max_len < j - i + 1)
        {
          max_len = j - i + 1;
        }
      }
    }
    return max_len;
  }

  // Driver code
  public static void main (String[] args)
  {
    String s = "101001000";

    // Function call
    System.out.println(longestSub(s));
  }
}

//  This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to find the length of
# the longest balanced substring

# Function to check if a contains
# equal number of one and zeros or not
def isValid(p):

    n = len(p)
    c1 = 0
    c0 = 0

    for i in range(n):
        if (p[i] == '0'):
            c0 += 1
        if (p[i] == '1'):
            c1 += 1

    if (c0 == c1):
        return True
    else:
        return False

# Function to find the length of
# the longest balanced substring
def longestSub(s):

    max_len = 0
    n = len(s)

    for i in range(n):
        for j in range(i, n):
            if (isValid(s[i : j - i + 1]) and
                    max_len < j - i + 1):
                max_len = j - i + 1

    return max_len

# Driver code
if __name__ == '__main__':

    s = "101001000"

    # Function call
    print(longestSub(s))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find the length of 
// the longest balanced substring
using System;

class GFG{

// Function to check if a string contains
// equal number of one and zeros or not
static bool isValid(string p)
{
    int n = p.Length;
    int c1 = 0, c0 = 0;

    for(int i = 0; i < n; i++)
    {
        if (p[i] == '0')
        {
            c0++;
        }
        if (p[i] == '1')
        {
            c1++;
        }
    }
    if (c0 == c1)
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Function to find the length of 
// the longest balanced substring
public static int longestSub(string s)
{
    int max_len = 0;
    int n = s.Length;

    for(int i = 0; i < n; i++)
    {
        for(int j = i; j < n; j++)
        {
            if (isValid(s.Substring(i, j - i + 1)) &&
                             max_len < j - i + 1)
            {
                max_len = j - i + 1;
            }
        }
    }
    return max_len;
}

// Driver code
static public void Main()
{
    string s = "101001000";

    // Function call
    Console.WriteLine(longestSub(s));
}
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// Javascript program to find the length of
// the longest balanced substring

// Function to check if a string contains
// equal number of one and zeros or not
function isValid(p)
{
    var n = p.length;
    var c1 = 0, c0 = 0;

    for(var i =0; i < n; i++)
    {
        if(p[i] == '0')
            c0++;
        if(p[i] == '1')
            c1++;
    }

    return (c0 == c1) ? true : false;
}

// Function to find the length of
// the longest balanced substring
function longestSub(s)
{
    var max_len = 0;
    var n = s.length;

    for(var i = 0; i < n; i++)
    {
        for(var j = i; j < n; j++)
        {
            if(isValid(s.substr(i, j - i + 1)) && max_len < j - i + 1)
                max_len = j - i + 1;
        }

    }
    return max_len;

}

// Driver code
var s = "101001000";

// Function call
document.write( longestSub(s));

</script>
```

**输出:**

```
6
```

一个有效的解决方案是使用散列法。
1)遍历字符串，记录 1 和 0 的计数，分别为 count_1 和 count_0。
2)查看两个计数之间的当前差异以前是否出现过(我们使用哈希来存储所有差异和出现差异的第一个索引)。如果是，则来自先前外观和当前索引的子字符串具有相同数量的 0 和 1。

下面是上述方法的实现。

## C++

```
// C++ for finding length of longest balanced
// substring
#include<bits/stdc++.h>
using namespace std;

// Returns length of the longest substring
// with equal number of zeros and ones.
int stringLen(string str)
{
    // Create a map to store differences
    // between counts of 1s and 0s.
    map<int, int> m;

    // Initially difference is 0.
    m[0] = -1;  

    int count_0 = 0, count_1 = 0;
    int res = 0;
    for (int i=0; i<str.size(); i++)
    {
        // Keeping track of counts of
        // 0s and 1s.
        if (str[i] == '0')
            count_0++;
        else
            count_1++;

        // If difference between current counts
        // already exists, then substring between
        // previous and current index has same
        // no. of 0s and 1s. Update result if this
        // substring is more than current result.
        if (m.find(count_1 - count_0) != m.end())
            res = max(res, i - m[count_1 - count_0]);

        // If current difference is seen first time.       
        else
            m[count_1 - count_0] = i;
    }

    return res;
}

// driver function
int main()
{
    string str = "101001000";
    cout << "Length of longest balanced"
            " sub string = ";
    cout << stringLen(str);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for finding the length of
// the longest balanced substring

import java.io.*;
import java.util.*;

public class MAX_LEN_0_1 {
    public static void main(String args[])throws IOException
    {
        String str = "101001000";

    // Create a map to store differences
    //between counts of 1s and 0s.
    HashMap<Integer,Integer> map = new HashMap<Integer,Integer>();

    // Initially difference is 0;
            map. put(0, -1);
            int res =0;
            int count_0 = 0, count_1 = 0;
            for(int i=0; i<str.length();i++)
            {
                // Keep track of count of 0s and 1s
                if(str.charAt(i)=='0')
                    count_0++;
                else
                    count_1++;

        // If difference between current counts
        // already exists, then substring between
        // previous and current index has same
        // no. of 0s and 1s. Update result if this
        // substring is more than current result.

                if(map.containsKey(count_1-count_0))
                    res = Math.max(res, (i - map.get(count_1-count_0)));

        // If the current difference is seen first time.
                else
                    map.put(count_1-count_0,i);

            }

            System.out.println("Length of longest balanced sub string = "+res);
    }
}
```

## 蟒蛇 3

```
# Python3 code for finding length of
# longest balanced substring

# Returns length of the longest substring
# with equal number of zeros and ones.
def stringLen( str ):

    # Create a python dictionary to store
    # differences between counts of 1s and 0s.
    m = dict()

    # Initially difference is 0.
    m[0] = -1

    count_0 = 0
    count_1 = 0
    res = 0
    for i in range(len(str)):

        # Keeping track of counts of
        # 0s and 1s.
        if str[i] == '0':
            count_0 += 1
        else:
            count_1 += 1

        # If difference between current
        # counts already exists, then
        # substring between previous and
        # current index has same no. of
        # 0s and 1s. Update result if
        # this substring is more than
        # current result.
        if m.get(count_1 - count_0)!=None:
            res = max(res, i - m[count_1 - count_0])

        # If current difference is
        # seen first time.
        else:
            m[count_1 - count_0] = i
    return res

# driver code
str = "101001000"
print("Length of longest balanced"
     " sub string = ",stringLen(str))

# This code is contributed by "Sharad_Bhardwaj"
```

## C#

```
// C# Code for finding the length of
// the longest balanced substring
using System;
using System.Collections.Generic;

class GFG
{
public static void Main(string[] args)
{
    string str = "101001000";

    // Create a map to store differences
    //between counts of 1s and 0s.
    Dictionary<int,
               int> map = new Dictionary<int,
                                         int>();

    // Initially difference is 0;
    map[0] = -1;
    int res = 0;
    int count_0 = 0, count_1 = 0;
    for (int i = 0; i < str.Length;i++)
    {
        // Keep track of count of 0s and 1s
        if (str[i] == '0')
        {
            count_0++;
        }
        else
        {
            count_1++;
        }

        // If difference between current counts
        // already exists, then substring between
        // previous and current index has same
        // no. of 0s and 1s. Update result if this
        // substring is more than current result.
        if (map.ContainsKey(count_1 - count_0))
        {
            res = Math.Max(res, (i - map[count_1 -
                                         count_0]));
        }

        // If the current difference is
        // seen first time.
        else
        {
            map[count_1 - count_0] = i;
        }

    }

    Console.WriteLine("Length of longest balanced" +
                            " sub string = " + res);
}
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript Code for finding the length of
// the longest balanced substring

    let str = "101001000";
    // Create a map to store differences
    // between counts of 1s and 0s.
    let map = new Map();

    // Initially difference is 0;
            map.set(0, -1);
            let res =0;
            let count_0 = 0, count_1 = 0;
            for(let i=0; i<str.length;i++)
            {
                // Keep track of count of 0s and 1s
                if(str[i]=='0')
                    count_0++;
                else
                    count_1++;

        // If difference between current counts
        // already exists, then substring between
        // previous and current index has same
        // no. of 0s and 1s. Update result if this
        // substring is more than current result.

                if(map.has(count_1-count_0))
                    res =
                    Math.max(res, (i -
                    map.get(count_1-count_0)));

        // If the current difference
        // is seen first time.
                else
                    map.set(count_1-count_0,i);

            }

            document.write(
            "Length of longest balanced sub string = "+res
            );

// This code is contributed by unknown2108

</script>
```

**输出:**

```
Length of longest balanced sub string = 6
```

**时间复杂度:** O(n)
扩展问题:[0 和 1 个数相等的最大子阵](https://www.geeksforgeeks.org/largest-subarray-with-equal-number-of-0s-and-1s/)

本文由[Shivam prad Han(anuj _ charm)](http://www.facebook.com/ma5ter6it)和 [ASIPU PAWAN KUMAR](https://auth.geeksforgeeks.org/profile.php?user=Pawan%20Asipu) 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。