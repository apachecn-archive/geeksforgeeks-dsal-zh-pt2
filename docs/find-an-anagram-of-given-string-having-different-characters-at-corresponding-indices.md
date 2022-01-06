# 在相应的索引处找到具有不同字符的给定字符串的字谜

> 原文:[https://www . geesforgeks . org/find-a-给定字符串在对应索引处具有不同字符的字谜/](https://www.geeksforgeeks.org/find-an-anagram-of-given-string-having-different-characters-at-corresponding-indices/)

给定一个由 **N** 个字符组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是[找到给定字符串](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/) **S** 的字谜，使得相同索引处的字符不同于原始字符串。

**示例:**

> **输入:** *S =【极客】*
> **输出:** egke
> **解释:**
> 给定字符串的字谜，使得所有对应索引处的所有字符都不相同，这就是“egke”。
> 
> **输入:**T2 S =AAAA”
> T5】输出: -1

**逼近:**给定的问题可以用[两点逼近](https://www.geeksforgeeks.org/two-pointers-technique/)来解决。其思想是交换字符串末尾的不同字符，如果这些索引中的字符相同，则检查下一个可能的具有不同字符的索引对。执行上述操作后，检查字谜是否在每个索引处生成不同的字符，并相应地打印结果。按照以下步骤解决给定的问题:

*   初始化一个字符串，比如存储给定字符串的**T****S**。
*   初始化两个指针，分别说 **i** 和 **j** 为 **0** 和**(N–1)**。
*   迭代直到 **i** 的值小于 **N** 和 **j** 的值为非负，并执行以下步骤:
    1.  如果字符 **S[i]** 和 **S[j]** 不相同，并且字符对 **(S[i]、T[j])** 和 **(T[i]、S[j])** 也不相同(确保交换操作后的字符变得与原始字符相同)，则[交换字符](https://www.geeksforgeeks.org/swap-characters-in-a-string/) **(S[i]、S[j])** 并更新 **j【的值**
    2.  否则，将 **i** 的值增加 **1** 。
*   [如果字符串具有奇数个字符](https://www.geeksforgeeks.org/program-to-check-if-all-characters-have-even-frequency/)，并且中间索引处的字符相等，则按照上述步骤执行交换操作。
*   完成上述步骤后，如果字符串 **S** 和 **T** 对应索引处的字符不相同，则打印字符串 **S** 作为结果字符串。否则，打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find anagram of string
// such that characters at the same
// indices are different
void findAnagram(string s)
{
    // Copying our original string
    // for comparison
    string check = s;

    // Declaring the two pointers
    int i = 0, j = s.length() - 1;

    while (i < s.length() && j >= 0) {

        // Checking the given condition
        if (s[i] != s[j] && check[i] != s[j]
            && check[j] != s[i]) {
            swap(s[i], s[j]);
            i++;

            j = s.length() - 1;
        }
        else {
            j--;
        }
    }

    // When string length is odd
    if (s.length() % 2 != 0) {

        // The mid element
        int mid = s.length() / 2;

        // If the characters are the
        // same, then perform the swap
        // operation as illustrated
        if (check[mid] == s[mid]) {
            for (int i = 0; i < s.length(); i++) {
                if (check[i] != s[mid]
                    && s[i] != s[mid]) {
                    swap(s[i], s[mid]);
                    break;
                }
            }
        }
    }

    // Check if the corresponding indices
    // has the same character or not
    bool ok = true;
    for (int i = 0; i < s.length(); i++) {
        if (check[i] == s[i]) {
            ok = false;
            break;
        }
    }

    // If string follows required
    // condition
    if (ok)
        cout << s;
    else
        cout << -1;
}

// Driver Code
int main()
{
    string S = "geek";
    findAnagram(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to find anagram of string
// such that characters at the same
// indices are different
static void findAnagram(String s)
{

    // Copying our original string
    // for comparison
    String check = s;

    // Declaring the two pointers
    int i = 0, j = s.length() - 1;

    while (i < s.length() && j >= 0) {

        // Checking the given condition
        if (s.charAt(i) != s.charAt(j) && check.charAt(i) != s.charAt(j)
            && check.charAt(j) != s.charAt(i)) {
            char temp = s.charAt(i);
            s = s.substring(0, i) + s.charAt(j) + s.substring(i + 1);
            s = s.substring(0, j) + temp + s.substring(j + 1);
            i++;

            j = s.length() - 1;
        }
        else {
            j--;
        }
    }

    // When string length is odd
    if (s.length() % 2 != 0) {

        // The mid element
        int mid = s.length() / 2;

        // If the characters are the
        // same, then perform the swap
        // operation as illustrated
        if (check.charAt(mid) == s.charAt(mid)) {
            for (i = 0; i < s.length(); i++) {
                if (check.charAt(i) != s.charAt(mid)
                    && s.charAt(i) != s.charAt(mid)) {
                    char temp = s.charAt(i);
                    s = s.substring(0, i) + s.charAt(mid) + s.substring(i + 1);
                    s = s.substring(0, mid) + temp + s.substring(mid + 1);
                    break;
                }
            }
        }
    }

    // Check if the corresponding indices
    // has the same character or not
    boolean ok = true;

    for (i = 0; i < s.length(); i++) {
        if (check.charAt(i) == s.charAt(i) ) {
            ok = false;
            break;
        }
    }

    // If string follows required
    // condition
    if (ok)
        System.out.println(s);
    else
        System.out.println(-1);
}

// Driver Code
public static void main (String[] args)
{
    String S = "geek";
    findAnagram(S);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find anagram of string
# such that characters at the same
# indices are different
def findAnagram(s):

    # Copying our original string
    # for comparison
    check = s
    st = list(s)

    # Declaring the two pointers
    i = 0
    j = len(st) - 1

    while (i < len(st) and j >= 0):

        # Checking the given condition
        if (st[i] != st[j] and check[i] != st[j]
                and check[j] != st[i]):
            st[i], st[j] = st[j], st[i]
            i += 1

            j = len(st) - 1

        else:
            j -= 1

    # When string length is odd
    if (len(st) % 2 != 0):

        # The mid element
        mid = len(st) / 2

        # If the characters are the
        # same, then perform the swap
        # operation as illustrated
        if (check[mid] == st[mid]):
            for i in range(len(st)):
                if (check[i] != st[mid]
                        and st[i] != st[mid]):
                    st[i], st[mid] = st[mid], st[i]
                    break

    # Check if the corresponding indices
    # has the same character or not
    ok = True
    for i in range(len(st)):
        if (check[i] == st[i]):
            ok = False
            break

    # If string follows required
    # condition
    if (ok):
        print("".join(st))
    else:
        print(-1)

# Driver Code
if __name__ == "__main__":

    S = "geek"
    findAnagram(S)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find anagram of string
// such that characters at the same
// indices are different
static void findAnagram(string s)
{

    // Copying our original string
    // for comparison
    string check = s;

    // Declaring the two pointers
    int i = 0, j = s.Length - 1;

    while (i < s.Length && j >= 0) {

        // Checking the given condition
        if (s[i] != s[j] && check[i] != s[j]
            && check[j] != s[i]) {
            char temp = s[i];
            s = s.Substring(0, i) + s[j] + s.Substring(i + 1);
            s = s.Substring(0, j) + temp + s.Substring(j + 1);
            i++;

            j = s.Length - 1;
        }
        else {
            j--;
        }
    }

    // When string length is odd
    if (s.Length % 2 != 0) {

        // The mid element
        int mid = s.Length / 2;

        // If the characters are the
        // same, then perform the swap
        // operation as illustrated
        if (check[mid] == s[mid]) {
            for (i = 0; i < s.Length; i++) {
                if (check[i] != s[mid]
                    && s[i] != s[mid]) {
                    char temp = s[i];
                    s = s.Substring(0, i) + s[mid] + s.Substring(i + 1);
                    s = s.Substring(0, mid) + temp + s.Substring(mid + 1);
                    break;
                }
            }
        }
    }

    // Check if the corresponding indices
    // has the same character or not
    bool ok = true;
    for (i = 0; i < s.Length; i++) {
        if (check[i] == s[i]) {
            ok = false;
            break;
        }
    }

    // If string follows required
    // condition
    if (ok)
        Console.Write(s);
    else
        Console.Write(-1);
}

// Driver Code
public static void Main()
{
    string S = "geek";
    findAnagram(S);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find anagram of string
        // such that characters at the same
        // indices are different
        function swap(str, i, j) {
            if (i == j) {
                return str;
            }

            if (j < i) {
                var temp = j;
                j = i;
                i = temp;
            }

            if (i >= str.length) {
                return str;

            }
            return str.substring(0, i) +
                str[j] +

                str.substring(i + 1, j) +

                str[i] +
                str.substring(j + 1);
        }

        function findAnagram(s)
        {

            // Copying our original string
            // for comparison
            let check = s.slice();

            // Declaring the two pointers
            let i = 0, j = s.length - 1;

            while (i < s.length && j >= 0) {

                // Checking the given condition
                if (s[i] != s[j] && check[i] != s[j]
                    && check[j] != s[i]) {
                    s = swap(s, i, j)
                    i++;

                    j = s.length - 1;
                }
                else {
                    j--;
                }
            }

            // When string length is odd
            if (s.length % 2 != 0) {

                // The mid element
                let mid = s.length / 2;

                // If the characters are the
                // same, then perform the swap
                // operation as illustrated
                if (check[mid] == s[mid]) {
                    for (let i = 0; i < s.length; i++) {
                        if (check[i] != s[mid]
                            && s[i] != s[mid]) {
                            s = swap(s, i, mid)
                            break;
                        }
                    }
                }
            }

            // Check if the corresponding indices
            // has the same character or not
            let ok = true;
            for (let i = 0; i < s.length; i++) {
                if (check[i] == s[i]) {
                    ok = false;
                    break;
                }
            }

            // If string follows required
            // condition
            if (ok)
                document.write(s);
            else
                document.write(-1);
        }

        // Driver Code

        let S = "geek";
        findAnagram(S);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
egke
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*