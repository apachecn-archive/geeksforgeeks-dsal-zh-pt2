# 寻找立方体对|集合 2(一个 n^(1/3)解)

> 原文:[https://www . geesforgeks . org/find-cube-pairs-set-2-n13-solution/](https://www.geeksforgeeks.org/find-cube-pairs-set-2-n13-solution/)

给定一个数 n，找出两对可以表示该数为两个立方体之和的数。换句话说，找到两对(a，b)和(c，d)，这样给定的数 n 可以表示为

```
n = a^3 + b^3 = c^3 + d^3
```

其中 a、b、c 和 d 是四个不同的数字。
**例:**

```
Input: n = 1729
Output: (1, 12) and (9, 10)
Explanation: 
1729 = 1^3 + 12^3 = 9^3 + 10^3

Input: n = 4104
Output: (2, 16) and (9, 15)
Explanation: 
4104 = 2^3 + 16^3 = 9^3 + 15^3

Input: n = 13832
Output: (2, 24) and (18, 20)
Explanation: 
13832 = 2^3 + 24^3 = 18^3 + 20^3
```

我们已经在下面的第 1 集讨论了一个 O( *n <sup>2/3</sup>* )解。
[求立方体对|集 1 (A n^(2/3)解)](https://www.geeksforgeeks.org/find-cube-pairs-set-1-n23-solution/)
在这篇文章中，a O( *n <sup>1/3</sup>* )解被讨论。
满足约束的任意数 n 将有两个不同的对(a，b)和(c，d)，使得 a，b，c 和 d 都小于 *n <sup>1/3</sup>* 。想法是创建一个大小为 *n <sup>1/3</sup>* 的辅助数组。数组中的每个索引 I 将存储等于该索引的立方的值，即 arr[i] = i^3.现在这个问题简化为寻找排序数组中的一对元素，其和等于给定的数 n。这个问题在这里[详细讨论](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)。
以下是上述思路的实现:

## C++

```
// C++ program to find pairs that can represent
// the given number as sum of two cubes
#include <iostream>
#include <cmath>
using namespace std;

// Function to find pairs that can represent
// the given number as sum of two cubes
void findPairs(int n)
{
    // find cube root of n
    int cubeRoot = pow(n, 1.0 / 3.0);

    // create a array of size of size 'cubeRoot'
    int cube[cubeRoot + 1];

    // for index i, cube[i] will contain i^3
    for (int i = 1; i <= cubeRoot; i++)
        cube[i] = i*i*i;

    // Find all pairs in above sorted
    // array cube[] whose sum is equal to n
    int l = 1;
    int r = cubeRoot;

    while (l < r)
    {
        if (cube[l] + cube[r] < n)
            l++;
        else if(cube[l] + cube[r] > n)
            r--;
        else {
            cout << "(" << l <<  ", "  << r
                 << ")" << endl;
            l++; r--;
        }
    }
}

// Driver function
int main()
{
    int n = 20683;
    findPairs(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find pairs
// that can represent the given
// number as sum of two cubes
import java.io.*;

class GFG
{

// Function to find pairs
// that can represent the
// given number as sum of
// two cubes
static void findPairs(int n)
{
    // find cube root of n
    int cubeRoot = (int)Math.pow(
                             n, 1.0 / 3.0);

    // create a array of
    // size of size 'cubeRoot'
    int cube[] = new int[cubeRoot + 1];

    // for index i, cube[i]
    // will contain i^3
    for (int i = 1; i <= cubeRoot; i++)
        cube[i] = i * i * i;

    // Find all pairs in above
    // sorted array cube[]
    // whose sum is equal to n
    int l = 1;
    int r = cubeRoot;

    while (l < r)
    {
        if (cube[l] + cube[r] < n)
            l++;
        else if(cube[l] + cube[r] > n)
            r--;
        else {
            System.out.println("(" + l +
                              ", " + r +
                                  ")" );
            l++; r--;
        }
    }
}

// Driver Code
public static void main (String[] args)
{
int n = 20683;
findPairs(n);
}
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python3 program to find pairs that
# can represent the given number
# as sum of two cubes
import math

# Function to find pairs that can
# represent the given number as
# sum of two cubes
def findPairs( n):

    # find cube root of n
    cubeRoot = int(math.pow(n, 1.0 / 3.0));

    # create a array of
    # size of size 'cubeRoot'
    cube = [0] * (cubeRoot + 1);

    # for index i, cube[i]
    # will contain i^3
    for i in range(1, cubeRoot + 1):
        cube[i] = i * i * i;

    # Find all pairs in above sorted
    # array cube[] whose sum
    # is equal to n
    l = 1;
    r = cubeRoot;

    while (l < r):
        if (cube[l] + cube[r] < n):
            l += 1;
        elif(cube[l] + cube[r] > n):
            r -= 1;
        else:
            print("(" , l , ", " , math.floor(r),
                                  ")", end = "");
            print();
            l += 1;
            r -= 1;

# Driver code
n = 20683;
findPairs(n);

# This code is contributed by mits
```

## C#

```
// C# program to find pairs
// that can represent the given
// number as sum of two cubes
using System;

class GFG
{

// Function to find pairs
// that can represent the
// given number as sum of
// two cubes
static void findPairs(int n)
{
    // find cube root of n
    int cubeRoot = (int)Math.Pow(n, 1.0 /
                                    3.0);

    // create a array of
    // size of size 'cubeRoot'
    int []cube = new int[cubeRoot + 1];

    // for index i, cube[i]
    // will contain i^3
    for (int i = 1; i <= cubeRoot; i++)
        cube[i] = i * i * i;

    // Find all pairs in above
    // sorted array cube[]
    // whose sum is equal to n
    int l = 1;
    int r = cubeRoot;

    while (l < r)
    {
        if (cube[l] + cube[r] < n)
            l++;
        else if(cube[l] + cube[r] > n)
            r--;
        else {
            Console.WriteLine("(" + l +
                              ", " + r +
                                  ")" );
            l++; r--;
        }
    }
}

// Driver Code
public static void Main ()
{
    int n = 20683;
    findPairs(n);
}
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find pairs
// that can represent the
// given number as sum of
// two cubes

// Function to find pairs
// that can represent the
// given number as sum of
// two cubes
function findPairs( $n)
{

    // find cube root of n
    $cubeRoot = pow($n, 1.0 / 3.0);

    // create a array of
    // size of size 'cubeRoot'
    $cube = array();

    // for index i, cube[i]
    // will contain i^3
    for ($i = 1; $i <= $cubeRoot; $i++)
        $cube[$i] = $i * $i * $i;

    // Find all pairs in above sorted
    // array cube[] whose sum
    // is equal to n
    $l = 1;
    $r = $cubeRoot;

    while ($l < $r)
    {
        if ($cube[$l] + $cube[$r] <$n)
            $l++;
        else if($cube[$l] + $cube[$r] > $n)
            $r--;
        else
        {
            echo "(" , $l , ", " , floor($r)
                , ")" ;
                echo "\n";
            $l++;$r--;
        }
    }
}

// Driver code
$n = 20683;
findPairs($n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program to find pairs
// that can represent the given
// number as sum of two cubes

// Function to find pairs
// that can represent the
// given number as sum of
// two cubes
function findPairs(n)
{
    // find cube root of n
    var cubeRoot = parseInt(Math.pow(
                             n, 1.0 / 3.0));

    // create a array of
    // size of size 'cubeRoot'
    var cube = Array.from({length: cubeRoot + 1}, (_, i) => 0);

    // for index i, cube[i]
    // will contain i^3
    for (i = 1; i <= cubeRoot; i++)
        cube[i] = i * i * i;

    // Find all pairs in above
    // sorted array cube
    // whose sum is equal to n
    var l = 1;
    var r = cubeRoot;

    while (l < r)
    {
        if (cube[l] + cube[r] < n)
            l++;
        else if(cube[l] + cube[r] > n)
            r--;
        else {
            document.write("(" + l +
                              ", " + r +
                                  ")<br>" );
            l++; r--;
        }
    }
}

// Driver Code
var n = 20683;
findPairs(n);

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
(10, 27)
(19, 24)
```

**上述解的时间复杂度**为 O(n^(1/3)).
本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。