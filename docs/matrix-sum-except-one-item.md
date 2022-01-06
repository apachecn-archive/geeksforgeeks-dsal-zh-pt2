# 除一项外的矩阵和

> 原文:[https://www.geeksforgeeks.org/matrix-sum-except-one-item/](https://www.geeksforgeeks.org/matrix-sum-except-one-item/)

给定一个 n*m 矩阵，求该矩阵元素的和，而不求其位置所指定的元素
**例:**

```
Input : mat[] = {{1 2 4}, 
                {5 6 8}}
         cell = (0 2)
Output :22
We need to find sum of all elements
except mat[0][2].

Input : mat[][] = {{5 6 2 3}, {2 3 1 8}, {9 6 5 2}}
        cell = (1 2)
Output :51
```

一个**简单的解决方案**就是遍历矩阵。对于每个被访问的单元，检查它是否是要被忽略的单元。

## C++

```
// C++ program to find sum
// of matrix except cell (x, y)
#include<bits/stdc++.h>
using namespace std;

// Dimension of input matrix
# define R 2
# define C 3

// Returns sum of arr[][]
// except cell arr[x][y]
int calcSum(int arr[R][C],
            int x, int y)
{
    int sum = 0;
    for (int i = 0; i < R; i++)
    {
        for (int j = 0; j < C; j++)
        {
            if (i != x || j != y)
                sum = sum + arr[i][j];
        }
    }
    return sum;
}

// Driver code
int main()
{
    int x = 0, y = 2;
    int arr[R][C] = {1, 2, 4,
                     5, 6, 8 };

    cout << calcSum(arr, x, y);
}

// This code is contributed
// by ChitraNayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of matrix except
// cell (x, y)
class Matrix {

    // Returns sum of arr[][] except cell arr[x][y]
    static int calcSum(int[][] arr, int x, int y)
    {
        int sum = 0;
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr[i].length; j++) {
              if (i != x || j != y)
                sum = sum + arr[i][j];
            }
        }
        return sum;
    }
    public static void main(String[] args)
    {
        int x = 0, y = 2;
        int[][] arr = {
            { 1, 2, 4 }, { 5, 6, 8 },
        };
        System.out.println(calcSum(arr, x, y));
    }
}
```

## C#

```
// C# program to find sum
// of matrix except cell (x, y)
using System;

class GFG
{

    // Returns sum of arr[,]
    // except cell arr[x][y]
    static int calcSum(int[,] arr,
                       int x, int y)
    {
        int sum = 0;
        for (int i = 0;
                 i < arr.GetLength(0); i++)
        {
            for (int j = 0;
                     j < arr.GetLength(1); j++)
            {
            if (i != x || j != y)
                sum = sum + arr[i, j];
            }
        }
        return sum;
    }

    // Driver Code
    public static void Main()
    {
        int x = 0, y = 2;
        int[,] arr = {{ 1, 2, 4 },
                      { 5, 6, 8 }};
        Console.Write(calcSum(arr, x, y));
    }
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to find
# sum of matrix except cell (x, y)

# Returns sum of arr[][]
# except cell arr[x][y]
def calcSum(arr, x, y):
    s = 0
    for i in range(R):
        for j in range(C):
            if (i != x or j != y):
                s = s + arr[i][j];
    return s;

# Driver code
x = 0
y = 2
arr = [[ 1, 2, 4 ],
       [ 5, 6, 8 ]]
R = 2
C = 3

print(calcSum(arr, x, y))

# This code is contributed
# by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// sum of matrix except
// cell (x, y)
$R = 2;
$C = 3;

// Returns sum of arr[][]
// except cell arr[x][y]
function calcSum(&$arr, $x, $y)
{
    global $R,$C;
    $sum = 0;
    for ($i = 0; $i < $R; $i++)
    {
        for ($j = 0; $j < $C; $j++)
        {
            if ($i != $x || $j != $y)
                $sum = $sum + $arr[$i][$j];
        }
    }
    return $sum;
}

// Driver code
$x = 0;
$y = 2;
$arr = array(array(1, 2, 4),
             array(5, 6, 8));

echo (calcSum($arr, $x, $y));

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
// Javascript program to find sum of matrix except
// cell (x, y)

    // Returns sum of arr[][] except cell arr[x][y]
    function calcSum(arr,x,y)
    {
         let sum = 0;
        for (let i = 0; i < arr.length; i++) {
            for (let j = 0; j < arr[i].length; j++) {
              if (i != x || j != y)
                sum = sum + arr[i][j];
            }
        }
        return sum;
    }

    let x = 0, y = 2;

    let arr=[[1, 2, 4],[5, 6, 8 ]];
    document.write(calcSum(arr, x, y));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
22
```

上述解决方案会对每个矩阵项进行额外的比较。一个**更好的解决方案**是先求整体和，然后减去给定的单元格。

## C++

```
// C++ program to find sum
// of matrix except cell (x, y)
#include<bits/stdc++.h>
using namespace std;

#define R 2
#define C 3

// Returns sum of arr[][]
// except cell arr[x][y]
int calcSum(int arr[R][C],
            int x, int y)
{
    int sum = 0;
    for (int i = 0; i < R; i++)
        for (int j = 0; j < C; j++)
            sum = sum + arr[i][j];

    return sum - arr[x][y];
}

// Driver code
int main()
{
    int x = 0, y = 2;
    int arr[R][C]= {1, 2, 4 ,
                    5, 6, 8 };

    cout << (calcSum(arr, x, y));
}

// This code is contributed
// by ChitraNayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of matrix except
// cell (x, y)
class Matrix {

    // Returns sum of arr[][] except cell arr[x][y]
    static int calcSum(int[][] arr, int x, int y)
    {
        int sum = 0;
        for (int i = 0; i < arr.length; i++)
            for (int j = 0; j < arr[i].length; j++)
                sum = sum + arr[i][j];

        return sum - arr[x][y];
    }

    public static void main(String[] args)
    {
        int x = 0, y = 2;
        int[][] arr = {
            { 1, 2, 4 }, { 5, 6, 8 },
        };
        System.out.println(calcSum(arr, x, y));
    }
}
```

## C#

```
// C# program to find sum
// of matrix except cell (x, y)
using System;

class GFG
{

    // Returns sum of arr[,]
    // except cell arr[x,y]
    static int calcSum(int[,] arr,
                       int x, int y)
    {
        int sum = 0;
        for (int i = 0;
                 i < arr.GetLength(0); i++)
            for (int j = 0;
                     j < arr.GetLength(1); j++)
                sum = sum + arr[i, j];

        return sum - arr[x, y];
    }

    // Driver code
    public static void Main()
    {
        int x = 0, y = 2;
        int[,] arr = {{ 1, 2, 4 },
                      { 5, 6, 8 }};
        Console.Write(calcSum(arr, x, y));
    }
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 program to find
# sum of matrix except cell (x, y)

# Returns sum of arr[][]
# except cell arr[x][y]
def calcSum( arr, x, y):
    s = 0
    for i in range(R):
        for j in range(C):
            s = s + arr[i][j]

    return s - arr[x][y]

# Driver code
x = 0
y = 2
R = 2
C = 3
arr = [[1, 2, 4 ],
       [5, 6, 8 ]]

print (calcSum(arr, x, y))

# This code is contributed
# by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum
// of matrix except cell (x, y)
$R = 2;
$C = 3;

// Returns sum of $arr[][]
// except cell $arr[$x][$y]
function calcSum(&$arr, $x, $y)
{
    global $R,$C;
    $sum = 0;
    for ($i = 0; $i < $R; $i++)
        for ($j = 0; $j < $C; $j++)
            $sum = $sum + $arr[$i][$j];

    return $sum - $arr[$x][$y];
}

// Driver code
$x = 0;
$y = 2;
$arr= array(array(1, 2, 4 ),
            array(5, 6, 8 ));

echo (calcSum($arr, $x, $y));

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find sum of matrix except
// cell (x, y)

    // Returns sum of arr[][] except cell arr[x][y]
    function calcSum(arr,x,y)
    {
        let sum = 0;
        for (let i = 0; i < arr.length; i++)
            for (let j = 0; j < arr[i].length; j++)
                sum = sum + arr[i][j];

        return sum - arr[x][y];
    }

    let x = 0, y = 2;
    let arr = [[1, 2, 4 ],
       [5, 6, 8 ]];

    document.write(calcSum(arr, x, y));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
22
```