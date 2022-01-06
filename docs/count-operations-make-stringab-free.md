# 使二进制字符串“ab”自由的操作计数

> 原文:[https://www . geesforgeks . org/count-operations-make-string gab-free/](https://www.geeksforgeeks.org/count-operations-make-stringab-free/)

给定仅包含字符“a”和“b”的字符串。将给定的字符串转换为没有“ab”子字符串的字符串。为了使字符串“ab”自由，我们可以执行一个操作，其中我们选择一个“ab”子字符串并用“bba”替换它。
求转换给定字符串所需的操作总数。
**例:**

```
Input : s = 'abbaa'
Output : 2
Explanation:
Here, ['ab'baa] is replaced s = [bbabaa]
[bb'ab'aa] is replaced s = [bbbbaaa]
which is ab free. Hence, 2 operations required.

Input : s = 'aab'
Output : 3
Explanation:
Here, [a'ab'] is replaced s = [abba]
['ab'ba] is replaced s = [bbaba]
[bb'ab'a] is replaced s = [bbbbaa]
which is ab free. Hence, 3 operations required.
```

**进场:**
最终状态会是某个字符‘a’在‘b’之后:**“BBB…baaa…a”**
很明显证明所有的‘b’都是彼此有区别的(即每个‘b’在初始状态下，会在最终状态加上一些‘b’与其他‘b’不相交)。对于初始状态的字符“b”，在看到字符“a”后会加倍。对于每个*I*-第 b 个字符，考虑 t <sub>i</sub> 之前的 a 的数字。所以 b 的最终个数可以定义为 2^t <sub>i</sub> 的和。
以下是上述办法的实施情况。

## C++

```
// C++ program to find all subsets of given set. Any
// repeated subset is considered only once in the output
#include<bits/stdc++.h>
using namespace std;

// code to make 'ab' free string
int abFree(string s)
{
    int n = s.length();
    char char_array[n + 1];

    // convert string into char array
    strcpy(char_array, s.c_str());

    // Traverse from end. Keep track of count
    // b's. For every 'a' encountered, add b_count
    // to result and double b_count.
    int b_count = 0;
    int res = 0;
    for (int i = 0; i < n; i++)
    {
        if (char_array[n - i - 1] == 'a')
        {
            res = (res + b_count);
            b_count = (b_count * 2);
        } else {
            b_count += 1;
        }
    }
    return res;
}

// Driver code
int main()
{
    string s = "abbaa";
    cout<<abFree(s)<<endl;

    s = "aab";
    cout<<abFree(s)<<endl;

    s = "ababab";
    cout<<abFree(s)<<endl;

    return 0;
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find all subsets of given set. Any
// repeated subset is considered only once in the output
import java.util.*;

class GFG
{

    // code to make 'ab' free string
    static int abFree(char[] s)
    {

        // Traverse from end. Keep track of count
        // b's. For every 'a' encountered, add b_count
        // to result and double b_count.
        int b_count = 0;
        int res = 0;
        for (int i = 0; i < s.length; i++)
        {
            if (s[s.length - i - 1] == 'a')
            {
                res = (res + b_count);
                b_count = (b_count * 2);
            } else {
                b_count += 1;
            }
        }
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {
        String s = "abbaa";
        System.out.println(abFree(s.toCharArray()));

        s = "aab";
        System.out.println(abFree(s.toCharArray()));

        s = "ababab";
        System.out.println(abFree(s.toCharArray()));
    }
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# code to make 'ab' free string
def abFree(s):

    # Traverse from end. Keep track of count
    # b's. For every 'a' encountered, add b_count
    # to result and double b_count.
    b_count = 0
    res = 0
    for i in range(len(s)):
        if s[~i] == 'a':
            res = (res + b_count)
            b_count  = (b_count  * 2)
        else:
            b_count  += 1
    return res

# driver code
s = 'abbaa'
print(abFree(s))

s = 'aab'
print(abFree(s))

s ='ababab'
print(abFree(s))
```

## C#

```
// C# program to find all subsets of given set.
// Any repeated subset is considered
// only once in the output
using System;
using System.Collections.Generic;

class GFG
{

    // code to make 'ab' free string
    static int abFree(char[] s)
    {

        // Traverse from end. Keep track of count
        // b's. For every 'a' encountered, add b_count
        // to result and double b_count.
        int b_count = 0;
        int res = 0;
        for (int i = 0; i < s.Length; i++)
        {
            if (s[s.Length - i - 1] == 'a')
            {
                res = (res + b_count);
                b_count = (b_count * 2);
            } else
            {
                b_count += 1;
            }
        }
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String s = "abbaa";
        Console.WriteLine(abFree(s.ToCharArray()));

        s = "aab";
        Console.WriteLine(abFree(s.ToCharArray()));

        s = "ababab";
        Console.WriteLine(abFree(s.ToCharArray()));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript program to find
// all subsets of given set. Any
// repeated subset is considered
// only once in the output

// code to make 'ab' free string
function abFree(s)
{
    var n = s.length;

    // convert string into char array
    var char_array = s.split('')

    // Traverse from end. Keep track of count
    // b's. For every 'a' encountered, add b_count
    // to result and double b_count.
    var b_count = 0;
    var res = 0;
    for (var i = 0; i < n; i++)
    {
        if (char_array[n - i - 1] == 'a')
        {
            res = (res + b_count);
            b_count = (b_count * 2);
        } else {
            b_count += 1;
        }
    }
    return res;
}

// Driver code
var s = "abbaa";
document.write( abFree(s) + "<br>");

s = "aab";
document.write( abFree(s) + "<br>");

s = "ababab";
document.write( abFree(s) + "<br>");

</script>
```

**输出:**

```
2
3
11
```