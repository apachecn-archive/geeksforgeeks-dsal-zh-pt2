# 计算环绕字符串中出现的字符串 S 的唯一子字符串

> 原文:[https://www . geesforgeks . org/count-unique-substrings-of-string-s-present-in-a-wrap-string/](https://www.geeksforgeeks.org/count-unique-substrings-of-a-string-s-present-in-a-wraparound-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，它是字符串**“abcdefghijklmnopqrstuvwxyz”**的无限环绕字符串，任务是计算在 **s** 中存在的字符串 **p** 的唯一非空子字符串的数量。

**示例:**

> **输入:** S = "zab"
> **输出:** 6
> **解释:**所有可能的子串都是“z”、“a”、“b”、“za”、“ab”、“zab”。
> 
> **输入:** S = "cac"
> **输出:** 2
> **解释:**所有可能的子串只有“a”和“c”。

**方法:**按照以下步骤解决问题

1.  [迭代字符串的每个字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)
2.  初始化一个大小为 **26** 的辅助[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，以存储从字符串 **P** 的每个字符开始的字符串 **S** 中存在的[子字符串](https://www.geeksforgeeks.org/substring-in-java/)的当前长度。
3.  初始化一个变量，比如**柯林**，它存储存在于 **P** 中的[子串](https://www.geeksforgeeks.org/substring-in-cpp/)的长度，如果当前字符不是前一个子串的一部分，则包括当前字符。
4.  初始化一个变量，比如说**和**，来存储 **S** 中存在的 **p** 的非空子串的唯一计数。
5.  [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)的字符，检查以下两种情况:
    *   检查当前字符是否可以与前一个子串相加，形成所需的子串。
    *   如果**(柯林+ 1)** 大于 **arr[curr]** ，则将**柯林**和 **arr[curr]** 之差加到 **ans** 上，避免子串重复。
6.  打印**和**的值。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of
// non-empty substrings of p present in s
int findSubstringInWraproundString(string p)
{
    // Stores the required answer
    int ans = 0;

    // Stores the length of
    // substring present in p
    int curLen = 0;

    // Stores the current length
    // of substring that is
    // present in string s starting
    // from each character of p
    int arr[26] = { 0 };

    // Iterate over the characters of the string
    for (int i = 0; i < (int)p.length(); i++) {

        int curr = p[i] - 'a';

        // Check if the current character
        // can be added with previous substring
        // to form the required substring
        if (i > 0
            && (p[i - 1]
                != ((curr + 26 - 1) % 26 + 'a'))) {
            curLen = 0;
        }

        // Increment current length
        curLen++;

        if (curLen > arr[curr]) {

            // To avoid repetition
            ans += (curLen - arr[curr]);

            // Update arr[cur]
            arr[curr] = curLen;
        }
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    string p = "zab";

    // Function call to find the
    // count of non-empty substrings
    // of p present in s
    findSubstringInWraproundString(p);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
class GFG
{

    // Function to find the count of
    // non-empty substrings of p present in s
    static void findSubstringInWraproundString(String p)
    {

        // Stores the required answer
        int ans = 0;

        // Stores the length of
        // substring present in p
        int curLen = 0;

        // Stores the current length
        // of substring that is
        // present in string s starting
        // from each character of p
        int arr[] = new int[26];

        // Iterate over the characters of the string
        for (int i = 0; i < p.length(); i++)
        {

            int curr = p.charAt(i) - 'a';

            // Check if the current character
            // can be added with previous substring
            // to form the required substring
            if (i > 0
                && (p.charAt(i - 1)
                    != ((curr + 26 - 1) % 26 + 'a')))
            {
                curLen = 0;
            }

            // Increment current length
            curLen++;
            if (curLen > arr[curr])
            {

                // To avoid repetition
                ans += (curLen - arr[curr]);

                // Update arr[cur]
                arr[curr] = curLen;
            }
        }

        // Print the answer
        System.out.println(ans);
    }

    // Driver Code
    public static void main(String args[])
    {
        String p = "zab";

        // Function call to find the
        // count of non-empty substrings
        // of p present in s
        findSubstringInWraproundString(p);
    }
}

// This code is contributed by hemanth gadarla
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to find the count of
# non-empty substrings of p present in s
def findSubstringInWraproundString(p) :

    # Stores the required answer
    ans = 0

    # Stores the length of
    # substring present in p
    curLen = 0

    # Stores the current length
    # of substring that is
    # present in string s starting
    # from each character of p
    arr = [0]*26

    # Iterate over the characters of the string
    for i in range(0, len(p)) :

        curr = ord(p[i]) - ord('a')

        # Check if the current character
        # can be added with previous substring
        # to form the required substring
        if (i > 0 and (ord(p[i - 1]) != ((curr + 26 - 1) % 26 + ord('a')))) :
            curLen = 0

        # Increment current length
        curLen += 1

        if (curLen > arr[curr]) :

            # To avoid repetition
            ans += (curLen - arr[curr])

            # Update arr[cur]
            arr[curr] = curLen

    # Print the answer
    print(ans)

p = "zab"

# Function call to find the
# count of non-empty substrings
# of p present in s
findSubstringInWraproundString(p)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program for
// the above approach
using System;
class GFG
{

  // Function to find the count of
  // non-empty substrings of p present in s
  static void findSubstringInWraproundString(string p)
  {

    // Stores the required answer
    int ans = 0;

    // Stores the length of
    // substring present in p
    int curLen = 0;

    // Stores the current length
    // of substring that is
    // present in string s starting
    // from each character of p
    int[] arr = new int[26];

    // Iterate over the characters of the string
    for (int i = 0; i < (int)p.Length; i++)
    {
      int curr = p[i] - 'a';

      // Check if the current character
      // can be added with previous substring
      // to form the required substring
      if (i > 0 && (p[i - 1] != ((curr + 26 - 1) % 26 + 'a')))
      {
        curLen = 0;
      }

      // Increment current length
      curLen++;
      if (curLen > arr[curr])
      {

        // To avoid repetition
        ans += (curLen - arr[curr]);

        // Update arr[cur]
        arr[curr] = curLen;
      }
    }

    // Print the answer
    Console.Write(ans);
  }

  // Driver code
  static void Main()
  {
    string p = "zab";

    // Function call to find the
    // count of non-empty substrings
    // of p present in s
    findSubstringInWraproundString(p);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

      // Function to find the count of
    // non-empty substrings of p present in s
    function findSubstringInWraproundString(p)
    {

      // Stores the required answer
      let ans = 0;

      // Stores the length of
      // substring present in p
      let curLen = 0;

      // Stores the current length
      // of substring that is
      // present in string s starting
      // from each character of p
      let arr = new Array(26);
      arr.fill(0);

      // Iterate over the characters of the string
      for (let i = 0; i < p.length; i++)
      {
        let curr = p[i].charCodeAt() - 'a'.charCodeAt();

        // Check if the current character
        // can be added with previous substring
        // to form the required substring
        if (i > 0 && (p[i - 1].charCodeAt() != ((curr + 26 - 1) % 26 + 'a'.charCodeAt())))
        {
          curLen = 0;
        }

        // Increment current length
        curLen++;
        if (curLen > arr[curr])
        {

          // To avoid repetition
          ans += (curLen - arr[curr]);

          // Update arr[cur]
          arr[curr] = curLen;
        }
      }

      // Print the answer
      document.write(ans);
    }

    let p = "zab";

    // Function call to find the
    // count of non-empty substrings
    // of p present in s
    findSubstringInWraproundString(p);

  // This code is contributed by surehs07.
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)