# 计算两个给定字符串中长度相同但相差一个字符的子字符串

> 原文:[https://www . geeksforgeeks . org/count-相同长度的子字符串-由两个给定字符串中的单个字符区分/](https://www.geeksforgeeks.org/count-substrings-of-same-length-differing-by-a-single-character-from-two-given-strings/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 和 **T** ，任务是计算从这两个字符串中获取相同长度的子字符串的方法数量，以便它们具有单个不同的字符。

**示例:**

> **输入:** S = "ab "，T = "bb"
> **输出:** 3
> **说明:**以下是 S 和 T 相差一个字符的子串对:
> 
> 1.  (“a”、“b”)
> 2.  (“a”、“b”)
> 3.  (“ab”、“bb”)
> 
> **输入:** S = "aba "，T = " Baba "
> T3】输出: 6

**天真方法:**最简单的方法是[从给定的两个字符串生成所有可能的子字符串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，然后计算所有可能的相同长度的子字符串对，通过改变单个字符可以使其相等。

***时间复杂度:**O(N<sup>3</sup>* M<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效方法:**为了优化上述方法，其思想是[同时迭代给定字符串的所有字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，并且对于每对不同的字符，从当前不同字符的下一个索引开始计数所有长度相等的子字符串。打印检查所有不同字符对后获得的计数。

下面是上述方法的实现:

## C++

```
// C++ pprogram for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// substrings of equal length which
// differ by a single character
 int countSubstrings(string s, string t)
{

    // Stores the count of
    // pairs of substrings
    int answ = 0;

    // Traverse the string s
    for(int i = 0; i < s.size(); i++)
    {

        // Traverse the string t
        for(int j = 0; j < t.size(); j++)
        {

            // Different character
            if (t[j] != s[i])
            {

                // Increment the answer
                answ += 1;

                int k = 1;
                int z = -1;
                int q = 1;

                // Count equal substrings
                // from next index
                while (j + z >= 0 &&
                       0 <= i + z &&
                   s[i + z] ==
                   t[j + z])
                {
                    z -= 1;

                    // Increment the count
                    answ += 1;

                    // Increment q
                    q += 1;
                }

                // Check the condition
                while (s.size() > i + k &&
                       j + k < t.size() &&
                         s[i + k] ==
                         t[j + k])
                {

                    // Increment k
                    k += 1;

                    // Add q to count
                    answ += q;

                    // Decrement z
                    z = -1;
                }
            }
        }
    }

    // Return the final count
    return answ;
}

// Driver Code
int main()
{
    string S = "aba";
    string T = "baba";

    // Function Call
    cout<<(countSubstrings(S, T));

}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count the number of
// subStrings of equal length which
// differ by a single character
static int countSubStrings(String s, String t)
{

    // Stores the count of
    // pairs of subStrings
    int answ = 0;

    // Traverse the String s
    for(int i = 0; i < s.length(); i++)
    {

        // Traverse the String t
        for(int j = 0; j < t.length(); j++)
        {

            // Different character
            if (t.charAt(j) != s.charAt(i))
            {

                // Increment the answer
                answ += 1;

                int k = 1;
                int z = -1;
                int q = 1;

                // Count equal subStrings
                // from next index
                while (j + z >= 0 &&
                       0 <= i + z &&
                   s.charAt(i + z) ==
                   t.charAt(j + z))
                {
                    z -= 1;

                    // Increment the count
                    answ += 1;

                    // Increment q
                    q += 1;
                }

                // Check the condition
                while (s.length() > i + k &&
                       j + k < t.length() &&
                         s.charAt(i + k) ==
                         t.charAt(j + k))
                {

                    // Increment k
                    k += 1;

                    // Add q to count
                    answ += q;

                    // Decrement z
                    z = -1;
                }
            }
        }
    }

    // Return the final count
    return answ;
}

// Driver Code
public static void main(String[] args)
{
    String S = "aba";
    String T = "baba";

    // Function Call
    System.out.println(countSubStrings(S, T));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# substrings of equal length which
# differ by a single character
def countSubstrings(s, t):

    # Stores the count of
    # pairs of substrings
    answ = 0

    # Traverse the string s
    for i in range(len(s)):

        # Traverse the string t
        for j in range(len(t)):

            # Different character
            if t[j] != s[i]:

                # Increment the answer
                answ += 1

                k = 1
                z = -1
                q = 1

                # Count equal substrings
                # from next index
                while (
                    j + z >= 0 <= i + z and
                    s[i + z] == t[j + z]
                    ):

                    z -= 1

                    # Increment the count
                    answ += 1

                    # Increment q
                    q += 1

                # Check the condition
                while (
                    len(s) > i + k and
                    j + k < len(t) and
                    s[i + k] == t[j + k]
                    ):

                    # Increment k
                    k += 1

                    # Add q to count
                    answ += q

                    # Decrement z
                    z = -1

    # Return the final count
    return answ

# Driver Code

S = "aba"
T = "baba"

# Function Call
print(countSubstrings(S, T))
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

// Function to count the number of
// subStrings of equal length which
// differ by a single character
static int countSubStrings(String s, String t)
{

    // Stores the count of
    // pairs of subStrings
    int answ = 0;

    // Traverse the String s
    for(int i = 0; i < s.Length; i++)
    {

        // Traverse the String t
        for(int j = 0; j < t.Length; j++)
        {

            // Different character
            if (t[j] != s[i])
            {

                // Increment the answer
                answ += 1;

                int k = 1;
                int z = -1;
                int q = 1;

                // Count equal subStrings
                // from next index
                while (j + z >= 0 &&
                       0 <= i + z &&
                   s[i + z] ==
                   t[j + z])
                {
                    z -= 1;

                    // Increment the count
                    answ += 1;

                    // Increment q
                    q += 1;
                }

                // Check the condition
                while (s.Length > i + k &&
                       j + k < t.Length &&
                         s[i + k] ==
                         t[j + k])
                {

                    // Increment k
                    k += 1;

                    // Add q to count
                    answ += q;

                    // Decrement z
                    z = -1;
                }
            }
        }
    }

    // Return the readonly count
    return answ;
}

// Driver Code
public static void Main(String[] args)
{
    String S = "aba";
    String T = "baba";

    // Function Call
    Console.WriteLine(countSubStrings(S, T));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count the number of
// subStrings of equal length which
// differ by a single character
function countSubStrings(s, t)
{

    // Stores the count of
    // pairs of subStrings
    let answ = 0;

    // Traverse the String s
    for(let i = 0; i < s.length; i++)
    {

        // Traverse the String t
        for(let j = 0; j < t.length; j++)
        {

            // Different character
            if (t[j] != s[i])
            {

                // Increment the answer
                answ += 1;

                let k = 1;
                let z = -1;
                let q = 1;

                // Count equal subStrings
                // from next index
                while (j + z >= 0 &&
                       0 <= i + z &&
                   s[i + z] ==
                   t[j + z])
                {
                    z -= 1;

                    // Increment the count
                    answ += 1;

                    // Increment q
                    q += 1;
                }

                // Check the condition
                while (s.length > i + k &&
                       j + k < t.length &&
                         s[i + k] ==
                         t[j + k])
                {

                    // Increment k
                    k += 1;

                    // Add q to count
                    answ += q;

                    // Decrement z
                    z = -1;
                }
            }
        }
    }

    // Return the readonly count
    return answ;
}

    // Driver Code
    let S = "aba";
    let T = "baba";

    // Function Call
    document.write(countSubStrings(S, T));

// This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N*M*max(N，M))*
***辅助空间:** O(1)*