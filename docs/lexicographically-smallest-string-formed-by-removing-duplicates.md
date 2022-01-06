# 通过删除重复项形成的字典最小字符串

> 原文:[https://www . geesforgeks . org/按字典顺序排列-最小-字符串-通过删除重复项形成/](https://www.geeksforgeeks.org/lexicographically-smallest-string-formed-by-removing-duplicates/)

给定一个由小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是通过从给定的[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** 中移除重复项来找到字典上最小的字符串。

**示例:**

> **输入:** S = "yzxyz"
> **输出:** xyz
> **解释:**去除给定字符串中索引 0 和 1 处的重复字符，剩余的字符串“xyz”仅由唯一的字母组成，并且是字典顺序中最小的可能字符串。
> 
> **输入:** S = "acbc"
> **输出:**【abc】
> **解释:**删除给定字符串中索引 3 处的重复字符，剩余的字符串“ABC”仅由唯一的字母组成，并且是字典顺序中最小的可能字符串。

**方法:**按照以下步骤解决问题:

*   初始化一个[字符串](https://www.geeksforgeeks.org/c-string-class-and-its-applications/) **res** 来存储结果字符串。
*   将给定字符串中每个字符的[频率存储在](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **频率[]** 中。
*   维护一个数组 **vis[]** ，用于标记已经出现在结果字符串 **res** 中的字符。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **S** ，对于每个字符**S【I】**，执行以下操作:
    *   通过 **1** 降低当前字符的频率。
    *   如果当前字符在数组**vis【】**中没有被标记为已访问，则执行以下操作:
        *   如果 **res** 的最后一个字母小于**S【I】**，则在 **res** 中加上**S【I】**。
        *   如果 **res** 的最后一个字母大于**S【I】**，并且 **res** 的最后一个字母的计数超过 **0** ，则移除该字符并将**访问【S【I】】**标记为 **0** 并继续该步骤，直到满足上述条件。
        *   在[从上述状态中脱离](https://www.geeksforgeeks.org/break-statement-cc/)后，将 **S[i]** 添加至 **res** 并将**访问【S[I]】**标记为 **1** 。
*   完成上述步骤后，打印字符串 **res** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds lexicographically
// smallest string after removing the
// duplicates from the given string
string removeDuplicateLetters(string s)
{
    // Stores the frequency of characters
    int cnt[26] = { 0 };

    // Mark visited characters
    int vis[26] = { 0 };

    int n = s.size();

    // Stores count of each character
    for (int i = 0; i < n; i++)
        cnt[s[i] - 'a']++;

    // Stores the resultant string
    string res = "";

    for (int i = 0; i < n; i++) {

        // Decrease the count of
        // current character
        cnt[s[i] - 'a']--;

        // If character is not already
        // in answer
        if (!vis[s[i] - 'a']) {

            // Last character > S[i]
            // and its count > 0
            while (res.size() > 0
                   && res.back() > s[i]
                   && cnt[res.back() - 'a'] > 0) {

                // Mark letter unvisited
                vis[res.back() - 'a'] = 0;
                res.pop_back();
            }

            // Add s[i] in res and
            // mark it visited
            res += s[i];
            vis[s[i] - 'a'] = 1;
        }
    }

    // Return the resultant string
    return res;
}

// Driver Code
int main()
{
    // Given string S
    string S = "acbc";

    // Function Call
    cout << removeDuplicateLetters(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function that finds lexicographically
// smallest string after removing the
// duplicates from the given string
static String removeDuplicateLetters(String s)
{

    // Stores the frequency of characters
    int[] cnt = new int[26];

    // Mark visited characters
    int[] vis = new int[26];

    int n = s.length();

    // Stores count of each character
    for(int i = 0; i < n; i++)
        cnt[s.charAt(i) - 'a']++;

    // Stores the resultant string
    String res = "";

    for(int i = 0; i < n; i++)
    {

        // Decrease the count of
        // current character
        cnt[s.charAt(i) - 'a']--;

        // If character is not already
        // in answer
        if (vis[s.charAt(i) - 'a'] == 0)
        {

            // Last character > S[i]
            // and its count > 0
            int size = res.length();
            while (size > 0 &&
                   res.charAt(size - 1) > s.charAt(i) &&
                   cnt[res.charAt(size - 1) - 'a'] > 0)
            {

                // Mark letter unvisited
                vis[res.charAt(size - 1) - 'a'] = 0;
                res = res.substring(0, size - 1);
                size--;
            }

            // Add s[i] in res and
            // mark it visited
            res += s.charAt(i);
            vis[s.charAt(i) - 'a'] = 1;
        }
    }

    // Return the resultant string
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Given string S
    String S = "acbc";

    // Function Call
    System.out.println(removeDuplicateLetters(S));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds lexicographically
# smallest after removing the
# duplicates from the given string
def removeDuplicateLetters(s):

    # Stores the frequency of characters
    cnt = [0] * 26

    # Mark visited characters
    vis = [0] * 26

    n = len(s)

    # Stores count of each character
    for i in s:
        cnt[ord(i) - ord('a')] += 1

    # Stores the resultant string
    res = []

    for i in range(n):

        # Decrease the count of
        # current character
        cnt[ord(s[i]) - ord('a')] -= 1

        # If character is not already
        # in answer
        if (not vis[ord(s[i]) - ord('a')]):

            # Last character > S[i]
            # and its count > 0
            while (len(res) > 0 and
                    res[-1] > s[i] and
           cnt[ord(res[-1]) - ord('a')] > 0):

                # Mark letter unvisited
                vis[ord(res[-1]) - ord('a')] = 0

                del res[-1]

            # Add s[i] in res and
            # mark it visited
            res += s[i]
            vis[ord(s[i]) - ord('a')] = 1

    # Return the resultant string
    return "".join(res)

# Driver Code
if __name__ == '__main__':

    # Given S
    S = "acbc"

    # Function Call
    print(removeDuplicateLetters(S))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that finds lexicographically
// smallest string after removing the
// duplicates from the given string
static string removeDuplicateLetters(string s)
{

    // Stores the frequency of characters
    int[] cnt = new int[26];

    // Mark visited characters
    int[] vis = new int[26];

    int n = s.Length;

    // Stores count of each character
    for(int i = 0; i < n; i++)
        cnt[s[i] - 'a']++;

    // Stores the resultant string
    String res = "";

    for(int i = 0; i < n; i++)
    {

        // Decrease the count of
        // current character
        cnt[s[i] - 'a']--;

        // If character is not already
        // in answer
        if (vis[s[i] - 'a'] == 0)
        {

            // Last character > S[i]
            // and its count > 0
            int size = res.Length;
            while (size > 0 && res[size - 1] > s[i] &&
                    cnt[res[size - 1] - 'a'] > 0)
            {

                // Mark letter unvisited
                vis[res[size - 1] - 'a'] = 0;
                res = res.Substring(0, size - 1);
                size--;
            }

            // Add s[i] in res and
            // mark it visited
            res += s[i];
            vis[s[i] - 'a'] = 1;
        }
    }

    // Return the resultant string
    return res;
}

// Driver Code
public static void Main()
{

    // Given string S
    string S = "acbc";

    // Function Call
    Console.WriteLine(removeDuplicateLetters(S));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that finds lexicographically
// smallest string after removing the
// duplicates from the given string
function removeDuplicateLetters(s)
{
    // Stores the frequency of characters
    var cnt = Array(26).fill(0);

    // Mark visited characters
    var vis = Array(26).fill(false);

    var n = s.length;

    // Stores count of each character
    for (var i = 0; i < n; i++)
        cnt[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]++;

    // Stores the resultant string
    var res = "";

    for (var i = 0; i < n; i++) {

        // Decrease the count of
        // current character
        cnt[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]--;

        // If character is not already
        // in answer
        if (!vis[s[i].charCodeAt(0) - 'a'.charCodeAt(0)]) {

            // Last character > S[i]
            // and its count > 0
            while (res.length > 0
                   && res[res.length-1].charCodeAt(0) >
                   s[i].charCodeAt(0)
                   && cnt[res[res.length-1].charCodeAt(0) -
                   'a'.charCodeAt(0)] > 0) {

                // Mark letter unvisited
                vis[res[res.length-1].charCodeAt(0) -
                'a'.charCodeAt(0)] = 0;
                res = res.substring(0, res.length-1);
            }

            // Add s[i] in res and
            // mark it visited
            res += s[i];
            vis[s[i].charCodeAt(0) - 'a'.charCodeAt(0)] = 1;
        }
    }

    // Return the resultant string
    return res;
}

// Driver Code
// Given string S
var S = "acbc";

// Function Call
document.write( removeDuplicateLetters(S));

</script>
```

**Output:** 

```
abc
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)