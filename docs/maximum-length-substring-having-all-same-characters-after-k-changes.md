# k 个变化后所有字符相同的最大长度子串

> 原文:[https://www . geeksforgeeks . org/最大长度-子字符串-k-changes 后具有所有相同的字符/](https://www.geeksforgeeks.org/maximum-length-substring-having-all-same-characters-after-k-changes/)

我们有一个长度为 n 的字符串，它只包含大写和小写字符，我们有一个数字 k(总是小于 n 且大于 0)。我们最多可以对字符串进行 k 次修改，这样我们就可以得到一个最大长度的子字符串，它包含所有相同的字符。
**例:**

```
n = length of string
k = changes you can make
Input : n = 5 k = 2
        str = ABABA
Output : maximum length = 5
which will be (AAAAA)

Input : n = 6 k = 4
       str = HHHHHH
Output : maximum length=6
which will be(HHHHHH) 
```

我们逐一检查英语字母表中的每个字符(大写和小写)。我们基本上是在寻找每个字符能够形成的子串的最大长度，无论哪个字符将形成最大长度的子串，那么这个长度将是我们的答案。

1.  我们检查子字符串的最大长度，它可以由一组 52 个字符(从“A”到“Z”和从“A”到“Z”)中的每个字符组成。
2.  为此，我们遍历整个字符串，每当我们发现一个不同的字符，我们就增加计数。
3.  如果计数变得大于 k(在右索引处)，我们再次从第 0 个索引开始，如果我们发现不同的字符，我们将减少计数。
4.  当计数等于 k 时(在左索引处)，那么此时长度将是右索引-左索引+1。
5.  我们重复这个过程，直到到达字符串的末尾，然后返回最大长度。
6.  我们对所有字符都这样做，最后返回最大长度。

## C++

```
// C++ program to find maximum length equal
// character string with k changes
#include <iostream>
using namespace std;

// function to find the maximum length of
// substring having character ch
int findLen(string& A, int n, int k, char ch)
{
    int maxlen = 1;
    int cnt = 0;
    int l = 0, r = 0;

    // traverse the whole string
    while (r < n) {

        /* if character is not same as ch
           increase count */
        if (A[r] != ch)
            ++cnt;

        /* While  count > k  traverse the string
           again until count becomes less than k
           and decrease the count when characters
           are not same */
        while (cnt > k) {
            if (A[l] != ch)
                --cnt;
            ++l;
        }

        /* length of substring will be rightIndex -
           leftIndex + 1\. Compare this with the maximum
           length and return maximum length */
        maxlen = max(maxlen, r - l + 1);
        ++r;
    }
    return maxlen;
}

// function which returns maximum length of substring
int answer(string& A, int n, int k)
{
    int maxlen = 1;
    for (int i = 0; i < 26; ++i) {
        maxlen = max(maxlen, findLen(A, n, k, i+'A'));
        maxlen = max(maxlen, findLen(A, n, k, i+'a'));
    }
    return maxlen;
}

// Driver code
int main()
{
    int n = 5, k = 2;
    string A = "ABABA";
    cout << "Maximum length = " << answer(A, n, k) << endl;

    n = 6, k = 4;
    string B = "HHHHHH";
    cout << "Maximum length = " << answer(B, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum length equal
// character string with k changes

public class GFG
{
    // method to find the maximum length of
    // substring having character ch
    static int findLen(String A, int n, int k, char ch)
    {
        int maxlen = 1;
        int cnt = 0;
        int l = 0, r = 0;

        // traverse the whole string
        while (r < n) {

            /* if character is not same as ch
               increase count */
            if (A.charAt(r) != ch)
                ++cnt;

            /* While  count > k  traverse the string
               again until count becomes less than k
               and decrease the count when characters
               are not same */
            while (cnt > k) {
                if (A.charAt(l) != ch)
                    --cnt;
                ++l;
            }

            /* length of substring will be rightIndex -
               leftIndex + 1\. Compare this with the maximum
               length and return maximum length */
            maxlen = Math.max(maxlen, r - l + 1);
            ++r;
        }
        return maxlen;
    }

    // method which returns maximum length of substring
    static int answer(String A, int n, int k)
    {
        int maxlen = 1;
        for (int i = 0; i < 26; ++i) {
            maxlen = Math.max(maxlen, findLen(A, n, k, (char) (i+'A')));
            maxlen = Math.max(maxlen, findLen(A, n, k, (char) (i+'a')));
        }
        return maxlen;
    }

    // Driver Method
    public static void main(String[] args)
    {
        int n = 5, k = 2;
        String A = "ABABA";
        System.out.println("Maximum length = " + answer(A, n, k));

        n = 6; k = 4;
        String B = "HHHHHH";
        System.out.println("Maximum length = " + answer(B, n, k));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find maximum length
# equal character string with k changes

# function to find the maximum length of
# substring having character ch
def findLen(A, n, k, ch):
    maxlen = 1
    cnt = 0
    l = 0
    r = 0

    # traverse the whole string
    while r < n:

        # if character is not same as ch
        # increase count
        if A[r] != ch:
            cnt += 1

        # While count > k traverse the string
        # again until count becomes less than k
        # and decrease the count when characters
        # are not same
        while cnt > k:
            if A[l] != ch:
                cnt -= 1
            l += 1

        # length of substring will be rightIndex -
        # leftIndex + 1\. Compare this with the
        # maximum length and return maximum length
        maxlen = max(maxlen, r - l + 1)
        r += 1

    return maxlen

# function which returns
# maximum length of substring
def answer(A, n, k):
    maxlen = 1
    for i in range(26):
        maxlen = max(maxlen, findLen(A, n, k,
                             chr(i + ord('A'))))
        maxlen = max(maxlen, findLen(A, n, k,
                             chr(i + ord('a'))))

    return maxlen

# Driver Code
if __name__ == "__main__":
    n = 5
    k = 2
    A = "ABABA"
    print("Maximum length =",
             answer(A, n, k))

    n = 6
    k = 4
    B = "HHHHHH"
    print("Maximum length =",
             answer(B, n, k))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find maximum length equal
// character string with k changes
using System;

class GFG
{

    // method to find the maximum length of
    // substring having character ch
    public static int findLen(string A, int n,
                               int k, char ch)
    {
        int maxlen = 1;
        int cnt = 0;
        int l = 0, r = 0;

        // traverse the whole string
        while (r < n)
        {

            // if character is
            // not same as ch
            // increase count
            if (A[r] != ch)
            {
                ++cnt;
            }

            // While count > k traverse
            // the string again until
            // count becomes less than
            // k and decrease the
            // count when characters
            // are not same
            while (cnt > k)
            {
                if (A[l] != ch)
                {
                    --cnt;
                }
                ++l;
            }

            // length of substring
            // will be rightIndex -
            // leftIndex + 1.
            // Compare this with the maximum
            // length and return maximum length
            maxlen = Math.Max(maxlen, r - l + 1);
            ++r;
        }
        return maxlen;
    }

    // method which returns
    // maximum length of substring
    public static int answer(string A, int n, int k)
    {
        int maxlen = 1;
        for (int i = 0; i < 26; ++i)
        {
            maxlen = Math.Max(maxlen,
              findLen(A, n, k, (char)(i + 'A')));

            maxlen = Math.Max(maxlen,
              findLen(A, n, k, (char)(i + 'a')));
        }
        return maxlen;
    }

// Driver Method
public static void Main(string[] args)
{
    int n = 5, k = 2;
    string A = "ABABA";
    Console.WriteLine("Maximum length = "
                      + answer(A, n, k));

    n = 6;
    k = 4;
    string B = "HHHHHH";
    Console.WriteLine("Maximum length = "
                      + answer(B, n, k));
}
}

// This code is contributed by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum length equal
// character string with k changes

// function to find the maximum length
// of substring having character ch
function findLen($A, $n, $k, $ch)
{
    $maxlen = 1; $cnt = 0;
    $l = 0; $r = 0;

    // traverse the whole string
    while ($r < $n)
    {

        /* if character is not same as
        ch increase count */
        if ($A[$r] != $ch)
            ++$cnt;

        /* While count > k traverse the string
        again until count becomes less than k
        and decrease the count when characters
        are not same */
        while ($cnt > $k)
        {
            if ($A[$l] != $ch)
                --$cnt;
            ++$l;
        }

        /* length of substring will be rightIndex -
        leftIndex + 1\. Compare this with the maximum
        length and return maximum length */
        $maxlen = max($maxlen, $r - $l + 1);
        ++$r;
    }
    return $maxlen;
}

// function which returns maximum
// length of substring
function answer($A, $n, $k)
{
    $maxlen = 1;
    for ($i = 0; $i < 26; ++$i)
    {
        $maxlen = max($maxlen,
                      findLen($A, $n, $k, $i + 'A'));
        $maxlen = max($maxlen,
                      findLen($A, $n, $k, $i + 'a'));
    }
    return $maxlen;
}

// Driver code
$n = 5; $k = 2; $A = "ABABA";
echo "Maximum length = " . answer($A, $n, $k) . "\n";

$n = 6; $k = 4; $B = "HHHHHH";
echo "Maximum length = " . answer($B, $n, $k) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to find maximum length equal
// character string with k changes

    // method to find the maximum length of
    // substring having character ch
    function findLen(A,n,k,ch)
    {
        let maxlen = 1;
        let cnt = 0;
        let l = 0, r = 0;

        // traverse the whole string
        while (r < n) {

            /* if character is not same as ch
               increase count */
            if (A[r] != ch)
                ++cnt;

            /* While  count > k  traverse the string
               again until count becomes less than k
               and decrease the count when characters
               are not same */
            while (cnt > k) {
                if (A[l] != ch)
                    --cnt;
                ++l;
            }

            /* length of substring will be rightIndex -
               leftIndex + 1\. Compare this with the maximum
               length and return maximum length */
            maxlen = Math.max(maxlen, r - l + 1);
            ++r;
        }
        return maxlen;
    }

    // method which returns maximum length of substring
    function answer(A,n,k)
    {
        let maxlen = 1;
        for (let i = 0; i < 26; ++i) {
            maxlen = Math.max(maxlen, findLen(A, n, k, String.fromCharCode(i+'A'.charCodeAt(0))));
            maxlen = Math.max(maxlen, findLen(A, n, k, String.fromCharCode (i+'a'.charCodeAt(0))));
        }
        return maxlen;
    }

    // Driver Method
    let  n = 5, k = 2;
    let A = "ABABA";
    document.write("Maximum length = " + answer(A, n, k)+"<br>");

    n = 6; k = 4;
    let B = "HHHHHH";
    document.write("Maximum length = " + answer(B, n, k));

    //This code is contributed by rag2127

</script>
```

**输出:**

```
Maximum length = 5
Maximum length = 6
```

本文由**尼泰什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。