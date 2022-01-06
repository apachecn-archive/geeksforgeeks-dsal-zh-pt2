# 通过将元音变为辅音，使给定字符串中的所有字符相等，反之亦然

> 原文:[https://www . geesforgeks . org/通过将元音变辅音使给定字符串中的所有字符相等，反之亦然/](https://www.geeksforgeeks.org/make-all-characters-in-given-string-equal-by-changing-vowel-into-consonant-and-vice-versa/)

给定一个包含小写字符的字符串 **str** ，任务是找到使所有字符相等所需的最小操作数。在一个操作中，任何辅音都可以转换成任何元音，或者任何元音都可以转换成任何辅音。

**示例:**

> **输入:** str = "banana"
> **输出:** 3
> **解释:**将所有辅音转换为元音字符 A
> 
> **输入:** str = "hexon"
> **输出:** 5
> **解释:**先把 E 转换成 O，然后把所有的辅音都转换成字母 O

**方法:**这里的基本思路是:

*   将一个辅音变成另一个辅音或一个元音变成另一个元音所需的操作:2 操作
*   将辅音变成元音或元音变成辅音所需的操作:1 操作

所以，很明显，把一个辅音变成一个元音或者把一个元音变成一个辅音比把一个辅音变成另一个辅音或者把一个元音变成另一个元音更经济。

现在要解决这个问题，请按照以下步骤操作:

1.  计算所有字符的频率，找出频率最高的辅音和元音，我们分别说 **A** 和 **B** 。
2.  尝试将所有字符改为 **A** 和 **B** ，并将所需操作分别存储在变量 **minA** 和 **minB** 中。
3.  最小的 **minA** 和 **minB** 就是这个问题的答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum operations
// required to make all string characters equal
int minOperations(string str)
{
    int n = str.size();

    // Vector to store the
    // frequency of all characters
    vector<int> freq(26, 0);

    for (auto x : str) {
        freq[x - 'a']++;
    }

    int mxA = INT_MIN, mxB = INT_MIN;

    // Variables to store
    // consonant and vowel
    // with highest frequency
    char A, B;

    vector<char> vowels
        = { 'a', 'e', 'i', 'o', 'u' };

    for (int i = 0; i < 26; ++i) {
        bool isVowel = 0;
        for (auto x : vowels) {
            if ('a' + i == x) {
                isVowel = 1;
                break;
            }
        }

        // If current character is a vowel
        if (isVowel) {
            if (mxB < freq[i]) {
                mxB = freq[i];
                B = 'a' + i;
            }
        }

        // If currenct character is a consonant
        else {
            if (mxA < freq[i]) {
                mxA = freq[i];
                A = 'a' + i;
            }
        }
    }

    int minA = 0, minB = 0;
    for (auto x : str) {
        bool isVowel = 0;
        for (auto y : vowels) {
            if (x == y) {
                isVowel = 1;
                break;
            }
        }

        // If current character is a vowel
        if (isVowel) {
            if (x != B) {
                minB += 2;
            }
            minA += 1;
        }

        // If currenct character is a
        // consonant
        else {
            if (x != A) {
                minA += 2;
            }
            minB += 1;
        }
    }

    // If no vowel exists
    if (mxB == INT_MIN) {
        return minA;
    }

    // If no consonant exists
    if (mxA == INT_MIN) {
        return minB;
    }

    // Returning minimum of the two
    return min(minA, minB);
}

// Driver Code
int main()
{
    string str = "hexon";
    cout << minOperations(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG {

    // Function to return the minimum operations
    // required to make all string characters equal
    static int minOperations(String str)
    {
        int n = str.length();

        // Vector to store the
        // frequency of all characters
        char[] freq = new char[26];

        for(char x : str.toCharArray()) { freq[x - 'a']++; }

        int mxA = Integer.MIN_VALUE, mxB = Integer.MIN_VALUE;

        // Variables to store
        // consonant and vowel
        // with highest frequency
        char A = ' ', B = ' ';

        char[] vowels = { 'a', 'e', 'i', 'o', 'u' };

        for (int i = 0; i < 26; ++i) {
            int isVowel = 0;
            for(char x : vowels)
            {
                if ('a' + i == x) {
                    isVowel = 1;
                    break;
                }
            }

            // If current character is a vowel
            if (isVowel > 0) {
                if (mxB < freq[i]) {
                    mxB = freq[i];
                    B = (char)(97 + i);
                }
            }

            // If currenct character is a consonant
            else {
                if (mxA < freq[i]) {
                    mxA = freq[i];
                    A = (char)(97 + i);
                }
            }
        }

        int minA = 0, minB = 0;
        for(char x : str.toCharArray())
        {
            int isVowel = 0;
            for(char y : vowels)
            {
                if (x == y) {
                    isVowel = 1;
                    break;
                }
            }

            // If current character is a vowel
            if (isVowel > 0) {
                if (x != B) {
                    minB += 2;
                }
                minA += 1;
            }

            // If currenct character is a
            // consonant
            else {
                if (x != A) {
                    minA += 2;
                }
                minB += 1;
            }
        }

        // If no vowel exists
        if (mxB == Integer.MIN_VALUE) {
            return minA;
        }

        // If no consonant exists
        if (mxA == Integer.MIN_VALUE) {
            return minB;
        }

        // Returning minimum of the two
        return Math.min(minA, minB);
    }

    // Driver Code
    public static void main(String args[])
    {
        String str = "hexon";
        System.out.println(minOperations(str));
    }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# python program for the above approach
INT_MIN = -2147483647 - 1

# Function to return the minimum operations
# required to make all string characters equal
def minOperations(str):

    n = len(str)

    # Vector to store the
    # frequency of all characters
    freq = [0 for _ in range(26)]

    for x in str:
        freq[ord(x) - ord('a')] += 1

    mxA = INT_MIN
    mxB = INT_MIN

    # Variables to store
    # consonant and vowel
    # with highest frequency
    A = ''
    B = ''

    vowels = ['a', 'e', 'i', 'o', 'u']

    for i in range(0, 26):
        isVowel = 0

        for x in vowels:
            if (ord('a') + i == ord(x)):
                isVowel = 1
                break

        # If current character is a vowel
        if (isVowel):
            if (mxB < freq[i]):
                mxB = freq[i]
                B = chr(ord('a') + i)

        # If currenct character is a consonant
        else:
            if (mxA < freq[i]):
                mxA = freq[i]
                A = chr(ord('a') + i)

    minA = 0
    minB = 0
    for x in str:
        isVowel = 0
        for y in vowels:
            if (x == y):
                isVowel = 1
                break

        # If current character is a vowel
        if (isVowel):
            if (x != B):
                minB += 2
            minA += 1

            # If currenct character is a
            # consonant
        else:
            if (x != A):
                minA += 2
            minB += 1

        # If no vowel exists
    if (mxB == INT_MIN):
        return minA

        # If no consonant exists
    if (mxA == INT_MIN):
        return minB

        # Returning minimum of the two
    return min(minA, minB)

# Driver Code
if __name__ == "__main__":

    str = "hexon"
    print(minOperations(str))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to return the minimum operations
    // required to make all string characters equal
    static int minOperations(string str)
    {
        int n = str.Length;

        // Vector to store the
        // frequency of all characters
        char[] freq = new char[26];

        foreach(char x in str) { freq[x - 'a']++; }

        int mxA = Int32.MinValue, mxB = Int32.MinValue;

        // Variables to store
        // consonant and vowel
        // with highest frequency
        char A = ' ', B = ' ';

        char[] vowels = { 'a', 'e', 'i', 'o', 'u' };

        for (int i = 0; i < 26; ++i) {
            int isVowel = 0;
            foreach(char x in vowels)
            {
                if ('a' + i == x) {
                    isVowel = 1;
                    break;
                }
            }

            // If current character is a vowel
            if (isVowel > 0) {
                if (mxB < freq[i]) {
                    mxB = freq[i];
                    B = (char)(97 + i);
                }
            }

            // If currenct character is a consonant
            else {
                if (mxA < freq[i]) {
                    mxA = freq[i];
                    A = (char)(97 + i);
                }
            }
        }

        int minA = 0, minB = 0;
        foreach(char x in str)
        {
            int isVowel = 0;
            foreach(char y in vowels)
            {
                if (x == y) {
                    isVowel = 1;
                    break;
                }
            }

            // If current character is a vowel
            if (isVowel > 0) {
                if (x != B) {
                    minB += 2;
                }
                minA += 1;
            }

            // If currenct character is a
            // consonant
            else {
                if (x != A) {
                    minA += 2;
                }
                minB += 1;
            }
        }

        // If no vowel exists
        if (mxB == Int32.MinValue) {
            return minA;
        }

        // If no consonant exists
        if (mxA == Int32.MinValue) {
            return minB;
        }

        // Returning minimum of the two
        return Math.Min(minA, minB);
    }

    // Driver Code
    public static void Main()
    {
        string str = "hexon";
        Console.WriteLine(minOperations(str));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to return the minimum operations
// required to make all string characters equal
function minOperations(str) {
  let n = str.length;

  // Vector to store the
  // frequency of all characters
  let freq = new Array(26).fill(0);

  for (x of str) {
    freq[x.charCodeAt(0) - 'a'.charCodeAt(0)]++;
  }

  let mxA = Number.MIN_SAFE_INTEGER, mxB = Number.MIN_SAFE_INTEGER;

  // Variables to store
  // consonant and vowel
  // with highest frequency
  let A = "", B = "";

  let vowels = ['a', 'e', 'i', 'o', 'u'];

  for (let i = 0; i < 26; ++i) {
    let isVowel = 0;
    for (x of vowels) {
      if ('a'.charCodeAt(0) + i == x.charCodeAt(0)) {
        isVowel = 1;
        break;
      }
    }

    // If current character is a vowel
    if (isVowel) {
      if (mxB < freq[i]) {
        mxB = freq[i];
        B = String.fromCharCode('a'.charCodeAt(0) + i);
      }
    }

    // If currenct character is a consonant
    else {
      if (mxA < freq[i]) {
        mxA = freq[i];
        A = String.fromCharCode('a'.charCodeAt(0) + i);
      }
    }
  }

  let minA = 0, minB = 0;
  for (x of str) {
    let isVowel = 0;
    for (y of vowels) {
      if (x == y) {
        isVowel = 1;
        break;
      }
    }

    // If current character is a vowel
    if (isVowel) {
      if (x != B) {
        minB += 2;
      }
      minA += 1;
    }

    // If currenct character is a
    // consonant
    else {
      if (x != A) {
        minA += 2;
      }
      minB += 1;
    }
  }

  // If no vowel exists
  if (mxB == Number.MIN_SAFE_INTEGER) {
    return minA;
  }

  // If no consonant exists
  if (mxA == Number.MIN_SAFE_INTEGER) {
    return minB;
  }

  // Returning minimum of the two
  return Math.min(minA, minB);
}

// Driver Cod

let str = "hexon";
document.write(minOperations(str))

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
5
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)