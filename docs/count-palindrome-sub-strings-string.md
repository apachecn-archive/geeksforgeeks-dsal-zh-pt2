# 统计一个字符串中所有回文子字符串|集合 1

> 原文:[https://www . geesforgeks . org/count-回文-子字符串-string/](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string/)

给定一个字符串，任务是统计给定字符串中的所有回文子字符串。回文子串长度大于等于 2。

**示例:**

```
Input : str = "abaab"
Output: 3
Explanation : 
All palindrome substring are :
 "aba" , "aa" , "baab" 

Input : str = "abbaeae"
Output: 4
Explanation : 
All palindrome substring are : 
"bb" , "abba" ,"aea","eae"
```

下面我们讨论了一个类似的问题。
[查找给定字符串的所有不同回文子字符串](https://www.geeksforgeeks.org/find-number-distinct-palindromic-sub-strings-given-string/)

上述问题可以递归定义。

```
Initial Values : i = 0, j = n-1;
Given string 'str'

CountPS(i, j)

   // If length of string is 2 then we 
   // check both character are same or not 
   If (j == i+1)
      return str[i] == str[j]
   //this condition shows that in recursion if i crosses j then it will be a invalid substring or
   //if i==j that means only one character is remaining and we require substring of length 2 
   //in both the conditions we need to return 0
   Else if(i == j ||  i > j) return 0;
   Else If str[i..j] is PALINDROME 
      // increment count by 1 and check for 
      // rest palindromic substring (i, j-1), (i+1, j)
      // remove common palindrome substring (i+1, j-1)
      return  countPS(i+1, j) + countPS(i, j-1) + 1 -
                                   countPS(i+1, j-1);

    Else // if NOT PALINDROME 
       // We check for rest palindromic substrings (i, j-1)
       // and (i+1, j)
       // remove common palindrome substring (i+1 , j-1)
       return  countPS(i+1, j) + countPS(i, j-1) - 
                             countPS(i+1 , j-1);
```

如果画出上述递归解的递归树，可以观察到[重叠子问题](https://www.geeksforgeeks.org/dynamic-programming-set-1/)。由于问题有重叠的子问题，我们可以使用动态规划来有效地解决它。下面是一个基于动态规划的解决方案。

## C++

```
// C++ program to find palindromic substrings of a string
#include <bits/stdc++.h>
using namespace std;

// Returns total number of palindrome substring of
// length greater then equal to 2
int CountPS(char str[], int n)
{
    // create empty 2-D matrix that counts all palindrome
    // substring. dp[i][j] stores counts of palindromic
    // substrings in st[i..j]
    int dp[n][n];
    memset(dp, 0, sizeof(dp));

    // P[i][j] = true if substring str[i..j] is palindrome,
    // else false
    bool P[n][n];
    memset(P, false, sizeof(P));

    // palindrome of single length
    for (int i = 0; i < n; i++)
        P[i][i] = true;

    // palindrome of length 2
    for (int i = 0; i < n - 1; i++) {
        if (str[i] == str[i + 1]) {
            P[i][i + 1] = true;
            dp[i][i + 1] = 1;
        }
    }

    // Palindromes of length more than 2\. This loop is
    // similar to Matrix Chain Multiplication. We start with
    // a gap of length 2 and fill the DP table in a way that
    // gap between starting and ending indexes increases one
    // by one by outer loop.
    for (int gap = 2; gap < n; gap++) {
        // Pick starting point for current gap
        for (int i = 0; i < n - gap; i++) {
            // Set ending point
            int j = gap + i;

            // If current string is palindrome
            if (str[i] == str[j] && P[i + 1][j - 1])
                P[i][j] = true;

            // Add current palindrome substring ( + 1)
            // and rest palindrome substring (dp[i][j-1] +
            // dp[i+1][j]) remove common palindrome
            // substrings (- dp[i+1][j-1])
            if (P[i][j] == true)
                dp[i][j] = dp[i][j - 1] + dp[i + 1][j] + 1
                           - dp[i + 1][j - 1];
            else
                dp[i][j] = dp[i][j - 1] + dp[i + 1][j]
                           - dp[i + 1][j - 1];
        }
    }

    // return total palindromic substrings
    return dp[0][n - 1];
}

// Driver code
int main()
{
    char str[] = "abaab";
    int n = strlen(str);
    cout << CountPS(str, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find palindromic substrings of a string

public class GFG {
    // Returns total number of palindrome substring of
    // length greater then equal to 2
    static int CountPS(char str[], int n)
    {
        // create empty 2-D matrix that counts all
        // palindrome substring. dp[i][j] stores counts of
        // palindromic substrings in st[i..j]
        int dp[][] = new int[n][n];

        // P[i][j] = true if substring str[i..j] is
        // palindrome, else false
        boolean P[][] = new boolean[n][n];

        // palindrome of single length
        for (int i = 0; i < n; i++)
            P[i][i] = true;

        // palindrome of length 2
        for (int i = 0; i < n - 1; i++) {
            if (str[i] == str[i + 1]) {
                P[i][i + 1] = true;
                dp[i][i + 1] = 1;
            }
        }

        // Palindromes of length more than 2\. This loop is
        // similar to Matrix Chain Multiplication. We start
        // with a gap of length 2 and fill the DP table in a
        // way that gap between starting and ending indexes
        // increases one by one by outer loop.
        for (int gap = 2; gap < n; gap++) {
            // Pick starting point for current gap
            for (int i = 0; i < n - gap; i++) {
                // Set ending point
                int j = gap + i;

                // If current string is palindrome
                if (str[i] == str[j] && P[i + 1][j - 1])
                    P[i][j] = true;

                // Add current palindrome substring ( + 1)
                // and rest palindrome substring (dp[i][j-1]
                // + dp[i+1][j]) remove common palindrome
                // substrings (- dp[i+1][j-1])
                if (P[i][j] == true)
                    dp[i][j] = dp[i][j - 1] + dp[i + 1][j]
                               + 1 - dp[i + 1][j - 1];
                else
                    dp[i][j] = dp[i][j - 1] + dp[i + 1][j]
                               - dp[i + 1][j - 1];
            }
        }

        // return total palindromic substrings
        return dp[0][n - 1];
    }

    // Driver code
    public static void main(String[] args)
    {
        String str = "abaab";
        System.out.println(
            CountPS(str.toCharArray(), str.length()));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find palindromic
# substrings of a string

# Returns total number of palindrome
# substring of length greater then
# equal to 2

def CountPS(str, n):

    # creat empty 2-D matrix that counts
    # all palindrome substring. dp[i][j]
    # stores counts of palindromic
    # substrings in st[i..j]
    dp = [[0 for x in range(n)]
          for y in range(n)]

    # P[i][j] = true if substring str[i..j]
    # is palindrome, else false
    P = [[False for x in range(n)]
         for y in range(n)]

    # palindrome of single length
    for i in range(n):
        P[i][i] = True

    # palindrome of length 2
    for i in range(n - 1):
        if (str[i] == str[i + 1]):
            P[i][i + 1] = True
            dp[i][i + 1] = 1

    # Palindromes of length more than 2\. This
    # loop is similar to Matrix Chain Multiplication.
    # We start with a gap of length 2 and fill DP
    # table in a way that the gap between starting and
    # ending indexes increase one by one by
    # outer loop.
    for gap in range(2, n):

        # Pick a starting point for the current gap
        for i in range(n - gap):

            # Set ending point
            j = gap + i

            # If current string is palindrome
            if (str[i] == str[j] and P[i + 1][j - 1]):
                P[i][j] = True

            # Add current palindrome substring ( + 1)
            # and rest palindrome substring (dp[i][j-1] +
            # dp[i+1][j]) remove common palindrome
            # substrings (- dp[i+1][j-1])
            if (P[i][j] == True):
                dp[i][j] = (dp[i][j - 1] +
                            dp[i + 1][j] + 1 - dp[i + 1][j - 1])
            else:
                dp[i][j] = (dp[i][j - 1] +
                            dp[i + 1][j] - dp[i + 1][j - 1])

    # return total palindromic substrings
    return dp[0][n - 1]

# Driver Code
if __name__ == "__main__":

    str = "abaab"
    n = len(str)
    print(CountPS(str, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find palindromic
// substrings of a string
using System;

class GFG {
    // Returns total number of
    // palindrome substring of
    // length greater then equal to 2
    public static int CountPS(char[] str, int n)
    {
        // create empty 2-D matrix that counts
        // all palindrome substring. dp[i][j]
        // stores counts of palindromic
        // substrings in st[i..j]

        int[][] dp
            = RectangularArrays.ReturnRectangularIntArray(
                n, n);

        // P[i][j] = true if substring str[i..j]
        // is palindrome, else false

        bool[][] P
            = RectangularArrays.ReturnRectangularBoolArray(
                n, n);

        // palindrome of single length
        for (int i = 0; i < n; i++) {
            P[i][i] = true;
        }

        // palindrome of length 2
        for (int i = 0; i < n - 1; i++) {
            if (str[i] == str[i + 1]) {
                P[i][i + 1] = true;
                dp[i][i + 1] = 1;
            }
        }

        // Palindromes of length more then 2.
        // This loop is similar to Matrix Chain
        // Multiplication. We start with a gap
        // of length 2 and fill DP table in a
        // way that gap between starting and
        // ending indexes increases one by one
        // by outer loop.
        for (int gap = 2; gap < n; gap++) {
            // Pick starting point for current gap
            for (int i = 0; i < n - gap; i++) {
                // Set ending point
                int j = gap + i;

                // If current string is palindrome
                if (str[i] == str[j] && P[i + 1][j - 1]) {
                    P[i][j] = true;
                }

                // Add current palindrome substring
                // ( + 1) and rest palindrome substring
                // (dp[i][j-1] + dp[i+1][j]) remove common
                // palindrome substrings (- dp[i+1][j-1])
                if (P[i][j] == true) {
                    dp[i][j] = dp[i][j - 1] + dp[i + 1][j]
                               + 1 - dp[i + 1][j - 1];
                }
                else {
                    dp[i][j] = dp[i][j - 1] + dp[i + 1][j]
                               - dp[i + 1][j - 1];
                }
            }
        }

        // return total palindromic substrings
        return dp[0][n - 1];
    }

    public static class RectangularArrays {
        public static int[][] ReturnRectangularIntArray(
            int size1, int size2)
        {
            int[][] newArray = new int[size1][];
            for (int array1 = 0; array1 < size1; array1++) {
                newArray[array1] = new int[size2];
            }

            return newArray;
        }

        public static bool[][] ReturnRectangularBoolArray(
            int size1, int size2)
        {
            bool[][] newArray = new bool[size1][];
            for (int array1 = 0; array1 < size1; array1++) {
                newArray[array1] = new bool[size2];
            }

            return newArray;
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        string str = "abaab";
        Console.WriteLine(
            CountPS(str.ToCharArray(), str.Length));
    }
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find palindromic substrings
// of a string

// Returns total number of palindrome
// substring of length greater then equal to 2
function CountPS($str, $n)
{
    // create empty 2-D matrix that counts
    // all palindrome substring. dp[i][j]
    // stores counts of palindromic
    // substrings in st[i..j]
    $dp = array(array());

    for ($i = 0; $i < $n; $i++)
        for($j = 0; $j < $n; $j++)
            $dp[$i][$j] = 0;

    // P[i][j] = true if substring str[i..j] 
    // is palindrome, else false
    $P = array(array());
        for ($i = 0; $i < $n; $i++)
            for($j = 0; $j < $n; $j++)
                $P[$i][$j] = false;

    // palindrome of single length
    for ($i= 0; $i< $n; $i++)
        $P[$i][$i] = true;

    // palindrome of length 2
    for ($i = 0; $i < $n - 1; $i++)
    {
        if ($str[$i] == $str[$i + 1])
        {
            $P[$i][$i + 1] = true;
            $dp[$i][$i + 1] = 1;
        }
    }

    // Palindromes of length more then 2\. This
    // loop is similar to Matrix Chain Multiplication.
    // We start with a gap of length 2 and fill DP
    // table in a way that gap between starting and
    // ending indexes increases one by one by
    // outer loop.
    for ($gap = 2; $gap < $n; $gap++)
    {
        // Pick starting point for current gap
        for ($i = 0; $i < $n - $gap; $i++)
        {
            // Set ending point
            $j = $gap + $i;

            // If current string is palindrome
            if ($str[$i] == $str[$j] && $P[$i + 1][$j - 1])
                $P[$i][$j] = true;

            // Add current palindrome substring (+ 1)
            // and rest palindrome substring (dp[i][j-1] +
            // dp[i+1][j]) remove common palindrome
            // substrings (- dp[i+1][j-1])
            if ($P[$i][$j] == true)
                $dp[$i][$j] = $dp[$i][$j - 1] +
                              $dp[$i + 1][$j] + 1 -
                              $dp[$i + 1][$j - 1];
            else
                $dp[$i][$j] = $dp[$i][$j - 1] +
                              $dp[$i + 1][$j] -
                              $dp[$i + 1][$j - 1];
        }
    }

    // return total palindromic substrings
    return $dp[0][$n - 1];
}

// Driver Code
$str = "abaab";
$n = strlen($str);
echo CountPS($str, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript program to find palindromic substrings of a string

    // Returns total number of palindrome substring of
    // length greater then equal to 2
    function CountPS(str,n)
    {
        // create empty 2-D matrix that counts all
        // palindrome substring. dp[i][j] stores counts of
        // palindromic substrings in st[i..j]
        let dp=new Array(n);

        // P[i][j] = true if substring str[i..j] is
        // palindrome, else false
        let P=new Array(n);

        for(let i=0;i<n;i++)
        {
            dp[i]=new Array(n);
            P[i]=new Array(n);
            for(let j=0;j<n;j++)
            {
                dp[i][j]=0;
                P[i][j]=false;
            }
        }

        // palindrome of single length
        for (let i = 0; i < n; i++)
            P[i][i] = true;

        // palindrome of length 2
        for (let i = 0; i < n - 1; i++) {
            if (str[i] == str[i + 1]) {
                P[i][i + 1] = true;
                dp[i][i + 1] = 1;
            }
        }

        // Palindromes of length more than 2\. This loop is
        // similar to Matrix Chain Multiplication. We start
        // with a gap of length 2 and fill the DP table in a
        // way that gap between starting and ending indexes
        // increases one by one by outer loop.
        for (let gap = 2; gap < n; gap++) {
            // Pick starting point for current gap
            for (let i = 0; i < n - gap; i++) {
                // Set ending point
                let j = gap + i;

                // If current string is palindrome
                if (str[i] == str[j] && P[i + 1][j - 1])
                    P[i][j] = true;

                // Add current palindrome substring ( + 1)
                // and rest palindrome substring (dp[i][j-1]
                // + dp[i+1][j]) remove common palindrome
                // substrings (- dp[i+1][j-1])
                if (P[i][j] == true)
                    dp[i][j] = dp[i][j - 1] + dp[i + 1][j]
                               + 1 - dp[i + 1][j - 1];
                else
                    dp[i][j] = dp[i][j - 1] + dp[i + 1][j]
                               - dp[i + 1][j - 1];
            }
        }

        // return total palindromic substrings
        return dp[0][n - 1];
    }

    // Driver code
    let str = "abaab";
    document.write(
            CountPS(str.split(""), str.length));

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
3
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n <sup>2</sup>

### 方法 2:

这种方法使用自顶向下的动态规划，即递归的记忆版本。

```
Recursive soln:
1\. Here base condition comes out to be i>j if we hit this condition, return 1.
2\. We check for each and every i and j, if the characters are equal, 
   if that is not the case, return 0.
3\. Call the is_palindrome function again with incremented i  and decremented j.
4\. Check this for all values of i and j by applying 2 for loops.
```

## C++

```
#include <bits/stdc++.h>
using namespace std;

int dp[1001][1001]; // 2D matrix
bool isPal(string s, int i, int j)
{
    // Base condition
    if (i > j)
        return 1;

    // check if the recursive tree
    // for given i, j
    // has already been executed
    if (dp[i][j] != -1)
        return dp[i][j];

    // If first and last characters of
    // substring are unequal
    if (s[i] != s[j])
        return dp[i][j] = 0;

    // memoization
    return dp[i][j] = isPal(s, i + 1, j - 1);
}

int countSubstrings(string s)
{
    memset(dp, -1, sizeof(dp));
    int n = s.length();
    int count = 0;

    // 2 for loops are required to check for
    // all the palindromes in the string.
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            // Increment count for every palindrome
            if (isPal(s, i, j))
                count++;
        }
    }
    // return total palindromic substrings
    return count;
}

// Driver code
int main()
{

    string s = "abbaeae";

    cout << countSubstrings(s);

    //"bb" , "abba" ,"aea", "eae" are
    // the 4 palindromic substrings.

    // This code is contributed by Bhavneet Singh

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
public class Main
{
    static int dp[][] = new int[1001][1001]; // 2D matrix

    public static int isPal(String s, int i, int j)
    {
        // Base condition
        if (i > j)
            return 1;

        // check if the recursive tree
        // for given i, j
        // has already been executed
        if (dp[i][j] != -1)
            return dp[i][j];

        // If first and last characters of
        // substring are unequal
        if (s.charAt(i) != s.charAt(j))
            return dp[i][j] = 0;

        // memoization
        return dp[i][j] = isPal(s, i + 1, j - 1);
    }

    public static int countSubstrings(String s)
    {
        for (int[] row: dp)
        {
            Arrays.fill(row, -1);
        }
        int n = s.length();
        int count = 0;

        // 2 for loops are required to check for
        // all the palindromes in the string.
        for (int i = 0; i < n; i++)
        {
            for (int j = i + 1; j < n; j++)
            {
                // Increment count for every palindrome
                if (isPal(s, i, j) != 0)
                    count++;
            }
        }

        // return total palindromic substrings
        return count;
    }

    public static void main(String[] args) {
        String s = "abbaeae";

        System.out.println(countSubstrings(s));
    }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# 2D matrix
dp = [[-1 for i in range(1001)]
          for j in range(1001)]

def isPal(s, i, j):

    # Base condition
    if (i > j):
        return 1

    # Check if the recursive tree
    # for given i, j
    # has already been executed
    if (dp[i][j] != -1):
        return dp[i][j]

    # If first and last characters of
    # substring are unequal
    if (s[i] != s[j]):
        dp[i][j] = 0
        return dp[i][j]

    # Memoization
    dp[i][j] = isPal(s, i + 1, j - 1)

    return dp[i][j]

def countSubstrings(s):

    n = len(s)

    count = 0

    # 2 for loops are required to check for
    # all the palindromes in the string.
    for i in range(n):
        for j in range(i + 1, n):

            # Increment count for every palindrome
            if (isPal(s, i, j)):
                count += 1

    # Return total palindromic substrings
    return count

# Driver code
s = "abbaeae"

print(countSubstrings(s))

# This code is contributed by rag2127
```

## C#

```
using System;

class GFG{

// 2D matrix
static int[,] dp = new int[1001, 1001];

static int isPal(string s, int i, int j)
{

    // Base condition
    if (i > j)
        return 1;

    // Check if the recursive tree
    // for given i, j
    // has already been executed
    if (dp[i, j] != -1)
        return dp[i, j];

    // If first and last characters of
    // substring are unequal
    if (s[i] != s[j])
        return dp[i, j] = 0;

    // Memoization
    return dp[i, j] = isPal(s, i + 1, j - 1);
}

static int countSubstrings(string s)
{
    for(int i = 0; i < 1001; i++)
    {
        for(int j = 0; j < 1001; j++)
        {
            dp[i, j] = -1;
        }
    }

    int n = s.Length;
    int count = 0;

    // 2 for loops are required to check for
    // all the palindromes in the string.
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Increment count for every palindrome
            if (isPal(s, i, j) != 0)
                count++;
        }
    }

    // Return total palindromic substrings
    return count;
}

// Driver Code   
static void Main()
{
    string s = "abbaeae";

    Console.WriteLine(countSubstrings(s));
}
}

// This code is contributed by divyesh072019
```

**Output**

```
4
```

[统计一个字符串中所有回文子字符串|集合 2](https://www.geeksforgeeks.org/count-palindrome-sub-strings-string-set-2/)

本文由[**Nishant _ Singh(Pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。