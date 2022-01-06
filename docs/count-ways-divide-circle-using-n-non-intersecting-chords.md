# 计算使用 N 个不相交弦划分圆的方法

> 原文:[https://www . geeksforgeeks . org/count-way-divide-circle-using-n-non-interfering-和弦/](https://www.geeksforgeeks.org/count-ways-divide-circle-using-n-non-intersecting-chords/)

给定一个数 N，找出在一个有 2*N 个点的圆上画 N 个弦的方法，这样就不会有 2 个弦相交。
如果有一个和弦以一种方式出现，而不是以另一种方式出现，那么两种方式是不同的。
**例:**

```
Input : N = 2
Output : 2
Explanation: If points are numbered 1 to 4 in 
clockwise direction, then different ways to 
draw chords are:
{(1-2), (3-4)} and {(1-4), (2-3)}

Input : N = 1
Output : 1
Explanation: Draw a chord between points 1 and 2.
```

如果我们在任意两点之间画一个弦，你能观察到当前的点集合被分成两个更小的集合 S1 和 S2 吗？如果我们从 S1 点到 S2 点画一个弦，它肯定会和我们刚才画的弦相交。
所以，我们可以得出一个递推公式，way(n)= sum[I = 0 到 n-1]{ way(I)* way(n-I-1)}。
这里我们迭代 I，假设其中一个集合的大小为 I，另一个集合的大小自动为(n-i-1)，因为我们已经在一个集合中使用了一对点和 I 对点。

## C++

```
// cpp code to count ways
// to divide circle using
// N non-intersecting chords.
#include <bits/stdc++.h>
using namespace std;

int chordCnt( int A){

    // n = no of points required
    int n = 2 * A;

    // dp array containing the sum
    int dpArray[n + 1]={ 0 };
    dpArray[0] = 1;
    dpArray[2] = 1;
    for (int i=4;i<=n;i+=2){
        for (int j=0;j<i-1;j+=2){

          dpArray[i] +=
            (dpArray[j]*dpArray[i-2-j]);
        }
    }

    // returning the required number
    return dpArray[n];
}
// Driver function
int main()
{

    int N;
    N = 2;
cout<<chordCnt( N)<<'\n';
    N = 1;
cout<<chordCnt( N)<<'\n';
    N = 4;
cout<<chordCnt( N)<<'\n';
    return 0;
}

// This code is contributed by Gitanjali.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count ways
// to divide circle using
// N non-intersecting chords.
import java.io.*;

class GFG {
    static int chordCnt(int A)
    {

        // n = no of points required
        int n = 2 * A;

        // dp array containing the sum
        int[] dpArray = new int[n + 1];
        dpArray[0] = 1;
        dpArray[2] = 1;
        for (int i = 4; i <= n; i += 2) {
            for (int j = 0; j < i - 1; j += 2)
            {
                dpArray[i] += (dpArray[j] *
                              dpArray[i - 2 - j]);
            }
        }

        // returning the required number
        return dpArray[n];
    }
    public static void main(String[] args)
    {
        int N;
        N = 2;
        System.out.println(chordCnt(N));
        N = 1;
        System.out.println(chordCnt(N));
        N = 4;
        System.out.println(chordCnt(N));
    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# python code to count ways to divide
# circle using N non-intersecting chords.
def chordCnt( A):

    # n = no of points required
    n = 2 * A

    # dp array containing the sum
    dpArray = [0]*(n + 1)
    dpArray[0] = 1
    dpArray[2] = 1
    for i in range(4, n + 1, 2):
        for j in range(0, i-1, 2):
            dpArray[i] += (dpArray[j]*dpArray[i-2-j])

    # returning the required number
    return int(dpArray[n])

# driver code
N = 2
print(chordCnt( N))
N = 1
print(chordCnt( N))
N = 4
print(chordCnt( N))
```

## C#

```
// C# code to count ways to divide
// circle using N non-intersecting chords.
using System;

class GFG {

    static int chordCnt(int A)
    {
        // n = no of points required
        int n = 2 * A;

        // dp array containing the sum
        int[] dpArray = new int[n + 1];
        dpArray[0] = 1;
        dpArray[2] = 1;

        for (int i = 4; i <= n; i += 2)
        {
            for (int j = 0; j < i - 1; j += 2)
            {
                dpArray[i] += (dpArray[j] * dpArray[i - 2 - j]);
            }
        }

        // returning the required number
        return dpArray[n];
    }

    // Driver code
    public static void Main()
    {
        int N;
        N = 2;
        Console.WriteLine(chordCnt(N));
        N = 1;
        Console.WriteLine(chordCnt(N));
        N = 4;
        Console.WriteLine(chordCnt(N));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to count ways
// to divide circle using
// N non-intersecting chords.
function chordCnt( $A)
{

    // n = no of points required
    $n = 2 * $A;

    // dp array containing the sum
    $dpArray = array_fill(0, $n + 1, 0);
    $dpArray[0] = 1;
    $dpArray[2] = 1;
    for ($i = 4; $i <= $n; $i += 2)
    {
        for ($j = 0; $j < $i - 1; $j += 2)
        {

            $dpArray[$i] += ($dpArray[$j] *
                             $dpArray[$i - 2 - $j]);
        }
    }

    // returning the required number
    return $dpArray[$n];
}

// Driver Code
$N = 2;
echo chordCnt($N), "\n";
$N = 1;
echo chordCnt($N), "\n";
$N = 4;
echo chordCnt($N), "\n";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript code to count ways
// to divide circle using
// N non-intersecting chords.

function chordCnt( A){

    // n = no of points required
    var n = 2 * A;

    // dp array containing the sum
    var dpArray = Array(n+1).fill(0);
    dpArray[0] = 1;
    dpArray[2] = 1;
    for (var i=4;i<=n;i+=2){
        for (var j=0;j<i-1;j+=2){

          dpArray[i] +=
            (dpArray[j]*dpArray[i-2-j]);
        }
    }

    // returning the required number
    return dpArray[n];
}

// Driver function
var N;
N = 2;
document.write( chordCnt( N) + '<br>');
N = 1;
document.write( chordCnt( N) + '<br>');
N = 4;
document.write( chordCnt( N) + '<br>');

</script>
```

**输出:**

```
2
1
14
```