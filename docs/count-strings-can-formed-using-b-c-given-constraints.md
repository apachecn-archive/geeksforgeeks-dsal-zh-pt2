# 在给定约束条件下，使用 a、b 和 c 可以形成的字符串数

> 原文:[https://www . geesforgeks . org/count-strings-can-formed-using-B- c-given-constraints/](https://www.geeksforgeeks.org/count-strings-can-formed-using-b-c-given-constraints/)

给定长度 n，计算使用“a”、“b”和“c”可以生成的长度为 n 的字符串数，最多允许一个“b”和两个“c”。
**例:**

```
Input : n = 3 
Output : 19 
Below strings follow given constraints:
aaa aab aac aba abc aca acb acc baa
bac bca bcc caa cab cac cba cbc cca ccb 

Input  : n = 4
Output : 39
```

在谷歌采访中问道

一个**简单的解决方案**是递归地计算所有可能的字符串组合，这些组合可以被模式化到后面的‘a’、‘b’和‘c’。
以下是上述想法的实现

## C++

```
// C++ program to count number of strings
// of n characters with
#include<bits/stdc++.h>
using namespace std;

// n is total number of characters.
// bCount and cCount are counts of 'b'
// and 'c' respectively.
int countStr(int n, int bCount, int cCount)
{
    // Base cases
    if (bCount < 0 || cCount < 0) return 0;
    if (n == 0) return 1;
    if (bCount == 0 && cCount == 0) return 1;

    // Three cases, we choose, a or b or c
    // In all three cases n decreases by 1.
    int res = countStr(n-1, bCount, cCount);
    res += countStr(n-1, bCount-1, cCount);
    res += countStr(n-1, bCount, cCount-1);

    return res;
}

// Driver code
int main()
{
    int n = 3;  // Total number of characters
    cout << countStr(n, 1, 2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number
// of strings of n characters with
import java.io.*;

class GFG
{

// n is total number of characters.
// bCount and cCount are counts of 'b'
// and 'c' respectively.
static int countStr(int n,
                    int bCount,
                    int cCount)
{
    // Base cases
    if (bCount < 0 || cCount < 0) return 0;
    if (n == 0) return 1;
    if (bCount == 0 && cCount == 0) return 1;

    // Three cases, we choose, a or b or c
    // In all three cases n decreases by 1.
    int res = countStr(n - 1, bCount, cCount);
    res += countStr(n - 1, bCount - 1, cCount);
    res += countStr(n - 1, bCount, cCount - 1);

    return res;
}

// Driver code
public static void main (String[] args)
{
    int n = 3; // Total number of characters
    System.out.println(countStr(n, 1, 2));
}
}

// This code is contributed by akt_mit
```

## 蟒蛇 3

```
# Python 3 program to
# count number of strings
# of n characters with

# n is total number of characters.
# bCount and cCount are counts
# of 'b' and 'c' respectively.
def countStr(n, bCount, cCount):

    # Base cases
    if (bCount < 0 or cCount < 0):
        return 0
    if (n == 0) :
        return 1
    if (bCount == 0 and cCount == 0):
        return 1

    # Three cases, we choose, a or b or c
    # In all three cases n decreases by 1.
    res = countStr(n - 1, bCount, cCount)
    res += countStr(n - 1, bCount - 1, cCount)
    res += countStr(n - 1, bCount, cCount - 1)

    return res

# Driver code
if __name__ =="__main__":
    n = 3 # Total number of characters
    print(countStr(n, 1, 2))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to count number
// of strings of n characters
// with a, b and c under given
// constraints
using System;

class GFG
{

// n is total number of
// characters. bCount and
// cCount are counts of
// 'b' and 'c' respectively.
static int countStr(int n,
                    int bCount,
                    int cCount)
{
    // Base cases
    if (bCount < 0 || cCount < 0)
        return 0;
    if (n == 0) return 1;
    if (bCount == 0 && cCount == 0)
        return 1;

    // Three cases, we choose,
    // a or b or c. In all three
    // cases n decreases by 1.
    int res = countStr(n - 1,
                       bCount, cCount);
    res += countStr(n - 1,
                    bCount - 1, cCount);
    res += countStr(n - 1,
                    bCount, cCount - 1);

    return res;
}

// Driver code
static public void Main ()
{
    // Total number
    // of characters
    int n = 3;
    Console.WriteLine(countStr(n, 1, 2));
}
}

// This code is contributed by aj_36
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of
// strings of n characters with

// n is total number of characters.
// bCount and cCount are counts
// of 'b' and 'c' respectively.
function countStr($n, $bCount,
                      $cCount)
{
    // Base cases
    if ($bCount < 0 ||
        $cCount < 0)
        return 0;
    if ($n == 0)
    return 1;
    if ($bCount == 0 &&
        $cCount == 0)
        return 1;

    // Three cases, we choose,
    // a or b or c. In all three
    // cases n decreases by 1.
    $res = countStr($n - 1,
                    $bCount,
                    $cCount);
    $res += countStr($n - 1,
                     $bCount - 1,
                     $cCount);
    $res += countStr($n - 1,
                     $bCount,
                     $cCount - 1);

    return $res;
}

// Driver code
$n = 3; // Total number
        // of characters
echo countStr($n, 1, 2);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// n is total number of characters.
// bCount and cCount are counts of 'b'
// and 'c' respectively.
function countStr(n, bCount, cCount)
{

    // Base cases
    if (bCount < 0 || cCount < 0) return 0;
    if (n == 0) return 1;
    if (bCount == 0 && cCount == 0) return 1;

    // Three cases, we choose, a or b or c
    // In all three cases n decreases by 1.
    let res = countStr(n - 1, bCount, cCount);
    res += countStr(n - 1, bCount - 1, cCount);
    res += countStr(n - 1, bCount, cCount - 1);

    return res;
}

// Driver Code
    let n = 3; // Total number of characters
    document.write(countStr(n, 1, 2));

        // This code is contributed by splevel62.
</script>
```

**输出:**

```
19
```

上述解的时间复杂度是指数的。

**高效解决方案**
如果我们淹没上面代码的递归树，我们会注意到相同的值会出现多次。因此，我们存储结果，如果重复，这些结果将在以后使用。

## C++

```
// C++ program to count number of strings
// of n characters with
#include<bits/stdc++.h>
using namespace std;

// n is total number of characters.
// bCount and cCount are counts of 'b'
// and 'c' respectively.
int countStrUtil(int dp[][2][3], int n, int bCount=1,
                 int cCount=2)
{
    // Base cases
    if (bCount < 0 || cCount < 0) return 0;
    if (n == 0) return 1;
    if (bCount == 0 && cCount == 0) return 1;

    // if we had saw this combination previously
    if (dp[n][bCount][cCount] != -1)
        return dp[n][bCount][cCount];

    // Three cases, we choose, a or b or c
    // In all three cases n decreases by 1.
    int res = countStrUtil(dp, n-1, bCount, cCount);
    res += countStrUtil(dp, n-1, bCount-1, cCount);
    res += countStrUtil(dp, n-1, bCount, cCount-1);

    return (dp[n][bCount][cCount] = res);
}

// A wrapper over countStrUtil()
int countStr(int n)
{
    int dp[n+1][2][3];
    memset(dp, -1, sizeof(dp));
    return countStrUtil(dp, n);
}

// Driver code
int main()
{
    int n = 3; // Total number of characters
    cout << countStr(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of strings
// of n characters with

class GFG
{
    // n is total number of characters.
    // bCount and cCount are counts of 'b'
    // and 'c' respectively.

    static int countStrUtil(int[][][] dp, int n,
                            int bCount, int cCount)
    {

        // Base cases
        if (bCount < 0 || cCount < 0)
        {
            return 0;
        }
        if (n == 0)
        {
            return 1;
        }
        if (bCount == 0 && cCount == 0)
        {
            return 1;
        }

        // if we had saw this combination previously
        if (dp[n][bCount][cCount] != -1)
        {
            return dp[n][bCount][cCount];
        }

        // Three cases, we choose, a or b or c
        // In all three cases n decreases by 1.
        int res = countStrUtil(dp, n - 1, bCount, cCount);
        res += countStrUtil(dp, n - 1, bCount - 1, cCount);
        res += countStrUtil(dp, n - 1, bCount, cCount - 1);

        return (dp[n][bCount][cCount] = res);
    }

    // A wrapper over countStrUtil()
    static int countStr(int n, int bCount, int cCount)
    {
        int[][][] dp = new int[n + 1][2][3];
        for (int i = 0; i < n + 1; i++)
        {
            for (int j = 0; j < 2; j++)
            {
                for (int k = 0; k < 3; k++)
                {
                    dp[i][j][k] = -1;
                }
            }
        }
        return countStrUtil(dp, n,bCount,cCount);
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 3; // Total number of characters
        int bCount = 1, cCount = 2;
        System.out.println(countStr(n,bCount,cCount));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to count number of strings
# of n characters with

# n is total number of characters.
# bCount and cCount are counts of 'b'
# and 'c' respectively.
def countStrUtil(dp, n, bCount=1,cCount=2):

    # Base cases
    if (bCount < 0 or cCount < 0):
        return 0
    if (n == 0):
        return 1
    if (bCount == 0 and cCount == 0):
        return 1

    # if we had saw this combination previously
    if (dp[n][bCount][cCount] != -1):
        return dp[n][bCount][cCount]

    # Three cases, we choose, a or b or c
    # In all three cases n decreases by 1.
    res = countStrUtil(dp, n-1, bCount, cCount)
    res += countStrUtil(dp, n-1, bCount-1, cCount)
    res += countStrUtil(dp, n-1, bCount, cCount-1)

    dp[n][bCount][cCount] = res
    return dp[n][bCount][cCount]

# A wrapper over countStrUtil()
def countStr(n):

    dp = [ [ [-1 for x in range(n+2)] for y in range(3)]for z in range(4)]
    return countStrUtil(dp, n)

# Driver code
if __name__ == "__main__":

    n = 3 # Total number of characters
    print(countStr(n))

# This code is contributed by chitranayal   
```

## C#

```
// C# program to count number of strings
// of n characters with
using System;

class GFG
{
    // n is total number of characters.
    // bCount and cCount are counts of 'b'
    // and 'c' respectively.
    static int countStrUtil(int[,,] dp, int n,
                    int bCount=1, int cCount=2)
    {
        // Base cases
        if (bCount < 0 || cCount < 0)
            return 0;
        if (n == 0)
            return 1;
        if (bCount == 0 && cCount == 0)
            return 1;

        // if we had saw this combination previously
        if (dp[n,bCount,cCount] != -1)
            return dp[n,bCount,cCount];

        // Three cases, we choose, a or b or c
        // In all three cases n decreases by 1.
        int res = countStrUtil(dp, n - 1, bCount, cCount);
        res += countStrUtil(dp, n - 1, bCount - 1, cCount);
        res += countStrUtil(dp, n - 1, bCount, cCount - 1);

        return (dp[n, bCount, cCount] = res);
    }

    // A wrapper over countStrUtil()
    static int countStr(int n)
    {
        int[,,] dp = new int[n + 1, 2, 3];
        for(int i = 0; i < n + 1; i++)
            for(int j = 0; j < 2; j++)
                for(int k = 0; k < 3; k++)
                    dp[i, j, k] = -1;
        return countStrUtil(dp, n);
    }

    // Driver code
    static void Main()
    {
        int n = 3; // Total number of characters

        Console.Write(countStr(n));
    }
}

// This code is contributed by DrRoot_
```

## java 描述语言

```
<script>

// javascript program to count number of strings
// of n characters with

    // n is total number of characters.
    // bCount and cCount are counts of 'b'
    // and 'c' respectively.

    function countStrUtil(dp , n, bCount , cCount)
    {

        // Base cases
        if (bCount < 0 || cCount < 0)
        {
            return 0;
        }
        if (n == 0)
        {
            return 1;
        }
        if (bCount == 0 && cCount == 0)
        {
            return 1;
        }

        // if we had saw this combination previously
        if (dp[n][bCount][cCount] != -1)
        {
            return dp[n][bCount][cCount];
        }

        // Three cases, we choose, a or b or c
        // In all three cases n decreases by 1.
        var res = countStrUtil(dp, n - 1, bCount, cCount);
        res += countStrUtil(dp, n - 1, bCount - 1, cCount);
        res += countStrUtil(dp, n - 1, bCount, cCount - 1);

        return (dp[n][bCount][cCount] = res);
    }

    // A wrapper over countStrUtil()
    function countStr(n , bCount , cCount)
    {
        dp = Array(n+1).fill(0).map
        (x => Array(2).fill(0).map
        (x => Array(3).fill(0)));
        for (i = 0; i < n + 1; i++)
        {
            for (j = 0; j < 2; j++)
            {
                for (k = 0; k < 3; k++)
                {
                    dp[i][j][k] = -1;
                }
            }
        }
        return countStrUtil(dp, n,bCount,cCount);
    }

// Driver code
var n = 3; // Total number of characters
var bCount = 1, cCount = 2;
document.write(countStr(n,bCount,cCount));

// This code contributed by shikhasingrajput

</script>
```

**输出:**

```
19
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
感谢懒先生提出以上解决方案。
**在 0(1)时间内有效的解决方案:**

我们可以应用组合学的概念在恒定时间内解决这个问题。我们可能会回想起这样一个公式，我们可以排列的方式的数量总共有 n 个对象，其中 p 个对象是一种类型，q 个对象是另一种类型，r 个对象是第三种类型就是 **n！/(p！q！r！)**

让我们一步一步地解决问题。

没有“b”和“c”我们能组成多少个字符串？答案是 1，因为我们只能以一种方式排列一个仅由“a”组成的字符串，该字符串将是 *aaaa。(n 次)*。

一个“b”可以组成多少个字符串？答案是 n，因为我们可以安排一个由(n-1)“a”和 1“b”组成的字符串是 n！/(n-1)！= n。c 也一样。

我们可以用两个位置组成多少个字符串，用“b”和/或“c”填充？答案是 n*(n-1) + n*(n-1)/2。因为，根据我们给定的约束条件，这两个位置可以是 1 'b '和 1 'c '或 2 'c '。对于第一种情况，排列总数为 n！/(n-2)！= n*(n-1)对于第二种情况，即 n！/(2!(n-2)！)= n*(n-1)/2。

最后，我们可以用 3 个位置组成多少个字符串，用“b”和/或“c”填充？答案是(n-2)*(n-1)*n/2。因为，根据我们给定的约束，这 3 个位置只能由 1 'b '和 2'c '组成。所以，排列总数是 n！/(2!(n-3)！)= (n-2)*(n-1)*n/2。

## C++

```
// A O(1) CPP program to find number of strings
// that can be made under given constraints.
#include<bits/stdc++.h>
using namespace std;
int countStr(int n){

    int count = 0;

    if(n>=1){
        //aaa...
        count += 1;
        //b...aaa...
          count += n;
        //c...aaa...
        count += n;

        if(n>=2){
          //bc...aaa...
          count += n*(n-1);
          //cc...aaa...
          count += n*(n-1)/2;

          if(n>=3){
            //bcc...aaa...
            count += (n-2)*(n-1)*n/2;
          }
        }

    }

    return count;

}

// Driver code
int main()
{
  int n = 3;
  cout << countStr(n);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A O(1) Java program to
// find number of strings
// that can be made under
// given constraints.
import java.io.*;

class GFG
{
    static int countStr(int n)
    {
    return 1 + (n * 2) +
           (n * ((n * n) - 1) / 2);
    }

// Driver code
public static void main (String[] args)
{
    int n = 3;
    System.out.println( countStr(n));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# A O(1) Python3 program to find
# number of strings that can be
# made under given constraints.

def countStr(n):
    return (1 + (n * 2) +
                (n * ((n * n) - 1) // 2))

# Driver code
if __name__ == "__main__":
    n = 3
    print(countStr(n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// A O(1) C# program to
// find number of strings
// that can be made under
// given constraints.
using System;

class GFG
{
    static int countStr(int n)
    {
    return 1 + (n * 2) +
          (n * ((n * n) - 1) / 2);
    }

// Driver code
static public void Main ()
{
    int n = 3;
    Console.WriteLine(countStr(n));
}
}

// This code is contributed by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A O(1) PHP program to find
// number of strings that can
// be made under given constraints.
function countStr($n)
{
    return 1 + ($n * 2) + ($n *
              (($n * $n) - 1) / 2);
}

// Driver code
$n = 3;
echo countStr($n);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>
// A O(1) javascript program to
// find number of strings
// that can be made under
// given constraints.
    function countStr(n) {
        return 1 + (n * 2) + (n * ((n * n) - 1) / 2);
    }

    // Driver code

        var n = 3;
        document.write(countStr(n));

// This code is contributed by Princi Singh
</script>
```

**输出:**

```
19
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)
感谢 Niharika Sahai 提供上述解决方案。
**参考:**
[https://careercup.appspot.com/question?id=5717453712654336](https://careercup.appspot.com/question?id=5717453712654336)
本文由 [**尼尚辛格**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。