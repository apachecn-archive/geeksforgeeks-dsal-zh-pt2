# 删除一个字符后 1 的最长子串

> 原文:[https://www . geesforgeks . org/移除一个字符后的最长 1s 子串/](https://www.geeksforgeeks.org/longest-substring-of-1s-after-removing-one-character/)

给定一个长度为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是在[从字符串](https://www.geeksforgeeks.org/stdstringerase-in-cpp/)中删除一个字符后，找到由**‘1’**S 组成的最长的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)。

**示例:**

> **输入:**S =“1101”
> T3】输出: 3
> **解释:**
> 去掉 S[0]，S 修饰为“101”。“1”的最长可能子字符串是 1。
> 去掉 S[1]，S 修饰为“101”。“1”的最长可能子字符串是 1。
> 去掉 S[2]，S 修饰为“111”。1 的最长可能子串是 3。
> 去掉 S[3]，S 修饰为“110”。“1”的最长可能子字符串是 2。
> 因此，可以得到的‘1’的最长子串是 3。
> 
> **输入:**S = " 011101101 "
> T3】输出: 5

**方法 1:** 思路是[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并在给定字符串中搜索**‘0’**s。对于每个被发现为**“0”**的字符，添加其相邻子串**“1”**的长度。打印获得的所有此类长度的最大值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the length of the
// longest substring of '1's that can be
// obtained by deleting one character
int longestSubarray(string s)
{
    // Add '0' at the end
    s += '0';

    // Iterator to traverse the string
    int i;

    // Stores maximum length
    // of required substring
    int res = 0;

    // Stores length of substring of '1'
    // preceding the current character
    int prev_one = 0;

    // Stores length of substring of '1'
    // succeeding the current character
    int curr_one = 0;

    // Counts number of '0's
    int numberOfZeros = 0;

    // Traverse the string S
    for (i = 0; i < s.length(); i++) {

        // If current character is '1'
        if (s[i] == '1') {

            // Increase curr_one by one
            curr_one += 1;
        }

        // Otherwise
        else {

            // Increment numberofZeros by one
            numberOfZeros += 1;

            // Count length of substring
            // obtained y concatenating
            // preceding and succeeding substrings of '1'
            prev_one += curr_one;

            // Store maximum size in res
            res = max(res, prev_one);

            // Assign curr_one to prev_one
            prev_one = curr_one;

            // Reset curr_one
            curr_one = 0;
        }
    }

    // If string contains only one '0'
    if (numberOfZeros == 1) {
        res -= 1;
    }

    // Return the answer
    return res;
}

// Driver Code
int main()
{
    string S = "1101";
    cout << longestSubarray(S);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.Arrays;

class GFG{

// Function to calculate the length of the
// longest substring of '1's that can be
// obtained by deleting one character
static int longestSubarray(String s)
{

    // Add '0' at the end
    s += '0';

    // Iterator to traverse the string
    int i;

    // Stores maximum length
    // of required substring
    int res = 0;

    // Stores length of substring of '1'
    // preceding the current character
    int prev_one = 0;

    // Stores length of substring of '1'
    // succeeding the current character
    int curr_one = 0;

    // Counts number of '0's
    int numberOfZeros = 0;

    // Traverse the string S
    for(i = 0; i < s.length(); i++)
    {

        // If current character is '1'
        if (s.charAt(i) == '1')
        {

            // Increase curr_one by one
            curr_one += 1;
        }

        // Otherwise
        else
        {

            // Increment numberofZeros by one
            numberOfZeros += 1;

            // Count length of substring
            // obtained y concatenating
            // preceding and succeeding
            // substrings of '1'
            prev_one += curr_one;

            // Store maximum size in res
            res = Math.max(res, prev_one);

            // Assign curr_one to prev_one
            prev_one = curr_one;

            // Reset curr_one
            curr_one = 0;
        }
    }

    // If string contains only one '0'
    if (numberOfZeros == 1)
    {
        res -= 1;
    }

    // Return the answer
    return res;
}

// Driver Code
public static void main (String[] args)
{
    String S = "1101";

    System.out.println(longestSubarray(S));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the length of the
# longest substring of '1's that can be
# obtained by deleting one character
def longestSubarray(s):

    # Add '0' at the end
    s += '0'

    # Iterator to traverse the string
    i = 0

    # Stores maximum length
    # of required substring
    res = 0

    # Stores length of substring of '1'
    # preceding the current character
    prev_one = 0

    # Stores length of substring of '1'
    # succeeding the current character
    curr_one = 0

    # Counts number of '0's
    numberOfZeros = 0

    # Traverse the string S
    for i in range(len(s)):

        # If current character is '1'
        if (s[i] == '1'):

            # Increase curr_one by one
            curr_one += 1

        # Otherwise
        else:

            # Increment numberofZeros by one
            numberOfZeros += 1

            # Count length of substring
            # obtained y concatenating
            # preceding and succeeding
            # substrings of '1'
            prev_one += curr_one

            # Store maximum size in res
            res = max(res, prev_one)

            # Assign curr_one to prev_one
            prev_one = curr_one

            # Reset curr_one
            curr_one = 0

    # If string contains only one '0'
    if (numberOfZeros == 1):
        res -= 1

    # Return the answer
    return res

# Driver Code
if __name__ == '__main__':

    S = "1101"

    print(longestSubarray(S))

# This code is contributed by ipg2016107
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Function to calculate the length of the
// longest substring of '1's that can be
// obtained by deleting one character
static int longestSubarray(String s)
{

    // Add '0' at the end
    s += '0';

    // Iterator to traverse the string
    int i;

    // Stores maximum length
    // of required substring
    int res = 0;

    // Stores length of substring of '1'
    // preceding the current character
    int prev_one = 0;

    // Stores length of substring of '1'
    // succeeding the current character
    int curr_one = 0;

    // Counts number of '0's
    int numberOfZeros = 0;

    // Traverse the string S
    for(i = 0; i < s.Length; i++)
    {

        // If current character is '1'
        if (s[i] == '1')
        {

            // Increase curr_one by one
            curr_one += 1;
        }

        // Otherwise
        else
        {

            // Increment numberofZeros by one
            numberOfZeros += 1;

            // Count length of substring
            // obtained y concatenating
            // preceding and succeeding
            // substrings of '1'
            prev_one += curr_one;

            // Store maximum size in res
            res = Math.Max(res, prev_one);

            // Assign curr_one to prev_one
            prev_one = curr_one;

            // Reset curr_one
            curr_one = 0;
        }
    }

    // If string contains only one '0'
    if (numberOfZeros == 1)
    {
        res -= 1;
    }

    // Return the answer
    return res;
}

// Driver Code
public static void Main(String[] args)
{
    String S = "1101";

    Console.WriteLine(longestSubarray(S));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach

// Function to calculate the length of the
// longest substring of '1's that can be
// obtained by deleting one character
function longestSubarray(s)
{

    // Add '0' at the end
    s += '0';

    // Iterator to traverse the string
    let i;

    // Stores maximum length
    // of required substring
    let res = 0;

    // Stores length of substring of '1'
    // preceding the current character
    let prev_one = 0;

    // Stores length of substring of '1'
    // succeeding the current character
    let curr_one = 0;

    // Counts number of '0's
    let numberOfZeros = 0;

    // Traverse the string S
    for(i = 0; i < s.length; i++)
    {

        // If current character is '1'
        if (s[i] == '1')
        {

            // Increase curr_one by one
            curr_one += 1;
        }

        // Otherwise
        else
        {

            // Increment numberofZeros by one
            numberOfZeros += 1;

            // Count length of substring
            // obtained y concatenating
            // preceding and succeeding
            // substrings of '1'
            prev_one += curr_one;

            // Store maximum size in res
            res = Math.max(res, prev_one);

            // Assign curr_one to prev_one
            prev_one = curr_one;

            // Reset curr_one
            curr_one = 0;
        }
    }

    // If string contains only one '0'
    if (numberOfZeros == 1)
    {
        res -= 1;
    }

    // Return the answer
    return res;
}

// Driver code
     let S = "1101";
    document.write(longestSubarray(S));

   // This code is contributed by splevel62.
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**方法二:**解决问题的另一种方法是使用[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)技术，在删除单个字符后，找到只包含**‘1’**s 的子串的最大长度。按照以下步骤解决问题:

*   用 **0** 初始化 3 个整数变量 **i，j** ，用 **1** 初始化 **k**
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** 的字符。
    *   对于遍历的每个字符，检查是否为**‘0’**。如果发现为真，将 **k** 减 **1** 。
    *   如果 **k < 0** 且**I<sup>th</sup>T5】索引处的字符为**‘0’**，则将 **k** 和 **i** 递增 1**
    *   将 **j** 增加**1**。
*   最后，在完成字符串遍历后，打印长度**j–I–1**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the length of the
// longest substring of '1's that can be
// obtained by deleting one character
int longestSubarray(string s)
{
    // Initializing i and j as left and
    // right boundaries of sliding window
    int i = 0, j = 0, k = 1;

    for (j = 0; j < s.size(); ++j) {

        // If current character is '0'
        if (s[j] == '0')

            // Decrement k by one
            k--;

        // If k is less than zero and character
        // at ith index is '0'
        if (k < 0 && s[i++] == '0')
            k++;
    }

    // Return result
    return j - i - 1;
}

// Driver Code
int main()
{
    string S = "011101101";
    cout << longestSubarray(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach

import java.util.*;

class GFG{

// Function to calculate the length of the
// longest subString of '1's that can be
// obtained by deleting one character
static int longestSubarray(String s)
{
    // Initializing i and j as left and
    // right boundaries of sliding window
    int i = 0, j = 0, k = 1;

    for (j = 0; j < s.length(); ++j)
    {

        // If current character is '0'
        if (s.charAt(j) == '0')

            // Decrement k by one
            k--;

        // If k is less than zero and character
        // at ith index is '0'
        if (k < 0 && s.charAt(i++) == '0')
            k++;
    }

    // Return result
    return j - i - 1;
}

// Driver Code
public static void main(String[] args)
{
    String S = "011101101";
    System.out.print(longestSubarray(S));

}
}

// This code contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the length of the
# longest substring of '1's that can be
# obtained by deleting one character
def longestSubarray(s):

    # Initializing i and j as left and
    # right boundaries of sliding window
    i = 0
    j = 0
    k = 1

    for j in range(len(s)):

        # If current character is '0'
        if (s[j] == '0'):

            # Decrement k by one
            k -= 1

        # If k is less than zero and character
        # at ith index is '0'
        if (k < 0 ):
            if s[i] == '0':
                k += 1

            i += 1

    j += 1

    # Return result
    return j - i - 1

# Driver Code
if __name__ == "__main__" :

    S = "011101101"

    print(longestSubarray(S))

# This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate the length of the
// longest subString of '1's that can be
// obtained by deleting one character
static int longestSubarray(string s)
{

    // Initializing i and j as left and
    // right boundaries of sliding window
    int i = 0, j = 0, k = 1;

    for(j = 0; j < s.Length; ++j)
    {

        // If current character is '0'
        if (s[j] == '0')

            // Decrement k by one
            k -= 1;

        // If k is less than zero and character
        // at ith index is '0'
        if (k < 0 && s[i++] == '0')
            k++;
    }

    // Return result
    return j - i - 1;
}

// Driver Code
public static void Main(string[] args)
{
    string S = "011101101";

    Console.Write(longestSubarray(S));
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to calculate the length of the
// longest substring of '1's that can be
// obtained by deleting one character
function longestSubarray(s)
{
    // Initializing i and j as left and
    // right boundaries of sliding window
    var i = 0, j = 0, k = 1;

    for (j = 0; j < s.length; ++j) {

        // If current character is '0'
        if (s[j] == '0')

            // Decrement k by one
            k--;

        // If k is less than zero and character
        // at ith index is '0'
        if (k < 0 && s[i++] == '0')
            k++;
    }

    // Return result
    return j - i - 1;
}

// Driver Code
var S = "011101101";
document.write( longestSubarray(S));

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)