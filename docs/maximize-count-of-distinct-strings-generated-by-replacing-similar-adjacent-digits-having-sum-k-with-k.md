# 通过用 K 替换具有和 K 的相似相邻数字来最大化不同字符串的计数

> 原文:[https://www . geeksforgeeks . org/通过用-k 替换相似的相邻数字来最大化不同字符串的计数/](https://www.geeksforgeeks.org/maximize-count-of-distinct-strings-generated-by-replacing-similar-adjacent-digits-having-sum-k-with-k/)

给定一个长度为 **N** 的数字串 **S** 和一个数字 **K** ，任务是找出最大出现次数为 **K** 的不同串的最大数量，如果它们的和为 **K** ，则用 **K** 替换 **S** 的任意两个相邻数字。

**示例:**

> **输入:** S = "313 "，K = 4
> **输出:** 2
> **说明:**可能生成的字符串有:
> 
> 1.  用 K 替换 S[0]和 S[1]将 S 修改为“43”。
> 2.  用 K 替换 S[1]和 S[2]将 S 修改为“34”。
> 
> **输入:**S =“12352”，K = 7
> **输出:** 1
> **解释:**唯一可能的字符串是用 K 替换 S[3]和 S[4]，即 S =“1237”。

**方法:**对于 **S** 的某些子串，有两种类型的可能性对结果有贡献，即它可以是具有相等数量的 **x** 和 **y** 的**xy**序列，即**“xyxy…xyxy”**或者它可以是具有一个额外的 **x 的 **xy** 序列**

*   **<u>情况 1:</u>** 形式的字符串**“xyxy…xyxy”**可以转换为字符串**“KK…KK”**其中 **K** 出现**(子字符串长度)/2** 次。因此，将要形成的不同弦的数量为 **1** 。
*   **<u>情况二:</u>** 形式的字符串**“xyxy…xyxyx”**多了一个**‘x’**，可以转换成**“KK…KKx”**出现 **K** 的字符串**(子串长度-1)/2** 次。让这个值为 **M** 。通过观察可以看出，转换后的字符串中 **x** 会有 **(M + 1)** 个可能的位置。

按照以下步骤解决问题:

*   用 **1** 初始化变量 **ans** ，用 **0** 标记，用 **-1** 初始化 **start_index** ，其中 **ans** 将存储直到索引**的答案 i** 和 **start_index** 将用于存储从期望序列开始的每个子串的起始索引。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 并执行以下操作:
    *   如果任意相邻数字 **S[i]** 和 **S[i + 1]** 之和为**K****标志**设置为**假**，将**标志**设置为**真****start _ index**设置为 **i** 。
    *   如果**标志**为**真**和**S【I】**和**S【I+1】**不是 **K** ，则将**标志**设置为**假**，如果**(start _ index–I+1)**为奇数，则将 **ans** 乘以**(start _ index–I+1–1)/2+1【1**
    *   遍历字符串 **S** 后，如果**标志**为**真**且**(N–start _ index)**为奇数，则将 **ans** 乘以**(N–start _ index–1)/2+1**。
*   完成上述步骤后，打印**和**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the desired number
// of strings
void countStrings(string s, int k)
{
    // Store the count of strings
    int ans = 1;

    // Store the length of the string
    int len = s.size();

    // Initialize variable to indicate
    // the start of the substring
    int flag = 0;

    // Store the starting index of
    // the substring
    int start_ind;

    // Traverse the string
    for (int i = 0; i < len - 1; i++) {

        // If sum of adjacent characters
        // is  K mark the starting index
        // and set flag to 1
        if (s[i] - '0' + s[i + 1] - '0'
                == k
            && flag == 0) {
            flag = 1;
            start_ind = i;
        }

        // If sum of adjacent characters
        // is not K and the flag variable
        // is set, end the substring here
        if (flag == 1
            && s[i] - '0'
                       + s[i + 1] - '0'
                   != k) {

            // Set flag to 0 denoting
            // the end of substring
            flag = 0;

            // Check if the length of the
            // substring formed is odd
            if ((i - start_ind + 1) % 2 != 0)

                // Update the answer
                ans *= (i - start_ind + 1 - 1)
                           / 2
                       + 1;
        }
    }

    // If flag is set and end of string
    // is reached, mark the end of substring
    if (flag == 1
        && (len - start_ind) % 2 != 0)

        // Update the answer
        ans *= (len - start_ind) / 2 + 1;

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    string S = "313";
    int K = 4;

    // Function Call
    countStrings(S, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the desired number
// of strings
static void countStrings(String s, int k)
{

    // Store the count of strings
    int ans = 1;

    // Store the length of the string
    int len = s.length();

    // Initialize variable to indicate
    // the start of the substring
    int flag = 0;

    // Store the starting index of
    // the substring
    int start_ind = 0;

    // Traverse the string
    for(int i = 0; i < len - 1; i++)
    {

        // If sum of adjacent characters
        // is  K mark the starting index
        // and set flag to 1
        if (s.charAt(i) - '0' +
            s.charAt(i + 1) - '0' == k && flag == 0)
        {
            flag = 1;
            start_ind = i;
        }

        // If sum of adjacent characters
        // is not K and the flag variable
        // is set, end the substring here
        if (flag == 1 && s.charAt(i) - '0' +
            s.charAt(i + 1) - '0' != k)
        {

            // Set flag to 0 denoting
            // the end of substring
            flag = 0;

            // Check if the length of the
            // substring formed is odd
            if ((i - start_ind + 1) % 2 != 0)

                // Update the answer
                ans *= (i - start_ind + 1 - 1) / 2 + 1;
        }
    }

    // If flag is set and end of string
    // is reached, mark the end of substring
    if (flag == 1 && (len - start_ind) % 2 != 0)

        // Update the answer
        ans *= (len - start_ind) / 2 + 1;

    // Print the answer
    System.out.println(ans);
}

// Driver Code
public static void main(String[] args)
{
    String S = "313";
    int K = 4;

    // Function Call
    countStrings(S, K);
}
}

// This code is contributed by jana_sayantan
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to find the desired number
# of strings
def countStrings(s, k) :

    # Store the count of strings
    ans = 1

    # Store the length of the string
    lenn = len(s)

    # Initialize variable to indicate
    # the start of the substring
    flag = 0

    # Traverse the string
    for i in range(lenn - 1):

        # If sum of adjacent characters
        # is  K mark the starting index
        # and set flag to 1
        if (ord(s[i]) - ord('0') + ord(s[i + 1]) - ord('0')
                == k
            and flag == 0) :
            flag = 1
            start_ind = i

        # If sum of adjacent characters
        # is not K and the flag variable
        # is set, end the substring here
        if (flag == 1
            and ord(s[i]) - ord('0')
                       + ord(s[i + 1]) - ord('0')
                   != k) :

            # Set flag to 0 denoting
            # the end of substring
            flag = 0

            # Check if the length of the
            # substring formed is odd
            if ((i - start_ind + 1) % 2 != 0) :

                # Update the answer
                ans *= (i - start_ind + 1 - 1) // 2 + 1

    # If flag is set and end of string
    # is reached, mark the end of substring
    if (flag == 1
        and (lenn - start_ind) % 2 != 0):

        # Update the answer
        ans *= (lenn - start_ind) // 2 + 1

    # Print the answer
    print(ans)

# Driver Code
S = "313"
K = 4

# Function Call
countStrings(S, K)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the desired number
// of strings
static void countStrings(String s, int k)
{

    // Store the count of strings
    int ans = 1;

    // Store the length of the string
    int len = s.Length;

    // Initialize variable to indicate
    // the start of the substring
    int flag = 0;

    // Store the starting index of
    // the substring
    int start_ind = 0;

    // Traverse the string
    for(int i = 0; i < len - 1; i++)
    {

        // If sum of adjacent characters
        // is  K mark the starting index
        // and set flag to 1
        if (s[i] - '0' +
            s[i + 1] - '0' == k && flag == 0)
        {
            flag = 1;
            start_ind = i;
        }

        // If sum of adjacent characters
        // is not K and the flag variable
        // is set, end the substring here
        if (flag == 1 && s[i] - '0' +
            s[i + 1] - '0' != k)
        {

            // Set flag to 0 denoting
            // the end of substring
            flag = 0;

            // Check if the length of the
            // substring formed is odd
            if ((i - start_ind + 1) % 2 != 0)

                // Update the answer
                ans *= (i - start_ind + 1 - 1) / 2 + 1;
        }
    }

    // If flag is set and end of string
    // is reached, mark the end of substring
    if (flag == 1 && (len - start_ind) % 2 != 0)

        // Update the answer
        ans *= (len - start_ind) / 2 + 1;

    // Print the answer
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(String[] args)
{
    String S = "313";
    int K = 4;

    // Function Call
    countStrings(S, K);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the desired number
// of strings
function countStrings(s, k)
{
    // Store the count of strings
    var ans = 1;

    // Store the length of the string
    var len = s.length;

    // Initialize variable to indicate
    // the start of the substring
    var flag = 0;

    // Store the starting index of
    // the substring
    var start_ind;

    // Traverse the string
    for (var i = 0; i < len - 1; i++) {

        // If sum of adjacent characters
        // is  K mark the starting index
        // and set flag to 1
        if ((s[i].charCodeAt(0) - '0'.charCodeAt(0) +
        s[i + 1].charCodeAt(0) - '0'.charCodeAt(0))
                == k
            && flag == 0) {
            flag = 1;
            start_ind = i;
        }

        // If sum of adjacent characters
        // is not K and the flag variable
        // is set, end the substring here
        if (flag == 1
            && (s[i].charCodeAt(0) - '0'.charCodeAt(0)
                       + s[i + 1].charCodeAt(0) -
                       '0'.charCodeAt(0))
                   != k) {

            // Set flag to 0 denoting
            // the end of substring
            flag = 0;

            // Check if the length of the
            // substring formed is odd
            if ((i - start_ind + 1) % 2 != 0)

                // Update the answer
                ans *= (i - start_ind + 1 - 1)
                           / 2
                       + 1;
        }
    }

    // If flag is set and end of string
    // is reached, mark the end of substring
    if (flag == 1
        && (len - start_ind) % 2 != 0)

        // Update the answer
        ans *= parseInt((len - start_ind) / 2) + 1;

    // Print the answer
    document.write( ans);
}

// Driver Code
var S = "313";
var K = 4;
// Function Call
countStrings(S, K);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)