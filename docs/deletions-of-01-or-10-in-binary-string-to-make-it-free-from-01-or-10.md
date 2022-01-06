# 删除二进制字符串中的“01”或“10”，使其不含“01”或“10”

> 原文:[https://www . geesforgeks . org/删除二进制字符串中的-01 或-10，使其免于-01 或-10/](https://www.geeksforgeeks.org/deletions-of-01-or-10-in-binary-string-to-make-it-free-from-01-or-10/)

给定一个二进制字符串 **str** ，任务是找到子字符串**“01”**或**“10”**从字符串中删除的计数，以便给定的字符串没有这些子字符串。打印最小删除数量。
**举例:**

> **输入:** str = "11010"
> **输出:** 2
> 结果字符串将为“1”
> **输入:** str = "1000101"
> **输出:** 3
> 结果字符串，str = "0"

**方式:**我们正在删除**【01】**和**【10】**，二进制字符串只包含字符**【0】**和**【1】**。因此，最小删除次数将等于“0”和“1”的最小计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of deletions
// of sub-strings "01" or "10"
int substrDeletion(string str, int len)
{

    // To store the count of 0s and 1s
    int count0 = 0, count1 = 0;

    for (int i = 0; i < len; i++) {
        if (str[i] == '0')
            count0++;
        else
            count1++;
    }

    return min(count0, count1);
}

// Driver code
int main()
{
    string str = "010";
    int len = str.length();
    cout << substrDeletion(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count of deletions
// of sub-strings "01" or "10"
static int substrDeletion(String str, int len)
{

    // To store the count of 0s and 1s
    int count0 = 0, count1 = 0;

    for (int i = 0; i < len; i++)
    {
        if (str.charAt(i) == '0')
            count0++;
        else
            count1++;
    }

    return Math.min(count0, count1);
}

// Driver code
public static void main(String[] args)
{
    String str = "010";
    int len = str.length();
    System.out.println(substrDeletion(str, len));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# deletions of sub-strings "01" or "10"
def substrDeletion(string, length) :

    # To store the count of 0s and 1s
    count0 = 0;
    count1 = 0;

    for i in range(length) :
        if (string[i] == '0') :
            count0 += 1;
        else :
            count1 += 1;

    return min(count0, count1);

# Driver code
if __name__ == "__main__" :

    string = "010";
    length = len(string);

    print(substrDeletion(string, length));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of deletions
// of sub-strings "01" or "10"
static int substrDeletion(string str, int len)
{

    // To store the count of 0s and 1s
    int count0 = 0, count1 = 0;

    for (int i = 0; i < len; i++)
    {
        if (str[i] == '0')
            count0++;
        else
            count1++;
    }

    return Math.Min(count0, count1);
}

// Driver code
public static void Main()
{
    string str = "010";
    int len = str.Length;
    Console.Write(substrDeletion(str, len));
}
}

// This code is contributed by Ita_c.
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count of deletions
// of sub-strings "01" or "10"
function substrDeletion(str,len)
{
    // To store the count of 0s and 1s
    let count0 = 0, count1 = 0;

    for (let i = 0; i < len; i++)
    {
        if (str[i] == '0')
            count0++;
        else
            count1++;
    }

    return Math.min(count0, count1);
}

// Driver code
let str = "010";
let len = str.length;
document.write(substrDeletion(str, len));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
1
```