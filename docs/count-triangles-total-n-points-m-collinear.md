# 共 n 个点共 m 条直线的三角形数量

> 原文:[https://www . geesforgeks . org/count-triangles-total-n-points-m-共线/](https://www.geeksforgeeks.org/count-triangles-total-n-points-m-collinear/)

平面上有 n 个点，其中 m 个点是共线的。求以点为顶点形成的三角形的个数？
**例:**

```
Input :  n = 5, m = 4
Output : 6
Out of five points, four points are 
collinear, we can make 6 triangles. We
can choose any 2 points from 4 collinear
points and use the single point as 3rd
point. So total count is 4C2 = 6

Input :  n = 10, m = 4
Output : 116
```

> 三角形数量=**<sup>n</sup>C<sub>3</sub>–<sup>m</sup>C<sub>3</sub>**
> **这个公式是如何工作的？**
> 考虑上面的第二个例子。共有 10 个点，其中 4 个共线。这十个点中的任何三个点将构成一个三角形。因此，形成一个三角形相当于选择 10 个点中的任何三个。在 <sup>n</sup> C <sub>3</sub> 方式的 10 个点中可以选择三个点。
> 三点不共线时 10 个点形成的三角形数=<sup>10</sup>C<sub>3</sub>……(I)
> 同样，三点不共线时 4 个点形成的三角形数=<sup>4</sup>C<sub>3</sub>………..(ii)
> 由于这 4 个点形成的三角形无效，所需形成的三角形数=<sup>10</sup>C<sub>3</sub>–<sup>4</sup>C<sub>3</sub>= 120–4 = 116

## C++

```
// CPP program to count number of triangles
// with n total points, out of which m are
// collinear.
#include <bits/stdc++.h>
using namespace std;

// Returns value of binomial coefficient
// Code taken from https://goo.gl/vhy4jp
int nCk(int n, int k)
{
    int C[k+1];
    memset(C, 0, sizeof(C));

    C[0] = 1;  // nC0 is 1

    for (int i = 1; i <= n; i++)
    {
        // Compute next row of pascal triangle
        // using the previous row
        for (int j = min(i, k); j > 0; j--)
            C[j] = C[j] + C[j-1];
    }
    return C[k];
}

/* function to calculate number of triangle
   can be formed */
int counTriangles(int n,int m)
{
    return (nCk(n, 3) - nCk(m, 3));
}

/* driver function*/
int main()
{
    int n = 5, m = 4;
    cout << counTriangles(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program to count number of triangles
// with n total points, out of which m are
// collinear.
import java.io.*;
import java.util.*;

class GFG {

// Returns value of binomial coefficient
// Code taken from https://goo.gl/vhy4jp
static int nCk(int n, int k)
{
    int[] C=new int[k+1];
    for (int i=0;i<=k;i++)
    C[i]=0;

    C[0] = 1; // nC0 is 1

    for (int i = 1; i <= n; i++)
    {
        // Compute next row of pascal triangle
        // using the previous row
        for (int j = Math.min(i, k); j > 0; j--)
            C[j] = C[j] + C[j-1];
    }
    return C[k];
}

/* function to calculate number of triangle
can be formed */
static int counTriangles(int n,int m)
{
    return (nCk(n, 3) - nCk(m, 3));
}

    public static void main (String[] args) {
      int n = 5, m = 4;
      System.out.println(counTriangles(n, m));

    }
}

//This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# python program to count number of triangles
# with n total points, out of which m are
# collinear.
import math

# Returns value of binomial coefficient
# Code taken from https://goo.gl / vhy4jp
def nCk(n, k):
    C = [0 for i in range(0, k + 2)]

    C[0] = 1; # nC0 is 1
    for i in range(0, n + 1):

        # Compute next row of pascal triangle
        # using the previous row
        for j in range(min(i, k), 0, -1):
            C[j] = C[j] + C[j-1]

    return C[k]

# function to calculate number of triangle
# can be formed
def counTriangles(n, m):
    return (nCk(n, 3) - nCk(m, 3))

# driver code
n = 5
m = 4
print (counTriangles(n, m))

# This code is contributed by Gitanjali
```

## C#

```
//C# program to count number of triangles
// with n total points, out of which m are
// collinear.
using System;

class GFG {

    // Returns value of binomial coefficient
    // Code taken from https://goo.gl/vhy4jp
    static int nCk(int n, int k)
    {
        int[] C=new int[k+1];
        for (int i = 0; i <= k; i++)
        C[i] = 0;

        // nC0 is 1
        C[0] = 1;

        for (int i = 1; i <= n; i++)
        {
            // Compute next row of pascal triangle
            // using the previous row
            for (int j = Math.Min(i, k); j > 0; j--)
                C[j] = C[j] + C[j - 1];
        }
        return C[k];
    }

    /* function to calculate number of triangle
    can be formed */
    static int counTriangles(int n,int m)
    {
        return (nCk(n, 3) - nCk(m, 3));
    }

    // Driver code
    public static void Main ()
    {
        int n = 5, m = 4;
        Console.WriteLine(counTriangles(n, m));

    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number
// of triangles with n total
// points, out of which m are collinear.

// Returns value of binomial coefficient
// Code taken from https://goo.gl/vhy4jp
function nCk($n, $k)
{
    for ($i = 0; $i <= $k; $i++)
    $C[$i] = 0;

    $C[0] = 1; // nC0 is 1

    for ($i = 1; $i <= $n; $i++)
    {
        // Compute next row of pascal
        // triangle using the previous row
        for ($j = min($i, $k); $j > 0; $j--)
            $C[$j] = $C[$j] + $C[$j - 1];
    }
    return $C[$k];
}

/* function to calculate number
of triangles that can be formed */
function counTriangles($n, $m)
{
    return (nCk($n, 3) - nCk($m, 3));
}

// Driver Code
$n = 5;
$m = 4;
echo counTriangles($n, $m);
return 0;

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>
    // Javascript program to count number of triangles
    // with n total points, out of which m are
    // collinear.

    // Returns value of binomial coefficient
    // Code taken from https://goo.gl/vhy4jp
    function nCk(n, k)
    {
        let C = new Array(k+1);
        C.fill(0);

        C[0] = 1;  // nC0 is 1

        for (let i = 1; i <= n; i++)
        {
            // Compute next row of pascal triangle
            // using the previous row
            for (let j = Math.min(i, k); j > 0; j--)
                C[j] = C[j] + C[j-1];
        }
        return C[k];
    }

    /* function to calculate number of triangle
       can be formed */
    function counTriangles(n, m)
    {
        return (nCk(n, 3) - nCk(m, 3));
    }

    let n = 5, m = 4;
    document.write(counTriangles(n, m));

    // This code is contributed by divyesh072019.
</script>
```

**输出:**

```
6
```