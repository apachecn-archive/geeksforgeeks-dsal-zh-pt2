# 第一半和第二半之和相同的最长偶数长度子串

> 原文:[https://www . geesforgeks . org/最长-偶数长度-子串-和-第一-第二-半/](https://www.geeksforgeeks.org/longest-even-length-substring-sum-first-second-half/)

给定一个数字串“str”，求“str”的最长子串的长度，使得子串的长度为 2k 个数字，左 k 个数字的和等于右 k 个数字的和。
**例:**

```
Input: str = "123123"
Output: 6
The complete string is of even length and sum of first and second
half digits is same

Input: str = "1538023"
Output: 4
The longest substring with same first and second half sum is "5380"
```

**简单的解决方案【O(n<sup>3</sup>)】**
简单的解决方案是检查每个偶长度的子串。下面是简单方法的实现。

## C++

```
// A simple C++ based program to find length of longest even length
// substring with same sum of digits in left and right
#include<bits/stdc++.h>
using namespace std;

int findLength(char *str)
{
    int n = strlen(str);
    int maxlen =0; // Initialize result

    // Choose starting point of every substring
    for (int i=0; i<n; i++)
    {
        // Choose ending point of even length substring
        for (int j =i+1; j<n; j += 2)
        {
            int length = j-i+1;//Find length of current substr

            // Calculate left & right sums for current substr
            int leftsum = 0, rightsum =0;
            for (int k =0; k<length/2; k++)
            {
                leftsum += (str[i+k]-'0');
                rightsum += (str[i+k+length/2]-'0');
            }

            // Update result if needed
            if (leftsum == rightsum && maxlen < length)
                    maxlen = length;
        }
    }
    return maxlen;
}

// Driver program to test above function
int main(void)
{
    char str[] = "1538023";
    cout << "Length of the substring is "
         << findLength(str);
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// A simple C based program to find length of longest  even length
// substring with same sum of digits in left and right
#include<stdio.h>
#include<string.h>

int findLength(char *str)
{
    int n = strlen(str);
    int maxlen =0;  // Initialize result

    // Choose starting point of every substring
    for (int i=0; i<n; i++)
    {
        // Choose ending point of even length substring
        for (int j =i+1; j<n; j += 2)
        {
            int length = j-i+1;//Find length of current substr

            // Calculate left & right sums for current substr
            int leftsum = 0, rightsum =0;
            for (int k =0; k<length/2; k++)
            {
                leftsum  += (str[i+k]-'0');
                rightsum += (str[i+k+length/2]-'0');
            }

            // Update result if needed
            if (leftsum == rightsum && maxlen < length)
                    maxlen = length;
        }
    }
    return maxlen;
}

// Driver program to test above function
int main(void)
{
    char str[] = "1538023";
    printf("Length of the substring is %d", findLength(str));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A simple Java based program to find
// length of longest even length substring
// with same sum of digits in left and right
import java.io.*;

class GFG {

static int findLength(String str)
{
    int n = str.length();
    int maxlen = 0; // Initialize result

    // Choose starting point of every
    // substring
    for (int i = 0; i < n; i++)
    {
        // Choose ending point of even
        // length substring
        for (int j = i + 1; j < n; j += 2)
        {  
            // Find length of current substr
            int length = j - i + 1;

            // Calculate left & right sums
            // for current substr
            int leftsum = 0, rightsum = 0;
            for (int k = 0; k < length/2; k++)
            {
                leftsum += (str.charAt(i + k) - '0');
                rightsum += (str.charAt(i + k + length/2) - '0');
            }

            // Update result if needed
            if (leftsum == rightsum && maxlen < length)
                    maxlen = length;
        }
    }
    return maxlen;
}

// Driver program to test above function
public static void main(String[] args)
{
    String str = "1538023";
    System.out.println("Length of the substring is "
                       + findLength(str));
}
}

// This code is contrtibuted by Prerna Saini
```

## 蟒蛇 3

```
# A simple Python 3 based
# program to find length
# of longest even length
# substring with same sum
# of digits in left and right

def findLength(str):

    n = len(str)
    maxlen = 0 # Initialize result

    # Choose starting point
        # of every substring
    for i in range(0, n):

        # Choose ending point
                # of even length substring
        for j in range(i+1, n, 2):

                        # Find length of current substr
            length = j - i + 1

            # Calculate left & right
                        # sums for current substr
            leftsum = 0
            rightsum =0
            for k in range(0,int(length/2)):

                leftsum += (int(str[i+k])-int('0'))
                rightsum += (int(str[i+k+int(length/2)])-int('0'))

            # Update result if needed
            if (leftsum == rightsum and maxlen < length):
                    maxlen = length

    return maxlen

# Driver program to
# test above function
str = "1538023"
print("Length of the substring is",
       findLength(str))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// A simple C# based program to find
// length of longest even length substring
// with same sum of digits in left and right
using System;

class GFG {

static int findLength(String str)
{
    int n = str.Length;
    int maxlen = 0; // Initialize result

    // Choose starting point
    // of every substring
    for (int i = 0; i < n; i++)
    {
        // Choose ending point of
        // even length substring
        for (int j = i + 1; j < n; j += 2)
        {
            // Find length of current substr
            int length = j - i + 1;

            // Calculate left & right sums
            // for current substr
            int leftsum = 0, rightsum = 0;
            for (int k = 0; k < length/2; k++)
            {
                leftsum += (str[i + k] - '0');
                rightsum += (str[i + k + length/2] - '0');
            }

            // Update result if needed
            if (leftsum == rightsum &&
                maxlen < length)
                    maxlen = length;
        }
    }
    return maxlen;
}

  // Driver program to test above function
  public static void Main()
  {
    String str = "1538023";
    Console.Write("Length of the substring is " +
                                findLength(str));
  }
}

// This code is contrtibuted by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A simple PHP based program to find length of
// longest even length substring with same sum
// of digits in left and right

function findLength($str)
{
    $n = strlen($str);
    $maxlen = 0; // Initialize result

    // Choose starting point of every substring
    for ($i = 0; $i < $n; $i++)
    {
        // Choose ending point of even
        // length substring
        for ($j = $i + 1; $j < $n; $j += 2)
        {
            $length = $j - $i + 1; // Find length of current substr

            // Calculate left & right sums
            // for current substr
            $leftsum = 0;
            $rightsum = 0;
            for ($k = 0; $k < $length / 2; $k++)
            {
                $leftsum += ($str[$i + $k] - '0');
                $rightsum += ($str[$i + $k +
                              $length / 2] - '0');
            }

            // Update result if needed
            if ($leftsum == $rightsum &&
                $maxlen < $length)
                    $maxlen = $length;
        }
    }
    return $maxlen;
}

// Driver Code
$str = "1538023";
echo("Length of the substring is ");
echo(findLength($str));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// A simple Javascript based program to find
// length of longest even length substring
// with same sum of digits in left and right

    function findLength(str)
    {
        let n = str.length;
        let maxlen = 0; // Initialize result

        // Choose starting point of every
        // substring
        for (let i = 0; i < n; i++)
        {
            // Choose ending point of even
            // length substring
            for (let j = i + 1; j < n; j += 2)
            {  
                // Find length of current substr
                let length = j - i + 1;

                // Calculate left & right sums
                // for current substr
                let leftsum = 0, rightsum = 0;
                for (let k = 0; k < Math.floor(length/2); k++)
                {
                    leftsum += (str[i+k] - '0');
                    rightsum += (str[i+k+Math.floor(length/2)] - '0');
                }

                // Update result if needed
                if (leftsum == rightsum && maxlen < length)
                        maxlen = length;
            }
        }
        return maxlen;
    }

    let str = "1538023";
    document.write("Length of the substring is " + findLength(str));

    // This code is contributed by rag2127

</script>
```

**输出:**

```
Length of the substring is 4
```

**动态编程【O(n <sup>2</sup> )和 O(n <sup>2</sup> )额外空间】**
使用**动态编程**可以将上述解决方案优化为在 O(n <sup>2</sup> 中工作。这个想法是建立一个存储子字符串总和的 2D 表。下面是动态编程方法的实现。

## C++

```
// A C++ based program that uses Dynamic
// Programming to find length of the
// longest even substring with same sum
// of digits in left and right half
#include<bits/stdc++.h>
using namespace std;

int findLength(char *str)
{
    int n = strlen(str);
    int maxlen = 0; // Initialize result

    // A 2D table where sum[i][j] stores
    // sum of digits from str[i] to str[j].
    // Only filled entries are the entries
    // where j >= i
    int sum[n][n];

    // Fill the diagonal values for
    // substrings of length 1
    for (int i =0; i<n; i++)
        sum[i][i] = str[i]-'0';

    // Fill entries for substrings of
    // length 2 to n
    for (int len = 2; len <= n; len++)
    {
        // Pick i and j for current substring
        for (int i = 0; i < n - len + 1; i++)
        {
            int j = i + len - 1;
            int k = len / 2;

            // Calculate value of sum[i][j]
            sum[i][j] = sum[i][j - k] +
                        sum[j - k + 1][j];

            // Update result if 'len' is even,
            // left and right sums are same and
            // len is more than maxlen
            if (len % 2 == 0 &&
                sum[i][j - k] == sum[(j - k + 1)][j] &&
                len > maxlen)
                maxlen = len;
        }
    }
    return maxlen;
}

// Driver Code
int main(void)
{
    char str[] = "153803";
    cout << "Length of the substring is "
         << findLength(str);
    return 0;
}

// This code is contributed
// by Mukul Singh.
```

## C

```
// A C based program that uses Dynamic Programming to find length of the
// longest even substring with same sum of digits in left and right half
#include <stdio.h>
#include <string.h>

int findLength(char *str)
{
    int n = strlen(str);
    int maxlen = 0; // Initialize result

    // A 2D table where sum[i][j] stores sum of digits
    // from str[i] to str[j].  Only filled entries are
    // the entries where j >= i
    int sum[n][n];

    // Fill the diagonal values for sunstrings of length 1
    for (int i =0; i<n; i++)
        sum[i][i] = str[i]-'0';

    // Fill entries for substrings of length 2 to n
    for (int len=2; len<=n; len++)
    {
        // Pick i and j for current substring
        for (int i=0; i<n-len+1; i++)
        {
            int j = i+len-1;
            int k = len/2;

            // Calculate value of sum[i][j]
            sum[i][j] = sum[i][j-k] + sum[j-k+1][j];

            // Update result if 'len' is even, left and right
            // sums are same and len is more than maxlen
            if (len%2 == 0 && sum[i][j-k] == sum[(j-k+1)][j]
                           && len > maxlen)
                 maxlen = len;
        }
    }
    return maxlen;
}

// Driver program to test above function
int main(void)
{
    char str[] = "153803";
    printf("Length of the substring is %d", findLength(str));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java based program that uses Dynamic
// Programming to find length of the longest
// even substring with same sum of digits
// in left and right half
import java.io.*;

class GFG {

static int findLength(String str)
{
    int n = str.length();
    int maxlen = 0; // Initialize result

    // A 2D table where sum[i][j] stores
    // sum of digits from str[i] to str[j].
    // Only filled entries are the entries
    // where j >= i
    int sum[][] = new int[n][n];

    // Fill the diagonal values for
    // substrings of length 1
    for (int i = 0; i < n; i++)
        sum[i][i] = str.charAt(i) - '0';

    // Fill entries for substrings of
    // length 2 to n
    for (int len = 2; len <= n; len++)
    {
        // Pick i and j for current substring
        for (int i = 0; i < n - len + 1; i++)
        {
            int j = i + len - 1;
            int k = len/2;

            // Calculate value of sum[i][j]
            sum[i][j] = sum[i][j-k] +
                        sum[j-k+1][j];

            // Update result if 'len' is even,
            // left and right sums are same
            // and len is more than maxlen
            if (len % 2 == 0 && sum[i][j-k] ==
                sum[(j-k+1)][j] && len > maxlen)
                maxlen = len;
        }
    }
    return maxlen;
}

// Driver program to test above function
public static void main(String[] args)
{
    String str = "153803";
    System.out.println("Length of the substring is "
                       + findLength(str));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python3 code that uses Dynamic Programming
# to find length of the longest even substring
# with same sum of digits in left and right half

def findLength(string):

    n = len(string)
    maxlen = 0 # Initialize result

    # A 2D table where sum[i][j] stores
    # sum of digits from str[i] to str[j].
    # Only filled entries are the entries
    # where j >= i
    Sum = [[0 for x in range(n)]
              for y in range(n)]

    # Fill the diagonal values for
    # substrings of length 1
    for i in range(0, n):
        Sum[i][i] = int(string[i])

    # Fill entries for substrings
    # of length 2 to n
    for length in range(2, n + 1):

        # Pick i and j for current substring
        for i in range(0, n - length + 1):

            j = i + length - 1
            k = length // 2

            # Calculate value of sum[i][j]
            Sum[i][j] = (Sum[i][j - k] +
                         Sum[j - k + 1][j])

            # Update result if 'len' is even,
            # left and right sums are same and
            # len is more than maxlen
            if (length % 2 == 0 and
                Sum[i][j - k] == Sum[(j - k + 1)][j] and
                length > maxlen):
                maxlen = length

    return maxlen

# Driver Code
if __name__ == "__main__":

    string = "153803"
    print("Length of the substring is",
                    findLength(string))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// A C# based program that uses Dynamic
// Programming to find length of the longest
// even substring with same sum of digits
// in left and right half
using System;

class GFG {

static int findLength(String str)
{
    int n = str.Length;
    int maxlen = 0; // Initialize result

    // A 2D table where sum[i][j] stores
    // sum of digits from str[i] to str[j].
    // Only filled entries are the entries
    // where j >= i
    int[,] sum = new int[n, n];

    // Fill the diagonal values for
    // substrings of length 1
    for (int i = 0; i < n; i++)
        sum[i, i] = str[i] - '0';

    // Fill entries for substrings of
    // length 2 to n
    for (int len = 2; len <= n; len++)
    {
        // Pick i and j for current substring
        for (int i = 0; i < n - len + 1; i++)
        {
            int j = i + len - 1;
            int k = len/2;

            // Calculate value of sum[i][j]
            sum[i, j] = sum[i, j-k] +
                        sum[j-k+1, j];

            // Update result if 'len' is even,
            // left and right sums are same
            // and len is more than maxlen
            if (len % 2 == 0 && sum[i, j-k] ==
                sum[(j-k+1), j] && len > maxlen)
                maxlen = len;
        }
    }
    return maxlen;
}

// Driver program to test above function
public static void Main()
{
    String str = "153803";
    Console.WriteLine("Length of the substring is "
                    + findLength(str));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP based program that uses Dynamic
// Programming to find length of the longest
// even substring with same sum of digits
// in left and right half

function findLength($str)
{
    $n = strlen($str);
    $maxlen = 0; // Initialize result

    // A 2D table where sum[i][j] stores sum
    // of digits from str[i] to str[j]. Only
    // filled entries are the entries where j >= i

    // Fill the diagonal values for
    // substrings of length 1
    for ($i = 0; $i < $n; $i++)
        $sum[$i][$i] = $str[$i] - '0';

    // Fill entries for substrings of
    // length 2 to n
    for ($len = 2; $len <= $n; $len++)
    {
        // Pick i and j for current substring
        for ($i = 0; $i < $n - $len + 1; $i++)
        {
            $j = $i + $len - 1;
            $k = $len / 2;

            // Calculate value of sum[i][j]
            $sum[$i][$j] = $sum[$i][$j - $k] +
                           $sum[$j - $k + 1][$j];

            // Update result if 'len' is even,
            // left and right sums are same and
            // len is more than maxlen
            if ($len % 2 == 0 &&
                $sum[$i][$j - $k] == $sum[($j - $k + 1)][$j] &&
                $len > $maxlen)
                $maxlen = $len;
        }
    }
    return $maxlen;
}

// Driver Code
$str = "153803";
echo("Length of the substring is ");
echo(findLength($str));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// A javascript based program that uses Dynamic
// Programming to find length of the longest
// even substring with same sum of digits
// in left and right half

function findLength(str)
{
    var n = str.length;
    var maxlen = 0; // Initialize result

    // A 2D table where sum[i][j] stores
    // sum of digits from str[i] to str[j].
    // Only filled entries are the entries
    // where j >= i
    var sum = Array(n).fill(0).map(x => Array(n).fill(0));

    // Fill the diagonal values for
    // substrings of length 1
    for (i = 0; i < n; i++)
        sum[i][i] = str.charAt(i).charCodeAt(0) - '0'.charCodeAt(0);

    // Fill entries for substrings of
    // length 2 to n
    for (len = 2; len <= n; len++)
    {
        // Pick i and j for current substring
        for (i = 0; i < n - len + 1; i++)
        {
            var j = i + len - 1;
            var k = parseInt(len/2);

            // Calculate value of sum[i][j]
            sum[i][j] = sum[i][j-k] +
                        sum[j-k+1][j];

            // Update result if 'len' is even,
            // left and right sums are same
            // and len is more than maxlen
            if (len % 2 == 0 && sum[i][j-k] ==
                sum[(j-k+1)][j] && len > maxlen)
                maxlen = len;
        }
    }
    return maxlen;
}

// Driver program to test above function
var str = "153803";
document.write("Length of the substring is "
                       + findLength(str));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
Length of the substring is 4
```

上述解决方案的时间复杂度为 O(n <sup>2</sup> ，但需要 O(n <sup>2</sup> )的额外空间。
**【A O(n)<sup>2</sup>)和 O(n)额外空间解】**
思路是用一维数组存储累计和。

## C++

```
// A O(n^2) time and O(n) extra space solution
#include<bits/stdc++.h>
using namespace std;

int findLength(string str, int n)
{
    int sum[n+1]; // To store cumulative sum from first digit to nth digit
    sum[0] = 0;

    /* Store cumulative sum of digits from first to last digit */
    for (int i = 1; i <= n; i++)
        sum[i] = (sum[i-1] + str[i-1]  - '0'); /* convert chars to int */

    int ans = 0; // initialize result

    /* consider all even length substrings one by one */
    for (int len = 2; len <= n; len += 2)
    {
        for (int i = 0; i <= n-len; i++)
        {
            int j = i + len - 1;

            /* Sum of first and second half is same than update ans */
            if (sum[i+len/2] - sum[i] == sum[i+len] - sum[i+len/2])
                ans = max(ans, len);
        }
    }
    return ans;
}

// Driver program to test above function
int main()
{
    string str = "123123";
    cout << "Length of the substring is " << findLength(str, str.length());
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of O(n^2) time
// and O(n) extra space solution
class GFG {

static int findLength(String str, int n)
{  
    // To store cumulative sum from
    // first digit to nth digit
    int sum[] = new int[ n + 1];
    sum[0] = 0;

    /* Store cumulative sum of digits
    from first to last digit */
    for (int i = 1; i <= n; i++)

        /* convert chars to int */
        sum[i] = (sum[i-1] + str.charAt(i-1)
                                    - '0');

    int ans = 0; // initialize result

    /* consider all even length
    substrings one by one */
    for (int len = 2; len <= n; len += 2)
    {
        for (int i = 0; i <= n-len; i++)
        {
            int j = i + len - 1;

            /* Sum of first and second half
            is same than update ans */
            if (sum[i+len/2] - sum[i] == sum[i+len]
                                   - sum[i+len/2])
                ans = Math.max(ans, len);
        }
    }
    return ans;
}

// Driver program to test above function
public static void main(String[] args)
{
    String str = "123123";
    System.out.println("Length of the substring is "
                    + findLength(str, str.length()));
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# A O(n^2) time and O(n) extra
# space solution in Python3
def findLength(string, n):

    # To store cumulative sum
    # from first digit to nth digit
    Sum = [0] * (n + 1)

    # Store cumulative sum of digits
    # from first to last digit
    for i in range(1, n + 1):
        Sum[i] = (Sum[i - 1] +
              int(string[i - 1])) # convert chars to int

    ans = 0 # initialize result

    # consider all even length
    # substrings one by one
    for length in range(2, n + 1, 2):

        for i in range(0, n - length + 1):

            j = i + length - 1

            # Sum of first and second half
            # is same than update ans
            if (Sum[i + length // 2] -
                Sum[i] == Sum[i + length] -
                Sum[i + length // 2]):
                ans = max(ans, length)

    return ans

# Driver code
if __name__ == "__main__":

    string = "123123"
    print("Length of the substring is",
           findLength(string, len(string)))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# implementation of O(n^2) time and O(n)
// extra space solution
using System;

class GFG {

    static int findLength(string str, int n)
    {

        // To store cumulative sum from
        // first digit to nth digit
        int []sum = new int[ n + 1];
        sum[0] = 0;

        /* Store cumulative sum of digits
        from first to last digit */
        for (int i = 1; i <= n; i++)

            /* convert chars to int */
            sum[i] = (sum[i-1] + str[i-1]
                                   - '0');

        int ans = 0; // initialize result

        /* consider all even length
        substrings one by one */
        for (int len = 2; len <= n; len += 2)
        {
            for (int i = 0; i <= n-len; i++)
            {
                // int j = i + len - 1;

                /* Sum of first and second half
                is same than update ans */
                if (sum[i+len/2] - sum[i] ==
                     sum[i+len] - sum[i+len/2])
                    ans = Math.Max(ans, len);
            }
        }

        return ans;
    }

    // Driver program to test above function
    public static void Main()
    {
        string str = "123123";
        Console.Write("Length of the substring"
        + " is " + findLength(str, str.Length));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A O(n^2) time and O(n) extra space solution

function findLength($str, $n)
{
    $sum[$n + 1] = array(); // To store cumulative sum from
                            // first digit to nth digit
    $sum[0] = 0;

    /* Store cumulative sum of digits
    from first to last digit */
    for ($i = 1; $i <= $n; $i++)
        $sum[$i] = ($sum[$i - 1] +
                    $str[$i - 1] - '0'); /* convert chars to int */

    $ans = 0; // initialize result

    /* consider all even length
    substrings one by one */
    for ($len = 2; $len <= $n; $len += 2)
    {
        for ($i = 0; $i <= $n - $len; $i++)
        {
            $j = $i + $len - 1;

            /* Sum of first and second half is
            same than update ans */
            if ($sum[$i + $len / 2] - $sum[$i] == $sum[$i + $len] -
                                                  $sum[$i + $len / 2])
                $ans = max($ans, $len);
        }
    }
    return $ans;
}

// Driver Code
$str = "123123";
echo "Length of the substring is " .
     findLength($str, strlen($str));

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// javascript implementation of O(n^2) time
// and O(n) extra space solution
function findLength(str , n)
{  
    // To store cumulative sum from
    // first digit to nth digit
    var sum = Array.from({length: n+1}, (_, i) => 0);
    sum[0] = 0;

    /* Store cumulative sum of digits
    from first to last digit */
    for (var i = 1; i <= n; i++)

        /* convert chars to var */
        sum[i] = (sum[i-1] + str.charAt(i-1).charCodeAt(0)
                                    - '0'.charCodeAt(0));

    var ans = 0; // initialize result

    /* consider all even length
    substrings one by one */
    for (var len = 2; len <= n; len += 2)
    {
        for (i = 0; i <= n-len; i++)
        {
            var j = i + len - 1;

            /* Sum of first and second half
            is same than update ans */
            if (sum[i+parseInt(len/2)] - sum[i] == sum[i+len]
                                   - sum[i+parseInt(len/2)])
                ans = Math.max(ans, len);
        }
    }
    return ans;
}

// Driver program to test above function
var str = "123123";
document.write("Length of the substring is "
                + findLength(str, str.length));

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
Length of the substring is 6
```

感谢 Gaurav Ahirwar 提出这个方法。
**【A O(n)<sup>2</sup>)时间和 O(1)额外空间解】**
思路是考虑所有可能的中点(偶数长度子串的中点)，随着两边之和变得相等，不断向两边扩展，得到并更新最优长度。
以下是上述思路的实现。

## C++

```
// A O(n^2) time and O(1) extra space solution
#include<bits/stdc++.h>
using namespace std;

int findLength(string str, int n)
{
    int ans = 0; // Initialize result

    // Consider all possible midpoints one by one
    for (int i = 0; i <= n-2; i++)
    {
        /* For current midpoint 'i', keep expanding substring on
           both sides, if sum of both sides becomes equal update
           ans */
        int l = i, r = i + 1;

        /* initialize left and right sum */
        int lsum = 0, rsum = 0;

        /* move on both sides till indexes go out of bounds */
        while (r < n && l >= 0)
        {
            lsum += str[l] - '0';
            rsum += str[r] - '0';
            if (lsum == rsum)
                ans = max(ans, r-l+1);
            l--;
            r++;
        }
    }
    return ans;
}

// Driver program to test above function
int main()
{
    string str = "123123";
    cout << "Length of the substring is " << findLength(str, str.length());
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A O(n^2) time and O(1) extra space solution

class GFG {

    static int findLength(String str, int n) {
        int ans = 0; // Initialize result

        // Consider all possible midpoints one by one
        for (int i = 0; i <= n - 2; i++) {
            /* For current midpoint 'i', keep expanding substring on
           both sides, if sum of both sides becomes equal update
           ans */
            int l = i, r = i + 1;

            /* initialize left and right sum */
            int lsum = 0, rsum = 0;

            /* move on both sides till indexes go out of bounds */
            while (r < n && l >= 0) {
                lsum += str.charAt(l) - '0';
                rsum += str.charAt(r) - '0';
                if (lsum == rsum) {
                    ans = Math.max(ans, r - l + 1);
                }
                l--;
                r++;
            }
        }
        return ans;
    }

// Driver program to test above function
    static public void main(String[] args) {
        String str = "123123";
        System.out.println("Length of the substring is "
                + findLength(str, str.length()));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# A O(n^2) time and O(n) extra
# space solution
def findLength(st, n):

    # To store cumulative total from
    # first digit to nth digit
    total = [0] * (n + 1)

    # Store cumulative total of digits
    # from first to last digit
    for i in range(1, n + 1):

        # convert chars to int
        total[i] = (total[i - 1] +
                   int(st[i - 1]) - int('0'))

    ans = 0 # initialize result

    # consider all even length
    # substings one by one
    l = 2
    while(l <= n):

        for i in range(n - l + 1):

            # total of first and second half
            # is same than update ans
            if (total[i + int(l / 2)] -
                total[i] == total[i + l] -
                total[i + int(l / 2)]):
                ans = max(ans, l)
        l = l + 2

    return ans

# Driver Code
st = "123123"
print("Length of the substring is",
           findLength(st, len(st)))

# This code is contributed by ash264
```

## C#

```

// A O(n^2) time and O(1) extra space solution
using System;
public class GFG {

    static int findLength(String str, int n) {
        int ans = 0; // Initialize result

        // Consider all possible midpoints one by one
        for (int i = 0; i <= n - 2; i++) {
            /* For current midpoint 'i', keep expanding substring on
           both sides, if sum of both sides becomes equal update
           ans */
            int l = i, r = i + 1;

            /* initialize left and right sum */
            int lsum = 0, rsum = 0;

            /* move on both sides till indexes go out of bounds */
            while (r < n && l >= 0) {
                lsum += str[l] - '0';
                rsum += str[r] - '0';
                if (lsum == rsum) {
                    ans = Math.Max(ans, r - l + 1);
                }
                l--;
                r++;
            }
        }
        return ans;
    }

// Driver program to test above function
    static public void Main() {
        String str = "123123";
        Console.Write("Length of the substring is "
                + findLength(str, str.Length));
    }
}

// This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A O(n^2) time and O(1) extra space solution

function findLength($str, $n)
{
    $ans = 0; // Initialize result

    // Consider all possible midpoints one by one
    for ($i = 0; $i <= $n - 2; $i++)
    {
        /* For current midpoint 'i',
        keep expanding substring on
        both sides, if sum of both
        sides becomes equal update
        ans */
        $l = $i;
        $r = $i + 1;

        /* initialize left and right sum */
        $lsum = 0;
        $rsum = 0;

        /* move on both sides till
        indexes go out of bounds */
        while ($r < $n && $l >= 0)
        {
            $lsum += $str[$l] - '0';
            $rsum += $str[$r] - '0';
            if ($lsum == $rsum)
                $ans = max($ans, $r - $l + 1);
            $l--;
            $r++;
        }
    }
    return $ans;
}

// Driver program to test above function

$str = "123123";
echo "Length of the substring is " .
        findLength($str, strlen($str));
return 0;

// This code is contributed by Ita_c.
?>
```

## java 描述语言

```
<script>
// A O(n^2) time and O(1) extra space solution

    function findLength(str,n)
    {
        let ans = 0; // Initialize result

        // Consider all possible midpoints one by one
        for (let i = 0; i <= n - 2; i++) {
            /* For current midpoint 'i', keep expanding substring on
           both sides, if sum of both sides becomes equal update
           ans */
            let l = i, r = i + 1;

            /* initialize left and right sum */
            let lsum = 0, rsum = 0;

            /* move on both sides till indexes go out of bounds */
            while (r < n && l >= 0) {
                lsum += str.charAt(l) - '0';
                rsum += str.charAt(r) - '0';
                if (lsum == rsum) {
                    ans = Math.max(ans, r - l + 1);
                }
                l--;
                r++;
            }
        }
        return ans;
    }

    // Driver program to test above function
    let str="123123";
    document.write("Length of the substring is "
                + findLength(str, str.length));

    // This code is contributed by avanitrachhadiya2155
</script>
```

**输出:**

```
Length of the substring is 6
```

感谢 Gaurav Ahirwar 提出这个方法。
本文由**阿诗班萨尔**供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息