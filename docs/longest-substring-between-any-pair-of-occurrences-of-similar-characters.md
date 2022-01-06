# 任何一对相似字符之间最长的子串

> 原文:[https://www . geeksforgeeks . org/任意对相似字符之间最长的子串/](https://www.geeksforgeeks.org/longest-substring-between-any-pair-of-occurrences-of-similar-characters/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是在任意一对出现的相同字符之间找到最长的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)的长度。

**示例:**

> **输入:** S = "accabbacc"
> **输出:** 6
> **说明:**满足要求条件的最长子串是“cabbac”，位于 S[1](= 'c ')和 s[8](= 'c ')之间。
> 
> **输入:**S = " aab "
> T3】输出: 0

**方法:**按照以下步骤解决问题:

1.  初始化两个变量 **res** 和 **diff** 分别存储最长子串的长度和同一对字符之间当前子串的长度。
2.  [从左到右迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)的字符。
3.  迭代右边剩余的字符串，从右向左直到当前字符。
4.  如果得到两个相等的字符，即 **S[i] = S[j]，**，将它们之间的子串长度存储在 **diff** 中。
5.  将 **res** 的值更新为**最大值(res，diff)。**以便 **res** 存储到目前为止获得的所需类型的最长子串。
6.  完成字符串遍历后，打印 **res** 作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the longest substring
// between pair of repetitions of the same character
int longestbetweenequalcharacters(string S)
{

    // Length of the string
    int n = S.length();

    // Stores the maximum length and
    // length of current substring
    // satisfying given conditions
    int res = -1, diff = -1;

    // Traverse the string
    for (int i = 0; i < n - 1; i++) {

        // Search for repetition of S[i]
        for (int j = n - 1; j > i; j--) {

            // If repetition occurs
            if (S[i] == S[j]) {

                // Store the length of
                // the substring
                diff = j - i - 1;

                // Update maximum length of
                // substring obtained
                res = max(diff, res);
            }
        }
    }

    // Return obtained maximum length
    return res;
}

// Driver Code
int main()
{
    string s = "accabbacc";
    cout << longestbetweenequalcharacters(s);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find the longest substring
// between pair of repetitions of the
// same character
static int longestbetweenequalcharacters(String S)
{

    // Length of the string
    int n = S.length();

    // Stores the maximum length and
    // length of current substring
    // satisfying given conditions
    int res = -1, diff = -1;

    // Traverse the string
    for(int i = 0; i < n - 1; i++)
    {

        // Search for repetition of S[i]
        for(int j = n - 1; j > i; j--)
        {

            // If repetition occurs
            if (S.charAt(i) == S.charAt(j))
            {

                // Store the length of
                // the substring
                diff = j - i - 1;

                // Update maximum length of
                // substring obtained
                res = Math.max(diff, res);
            }
        }
    }

    // Return obtained maximum length
    return res;
}

// Driver code
public static void main(String[] args)
{

    String s = "accabbacc";

    System.out.println(
        longestbetweenequalcharacters(s));
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the longest
# substring between pair of
# repetitions of the same character
def longestbetweenequalcharacters(S):

    # Length of the string
    n = len(S)

    # Stores the maximum length and
    # length of current substring
    # satisfying given conditions
    res = -1
    diff = -1

    # Traverse the string
    for i in range(n - 1):

        # Search for repetition of S[i]
        for j in range(n - 1, i, -1):

            # If repetition occurs
            if (S[i] == S[j]):

                # Store the length of
                # the substring
                diff = j - i - 1

                # Update maximum length of
                # substring obtained
                res = max(diff, res)

    # Return obtained maximum length
    return res

# Driver Code
if __name__ == '__main__':

    s = "accabbacc"

    print(longestbetweenequalcharacters(s))

# This code is contributed by doreamon_
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the longest substring
// between pair of repetitions of the
// same character
static int longestbetweenequalcharacters(String S)
{

    // Length of the string
    int n = S.Length;

    // Stores the maximum length and
    // length of current substring
    // satisfying given conditions
    int res = -1, diff = -1;

    // Traverse the string
    for(int i = 0; i < n - 1; i++)
    {

        // Search for repetition of S[i]
        for(int j = n - 1; j > i; j--)
        {

            // If repetition occurs
            if (S[i] == S[j])
            {

                // Store the length of
                // the substring
                diff = j - i - 1;

                // Update maximum length of
                // substring obtained
                res = Math.Max(diff, res);
            }
        }
    }

    // Return obtained maximum length
    return res;
}

// Driver code
public static void Main()
{
    string s = "accabbacc";

    Console.WriteLine(
        longestbetweenequalcharacters(s));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// javascript program to implement
// the above approach

// Function to find the longest substring
// between pair of repetitions of the
// same character
function longestbetweenequalcharacters(S)
{

    // Length of the string
    var n = S.length;

    // Stores the maximum length and
    // length of current substring
    // satisfying given conditions
    var res = -1, diff = -1;

    // Traverse the string
    for(i = 0; i < n - 1; i++)
    {

        // Search for repetition of S[i]
        for(j = n - 1; j > i; j--)
        {

            // If repetition occurs
            if (S.charAt(i) == S.charAt(j))
            {

                // Store the length of
                // the substring
                diff = j - i - 1;

                // Update maximum length of
                // substring obtained
                res = Math.max(diff, res);
            }
        }
    }

    // Return obtained maximum length
    return res;
}

// Driver code

var s = "accabbacc";

document.write(
    longestbetweenequalcharacters(s));

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*