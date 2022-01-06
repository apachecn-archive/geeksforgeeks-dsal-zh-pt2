# 给定字符串中递增子字符串的计数

> 原文:[https://www . geeksforgeeks . org/给定字符串中不断增加的子字符串数/](https://www.geeksforgeeks.org/count-of-increasing-substrings-in-given-string/)

给定长度为 **N、**的[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **字符串**，任务是[打印子字符串](https://www.geeksforgeeks.org/number-substrings-string/)的数量，其中每个字符的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)大于或等于前一个字符的 ASCII 值。子字符串的长度必须至少为 2。

**例**:

> **输入** : str = "bcdabc"
> **输出** : 6
> **解释**:字母表的 ASCII 值大于前一个字符且长度至少为 2 的 6 个子字符串是 bc、bcd、cd、ab、abc、bc
> 
> **输入** : str = "cegxza"
> **输出** : 10

**天真方法**:上面的问题可以是[迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并从每个索引开始计数递增的 ASCII 值子串。
**时间复杂度:** O(N^2)

**方法:**针对给定问题的有效方法是[迭代字符串](https://www.geeksforgeeks.org/iterate-over-the-characters-of-a-string-in-java/)并使用[数学计算](https://www.geeksforgeeks.org/c-mathematical-functions/)在更大的子字符串中找到所有可能增加的 ASCII 值[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)。按照以下方法解决问题:

*   将左和右**指针**初始化为 0****
*   初始化一个变量 **ans** 到存储答案
*   [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)直到**右侧**指针小于字符串长度:
    *   使用 [while 循环](https://www.geeksforgeeks.org/java-while-loop-with-examples/)使用**右**指针迭代，直到 **str【右】** **> = str【右–1】**和**右< str.length()**
    *   通过将初始化 **len =右-左、**相加，然后将**(len *(len+1)/2)–len**的值相加至 **ans** 来计算增加了 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)的子串[数量](https://www.geeksforgeeks.org/number-substrings-count-character-k/)
    *   使**左=右**和**右**指针将在下一次迭代中递增
*   返回**和**作为我们的结果

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number of substrings
// with increasing ascii values
int countIncSub(string str)
{

    // Initialize left and right pointers
    int left = 0, right = 1;

    // Initialize length of the string str
    int l = str.length();

    // Initialize a variable to store answer
    int ans = 0;

    // Iterate the string
    for (; right < l; right++)
    {

        // Iterate the while loop until the
        // string has increasing ASCII value
        while (right < l && str[right] >= str[right - 1])
        {

            right++;
        }

        // Calculate length of longest
        // substring found starting from left
        int len = right - left;

        // Calculate the number of substrings
        // with length at least 2 and add it
        // to the ans
        ans += (len * (len + 1)) / 2 - len;

        // Update left equal to right
        left = right;
    }

    // Return the answer
    return ans;
}

int main()
{

    // Initialize the string str
    string str = "cegxza";

    // Call the function and
    // print the result
    cout << (countIncSub(str));
}

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

// Driver code
class GFG {

    // Function to count number of substrings
    // with increasing ascii values
    public static int countIncSub(String str)
    {

        // Initialize left and right pointers
        int left = 0, right = 1;

        // Initialize length of the string str
        int l = str.length();

        // Initialize a variable to store answer
        int ans = 0;

        // Iterate the string
        for (; right < l; right++) {

            // Iterate the while loop until the
            // string has increasing ASCII value
            while (right < l
                   && str.charAt(right)
                          >= str.charAt(right - 1)) {

                right++;
            }

            // Calculate length of longest
            // substring found starting from left
            int len = right - left;

            // Calculate the number of substrings
            // with length at least 2 and add it
            // to the ans
            ans += (len * (len + 1)) / 2 - len;

            // Update left equal to right
            left = right;
        }

        // Return the answer
        return ans;
    }

    public static void main(String[] args)
    {

        // Initialize the string str
        String str = "cegxza";

        // Call the function and
        // print the result
        System.out.println(countIncSub(str));
    }
}
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to count number of substrings
# with increasing ascii values
def countIncSub(str):

    # Initialize left and right pointers
    left = 0
    right = 1

    # Initialize length of the string str
    l = len(str)

    # Initialize a variable to store answer
    ans = 0

    # Iterate the string
    for right in range(1, l):

        # Iterate the while loop until the
        # string has increasing ASCII value
        while (right < l and str[right] >= str[right - 1]):
            right += 1

        # Calculate length of longest
        # substring found starting from left
        length = right - left

        # Calculate the number of substrings
        # with length at least 2 and add it
        # to the ans
        ans += (length * (length + 1)) // 2 - length

        # Update left equal to right
        left = right

    # Return the answer
    return ans

# Driver Code
# Initialize the string str
str = "cegxza"

# Call the function and
# print the result
print(countIncSub(str))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections;

// Driver code
class GFG {

    // Function to count number of substrings
    // with increasing ascii values
    static int countIncSub(string str)
    {
        // Initialize left and right pointers
        int left = 0, right = 1;

        // Initialize length of the string str
        int l = str.Length;

        // Initialize a variable to store answer
        int ans = 0;

        // Iterate the string
        for (; right < l; right++) {

            // Iterate the while loop until the
            // string has increasing ASCII value
            while (right < l
                   && str[right]
                          >= str[right - 1]) {

                right++;
            }

            // Calculate length of longest
            // substring found starting from left
            int len = right - left;

            // Calculate the number of substrings
            // with length at least 2 and add it
            // to the ans
            ans += (len * (len + 1)) / 2 - len;

            // Update left equal to right
            left = right;
        }

        // Return the answer
        return ans;
    }

    public static void Main()
    {

        // Initialize the string str
        string str = "cegxza";

        // Call the function and
        // print the result
        Console.Write(countIncSub(str));
    }
}
// This code is contributed by Samim Hossain Mondal
```

## java 描述语言

```
<script>
// Javascript code for the above approach

// Function to count number of substrings
// with increasing ascii values
function countIncSub(str)
{

    // Initialize left and right pointers
    let left = 0, right = 1;

    // Initialize length of the string str
    let l = str.length;

    // Initialize a variable to store answer
    let ans = 0;

    // Iterate the string
    for (; right < l; right++)
    {

        // Iterate the while loop until the
        // string has increasing ASCII value
        while (right < l && str[right] >= str[right - 1])
        {

            right++;
        }

        // Calculate length of longest
        // substring found starting from left
        let len = right - left;

        // Calculate the number of substrings
        // with length at least 2 and add it
        // to the ans
        ans += (len * (len + 1)) / 2 - len;

        // Update left equal to right
        left = right;
    }

    // Return the answer
    return ans;
}

// Driver Code
// Initialize the string str
let str = "cegxza";

// Call the function and
// print the result
document.write(countIncSub(str));

// This code is contributed by Samim Hossain Mondal
</script>
```

**Output:** 

```
10
```

**时间复杂度** : O(N)
**辅助空间:** O(1)