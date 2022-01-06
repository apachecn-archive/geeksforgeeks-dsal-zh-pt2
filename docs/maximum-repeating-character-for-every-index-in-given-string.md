# 给定字符串中每个索引的最大重复字符数

> 原文:[https://www . geesforgeks . org/给定字符串中每个索引的最大重复字符数/](https://www.geeksforgeeks.org/maximum-repeating-character-for-every-index-in-given-string/)

给定由小写字母组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，任务是为字符串的每个字符找到[最大重复字符](https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/)。如果对于任何索引，一个以上的字符出现了最大次数，则打印最近出现的字符。

**示例:**

> **输入:** str = "abbc"
> **输出:**
> a->1
> B->1
> B->2
> B->2
> **解释:**
> str[0] = 'a '。因此，打印 a - > 1。
> str[1] = 'b '。现在 a 和 b 的频率相等。因为，‘b’是最近出现的字符，打印 b - > 1。
> str[2] = 'b '。因为‘b’是重复次数最多的字符，所以打印 b - > 2。
> str[3] = 'c '。因为‘b’是重复次数最多的字符，所以打印 b - > 2。
> 
> **输入:**str = " htdddg "
> T3】输出:h->1
> t->1
> d->1
> d->2
> d->3
> d->3

**方法:**按照下面给出的步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如 **freq[]** 来存储字符串中每个不同字符的[频率。](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)
*   初始化两个变量，说 **max** 、 **charMax** 分别存储最大重复字符的[频率和](https://www.geeksforgeeks.org/maximum-repeated-frequency-of-characters-in-a-given-string/)[最大重复字符](https://www.geeksforgeeks.org/return-maximum-occurring-character-in-the-input-string/)。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并更新当前字符的频率，更新 **max** 和 **charMax 的值。**
*   最后，在每次字符遍历后打印 **charMax** 和 **max** 的值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the
// maximum repeating
// character at each index
// of the String
void findFreq(string str,
              int N)
{
  // Stores frequency of
  // each distinct character
  int freq[256];

  memset(freq, 0,
         sizeof(freq));

  // Stores frequency of
  // maximum repeating
  // character
  int max = 0;

  // Stores the character having
  // maximum frequency
  char charMax = '0';

  // Traverse the String
  for (int i = 0; i < N; i++)
  {
    // Stores current character
    char ch = str[i];

    // Update the frequency of str[i]
    freq[ch]++;

    // If frequency of current
    // character exceeds max
    if (freq[ch] >= max)
    {
      // Update max
      max = freq[ch];

      // Update charMax
      charMax = ch;
    }

    // Print the required output
    cout<< charMax << "->" <<
           max << endl;
  }
}

// Driver Code
int main()
{
  string str = "abbc";

  // Stores length of str
  int N = str.size();

  findFreq(str, N);
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;

public class GFG {

    // Function to print the maximum repeating
    // character at each index of the string
    public static void findFreq(String str,
                                int N)
    {

        // Stores frequency of
        // each distinct character
        int[] freq = new int[256];

        // Stores frequency of maximum
        // repeating character
        int max = 0;

        // Stores the character having
        // maximum frequency
        char charMax = '0';

        // Traverse the string
        for (int i = 0; i < N; i++) {

            // Stores current character
            char ch = str.charAt(i);

            // Update the frequency of str[i]
            freq[ch]++;

            // If frequency of current
            // character exceeds max
            if (freq[ch] >= max) {

                // Update max
                max = freq[ch];

                // Update charMax
                charMax = ch;
            }

            // Print the required output
            System.out.println(
                charMax + " -> " + max);
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String str = "abbc";

        // Stores length of str
        int N = str.length();

        findFreq(str, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print the maximum repeating
# character at each index of the string
def findFreq(strr, N):

    # Stores frequency of
    # each distinct character
    freq = [0] * 256

    # Stores frequency of maximum
    # repeating character
    max = 0

    # Stores the character having
    # maximum frequency
    charMax = '0'

    # Traverse the string
    for i in range(N):

        # Stores current character
        ch = ord(strr[i])

        # Update the frequency of strr[i]
        freq[ch] += 1

        # If frequency of current
        # character exceeds max
        if (freq[ch] >= max):

            # Update max
            max = freq[ch]

            # Update charMax
            charMax = ch

        # Print the required output
        print(chr(charMax), "->", max)

# Driver Code
if __name__ == '__main__':

    strr = "abbc"

    # Stores length of strr
    N = len(strr)

    findFreq(strr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to print the maximum repeating
// character at each index of the string
public static void findFreq(String str,
                            int N)
{
  // Stores frequency of
  // each distinct character
  int[] freq = new int[256];

  // Stores frequency of maximum
  // repeating character
  int max = 0;

  // Stores the character having
  // maximum frequency
  char charMax = '0';

  // Traverse the string
  for (int i = 0; i < N; i++)
  {
    // Stores current character
    char ch = str[i];

    // Update the frequency of
    // str[i]
    freq[ch]++;

    // If frequency of current
    // character exceeds max
    if (freq[ch] >= max)
    {
      // Update max
      max = freq[ch];

      // Update charMax
      charMax = ch;
    }

    // Print the required output
    Console.WriteLine(charMax +
                      " -> " + max);
  }
}

// Driver Code
public static void Main(String[] args)
{
  String str = "abbc";

  // Stores length of str
  int N = str.Length;

  findFreq(str, N);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript Program to implement
// the above approach

// Function to print the
// maximum repeating
// character at each index
// of the String
function findFreq(str, N) {
    // Stores frequency of
    // each distinct character
    let freq = new Array(256).fill(0);

    // Stores frequency of
    // maximum repeating
    // character
    let max = 0;

    // Stores the character having
    // maximum frequency
    let charMax = '0';

    // Traverse the String
    for (let i = 0; i < N; i++) {
        // Stores current character
        let ch = str[i].charCodeAt(0);

        // Update the frequency of str[i]
        freq[ch]++;

        // If frequency of current
        // character exceeds max
        if (freq[ch] >= max) {
            // Update max
            max = freq[ch];

            // Update charMax
            charMax = ch;
        }

        // Print the required output
        document.write(String.fromCharCode(charMax) + "->" +
        max + "<br>");
    }
}

// Driver Code

let str = "abbc";

// Stores length of str
let N = str.length;

findFreq(str, N);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
a -> 1
b -> 1
b -> 2
b -> 2
```

***时间复杂度** : O(N)*
***辅助空间:** O(1)*