# 每个字符的频率最多为 X，长度至少为 Y 的字符串数

> 原文:[https://www . geeksforgeeks . org/最多 x 个字符且长度至少为 y 的字符串计数/](https://www.geeksforgeeks.org/count-of-strings-with-frequency-of-each-character-at-most-x-and-length-at-least-y/)

给定字符串和整数的数组**arr[]****X**和 **Y** ，任务是找出每个字符**的**频率最多为 X****且字符串**的**长度至少为 Y** 的字符串数。**

**示例:**

> **输入:**arr[]= {“ab”、“derdee”、“erre”}，X = 2，Y = 4
> **输出:** 1
> **说明:**字符频率最多为 2、
> 长度至少为 4 的字符串为“erre”。因此计数为 1
> 
> **输入:** arr[] = {"ag "，" ka "，" nanana " }，X = 3，Y = 2
> **输出:** 3

**方法:**按照下面提到的方法解决问题:

*   遍历字符串数组，并对每个字符串执行以下步骤。
*   创建字符的**频率图**。
*   每当任何字符的频率**大于 X、**或长度**小于 Y** 、**时，跳过当前字符串。**
*   如果没有字符的频率超过 X，长度至少为 Y，**增加答案的计数**。
*   遍历所有字符串时，返回存储在答案中的计数。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to check if
// the string has
// frequency of each character
// less than X
bool isValid(string s, int X)
{
    vector<int> freq(26, 0);

    // Loop to check the frequency
    // of each character in the string
    for (char c : s) {
        freq++;
    }

    // Loop to check
    // if the frequency of all characters
    // are at most X
    for (int i = 0; i < 26; i++)
        if (freq[i] > X)
            return false;
    return true;
}

// Function to calculate the count of strings
int getCount(vector<string>& arr, int X, int Y)
{
    int ans = 0;

    // Loop to iterate the string array
    for (string st : arr) {
        if (isValid(st, X) && st.length() >= Y) {
            ans++;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    vector<string> arr = { "ab", "derdee", "erre" };
    int X = 2, Y = 4;

    // Function call to get count for arr[]
    cout << getCount(arr, X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

  // Function to check if
  // the string has
  // frequency of each character
  // less than X
  static boolean isValid(String s, int X)
  {
    int freq[] = new int[26];

    // Loop to check the frequency
    // of each character in the string
    for (int i=0;i<s.length();i++) {
      char c = s.charAt(i);
      freq++;
    }

    // Loop to check
    // if the frequency of all characters
    // are at most X
    for (int i = 0; i < 26; i++)
      if (freq[i] > X)
        return false;
    return true;
  }

  // Function to calculate the count of strings
  static int getCount(String[] arr, int X, int Y)
  {
    int ans = 0;

    // Loop to iterate the string array
    for (String st : arr) {
      if (isValid(st, X) && st.length() >= Y) {
        ans++;
      }
    }
    return ans;
  }

  // Driver Code
  public static void main (String[] args)
  {
    String arr[] = { "ab", "derdee", "erre" };
    int X = 2, Y = 4;

    // Function call to get count for arr[]

    System.out.println(getCount(arr, X, Y));
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Function to check if
# the string has
# frequency of each character
# less than X
def isValid (s, X) :
    freq = [0] * 26

    # Loop to check the frequency
    # of each character in the string
    for c in s:
        freq[ord(c)  - ord("a")] += 1

    # Loop to check
    # if the frequency of all characters
    # are at most X
    for i in range(26):
        if (freq[i] > X):
            return False
    return True

# Function to calculate the count of strings
def getCount (arr, X, Y):
    ans = 0

    # Loop to iterate the string array
    for st in arr:
        if (isValid(st, X) and len(st) >= Y):
            ans += 1
    return ans

# Driver Code

arr = ["ab", "derdee", "erre"]
X = 2
Y = 4

# Function call to get count for arr[]
print(getCount(arr, X, Y))

# This code is contributed by gfgking.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to check if the string
// has frequency of each character
// less than X
static bool isValid(String s, int X)
{
    int []freq = new int[26];

    // Loop to check the frequency
    // of each character in the string
    for(int i = 0; i < s.Length; i++)
    {
        char c = s[i];
        freq++;
    }

    // Loop to check if the frequency
    // of all characters are at most X
    for(int i = 0; i < 26; i++)
        if (freq[i] > X)
            return false;

        return true;
}

// Function to calculate the count of strings
static int getCount(String[] arr, int X, int Y)
{
    int ans = 0;

    // Loop to iterate the string array
    foreach (String st in arr)
    {
        if (isValid(st, X) && st.Length >= Y)
        {
            ans++;
        }
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    String []arr = { "ab", "derdee", "erre" };
    int X = 2, Y = 4;

    // Function call to get count for []arr
    Console.WriteLine(getCount(arr, X, Y));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

    // Function to check if
    // the string has
    // frequency of each character
    // less than X
    const isValid = (s, X) => {
        let freq = new Array(26).fill(0);

        // Loop to check the frequency
        // of each character in the string
        for (let c in s) {
            freq[s.charCodeAt(c) - "a".charCodeAt(0)]++;
        }

        // Loop to check
        // if the frequency of all characters
        // are at most X
        for (let i = 0; i < 26; i++)
            if (freq[i] > X)
                return false;
        return true;
    }

    // Function to calculate the count of strings
    const getCount = (arr, X, Y) => {
        let ans = 0;

        // Loop to iterate the string array
        for (let st in arr) {
            if (isValid(arr[st], X) && arr[st].length >= Y) {
                ans++;
            }
        }
        return ans;
    }

    // Driver Code

    let arr = ["ab", "derdee", "erre"];
    let X = 2, Y = 4;

    // Function call to get count for arr[]
    document.write(getCount(arr, X, Y));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
1
```

**时间复杂度:** O(N*M)，其中 N 是数组的大小，M 是最长字符串的大小
T3】辅助空间: O(1)