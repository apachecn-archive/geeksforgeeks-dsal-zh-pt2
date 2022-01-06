# 查找字符串是否为 K 回文|设置 1

> 原文:[https://www . geesforgeks . org/find-if-string-is-k-回文-or-not/](https://www.geeksforgeeks.org/find-if-string-is-k-palindrome-or-not/)

给定一个字符串，找出这个字符串是否是 K-回文。一个 k-回文串最多去掉 k 个字符就变成了回文。
示例:

```
Input : String - abcdecba, k = 1
Output : Yes
String can become palindrome by remo-
-ving 1 character i.e. either d or e)

Input  : String - abcdeca, K = 2
Output : Yes
Can become palindrome by removing
2 characters b and e.

Input : String - acdcb, K = 1
Output : No
String can not become palindrome by
removing only one character.
```

如果我们仔细分析这个问题，任务是通过从给定字符串中最多删除 K 个字符，将该字符串转换成它的反串。问题基本上是[编辑距离](https://www.geeksforgeeks.org/dynamic-programming-set-5-edit-distance/)的变异。我们可以修改编辑距离问题，将给定的字符串及其反向作为输入，并且只允许删除操作。由于给定的字符串与其相反的字符串进行比较，我们将从第一个字符串中最多删除 N 个，从第二个字符串中最多删除 N 个，以使它们相等。因此，一个字符串要成为 K 回文，2*N < = 2*K 应该成立。
下面是算法的详细步骤–
从两个字符串的左侧或右侧开始，逐个处理所有字符。让我们从右上角遍历，每对被遍历的字符有两种可能。

1.  如果两个字符串的最后一个字符相同，我们将忽略最后一个字符，并计算剩余字符串的数量。所以我们重复长度 m-1 和 n-1，其中 m 是 str1 的长度，n 是 str2 的长度。
2.  如果最后一个字符不相同，我们考虑对第一个字符串的最后一个字符和第二个字符串的最后一个字符进行删除操作，递归计算操作的最小代价，取两个值的最小值。
    *   从 str1 中删除最后一个字符:m-1 和 n 的重复出现
    *   从 str2 中删除最后一个字符:重复 m 和 n-1。

下面是上述方法的朴素递归实现。

## C++

```
// A Naive recursive C++ program to find
// if given string is K-Palindrome or not
#include<bits/stdc++.h>
using namespace std;

// find if given string is K-Palindrome or not
int isKPalRec(string str1, string str2, int m, int n)
{
    // If first string is empty, the only option is to
    // remove all characters of second string
    if (m == 0) return n;

    // If second string is empty, the only option is to
    // remove all characters of first string
    if (n == 0) return m;

    // If last characters of two strings are same, ignore
    // last characters and get count for remaining strings.
    if (str1[m-1] == str2[n-1])
        return isKPalRec(str1, str2, m-1, n-1);

    // If last characters are not same,
    // 1\. Remove last char from str1 and recur for m-1 and n
    // 2\. Remove last char from str2 and recur for m and n-1
    // Take minimum of above two operations
    return 1 + min(isKPalRec(str1, str2, m-1, n), // Remove from str1
                   isKPalRec(str1, str2, m, n-1)); // Remove from str2
}

// Returns true if str is k palindrome.
bool isKPal(string str, int k)
{
    string revStr = str;
    reverse(revStr.begin(), revStr.end());
    int len = str.length();

    return (isKPalRec(str, revStr, len, len) <= k*2);
}

// Driver program
int main()
{
    string str = "acdcb";
    int k = 2;
    isKPal(str, k)? cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Naive recursive Java program
// to find if given string is
// K-Palindrome or not
class GFG
{

    // find if given string is
    // K-Palindrome or not
    static int isKPalRec(String str1,
            String str2, int m, int n)
    {
        // If first string is empty,
        // the only option is to remove
        // all characters of second string
        if (m == 0)
        {
            return n;
        }

        // If second string is empty,
        // the only option is to remove
        // all characters of first string
        if (n == 0)
        {
            return m;
        }

        // If last characters of two
        // strings are same, ignore
        // last characters and get
        // count for remaining strings.
        if (str1.charAt(m - 1) ==
            str2.charAt(n - 1))
        {
            return isKPalRec(str1, str2,
                            m - 1, n - 1);
        }

        // If last characters are not same,
        // 1\. Remove last char from str1 and
        // recur for m-1 and n
        // 2\. Remove last char from str2 and
        // recur for m and n-1
        // Take minimum of above two operations
        return 1 + Math.min(isKPalRec(str1, str2, m - 1, n), // Remove from str1
                isKPalRec(str1, str2, m, n - 1)); // Remove from str2
    }

    // Returns true if str is k palindrome.
    static boolean isKPal(String str, int k)
    {
        String revStr = str;
        revStr = reverse(revStr);
        int len = str.length();

        return (isKPalRec(str, revStr, len, len) <= k * 2);
    }

    static String reverse(String input)
    {
        char[] temparray = input.toCharArray();
        int left, right = 0;
        right = temparray.length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.valueOf(temparray);
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "acdcb";
        int k = 2;
        if (isKPal(str, k))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# A Naive recursive Python3
# code to find if given string
# is K-Palindrome or not

# Find if given string
# is K-Palindrome or not
def isKPalRec(str1, str2, m, n):

    # If first string is empty,
    # the only option is to remove
    # all characters of second string
    if not m: return n

    # If second string is empty,
    # the only option is to remove
    # all characters of first string
    if not n: return m

    # If last characters of two strings
    # are same, ignore last characters
    # and get count for remaining strings.
    if str1[m-1] == str2[n-1]:
        return isKPalRec(str1, str2, m-1, n-1)

    # If last characters are not same,
    # 1\. Remove last char from str1 and recur for m-1 and n
    # 2\. Remove last char from str2 and recur for m and n-1
    # Take minimum of above two operations
    res = 1 + min(isKPalRec(str1, str2, m-1, n),  # Remove from str1
                 (isKPalRec(str1, str2, m, n-1))) # Remove from str2

    return res

# Returns true if str is k palindrome.
def isKPal(string, k):
    revStr = string[::-1]
    l = len(string)

    return (isKPalRec(string, revStr, l, l) <= k * 2)

# Driver program
string = "acdcb"
k = 2

print("Yes" if isKPal(string, k) else "No")

# This code is contributed by Ansu Kumari.
```

## C#

```
// A Naive recursive C# program
// to find if given string is
// K-Palindrome or not
using System;

class GFG
{

    // find if given string is
    // K-Palindrome or not
    static int isKPalRec(String str1,
            String str2, int m, int n)
    {
        // If first string is empty,
        // the only option is to remove
        // all characters of second string
        if (m == 0)
        {
            return n;
        }

        // If second string is empty,
        // the only option is to remove
        // all characters of first string
        if (n == 0)
        {
            return m;
        }

        // If last characters of two
        // strings are same, ignore
        // last characters and get
        // count for remaining strings.
        if (str1[m - 1] ==
            str2[n - 1])
        {
            return isKPalRec(str1, str2,
                            m - 1, n - 1);
        }

        // If last characters are not same,
        // 1\. Remove last char from str1 and
        // recur for m-1 and n
        // 2\. Remove last char from str2 and
        // recur for m and n-1
        // Take minimum of above two operations
        return 1 + Math.Min(isKPalRec(str1, str2, m - 1, n), // Remove from str1
                isKPalRec(str1, str2, m, n - 1)); // Remove from str2
    }

    // Returns true if str is k palindrome.
    static bool isKPal(String str, int k)
    {
        String revStr = str;
        revStr = reverse(revStr);
        int len = str.Length;

        return (isKPalRec(str, revStr, len, len) <= k * 2);
    }

    static String reverse(String input)
    {
        char[] temparray = input.ToCharArray();
        int left, right = 0;
        right = temparray.Length - 1;

        for (left = 0; left < right; left++, right--)
        {
            // Swap values of left and right
            char temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return String.Join("",temparray);
    }

    // Driver code
    public static void Main(String[] args)
    {
        String str = "acdcb";
        int k = 2;
        if (isKPal(str, k))
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// A Naive recursive javascript program
// to find if given string is
// K-Palindrome or not    // find if given string is
    // K-Palindrome or not
    function isKPalRec( str1,  str2 , m , n)
    {

        // If first string is empty,
        // the only option is to remove
        // all characters of second string
        if (m == 0) {
            return n;
        }

        // If second string is empty,
        // the only option is to remove
        // all characters of first string
        if (n == 0) {
            return m;
        }

        // If last characters of two
        // strings are same, ignore
        // last characters and get
        // count for remaining strings.
        if (str1.charAt(m - 1) == str2[n - 1]) {
            return isKPalRec(str1, str2, m - 1, n - 1);
        }

        // If last characters are not same,
        // 1\. Remove last char from str1 and
        // recur for m-1 and n
        // 2\. Remove last char from str2 and
        // recur for m and n-1
        // Take minimum of above two operations
        return 1 + Math.min(isKPalRec(str1, str2, m - 1, n), // Remove from str1
                isKPalRec(str1, str2, m, n - 1)); // Remove from str2
    }

    // Returns true if str is k palindrome.
    function isKPal( str , k) {
        var revStr = str;
        revStr = reverse(revStr);
        var len = str.length;

        return (isKPalRec(str, revStr, len, len) <= k * 2);
    }

     function reverse( input) {
        var temparray = input;
        var left, right = 0;
        right = temparray.length - 1;

        for (left = 0; left < right; left++, right--)
        {

            // Swap values of left and right
            var temp = temparray[left];
            temparray[left] = temparray[right];
            temparray[right] = temp;
        }
        return temparray;
    }

    // Driver code

        var str = "acdcb";
        var k = 2;
        if (isKPal(str, k)) {
            document.write("Yes");
        } else {
            document.write("No");
        }

// This code is contributed by umadevi9616
</script>
```

**输出:**

```
Yes
```

上述解的时间复杂度是指数的。最坏的情况下，我们最终可能会做 O(2 <sup>n</sup> )运算。最坏的情况是字符串包含所有不同的字符。
这个问题同时具有动态规划问题的两个属性(参见[这个](https://www.geeksforgeeks.org/dynamic-programming-set-1/)和[这个](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/))。像其他典型的动态规划问题一样，通过构造一个存储子问题结果的临时数组，可以避免重复计算相同的子问题。
下面是上述递归方法的自下而上的实现:

## C++

```
// C++ program to find if given string is K-Palindrome or not
#include <bits/stdc++.h>
using namespace std;

// find if given string is K-Palindrome or not
int isKPalDP(string str1, string str2, int m, int n)
{
    // Create a table to store results of subproblems
    int dp[m + 1][n + 1];

    // Fill dp[][] in bottom up manner
    for (int i = 0; i <= m; i++)
    {
        for (int j = 0; j <= n; j++)
        {
            // If first string is empty, only option is to
            // remove all characters of second string
            if (i == 0)
                dp[i][j] = j; // Min. operations = j

            // If second string is empty, only option is to
            // remove all characters of first string
            else if (j == 0)
                dp[i][j] = i; // Min. operations = i

            // If last characters are same, ignore last character
            // and recur for remaining string
            else if (str1[i - 1] == str2[j - 1])
                dp[i][j] = dp[i - 1][j - 1];

            // If last character are different, remove it
            // and find minimum
            else
             dp[i][j] = 1 + min(dp[i - 1][j], // Remove from str1
                             dp[i][j - 1]); // Remove from str2
        }
    }

    return dp[m][n];
}

// Returns true if str is k palindrome.
bool isKPal(string str, int k)
{
    string revStr = str;
    reverse(revStr.begin(), revStr.end());
    int len = str.length();

    return (isKPalDP(str, revStr, len, len) <= k*2);
}

// Driver program
int main()
{
    string str = "acdcb";
    int k = 2;
    isKPal(str, k)? cout << "Yes" : cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find if given
// string is K-Palindrome or not
class GFG
{

    // find if given string is
    // K-Palindrome or not
    static int isKPalDP(String str1,
            String str2, int m, int n)
    {

        // Create a table to store
        // results of subproblems
        int dp[][] = new int[m + 1][n + 1];

        // Fill dp[][] in bottom up manner
        for (int i = 0; i <= m; i++)
        {
            for (int j = 0; j <= n; j++)
            {

                // If first string is empty,
                // only option is to remove all
                // characters of second string
                if (i == 0)
                {
                    // Min. operations = j
                    dp[i][j] = j;
                }

                // If second string is empty,
                // only option is to remove all
                // characters of first string
                else if (j == 0)
                {
                    // Min. operations = i
                    dp[i][j] = i;
                }

                // If last characters are same,
                // ignore last character and
                // recur for remaining string
                else if (str1.charAt(i - 1) ==
                        str2.charAt(j - 1))
                {
                    dp[i][j] = dp[i - 1][j - 1];
                }

                // If last character are different,
                //  remove it and find minimum
                else
                {
                    // Remove from str1
                    // Remove from str2
                    dp[i][j] = 1 + Math.min(dp[i - 1][j],
                            dp[i][j - 1]);
                }
            }
        }
        return dp[m][n];
    }

    // Returns true if str is k palindrome.
    static boolean isKPal(String str, int k)
    {
        String revStr = str;
        revStr = reverse(revStr);
        int len = str.length();

        return (isKPalDP(str, revStr,
                len, len) <= k * 2);
    }

    static String reverse(String str)
    {
        StringBuilder sb = new StringBuilder(str);
        sb.reverse();
        return sb.toString();
    }

    // Driver program
    public static void main(String[] args)
    {
        String str = "acdcb";
        int k = 2;
        if (isKPal(str, k))
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }
}

// This code is contributed by
// PrinciRaj1992
```

## 蟒蛇 3

```
# Python program to find if given
# string is K-Palindrome or not

# Find if given string is
# K-Palindrome or not
def isKPalDP(str1, str2, m, n):

    # Create a table to store
    # results of subproblems
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Fill dp[][] in bottom up manner
    for i in range(m + 1):

        for j in range(n + 1):

            # If first string is empty,
            # only option is to remove
            # all characters of second string
            if not i :
                dp[i][j] = j    # Min. operations = j

            # If second string is empty,
            # only option is to remove
            # all characters of first string
            elif not j :
                dp[i][j] = i    # Min. operations = i

            # If last characters are same,
            # ignore last character and
            # recur for remaining string
            elif (str1[i - 1] == str2[j - 1]):
                dp[i][j] = dp[i - 1][j - 1]

            # If last character are different,
            # remove it and find minimum
            else:
                dp[i][j] = 1 + min(dp[i - 1][j],  # Remove from str1
                                  (dp[i][j - 1])) # Remove from str2

    return dp[m][n]

# Returns true if str
# is k palindrome.
def isKPal(string, k):

    revStr = string[::-1]
    l = len(string)

    return (isKPalDP(string, revStr, l, l) <= k * 2)

# Driver program
string = "acdcb"
k = 2
print("Yes" if isKPal(string, k) else "No")

# This code is contributed by Ansu Kumari.
```

## C#

```
// C# program to find if given 
// string is K-Palindrome or not
using System;
class GFG {

    // find if given string is
    // K-Palindrome or not
    static int isKPalDP(string str1, 
            string str2, int m, int n) 
    {

        // Create a table to store 
        // results of subproblems
        int[,] dp = new int[m + 1, n + 1];

        // Fill dp[][] in bottom up manner
        for (int i = 0; i <= m; i++) 
        {
            for (int j = 0; j <= n; j++) 
            {

                // If first string is empty,
                // only option is to remove all
                // characters of second string
                if (i == 0) 
                {
                    // Min. operations = j
                    dp[i, j] = j; 
                } 

                // If second string is empty, 
                // only option is to remove all
                // characters of first string
                else if (j == 0) 
                {
                    // Min. operations = i
                    dp[i, j] = i; 
                } 

                // If last characters are same, 
                // ignore last character and
                // recur for remaining string
                else if (str1[i - 1] == str2[j - 1]) 
                {
                    dp[i, j] = dp[i - 1, j - 1];
                } 

                // If last character are different,
                //  remove it and find minimum
                else
                {
                    // Remove from str1
                    // Remove from str2
                    dp[i, j] = 1 + Math.Min(dp[i - 1, j], dp[i, j - 1]); 
                }
            }
        }
        return dp[m, n];
    }

    // Returns true if str is k palindrome.
    static bool isKPal(string str, int k)
    {
        string revStr = str;
        revStr = reverse(revStr);
        int len = str.Length;
        return (isKPalDP(str, revStr, len, len) <= k * 2);
    }

    static string reverse(string str)
    {
        char[] sb = str.ToCharArray();
        Array.Reverse(sb);
        return new string(sb);
    }

    static void Main() {
        string str = "acdcb";
        int k = 2;
        if (isKPal(str, k)) 
        {
            Console.WriteLine("Yes");
        } 
        else
        {
            Console.WriteLine("No");
        }
    }
}

// This code is contributed by divyesh072019
```

**输出:**

```
Yes
```

上述解的时间复杂度为 O(m×n)。我们可以利用只允许 k 次删除的事实来提高时间复杂度。使用的辅助空间为 O(m x n)。
**交替法:**
1)求最长回文子序列的[长度](https://www.geeksforgeeks.org/longest-palindromic-subsequence-dp-12/)
2)如果原始字符串和最长回文子序列的长度之差小于或等于 k，则返回 true。否则返回 false。
[查找字符串是否为 K-回文|第二集(使用 LCS)](https://www.geeksforgeeks.org/find-if-string-is-k-palindrome-or-not-set-2/)
本文由 **Aditya Goel** 供稿。如果你喜欢极客博客并想投稿，你也可以写一篇文章并把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
发现有不正确的地方请写评论，或者想分享更多以上讨论话题的信息