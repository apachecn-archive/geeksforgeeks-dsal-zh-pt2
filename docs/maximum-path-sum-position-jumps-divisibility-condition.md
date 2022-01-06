# 在可除条件下每个位置跳跃的最大路径和

> 原文:[https://www . geesforgeks . org/max-path-sum-position-jumps-divisioning-condition/](https://www.geeksforgeeks.org/maximum-path-sum-position-jumps-divisibility-condition/)

给定一组 **n 个**正整数。最初我们处于第一位置。如果 x 除 y 和 x < y，我们可以从位置 x (1 < = x < = n)跳到位置 y (1 < = y < = n)。任务是打印在每个位置 x 结束的最大和路径。
注意:由于第一个元素在位置 1，我们可以从这里跳到任何位置，因为 1 除了所有其他位置号。
**示例:**

```
Input :  arr[] = {2, 3, 1, 4, 6, 5}
Output : 2 5 3 9 8 10
Explanation:
Maximum sum path ending with position 1 is 2.
For position 1, last position to visit is 1 only.
So maximum sum for position 1 = 2.

Maximum sum path ending with position 2 is 5.
For position 2, path can be jump from position 1 
to 2 as 1 divides 2.
So maximum sum for position 2 = 2 + 3 = 5.

For position 3, path can be jump from position 1 
to 3 as 1 divides 3.
So maximum sum for position 3 = 2 + 1 = 3.

For position 4, path can be jump from position 1
to 2 and 2 to 4.
So maximum sum for position 4 = 2 + 3 + 4 = 9.

For position 5, path can be jump from position 1 
to 5.
So maximum sum for position 5 = 2 + 6 = 8.

For position 6, path can be jump from position 
1 to 2 and 2 to 6 or 1 to 3 and 3 to 6.
But path 1 -> 2 -> 6 gives maximum sum for
position 6 = 2 + 3 + 5 = 10.
```

**进场:**

想法是用动态规划来解决这个问题。

```
Create an 1-D array dp[] where each element dp[i] 
stores maximum sum path ending at index i (or 
position x where x = i+1) with divisible jumps.

The recurrence relation for dp[i] can be defined as:

dp[i] = max(dp[i], dp[divisor of i+1] + arr[i]) 

To find all the divisor of i+1, move from 1 
divisor to sqrt(i+1).
```

下面是该方法的实现:

## C++

```
// C++ program to print maximum
// path sum ending with
// each position x such that all
// path step positions
// divide x.
#include <bits/stdc++.h>
using namespace std;

void printMaxSum(int arr[], int n)
{

    // Create an array such that dp[i]
    // stores maximum
    // path sum ending with i.
    int dp[n];
    memset(dp, 0, sizeof dp);

    // Calculating maximum sum path
    // for each element.
    for (int i = 0; i < n; i++) {
        dp[i] = arr[i];

        // Finding previous step for arr[i]
        // Moving from 1 to sqrt(i+1) since all the
        // divisors are present from sqrt(i+1).
        int maxi = 0;
        for (int j = 1; j <= sqrt(i + 1); j++) {
            // Checking if j is divisor of i+1.
            if (((i + 1) % j == 0) && (i + 1) != j) {
                // Checking which divisor will provide
                // greater value.
                if (dp[j - 1] > maxi)
                    maxi = dp[j - 1];
                if (dp[(i + 1) / j - 1] > maxi && j != 1)
                    maxi = dp[(i + 1) / j - 1];
            }
        }

        dp[i] += maxi;
    }

    // Printing the answer (Maximum path sum ending
    // with every position i+1.
    for (int i = 0; i < n; i++)
        cout << dp[i] << " ";
}

// Driven Program
int main()
{
    int arr[] = { 2, 3, 1, 4, 6, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printMaxSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print maximum path
// sum ending with each position x such
// that all path step positions divide x.
import java.util.*;

class GFG {

    static void printMaxSum(int arr[], int n)
    {
        // Create an array such that dp[i]
        // stores maximum path sum ending with i.
        int dp[] = new int[n];
        Arrays.fill(dp, 0);

        // Calculating maximum sum
        // path for each element.
        for (int i = 0; i < n; i++) {
            dp[i] = arr[i];

            // Finding previous step for arr[i]
            // Moving from 1 to sqrt(i+1) since all the
            // divisors are present from sqrt(i+1).
            int maxi = 0;
            for (int j = 1; j <= Math.sqrt(i + 1); j++) {

                // Checking if j is divisor of i+1.
                if (((i + 1) % j == 0) && (i + 1) != j) {

                    // Checking which divisor will
                    // provide greater value.
                    if (dp[j - 1] > maxi)
                        maxi = dp[j - 1];
                    if (dp[(i + 1) / j - 1] > maxi && j != 1)
                        maxi = dp[(i + 1) / j - 1];
                }
            }

            dp[i] += maxi;
        }

        // Printing the answer (Maximum path sum
        // ending with every position i+1.)
        for (int i = 0; i < n; i++)
            System.out.print(dp[i] + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 1, 4, 6, 5 };
        int n = arr.length;

        // Function calling
        printMaxSum(arr, n);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to print maximum
# path sum ending with each position
# x such that all path step positions
# divide x.

def printMaxSum(arr, n):

    # Create an array such that dp[i]
    # stores maximum path sum ending with i.
    dp = [0 for i in range(n)]

    # Calculating maximum sum path
    # for each element.
    for i in range(n):
        dp[i] = arr[i]

        # Finding previous step for arr[i]
        # Moving from 1 to sqrt(i + 1) since all the
        # divisiors are present from sqrt(i + 1).
        maxi = 0
        for j in range(1, int((i + 1) ** 0.5) + 1):

            # Checking if j is divisior of i + 1.
            if ((i + 1) % j == 0 and (i + 1) != j):

                # Checking which divisor will provide
                # greater value.
                if (dp[j - 1] > maxi):
                    maxi = dp[j - 1]
                if (dp[(i + 1) // j - 1] > maxi and j != 1):
                    maxi = dp[(i + 1) // j - 1]

        dp[i] += maxi

    # Printing the answer
    # (Maximum path sum ending
    # with every position i + 1).
    for i in range(n):
        print(dp[i], end = ' ')

# Driver Program
arr = [2, 3, 1, 4, 6, 5]
n = len(arr)
printMaxSum(arr, n)

# This code is contributed by Soumen Ghosh.
```

## C#

```
// C# program to print maximum path
// sum ending with each position x such
// that all path step positions divide x.
using System;

class GFG {

    static void printMaxSum(int[] arr, int n)
    {
        // Create an array such that dp[i]
        // stores maximum path sum ending with i.
        int[] dp = new int[n];

        // Calculating maximum sum
        // path for each element.
        for (int i = 0; i < n; i++) {
            dp[i] = arr[i];

            // Finding previous step for arr[i]
            // Moving from 1 to sqrt(i+1) since all the
            // divisors are present from sqrt(i+1).
            int maxi = 0;
            for (int j = 1; j <= Math.Sqrt(i + 1); j++)
            {
                // Checking if j is divisor of i+1.
                if (((i + 1) % j == 0) && (i + 1) != j)
                {
                    // Checking which divisor will
                    // provide greater value.
                    if (dp[j - 1] > maxi)
                        maxi = dp[j - 1];
                    if (dp[(i + 1) / j - 1] > maxi && j != 1)
                        maxi = dp[(i + 1) / j - 1];
                }
            }

            dp[i] += maxi;
        }

        // Printing the answer (Maximum path sum ending
        // with every position i+1.)
        for (int i = 0; i < n; i++)
            Console.Write(dp[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 3, 1, 4, 6, 5 };
        int n = arr.Length;

        // Function calling
        printMaxSum(arr, n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print maximum path sum ending with
// each position x such that all path step positions
// divide x.

function printMaxSum($arr, $n)
{
    // Create an array such that dp[i] stores maximum
    // path sum ending with i.
    $dp = array() ;

    // Calculating maximum sum path for each element.
    for ($i = 0; $i < $n; $i++) {
        $dp[$i] = $arr[$i];

        // Finding previous step for arr[i]
        // Moving from 1 to sqrt(i+1) since all the
        // divisors are present from sqrt(i+1).
        $maxi = 0;
        for ($j = 1; $j <= sqrt($i + 1); $j++) {
            // Checking if j is divisor of i+1.
            if ((($i + 1) % $j == 0) && ($i + 1) != $j) {
                // Checking which divisor will provide
                // greater value.
                if ($dp[$j - 1] > $maxi)
                    $maxi = $dp[$j - 1];
                if ($dp[($i + 1) / $j - 1] > $maxi && $j != 1)
                    $maxi = $dp[($i + 1) / $j - 1];
            }
        }

        $dp[$i] += $maxi;
    }

    // Printing the answer (Maximum path sum ending
    // with every position i+1.
    for ($i = 0; $i < $n; $i++)
        echo $dp[$i] , " " ;
}

// Driven Program
$arr = array(2, 3, 1, 4, 6, 5 );
$n = sizeof($arr);

printMaxSum($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript program to print maximum path
    // sum ending with each position x such
    // that all path step positions divide x.

    function printMaxSum(arr, n)
    {
        // Create an array such that dp[i]
        // stores maximum path sum ending with i.
        let dp = new Array(n);
        dp.fill(0);

        // Calculating maximum sum
        // path for each element.
        for (let i = 0; i < n; i++) {
            dp[i] = arr[i];

            // Finding previous step for arr[i]
            // Moving from 1 to sqrt(i+1) since all the
            // divisors are present from sqrt(i+1).
            let maxi = 0;
            for (let j = 1; j <= Math.sqrt(i + 1); j++)
            {
                // Checking if j is divisor of i+1.
                if (((i + 1) % j == 0) && (i + 1) != j)
                {
                    // Checking which divisor will
                    // provide greater value.
                    if (dp[j - 1] > maxi)
                        maxi = dp[j - 1];
                    if (dp[parseInt((i + 1) / j, 10) - 1] > maxi && j != 1)
                        maxi = dp[parseInt((i + 1) / j, 10) - 1];
                }
            }

            dp[i] += maxi;
        }

        // Printing the answer (Maximum path sum ending
        // with every position i+1.)
        for (let i = 0; i < n; i++)
            document.write(dp[i] + " ");
    }

    let arr = [ 2, 3, 1, 4, 6, 5 ];
    let n = arr.length;

    // Function calling
    printMaxSum(arr, n);

</script>
```

**输出:**

```
2 5 3 9 8 10
```

**时间复杂度:** O(n*sqrt(n))。
本文由 [**Anuj Chauhan**](https://web.facebook.com/anuj0503) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。