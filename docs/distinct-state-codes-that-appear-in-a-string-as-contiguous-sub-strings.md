# 作为连续子串出现在串中的不同状态代码

> 原文:[https://www . geesforgeks . org/distinct-state-codes-in-string-as-continuous-sub-strings/](https://www.geeksforgeeks.org/distinct-state-codes-that-appear-in-a-string-as-contiguous-sub-strings/)

每个状态都由长度为 2 的字符串表示。例如 **DL** 用于**德里**、 **HP** 用于**喜马偕尔邦**、 **UP** 用于**北方邦**、 **PB** 用于**旁遮普**等。
给定一个仅由大写英文字母组成的字符串 **str** ，任务是找出作为连续子字符串出现在字符串中的不同状态代码的数量。
**例:**

> **输入:**str = " upbcc "
> T3】输出: 4
> UP、PB、BR 和 RC 是 4 个不同的状态码，以连续的子串形式出现在串中。
> **输入:** str = "UPUP"
> **输出:** 2
> UP 和 PU 是给定字符串中出现的唯一状态码。

**方法:**将长度为 2 的每个子串存储在[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，并最终返回集合的大小，该大小是作为子串出现在给定串中的不同状态码的所需数量。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// distinct state codes
int countDistinctCode(string str)
{
    set<string> codes;
    for (int i = 0; i < str.length() - 1; i++)

        // Insert every sub-string
        // of length 2 in the set
        codes.insert(str.substr(i, 2));

    // Return the size of the set
    return codes.size();
}

// Driver code
int main()
{
    string str = "UPUP";
    cout << countDistinctCode(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
import java.util.*;

class GFG
{

// Function to return the count of
// distinct state codes
static int countDistinctCode(String str)
{
    Set<String> codes = new HashSet<>();
    for (int i = 0; i < str.length() - 1; i++)

        // Insert every sub-String
        // of length 2 in the set
        codes.add(str.substring(i, i + 2));

    // Return the size of the set
    return codes.size();
}

// Driver code
public static void main(String[] args)
{
    String str = "UPUP";
    System.out.println(countDistinctCode(str));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# distinct state codes
def countDistinctCode(string):

    codes = set()
    for i in range(0, len(string) - 1):

        # Insert every sub-string
        # of length 2 in the set
        codes.add(string[i:i + 2])

    # Return the size of the set
    return len(codes)

# Driver code
if __name__ == "__main__":

    string = "UPUP"
    print(countDistinctCode(string))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of the above approach.
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the count of
// distinct state codes
static int countDistinctCode(String str)
{
    HashSet<String> codes = new HashSet<String>();
    for (int i = 0; i < str.Length - 1; i++)

        // Insert every sub-String
        // of length 2 in the set
        codes.Add(str.Substring(i,2));

    // Return the size of the set
    return codes.Count;
}

// Driver code
public static void Main(String []args)
{
    String str = "UPUP";
    Console.Write(countDistinctCode(str));
}
}

// This code has been contributed by Arnab Kundu
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Function to return the count of
// distinct state codes
function countDistinctCode(str)
{
    var codes = new Set();
    for (var i = 0; i < str.length - 1; i++)

        // Insert every sub-string
        // of length 2 in the set
        codes.add(str.substr(i, 2));

    // Return the size of the set
    return codes.size;
}

// Driver code
var str = "UPUP";
document.write(countDistinctCode(str))

// This code is contributed by ShubhamSingh10
</script>
```

**Output:** 

```
2
```