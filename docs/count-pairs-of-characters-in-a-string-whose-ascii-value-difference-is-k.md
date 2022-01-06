# 统计 ASCII 值差为 K 的字符串中的字符对

> 原文:[https://www . geesforgeks . org/count-字符串中的字符对-其 ascii 值差为-k/](https://www.geeksforgeeks.org/count-pairs-of-characters-in-a-string-whose-ascii-value-difference-is-k/)

给定小写字母的字符串**和一个非负整数 **K** 。任务是找出给定字符串中 ASCII 值差正好为 **K** 的字符对的数量。
**举例:**** 

> **输入:** str = "abcdab "，K = 0
> **输出:** 2
> (a，a)和(b，b)是唯一有效的对。
> **输入:** str = "geeksforgeeks "，K = 1
> **输出:** 8
> (e，f)，(e，f)，(f，e)，(f，e)，(g，f)，
> (f，g)，(s，r)和(r，s)为有效对。

**方法:**将每个字符的频率存储在一个数组中。遍历这个频率数组，得到所需的答案。存在两种情况:

1.  如果 **K = 0** 则检查相似字符是否出现不止一次，即 **freq[i] > 1** 。如果是，则将**(频率[i] *(频率[I]–1))/2**添加到计数中。
2.  如果 **K！= 0** 然后检查是否存在两个 ASCII 值不同的字符，如 **K** 表示 **freq[i]** 和 **freq[j]** 。然后将 **freq[i] * freq[j]** 加到计数中。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define MAX 26

// Function to return the count of
// required pairs of characters
int countPairs(string str, int k)
{

    // Length of the string
    int n = str.size();

    // To store the frequency
    // of each character
    int freq[MAX];
    memset(freq, 0, sizeof freq);

    // Update the frequency
    // of each character
    for (int i = 0; i < n; i++)
        freq[str[i] - 'a']++;

    // To store the required
    // count of pairs
    int cnt = 0;

    // If ascii value difference is zero
    if (k == 0) {

        // If there exists similar characters
        // more than once
        for (int i = 0; i < MAX; i++)
            if (freq[i] > 1)
                cnt += ((freq[i] * (freq[i] - 1)) / 2);
    }
    else {

        // If there exits characters with
        // ASCII value difference as k
        for (int i = 0; i < MAX; i++)
            if (freq[i] > 0 && i + k < MAX && freq[i + k] > 0)
                cnt += (freq[i] * freq[i + k]);
        ;
    }

    // Return the required count
    return cnt;
}

// Driver code
int main()
{
    string str = "abcdab";
    int k = 0;

    cout << countPairs(str, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

    static int MAX = 26;

    // Function to return the count of
    // required pairs of characters
    static int countPairs(char[] str, int k)
    {

        // Length of the string
        int n = str.length;

        // To store the frequency
        // of each character
        int[] freq = new int[MAX];

        // Update the frequency
        // of each character
        for (int i = 0; i < n; i++)
        {
            freq[str[i] - 'a']++;
        }

        // To store the required
        // count of pairs
        int cnt = 0;

        // If ascii value difference is zero
        if (k == 0)
        {

            // If there exists similar characters
            // more than once
            for (int i = 0; i < MAX; i++)
            {
                if (freq[i] > 1)
                {
                    cnt += ((freq[i] * (freq[i] - 1)) / 2);
                }
            }
        }
        else
        {

            // If there exits characters with
            // ASCII value difference as k
            for (int i = 0; i < MAX; i++)
            {
                if (freq[i] > 0 && i + k < MAX && freq[i + k] > 0)
                {
                    cnt += (freq[i] * freq[i + k]);
                }
            }
            ;
        }

        // Return the required count
        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "abcdab";
        int k = 0;

        System.out.println(countPairs(str.toCharArray(), k));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 26

# Function to return the count of
# required pairs of characters
def countPairs(string, k) :

    # Length of the string
    n = len(string);

    # To store the frequency
    # of each character
    freq = [0] * MAX;

    # Update the frequency
    # of each character
    for i in range(n) :
        freq[ord(string[i]) -
             ord('a')] += 1;

    # To store the required
    # count of pairs
    cnt = 0;

    # If ascii value difference is zero
    if (k == 0) :

        # If there exists similar characters
        # more than once
        for i in range(MAX) :
            if (freq[i] > 1) :
                cnt += ((freq[i] *
                        (freq[i] - 1)) // 2);

    else :

        # If there exits characters with
        # ASCII value difference as k
        for i in range(MAX) :
            if (freq[i] > 0 and
                i + k < MAX and
                freq[i + k] > 0) :
                cnt += (freq[i] * freq[i + k]);

    # Return the required count
    return cnt;

# Driver code
if __name__ == "__main__" :

    string = "abcdab";
    k = 0;

    print(countPairs(string, k));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int MAX = 26;

    // Function to return the count of
    // required pairs of characters
    static int countPairs(char[] str, int k)
    {

        // Length of the string
        int n = str.Length;

        // To store the frequency
        // of each character
        int[] freq = new int[MAX];

        // Update the frequency
        // of each character
        for (int i = 0; i < n; i++)
        {
            freq[str[i] - 'a']++;
        }

        // To store the required
        // count of pairs
        int cnt = 0;

        // If ascii value difference is zero
        if (k == 0)
        {

            // If there exists similar characters
            // more than once
            for (int i = 0; i < MAX; i++)
            {
                if (freq[i] > 1)
                {
                    cnt += ((freq[i] * (freq[i] - 1)) / 2);
                }
            }
        }
        else
        {

            // If there exits characters with
            // ASCII value difference as k
            for (int i = 0; i < MAX; i++)
            {
                if (freq[i] > 0 && i + k < MAX && freq[i + k] > 0)
                {
                    cnt += (freq[i] * freq[i + k]);
                }
            }
            ;
        }

        // Return the required count
        return cnt;
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "abcdab";
        int k = 0;

        Console.WriteLine(countPairs(str.ToCharArray(), k));
    }
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

      // JavaScript implementation of the approach
      const MAX = 26;

      // Function to return the count of
      // required pairs of characters
      function countPairs(str, k) {
        // Length of the string
        var n = str.length;

        // To store the frequency
        // of each character
        var freq = new Array(MAX).fill(0);

        // Update the frequency
        // of each character
        for (var i = 0; i < n; i++) {
          freq[str[i].charCodeAt(0) -
          "a".charCodeAt(0)]++;
        }

        // To store the required
        // count of pairs
        var cnt = 0;

        // If ascii value difference is zero
        if (k === 0) {
          // If there exists similar characters
          // more than once
          for (var i = 0; i < MAX; i++) {
            if (freq[i] > 1) {
              cnt += (freq[i] * (freq[i] - 1)) / 2;
            }
          }
        } else {
          // If there exits characters with
          // ASCII value difference as k
          for (var i = 0; i < MAX; i++) {
            if (freq[i] > 0 && i + k < MAX &&
            freq[i + k] > 0) {
              cnt += freq[i] * freq[i + k];
            }
          }
        }

        // Return the required count
        return cnt;
      }

      // Driver code
      var str = "abcdab";
      var k = 0;

      document.write(countPairs(str.split(""), k));

</script>
```

**Output:** 

```
2
```