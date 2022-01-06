# 在棋盘上可以进行最小切割，这样棋盘就不会被分成两部分

> 原文:[https://www . geeksforgeeks . org/最小切割-棋盘上可以制作-这样-它就不会被分成两部分/](https://www.geeksforgeeks.org/minimum-cuts-can-be-made-in-the-chessboard-such-that-it-is-not-divided-into-2-parts/)

给定 M×N 棋盘。任务是确定我们可以在棋盘上进行的最大切割数，这样棋盘就不会被分成两部分。
**例:**

```
Input: M = 2, N = 4
Output: Maximum cuts = 3

Input: M = 3, N = 3
Output: Maximum cuts = 4
```

**表示:**

1.  对于 M = 2，N = 2，我们只能进行 1 次切割(用红色标记)。如果我们再切 1 刀，棋盘就会分成 2 块。
2.  对于 M = 2，N = 4，我们可以进行 3 次切割(红色标记)。如果我们再切 1 刀，棋盘就会分成 2 块。

因此，可以观察到切割数= **(m-1) * (n-1)** 。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// function that calculates the
// maximum no. of cuts
int numberOfCuts(int M, int N)
{
    int result = 0;

    result = (M - 1) * (N - 1);

    return result;
}

// Driver Code
int main()
{
    int M = 4, N = 4;

    // Calling function.
    int Cuts = numberOfCuts(M, N);

    cout << "Maximum cuts = " << Cuts;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG {

// function that calculates the
// maximum no. of cuts
static int numberOfCuts(int M, int N)
{
    int result = 0;

    result = (M - 1) * (N - 1);

    return result;
}

// Driver Code
public static void main(String args[])
{
    int M = 4, N = 4;

    // Calling function.
    int Cuts = numberOfCuts(M, N);

    System.out.println("Maximum cuts = " + Cuts);

}
}
```

## 蟒蛇 3

```
# Python3 implementation of
# above approach

# function that calculates the
# maximum no. of cuts
def numberOfCuts(M, N):
    result = 0

    result = (M - 1) * (N - 1)

    return result

# Driver code
if __name__=='__main__':

    M, N = 4, 4

    # Calling function.
    Cuts = numberOfCuts(M, N)

    print("Maximum cuts = ", Cuts)

# This code is contributed by
# Kriti_mangal
```

## C#

```
//C#  implementation of above approach
using System;

public class GFG{
// function that calculates the
// maximum no. of cuts
static int numberOfCuts(int M, int N)
{
    int result = 0;

    result = (M - 1) * (N - 1);

    return result;
}

// Driver Code

    static public void Main (){

    int M = 4, N = 4;
    // Calling function.
    int Cuts = numberOfCuts(M, N);

    Console.WriteLine("Maximum cuts = " + Cuts);
    }
//This code is contributed by akt_mit   
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php implementation of above approach

// function that calculates the
// maximum no. of cuts
function numberOfCuts($M, $N)
{
    $result = 0;

    $result = ($M - 1) * ($N - 1);

    return $result;
}

// Driver Code
$M = 4;
$N = 4;

// Calling function.
$Cuts = numberOfCuts($M, $N);

echo "Maximum cuts = ", $Cuts ;

// This code is contributed by ANKITRAI1
?>
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// function that calculates the
// maximum no. of cuts
function numberOfCuts(M, N)
{
    var result = 0;

    result = (M - 1) * (N - 1);

    return result;
}

// Driver Code
var M = 4, N = 4;

// Calling function.
var Cuts = numberOfCuts(M, N);
document.write( "Maximum cuts = " + Cuts);

</script>
```

**Output:** 

```
Maximum cuts = 9
```

**时间复杂度:** O(1)

**辅助空间:** O(1)