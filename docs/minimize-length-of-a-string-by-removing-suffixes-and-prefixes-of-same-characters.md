# 通过删除相同字符的后缀和前缀来最小化字符串的长度

> 原文:[https://www . geesforgeks . org/通过删除相同字符的后缀和前缀来最小化字符串长度/](https://www.geeksforgeeks.org/minimize-length-of-a-string-by-removing-suffixes-and-prefixes-of-same-characters/)

给定长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，该字符串仅由字符**【a】****【b】**和**【c】**组成，任务是通过仅执行一次以下操作来最小化给定字符串的长度:

*   将字符串分成两个非空子字符串，然后将左子字符串追加到右子字符串的末尾。
*   追加时，如果右子串的[后缀](https://www.geeksforgeeks.org/suffix-array-set-1-introduction/)和左子串的[前缀](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)包含相同的字符，则分别从右子串和左子串的后缀和前缀中删除这些字符。重复此步骤，直到没有不可移除的子字符串。

**示例:**

> **输入:**S =【aabcccaba】
> T3】输出 : 4
> **说明:**
> 将给定的字符串 S 分为两部分**【aabcc】**和**【cabba】**。下面是对上述两个子字符串执行的操作:
> 
> *   去掉相同字符的前缀和后缀，即**‘a’**。该字符串变为**“bcc”**和**“cabb”**。
> *   去掉相同字符的后缀和前缀，即**‘b’**。弦变成**【cc】****【ca】**。
> 
> 现在，连接左右子串后，得到的字符串是**“cacc”**，长度最短，即 4。
> 
> **输入:**S = " aacbcca "
> T3】输出: 1

**方法:**通过找到字符串的[后缀和字符串的](https://www.geeksforgeeks.org/string-from-prefix-and-suffix-of-given-two-strings/)前缀中存在的相似字符，使用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)可以解决给定的问题。
按照以下步骤解决问题:

*   初始化两个变量，说 **i** 为 **0** 和 **j** 为**(N–1)**。
*   [循环迭代](https://www.geeksforgeeks.org/range-based-loop-c/)直到 **i < j** 和字符**S【I】**和**S【j】**相同，执行以下步骤:
    *   初始化一个变量，用**S【I】**表示 **d** ，向右移动指针 **i** ，而 **i** 最多为**j****d = S【I】**。
    *   向左移动指针 **j** 直到 **i** 最多为 **j** 和**d = S【j】**。
*   完成上述步骤后，**(j–I+1)**的值是字符串的最小可能长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum length
// of the string after removing the same
// characters from the end and front of the
// two strings after dividing into 2 substrings
int minLength(string s)
{

    // Initialize two pointers
    int i = 0, j = s.length() - 1;

    // Traverse the string S
    for(; i < j && s[i] == s[j];)
    {

        // Current char on left pointer
        char d = s[i];

        // Shift i towards right
        while (i <= j && s[i] == d)
            i++;

        // Shift j towards left
        while (i <= j && s[j] == d)
            j--;
    }

    // Return the minimum possible
    // length of string
    return j - i + 1;
}

// Driver Code
int main()
{
    string S = "aacbcca";

    cout << minLength(S);
}

// This code is contributed by bgangwar59
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.lang.*;
import java.util.*;

class GFG {

    // Function to find the minimum length
    // of the string after removing the same
    // characters from the end and front of the
    // two strings after dividing into 2 substrings
    static int minLength(String s)
    {
        // Initialize two pointers
        int i = 0, j = s.length() - 1;

        // Traverse the string S
        for (; i < j
               && s.charAt(i) == s.charAt(j);) {

            // Current char on left pointer
            char d = s.charAt(i);

            // Shift i towards right
            while (i <= j
                   && s.charAt(i) == d)
                i++;

            // Shift j towards left
            while (i <= j
                   && s.charAt(j) == d)
                j--;
        }

        // Return the minimum possible
        // length of string
        return j - i + 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "aacbcca";
        System.out.println(minLength(S));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum length
# of the string after removing the same
# characters from the end and front of the
# two strings after dividing into 2 substrings
def minLength(s):

    # Initialize two pointers
    i = 0; j = len(s) - 1

    # Traverse the string S
    while (i < j and s[i] == s[j]):

        # Current char on left pointer
        d = s[i]

        # Shift i towards right
        while (i <= j and s[i] == d):
            i += 1

        # Shift j towards left
        while (i <= j and s[j] == d):
            j -= 1

    # Return the minimum possible
    # length of string
    return j - i + 1

# Driver Code
if __name__ == "__main__" :

    S = "aacbcca"

    print(minLength(S))

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum length
// of the string after removing the same
// characters from the end and front of the
// two strings after dividing into 2 substrings
static int minLength(string s)
{

    // Initialize two pointers
    int i = 0, j = s.Length - 1;

    // Traverse the string S
    for(; i < j && s[i] == s[j];)
    {

        // Current char on left pointer
        char d = s[i];

        // Shift i towards right
        while (i <= j && s[i] == d)
            i++;

        // Shift j towards left
        while (i <= j && s[j] == d)
            j--;
    }

    // Return the minimum possible
    // length of string
    return j - i + 1;
}

// Driver Code
public static void Main(string[] args)
{
    string S = "aacbcca";

    Console.WriteLine(minLength(S));
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find the minimum length
// of the string after removing the same
// characters from the end and front of the
// two strings after dividing into 2 substrings
function minLength(s)
{

    // Initialize two pointers
    i = 0; j = s.length - 1

    // Traverse the string S
    while (i < j && s[i] == s[j]){

        // Current char on left pointer
        d = s[i]

        // Shift i towards right
        while (i <= j && s[i] == d)
            i += 1

        // Shift j towards left
        while (i <= j && s[j] == d)
            j -= 1

    // Return the minimum possible
    // length of string
            }
    return j - i + 1
}

// Driver Code
S = "aacbcca"

document.write(minLength(S))

// This code is contributed by AnkThon
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)