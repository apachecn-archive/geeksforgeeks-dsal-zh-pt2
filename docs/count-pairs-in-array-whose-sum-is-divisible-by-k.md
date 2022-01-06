# 计数数组中总和可被 K 整除的对

> 原文:[https://www . geesforgeks . org/count-pairs-in-array-其和可被 k 整除/](https://www.geeksforgeeks.org/count-pairs-in-array-whose-sum-is-divisible-by-k/)

给定一个数组 **A[]** 和正整数 **K** ，任务是计算数组中总和可被 **K** 整除的对的总数。
**注:**这个问题是[这个](https://www.geeksforgeeks.org/count-pairs-array-whose-sum-divisible-4/)的一般化版本

**示例:**

```
Input : A[] = {2, 2, 1, 7, 5, 3}, K = 4
Output : 5
Explanation : 
There are five pairs possible whose sum
is divisible by '4' i.e., (2, 2), 
(1, 7), (7, 5), (1, 3) and (5, 3)

Input : A[] = {5, 9, 36, 74, 52, 31, 42}, K = 3
Output : 7
```

**天真方法**:最简单的方法是遍历数组中的每一对，但使用两个嵌套的 for 循环，并计算那些和可被“K”整除的对。这种方法的时间复杂度为 0(N<sup>2</sup>)。

**有效方法**:一种有效的方法是使用哈希技术。我们将根据元素的值(mod K)将元素分成桶。当一个数除以 K 时，余数可以是 0，1，2，直到(k-1)。所以拿一个数组来说大小为 K 的 **freq[]** (用 Zero 初始化)并增加 freq[A[i]%K]的值，这样我们就可以计算出用 K 除余数 j 的值的个数

## C++

```
// C++ Program to count pairs
// whose sum divisible by 'K'
#include <bits/stdc++.h>
using namespace std;

// Program to count pairs whose sum divisible
// by 'K'
int countKdivPairs(int A[], int n, int K)
{
    // Create a frequency array to count
    // occurrences of all remainders when
    // divided by K
    int freq[K] = { 0 };

    // Count occurrences of all remainders
    for (int i = 0; i < n; i++)
        ++freq[A[i] % K];

    // If both pairs are divisible by 'K'
    int sum = freq[0] * (freq[0] - 1) / 2;

    // count for all i and (k-i)
    // freq pairs
    for (int i = 1; i <= K / 2 && i != (K - i); i++)
        sum += freq[i] * freq[K - i];
    // If K is even
    if (K % 2 == 0)
        sum += (freq[K / 2] * (freq[K / 2] - 1) / 2);
    return sum;
}

// Driver code
int main()
{

    int A[] = { 2, 2, 1, 7, 5, 3 };
    int n = sizeof(A) / sizeof(A[0]);
    int K = 4;
    cout << countKdivPairs(A, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs
// whose sum divisible by 'K'
import java.util.*;

class Count {
    public static int countKdivPairs(int A[], int n, int K)
    {
        // Create a frequency array to count
        // occurrences of all remainders when
        // divided by K
        int freq[] = new int[K];

        // Count occurrences of all remainders
        for (int i = 0; i < n; i++)
            ++freq[A[i] % K];

        // If both pairs are divisible by 'K'
        int sum = freq[0] * (freq[0] - 1) / 2;

        // count for all i and (k-i)
        // freq pairs
        for (int i = 1; i <= K / 2 && i != (K - i); i++)
            sum += freq[i] * freq[K - i];
        // If K is even
        if (K % 2 == 0)
            sum += (freq[K / 2] * (freq[K / 2] - 1) / 2);
        return sum;
    }
    public static void main(String[] args)
    {
        int A[] = { 2, 2, 1, 7, 5, 3 };
        int n = 6;
        int K = 4;
        System.out.print(countKdivPairs(A, n, K));
    }
}
```

## 蟒蛇 3

```
# Python3 code to count pairs whose
# sum is divisible by 'K'

# Function to count pairs whose
# sum is divisible by 'K'
def countKdivPairs(A, n, K):

    # Create a frequency array to count
    # occurrences of all remainders when
    # divided by K
    freq = [0] * K

    # Count occurrences of all remainders
    for i in range(n):
        freq[A[i] % K]+= 1

    # If both pairs are divisible by 'K'
    sum = freq[0] * (freq[0] - 1) / 2;

    # count for all i and (k-i)
    # freq pairs
    i = 1
    while(i <= K//2 and i != (K - i) ):
        sum += freq[i] * freq[K-i]
        i+= 1

    # If K is even
    if( K % 2 == 0 ):
        sum += (freq[K//2] * (freq[K//2]-1)/2);

    return int(sum)

# Driver code
A = [2, 2, 1, 7, 5, 3]
n = len(A)
K = 4
print(countKdivPairs(A, n, K))
```

## C#

```
// C# program to count pairs
// whose sum divisible by 'K'
using System;

class Count
{
    public static int countKdivPairs(int []A, int n, int K)
    {
        // Create a frequency array to count
        // occurrences of all remainders when
        // divided by K
        int []freq = new int[K];

        // Count occurrences of all remainders
        for (int i = 0; i < n; i++)
            ++freq[A[i] % K];

        // If both pairs are divisible by 'K'
        int sum = freq[0] * (freq[0] - 1) / 2;

        // count for all i and (k-i)
        // freq pairs
        for (int i = 1; i <= K / 2 && i != (K - i); i++)
            sum += freq[i] * freq[K - i];

        // If K is even
        if (K % 2 == 0)
            sum += (freq[K / 2] * (freq[K / 2] - 1) / 2);
        return sum;
    }

    // Driver code
    static public void Main ()
    {
        int []A = { 2, 2, 1, 7, 5, 3 };
        int n = 6;
        int K = 4;
        Console.WriteLine(countKdivPairs(A, n, K));
    }
}

// This code is contributed by akt_mit.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to count pairs
// whose sum divisible by 'K'

// Program to count pairs whose sum
// divisible by 'K'
function countKdivPairs($A, $n, $K)
{

    // Create a frequency array to count
    // occurrences of all remainders when
    // divided by K
    $freq = array_fill(0, $K, 0);

    // Count occurrences of all remainders
    for ($i = 0; $i < $n; $i++)
        ++$freq[$A[$i] % $K];

    // If both pairs are divisible by 'K'
    $sum = (int)($freq[0] * ($freq[0] - 1) / 2);

    // count for all i and (k-i)
    // freq pairs
    for ($i = 1; $i <= $K / 2 &&
                 $i != ($K - $i); $i++)
        $sum += $freq[$i] * $freq[$K - $i];

    // If K is even
    if ($K % 2 == 0)
        $sum += (int)($freq[(int)($K / 2)] *
                     ($freq[(int)($K / 2)] - 1) / 2);
    return $sum;
}

// Driver code
$A = array( 2, 2, 1, 7, 5, 3 );
$n = count($A);
$K = 4;
echo countKdivPairs($A, $n, $K);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript program to count pairs whose sum divisible by 'K'

    function countKdivPairs(A, n, K)
    {
        // Create a frequency array to count
        // occurrences of all remainders when
        // divided by K
        let freq = new Array(K);
        freq.fill(0);

        // Count occurrences of all remainders
        for (let i = 0; i < n; i++)
            ++freq[A[i] % K];

        // If both pairs are divisible by 'K'
        let sum = freq[0] * parseInt((freq[0] - 1) / 2, 10);

        // count for all i and (k-i)
        // freq pairs
        for (let i = 1; i <= K / 2 && i != (K - i); i++)
            sum += freq[i] * freq[K - i];

        // If K is even
        if (K % 2 == 0)
            sum += parseInt(freq[parseInt(K / 2, 10)] * (freq[parseInt(K / 2, 10)] - 1) / 2, 10);
        return sum;
    }

    let A = [ 2, 2, 1, 7, 5, 3 ];
    let n = 6;
    let K = 4;
    document.write(countKdivPairs(A, n, K));

</script>
```

**输出:**

```
 5
```

**时间复杂度:**O(N)
T3】辅助空间: O(K)

https://www.youtube.com/watch?v=5UJvXcSUyT0&list=PLM68oyaqFM7Q-sv3gA5xbzfgVkoQ0xDrW&index=16