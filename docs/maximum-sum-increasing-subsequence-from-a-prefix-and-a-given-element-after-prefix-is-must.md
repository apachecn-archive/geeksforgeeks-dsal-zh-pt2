# 前缀和前缀后给定元素的最大和增加子序列是必须的

> 原文:[https://www . geeksforgeeks . org/最大和递增子序列从前缀和前缀后给定元素是必须的/](https://www.geeksforgeeks.org/maximum-sum-increasing-subsequence-from-a-prefix-and-a-given-element-after-prefix-is-must/)

给定一个 n 个正整数的数组，编写一个程序来寻找从前缀到第 I 个索引的递增子序列的最大和，并且还包括在 I 之后的给定的第 k 个元素，即 k > i。

**示例:**

> **输入:** arr[] = {1，101，2，3，100，4，5}第 I 个索引= 4(第 4 个索引处的元素为 100)第 K 个索引= 6(第 6 个索引处的元素为 5。)
> **输出:** 11
> **解释:**
> 所以我们需要计算子序列(1 101 2 3 100 5)的最大和，这样 5 必然包含在子序列中，所以答案是 11 乘子序列(1 2 3 5)。
> 
> **输入:** arr[] = {1，101，2，3，100，4，5}第 I 个索引= 2(第 2 个索引处的元素为 2)第 K 个索引= 5(第 5 个索引处的元素为 4。)
> **输出:** 7
> **解释:**
> 所以我们需要计算子序列(1 101 2 4)的最大和，这样 4 必然包含在子序列中，所以答案是 7 乘子序列(1 2 4)。

**先决条件:** [最大和增子序列](https://www.geeksforgeeks.org/dynamic-programming-set-14-maximum-sum-increasing-subsequence/)

**天真方法:**

1.  构造一个新的数组，该数组包含第 I 个索引和第 k 个元素。
2.  递归计算所有递增的子序列。
3.  丢弃所有不包含第 k 个元素的子序列。
4.  计算剩余子序列的最大和并显示出来。

***时间复杂度:** O(2 <sup>n</sup> )*

**更好的方法:**使用动态的方法维护一个表 dp[][]。dp[i][k]的值存储递增子序列的最大和，直到第 I 个索引并包含第 k 个元素。

## C++

```
// C++ program to find maximum sum increasing
// subsequence till i-th index and including
// k-th index.
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

ll pre_compute(ll a[], ll n, ll index, ll k)
{
    ll dp[n][n] = { 0 };

    // Initializing the first row of the dp[][].
    for (int i = 0; i < n; i++) {
        if (a[i] > a[0])
            dp[0][i] = a[i] + a[0];       
        else
            dp[0][i] = a[i];       
    }

    // Creating the dp[][] matrix.
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < n; j++) {
            if (a[j] > a[i] && j > i) {
                if (dp[i - 1][i] + a[j] > dp[i - 1][j])
                    dp[i][j] = dp[i - 1][i] + a[j];               
                else
                    dp[i][j] = dp[i - 1][j];
            }
            else
                dp[i][j] = dp[i - 1][j];           
        }
    }

    // To calculate for i=4 and k=6.
    return dp[index][k];
}

int main()
{
    ll a[] = { 1, 101, 2, 3, 100, 4, 5 };
    ll n = sizeof(a) / sizeof(a[0]);
    ll index = 4, k = 6;
    printf("%lld", pre_compute(a, n, index, k));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum sum increasing
// subsequence tiint i-th index and including
// k-th index.
class GFG {

    static int pre_compute(int a[], int n,
                             int index, int k)
    {
        int dp[][] = new int[n][n];

        // Initializing the first row of
        // the dp[][].
        for (int i = 0; i < n; i++) {
            if (a[i] > a[0])
                dp[0][i] = a[i] + a[0];
            else
                dp[0][i] = a[i];    
        }

        // Creating the dp[][] matrix.
        for (int i = 1; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                if (a[j] > a[i] && j > i)
                {
                    if (dp[i - 1][i] + a[j] >
                                 dp[i - 1][j])
                        dp[i][j] = dp[i - 1][i]
                                        + a[j];        
                    else
                        dp[i][j] = dp[i - 1][j];
                }
                else
                    dp[i][j] = dp[i - 1][j];        
            }
        }

        // To calculate for i=4 and k=6.
        return dp[index][k];
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 1, 101, 2, 3, 100, 4, 5 };
        int n = a.length;
        int index = 4, k = 6;
        System.out.println(
                  pre_compute(a, n, index, k));
    }
}

// This code is contributed by Smitha.
```

## 蟒蛇 3

```
# Python3 program to find maximum
# sum increasing subsequence till 
# i-th index and including k-th index.

def pre_compute(a, n, index, k):

    dp = [[0 for i in range(n)]
             for i in range(n)]

    # Initializing the first
    # row of the dp[][]
    for i in range(n):
        if a[i] > a[0]:
            dp[0][i] = a[i] + a[0]
        else:
            dp[0][i] = a[i]

    # Creating the dp[][] matrix.
    for i in range(1, n):
        for j in range(n):
            if a[j] > a[i] and j > i:
                if dp[i - 1][i] + a[j] > dp[i - 1][j]:
                    dp[i][j] = dp[i - 1][i] + a[j]
                else:
                    dp[i][j] = dp[i - 1][j]
            else:
                dp[i][j] = dp[i - 1][j]

    # To calculate for i=4 and k=6.
    return dp[index][k]

# Driver code
a = [1, 101, 2, 3, 100, 4, 5 ]
n = len(a)
index = 4
k = 6
print(pre_compute(a, n, index, k))

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program to find maximum
// sum increasing subsequence
// till i-th index and including
// k-th index.
using System;

class GFG
{
    static int pre_compute(int []a, int n,
                           int index, int k)
    {
    int [,]dp = new int[n, n];

    // Initializing the first
    // row of the dp[][].
    for (int i = 0; i < n; i++)
    {
        if (a[i] > a[0])
            dp[0, i] = a[i] + a[0];
        else
            dp[0, i] = a[i];
    }

    // Creating the dp[][] matrix.
    for (int i = 1; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (a[j] > a[i] && j > i)
            {
                if (dp[i - 1, i] + a[j] >
                            dp[i - 1, j])
                    dp[i, j] = dp[i - 1, i] +
                                        a[j];    
                else
                    dp[i, j] = dp[i - 1, j];
            }
            else
                dp[i, j] = dp[i - 1, j];        
        }
    }

    // To calculate for i=4 and k=6.
    return dp[index, k];
}

// Driver code
static public void Main ()
{
    int []a = {1, 101, 2,
               3, 100, 4, 5};
    int n = a.Length;
    int index = 4, k = 6;
    Console.WriteLine(pre_compute(a, n,
                                  index, k));
}
}

// This code is contributed by @ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum sum increasing
// subsequence till i-th index and including
// k-th index.

function pre_compute(&$a, $n, $index, $k)
{
    $dp = array_fill(0, $n,
          array_fill(0, $n, NULL));

    // Initializing the first row of the dp[][].
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] > $a[0])
            $dp[0][$i] = $a[$i] + $a[0];    
        else
            $dp[0][$i] = $a[$i];    
    }

    // Creating the dp[][] matrix.
    for ($i = 1; $i < $n; $i++)
    {
        for ($j = 0; $j < $n; $j++)
        {
            if ($a[$j] > $a[$i] && $j > $i)
            {
                if (($dp[$i - 1][$i] + $a[$j]) >
                                 $dp[$i - 1][$j])
                    $dp[$i][$j] = $dp[$i - 1][$i] +
                                           $a[$j];            
                else
                    $dp[$i][$j] = $dp[$i - 1][$j];
            }
            else
                $dp[$i][$j] = $dp[$i - 1][$j];        
        }
    }

    // To calculate for i=4 and k=6.
    return $dp[$index][$k];
}

// Driver Code
$a = array( 1, 101, 2, 3, 100, 4, 5 );
$n = sizeof($a);
$index = 4;
$k = 6;
echo pre_compute($a, $n, $index, $k);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum
// sum increasing subsequence tiint
// i-th index and including k-th index.
function pre_compute(a, n, index, k)
{
    let dp = new Array(n);
    for(let i = 0; i < n; i++)
    {
        dp[i] = new Array(n);
        for(let j = 0; j < n; j++)
        {
            dp[i][j] = 0;
        }
    }

    // Initializing the first row of
    // the dp[][].
    for(let i = 0; i < n; i++)
    {
        if (a[i] > a[0])
            dp[0][i] = a[i] + a[0];
        else
            dp[0][i] = a[i];   
    }

    // Creating the dp[][] matrix.
    for(let i = 1; i < n; i++)
    {
        for(let j = 0; j < n; j++)
        {
            if (a[j] > a[i] && j > i)
            {
                if (dp[i - 1][i] + a[j] >
                    dp[i - 1][j])
                    dp[i][j] = dp[i - 1][i] +
                                a[j];       
                else
                    dp[i][j] = dp[i - 1][j];
            }
            else
                dp[i][j] = dp[i - 1][j];       
        }
    }

    // To calculate for i=4 and k=6.
    return dp[index][k];
}

// Driver code
let a = [ 1, 101, 2, 3, 100, 4, 5 ];
let n = a.length;
let index = 4, k = 6;

document.write(pre_compute(a, n, index, k));

// This code is contributed by mukesh07

</script>
```

**Output**

```
11
```

***时间复杂度:**O(n<sup>2</sup>)*
***辅助空间:** O(n <sup>2</sup> )*

**有效方法:**这个问题基本上是求给定索引 I 下递增子序列的最大和，即子序列的所有元素都小于第 k 个(索引)元素或 arr[k]。因此，找到[最大和增加子序列](https://www.geeksforgeeks.org/maximum-sum-increasing-subsequence-dp-14/)。

> 例如:arr[] = {1，101，2，3，100，4，5}，index = 4；k = 6；
> 
> 现在，我们只需要找到从数组到索引 4 的最大和子序列，假设该子序列的所有元素都小于 arr[k],即 5。现在，遍历数组。
> 
> 对于 I = 0；作为 1 < 5; max increasing sub-sequence {1}, max = 1. 
> 对于 I = 1；as 101>5；跳过这个条目。最大递增子序列{1}，最大= 1。
> 对于 I = 2；as 2<5；最大递增子序列{1，2}，最大= 3。
> 为 I = 3；as 3<5；最大递增子序列{1，2，3}，最大= 6。
> 对于 I = 4；as 100>5；跳过这个条目。最大递增子序列{1，2，3}，最大= 6。
> as 指数= 4；因此到此为止，答案将是 max + a[k] = 6 + 5 = 11。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
#include <limits.h>
using namespace std;

// Function to find the
// maximum of two numbers
int max(int a, int b)
{
    if (a > b) {
        return a;
    }
    return b;
}

// Function to find the sum
int pre_compute(int a[], int n, int index, int k)
{
    // Base case
    if (index >= k) {
        return -1;
    }
    // Initialize the dp table
    int dp[index] = { 0 };

    int i;

    // Initialize the dp array with
    // corresponding array index value
    for (i = 0; i <= index; i++) {
        dp[i] = a[i];
    }

    int maxi = INT_MIN;

    for (i = 0; i <= index; i++) {
        // Only include values
        // which are less than a[k]
        if (a[i] >= a[k]) {
            continue;
        }

        for (int j = 0; j < i; j++) {
            // Check if a[i] is
            // greater than a[j]
            if (a[i] > a[j]) {
                dp[i] = dp[j] + a[i];
            }

            // Update maxi
            maxi = max(maxi, dp[i]);
        }
    }

    // Incase all the elements in
    // the array upto ith index
    // are greater or equal to a[k]
    if (maxi == INT_MIN) {
        return a[k];
    }
    return maxi + a[k];
    // Contributed by Mainak Dutta
}

// Driver code
int main()
{
    int a[] = { 1, 101, 2, 3, 100, 4, 5 };
    int n = sizeof(a) / sizeof(a[0]);
    int index = 4, k = 6;

    // Function call
    printf("%d", pre_compute(a, n, index, k));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the
// maximum of two numbers
static int max(int a, int b)
{
    if (a > b)
    {
        return a;
    }
    return b;
}

// Function to find the sum
static int pre_compute(int a[], int n,
                       int index, int k)
{

    // Base case
    if (index >= k)
    {
        return -1;
    }

    // Initialize the dp table
    int[] dp = new int[index + 1];

    int i;

    // Initialize the dp array with
    // corresponding array index value
    for(i = 0; i <= index; i++)
    {
        dp[i] = a[i];
    }

    int maxi = Integer.MIN_VALUE;

    for(i = 0; i <= index; i++)
    {

        // Only include values
        // which are less than a[k]
        if (a[i] >= a[k])
        {
            continue;
        }

        for(int j = 0; j < i; j++)
        {

            // Check if a[i] is
            // greater than a[j]
            if (a[i] > a[j])
            {
                dp[i] = dp[j] + a[i];
            }

            // Update maxi
            maxi = max(maxi, dp[i]);
        }
    }

    // Incase all the elements in
    // the array upto ith index
    // are greater or equal to a[k]
    if (maxi == Integer.MIN_VALUE)
    {
        return a[k];
    }
    return maxi + a[k];
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 1, 101, 2, 3, 100, 4, 5 };
    int n = a.length;
    int index = 4, k = 6;

    System.out.println(pre_compute(a, n, index, k));
}
}

// This code is contributed by rag2127
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the sum
def pre_compute(a, n, index, k):

    # Base case
    if (index >= k):
        return -1

    # Initialize the dp table
    dp = [0 for i in range(index)]

    # Initialize the dp array with
    # corresponding array index value
    for i in range(index):
        dp[i] = a[i]

    maxi = -float('inf')

    for i in range(index):

        # Only include values
        # which are less than a[k]
        if (a[i] >= a[k]):
            continue

        for j in range(i):

            # Check if a[i] is
            # greater than a[j]
            if (a[i] > a[j]):
                dp[i] = dp[j] + a[i]

            # Update maxi
            maxi = max(maxi, dp[i])

    # Incase all the elements in
    # the array upto ith index
    # are greater or equal to a[k]
    if (maxi == -float('inf')):
        return a[k]

    return maxi + a[k]

# Driver code
a = [ 1, 101, 2, 3, 100, 4, 5 ]
n = len(a)
index = 4
k = 6

# Function call
print(pre_compute(a, n, index, k))

# This code is contributed by rohitsingh07052
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the
// maximum of two numbers
static int max(int a, int b)
{
    if (a > b)
    {
        return a;
    }
    return b;
}

// Function to find the sum
static int pre_compute(int[] a, int n,
                       int index, int k)
{

    // Base case
    if (index >= k)
    {
        return -1;
    }

    // Initialize the dp table
    int[] dp = new int[index + 1];

    int i;

    // Initialize the dp array with
    // corresponding array index value
    for(i = 0; i <= index; i++)
    {
        dp[i] = a[i];
    }

    int maxi = Int32.MinValue;

    for(i = 0; i <= index; i++)
    {

        // Only include values
        // which are less than a[k]
        if (a[i] >= a[k])
        {
            continue;
        }

        for(int j = 0; j < i; j++)
        {

            // Check if a[i] is
            // greater than a[j]
            if (a[i] > a[j])
            {
                dp[i] = dp[j] + a[i];
            }

            // Update maxi
            maxi = Math.Max(maxi, dp[i]);
        }
    }

    // Incase all the elements in
    // the array upto ith index
    // are greater or equal to a[k]
    if (maxi == Int32.MinValue)
    {
        return a[k];
    }
    return maxi + a[k];
}

// Driver code
static public void Main()
{
    int[] a = { 1, 101, 2, 3, 100, 4, 5 };
    int n = a.Length;
    int index = 4, k = 6;

    Console.WriteLine(pre_compute(a, n, index, k));
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the
// maximum of two numbers
function max(a, b)
{
    if (a > b)
    {
        return a;
    }
    return b;
}

// Function to find the sum
function pre_compute(a, n, index, k)
{

    // Base case
    if (index >= k)
    {
        return -1;
    }

    // Initialize the dp table
    let dp = new Array(index + 1);
    dp.fill(0);

    let i;

    // Initialize the dp array with
    // corresponding array index value
    for(i = 0; i <= index; i++)
    {
        dp[i] = a[i];
    }

    let maxi = Number.MIN_VALUE;

    for(i = 0; i <= index; i++)
    {

        // Only include values
        // which are less than a[k]
        if (a[i] >= a[k])
        {
            continue;
        }

        for(let j = 0; j < i; j++)
        {

            // Check if a[i] is
            // greater than a[j]
            if (a[i] > a[j])
            {
                dp[i] = dp[j] + a[i];
            }

            // Update maxi
            maxi = Math.max(maxi, dp[i]);
        }
    }

    // Incase all the elements in
    // the array upto ith index
    // are greater or equal to a[k]
    if (maxi == Number.MIN_VALUE)
    {
        return a[k];
    }
    return maxi + a[k];
}

// Driver code
let a = [ 1, 101, 2, 3, 100, 4, 5 ];
let n = a.length;
let index = 4, k = 6;

document.write(pre_compute(a, n, index, k));

// This code is contributed by divyeshrabadiya07

</script>
```

**Output**

```
11
```

***时间复杂度:** O(指数 <sup>2</sup> )*
***辅助空间:** O(指数)*