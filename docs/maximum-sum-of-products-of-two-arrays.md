# 两个数组乘积的最大和

> 原文:[https://www . geeksforgeeks . org/两个阵列的最大乘积和/](https://www.geeksforgeeks.org/maximum-sum-of-products-of-two-arrays/)

给定两个大小相同的正整数数组 A 和 B，任务是找出它们元素乘积的最大和。A 中的每个元素必须与 B 中的恰好一个元素相乘，反之亦然，这样两个数组中的每个元素恰好出现一次，所得乘积之和最大。
**例** :

> **输入** : A[] = {1，2，3}
> B[] = {4，5，1}
> **输出** : 24
> **说明**:乘积的最大和为 5*3+4*2+1*1 = 24。
> **输入** : A[] = {5，1，3，4，2}
> B[] = {8，10，9，7，6}
> **输出** : 130
> **解释**:积的最大和是 10*5+9*4+8*3+7*2+6*1 = 130。

这个想法是观察两个最大数的乘积将对乘积的最大和有贡献。所以想法是:

1.  对两个数组进行排序。
2.  遍历数组，并计算位于同一索引处的数组元素的乘积之和。

以下是上述方法的实现:

## C++

```
// CPP program to calculate maximum sum
// of products of two arrays
#include<bits/stdc++.h>
using namespace std;

    // Function that calculates maximum sum
    // of products of two arrays
    int maximumSOP(int *a, int *b)
    {
        // Variable to store the sum of
        // products of array elements
        int sop = 0;

        // length of the arrays
        int n = sizeof(a)/sizeof(a[0]);

        // Sorting both the arrays
        sort(a,a+n+1);
        sort(b,b+n+1);

        // Traversing both the arrays
        // and calculating sum of product
        for (int i = 0; i <=n; i++) {
            sop += a[i] * b[i];
        }

        return sop;
    }

    // Driver code
    int main()
    {
        int A[] = { 1, 2, 3 };
        int B[] = { 4, 5, 1 };

        cout<<maximumSOP(A, B);
        return 0;
    }

// This code is contributed by mits
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate maximum sum
// of products of two arrays

import java.io.*;
import java.util.*;
public class GFG {

    // Function that calculates maximum sum
    // of products of two arrays
    static int maximumSOP(int[] a, int[] b)
    {
        // Variable to store the sum of
        // products of array elements
        int sop = 0;

        // length of the arrays
        int n = a.length;

        // Sorting both the arrays
        Arrays.sort(a);
        Arrays.sort(b);

        // Traversing both the arrays
        // and calculating sum of product
        for (int i = 0; i < n; i++) {
            sop += a[i] * b[i];
        }

        return sop;
    }

    // Driver code
    public static void main(String args[])
    {
        int[] A = { 1, 2, 3 };
        int[] B = { 4, 5, 1 };

        System.out.println(maximumSOP(A, B));
    }
}
```

## 蟒蛇 3

```
# Python program to calculate
# maximum sum of products of
# two arrays

# Function that calculates
# maximum sum of products
# of two arrays
def maximumSOP(a, b) :

    # Variable to store the sum of
    # products of array elements
    sop = 0

    # length of the arrays
    n = len(a)

    # Sorting both the arrays
    a.sort()
    b.sort()

    # Traversing both the arrays
    # and calculating sum of product
    for i in range(n) :
        sop += a[i] * b[i]

    return sop

# Driver code    
if __name__ == "__main__" :

    A = [1, 2, 3]
    B = [4, 5, 1]

    print(maximumSOP(A, B))

# This code is contributed by ANKITRAI1
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-3">C#</gfg-tab><gfg-panel role="tabpanel" slot="panel" id="gfg-panel-3" data-code-lang="CSHARP"></gfg-panel>

```
 // C# program to calculate maximum sum
// of products of two arrays
using System;

class GFG 
{

// Function that calculates maximum 
// sum of products of two arrays
static int maximumSOP(int[] a, int[] b)
{
    // Variable to store the sum of
    // products of array elements
    int sop = 0;

    // length of the arrays
    int n = a.Length;

    // Sorting both the arrays
    Array.Sort(a);
    Array.Sort(b);

    // Traversing both the arrays
    // and calculating sum of product
    for (int i = 0; i < n; i++) 
    {
        sop += a[i] * b[i];
    }

    return sop;
}

// Driver code
public static void Main()
{
    int[] A = { 1, 2, 3 };
    int[] B = { 4, 5, 1 };

    Console.Write(maximumSOP(A, B));
}
}

// This code is contributed 
// by ChitraNayal 
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate maximum 
// sum of products of two arrays

// Function that calculates maximum
// sum of products of two arrays
function maximumSOP(&$a, &$b)
{
    $sop = 0;

    // Sorting both the arrays
    sort($a);
    sort($b);

    // length of the arrays
    $n = sizeof($a);

    // Traversing both the arrays
    // and calculating sum of product
    for ($i = 0; $i < $n; $i++)
    {
        $sop = $sop + ($a[$i] * $b[$i]);
    }

    return $sop;
}

// Driver code
$A = array(1, 2, 3 );
$B = array(4, 5, 1 );
echo maximumSOP($A, $B);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate maximum sum
// of products of two arrays 

    // Function that calculates maximum sum
    // of products of two arrays
    function maximumSOP(a, b)
    {
        // Variable to store the sum of
        // products of array elements
        let sop = 0;

        // length of the arrays
        let n = a.length;

        // Sorting both the arrays
        a.sort();
        b.sort();

        // Traversing both the arrays
        // and calculating sum of product
        for (let i = 0; i <n; i++) {
            sop += (a[i] * b[i]);
        }

        return sop;
    }

    // Driver code
        let A = [ 1, 2, 3 ];
        let B = [ 4, 5, 1 ];

        document.write(maximumSOP(A, B));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
24
```