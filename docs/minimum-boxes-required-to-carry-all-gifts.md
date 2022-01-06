# 携带所有礼物所需的最小箱子数

> 原文:[https://www . geesforgeks . org/最小盒数-要求携带所有礼物/](https://www.geeksforgeeks.org/minimum-boxes-required-to-carry-all-gifts/)

给定一个包含**礼物重量**的数组，以及一个代表**一个盒子**所能包含的最大重量的整数 K(所有盒子都是一样的)。每个盒子最多同时携带 2 个**礼物，前提是这些礼物的重量总和最多是盒子的极限。任务是找到携带所有礼物所需的**最小数量**的箱子。
注意:保证每件礼物可以一箱携带。**

**示例:**

> 输入:A = [3，2，2，1]，K = 3
> 输出:3
> 说明:3 个带砝码的盒子(1，2)、(2)、(3)
> 
> 输入:A = [3，5，3，4]，K = 5
> 输出:4
> 说明:4 个带砝码的盒子(3)、(3)、(4)、(5)

**做法:**如果最重的礼物可以和最轻的礼物共用一个盒子，那就这样做。否则，最重的礼物不能与任何人配对，所以它会得到一个单独的盒子。

这样做的原因是，如果最轻的礼物可以和任何人配对，那么它也可以和最重的礼物配对。
让**A【I】**成为目前**最轻的礼物**，让**A【j】**成为**最重的**。

然后，如果**最重的礼物**可以**与**最轻的礼物**共享**一个盒子(如果 **A[j] + A[i] < = K** )那么这样做，否则最重的礼物得到一个单独的盒子。

**以下是上述方法的实施:**

## C++

```
// CPP implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return number of boxes
int numBoxes(int A[], int n, int K)
{
    // Sort the boxes in ascending order
    sort(A, A + n);

    // Try to fit smallest box with
    // current heaviest box (from right
    // side)
    int i = 0, j = n - 1;
    int ans = 0;
    while (i <= j) {
        ans++;
        if (A[i] + A[j] <= K)
            i++;
        j--;
    }

    return ans;
}

// Driver program
int main()
{
    int A[] = { 3, 2, 2, 1 }, K = 3;
    int n = sizeof(A) / sizeof(A[0]);
    cout << numBoxes(A, n, K);
    return 0;
}

// This code is written by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.*;

class solution
{

// Function to return number of boxes
static int numBoxes(int A[], int n, int K)
{
    // Sort the boxes in ascending order
    Arrays.sort(A);

    // Try to fit smallest box with
    // current heaviest box (from right
    // side)
    int i = 0, j = n - 1;
    int ans = 0;
    while (i <= j) {
        ans++;
        if (A[i] + A[j] <= K)
            i++;
        j--;
    }

    return ans;
}

// Driver program
public static void main(String args[])
{
    int A[] = { 3, 2, 2, 1 }, K = 3;
    int n = A.length;
    System.out.println(numBoxes(A, n, K));

}
}

//THis code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# Function to return number of boxes
def numBoxex(A,n,K):

    # Sort the boxes in ascending order
    A.sort()
    # Try to fit smallest box with current
    # heaviest box (from right side)
    i =0
    j = n-1
    ans=0
    while i<=j:
        ans +=1
        if A[i]+A[j] <=K:
            i+=1
        j-=1

    return ans

# Driver code
if __name__=='__main__':
    A = [3, 2, 2, 1]
    K= 3
    n = len(A)
    print(numBoxex(A,n,K))

# This code is contributed by
# Shrikant13
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

// Function to return number of boxes
static int numBoxes(int []A, int n, int K)
{
    // Sort the boxes in ascending order
    Array.Sort(A);

    // Try to fit smallest box with
    // current heaviest box (from right
    // side)
    int i = 0, j = (n - 1);
    int ans = 0;
    while (i <= j)
    {
        ans++;
        if (A[i] + A[j] <= K)
            i++;
        j--;
    }

    return ans;
}

// Driver Code
static public void Main ()
{
    int []A = { 3, 2, 2, 1 };
    int K = 3;
    int n = A.Length;
    Console.WriteLine(numBoxes(A, n, K));
}
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP  implementation of above approach
// Function to return number of boxes
function  numBoxes($A, $n, $K)
{
    // Sort the boxes in ascending order
    sort($A);

    // Try to fit smallest box with
    // current heaviest box (from right
    // side)
    $i = 0;
    $j = $n - 1;
    $ans = 0;
    while ($i <= $j) {
        $ans++;
        if ($A[$i] + $A[$j] <= $K)
            $i++;
        $j--;
    }

    return $ans;
}

// Driver program
    $A = array (3, 2, 2, 1 );
    $K = 3;
    $n = sizeof($A) / sizeof($A[0]);
    echo  numBoxes($A, $n, $K);

// This code is written by ajit
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to return number of boxes
function numBoxes(A, n, K)
{

    // Sort the boxes in ascending order
    A.sort(function(a, b){return a - b});

    // Try to fit smallest box with
    // current heaviest box (from right
    // side)
    let i = 0, j = (n - 1);
    let ans = 0;

    while (i <= j)
    {
        ans++;

        if (A[i] + A[j] <= K)
            i++;
        j--;
    }
    return ans;
}

// Driver code
let A = [ 3, 2, 2, 1 ];
let K = 3;
let n = A.length;

document.write(numBoxes(A, n, K));

// This code is contributed by suresh07

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(N*log(N))，其中 N 为数组长度。