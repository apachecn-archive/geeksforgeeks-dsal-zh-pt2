# 包含 K 个 1 的二进制串的子串计数

> 原文:[https://www . geesforgeks . org/count-substrings-binary-string-containing-k-one/](https://www.geeksforgeeks.org/count-substrings-binary-string-containing-k-ones/)

给定一个长度为 N 的二进制串和一个整数 K，我们需要找出这个串中有多少子串恰好包含 K 个子串。

**示例:**

```
Input : s = “10010”
        K = 1
Output : 9
The 9 substrings containing one 1 are,
“1”, “10”, “100”, “001”, “01”, “1”, 
“10”, “0010” and “010”
```

在这个问题中，我们需要找到恰好包含 K 个 1 的子串的计数，或者换句话说，这些子串中的数字的和是 K。我们首先创建一个前缀和数组，并在该数组上循环，当和值大于或等于 K 时停止。现在，如果当前索引处的和是(K + a)，那么我们知道子串和，从所有那些和是(a)的索引，直到当前索引将是 K，所以具有和(a)的索引的计数将被添加到结果中。下面用一个例子解释这个过程，

```
string s = “100101”
K = 2
prefix sum array = [1, 1, 1, 2, 2, 3]

So, at index 3,    we have prefix sum 2, 
Now total indices from where sum is 2, is 1
so result = 1

Substring considered = [“1001”]
At index 4,        we have prefix sum 2,
Now total indices from where sum is 2, is 
1 so result = 2

Substring considered = [“1001”, “10010”]
At index 5,     we have prefix sum 3,
Now total indices from where sum is 2, 
is 3 so result = 5
Substring considered = [“1001”, “10010”, 
“00101”, “0101”, “101”]
```

所以我们需要跟踪两件事，前缀和特定和的频率。在下面的代码中，不是存储完整的前缀和，而是仅使用一个变量和数组中存储的和的频率来存储当前索引处的前缀和。解的总时间复杂度为 0(N)。

## C++

```
// C++ program to find count of substring containing
// exactly K ones
#include <bits/stdc++.h>
using namespace std;

// method returns total number of substring having K ones
int countOfSubstringWithKOnes(string s, int K)
{
    int N = s.length();
    int res = 0;
    int countOfOne = 0;
    int freq[N + 1] = {0};

    // initialize index having zero sum as 1
    freq[0] = 1;

    // loop over binary characters of string
    for (int i = 0; i < N; i++) {

        // update countOfOne variable with value
        // of ith character
        countOfOne += (s[i] - '0');

        // if value reaches more than K, then
        // update result
        if (countOfOne >= K) {

            // add frequency of indices, having
            // sum (current sum - K), to the result
            res += freq[countOfOne - K];
        }

        // update frequency of one's count
        freq[countOfOne]++;
    }
    return res;
}

// Driver code to test above methods
int main()
{
    string s = "10010";
    int K = 1;
    cout << countOfSubstringWithKOnes(s, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of substring
// containing exactly K ones
import java.io.*;

public class GFG {

    // method returns total number of
    // substring having K ones
    static int countOfSubstringWithKOnes(
                            String s, int K)
    {
        int N = s.length();
        int res = 0;
        int countOfOne = 0;
        int []freq = new int[N+1];

        // initialize index having zero
        // sum as 1
        freq[0] = 1;

        // loop over binary characters
        // of string
        for (int i = 0; i < N; i++) {

            // update countOfOne variable
            // with value of ith character
            countOfOne += (s.charAt(i) - '0');

            // if value reaches more than
            // K, then update result
            if (countOfOne >= K) {

                // add frequency of indices,
                // having sum (current sum - K),
                // to the result
                res += freq[countOfOne - K];
            }

            // update frequency of one's count
            freq[countOfOne]++;
        }

        return res;
    }

    // Driver code to test above methods
    static public void main (String[] args)
    {
        String s = "10010";
        int K = 1;

        System.out.println(
            countOfSubstringWithKOnes(s, K));
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Python 3 program to find count of
# substring containing exactly K ones

# method returns total number of
# substring having K ones
def countOfSubstringWithKOnes(s, K):
    N = len(s)
    res = 0
    countOfOne = 0
    freq = [0 for i in range(N + 1)]

    # initialize index having
    # zero sum as 1
    freq[0] = 1

    # loop over binary characters of string
    for i in range(0, N, 1):

        # update countOfOne variable with
        # value of ith character
        countOfOne += ord(s[i]) - ord('0')

        # if value reaches more than K,
        # then update result
        if (countOfOne >= K):

            # add frequency of indices, having
            # sum (current sum - K), to the result
            res += freq[countOfOne - K]

        # update frequency of one's count
        freq[countOfOne] += 1

    return res

# Driver code
if __name__ == '__main__':
    s = "10010"
    K = 1
    print(countOfSubstringWithKOnes(s, K))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find count of substring
// containing exactly K ones
using System;

public class GFG {

    // method returns total number of
    // substring having K ones
    static int countOfSubstringWithKOnes(
                           string s, int K)
    {
        int N = s.Length;
        int res = 0;
        int countOfOne = 0;
        int []freq = new int[N+1];

        // initialize index having zero
        // sum as 1
        freq[0] = 1;

        // loop over binary characters
        // of string
        for (int i = 0; i < N; i++) {

            // update countOfOne variable
            // with value of ith character
            countOfOne += (s[i] - '0');

            // if value reaches more than
            // K, then update result
            if (countOfOne >= K) {

                // add frequency of indices,
                // having sum (current sum - K),
                // to the result
                res += freq[countOfOne - K];
            }

            // update frequency of one's count
            freq[countOfOne]++;
        }

        return res;
    }

    // Driver code to test above methods
    static public void Main ()
    {
        string s = "10010";
        int K = 1;

        Console.WriteLine(
            countOfSubstringWithKOnes(s, K));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find count
// of substring containing
// exactly K ones

// method returns total number
// of substring having K ones
function countOfSubstringWithKOnes($s, $K)
{
    $N = strlen($s);
    $res = 0;
    $countOfOne = 0;
    $freq = array();
    for ($i = 0; $i <= $N; $i++)
        $freq[$i] = 0;

    // initialize index
    // having zero sum as 1
    $freq[0] = 1;

    // loop over binary
    // characters of string
    for ($i = 0; $i < $N; $i++)
    {

        // update countOfOne
        // variable with value
        // of ith character
        $countOfOne += ($s[$i] - '0');

        // if value reaches more
        // than K, then update result
        if ($countOfOne >= $K)
        {

            // add frequency of indices,
            // having sum (current sum - K),
            // to the result
            $res = $res + $freq[$countOfOne - $K];
        }

        // update frequency
        // of one's count
        $freq[$countOfOne]++;
    }
    return $res;
}

// Driver code
$s = "10010";
$K = 1;
echo countOfSubstringWithKOnes($s, $K) ,"\n";

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// Javascript program to find count of
// substring containing exactly K ones

// Method returns total number of
// substring having K ones
function countOfSubstringWithKOnes(s, K)
{
    let N = s.length;
    let res = 0;
    let countOfOne = 0;
    let freq = new Array(N + 1);
    freq.fill(0);

    // Initialize index having zero
    // sum as 1
    freq[0] = 1;

    // Loop over binary characters
    // of string
    for(let i = 0; i < N; i++)
    {

        // Update countOfOne variable
        // with value of ith character
        countOfOne += (s[i] - '0');

        // If value reaches more than
        // K, then update result
        if (countOfOne >= K)
        {

            // Add frequency of indices,
            // having sum (current sum - K),
            // to the result
            res += freq[countOfOne - K];
        }

        // Update frequency of one's count
        freq[countOfOne]++;
    }
    return res;
}

// Driver code
let s = "10010";
let K = 1;

document.write(countOfSubstringWithKOnes(s, K));

// This code is contributed by suresh07 

</script>
```

**输出:**

```
9
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。