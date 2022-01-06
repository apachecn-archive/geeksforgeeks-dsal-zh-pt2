# 找到一个排列，使得 gcd(p[i]，i) > 1 的指数的数量正好为 K

> 原文:[https://www . geeksforgeeks . org/find-a-arrangement-so-number-for-gcdpi-I-1-恰好是-k/](https://www.geeksforgeeks.org/find-a-permutation-such-that-number-of-indices-for-which-gcdpi-i-1-is-exactly-k/)

给定两个整数 **N** 和 **K** ，任务是从范围**【1，N】**中找到整数的排列，使得其中 **gcd(p[i]，i) > 1** 恰好是 **K** 的索引数(基于 1 的索引)。打印 **-1** 如果这样的排列是不可能的。

**示例:**

> **输入:** N = 4，K = 3
> **输出:** 1 2 3 4
> gcd(1，1) = 1
> gcd(2，2) = 2
> gcd(3，3) = 3
> gcd(4，4) = 4
> 因此，正好有 3 个指数 gcd(p[i]，i) > 1
> 
> **输入:** N = 1，K = 1
> **输出:** -1

**方法:**在这里可以观察到几个问题:

1.  gcd(i，i + 1) = 1
2.  gcd(1，i) = 1
3.  gcd(i，i) = i

因为 1 的 gcd 与任何其他数字总是 1，所以 **K** 几乎可以是**N–1**。考虑其中 **p[i] = i** 的排列，其中 **gcd(p[i]，i) > 1** 的指数数将为**N–1**。请注意，交换 2 个连续元素(不包括 1 个)将使这类索引的数量减少正好 2。用 1 交换将会减少正好 1 的计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the required permutation
void printPermutation(int n, int k)
{

    // Not possible
    if (k >= n || (n % 2 == 0 && k == 0)) {
        cout << -1;
        return;
    }
    int per[n + 1], i;

    // Initial permutation
    for (i = 1; i <= n; i++)
        per[i] = i;

    // Indices for which gcd(p[i], i) > 1
    // in the initial permutation
    int cnt = n - 1;
    i = 2;
    while (i < n) {

        // Reduce the count by 2
        if (cnt - 1 > k) {
            swap(per[i], per[i + 1]);
            cnt -= 2;
        }

        // Reduce the count by 1
        else if (cnt - 1 == k) {
            swap(per[1], per[i]);
            cnt--;
        }
        else
            break;
        i += 2;
    }

    // Print the permutation
    for (i = 1; i <= n; i++)
        cout << per[i] << " ";
}

// Driver code
int main()
{
    int n = 4, k = 3;
    printPermutation(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to print the required permutation
    static void printPermutation(int n, int k)
    {

        // Not possible
        if (k >= n || (n % 2 == 0 && k == 0))
        {
            System.out.print(-1);
            return;
        }
        int per[] = new int[n + 1], i;

        // Initial permutation
        for (i = 1; i <= n; i++)
        {
            per[i] = i;
        }

        // Indices for which gcd(p[i], i) > 1
        // in the initial permutation
        int cnt = n - 1;
        i = 2;
        while (i < n)
        {

            // Reduce the count by 2
            if (cnt - 1 > k)
            {
                swap(per, i, i + 1);
                cnt -= 2;
            }

            // Reduce the count by 1
            else if (cnt - 1 == k)
            {
                swap(per, 1, i);
                cnt--;
            }
            else
            {
                break;
            }
            i += 2;
        }

        // Print the permutation
        for (i = 1; i <= n; i++)
        {
            System.out.print(per[i] + " ");
        }
    }

    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4, k = 3;
        printPermutation(n, k);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the required permutation
def printPermutation(n, k):

    # Not possible
    if (k >= n or (n % 2 == 0 and
                   k == 0)):
        print(-1);
        return;
    per = [0] * (n + 1);

    # Initial permutation
    for i in range(1, n + 1):
        per[i] = i;

    # Indices for which gcd(p[i], i) > 1
    # in the initial permutation
    cnt = n - 1;
    i = 2;
    while (i < n):

        # Reduce the count by 2
        if (cnt - 1 > k):

            t = per[i];
            per[i] = per[i + 1];
            per[i + 1] = t;

            # swap(per[i], per[i + 1]);
            cnt -= 2;

        # Reduce the count by 1
        elif (cnt - 1 == k):

            # swap(per[1], per[i]);
            t = per[1];
            per[1] = per[i];
            per[i] = t;
            cnt -= 1;
        else:
            break;
        i += 2;

    # Print the permutation
    for i in range(1, n + 1):
        print(per[i], end = " ");

# Driver code
n = 4;
k = 3;
printPermutation(n, k);

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to print the required permutation
    static void printPermutation(int n, int k)
    {

        // Not possible
        if (k >= n || (n % 2 == 0 && k == 0))
        {
            Console.Write(-1);
            return;
        }
        int []per = new int[n + 1] ;
        int i ;

        // Initial permutation
        for (i = 1; i <= n; i++)
        {
            per[i] = i;
        }

        // Indices for which gcd(p[i], i) > 1
        // in the initial permutation
        int cnt = n - 1;
        i = 2;
        while (i < n)
        {

            // Reduce the count by 2
            if (cnt - 1 > k)
            {
                swap(per, i, i + 1);
                cnt -= 2;
            }

            // Reduce the count by 1
            else if (cnt - 1 == k)
            {
                swap(per, 1, i);
                cnt--;
            }
            else
            {
                break;
            }
            i += 2;
        }

        // Print the permutation
        for (i = 1; i <= n; i++)
        {
            Console.Write(per[i] + " ");
        }
    }

    static int[] swap(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Driver code
    public static void Main()
    {
        int n = 4, k = 3;
        printPermutation(n, k);
    }
}

/* This code contributed by Ryuga */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the required permutation
function printPermutation($n, $k)
{

    // Not possible
    if ($k >= $n || ($n % 2 == 0 &&
                     $k == 0))
    {
        echo -1;
        return;
    }
    $per[$n + 1] = array();
    $i;

    // Initial permutation
    for ($i = 1; $i <= $n; $i++)
        $per[$i] = $i;

    // Indices for which gcd(p[i], i) > 1
    // in the initial permutation
    $cnt = $n - 1;
    $i = 2;
    while ($i < $n)
    {

        // Reduce the count by 2
        if ($cnt - 1 > $k)
        {

            list($per[$i],
                 $per[$i + 1]) = array($per[$i + 1],
                                       $per[$i]);
            //swap(per[i], per[i + 1]);
            $cnt -= 2;
        }

        // Reduce the count by 1
        else if ($cnt - 1 == $k)
        {

            // swap(per[1], per[i]);
            list($per[1],
                 $per[$i]) = array($per[$i],
                                   $per[1]);
            $cnt--;
        }
        else
            break;
        $i += 2;
    }

    // Print the permutation
    for ($i = 1; $i <= $n; $i++)
        echo $per[$i], " ";
}

// Driver code
$n = 4;
$k = 3;
printPermutation($n, $k);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to print the required permutation
    function printPermutation(n, k)
    {

        // Not possible
        if (k >= n || (n % 2 == 0 && k == 0))
        {
            document.write(-1);
            return;
        }
        let per = new Array(n + 1);
        per.fill(0);
        let i ;

        // Initial permutation
        for (i = 1; i <= n; i++)
        {
            per[i] = i;
        }

        // Indices for which gcd(p[i], i) > 1
        // in the initial permutation
        let cnt = n - 1;
        i = 2;
        while (i < n)
        {

            // Reduce the count by 2
            if (cnt - 1 > k)
            {
                swap(per, i, i + 1);
                cnt -= 2;
            }

            // Reduce the count by 1
            else if (cnt - 1 == k)
            {
                swap(per, 1, i);
                cnt--;
            }
            else
            {
                break;
            }
            i += 2;
        }

        // Print the permutation
        for (i = 1; i <= n; i++)
        {
            document.write(per[i] + " ");
        }
    }

    function swap(arr, i, j)
    {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    let n = 4, k = 3;
      printPermutation(n, k);

</script>
```

**Output:** 

```
1 2 3 4
```

**时间复杂度:** O(N)