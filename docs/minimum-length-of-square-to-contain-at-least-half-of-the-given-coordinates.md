# 包含至少一半给定坐标的最小正方形长度

> 原文:[https://www . geesforgeks . org/最小平方长度至少包含给定坐标的一半/](https://www.geeksforgeeks.org/minimum-length-of-square-to-contain-at-least-half-of-the-given-coordinates/)

给定二维平面上的一组 N 个点。任务是找到 M 的最小值，使得以原点为中心、边长为 2*M 的正方形至少包含其内部或上面的地板(N/2)点。

**示例:**

> **输入:** N = 4
> 点为:{(1，2)、(-3，4)、(1，78)、(-3，-7)}
> **输出:** 4
> 端点为(4，4)、(-4，-4)、(4，-4)、(-4，4)的正方形将包含点(1，2)和(-3，4)。
> M 的最小可能值为 4，使得正方形至少有 2 个点。
> **输入:** N = 3
> 点为:{(1，2)，(-3，4)，(1，78)}
> **输出:** 2
> 正方形包含点(1，2)。{楼层(3/2) = 1}

**接近**:

1.  任何点(x，y)的一个主要观察点，该点所在的最小值 M 是最大值(abs(x)，abs(y))。
2.  用第一点。我们可以找到所有点的 M 的最小值，并将它们存储在一个数组中。
3.  对数组排序。
4.  现在，数组[i]表示最小值 M，这样，如果在边 2*M 的平方中需要 I 个点(因为下面的所有点，M 的最小值小于或等于 I)。
5.  打印数组[floor(n/2)]的值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to Calculate Absolute Value
int mod(int x)
{
    if (x >= 0)
        return x;
    return -x;
}

// Function to Calculate the Minimum value of M
void findSquare(int n)
{
    int points[n][2] = { { 1, 2 }, { -3, 4 },
                       { 1, 78 }, { -3, -7 } };
    int a[n];

    // To store the minimum M for each
    // point in array
    for (int i = 0; i < n; i++) {
        int x, y;
        x = points[i][0];
        y = points[i][1];
        a[i] = max(mod(x), mod(y));
    }

    // Sort the array
    sort(a, a + n);

    // Index at which atleast required point are
    // inside square of length 2*M
    int index = floor(n / 2) - 1;
    cout << "Minimum M required is: " << a[index] << endl;
}

// Driver Code
int main()
{
    int N;
    N = 4;
    findSquare(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

// Java program to find next identical year
class GFG
{

// Function to Calculate Absolute Value
static int mod(int x)
{
    if (x >= 0)
        return x;
    return -x;
}

// Function to Calculate the Minimum value of M
static void findSquare(int n)
{
    int points[][] = { { 1, 2 }, { -3, 4 },
                    { 1, 78 }, { -3, -7 } };
    int []a = new int[n];

    // To store the minimum M for each
    // point in array
    for (int i = 0; i < n; i++)
    {
        int x, y;
        x = points[i][0];
        y = points[i][1];
        a[i] = Math.max(mod(x), mod(y));
    }

    // Sort the array
    Arrays.sort(a);

    // Index at which atleast required point are
    // inside square of length 2*M
    int index = (int) (Math.floor(n / 2) - 1);
    System.out.println("Minimum M required is: " + a[index]);
}

// Driver Code
public static void main(String[] args)
{
    int N;
    N = 4;
    findSquare(N);
}
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to Calculate the
# Minimum value of M
def findSquare(n):

    points = [[1, 2], [-3, 4],
              [1, 78], [-3, -7]]
    a = [None] * n

    # To store the minimum M
    # for each point in array
    for i in range(0, n):
        x = points[i][0]
        y = points[i][1]
        a[i] = max(abs(x), abs(y))

    # Sort the array
    a.sort()

    # Index at which atleast required
    # point are inside square of length 2*M
    index = n // 2 - 1
    print("Minimum M required is:", a[index])

# Driver Code
if __name__ == "__main__":

    N = 4
    findSquare(N)

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to find next identical year
using System;

class GFG
{

// Function to Calculate Absolute Value
static int mod(int x)
{
    if (x >= 0)
        return x;
    return -x;
}

// Function to Calculate the Minimum value of M
static void findSquare(int n)
{
    int [,]points = new int[4,2]{ { 1, 2 }, { -3, 4 },
                    { 1, 78 }, { -3, -7 } };
    int []a = new int[n];

    // To store the minimum M for each
    // point in array
    for (int i = 0; i < n; i++)
    {
        int x, y;
        x = points[i,0];
        y = points[i,1];
        a[i] = Math.Max(mod(x), mod(y));
    }

    // Sort the array
    Array.Sort(a);

    // Index at which atleast required point are
    // inside square of length 2*M
    int index = (int) (n / 2 - 1);
    Console.WriteLine("Minimum M required is: " + a[index]);
}

// Driver Code
public static void Main(String []args)
{
    int N;
    N = 4;
    findSquare(N);
}
}

// This code contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to Calculate Absolute Value
function mod($x)
{
    if ($x >= 0)
        return $x;
    return -$x;
}

// Function to Calculate the
// Minimum value of M
function findSquare($n)
{
    $points = array(array( 1, 2 ),
                    array( -3, 4 ),
                    array( 1, 78 ),
                    array( -3, -7 ));
    $a[$n] = array();

    // To store the minimum M for each
    // point in array
    for ($i = 0; $i < $n; $i++)
    {
        $x; $y;
        $x = $points[$i][0];
        $y = $points[$i][1];
        $a[$i] = max(mod($x), mod($y));
    }

    // Sort the array
    sort($a);

    // Index at which atleast required point
    // are inside square of length 2*M
    $index = floor($n / 2) - 1;
    echo "Minimum M required is: ",
                  $a[$index], "\n";
}

// Driver Code
$N = 4;
findSquare($N);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find next identical year

    // Function to Calculate Absolute Value
    function mod(x)
    {
        if (x >= 0)
            return x;
        return -x;
    }

    // Function to Calculate the Minimum value of M
    function findSquare(n)
    {
        let points = [ [ 1, 2 ], [ -3, 4 ],
                        [ 1, 78 ], [ -3, -7 ] ];
        let a = new Array(n);

        // To store the minimum M for each
        // point in array
        for (let i = 0; i < n; i++)
        {
            let x, y;
            x = points[i][0];
            y = points[i][1];
            a[i] = Math.max(mod(x), mod(y));
        }

        // Sort the array
        a.sort(function(a, b){return a - b});

        // Index at which atleast required point are
        // inside square of length 2*M
        let index = (Math.floor(n / 2) - 1);
        document.write("Minimum M required is: " + a[index]);
    }

    let N;
    N = 4;
    findSquare(N);

</script>
```

**Output:** 

```
Minimum M required is: 4
```