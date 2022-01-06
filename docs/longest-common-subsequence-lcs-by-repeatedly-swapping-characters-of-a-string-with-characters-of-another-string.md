# 通过重复地将一个字符串的字符与另一个字符串的字符交换来获得最长的公共子序列(LCS)

> 原文:[https://www . geeksforgeeks . org/最长公共子序列-LCS-通过重复交换字符串中的字符与另一个字符串中的字符/](https://www.geeksforgeeks.org/longest-common-subsequence-lcs-by-repeatedly-swapping-characters-of-a-string-with-characters-of-another-string/)

给定两个长度分别为 **N** 和 **M** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **A** 和 **B** ，任务是找到[最长公共子序列](https://www.geeksforgeeks.org/longest-common-subsequence-dp-4/)的长度，如果字符串 **A** 中的任何字符可以与 **B** 中的任何其他字符交换任意次数，则该长度可以是两个字符串。

**示例:**

> **输入:** A = "abdeff "，B = "abbet"
> **输出:** 4
> **解释:**交换 A[5]和 B[4]将 A 修改为“abdeft”，将 B 修改为“abbef”。给定字符串中的 LCS 是“abef”。因此，长度为 4。
> 
> **输入:** A = "abcd "，B = "ab"
> **输出:** 2
> **说明:**给定字符串的 LCS 为“ab”。因此，长度为 2。

**方法:**这个想法是基于这样的观察:如果字符串 **A** 中的任何字符可以与字符串 **B** 中的任何其他字符交换，那么也有可能在字符串 **A** 内以及字符串 **B** 内交换字符。

**证明:**如果需要交换字符**A【I】**和**A【j】**，那么在字符串 **B** 中的任意索引 **k** 处取一个临时元素。按照以下步骤解决问题:

*   将 **A[i]** 换成 **B[k]** 。
*   将 **B[k]** 换成 **A[j]** 。
*   将 **B[k]** 换成 **A[i]** 。

这样，字符串中的字符可以交换。现在，元素可以以任何顺序排列。因此，这个想法是找到两个字符串中出现的所有字符的频率，并平均分配它们。
按照以下步骤解决问题:

*   初始化一个数组，比如大小为 **26** 的 **freq** ，以[存储字符串](https://www.geeksforgeeks.org/frequency-of-each-character-in-a-string-using-unordered_map-in-c/)中出现的每个字符的频率。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **A** 和 **B** 和[更新数组中每个字符的频率 **freq[]**](https://www.geeksforgeeks.org/print-the-frequency-of-each-character-in-alphabetical-order/) 。
*   初始化一个变量，比如 **cnt** ，来存储需要的长度。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **freq[]** ，将 **cnt** 的值增加 **freq[i] / 2** 。
*   将 **cnt** 、 **N** 和 **M** 的最小值存储在一个变量中，比如 **ans** 。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the length of LCS
// possible by swapping any character
// of a string with that of another string
void lcsBySwapping(string A, string B)
{
    // Store the size of the strings
    int N = A.size();
    int M = B.size();

    // Stores frequency of characters
    int freq[26];

    memset(freq, 0, sizeof(freq));

    // Iterate over characters of the string A
    for (int i = 0; i < A.size(); i++) {

        // Update frequency of character A[i]
        freq[A[i] - 'a'] += 1;
    }

    // Iterate over characters of the string B
    for (int i = 0; i < B.size(); i++) {

        // Update frequency of character B[i]
        freq[B[i] - 'a'] += 1;
    }

    // Store the count of all pairs
    // of similar characters
    int cnt = 0;

    // Traverse the array freq[]
    for (int i = 0; i < 26; i++) {

        // Update cnt
        cnt += freq[i] / 2;
    }

    // Print the minimum of cnt, N and M
    cout << min(cnt, min(N, M));
}

// Driver Code
int main()
{
    // Given strings
    string A = "abdeff";
    string B = "abbet";

    lcsBySwapping(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the length of LCS
// possible by swapping any character
// of a string with that of another string
static void lcsBySwapping(String A, String B)
{

    // Store the size of the strings
    int N = A.length();
    int M = B.length();

    // Stores frequency of characters
    int freq[] = new int[26];

    // Iterate over characters of the string A
    for(int i = 0; i < N; i++)
    {

        // Update frequency of character A[i]
        freq[A.charAt(i) - 'a'] += 1;
    }

    // Iterate over characters of the string B
    for(int i = 0; i < M; i++)
    {

        // Update frequency of character B[i]
        freq[B.charAt(i) - 'a'] += 1;
    }

    // Store the count of all pairs
    // of similar characters
    int cnt = 0;

    // Traverse the array freq[]
    for(int i = 0; i < 26; i++)
    {

        // Update cnt
        cnt += freq[i] / 2;
    }

    // Print the minimum of cnt, N and M
    System.out.println(Math.min(cnt, Math.min(N, M)));
}

// Driver Code
public static void main(String[] args)
{

    // Given strings
    String A = "abdeff";
    String B = "abbet";

    lcsBySwapping(A, B);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the length of LCS
# possible by swapping any character
# of a with that of another string
def lcsBySwapping(A, B):

    # Store the size of the strings
    N = len(A)
    M = len(B)

    # Stores frequency of characters
    freq = [0] * 26

    # Iterate over characters of the A
    for i in range(len(A)):

        # Update frequency of character A[i]
        freq[ord(A[i]) - ord('a')] += 1

    # Iterate over characters of the B
    for i in range(len(B)):

        # Update frequency of character B[i]
        freq[ord(B[i]) - ord('a')] += 1

    # Store the count of all pairs
    # of similar characters
    cnt = 0

    # Traverse the array freq[]
    for i in range(26):

        # Update cnt
        cnt += freq[i] // 2

    # Print the minimum of cnt, N and M
    print (min(cnt, min(N, M)))

# Driver Code
if __name__ == '__main__':

    # Given strings
    A = "abdeff"
    B = "abbet"

    lcsBySwapping(A, B)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the length of LCS
// possible by swapping any character
// of a string with that of another string
static void lcsBySwapping(string A, string B)
{

    // Store the size of the strings
    int N = A.Length;
    int M = B.Length;

    // Stores frequency of characters
    int[] freq = new int[26];

    // Iterate over characters of the string A
    for(int i = 0; i < N; i++)
    {

        // Update frequency of character A[i]
        freq[A[i] - 'a'] += 1;
    }

    // Iterate over characters of the string B
    for(int i = 0; i < M; i++)
    {

        // Update frequency of character B[i]
        freq[B[i] - 'a'] += 1;
    }

    // Store the count of all pairs
    // of similar characters
    int cnt = 0;

    // Traverse the array freq[]
    for(int i = 0; i < 26; i++)
    {

        // Update cnt
        cnt += freq[i] / 2;
    }

    // Print the minimum of cnt, N and M
    Console.WriteLine(Math.Min(cnt, Math.Min(N, M)));
}

// Driver Code
public static void Main(string[] args)
{

    // Given strings
    string A = "abdeff";
    string B = "abbet";

    lcsBySwapping(A, B);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
//Javascript program for the above approach

// Function to find the length of LCS
// possible by swapping any character
// of a string with that of another string
function lcsBySwapping(A, B)
{
    // Store the size of the strings
    var N = A.length;
    var M = B.length;

    // Stores frequency of characters
    var freq = new Array(26);

    freq.fill(0);

    // Iterate over characters of the string A
    for (var i = 0; i < A.length; i++) {

        // Update frequency of character A[i]
        freq[A[i].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;
    }

    // Iterate over characters of the string B
    for (var i = 0; i < B.length; i++) {

        // Update frequency of character B[i]
        freq[B[i].charCodeAt(0) - 'a'.charCodeAt(0)] += 1;
    }

    // Store the count of all pairs
    // of similar characters
    var cnt = 0;

    // Traverse the array freq[]
    for (var i = 0; i < 26; i++) {

        // Update cnt
        cnt += parseInt(freq[i] / 2);
    }

    // Print the minimum of cnt, N and M
   document.write( Math.min(cnt, Math.min(N, M)));
}

var A = "abdeff";
var B = "abbet";
lcsBySwapping(A, B);

//This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(1)*