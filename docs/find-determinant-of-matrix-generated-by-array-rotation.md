# 求数组旋转生成矩阵的行列式

> 原文:[https://www . geesforgeks . org/find-矩阵的行列式-由数组旋转生成/](https://www.geeksforgeeks.org/find-determinant-of-matrix-generated-by-array-rotation/)

给定一个由三个元素组成的数组。任务是利用阵列的所有三个旋转作为矩阵的一行，构造一个 3×3 阶的矩阵，并求出结果矩阵的行列式。

**示例**:

```
Input : arr[] = {1, 2, 3}
Output : 18

Input : arr[] = {1, 1, 1}
Output : 0
```

**方法:**根据问题陈述，使用给定的数组构造一个 3*3 的矩阵。如果 a1、a2、a3 是数组元素，那么对应的矩阵将是:

```
{{a1, a2, a3}, 
 {a3, a1, a2},
 {a2, a3, a1}}
```

任务是计算上述矩阵的行列式。
这个行列式可以用适当的[方法](https://www.geeksforgeeks.org/determinant-of-a-matrix/)来计算，但是另一方面，如果将结果矩阵展开计算，结果将是**a1<sup>3</sup>+a2<sup>3</sup>+a3<sup>3</sup>–3 * a1 * a2 * a3**。因此，使用上面生成的公式，而不是通过适当的展开来计算行列式。
因此，上述矩阵的行列式为:

```
a13 + a23 + a33 - (3*a1*a2*a3)
```

以下是上述方法的实现:

## C++

```
// C++ program for finding determinant of generated matrix

#include <bits/stdc++.h>
#define N 3
using namespace std;

// Function to calculate determinant
int calcDeterminant(int arr[])
{
    int determinant = 0;

    for (int i = 0; i < N; i++) {
        determinant += pow(arr[i], 3);
    }

    determinant -= 3 * arr[0] * arr[1] * arr[2];

    return determinant;
}

// Driver code
int main()
{
    int arr[] = { 4, 5, 3 };
    cout << calcDeterminant(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding determinant
// of generated matrix
import java.util.*;
import java.lang.*;

class GFG
{
static int N = 3;

// Function to calculate determinant
static double calcDeterminant(int arr[])
{
    double determinant = 0;

    for (int i = 0; i < N; i++)
    {
        determinant += Math.pow(arr[i], 3);
    }

    determinant -= 3 * arr[0] *
                    arr[1] * arr[2];

    return determinant;
}

// Driver code
static public void main (String args[])
{
    int []arr = { 4, 5, 3 };
    System.out.println(calcDeterminant(arr));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python3 program for finding determinant of generated matrix

# Function to calculate determinant
def calcDeterminant(arr,n):
    determinant =0

    for i in range(n):
        determinant+= pow(arr[i],3)

    determinant -= 3*arr[0]*arr[1]*arr[2]

    return determinant

# Driver code
arr = [4,5,3]
n = len(arr)
print(calcDeterminant(arr,n))

# This code is contributed by Shrikant13
```

## C#

```
// C# program for finding determinant
// of generated matrix
using System;

class GFG
{
static int N = 3;

// Function to calculate determinant
static double calcDeterminant(int []arr)
{
    double determinant = 0;

    for (int i = 0; i < N; i++)
    {
        determinant += Math.Pow(arr[i], 3);
    }

    determinant -= 3 * arr[0] *
                       arr[1] * arr[2];

    return determinant;
}

// Driver code
static public void Main ()
{
    int []arr = { 4, 5, 3 };
    Console.WriteLine(calcDeterminant(arr));
}
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding determinant
// of generated matrix

$N = 3;

// Function to calculate determinant
function calcDeterminant($arr)
{
    global $N;
    $determinant = 0;

    for ($i = 0; $i < $N; $i++)
    {
        $determinant += pow($arr[$i], 3);
    }

    $determinant -= 3 * $arr[0] *
                        $arr[1] * $arr[2];

    return $determinant;
}

// Driver code
$arr = array( 4, 5, 3 );
echo calcDeterminant($arr);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// Java script  program for finding determinant
// of generated matrix

let  N = 3;

// Function to calculate determinant
function calcDeterminant(arr)
{
    let determinant = 0;

    for (let i = 0; i < N; i++)
    {
        determinant += Math.pow(arr[i], 3);
    }

    determinant -= 3 * arr[0] *
                    arr[1] * arr[2];

    return determinant;
}

// Driver code

    let arr =[ 4, 5, 3 ];
    document.write(calcDeterminant(arr));

//contributed by bobby

</script>
```

**Output:** 

```
36
```