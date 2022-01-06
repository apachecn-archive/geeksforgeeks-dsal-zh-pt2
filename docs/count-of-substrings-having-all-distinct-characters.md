# 具有所有不同字符的子串计数

> 原文:[https://www . geesforgeks . org/count-of-substrings-all-distinct-characters/](https://www.geeksforgeeks.org/count-of-substrings-having-all-distinct-characters/)

给定一个由小写字母组成的字符串 **str** ，任务是找到仅由不同字符组成的可能子字符串(不一定是不同的)的数量。
**例:**

> **输入:** Str = "gffg"
> **输出:** 6
> **解释:**
> 来自给定字符串的所有可能的子字符串为，
> (**g**)、 **gf** 、【gff】、【gffg】、 **f** 、【ff】、【ffg】、 **f** 、 **fg**
> 
> **输入:** str = "gfg"
> **输出:** 5
> **解释:**
> 来自给定字符串的所有可能的子字符串为，
> (**g**)、 **gf** 、【gfg】、 **f** 、 **fg** 、**g**)
> 其中，高亮显示的

**天真方法:**
最简单的方法是从给定的字符串中生成所有可能的子字符串，并检查每个子字符串是否包含所有不同的字符。如果字符串的长度是 **N** ，那么将会有 **N*(N+1)/2** 个可能的子字符串。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**
借助于字符串字符的[计数频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)，使用[双指针技术](https://www.geeksforgeeks.org/two-pointers-technique/)可以在线性时间内解决问题。

此方法的详细步骤如下:

*   考虑两个指针 **i** 和 **j** ，最初都指向字符串的第一个字符，即 **i = j = 0** 。
*   初始化一个数组 **Cnt[ ]** 来存储从索引 **i** 到 **j** 的子串中的字符数。
*   现在，继续增加 **j** 指针，直到遇到某个重复的字符。递增 **j** 时，将所有以**j**T6 索引结束并以 **i** 和 **j** 之间的任何索引开始的子字符串的计数添加到答案中。所有这些子字符串都将包含不同的字符，因为其中没有重复的字符。
*   如果在索引 **i** 到 **j** 之间的子串中遇到一些重复字符，为了排除这个重复字符，继续递增 **i** 指针，直到重复字符被移除，并相应地继续更新**Cnt【】**数组。
*   继续这个过程，直到 **j** 到达弦的末端。一旦字符串被完全遍历，打印答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above appraoach
#include <bits/stdc++.h>
using namespace std;

// Function to count total
// number of valid substrings
long long int countSub(string str)
{
    int n = (int)str.size();

    // Stores the count of
    // substrings
    long long int ans = 0;

    // Stores the frequency
    // of characters
    int cnt[26];

    memset(cnt, 0, sizeof(cnt));

    // Initialised both pointers
    // to beginning of the string
    int i = 0, j = 0;

    while (i < n) {

        // If all characters in
        // substring from index i
        // to j are distinct
        if (j < n && (cnt[str[j] - 'a']
                      == 0)) {

            // Increment count of j-th
            // character
            cnt[str[j] - 'a']++;

            // Add all substring ending
            // at j and starting at any
            // index between i and j
            // to the answer
            ans += (j - i + 1);

            // Increment 2nd pointer
            j++;
        }

        // If some characters are repeated
        // or j pointer has reached to end
        else {

            // Decrement count of j-th
            // character
            cnt[str[i] - 'a']--;

            // Increment first pointer
            i++;
        }
    }

    // Return the final
    // count of substrings
    return ans;
}

// Driver Code
int main()
{
    string str = "gffg";

    cout << countSub(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above appraoach
import java.util.*;

class GFG{

// Function to count total
// number of valid subStrings
static int countSub(String str)
{
    int n = (int)str.length();

    // Stores the count of
    // subStrings
    int ans = 0;

    // Stores the frequency
    // of characters
    int []cnt = new int[26];

    // Initialised both pointers
    // to beginning of the String
    int i = 0, j = 0;

    while (i < n)
    {

        // If all characters in
        // subString from index i
        // to j are distinct
        if (j < n &&
           (cnt[str.charAt(j) - 'a'] == 0))
        {

            // Increment count of j-th
            // character
            cnt[str.charAt(j) - 'a']++;

            // Add all subString ending
            // at j and starting at any
            // index between i and j
            // to the answer
            ans += (j - i + 1);

            // Increment 2nd pointer
            j++;
        }

        // If some characters are repeated
        // or j pointer has reached to end
        else
        {

            // Decrement count of j-th
            // character
            cnt[str.charAt(i) - 'a']--;

            // Increment first pointer
            i++;
        }
    }

    // Return the final
    // count of subStrings
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String str = "gffg";

    System.out.print(countSub(str));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to implement
# the above appraoach

# Function to count total
# number of valid substrings
def countSub(Str):

    n = len(Str)

    # Stores the count of
    # substrings
    ans = 0

    # Stores the frequency
    # of characters
    cnt = 26 * [0]

    # Initialised both pointers
    # to beginning of the string
    i, j = 0, 0

    while (i < n):

        # If all characters in
        # substring from index i
        # to j are distinct
        if (j < n and
           (cnt[ord(Str[j]) - ord('a')] == 0)):

            # Increment count of j-th
            # character
            cnt[ord(Str[j]) - ord('a')] += 1

            # Add all substring ending
            # at j and starting at any
            # index between i and j
            # to the answer
            ans += (j - i + 1)

            # Increment 2nd pointer
            j += 1

        # If some characters are repeated
        # or j pointer has reached to end
        else:

            # Decrement count of j-th
            # character
            cnt[ord(Str[i]) - ord('a')] -= 1

            # Increment first pointer
            i += 1

    # Return the final
    # count of substrings
    return ans

# Driver code
Str = "gffg"

print(countSub(Str))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to implement
// the above appraoach
using System;

class GFG{

// Function to count total
// number of valid subStrings
static int countSub(String str)
{
    int n = (int)str.Length;

    // Stores the count of
    // subStrings
    int ans = 0;

    // Stores the frequency
    // of characters
    int []cnt = new int[26];

    // Initialised both pointers
    // to beginning of the String
    int i = 0, j = 0;

    while (i < n)
    {

        // If all characters in
        // subString from index i
        // to j are distinct
        if (j < n &&
           (cnt[str[j] - 'a'] == 0))
        {

            // Increment count of j-th
            // character
            cnt[str[j] - 'a']++;

            // Add all subString ending
            // at j and starting at any
            // index between i and j
            // to the answer
            ans += (j - i + 1);

            // Increment 2nd pointer
            j++;
        }

        // If some characters are repeated
        // or j pointer has reached to end
        else
        {

            // Decrement count of j-th
            // character
            cnt[str[i] - 'a']--;

            // Increment first pointer
            i++;
        }
    }

    // Return the final
    // count of subStrings
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "gffg";

    Console.Write(countSub(str));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above appraoach

// Function to count total
// number of valid substrings
function countSub(str)
{
    var n = str.length;

    // Stores the count of
    // substrings
    var ans = 0;

    // Stores the frequency
    // of characters
    var cnt = Array(26).fill(0);

    // Initialised both pointers
    // to beginning of the string
    var i = 0, j = 0;

    while (i < n) {

        // If all characters in
        // substring from index i
        // to j are distinct
        if (j < n && (cnt[str[j].charCodeAt(0) - 'a'.charCodeAt(0)]
                      == 0)) {

            // Increment count of j-th
            // character
            cnt[str[j].charCodeAt(0) - 'a'.charCodeAt(0)]++;

            // Add all substring ending
            // at j and starting at any
            // index between i and j
            // to the answer
            ans += (j - i + 1);

            // Increment 2nd pointer
            j++;
        }

        // If some characters are repeated
        // or j pointer has reached to end
        else {

            // Decrement count of j-th
            // character
            cnt[str[i].charCodeAt(0) - 'a'.charCodeAt(0)]--;

            // Increment first pointer
            i++;
        }
    }

    // Return the final
    // count of substrings
    return ans;
}

// Driver Code
var str = "gffg";
document.write( countSub(str));

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*