# 允许奇数和偶数变化的不同字符串

> 原文:[https://www . geesforgeks . org/distinct-strings-奇数-偶数-允许更改/](https://www.geeksforgeeks.org/distinct-strings-odd-even-changes-allowed/)

给定一个小写字符串数组，任务是找出不同字符串的数量。如果在一个字符串上应用以下操作时，无法形成第二个字符串，则两个字符串是不同的。

*   奇数索引上的一个字符只能与奇数索引上的另一个字符交换。
*   偶数索引中的一个字符只能与偶数索引中的另一个字符交换。

**示例:**

```
Input  : arr[] = {"abcd", "cbad", "bacd"}
Output : 2
The 2nd string can be converted to the 1st by swapping 
the first and third characters. So there are 2 distinct 
```

```
strings as the third string cannot be converted to the 
first.

Input  : arr[] = {"abc", "cba"}
Output : 1 
```

一个**简单的解决方案**是运行两个循环。外部循环挑选一个字符串，内部循环检查是否有一个先前的字符串可以通过允许的转换转换为当前的字符串。该解决方案需要 O(n <sup>2</sup> m)时间，其中 n 是字符串的数量，m 是任何字符串中的最大字符数。

一个有效的解决方案为每个输入字符串生成一个编码字符串。编码后的计数包含由分隔符分隔的偶数和奇数位置的字符。如果两个字符串的编码字符串相同，则视为不同，否则视为不同。一旦我们有了编码字符串的方法，问题就简化为计算不同的编码字符串。这是典型的哈希问题。我们创建一个散列集，并一个接一个地存储字符串的编码。如果编码已经存在，我们将忽略该字符串。否则，我们将编码存储在散列和不同字符串的增量计数中。

## C++

```
#include<bits/stdc++.h>
using namespace std;

int MAX_CHAR = 26;

    string encodeString(char str[], int m) {
        // hashEven stores the count of even indexed character
        // for each string hashOdd stores the count of odd
        // indexed characters for each string
        int hashEven[MAX_CHAR];
        int hashOdd[MAX_CHAR];

        // creating hash for each string
        for (int i = 0; i < m; i++) {
            char c = str[i];
            if ((i & 1) != 0) // If index of current character is odd
                hashOdd[c-'a']++;
            else
                hashEven[c-'a']++;

        }

        // For every character from 'a' to 'z', we store its
        // count at even position followed by a separator,
        // followed by count at odd position.
        string encoding = "";
        for (int i = 0; i < MAX_CHAR; i++) {
            encoding += (hashEven[i]);
            encoding += ('-');
            encoding += (hashOdd[i]);
            encoding += ('-');
        }
        return encoding;
    }

    // This function basically uses a hashing based set to
// store strings which are distinct according to according
// to criteria given in question.
    int countDistinct(string input[], int n) {
        int countDist = 0; // Initialize result

        // Create an empty set and store all distinct
        // strings in it.
        set<string> s;
        for (int i = 0; i < n; i++) {
            // If this encoding appears first time, increment
            // count of distinct encodings.
              char char_array[input[i].length()+1];
              strcpy(char_array, input[i].c_str());
            if (s.find(encodeString(char_array, input[i].length()+1)) == s.end()) {
                s.insert(encodeString(char_array,input[i].length()+1));
                countDist++;
            }
        }

        return countDist;
    }

// Driver code
    int main() {
        string input[] = {"abcd", "acbd", "adcb", "cdba",
                "bcda", "badc"};
        int n = sizeof(input)/sizeof(input[0]);

        cout << countDistinct(input, n) << "\n";
    }

// This code is contributed by NishaBharti.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count distinct strings with
// even odd swapping allowed.
import java.util.HashSet;
import java.util.Set;
class GFG {
static int MAX_CHAR = 26;

    static String encodeString(char[] str) {
        // hashEven stores the count of even indexed character
        // for each string hashOdd stores the count of odd
        // indexed characters for each string
        int hashEven[] = new int[MAX_CHAR];
        int hashOdd[] = new int[MAX_CHAR];

        // creating hash for each string
        for (int i = 0; i < str.length; i++) {
            char c = str[i];
            if ((i & 1) != 0) // If index of current character is odd
                hashOdd[c-'a']++;
            else
                hashEven[c-'a']++;

        }

        // For every character from 'a' to 'z', we store its
        // count at even position followed by a separator,
        // followed by count at odd position.
        String encoding = "";
        for (int i = 0; i < MAX_CHAR; i++) {
            encoding += (hashEven[i]);
            encoding += ('-');
            encoding += (hashOdd[i]);
            encoding += ('-');
        }
        return encoding;
    }

    // This function basically uses a hashing based set to
// store strings which are distinct according to according
// to criteria given in question.
    static int countDistinct(String input[], int n) {
        int countDist = 0; // Initialize result

        // Create an empty set and store all distinct
        // strings in it.
        Set<String> s = new HashSet<>();
        for (int i = 0; i < n; i++) {
            // If this encoding appears first time, increment
            // count of distinct encodings.
            if (!s.contains(encodeString(input[i].toCharArray()))) {
                s.add(encodeString(input[i].toCharArray()));
                countDist++;
            }
        }

        return countDist;
    }

    public static void main(String[] args) {
        String input[] = {"abcd", "acbd", "adcb", "cdba",
                "bcda", "badc"};
        int n = input.length;

        System.out.println(countDistinct(input, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to count distinct strings with
# even odd swapping allowed.
MAX_CHAR = 26

# Returns encoding of string that can be used
# for hashing. The idea is to return same encoding
# for strings which can become same after swapping
# a even positioned character with other even characters
# OR swapping an odd character with other odd characters.
def encodeString(string):

    # hashEven stores the count of even indexed character
    # for each string hashOdd stores the count of odd
    # indexed characters for each string
    hashEven = [0] * MAX_CHAR
    hashOdd = [0] * MAX_CHAR

    # creating hash for each string
    for i in range(len(string)):
        c = string[i]
        if i & 1: # If index of current character is odd
            hashOdd[ord(c) - ord('a')] += 1
        else:
            hashEven[ord(c) - ord('a')] += 1

    # For every character from 'a' to 'z', we store its
    # count at even position followed by a separator,
    # followed by count at odd position.
    encoding = ""
    for i in range(MAX_CHAR):
        encoding += str(hashEven[i])
        encoding += str('-')
        encoding += str(hashOdd[i])
        encoding += str('-')

    return encoding

# This function basically uses a hashing based set to
# store strings which are distinct according to according
# to criteria given in question.
def countDistinct(input, n):
    countDist = 0 # Initialize result

    # Create an empty set and store all distinct
    # strings in it.
    s = set()
    for i in range(n):

        # If this encoding appears first time, increment
        # count of distinct encodings.
        if encodeString(input[i]) not in s:
            s.add(encodeString(input[i]))
            countDist += 1

    return countDist

# Driver Code
if __name__ == "__main__":
    input = ["abcd", "acbd", "adcb",
             "cdba", "bcda", "badc"]
    n = len(input)
    print(countDistinct(input, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to count distinct strings with
// even odd swapping allowed.
using System;
using System.Collections.Generic;

class GFG
{
    static int MAX_CHAR = 26;

    static String encodeString(char[] str)
    {
        // hashEven stores the count of even
        // indexed character for each string
        // hashOdd stores the count of odd
        // indexed characters for each string
        int []hashEven = new int[MAX_CHAR];
        int []hashOdd = new int[MAX_CHAR];

        // creating hash for each string
        for (int i = 0; i < str.Length; i++)
        {
            char m = str[i];

            // If index of current character is odd
            if ((i & 1) != 0)
                hashOdd[m - 'a']++;
            else
                hashEven[m - 'a']++;
        }

        // For every character from 'a' to 'z',
        // we store its count at even position
        // followed by a separator,
        // followed by count at odd position.
        String encoding = "";
        for (int i = 0; i < MAX_CHAR; i++)
        {
            encoding += (hashEven[i]);
            encoding += ('-');
            encoding += (hashOdd[i]);
            encoding += ('-');
        }
        return encoding;
    }

    // This function basically uses a hashing based set
    // to store strings which are distinct according
    // to criteria given in question.
    static int countDistinct(String []input, int n)
    {
        int countDist = 0; // Initialize result

        // Create an empty set and store all distinct
        // strings in it.
        HashSet<String> s = new HashSet<String>();
        for (int i = 0; i < n; i++)
        {
            // If this encoding appears first time,
            // increment count of distinct encodings.
            if (!s.Contains(encodeString(input[i].ToCharArray())))
            {
                s.Add(encodeString(input[i].ToCharArray()));
                countDist++;
            }
        }

        return countDist;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String []input = {"abcd", "acbd", "adcb",
                          "cdba", "bcda", "badc"};
        int n = input.Length;

        Console.WriteLine(countDistinct(input, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

    // Javascript program to count distinct strings with
    // even odd swapping allowed

    let MAX_CHAR = 26;

    function encodeString(str) {
        // hashEven stores the count of even indexed character
        // for each string hashOdd stores the count of odd
        // indexed characters for each string
        let hashEven =  Array(MAX_CHAR).fill(0);
        let hashOdd = Array(MAX_CHAR).fill(0);

        // creating hash for each string
        for (let i = 0; i < str.length; i++) {
            let c = str[i];
            if ((i & 1) != 0) // If index of current character is odd
                hashOdd[c.charCodeAt() - 'a'.charCodeAt()]++;
            else
                hashEven[c.charCodeAt() - 'a'.charCodeAt()]++;

        }

        // For every character from 'a' to 'z', we store its
        // count at even position followed by a separator,
        // followed by count at odd position.
        let encoding = "";
        for (let i = 0; i < MAX_CHAR; i++) {
            encoding += (hashEven[i]);
            encoding += ('-');
            encoding += (hashOdd[i]);
            encoding += ('-');
        }
        return encoding;
    }

    // This function basically uses a hashing based set to
    // store strings which are distinct according to according
    // to criteria given in question.
    function countDistinct(input, n) {
        let countDist = 0; // Initialize result

        // Create an empty set and store all distinct
        // strings in it.
        let s = new Set();
        for (let i = 0; i < n; i++) {
            // If this encoding appears first time, increment
            // count of distinct encodings.
            if (!s.has(encodeString(input[i].split('')))) {
                s.add(encodeString(input[i].split('')));
                countDist++;
            }
        }

        return countDist;
    }

// Driver program

        let input = ["abcd", "acbd", "adcb", "cdba",
                "bcda", "badc"];
        let n = input.length;

        document.write(countDistinct(input, n));

</script>
```

**Output**

```
4
```

本文由 **kp93** 投稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息