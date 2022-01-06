# 给定字符串中的双音素子串的计数

> 原文:[https://www . geeksforgeeks . org/从给定字符串计算二进制子字符串数/](https://www.geeksforgeeks.org/count-of-bitonic-substrings-from-the-given-string/)

给定一个字符串 **str** ，任务是统计给定字符串的所有二进制子字符串。

> 一个**双音素子串**是给定字符串的一个子串，其中的元素要么严格递增要么严格递减，要么先递增后递减。

**示例:**

> **输入:** str = "bade"
> **输出:** 8
> **解释:**
> 长度为 1 的子串总是双音素的，“b”、“a”、“d”、“e”
> 长度为 2 的子串是“ba”、“ad”、“de”，这些也都是双音素的，因为它们只是在增加或减少。
> 长度为 3 的子串是“坏”和“ade”，其中“ade”是双音素的。
> 长度为 4“bade”的子串不是双音素，因为它先减少后增加。
> 所以总共有 8 个子串是双音素的。
> 
> **输入:** str = "abc"
> **输出:** 6
> **解释:**
> 给定的字符串在增加，所以它的所有子字符串也在增加，因此是双音素的。所以总数= 6。

**方法:**想法是[生成给定字符串的所有可能的子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，并检查每个子字符串是否是双音素的。如果子字符串是 Bitonic，则增加答案的计数。最后，打印所有双离子子阵列的计数。

下面是上述方法的实现:

## C++

```
// C+++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find all the bitonic
// sub strings
void subString(char str[], int n)
{
    // Pick starting point
    int c = 0;

    // Iterate till length of the string
    for (int len = 1; len <= n; len++) {

        // Pick ending point for string
        for (int i = 0; i <= n - len; i++) {

            // Substring from i to j
            // is obtained
            int j = i + len - 1;
            char temp = str[i], f = 0;

            // Substrings of length 1
            if (j == i) {

                // Increase count
                c++;
                continue;
            }

            int k = i + 1;

            // For increasing sequence
            while (temp < str[k] && k <= j) {
                temp = str[k];
                k++;
                f = 2;
            }

            // Check for strictly increasing
            if (k > j) {

                // Increase count
                c++;
                f = 2;
            }

            // Check for decreasing sequence
            while (temp > str[k]
                   && k <= j
                   && f != 2) {
                k++;
                f = 0;
            }

            if (k > j && f != 2) {

                // Increase count
                c++;
                f = 0;
            }
        }
    }

    // Print the result
    cout << c << endl;
}

// Driver Code
int main()
{
    // Given string
    char str[] = "bade";

    // Function Call
    subString(str, strlen(str));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java+ program for the above approach
import java.util.*;

class GFG{

// Function to find all the bitonic
// sub Strings
static void subString(char str[], int n)
{

    // Pick starting point
    int c = 0;

    // Iterate till length of the String
    for(int len = 1; len <= n; len++)
    {

        // Pick ending point for String
        for(int i = 0; i <= n - len; i++)
        {

            // SubString from i to j
            // is obtained
            int j = i + len - 1;
            char temp = str[i], f = 0;

            // SubStrings of length 1
            if (j == i)
            {

                // Increase count
                c++;
                continue;
            }

            int k = i + 1;

            // For increasing sequence
            while (k < n && temp < str[k])
            {
                temp = str[k];
                k++;
                f = 2;
            }

            // Check for strictly increasing
            if (k > j)
            {

                // Increase count
                c++;
                f = 2;
            }

            // Check for decreasing sequence
            while (k < n && temp > str[k] &&
                   f != 2)
            {
                k++;
                f = 0;
            }

            if (k > j && f != 2)
            {

                // Increase count
                c++;
                f = 0;
            }
        }
    }

    // Print the result
    System.out.print(c + "\n");
}

// Driver Code
public static void main(String[] args)
{

    // Given String
    char str[] = "bade".toCharArray();

    // Function call
    subString(str, str.length);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find all the bitonic
# sub strings
def subString(str, n):

    # Pick starting po
    c = 0;

    # Iterate till length of the string
    for len in range(1, n + 1):

        # Pick ending pofor string
        for i in range(0, n - len + 1):

            # Substring from i to j
            # is obtained
            j = i + len - 1;
            temp = str[i]
            f = 0;

            # Substrings of length 1
            if (j == i):

                # Increase count
                c += 1
                continue;
            k = i + 1;

            # For increasing sequence
            while (k <= j and temp < str[k]):
                temp = str[k];
                k += 1;
                f = 2;

            # Check for strictly increasing
            if (k > j):

                # Increase count
                c += 1;
                f = 2;

            # Check for decreasing sequence
            while (k <= j and temp > str[k] and
                   f != 2):
                k += 1;
                f = 0;
            if (k > j and f != 2):

                # Increase count
                c += 1;
                f = 0;

    # Print the result
    print(c)

# Driver code

# Given string
str = "bade";

# Function Call
subString(str, len(str))

# This code is contributed by grand_master
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find all the bitonic
// sub Strings
static void subString(char []str, int n)
{

    // Pick starting point
    int c = 0;

    // Iterate till length of the String
    for(int len = 1; len <= n; len++)
    {

        // Pick ending point for String
        for(int i = 0; i <= n - len; i++)
        {

            // SubString from i to j
            // is obtained
            int j = i + len - 1;
            char temp = str[i], f = (char)0;

            // SubStrings of length 1
            if (j == i)
            {

                // Increase count
                c++;
                continue;
            }

            int k = i + 1;

            // For increasing sequence
            while (k < n && temp < str[k])
            {
                temp = str[k];
                k++;
                f = (char)2;
            }

            // Check for strictly increasing
            if (k > j)
            {

                // Increase count
                c++;
                f = (char)2;
            }

            // Check for decreasing sequence
            while (k < n && temp > str[k] &&
                f != 2)
            {
                k++;
                f = (char)0;
            }

            if (k > j && f != 2)
            {

                // Increase count
                c++;
                f = (char)0;
            }
        }
    }

    // Print the result
    Console.Write(c + "\n");
}

// Driver Code
public static void Main(String[] args)
{

    // Given String
    char []str = "bade".ToCharArray();

    // Function call
    subString(str, str.Length);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find all the bitonic
// sub strings
function subString(str, n)
{
    // Pick starting point
    var c = 0;

    // Iterate till length of the string
    for (var len = 1; len <= n; len++) {

        // Pick ending point for string
        for (var i = 0; i <= n - len; i++) {

            // Substring from i to j
            // is obtained
            var j = i + len - 1;
            var temp = str[i], f = 0;

            // Substrings of length 1
            if (j == i) {

                // Increase count
                c++;
                continue;
            }

            var k = i + 1;

            // For increasing sequence
            while (temp < str[k] && k <= j) {
                temp = str[k];
                k++;
                f = 2;
            }

            // Check for strictly increasing
            if (k > j) {

                // Increase count
                c++;
                f = 2;
            }

            // Check for decreasing sequence
            while (temp > str[k]
                   && k <= j
                   && f != 2) {
                k++;
                f = 0;
            }

            if (k > j && f != 2) {

                // Increase count
                c++;
                f = 0;
            }
        }
    }

    // Print the result
    document.write( c );
}

// Driver Code

// Given string
var str = "bade".split('');

// Function Call
subString(str, str.length);

// This code is contributed by itsok.
</script>
```

**Output:** 

```
8
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间: *O(1)*