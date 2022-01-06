# 通过重复追加两个给定字符串的第一个字符，可能的字典上最大的字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序重复追加两个给定字符串中的第一个字符可能的最大字符串/](https://www.geeksforgeeks.org/lexicographically-largest-string-possible-by-repeatedly-appending-first-character-of-two-given-strings/)

给定两个由小写字符组成的 **N** 和 **M** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/)**【S1】**和 **S2** ，任务是通过重复追加任一字符串的第一个字符并从选择的字符串中移除该字符来构建[字典上最大的](https://www.geeksforgeeks.org/lexicographically-largest-subsequence-every-character-occurs-least-k-times/)字符串。

**示例:**

> **输入:**S1 =“dbcbb”，S2 =“cdbbb”
> T3】输出:“dcdbcbbbb”
> **解释:**
> 让 **ans** 成为最初为空的字典上最大的字符串，并执行以下步骤生成结果字符串:
> 从 S1 中获取第一个字符:ans =“d”，S1 =“bcbb”，S2 =“cdbbb”
> 从 S2 中获取第一个字符:ans =“DC” s1 =“bcbb”，word 2 =“BBB”
> 取 S1:ans =“dcdb”中的第一个字符，S1 =“cbb”，word 2 =“BBB”
> 取 S1:ans =“dcbdc”中的第一个字符，S1 =“bb”，word 2 =“BBB”
> 在 ans 末尾追加 S1 和 s2 中剩余的 5 个 b。 因此，打印“dcdbcbbbbb”作为结果字符串。
> 
> **输入:**S1 = " xyxyz "，S2 = " xywzxyx "
> T3】输出:【xyzxyzxywzxyx "

**方法:**给定的问题可以用[两点法](https://www.geeksforgeeks.org/two-pointers-technique/)解决。按照以下步骤解决问题:

*   初始化一个空字符串，说**合并**为**存储[字典上最大的字符串](https://www.geeksforgeeks.org/lexicographically-largest-string-possible-in-one-swap/)。**
*   **初始化两个[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)，说 **i** 为 **0** ， **j** 为 **0** ，同时遍历两个字符串。**
*   **[遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)直到任一字符串已经完全使用。

    *   如果[子串](https://www.geeksforgeeks.org/substring-in-cpp/) **字 1【I，N–1】**在字典上大于或等于子串**字 2【j，M–1】**，则在字符串**的末尾追加字符**字 1【I】**，合并**，并将指针 **i** 增加 **1** 。
    *   否则，在字符串**的末尾追加字符**字 2【I】**合并**并将指针 **j** 增加 **1** 。** 
*   **完成以上步骤后，打印字符串**合并**作为结果字符串。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to make the lexicographically
// largest string by merging two strings
string largestMerge(string word1,
                    string word2)
{
    // Stores the resultant string
    string merge = "";

    while (word1.size() != 0
           || word2.size() != 0) {

        // If the string word1 is
        // lexographically greater
        // than or equal to word2
        if (word1 >= word2) {

            // Update the string merge
            merge = merge + word1[0];

            // Erase the first index
            // of the string word1
            word1.erase(word1.begin() + 0);
        }

        // Otherwise
        else {

            // Update the string merge
            merge = merge + word2[0];

            // Erase the first index of
            // the string word2
            word2.erase(word2.begin() + 0);
        }
    }

    // Return the final string
    return merge;
}

// Driver Code
int main()
{
    string S1 = "xyzxyz";
    string S2 = "xywzxyx";
    cout << largestMerge(S1, S2);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;

class GFG {

// Function to make the lexicographically
// largest string by merging two strings
static String largestMerge(String word1,
                           String word2)
{

    // Stores the resultant string
    String merge = "";

    while (word1.length() != 0 ||
           word2.length() != 0)
    {

        // If the string word1 is
        // lexographically greater
        // than or equal to word
        if (word1.compareTo(word2) == 0 || ( word1.compareTo(word2) > 0))
        {

            // Update the string merge
            merge = merge + word1.charAt(0);

            // Erase the first index
            // of the string word1
            word1 = word1.substring(1);
        }

        // Otherwise
        else
        {

            // Update the string merge
            merge = merge + word2.charAt(0);

            // Erase the first index of
            // the string word2
            word2 = word2.substring(1);
        }
    }

    // Return the final string
    return merge;
}

// Driver Code
public static void main(String[] args)
{
    String S1 = "xyzxyz";
    String S2 = "xywzxyx";

    System.out.println(largestMerge(S1, S2));
}
}

// This code is contributed by sanjoy_62.
```

## **蟒蛇 3**

```
# Python program for the above approach

# Function to make the lexicographically
# largest string by merging two strings
def largestMerge(word1, word2):

     # Stores the resultant string
    merge = ""
    while len(word1) != 0 or len(word2) != 0:

          # If the string word1 is
        # lexographically greater
        # than or equal to word2
        if word1 >= word2:

          # Update the string merge
            merge = merge + word1[0]

             # Erase the first index
            # of the string word1
            word1 = word1[1:]

            #  Otherwise
        else:

          # Update the string merge
            merge = merge + word2[0]

             # Erase the first index
            # of the string word2
            word2 = word2[1:]

    # Return the final string       
    return merge

# Driver code
S1 = "xyzxyz"
S2 = "xywzxyx"
print(largestMerge(S1, S2))

# This code is contributed by Parth Manchanda
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to make the lexicographically
// largest string by merging two strings
static string largestMerge(string word1,
                           string word2)
{

    // Stores the resultant string
    string merge = "";

    while (word1.Length != 0 ||
           word2.Length != 0)
    {

        // If the string word1 is
        // lexographically greater
        // than or equal to word2
        if (String.Compare(word1, word2) == 0 ||
            String.Compare(word1, word2) > 0)
        {

            // Update the string merge
            merge = merge + word1[0];

            // Erase the first index
            // of the string word1
            word1 = word1.Substring(1);
        }

        // Otherwise
        else
        {

            // Update the string merge
            merge = merge + word2[0];

            // Erase the first index of
            // the string word2
            word2 = word2.Substring(1);
        }
    }

    // Return the final string
    return merge;
}

// Driver Code
public static void Main()
{
    string S1 = "xyzxyz";
    string S2 = "xywzxyx";

    Console.Write(largestMerge(S1, S2));

}
}

// This code is contributed by SURENDRA_GANGWAR
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to make the lexicographically
// largest let by merging two lets
function largestMerge(word1, word2)
{

    // Stores the resultant let
    let merge = "";

    while (word1.length != 0 ||
           word2.length != 0)
    {

        // If the let word1 is
        // lexographically greater
        // than or equal to word
        if (word1.localeCompare(word2) == 0 || ( word1.localeCompare(word2) > 0))
        {

            // Update the let merge
            merge = merge + word1[0];

            // Erase the first index
            // of the let word1
            word1 = word1.substring(1);
        }

        // Otherwise
        else
        {

            // Update the let merge
            merge = merge + word2[0];

            // Erase the first index of
            // the let word2
            word2 = word2.substring(1);
        }
    }

    // Return the final let
    return merge;
}

// Driver Code

      let S1 = "xyzxyz";
    let S2 = "xywzxyx";

    document.write(largestMerge(S1, S2));

// This code is contributed by splevel62.
</script>
```

****Output:** 

```
xyzxyzxywzxyx
```** 

*****时间复杂度:** O(N*M)*
***辅助空间:** O(1)***