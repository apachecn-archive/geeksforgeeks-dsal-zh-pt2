# 最长的子序列，相邻元素至少有一个共同的数字

> 原文:[https://www . geeksforgeeks . org/最长子序列这样相邻元素至少有一个公共数字/](https://www.geeksforgeeks.org/longest-subsequence-such-that-adjacent-elements-have-at-least-one-common-digit/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找到最长子序列的长度，使得子序列的相邻元素至少有一个相同的数字。
**例:**

> **输入:** arr[] = {1，12，44，29，33，96，89}
> **输出:** 5
> 最长的子序列为{1 12 29 96 89}
> **输入:** arr[] = {12，23，45，43，36，97}
> **输出:** 4
> 最长的子序列为{ 12 23 44

**方法:**想法是为数组元素中出现的每个数字存储最长子序列的长度。

*   如果数字 d 是公共数字，dp[i][d]表示直到第 I 个元素的最长子序列的长度。

*   声明一个 cnt 数组，并为当前元素中的每个数字设置 cnt[d] = 1。

*   将每个数字 d 视为公共数字，并将结束于 arr[i]的最大长度子序列视为 DP[I][d]= max(DP[j][d]+1)(0 < = j < I)。

*   还要为当前元素找到一个局部最大值(dp[i][d])。

*   找到局部最大值后，将当前元素中所有数字的 dp[i][d]更新为局部最大值。

*   这是必需的，因为局部最大值代表具有数字 d 的元素的最大长度子序列。

> **例如**考虑 arr[] = {24，49，96}。
> 49 的本地最大值是 2，从数字 4 获得。
> 该局部最大值将用于查找具有公共数字 9 的 96 的局部最大值。
> 对于 49 位的所有数字都需要，dp[i][d]应设置为本地最大值。

以下是上述方法的实现:

## C++

```
// C++ program to find maximum length subsequence
// such that adjacent elements have at least
// one common digit
#include <bits/stdc++.h>
using namespace std;

// Returns length of maximum length subsequence
int findSubsequence(int arr[], int n)
{

    // To store the length of the
    // maximum length subsequence
    int len = 1;

    // To store current element arr[i]
    int tmp;

    int i, j, d;

    // To store the length of the sub-sequence
    // ending at index i and having common digit d
    int dp[n][10];

    memset(dp, 0, sizeof(dp));

    // To store digits present in current element
    int cnt[10];

    // To store length of maximum length subsequence
    // ending at index i
    int locMax;

    // For first element maximum length is 1 for
    // each digit
    tmp = arr[0];
    while (tmp > 0) {
        dp[0][tmp % 10] = 1;
        tmp /= 10;
    }

    // Find digits of each element, then find length
    // of subsequence for each digit and then find
    // local maximum
    for (i = 1; i < n; i++) {
        tmp = arr[i];
        locMax = 1;
        memset(cnt, 0, sizeof(cnt));

        // Find digits in current element
        while (tmp > 0) {
            cnt[tmp % 10] = 1;
            tmp /= 10;
        }

        // For each digit present find length of
        // subsequence and find local maximum
        for (d = 0; d <= 9; d++) {
            if (cnt[d]) {
                dp[i][d] = 1;
                for (j = 0; j < i; j++) {
                    dp[i][d] = max(dp[i][d], dp[j][d] + 1);
                    locMax = max(dp[i][d], locMax);
                }
            }
        }

        // Update value of dp[i][d] for each digit
        // present in current element to local maximum
        // found.
        for (d = 0; d <= 9; d++) {
            if (cnt[d]) {
                dp[i][d] = locMax;
            }
        }

        // Update maximum length with local maximum
        len = max(len, locMax);
    }

    return len;
}

// Driver code
int main()
{
    int arr[] = { 1, 12, 44, 29, 33, 96, 89 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findSubsequence(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum length subsequence
// such that adjacent elements have at least
// one common digit

class GFG
{

// Returns length of maximum length subsequence
static int findSubsequence(int arr[], int n)
{

    // To store the length of the
    // maximum length subsequence
    int len = 1;

    // To store current element arr[i]
    int tmp;

    int i, j, d;

    // To store the length of the sub-sequence
    // ending at index i and having common digit d
    int[][] dp = new int[n][10];

    // To store digits present in current element
    int[] cnt = new int[10];

    // To store length of maximum length subsequence
    // ending at index i
    int locMax;

    // For first element maximum length is 1 for
    // each digit
    tmp = arr[0];
    while (tmp > 0)
    {
        dp[0][tmp % 10] = 1;
        tmp /= 10;
    }

    // Find digits of each element, then find length
    // of subsequence for each digit and then find
    // local maximum
    for (i = 1; i < n; i++)
    {
        tmp = arr[i];
        locMax = 1;
        for (int x = 0; x < 10; x++)
        cnt[x]=0;

        // Find digits in current element
        while (tmp > 0)
        {
            cnt[tmp % 10] = 1;
            tmp /= 10;
        }

        // For each digit present find length of
        // subsequence and find local maximum
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] > 0)
            {
                dp[i][d] = 1;
                for (j = 0; j < i; j++)
                {
                    dp[i][d] = Math.max(dp[i][d], dp[j][d] + 1);
                    locMax = Math.max(dp[i][d], locMax);
                }
            }
        }

        // Update value of dp[i][d] for each digit
        // present in current element to local maximum
        // found.
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] > 0)
            {
                dp[i][d] = locMax;
            }
        }

        // Update maximum length with local maximum
        len = Math.max(len, locMax);
    }

    return len;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 12, 44, 29, 33, 96, 89 };
    int n = arr.length;

    System.out.println(findSubsequence(arr, n));
}
}

// This code is contributed by mits
```

## 蟒蛇 3

```
# Python3 program to find maximum
# Length subsequence such that
# adjacent elements have at least
# one common digit

# Returns Length of maximum
# Length subsequence
def findSubsequence(arr, n):

    # To store the Length of the
    # maximum Length subsequence
    Len = 1

    # To store current element arr[i]
    tmp = 0

    i, j, d = 0, 0, 0

    # To store the Length of the sub-sequence
    # ending at index i and having common digit d
    dp = [[0 for i in range(10)]
             for i in range(n)]

    # To store digits present in current element
    cnt = [0 for i in range(10)]

    # To store Length of maximum
    # Length subsequence ending at index i
    locMax = 0

    # For first element maximum
    # Length is 1 for each digit
    tmp = arr[0]
    while (tmp > 0):
        dp[0][tmp % 10] = 1
        tmp //= 10

    # Find digits of each element,
    # then find Length of subsequence
    # for each digit and then find
    # local maximum
    for i in range(1, n):
        tmp = arr[i]
        locMax = 1
        cnt = [0 for i in range(10)]

        # Find digits in current element
        while (tmp > 0):
            cnt[tmp % 10] = 1
            tmp //= 10

        # For each digit present find Length of
        # subsequence and find local maximum
        for d in range(10):
            if (cnt[d]):
                dp[i][d] = 1
                for j in range(i):
                    dp[i][d] = max(dp[i][d],
                                   dp[j][d] + 1)
                    locMax = max(dp[i][d], locMax)

        # Update value of dp[i][d] for each digit
        # present in current element to local
        # maximum found.
        for d in range(10):
            if (cnt[d]):
                dp[i][d] = locMax

        # Update maximum Length
        # with local maximum
        Len = max(Len, locMax)
    return Len

# Driver code
arr = [1, 12, 44, 29, 33, 96, 89]
n = len(arr)

print(findSubsequence(arr, n))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# program to find maximum length subsequence
// such that adjacent elements have at least
// one common digit
using System;

class GFG
{

// Returns length of maximum length subsequence
static int findSubsequence(int []arr, int n)
{

    // To store the length of the
    // maximum length subsequence
    int len = 1;

    // To store current element arr[i]
    int tmp;

    int i, j, d;

    // To store the length of the sub-sequence
    // ending at index i and having common digit d
    int[,] dp = new int[n, 10];

    // To store digits present in current element
    int[] cnt = new int[10];

    // To store length of maximum length subsequence
    // ending at index i
    int locMax;

    // For first element maximum length is 1 for
    // each digit
    tmp = arr[0];
    while (tmp > 0)
    {
        dp[0, tmp % 10] = 1;
        tmp /= 10;
    }

    // Find digits of each element, then find length
    // of subsequence for each digit and then find
    // local maximum
    for (i = 1; i < n; i++)
    {
        tmp = arr[i];
        locMax = 1;
        for (int x = 0; x < 10; x++)
            cnt[x] = 0;

        // Find digits in current element
        while (tmp > 0)
        {
            cnt[tmp % 10] = 1;
            tmp /= 10;
        }

        // For each digit present find length of
        // subsequence and find local maximum
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] > 0)
            {
                dp[i, d] = 1;
                for (j = 0; j < i; j++)
                {
                    dp[i, d] = Math.Max(dp[i, d], dp[j, d] + 1);
                    locMax = Math.Max(dp[i, d], locMax);
                }
            }
        }

        // Update value of dp[i,d] for each digit
        // present in current element to local maximum
        // found.
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] > 0)
            {
                dp[i, d] = locMax;
            }
        }

        // Update maximum length with local maximum
        len = Math.Max(len, locMax);
    }

    return len;
}

// Driver code
public static void Main()
{
    int []arr = { 1, 12, 44, 29, 33, 96, 89 };
    int n = arr.Length;

    Console.WriteLine(findSubsequence(arr, n));
}
}

// This code is contributed by mits
```

## java 描述语言

```
<script>
// Javascript program to find maximum length subsequence
// such that adjacent elements have at least
// one common digit

// Returns length of maximum length subsequence
function findSubsequence(arr,n)
{

    // To store the length of the
    // maximum length subsequence
    let len = 1;

    // To store current element arr[i]
    let tmp;

    let i, j, d;

    // To store the length of the sub-sequence
    // ending at index i and having common digit d
    let dp = new Array(n);
    for(let i = 0; i < n; i++)
    {
        dp[i] = new Array(10);
        for(let j = 0; j < 10; j++)
        {
            dp[i][j] = 0;
        }
    }

    // To store digits present in current element
    let cnt = new Array(10);

    // To store length of maximum length subsequence
    // ending at index i
    let locMax;

    // For first element maximum length is 1 for
    // each digit
    tmp = arr[0];
    while (tmp > 0)
    {
        dp[0][tmp % 10] = 1;
        tmp = Math.floor(tmp/10);
    }

    // Find digits of each element, then find length
    // of subsequence for each digit and then find
    // local maximum
    for (i = 1; i < n; i++)
    {
        tmp = arr[i];
        locMax = 1;
        for (let x = 0; x < 10; x++)
            cnt[x]=0;

        // Find digits in current element
        while (tmp > 0)
        {
            cnt[tmp % 10] = 1;
            tmp = Math.floor(tmp/10);
        }

        // For each digit present find length of
        // subsequence and find local maximum
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] > 0)
            {
                dp[i][d] = 1;
                for (j = 0; j < i; j++)
                {
                    dp[i][d] = Math.max(dp[i][d], dp[j][d] + 1);
                    locMax = Math.max(dp[i][d], locMax);
                }
            }
        }

        // Update value of dp[i][d] for each digit
        // present in current element to local maximum
        // found.
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] > 0)
            {
                dp[i][d] = locMax;
            }
        }

        // Update maximum length with local maximum
        len = Math.max(len, locMax);
    }

    return len;
}

// Driver code
let arr=[ 1, 12, 44, 29, 33, 96, 89];
let n = arr.length;
document.write(findSubsequence(arr, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
5
```

**时间复杂度:**O(n)<sup>2</sup>)
**辅助空间:** O(n)
以上解需要的辅助空间可以进一步减少。注意，对于 arr[i]中出现的每个数字 d，需要找到直到该数字的最大长度子序列，而不管子序列在哪个元素结束。这减少了 O(1)所需的辅助空间。对于每个 arr[i]，找到局部最大值，并将 arr[i]中每个数字 d 的摘要[d]更新为局部最大值。
以下是上述方法的实施:

## C++

```
// C++ program to find maximum length subsequence
// such that adjacent elements have at least
// one common digit
#include <bits/stdc++.h>
using namespace std;

// Returns length of maximum length subsequence
int findSubsequence(int arr[], int n)
{

    // To store length of maximum length subsequence
    int len = 1;

    // To store current element arr[i]
    int tmp;

    int i, j, d;

    // To store length of subsequence
    // having common digit d
    int dp[10];

    memset(dp, 0, sizeof(dp));

    // To store digits present in current element
    int cnt[10];

    // To store local maximum for current element
    int locMax;

    // For first element maximum length is 1 for
    // each digit
    tmp = arr[0];
    while (tmp > 0) {
        dp[tmp % 10] = 1;
        tmp /= 10;
    }

    // Find digits of each element, then find length
    // of subsequence for each digit and then find
    // local maximum
    for (i = 1; i < n; i++) {
        tmp = arr[i];
        locMax = 1;
        memset(cnt, 0, sizeof(cnt));

        // Find digits in current element
        while (tmp > 0) {
            cnt[tmp % 10] = 1;
            tmp /= 10;
        }

        // For each digit present find length of
        // subsequence and find local maximum
        for (d = 0; d <= 9; d++) {
            if (cnt[d]) {
                dp[d]++;
                locMax = max(locMax, dp[d]);
            }
        }

        // Update value of dp[d] for each digit
        // present in current element to local maximum
        // found
        for (d = 0; d <= 9; d++) {
            if (cnt[d]) {
                dp[d] = locMax;
            }
        }

        // Update maximum length with local maximum
        len = max(len, locMax);
    }

    return len;
}

// Driver code
int main()
{
    int arr[] = { 1, 12, 44, 29, 33, 96, 89 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findSubsequence(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum length subsequence
// such that adjacent elements have at least
// one common digit
import java.util.*;

class GFG
{

// Returns length of maximum length subsequence
static int findSubsequence(int arr[], int n)
{

    // To store length of maximum length subsequence
    int len = 1;

    // To store current element arr[i]
    int tmp;

    int i, j, d;

    // To store length of subsequence
    // having common digit d
    int dp[] = new int[10];

    // To store digits present in current element
    int cnt[] = new int[10];

    // To store local maximum for current element
    int locMax;

    // For first element maximum length is 1 for
    // each digit
    tmp = arr[0];
    while (tmp > 0)
    {
        dp[tmp % 10] = 1;
        tmp /= 10;
    }

    // Find digits of each element, then find length
    // of subsequence for each digit and then find
    // local maximum
    for (i = 1; i < n; i++)
    {
        tmp = arr[i];
        locMax = 1;
                Arrays.fill(cnt, 0);

        // Find digits in current element
        while (tmp > 0)
        {
            cnt[tmp % 10] = 1;
            tmp /= 10;
        }

        // For each digit present find length of
        // subsequence and find local maximum
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] == 1)
            {
                dp[d]++;
                locMax = Math.max(locMax, dp[d]);
            }
        }

        // Update value of dp[d] for each digit
        // present in current element to local maximum
        // found
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] == 1)
            {
                dp[d] = locMax;
            }
        }

        // Update maximum length with local maximum
        len = Math.max(len, locMax);
    }

    return len;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 12, 44, 29, 33, 96, 89 };
    int n = arr.length;
        System.out.print(findSubsequence(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 program to find maximum length
# subsequence such that adjacent elements
# have at least one common digit

# Returns length of maximum
# length subsequence
def findSubsequence(arr, n) :

    # To store length of maximum
    # length subsequence
    length = 1;

    # To store length of subsequence
    # having common digit d
    dp = [0] * 10;

    # For first element maximum length
    # is 1 for each digit
    tmp = arr[0];
    while (tmp > 0) :
        dp[tmp % 10] = 1;
        tmp //= 10;

    # Find digits of each element, then
    # find length of subsequence for each
    # digit and then find local maximum
    for i in range(1, n) :
        tmp = arr[i];
        locMax = 1;
        cnt = [0] * 10

        # Find digits in current element
        while (tmp > 0) :
            cnt[tmp % 10] = 1;
            tmp //= 10;

        # For each digit present find length of
        # subsequence and find local maximum
        for d in range(10) :
            if (cnt[d]) :
                dp[d] += 1;
                locMax = max(locMax, dp[d]);

        # Update value of dp[d] for each digit
        # present in current element to local
        # maximum found
        for d in range(10) :
            if (cnt[d]) :
                dp[d] = locMax;

        # Update maximum length with local
        # maximum
        length = max(length, locMax);

    return length;

# Driver code
if __name__ == "__main__" :
    arr = [ 1, 12, 44, 29, 33, 96, 89 ];
    n = len(arr)

    print(findSubsequence(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# program to find maximum length subsequence
// such that adjacent elements have at least
// one common digit
using System;

class GFG
{

// Returns length of maximum length subsequence
static int findSubsequence(int []arr, int n)
{

    // To store length of maximum length subsequence
    int len = 1;

    // To store current element arr[i]
    int tmp;

    int i, j, d;

    // To store length of subsequence
    // having common digit d
    int []dp = new int[10];

    // To store digits present in current element
    int []cnt = new int[10];

    // To store local maximum for current element
    int locMax;

    // For first element maximum length is 1 for
    // each digit
    tmp = arr[0];
    while (tmp > 0)
    {
        dp[tmp % 10] = 1;
        tmp /= 10;
    }

    // Find digits of each element, then find length
    // of subsequence for each digit and then find
    // local maximum
    for (i = 1; i < n; i++)
    {
        tmp = arr[i];
        locMax = 1;
        for(int k = 0; k < 10; k++)
        {
            cnt[k] = 0;
        }
        // Find digits in current element
        while (tmp > 0)
        {
            cnt[tmp % 10] = 1;
            tmp /= 10;
        }

        // For each digit present find length of
        // subsequence and find local maximum
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] == 1)
            {
                dp[d]++;
                locMax = Math.Max(locMax, dp[d]);
            }
        }

        // Update value of dp[d] for each digit
        // present in current element to local maximum
        // found
        for (d = 0; d <= 9; d++)
        {
            if (cnt[d] == 1)
            {
                dp[d] = locMax;
            }
        }

        // Update maximum length with local maximum
        len = Math.Max(len, locMax);
    }

    return len;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 12, 44, 29, 33, 96, 89 };
    int n = arr.Length;
        Console.WriteLine(findSubsequence(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum length subsequence
// such that adjacent elements have at least
// one common digit

// Returns length of maximum length subsequence
function findSubsequence($arr, $n)
{

    // To store length of maximum length
    // subsequence
    $len = 1;

    // To store length of subsequence
    // having common digit d
    $dp = array_fill(0, 10, NULL);

    // For first element maximum length is 1
    // for each digit
    $tmp = $arr[0];
    while ($tmp > 0)
    {
        $dp[$tmp % 10] = 1;
        $tmp = intval($tmp / 10);
    }

    // Find digits of each element, then
    // find length of subsequence for each
    // digit and then find local maximum
    for ($i = 1; $i < $n; $i++)
    {
        $tmp = $arr[$i];
        $locMax = 1;
        $cnt = array_fill(0, 10, NULL);

        // Find digits in current element
        while ($tmp > 0)
        {
            $cnt[$tmp % 10] = 1;
            $tmp = intval($tmp / 10);
        }

        // For each digit present find length of
        // subsequence and find local maximum
        for ($d = 0; $d <= 9; $d++)
        {
            if ($cnt[$d])
            {
                $dp[$d]++;
                $locMax = max($locMax, $dp[$d]);
            }
        }

        // Update value of dp[d] for each digit
        // present in current element to local
        // maximum found
        for ($d = 0; $d <= 9; $d++)
        {
            if ($cnt[$d])
            {
                $dp[$d] = $locMax;
            }
        }

        // Update maximum length with
        // local maximum
        $len = max($len, $locMax);
    }

    return $len;
}

// Driver code
$arr = array( 1, 12, 44, 29, 33, 96, 89 );
$n = sizeof($arr);
echo findSubsequence($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum length subsequence
// such that adjacent elements have at least
// one common digit

    // Returns length of maximum length subsequence
    function findSubsequence(arr , n) {

        // To store length of maximum length subsequence
        var len = 1;

        // To store current element arr[i]
        var tmp;

        var i, j, d;

        // To store length of subsequence
        // having common digit d
        var dp = Array(10).fill(0);

        // To store digits present in current element
        var cnt = Array(10).fill(0);

        // To store local maximum for current element
        var locMax;

        // For first element maximum length is 1 for
        // each digit
        tmp = arr[0];
        while (tmp > 0) {
            dp[tmp % 10] = 1;
            tmp = parseInt(tmp/10);
        }

        // Find digits of each element, then find length
        // of subsequence for each digit and then find
        // local maximum
        for (var i = 1; i < n; i++) {
            tmp = arr[i];
            locMax = 1;
            cnt.fill( 0);

            // Find digits in current element
            while (tmp > 0) {
                cnt[tmp % 10] = 1;
                tmp = parseInt(tmp/10);
            }

            // For each digit present find length of
            // subsequence and find local maximum
            for (d = 0; d <= 9; d++) {
                if (cnt[d] == 1) {
                    dp[d]++;
                    locMax = Math.max(locMax, dp[d]);
                }
            }

            // Update value of dp[d] for each digit
            // present in current element to local maximum
            // found
            for (d = 0; d <= 9; d++) {
                if (cnt[d] == 1) {
                    dp[d] = locMax;
                }
            }

            // Update maximum length with local maximum
            len = Math.max(len, locMax);
        }

        return len;
    }

    // Driver code

        var arr = [ 1, 12, 44, 29, 33, 96, 89 ];
        var n = arr.length;
        document.write(findSubsequence(arr, n));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
5
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)