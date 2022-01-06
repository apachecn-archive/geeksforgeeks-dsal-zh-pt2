# 具有回文置换的 K 大小子串的计数

> 原文:[https://www . geeksforgeeks . org/count-of-k-size-substrings-having-回文-置换/](https://www.geeksforgeeks.org/count-of-k-size-substrings-having-palindromic-permutations/)

给定字符串 **str** 仅由小写字母和整数 **K** 组成，任务是计算大小为 **K** 的子串的数量，使得子串的任何排列都是回文。

**示例:**

> **输入:**str = " abbca "，K = 3
> **输出:** 3
> **解释:**
> 大小 3 的置换为回文的子串有{“abb”、“bba”、“ACA”}。
> 
> **输入:** str = "aaaa "，K = 1
> **输出:** 4
> **解释:**
> 大小为 1 的置换为回文的子串有{'a '，' a '，' a '，' a'}。

**天真方法:**一个天真的解决方案是运行两个循环来[生成大小为 **K** 的所有子串](https://www.geeksforgeeks.org/program-print-substrings-given-string/)。对于形成的每个子串，找出子串中每个字符的频率。如果最多一个字符有奇数频率，那么它的一个[排列将是回文](https://www.geeksforgeeks.org/number-of-palindromic-permutations-set-1/)。增加当前子字符串的计数，并在所有操作后打印最终计数。

**时间复杂度:** *O(N*K)*

**有效方法:**这个问题可以通过使用[窗口滑动技术](https://www.geeksforgeeks.org/window-sliding-technique/)和使用大小为 **26** 的频率阵列来有效解决。以下是步骤:

1.  将给定字符串的第一个 **K** 元素的频率存储在一个频率数组中(比如 **freq[]** )。
2.  使用频率数组，检查具有奇数频率的元素的计数。如果**小于 2** ，则回文置换计数的增量。
3.  现在，向前线性滑动窗户，直到它到达终点。
4.  在每次迭代中，将窗口的第一个元素的计数减少 **1** ，将窗口的下一个元素的计数增加 **1** ，并再次检查具有奇数频率的频率阵列中的元素的计数。如果是**小于 2** ，则增加回文排列的计数。
5.  重复以上步骤，直到我们到达字符串的末尾，并打印回文排列的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// To store the frequency array
vector<int> freq(26);

// Function to check palindromic of
// of any substring using frequency array
bool checkPalindrome()
{

    // Initialise the odd count
    int oddCnt = 0;

    // Traversing frequency array to
    // compute the count of characters
    // having odd frequency
    for (auto x : freq) {

        if (x % 2 == 1)
            oddCnt++;
    }

    // Returns true if odd count is atmost 1
    return oddCnt <= 1;
}

// Function to count the total number
// substring whose any permutations
// are palindromic
int countPalindromePermutation(
    string s, int k)
{

    // Computing the frequency of
    // first K character of the string
    for (int i = 0; i < k; i++) {
        freq[s[i] - 97]++;
    }

    // To store the count of
    // palindromic permutations
    int ans = 0;

    // Checking for the current window
    // if it has any palindromic
    // permutation
    if (checkPalindrome()) {
        ans++;
    }

    // Start and end point of window
    int i = 0, j = k;

    while (j < s.size()) {

        // Sliding window by 1

        // Decrementing count of first
        // element of the window
        freq[s[i++] - 97]--;

        // Incrementing count of next
        // element of the window
        freq[s[j++] - 97]++;

        // Checking current window
        // character frequency count
        if (checkPalindrome()) {
            ans++;
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
int main()
{
    // Given string str
    string str = "abbaca";

    // Window of size K
    int K = 3;

    // Function Call
    cout << countPalindromePermutation(str, K)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// To store the frequency array
static int []freq = new int[26];

// Function to check palindromic of
// of any subString using frequency array
static boolean checkPalindrome()
{

    // Initialise the odd count
    int oddCnt = 0;

    // Traversing frequency array to
    // compute the count of characters
    // having odd frequency
    for(int x : freq)
    {
       if (x % 2 == 1)
           oddCnt++;
    }

    // Returns true if odd count
    // is atmost 1
    return oddCnt <= 1;
}

// Function to count the total number
// subString whose any permutations
// are palindromic
static int countPalindromePermutation(char []s,
                                      int k)
{

    // Computing the frequency of
    // first K character of the String
    for(int i = 0; i < k; i++)
    {
       freq[s[i] - 97]++;
    }

    // To store the count of
    // palindromic permutations
    int ans = 0;

    // Checking for the current window
    // if it has any palindromic
    // permutation
    if (checkPalindrome())
    {
        ans++;
    }

    // Start and end point of window
    int i = 0, j = k;

    while (j < s.length)
    {

        // Sliding window by 1

        // Decrementing count of first
        // element of the window
        freq[s[i++] - 97]--;

        // Incrementing count of next
        // element of the window
        freq[s[j++] - 97]++;

        // Checking current window
        // character frequency count
        if (checkPalindrome())
        {
            ans++;
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given String str
    String str = "abbaca";

    // Window of size K
    int K = 3;

    // Function Call
    System.out.print(countPalindromePermutation(
                     str.toCharArray(), K) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# To store the frequency array
freq = [0] * 26

# Function to check palindromic of
# of any substring using frequency array
def checkPalindrome():

    # Initialise the odd count
    oddCnt = 0

    # Traversing frequency array to
    # compute the count of characters
    # having odd frequency
    for x in freq:
        if (x % 2 == 1):
            oddCnt += 1

    # Returns true if odd count is atmost 1
    return oddCnt <= 1

# Function to count the total number
# substring whose any permutations
# are palindromic
def countPalindromePermutation(s, k):

    # Computing the frequency of
    # first K character of the string
    for i in range(k):
        freq[ord(s[i]) - 97] += 1

    # To store the count of
    # palindromic permutations
    ans = 0

    # Checking for the current window
    # if it has any palindromic
    # permutation
    if (checkPalindrome()):
        ans += 1

    # Start and end point of window
    i = 0
    j = k

    while (j < len(s)):

        # Sliding window by 1

        # Decrementing count of first
        # element of the window
        freq[ord(s[i]) - 97] -= 1
        i += 1

        # Incrementing count of next
        # element of the window
        freq[ord(s[j]) - 97] += 1
        j += 1

        # Checking current window
        # character frequency count
        if (checkPalindrome()):
            ans += 1

    # Return the final count
    return ans

# Driver Code

# Given string str
str = "abbaca"

# Window of size K
K = 3

# Function call
print(countPalindromePermutation(str, K))

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// To store the frequency array
static int []freq = new int[26];

// Function to check palindromic of
// of any subString using frequency array
static bool checkPalindrome()
{

    // Initialise the odd count
    int oddCnt = 0;

    // Traversing frequency array to
    // compute the count of characters
    // having odd frequency
    foreach(int x in freq)
    {
        if (x % 2 == 1)
            oddCnt++;
    }

    // Returns true if odd count
    // is atmost 1
    return oddCnt <= 1;
}

// Function to count the total number
// subString whose any permutations
// are palindromic
static int countPalindromePermutation(char []s,
                                      int k)
{
    int i = 0;

    // Computing the frequency of
    // first K character of the String
    for(i = 0; i < k; i++)
    {
       freq[s[i] - 97]++;
    }

    // To store the count of
    // palindromic permutations
    int ans = 0;

    // Checking for the current window
    // if it has any palindromic
    // permutation
    if (checkPalindrome())
    {
        ans++;
    }

    // Start and end point of window
    int j = k;
        i = 0;

    while (j < s.Length)
    {

        // Sliding window by 1

        // Decrementing count of first
        // element of the window
        freq[s[i++] - 97]--;

        // Incrementing count of next
        // element of the window
        freq[s[j++] - 97]++;

        // Checking current window
        // character frequency count
        if (checkPalindrome())
        {
            ans++;
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given String str
    String str = "abbaca";

    // Window of size K
    int K = 3;

    // Function Call
    Console.Write(countPalindromePermutation(
                  str.ToCharArray(), K) + "\n");
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// To store the frequency array
var freq = Array(26).fill(0);

// Function to check palindromic of
// of any substring using frequency array
function checkPalindrome()
{

    // Initialise the odd count
    var oddCnt = 0;

    // Traversing frequency array to
    // compute the count of characters
    // having odd frequency
    freq.forEach(x => {

        if (x % 2 == 1)
            oddCnt++;
    });

    // Returns true if odd count is atmost 1
    return oddCnt <= 1;
}

// Function to count the total number
// substring whose any permutations
// are palindromic
function countPalindromePermutation( s, k)
{

    // Computing the frequency of
    // first K character of the string
    for (var i = 0; i < k; i++) {
        freq[s[i].charCodeAt(0) - 97]++;
    }

    // To store the count of
    // palindromic permutations
    var ans = 0;

    // Checking for the current window
    // if it has any palindromic
    // permutation
    if (checkPalindrome()) {
        ans++;
    }

    // Start and end point of window
    var i = 0, j = k;

    while (j < s.length) {

        // Sliding window by 1

        // Decrementing count of first
        // element of the window
        freq[s[i++].charCodeAt(0) - 97]--;

        // Incrementing count of next
        // element of the window
        freq[s[j++].charCodeAt(0) - 97]++;

        // Checking current window
        // character frequency count
        if (checkPalindrome()) {
            ans++;
        }
    }

    // Return the final count
    return ans;
}

// Driver Code
// Given string str
var str = "abbaca";
// Window of size K
var K = 3;
// Function Call
document.write( countPalindromePermutation(str, K));

</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*