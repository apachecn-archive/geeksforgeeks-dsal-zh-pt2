# 字符可以重新排列形成回文的最长子串

> 原文:[https://www . geesforgeks . org/最长子串-其字符可以重新排列以形成回文/](https://www.geeksforgeeks.org/longest-substring-whose-characters-can-be-rearranged-to-form-a-palindrome/)

给定一个长度为 **N** 的字符串 **S** ，其中只包含小写字母。找到 **S** 最长子串的长度，这样里面的字符就可以重新排列形成[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。

**示例:**

> ***输入:*****S = " aabe "
> ***输出:** 3*
> ***解释:***
> 子串“aab”可以重新排列形成“aba”，这是一个回文子串。
> 因为“aab”的长度是 3，所以输出是 3。
> 注意“a”、“aa”、“b”和“e”可以排列成回文串，但不能长于“aab”。**
> 
> *****输入:*** S = "adbabd"
> ***输出:*** 6
> ***解释:***
> 整个字符串“adbabd”可以重新排列形成回文子串。一种可能的安排是“abddba”。
> 因此，输出字符串的长度，即 6。**

****天真方法:**想法是[生成所有可能的子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)，并记录其中每个字符的数量。初始化*用值 0 回答* 。如果每个字符的计数是偶数，最多出现一个奇数字符，则子串可以重新排列以形成回文串。如果子串满足这个属性，那么更新答案。完成上述步骤后，打印最大长度。**

*****时间复杂度:**O(N<sup>3</sup>* 26)*
***辅助空间:****O(N<sup>2</sup>* 26)***

****高效方法:**思路是观察如果**最多**一个字符出现奇数次，则该字符串为回文。所以不需要保留每个字符的总计数。仅仅知道它出现偶数或奇数次就足够了。为此，使用[位屏蔽](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)，因为小写字母的计数只有 26。**

1.  **定义一个位掩码变量 ***掩码*** ，它跟踪每个字符的出现是偶数还是奇数。**
2.  **创建一个字典*索引* ，跟踪每个位掩码的索引。**
3.  **遍历给定的字符串 S **。**首先，将字符从**‘a’–‘z’**转换为**0–25**，并将该值存储在变量 *temp* 中。对于字符的每一次出现，用*掩码*对 **2 <sup>温度</sup>** 进行[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。**
4.  **如果角色出现*甚至* 次，其在*面具*中的位将被*关闭*否则将被*开启*。如果*掩码*当前不在*索引*中，只需将当前索引 **i** 分配给*索引*中的位掩码 ***掩码*** 。**
5.  **如果*掩码*出现在*索引* 中，这意味着从**索引【掩码】**到 **i** ，所有字符的出现是偶数，这适合于回文子串。因此，如果该段从**索引【掩码】**到 **i** 的长度大于答案，则更新答案。**
6.  **要检查一个字符出现奇数次的子字符串，将变量 **j** 迭代到**【0，25】**上。将 **x** 与 **2 <sup>j</sup>** 的[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)存储在 *mask2* **中。****
7.  **如果*索引*中存在 *mask2* ，这意味着该字符出现奇数次，所有字符在段**索引【mask 2】**到 **i** 中出现偶数次，这也是回文串的合适条件。因此，如果这个子串的长度大于*答案*，就用这个子串的长度更新我们的答案。**
8.  **在上述步骤之后，打印子字符串的最大长度。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to get the length of longest
// substring whose characters can be
// arranged to form a palindromic string
int longestSubstring(string s, int n)
{

    // To keep track of the last
    // index of each xor
    map<int, int> index;

    // Initialize answer with 0
    int answer = 0;

    int mask = 0;
    index[mask] = -1;

    // Now iterate through each character
    // of the string
    for(int i = 0; i < n; i++)
    {

        // Convert the character from
        // [a, z] to [0, 25]
        int temp = (int)s[i] - 97;

        // Turn the temp-th bit on if
        // character occurs odd number
        // of times and turn off the temp-th
        // bit off if the character occurs
        // ever number of times
        mask ^= (1 << temp);

        // If a mask is present in the index
        // Therefore a palindrome is
        // found from index[mask] to i
        if (index[mask])
        {
            answer = max(answer,
                         i - index[mask]);
        }

        // If x is not found then add its
        // position in the index dict.
        else
            index[mask] = i;

        // Check for the palindrome of
        // odd length
        for(int j = 0; j < 26; j++)
        {

            // We cancel the occurrence
            // of a character if it occurs
            // odd number times
            int mask2 = mask ^ (1 << j);
            if (index[mask2])
            {
                answer =max(answer,
                            i - index[mask2]);
            }
        }
    }
    return answer;
}

// Driver code
int main ()
{

    // Given String
    string s = "adbabd";

    // Length of given string
    int n = s.size();

    // Function call
    cout << (longestSubstring(s, n));
}

// This code is contributed by Stream_Cipher
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to get the length of longest
// substring whose characters can be
// arranged to form a palindromic string
static int longestSubstring(String s, int n)
{

    // To keep track of the last
    // index of each xor
    Map<Integer, Integer> index = new HashMap<>();

    // Initialize answer with 0
    int answer = 0;

    int mask = 0;
    index.put(mask, -1);

    // Now iterate through each character
    // of the string
    for(int i = 0; i < n; i++)
    {

        // Convert the character from
        // [a, z] to [0, 25]
        int temp = (int)s.charAt(i) - 97;

        // Turn the temp-th bit on if
        // character occurs odd number
        // of times and turn off the temp-th
        // bit off if the character occurs
        // ever number of times
        mask ^= (1 << temp);

        // If a mask is present in the index
        // Therefore a palindrome is
        // found from index[mask] to i
        if (index.containsKey(mask))
        {
            answer = Math.max(answer,
                i - index.get(mask));
        }

        // If x is not found then add its
        // position in the index dict.
        else
            index.put(mask,i);

        // Check for the palindrome of
        // odd length
        for (int j = 0;j < 26; j++)
        {

            // We cancel the occurrence
            // of a character if it occurs
            // odd number times
            int mask2 = mask ^ (1 << j);
            if (index.containsKey(mask2))
            {
                answer = Math.max(answer,
                    i - index.get(mask2));
            }
        }
    }
    return answer;
}

// Driver code
public static void main (String[] args)
{

    // Given String
    String s = "adbabd";

    // Length of given string
    int n = s.length();

    // Function call
    System.out.print(longestSubstring(s, n));
}
}

// This code is contributed by offbeat
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to get the length of longest
# substring whose characters can be
# arranged to form a palindromic string
def longestSubstring(s: str, n: int):

    # To keep track of the last
    # index of each xor
    index = dict()

    # Initialize answer with 0
    answer = 0

    mask = 0
    index[mask] = -1

    # Now iterate through each character
    # of the string
    for i in range(n):

        # Convert the character from
        # [a, z] to [0, 25]
        temp = ord(s[i]) - 97

        # Turn the temp-th bit on if
        # character occurs odd number
        # of times and turn off the temp-th
        # bit off if the character occurs
        # ever number of times
        mask ^= (1 << temp)

        # If a mask is present in the index
        # Therefore a palindrome is
        # found from index[mask] to i
        if mask in index.keys():
            answer = max(answer,
                         i - index[mask])

        # If x is not found then add its
        # position in the index dict.
        else:
            index[mask] = i

        # Check for the palindrome of
        # odd length
        for j in range(26):

            # We cancel the occurrence
            # of a character if it occurs
            # odd number times
            mask2 = mask ^ (1 << j)
            if mask2 in index.keys():

                answer = max(answer,
                             i - index[mask2])

    return answer

# Driver Code

# Given String
s = "adbabd"

# Length of given string
n = len(s)

# Function call
print(longestSubstring(s, n))
```

## **C#**

```
// C# program for the above approach
using System.Collections.Generic;
using System;

class GFG{

// Function to get the length of longest
// substring whose characters can be
// arranged to form a palindromic string
static int longestSubstring(string s, int n)
{

    // To keep track of the last
    // index of each xor
    Dictionary<int,
               int> index = new Dictionary<int,
                                           int>();

    // Initialize answer with 0
    int answer = 0;

    int mask = 0;
    index[mask] = -1;

    // Now iterate through each character
    // of the string
    for(int i = 0; i < n; i++)
    {

        // Convert the character from
        // [a, z] to [0, 25]
        int temp = (int)s[i] - 97;

        // Turn the temp-th bit on if
        // character occurs odd number
        // of times and turn off the temp-th
        // bit off if the character occurs
        // ever number of times
        mask ^= (1 << temp);

        // If a mask is present in the index
        // Therefore a palindrome is
        // found from index[mask] to i
        if (index.ContainsKey(mask) == true)
        {
            answer = Math.Max(answer,
                              i - index[mask]);
        }

        // If x is not found then add its
        // position in the index dict.
        else
            index[mask] = i;

        // Check for the palindrome of
        // odd length
        for(int j = 0; j < 26; j++)
        {

            // We cancel the occurrence
            // of a character if it occurs
            // odd number times
            int mask2 = mask ^ (1 << j);
            if (index.ContainsKey(mask2) == true)
            {
                answer = Math.Max(answer,
                                  i - index[mask2]);
            }
        }
    }
    return answer;
}

// Driver code
public static void Main ()
{

    // Given String
    string s = "adbabd";

    // Length of given string
    int n = s.Length;

    // Function call
    Console.WriteLine(longestSubstring(s, n));
}
}

// This code is contributed by Stream_Cipher
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to get the length of longest
// substring whose characters can be
// arranged to form a palindromic string
function longestSubstring(s, n)
{

    // To keep track of the last
    // index of each xor
    var index = new Map();

    // Initialize answer with 0
    var answer = 0;

    var mask = 0;
    index[mask] = -1;

    // Now iterate through each character
    // of the string
    for(var i = 0; i < n; i++)
    {

        // Convert the character from
        // [a, z] to [0, 25]
        var temp = s[i].charCodeAt(0) - 97;

        // Turn the temp-th bit on if
        // character occurs odd number
        // of times and turn off the temp-th
        // bit off if the character occurs
        // ever number of times
        mask ^= (1 << temp);

        // If a mask is present in the index
        // Therefore a palindrome is
        // found from index[mask] to i
        if (index[mask])
        {
            answer = Math.max(answer,
                         i - index[mask]);
        }

        // If x is not found then add its
        // position in the index dict.
        else
            index[mask] = i;

        // Check for the palindrome of
        // odd length
        for(var j = 0; j < 26; j++)
        {

            // We cancel the occurrence
            // of a character if it occurs
            // odd number times
            var mask2 = mask ^ (1 << j);
            if (index[mask2])
            {
                answer = Math.max(answer,
                            i - index[mask2]);
            }
        }
    }
    return answer;
}

// Driver code
// Given String
var s = "adbabd";

// Length of given string
var n = s.length;

// Function call
document.write(longestSubstring(s, n));

// This code is contributed by rrrtnx.
</script>
```

****Output:** 

```
6
```** 

*****时间复杂度:** O(N * 26)*
***辅助空间:** O(N * 26)***