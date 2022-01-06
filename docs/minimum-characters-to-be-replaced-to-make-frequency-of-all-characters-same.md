# 为使所有字符的频率相同，需要替换的最少字符数

> 原文:[https://www . geesforgeks . org/最少要替换的字符-使所有字符的频率相同/](https://www.geeksforgeeks.org/minimum-characters-to-be-replaced-to-make-frequency-of-all-characters-same/)

给定一个由字母**[' A '–' Z ']**组成的字符串 **S** ，任务是找到使每个字符的频率相等所需的最小操作数。在一个操作中，可以选择字符串中的任何字符，并用另一个有效字符替换。
**例:**

> **输入:** S = "ABCB"
> **输出:** 1
> **说明:**
> 在给定的字符串中，字符‘C’可以用‘A’代替，这样每个字符的出现次数就等于 2。
> 更新字符串=“ABAB”
> **输入:**S =“BBC”
> **输出:** 1
> **说明:**
> 在给定的字符串中，字符‘C’可以替换为‘B’，这样每个字符的出现次数就变成等于 3。
> 更新字符串=“BBB”

**方法:**思路是[找到字符串](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)中每个字符的频率，然后[按照频率降序排列字符](https://www.geeksforgeeks.org/sort-elements-by-frequency/)。最后，我们可以检查字符串中的每一个字符，它会产生最小数量的要更改的字符，并打印这个最小数量的要更改的字符。
以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// Minimum characters to be replaced
// to make frequency of all characters same

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// Minimum operations to convert
// given string to another with
// equal frequencies of characters
int minOperations(string s)
{
    // Frequency of characters
    int freq[26] = { 0 };
    int n = s.length();

    // Loop to find the Frequency
    // of each character
    for (int i = 0; i < n; i++) {
        freq[s[i] - 'A']++;
    }

    // Sort in decreasing order
    // based on frequency
    sort(freq, freq + 26, greater<int>());

    // Maximum possible answer
    int answer = n;

    // Loop to find the minimum operations
    // required such that frequency of
    // every character is equal
    for (int i = 1; i <= 26; i++) {
        if (n % i == 0) {
            int x = n / i;
            int y = 0;
            for (int j = 0; j < i; j++) {
                y += min(freq[j], x);
            }
            answer = min(answer, n - y);
        }
    }
    return answer;
}

// Driver Code
int main()
{
    string s = "BBC";
    cout << minOperations(s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// Minimum characters to be replaced
// to make frequency of all characters same

import java.util.*;

class GFG{

// Function to find the
// Minimum operations to convert
// given String to another with
// equal frequencies of characters
static int minOperations(String s)
{
    // Frequency of characters
    Integer freq[] = new Integer[26];
    Arrays.fill(freq, 0);
    int n = s.length();

    // Loop to find the Frequency
    // of each character
    for (int i = 0; i < n; i++) {
        freq[s.charAt(i) - 'A']++;
    }

    // Sort in decreasing order
    // based on frequency
    Arrays.sort(freq, Collections.reverseOrder());

    // Maximum possible answer
    int answer = n;

    // Loop to find the minimum operations
    // required such that frequency of
    // every character is equal
    for (int i = 1; i <= 26; i++) {
        if (n % i == 0) {
            int x = n / i;
            int y = 0;
            for (int j = 0; j < i; j++) {
                y += Math.min(freq[j], x);
            }
            answer = Math.min(answer, n - y);
        }
    }
    return answer;
}

// Driver Code
public static void main(String[] args)
{
    String s = "BBC";
    System.out.print(minOperations(s));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum characters to be replaced
# to make frequency of all characters same

# Function to find the minimum
# operations to convert given
# string to another with equal
# frequencies of characters
def minOperations(s):

    # Frequency of characters
    freq = [0] * 26
    n = len(s)

    # Loop to find the Frequency
    # of each character
    for i in range(n):
        freq[ord(s[i]) - ord('A')] += 1

    # Sort in decreasing order
    # based on frequency
    freq.sort(reverse = True)

    # Maximum possible answer
    answer = n

    # Loop to find the minimum operations
    # required such that frequency of
    # every character is equal
    for i in range(1, 27):
        if (n % i == 0):
            x = n // i
            y = 0

            for j in range(i):
                y += min(freq[j], x)

            answer = min(answer, n - y)

    return answer

# Driver Code
if __name__ == "__main__":

    s = "BBC"

    print (minOperations(s))

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find the minimum
// characters to be replaced to make
// frequency of all characters same
using System;

class GFG{

// Function to find the minimum
// operations to convert given
// string to another with equal
// frequencies of characters
static int minOperations(String s)
{

    // Frequency of characters
    int []freq = new int[26];
    int n = s.Length;

    // Loop to find the frequency
    // of each character
    for(int i = 0; i < n; i++)
    {
       freq[s[i] - 'A']++;
    }

    // Sort in decreasing order
    // based on frequency
    Array.Sort(freq);
    Array.Reverse(freq);

    // Maximum possible answer
    int answer = n;

    // Loop to find the minimum operations
    // required such that frequency of
    // every character is equal
    for(int i = 1; i <= 26; i++)
    {
       if (n % i == 0)
       {
           int x = n / i;
           int y = 0;

           for(int j = 0; j < i; j++)
           {
              y += Math.Min(freq[j], x);
           }
           answer = Math.Min(answer, n - y);
       }
    }
    return answer;
}

// Driver Code
public static void Main(String[] args)
{
    String s = "BBC";

    Console.Write(minOperations(s));

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

      // JavaScript implementation to find the minimum
      // characters to be replaced to make
      // frequency of all characters same

      // Function to find the minimum
      // operations to convert given
      // string to another with equal
      // frequencies of characters
      function minOperations(s) {
        // Frequency of characters
        var freq = new Array(26).fill(0);
        var n = s.length;

        // Loop to find the frequency
        // of each character
        for (var i = 0; i < n; i++) {
          freq[s[i].charCodeAt(0) -
          "A".charCodeAt(0)]++;
        }

        // Sort in decreasing order
        // based on frequency
        freq.sort((a, b) => b - a);

        // Maximum possible answer
        var answer = n;

        // Loop to find the minimum operations
        // required such that frequency of
        // every character is equal
        for (var i = 1; i <= 26; i++) {
          if (n % i === 0) {
            var x = n / i;
            var y = 0;

            for (var j = 0; j < i; j++) {
              y += Math.min(freq[j], x);
            }
            answer = Math.min(answer, n - y);
          }
        }
        return answer;
      }

      // Driver Code
      var s = "BBC";
      document.write(minOperations(s));

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(n)*

***辅助空间:** O(26)*