# 按升序对二进制字符串排序时需要删除的最少字符数

> 原文:[https://www . geeksforgeeks . org/最小字符-要求删除-排序-二进制-字符串升序/](https://www.geeksforgeeks.org/minimum-characters-required-to-be-removed-to-sort-binary-string-in-ascending-order/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **字符串**，任务是从给定的二进制字符串中移除最小数量的字符，使得剩余字符串中的字符形成排序顺序。

**示例:**

> **输入:** str = "1000101"
> **输出:** 2
> **解释:**
> 删除前两次出现的‘1’将字符串修改为“00001”，这是一个排序顺序。
> 因此，要删除的最小字符数为 2。
> 
> **输入:** str = "001111"
> **输出:** 0
> **说明:**
> 字符串已经排序。
> 因此，要删除的字符的最小计数为 0。

**方法:**思路是统计[最后一次出现 **0**](https://www.geeksforgeeks.org/python-find-last-occurrence-of-substring/) 之前的 **1** 的个数，以及第一次出现 1 之后的 0 的个数。两个计数中的最小值是需要删除的字符数。以下是步骤:

1.  [遍历串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **串**找到第一个出现的 **1** 和最后一个出现的 **0** 的位置。
2.  如果**字符串**只有一种字符类型，则打印 **0** 。
3.  现在，计算最后一次出现 **0** 之前出现的 **1** 的数量，并存储在一个变量中，比如 **cnt1** 。
4.  现在，在一个变量中计算第一次出现 **1** 后出现的 **0** 的数量，比如说 **cnt0** 。
5.  打印 **cnt0** 和 **cnt1** 的最小值，作为需要删除的最小字符数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count
// of characters to be removed to make
// the string sorted in ascending order
int minDeletion(string str)
{

    // Length of given string
    int n = str.length();

    // Stores the first
    // occurrence of '1'
    int firstIdx1 = -1;

    // Stores the last
    // occurrence of '0'
    int lastIdx0 = -1;

    // Traverse the string to find
    // the first occurrence of '1'
    for(int i = 0; i < n; i++)
    {
        if (str[i] == '1')
        {
            firstIdx1 = i;
            break;
        }
    }

    // Traverse the string to find
    // the last occurrence of '0'
    for(int i = n - 1; i >= 0; i--)
    {
        if (str[i] == '0')
        {
            lastIdx0 = i;
            break;
        }
    }

    // Return 0 if the str have
    // only one type of character
    if (firstIdx1 == -1 ||
         lastIdx0 == -1)
        return 0;

    // Initialize count1 and count0 to
    // count '1's before lastIdx0
    // and '0's after firstIdx1
    int count1 = 0, count0 = 0;

    // Traverse the string to count0
    for(int i = 0; i < lastIdx0; i++)
    {
        if (str[i] == '1')
        {
            count1++;
        }
    }

    // Traverse the string to count1
    for(int i = firstIdx1 + 1; i < n; i++)
    {
        if (str[i] == '1')
        {
            count0++;
        }
    }

    // Return the minimum of
    // count0 and count1
    return min(count0, count1);
}

// Driver code
int main()
{

    // Given string str
    string str = "1000101";

    // Function call
    cout << minDeletion(str);

    return 0;
}

// This code is contributed by bikram2001jha
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to find the minimum count
    // of characters to be removed to make
    // the string sorted in ascending order
    static int minDeletion(String str)
    {

        // Length of given string
        int n = str.length();

        // Stores the first
        // occurrence of '1'
        int firstIdx1 = -1;

        // Stores the last
        // occurrence of '0'
        int lastIdx0 = -1;

        // Traverse the string to find
        // the first occurrence of '1'
        for (int i = 0; i < n; i++) {

            if (str.charAt(i) == '1') {

                firstIdx1 = i;
                break;
            }
        }

        // Traverse the string to find
        // the last occurrence of '0'
        for (int i = n - 1; i >= 0; i--) {

            if (str.charAt(i) == '0') {

                lastIdx0 = i;
                break;
            }
        }

        // Return 0 if the str have
        // only one type of character
        if (firstIdx1 == -1
            || lastIdx0 == -1)
            return 0;

        // Initialize count1 and count0 to
        // count '1's before lastIdx0
        // and '0's after firstIdx1
        int count1 = 0, count0 = 0;

        // Traverse the string to count0
        for (int i = 0; i < lastIdx0; i++) {

            if (str.charAt(i) == '1') {

                count1++;
            }
        }

        // Traverse the string to count1
        for (int i = firstIdx1 + 1; i < n; i++) {

            if (str.charAt(i) == '1') {

                count0++;
            }
        }

        // Return the minimum of
        // count0 and count1
        return Math.min(count0, count1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given string str
        String str = "1000101";

        // Function Call
        System.out.println(minDeletion(str));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum count
# of characters to be removed to make
# the string sorted in ascending order
def minDeletion(s):

    # Length of given string
    n = len(s)

    # Stores the first
    # occurrence of '1'
    firstIdx1 = -1

    # Stores the last
    # occurrence of '0'
    lastIdx0 = -1

    # Traverse the string to find
    # the first occurrence of '1'
    for i in range(0, n):
        if (str[i] == '1'):
            firstIdx1 = i
            break

    # Traverse the string to find
    # the last occurrence of '0'
    for i in range(n - 1, -1, -1):
        if (str[i] == '0'):
            lastIdx0 = i
            break

    # Return 0 if the str have
    # only one type of character
    if (firstIdx1 == -1 or
         lastIdx0 == -1):
        return 0

    # Initialize count1 and count0 to
    # count '1's before lastIdx0
    # and '0's after firstIdx1
    count1 = 0
    count0 = 0

    # Traverse the string to count0
    for i in range(0, lastIdx0):
        if (str[i] == '1'):
            count1 += 1

    # Traverse the string to count1
    for i in range(firstIdx1 + 1, n):
        if (str[i] == '1'):
            count0 += 1

    # Return the minimum of
    # count0 and count1
    return min(count0, count1)

# Driver code

# Given string str
str = "1000101"

# Function call
print(minDeletion(str))

# This code is contributed by Stream_Cipher
```

## C#

```
// C# program for the above approach
using System.Collections.Generic;
using System;

class GFG{

// Function to find the minimum count
// of characters to be removed to make
// the string sorted in ascending order
static int minDeletion(string str)
{

    // Length of given string
    int n = str.Length;

    // Stores the first
    // occurrence of '1'
    int firstIdx1 = -1;

    // Stores the last
    // occurrence of '0'
    int lastIdx0 = -1;

    // Traverse the string to find
    // the first occurrence of '1'
    for(int i = 0; i < n; i++)
    {
        if (str[i] == '1')
        {
            firstIdx1 = i;
            break;
        }
    }

    // Traverse the string to find
    // the last occurrence of '0'
    for(int i = n - 1; i >= 0; i--)
    {
        if (str[i] == '0')
        {
            lastIdx0 = i;
            break;
        }
    }

    // Return 0 if the str have
    // only one type of character
    if (firstIdx1 == -1 ||
         lastIdx0 == -1)
        return 0;

    // Initialize count1 and count0 to
    // count '1's before lastIdx0
    // and '0's after firstIdx1
    int count1 = 0, count0 = 0;

    // Traverse the string to count0
    for(int i = 0; i < lastIdx0; i++)
    {
        if (str[i] == '1')
        {
            count1++;
        }
    }

    // Traverse the string to count1
    for(int i = firstIdx1 + 1; i < n; i++)
    {
        if (str[i] == '1')
        {
            count0++;
        }
    }

    // Return the minimum of
    // count0 and count1
    return Math.Min(count0, count1);
}

// Driver Code
public static void Main()
{

    // Given string str
    string str = "1000101";

    // Function call
    Console.WriteLine(minDeletion(str));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the minimum count
// of characters to be removed to make
// the string sorted in ascending order
function minDeletion(str)
{

    // Length of given string
    let n = str.length;

    // Stores the first
    // occurrence of '1'
    let firstIdx1 = -1;

    // Stores the last
    // occurrence of '0'
    let lastIdx0 = -1;

    // Traverse the string to find
    // the first occurrence of '1'
    for(let i = 0; i < n; i++)
    {
        if (str[i] == '1')
        {
            firstIdx1 = i;
            break;
        }
    }

    // Traverse the string to find
    // the last occurrence of '0'
    for(let i = n - 1; i >= 0; i--)
    {
        if (str[i] == '0')
        {
            lastIdx0 = i;
            break;
        }
    }

    // Return 0 if the str have
    // only one type of character
    if (firstIdx1 == -1 ||
         lastIdx0 == -1)
        return 0;

    // Initialize count1 and count0 to
    // count '1's before lastIdx0
    // and '0's after firstIdx1
    let count1 = 0, count0 = 0;

    // Traverse the string to count0
    for(let i = 0; i < lastIdx0; i++)
    {
        if (str[i] == '1')
        {
            count1++;
        }
    }

    // Traverse the string to count1
    for(let i = firstIdx1 + 1; i < n; i++)
    {
        if (str[i] == '1')
        {
            count0++;
        }
    }

    // Return the minimum of
    // count0 and count1
    return Math.min(count0, count1);
}

// Driver code

    // Given string str
    let str = "1000101";

    // Function call
    document.write(minDeletion(str));

// This code is contributed by target_2.
</script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)