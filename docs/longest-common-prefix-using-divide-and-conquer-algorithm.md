# 使用分治算法的最长公共前缀

> 原文:[https://www . geesforgeks . org/最长公共前缀使用分治算法/](https://www.geeksforgeeks.org/longest-common-prefix-using-divide-and-conquer-algorithm/)

给定一组字符串，找到最长的公共前缀。

**示例:**

```
Input  : {“geeksforgeeks”, “geeks”, “geek”, “geezer”}
Output : "gee"

Input  : {"apple", "ape", "april"}
Output : "ap"
```

我们已经讨论了[逐词匹配](https://www.geeksforgeeks.org/longest-common-prefix-set-1-word-by-word-matching/)和[逐字符匹配](https://www.geeksforgeeks.org/longest-common-prefix-set-2-character-by-character-matching/)算法。
在该算法中，讨论了一种分治的方法。我们首先把字符串数组分成两部分。然后我们对左半部分做同样的操作，然后对右半部分做同样的操作。我们将这样做，直到并且除非所有的字符串都变成长度 1。之后，我们将通过返回左右字符串的公共前缀来开始征服。
使用下图，算法将变得清晰。我们认为我们的琴弦是——“极客”、“极客”、“极客”、“怪客”。

![longest_common_prefix6](https://media.geeksforgeeks.org/wp-content/cdn-uploads/longest_common_prefix6.jpg)

下面是实现。

## C++

```
//  A C++ Program to find the longest common prefix
#include<bits/stdc++.h>
using namespace std;

// A Utility Function to find the common prefix between
// strings- str1 and str2
string commonPrefixUtil(string str1, string str2)
{
    string result;
    int n1 = str1.length(), n2 = str2.length();

    for (int i=0, j=0; i<=n1-1&&j<=n2-1; i++,j++)
    {
        if (str1[i] != str2[j])
            break;
        result.push_back(str1[i]);
    }
    return (result);
}

// A Divide and Conquer based function to find the
// longest common prefix. This is similar to the
// merge sort technique
string commonPrefix(string arr[], int low, int high)
{
    if (low == high)
        return (arr[low]);

    if (high > low)
    {
        // Same as (low + high)/2, but avoids overflow for
        // large low and high
        int mid = low + (high - low) / 2;

        string str1 = commonPrefix(arr, low, mid);
        string str2 = commonPrefix(arr, mid+1, high);

        return (commonPrefixUtil(str1, str2));
    }
}

// Driver program to test above function
int main()
{
    string arr[] = {"geeksforgeeks", "geeks",
                    "geek", "geezer"};
    int n = sizeof (arr) / sizeof (arr[0]);

    string ans = commonPrefix(arr, 0, n-1);

    if (ans.length())
        cout << "The longest common prefix is "
             << ans;
    else
        cout << "There is no common prefix";
    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the longest common prefix

class GFG {

// A Utility Function to find the common prefix between
// strings- str1 and str2
    static String commonPrefixUtil(String str1, String str2) {
        String result = "";
        int n1 = str1.length(), n2 = str2.length();

        for (int i = 0, j = 0; i <= n1 - 1 &&
                j <= n2 - 1; i++, j++) {
            if (str1.charAt(i) != str2.charAt(j)) {
                break;
            }
            result += str1.charAt(i);
        }
        return (result);
    }

// A Divide and Conquer based function to find the
// longest common prefix. This is similar to the
// merge sort technique
    static String commonPrefix(String arr[], int low, int high) {
        if (low == high) {
            return (arr[low]);
        }

        if (high > low) {
            // Same as (low + high)/2, but avoids overflow for
            // large low and high
            int mid = low + (high - low) / 2;

            String str1 = commonPrefix(arr, low, mid);
            String str2 = commonPrefix(arr, mid + 1, high);

            return (commonPrefixUtil(str1, str2));
        }
        return null;
    }

// Driver program to test above function
    public static void main(String[] args) {
        String arr[] = {"geeksforgeeks", "geeks",
            "geek", "geezer"};
        int n = arr.length;

        String ans = commonPrefix(arr, 0, n - 1);

        if (ans.length() != 0) {
            System.out.println("The longest common prefix is "
                    + ans);
        } else {
            System.out.println("There is no common prefix");
        }
    }
}
/* This JAVA code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# A Python3 Program to find the longest common prefix

# A Utility Function to find the common
# prefix between strings- str1 and str2
def commonPrefixUtil(str1, str2):

    result = ""
    n1, n2 = len(str1), len(str2)
    i, j = 0, 0

    while i <= n1 - 1 and j <= n2 - 1:

        if str1[i] != str2[j]:
            break
        result += str1[i]
        i, j = i + 1, j + 1

    return result

# A Divide and Conquer based function to
# find the longest common prefix. This is
# similar to the merge sort technique
def commonPrefix(arr, low, high):

    if low == high:
        return arr[low]

    if high > low:

        # Same as (low + high)/2, but avoids
        # overflow for large low and high
        mid = low + (high - low) // 2

        str1 = commonPrefix(arr, low, mid)
        str2 = commonPrefix(arr, mid + 1, high)

        return commonPrefixUtil(str1, str2)

# Driver Code
if __name__ == "__main__":

    arr = ["geeksforgeeks", "geeks",
                   "geek", "geezer"]
    n = len(arr)
    ans = commonPrefix(arr, 0, n - 1)

    if len(ans):
        print("The longest common prefix is", ans)
    else:
        print("There is no common prefix")

# This code is contributed by Rituraj Jain
```

## C#

```
// C# Program to find the longest
// common prefix
using System;

class GFG
{
// A Utility Function to find
// the common prefix between
// strings- str1 and str2
static string commonPrefixUtil(string str1,
                               string str2)
{
    string result = "";
    int n1 = str1.Length,
        n2 = str2.Length;

    for (int i = 0, j = 0;
             i <= n1 - 1 && j <= n2 - 1;
             i++, j++)
    {
        if (str1[i] != str2[j])
            break;
        result += str1[i];
    }
    return (result);
}

// A Divide and Conquer based
// function to find the longest
// common prefix. This is similar
// to the merge sort technique
static string commonPrefix(string []arr,
                           int low, int high)
{
    if (low == high)
        return (arr[low]);

    if (high > low)
    {
        // Same as (low + high)/2,
        // but avoids overflow for
        // large low and high
        int mid = low + (high - low) / 2;

        string str1 = commonPrefix(arr, low, mid);
        string str2 = commonPrefix(arr, mid + 1, high);

        return (commonPrefixUtil(str1, str2));
    }
    return null;
}

// Driver Code
public static void Main()
{
    String []arr = {"geeksforgeeks", "geeks",
                    "geek", "geezer"};
    int n = arr.Length;

    String ans = commonPrefix(arr, 0, n - 1);

    if (ans.Length!= 0)
    {
        Console.Write("The longest common " +
                         "prefix is " + ans);
    }
    else
    {
        Console.Write("There is no common prefix");
    }
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the
// longest common prefix

// A Utility Function to find the
// common prefix between strings-
// str1 and str2
function commonPrefixUtil(str1, str2)
{
    let result = "";
    let n1 = str1.length, n2 = str2.length;

    for(let i = 0, j = 0; i <= n1 - 1 &&
            j <= n2 - 1; i++, j++)
    {
        if (str1[i] != str2[j])
        {
            break;
        }
        result += str1[i];
    }
    return (result);
}

// A Divide and Conquer based function
// to find the longest common prefix. This
// is similar to the merge sort technique
function commonPrefix(arr, low, high)
{
    if (low == high)
    {
        return (arr[low]);
    }

    if (high > low)
    {

        // Same as (low + high)/2, but avoids
        // overflow for large low and high
        let mid = low + Math.floor((high - low) / 2);

        let str1 = commonPrefix(arr, low, mid);
        let str2 = commonPrefix(arr, mid + 1, high);

        return (commonPrefixUtil(str1, str2));
    }
    return null;
}

// Driver code
let arr = [ "geeksforgeeks", "geeks",
            "geek", "geezer" ];
let n = arr.length;
let ans = commonPrefix(arr, 0, n - 1);

if (ans.length != 0)
{
    document.write(
        "The longest common prefix is " + ans);
}
else
{
    document.write(
        "There is no common prefix");
}

// This code is contributed by rag2127

</script>
```

**输出:**

```
The longest common prefix is gee
```

**时间复杂度:**由于我们是迭代所有字符串的所有字符，所以可以说时间复杂度是 O(N ^ M)其中，

```
N = Number of strings
M = Length of the largest string string
```

**辅助空间:**为了存储最长的前缀字符串，我们分配的空间是 O(M Log N)。

本文由**拉希特·贝尔瓦亚尔**供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。