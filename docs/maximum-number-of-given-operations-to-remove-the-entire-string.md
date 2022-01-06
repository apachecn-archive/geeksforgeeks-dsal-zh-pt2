# 移除整个管柱的最大给定操作次数

> 原文:[https://www . geesforgeks . org/移除整个字符串的最大给定操作数/](https://www.geeksforgeeks.org/maximum-number-of-given-operations-to-remove-the-entire-string/)

给定一个包含小写英文字符的字符串 **str** ，我们可以对给定的字符串执行以下两个操作:

1.  删除整个字符串。
2.  仅当字符串**字符串【0…I】**等于子字符串**字符串[(I+1)……(2 * I+1)]**时，删除该字符串的前缀。

任务是找到删除整个字符串所需的最大操作数。

**示例:**

> **输入:**str = " ababab "
> **输出:** 4
> 操作 1:删除前缀“ab”，字符串变为“ababab”。
> 操作二:删除前缀“ab”，字符串变成“abab”。
> 操作 3:删除前缀“ab”，str =“ab”。
> 操作 4:删除整个字符串。
> 
> **输入:**s = " ABC "
> T3】输出: 1

**方法:**为了使操作次数最大化，要删除的前缀必须是最小长度的，即从单个字符开始，逐个追加连续的字符，找到满足给定条件的最小长度前缀。需要一个操作来删除这个前缀，比如 str[0…i]，然后递归调用同一个函数来找到子字符串 str[i+1…2*i+1]的结果。如果没有可以删除的前缀，那么返回 1，因为唯一可能的操作是删除整个字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the maximum number
// of given operations required to
// remove the given string entirely
int find(string s)
{

    // If length of the string is zero
    if (s.length() == 0)
        return 0;

    // Single operation can delete the entire string
    int c = 1;

    // To store the prefix of the string
    // which is to be deleted
    string d = "";

    for (int i = 0; i < s.length(); i++) {

        // Prefix s[0..i]
        d += s[i];

        // To store the substring s[i+1...2*i+1]
        string s2 = s.substr(i + 1, d.length());

        // If the prefix s[0...i] can be deleted
        if (s2 == d) {

            // 1 operation to remove the current prefix
            // and then recursively find the count of
            // operations for the substring s[i+1...n-1]
            c = 1 + find(s.substr(i + 1));
            break;
        }
    }

    // Entire string has to be deleted
    return c;
}

// Driver code
int main()
{
    string s = "abababab";

    cout << find(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// Function to return the maximum number
// of given operations required to
// remove the given string entirely
static int find(String s)
{

    // If length of the string is zero
    if (s.length() == 0)
        return 0;

    // Single operation can delete
    // the entire string
    int c = 1;

    // To store the prefix of the string
    // which is to be deleted
    String d = "";

    for(int i = 0; i < s.length(); i++)
    {

        // Prefix s[0..i]
        d += s.charAt(i);

        // To store the substring s[i+1...2*i+1]
        String s2 = "";

        if (i + d.length() < s.length())
        {
            s2 = s.substring(i + 1,
               d.length() + (i + 1));
        }

        // If the prefix s[0...i] can be deleted
        if (s2.equals(d))
        {

            // 1 operation to remove the current prefix
            // and then recursively find the count of
            // operations for the substring s[i+1...n-1]
            c = 1 + find(s.substring(i + 1));
            break;
        }
    }

    // Entire string has to be deleted
    return c;
}

// Driver code
public static void main(String[] args)
{
    String s = "abababab";

    System.out.print(find(s));
}
}

// This code is contributed by pratham76
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum number
# of given operations required to
# remove the given entirely
def find(s):

    # If length of the is zero
    if (len(s) == 0):
        return 0

    # Single operation can delete
    # the entire string
    c = 1

    # To store the prefix of the string
    # which is to be deleted
    d = ""

    for i in range(len(s)):

        # Prefix s[0..i]
        d += s[i]

        # To store the subs[i+1...2*i+1]
        s2 = s[i + 1:i + 1 + len(d)]

        # If the prefix s[0...i] can be deleted
        if (s2 == d):

            # 1 operation to remove the current prefix
            # and then recursively find the count of
            # operations for the subs[i+1...n-1]
            c = 1 + find(s[i + 1:])
            break

    # Entire has to be deleted
    return c

# Driver code
s = "abababab"
print(find(s))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG{

// Function to return the maximum number
// of given operations required to
// remove the given string entirely
static int find(string s)
{

    // If length of the string is zero
    if (s.Length == 0)
        return 0;

    // Single operation can delete the entire string
    int c = 1;

    // To store the prefix of the string
    // which is to be deleted
    string d = "";

    for (int i = 0; i < s.Length; i++)
    {

        // Prefix s[0..i]
        d += s[i];

        // To store the substring s[i+1...2*i+1]
       string s2 = "";
       if(i + d.Length < s.Length)
       {
           s2 = s.Substring(i + 1, d.Length);
       }

       // If the prefix s[0...i] can be deleted
       if (s2 == d)
       {
            // 1 operation to remove the current prefix
            // and then recursively find the count of
            // operations for the substring s[i+1...n-1]
            c = 1 + find(s.Substring(i + 1));
            break;
       }
    }

    // Entire string has to be deleted
    return c;
}

    // Driver code
    public static void Main(string[] args)
    {
       string s = "abababab";
       Console.Write(find(s));
    }
}

// This code is contributed by rutvik
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum number
// of given operations required to
// remove the given string entirely
function find(s)
{

    // If length of the string is zero
    if (s.length == 0)
        return 0;

    // Single operation can delete the entire string
    var c = 1;

    // To store the prefix of the string
    // which is to be deleted
    var d = "";

    for (var i = 0; i < s.length; i++) {

        // Prefix s[0..i]
        d += s[i];

        // To store the substring s[i+1...2*i+1]
        var s2 = s.substring(i + 1, i+ 1+d.length);

        // If the prefix s[0...i] can be deleted
        if (s2 == d) {

            // 1 operation to remove the current prefix
            // and then recursively find the count of
            // operations for the substring s[i+1...n-1]
            c = 1 + find(s.substring(i + 1));
            break;
        }
    }

    // Entire string has to be deleted
    return c;
}

// Driver code
var s = "abababab";
document.write( find(s));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
4
```