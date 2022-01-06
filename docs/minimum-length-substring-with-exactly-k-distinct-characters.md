# 最小长度子串，正好有 K 个不同的字符

> 原文:[https://www . geeksforgeeks . org/最小长度-带有-k-distinct-字符的子字符串/](https://www.geeksforgeeks.org/minimum-length-substring-with-exactly-k-distinct-characters/)

给定一个字符串 **S** 和一个数字 **K** 。任务是找到正好有 K 个不同字符的最小长度子串。
**注**:字符串 S 仅由小写英文字母组成。
**示例:**

```
Input:  S = "ababcb", K = 3
Output:  abc

Input:  S="efecfefd", K = 4
Output:  cfefd
```

**简单解法:**简单解法是考虑每个子串，检查是否包含 k 个不同的字符。如果是，则将该子串的长度与之前找到的最小长度子串进行比较。这种方法的时间复杂度为 0(N)<sup>2</sup>，其中 N 是字符串的长度。高效解决方案:高效解决方案是使用滑动窗口技术和哈希。思路是用两个指针 *st* 和 *end* 来表示滑动窗口的起点和终点。首先将两者指向字符串的开头。向前移动末端并增加相应字符的计数。如果计数为 1，则找到一个新的不同字符，并增加不同字符的计数。如果不同字符数的计数大于 **k** ，则向前移动 *st* 并减少字符数。如果字符计数为零，则删除一个不同的字符，不同元素的计数可以减少到 *k* 。如果不同元素的计数为 *k* ，则通过向前移动 st 从滑动窗口的开头移除计数大于 1 的字符。将当前滑动窗口的长度与目前为止找到的最小长度进行比较，并在必要时进行更新。
注意每个字符最多在滑动窗口中添加和删除一次，所以每个字符遍历两次。因此时间复杂度是线性的。
以下是上述办法的实施:

## C++

```
// C++ program to find minimum length substring
// having exactly k distinct character.

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum length substring
// having exactly k distinct character.
string findMinLenStr(string str, int k)
{
    int n = str.length();

    // Starting index of sliding window.
    int st = 0;

    // Ending index of sliding window.
    int end = 0;

    // To store count of character.
    int cnt[26];
    memset(cnt, 0, sizeof(cnt));

    // To store count of distinct
    // character in current sliding
    // window.
    int distEle = 0;

    // To store length of current
    // sliding window.
    int currlen;

    // To store minimum length.
    int minlen = n;

    // To store starting index of minimum
    // length substring.
    int startInd = -1;

    while (end < n) {

        // Increment count of current character
        // If this count is one then a new
        // distinct character is found in
        // sliding window.
        cnt[str[end] - 'a']++;
        if (cnt[str[end] - 'a'] == 1)
            distEle++;

        // If number of distinct characters is
        // is greater than k, then move starting
        // point of sliding window forward,
        // until count is k.
        if (distEle > k) {
            while (st < end && distEle > k) {
                if (cnt[str[st] - 'a'] == 1)
                    distEle--;
                cnt[str[st] - 'a']--;
                st++;
            }
        }

        // Remove characters from the beginning of
        // sliding window having count more than 1
        // to minimize length.
        if (distEle == k) {
            while (st < end && cnt[str[st] - 'a'] > 1) {
                cnt[str[st] - 'a']--;
                st++;
            }

            // Compare length with minimum length
            // and update if required.
            currlen = end - st + 1;
            if (currlen < minlen) {
                minlen = currlen;
                startInd = st;
            }
        }

        end++;
    }

    // Return minimum length  substring.
    return str.substr(startInd, minlen);
}

// Driver code
int main()
{
    string str = "efecfefd";

    int k = 4;

    cout << findMinLenStr(str, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum length subString
// having exactly k distinct character.
class GFG
{

// Function to find minimum length subString
// having exactly k distinct character.
static String findMinLenStr(String str, int k)
{
    int n = str.length();

    // Starting index of sliding window.
    int st = 0;

    // Ending index of sliding window.
    int end = 0;

    // To store count of character.
    int cnt[] = new int[26];
    for(int i = 0; i < 26; i++)cnt[i] = 0;

    // To store count of distinct
    // character in current sliding
    // window.
    int distEle = 0;

    // To store length of current
    // sliding window.
    int currlen;

    // To store minimum length.
    int minlen = n;

    // To store starting index of minimum
    // length subString.
    int startInd = -1;

    while (end < n)
    {

        // Increment count of current character
        // If this count is one then a new
        // distinct character is found in
        // sliding window.
        cnt[str.charAt(end) - 'a']++;
        if (cnt[str.charAt(end) - 'a'] == 1)
            distEle++;

        // If number of distinct characters is
        // is greater than k, then move starting
        // point of sliding window forward,
        // until count is k.
        if (distEle > k)
        {
            while (st < end && distEle > k)
            {
                if (cnt[str.charAt(st) - 'a'] == 1)
                    distEle--;
                cnt[str.charAt(st) - 'a']--;
                st++;
            }
        }

        // Remove characters from the beginning of
        // sliding window having count more than 1
        // to minimize length.
        if (distEle == k)
        {
            while (st < end && cnt[str.charAt(st) - 'a'] > 1)
            {
                cnt[str.charAt(st) - 'a']--;
                st++;
            }

            // Compare length with minimum length
            // and update if required.
            currlen = end - st + 1;
            if (currlen < minlen)
            {
                minlen = currlen;
                startInd = st;
            }
        }

        end++;
    }

    // Return minimum length subString.
    return str.substring(startInd,startInd + minlen);
}

// Driver code
public static void main(String args[])
{
    String str = "efecfefd";
    int k = 4;
    System.out.println(findMinLenStr(str, k));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to find minimum length
# substring having exactly k distinct character.

# Function to find minimum length substring
# having exactly k distinct character.
def findMinLenStr(str, k):

    n = len(str)

    # Starting index of sliding window.
    st = 0

    # Ending index of sliding window.
    end = 0

    # To store count of character.
    cnt = [0] * 26

    # To store count of distinct
    # character in current sliding
    # window.
    distEle = 0

    # To store length of current
    # sliding window.
    currlen =0

    # To store minimum length.
    minlen = n

    # To store starting index of minimum
    # length substring.
    startInd = -1

    while (end < n):

        # Increment count of current character
        # If this count is one then a new
        # distinct character is found in
        # sliding window.
        cnt[ord(str[end]) - ord('a')] += 1
        if (cnt[ord(str[end]) - ord('a')] == 1):
            distEle += 1

        # If number of distinct characters is
        # is greater than k, then move starting
        # point of sliding window forward,
        # until count is k.
        if (distEle > k):
            while (st < end and distEle > k):
                if (cnt[ord(str[st]) -
                        ord('a')] == 1):
                    distEle -= 1
                cnt[ord(str[st]) - ord('a')] -= 1
                st += 1

        # Remove characters from the beginning of
        # sliding window having count more than 1
        # to minimize length.
        if (distEle == k):
            while (st < end and cnt[ord(str[st]) -
                                    ord('a')] > 1):
                cnt[ord(str[st]) - ord('a')] -= 1
                st += 1

            # Compare length with minimum length
            # and update if required.
            currlen = end - st + 1
            if (currlen < minlen):
                minlen = currlen
                startInd = st

        end += 1

    # Return minimum length substring.
    return str[startInd : startInd + minlen]

# Driver code
if __name__ == "__main__":

    str = "efecfefd"

    k = 4

    print(findMinLenStr(str, k))

# This code is contributed by Ita_c
```

## C#

```
// C# program to find minimum length subString
// having exactly k distinct character.
using System;

class GFG
{

    // Function to find minimum length subString
    // having exactly k distinct character.
    static String findMinLenStr(string str, int k)
    {
        int n = str.Length;

        // Starting index of sliding window.
        int st = 0;

        // Ending index of sliding window.
        int end = 0;

        // To store count of character.
        int []cnt = new int[26];
        for(int i = 0; i < 26; i++)cnt[i] = 0;

        // To store count of distinct
        // character in current sliding
        // window.
        int distEle = 0;

        // To store length of current
        // sliding window.
        int currlen;

        // To store minimum length.
        int minlen = n;

        // To store starting index of minimum
        // length subString.
        int startInd = -1;

        while (end < n)
        {

            // Increment count of current character
            // If this count is one then a new
            // distinct character is found in
            // sliding window.
            cnt[str[end] - 'a']++;
            if (cnt[str[end] - 'a'] == 1)
                distEle++;

            // If number of distinct characters is
            // is greater than k, then move starting
            // point of sliding window forward,
            // until count is k.
            if (distEle > k)
            {
                while (st < end && distEle > k)
                {
                    if (cnt[str[st] - 'a'] == 1)
                        distEle--;
                    cnt[str[st] - 'a']--;
                    st++;
                }
            }

            // Remove characters from the beginning of
            // sliding window having count more than 1
            // to minimize length.
            if (distEle == k)
            {
                while (st < end && cnt[str[st] - 'a'] > 1)
                {
                    cnt[str[st] - 'a']--;
                    st++;
                }

                // Compare length with minimum length
                // and update if required.
                currlen = end - st + 1;
                if (currlen < minlen)
                {
                    minlen = currlen;
                    startInd = st;
                }
            }

            end++;
        }

        // Return minimum length subString.
        return str.Substring(startInd, minlen);
    }

    // Driver code
    public static void Main()
    {
        string str = "efecfefd";
        int k = 4;
        Console.WriteLine(findMinLenStr(str, k));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// Javascript program to find minimum length substring
// having exactly k distinct character.

// Function to find minimum length substring
// having exactly k distinct character.
function findMinLenStr(str, k)
{
    var n = str.length;

    // Starting index of sliding window.
    var st = 0;

    // Ending index of sliding window.
    var end = 0;

    // To store count of character.
    var cnt = Array(26).fill(0);

    // To store count of distinct
    // character in current sliding
    // window.
    var distEle = 0;

    // To store length of current
    // sliding window.
    var currlen;

    // To store minimum length.
    var minlen = n;

    // To store starting index of minimum
    // length substring.
    var startInd = -1;

    while (end < n) {

        // Increment count of current character
        // If this count is one then a new
        // distinct character is found in
        // sliding window.
        cnt[str[end].charCodeAt(0) - 'a'.charCodeAt(0)]++;
        if (cnt[str[end].charCodeAt(0) - 'a'.charCodeAt(0)] == 1)
            distEle++;

        // If number of distinct characters is
        // is greater than k, then move starting
        // point of sliding window forward,
        // until count is k.
        if (distEle > k) {
            while (st < end && distEle > k) {
                if (cnt[str[st].charCodeAt(0) - 'a'.charCodeAt(0)] == 1)
                    distEle--;
                cnt[str[st].charCodeAt(0) - 'a'.charCodeAt(0)]--;
                st++;
            }
        }

        // Remove characters from the beginning of
        // sliding window having count more than 1
        // to minimize length.
        if (distEle == k) {
            while (st < end && cnt[str[st].charCodeAt(0) - 'a'.charCodeAt(0)] > 1) {
                cnt[str[st].charCodeAt(0) - 'a'.charCodeAt(0)]--;
                st++;
            }

            // Compare length with minimum length
            // and update if required.
            currlen = end - st + 1;
            if (currlen < minlen) {
                minlen = currlen;
                startInd = st;
            }
        }

        end++;
    }

    // Return minimum length  substring.
    return str.substr(startInd, minlen);
}

// Driver code
var str = "efecfefd";
var k = 4;
document.write( findMinLenStr(str, k));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
cfefd
```

**时间复杂度:** O(N)，其中 N 为给定字符串的长度。
**辅助空间:** O(1)