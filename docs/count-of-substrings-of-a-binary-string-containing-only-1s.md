# 仅包含 1 的二进制字符串的子字符串计数

> 原文:[https://www . geesforgeks . org/count-of-substrings-of-a-binary-string-only-1s/](https://www.geeksforgeeks.org/count-of-substrings-of-a-binary-string-containing-only-1s/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)，我们需要找出这个字符串有多少子字符串只包含 1。

**示例:**

> **输入:** S = "0110111"
> **输出:** 9
> **说明:**
> 有 9 个只有 1 个 S 字符的子串。
> “1”出现 5 次。
> “11”来了 3 次。
> “111”来 1 次。
> 
> **输入:**S = " 000 "
> T3】输出: 0

**逼近**:思路是遍历二进制串，统计串中连续的。以下是该方法的示例:

*   遍历给定的二进制字符串，从索引 0 到长度–1
*   计算索引 I 前连续“1”的数量。
*   对于每个新字符串[i]，将会有更多子字符串，所有字符都为“1”

下面是上述方法的实现:

## C++

```
// C++ implementation to find
// count of substring containing
// only ones

#include <bits/stdc++.h>
using namespace std;

// Function to find the total number
// of substring having only ones
int countOfSubstringWithOnlyOnes(string s)
{
    int res = 0, count = 0;
    for (int i = 0; i < s.length(); i++) {
    count = s[i] == '1' ? count + 1 : 0;
    res = (res + count);
    }
    return res;
}

// Driver Code
int main()
{
    string s = "0110111";
    cout << countOfSubstringWithOnlyOnes(s)
        << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// count of substring containing
// only ones
class GFG{

// Function to find the total number
// of substring having only ones
static int countOfSubstringWithOnlyOnes(String s)
{
    int res = 0, count = 0;
    for(int i = 0; i < s.length(); i++)
    {
        count = s.charAt(i) == '1' ? count + 1 : 0;
        res = (res + count);
    }
    return res;
}

// Driver code
public static void main(String[] args)
{
    String s = "0110111";

    System.out.println(countOfSubstringWithOnlyOnes(s));
}
}

// This code is contributed by dewantipandeydp
```

## 蟒蛇 3

```
# Python3 implementation to find
# count of substring containing
# only ones

# Function to find the total number
# of substring having only ones
def countOfSubstringWithOnlyOnes(s):

    count = 0
    res = 0

    for i in range(0,len(s)):
        if s[i] == '1':
            count = count + 1
        else:
            count = 0;

        res = res + count

    return res

# Driver Code
s = "0110111"
print(countOfSubstringWithOnlyOnes(s))

# This code is contributed by jojo9911
```

## C#

```
// C# implementation to find count
// of substring containing only ones
using System;

class GFG{

// Function to find the total number
// of substring having only ones
static int countOfSubstringWithOnlyOnes(string s)
{
    int res = 0, count = 0;

    for(int i = 0; i < s.Length; i++)
    {
        count = s[i] == '1' ? count + 1 : 0;
        res = (res + count);
    }
    return res;
}

// Driver code
public static void Main(string[] args)
{
    string s = "0110111";

    Console.Write(countOfSubstringWithOnlyOnes(s));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to find
// count of substring containing
// only ones

// Function to find the total number
// of substring having only ones
function countOfSubstringWithOnlyOnes(s)
{
    var res = 0, count = 0;
    for (var i = 0; i < s.length; i++) {
    count = s[i] == '1' ? count + 1 : 0;
    res = (res + count);
    }
    return res;
}

// Driver Code
var s = "0110111";
document.write( countOfSubstringWithOnlyOnes(s));

</script>
```

**Output**

```
9
```