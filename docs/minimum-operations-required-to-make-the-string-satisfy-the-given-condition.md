# 使管柱满足给定条件所需的最小操作数

> 原文:[https://www . geeksforgeeks . org/制造满足给定条件的字符串所需的最小操作数/](https://www.geeksforgeeks.org/minimum-operations-required-to-make-the-string-satisfy-the-given-condition/)

给定一个字符串 **str** ，任务是以给定的最少操作数，使字符串在同一字符处开始和结束。在一次操作中，可以删除字符串中的任何字符。**注意**结果字符串的长度必须大于 **1** ，并且不可能打印 **-1** 。
**举例:**

> **输入:** str = "geeksforgeeks"
> **输出:** 3
> 去掉第一个和最后两个字符
> 字符串变成
> **输入:** str = "abcda"
> **输出:** 0

**方法:**如果字符串需要在一个字符处开始和结束，比如说 **ch** ，那么最佳的方法是删除第一次出现 **ch** 之前的所有字符和最后一次出现 **ch** 之后的所有字符。从 **'a'** 到 **'z'** 找到 **ch** 每个可能值需要删除的字符数，选择删除操作次数最少的一个。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MAX = 26;

// Function to return the minimum
// operations required
int minOperation(string str, int len)
{

    // To store the first and the last
    // occurrence of all the characters
    int first[MAX], last[MAX];

    // Set the first and the last occurrence
    // of all the characters to -1
    for (int i = 0; i < MAX; i++) {
        first[i] = -1;
        last[i] = -1;
    }

    // Update the occurrences of the characters
    for (int i = 0; i < len; i++) {

        int index = (str[i] - 'a');

        // Only set the first occurrence if
        // it hasn't already been set
        if (first[index] == -1)
            first[index] = i;

        last[index] = i;
    }

    // To store the minimum operations
    int minOp = -1;

    for (int i = 0; i < MAX; i++) {

        // If the frequency of the current
        // character in the string
        // is less than 2
        if (first[i] == -1 || first[i] == last[i])
            continue;

        // Count of characters to be
        // removed so that the string
        // starts and ends at the
        // current character
        int cnt = len - (last[i] - first[i] + 1);

        if (minOp == -1 || cnt < minOp)
            minOp = cnt;
    }

    return minOp;
}

// Driver code
int main()
{
    string str = "abcda";
    int len = str.length();

    cout << minOperation(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    final static int MAX = 26;

    // Function to return the minimum
    // operations required
    static int minOperation(String str, int len)
    {

        // To store the first and the last
        // occurrence of all the characters
        int first[] = new int[MAX];
        int last[] = new int[MAX];

        // Set the first and the last occurrence
        // of all the characters to -1
        for (int i = 0; i < MAX; i++)
        {
            first[i] = -1;
            last[i] = -1;
        }

        // Update the occurrences of the characters
        for (int i = 0; i < len; i++)
        {
            int index = (str.charAt(i) - 'a');

            // Only set the first occurrence if
            // it hasn't already been set
            if (first[index] == -1)
                first[index] = i;

            last[index] = i;
        }

        // To store the minimum operations
        int minOp = -1;

        for (int i = 0; i < MAX; i++)
        {

            // If the frequency of the current
            // character in the string
            // is less than 2
            if (first[i] == -1 ||
                first[i] == last[i])
                continue;

            // Count of characters to be
            // removed so that the string
            // starts and ends at the
            // current character
            int cnt = len - (last[i] - first[i] + 1);

            if (minOp == -1 || cnt < minOp)
                minOp = cnt;
        }
        return minOp;
    }

    // Driver code
    public static void main (String[] args)
    {
        String str = "abcda";
        int len = str.length();

        System.out.println(minOperation(str, len));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python implementation of the approach
MAX = 26;

# Function to return the minimum
# operations required
def minOperation(str, len):

    # To store the first and the last
    # occurrence of all the characters
    first, last = [0] * MAX, [0] * MAX;

    # Set the first and the last occurrence
    # of all the characters to -1
    for i in range(MAX):
        first[i] = -1;
        last[i] = -1;

    # Update the occurrences of the characters
    for i in range(len):

        index = (ord(str[i]) - ord('a'));

        # Only set the first occurrence if
        # it hasn't already been set
        if (first[index] == -1):
            first[index] = i;

        last[index] = i;

    # To store the minimum operations
    minOp = -1;

    for i in range(MAX):

        # If the frequency of the current
        # character in the string
        # is less than 2
        if (first[i] == -1 or first[i] == last[i]):
            continue;

        # Count of characters to be
        # removed so that the string
        # starts and ends at the
        # current character
        cnt = len - (last[i] - first[i] + 1);

        if (minOp == -1 or cnt < minOp):
            minOp = cnt;
    return minOp;

# Driver code
str = "abcda";
len = len(str);

print( minOperation(str, len));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    readonly static int MAX = 26;

    // Function to return the minimum
    // operations required
    static int minOperation(String str, int len)
    {

        // To store the first and the last
        // occurrence of all the characters
        int []first = new int[MAX];
        int []last = new int[MAX];

        // Set the first and the last occurrence
        // of all the characters to -1
        for (int i = 0; i < MAX; i++)
        {
            first[i] = -1;
            last[i] = -1;
        }

        // Update the occurrences of the characters
        for (int i = 0; i < len; i++)
        {
            int index = (str[i] - 'a');

            // Only set the first occurrence if
            // it hasn't already been set
            if (first[index] == -1)
                first[index] = i;

            last[index] = i;
        }

        // To store the minimum operations
        int minOp = -1;

        for (int i = 0; i < MAX; i++)
        {

            // If the frequency of the current
            // character in the string
            // is less than 2
            if (first[i] == -1 ||
                first[i] == last[i])
                continue;

            // Count of characters to be
            // removed so that the string
            // starts and ends at the
            // current character
            int cnt = len - (last[i] - first[i] + 1);

            if (minOp == -1 || cnt < minOp)
                minOp = cnt;
        }
        return minOp;
    }

    // Driver code
    public static void Main (String[] args)
    {
        String str = "abcda";
        int len = str.Length;

        Console.WriteLine(minOperation(str, len));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 26;

// Function to return the minimum
// operations required
function minOperation(str, len)
{

    // To store the first and the last
    // occurrence of all the characters
    var first = Array(MAX).fill(-1);
    var last = Array(MAX).fill(-1);

    // Update the occurrences of the characters
    for (var i = 0; i < len; i++) {

        var index = (str[i].charCodeAt(0) - 'a'.charCodeAt(0));

        // Only set the first occurrence if
        // it hasn't already been set
        if (first[index] == -1)
            first[index] = i;

        last[index] = i;
    }

    // To store the minimum operations
    var minOp = -1;

    for (var i = 0; i < MAX; i++) {

        // If the frequency of the current
        // character in the string
        // is less than 2
        if (first[i] == -1 || first[i] == last[i])
            continue;

        // Count of characters to be
        // removed so that the string
        // starts and ends at the
        // current character
        var cnt = len - (last[i] - first[i] + 1);

        if (minOp == -1 || cnt < minOp)
            minOp = cnt;
    }

    return minOp;
}

// Driver code
var str = "abcda";
var len = str.length;
document.write( minOperation(str, len));

</script>
```

**Output:** 

```
0
```