# 用按位“或”作为偶数计数对

> 原文:[https://www . geesforgeks . org/count-pairs-with-bitwise-or-as-偶数/](https://www.geeksforgeeks.org/count-pairs-with-bitwise-or-as-even-number/)

给定一个大小为 n 的数组 A[]，任务是找出存在多少对(I，j)，使得 A[i]或 A[j]为偶数。
**例:**

```
Input : N = 4
        A[] = { 5, 6, 2, 8 }
Output :3
Explanation :
Since pair of A[] = ( 5, 6 ), ( 5, 2 ), ( 5, 8 ),
( 6, 2 ), ( 6, 8 ), ( 2, 8 )
5 OR 6 = 7, 5 OR 2 = 7, 5 OR 8 = 13
6 OR 2 = 6, 6 OR 8 = 14, 2 OR 8 = 10
Total pair A( i, j ) = 6 and Even = 3

Input : N = 7
        A[] = {8, 6, 2, 7, 3, 4, 9}
Output :6
```

一个**简单的解决方法**就是检查每一对。

## C++

```
// C++ program to count pairs with even OR
#include <iostream>
using namespace std;

int findEvenPair(int A[], int N)
{
    int evenPair = 0;
    for (int i = 0; i < N; i++) {
        for (int j = i + 1; j < N; j++) {

            // find OR operation
            // check odd or even
            if ((A[i] | A[j]) % 2 == 0)
                evenPair++;
        }
    }
    // return count of even pair
    return evenPair;
}
// Driver main
int main()
{
    int A[] = { 5, 6, 2, 8 };
    int N = sizeof(A) / sizeof(A[0]);
    cout << findEvenPair(A, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// pairs with even OR
import java.io.*;

class GFG
{

static int findEvenPair(int A[],
                        int N)
{
    int evenPair = 0;
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {

            // find OR operation
            // check odd or even
            if ((A[i] | A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return count of even pair
    return evenPair;
}

// Driver Code
public static void main (String[] args)
{
    int A[] = { 5, 6, 2, 8 };
    int N = A.length;
    System.out.println(findEvenPair(A, N));
}
}

// This code is contributed
// by inder_verma.
```

## 蟒蛇 3

```
# Python 3 program to count pairs
# with even OR

def findEvenPair(A, N) :
    evenPair = 0

    for i in range(N) :
        for j in range(i+1, N):

            # find OR operation
            # check odd or even
            if (A[i] | A[j]) % 2 == 0 :
                evenPair += 1

    # return count of even pair
    return evenPair

# Driver Code
if __name__ == "__main__" :

    A = [ 5, 6, 2, 8]
    N = len(A)

    # function calling
    print(findEvenPair(A, N))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to count
// pairs with even OR
using System;

class GFG
{

static int findEvenPair(int []A,
                        int N)
{
    int evenPair = 0;
    for (int i = 0; i < N; i++)
    {
        for (int j = i + 1; j < N; j++)
        {

            // find OR operation
            // check odd or even
            if ((A[i] | A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return count of even pair
    return evenPair;
}

// Driver Code
public static void Main ()
{
    int []A = { 5, 6, 2, 8 };
    int N = A.Length;
    Console.WriteLine(findEvenPair(A, N));
}
}

// This code is contributed
// by inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// pairs with even OR
function findEvenPair($A, $N)
{
    $evenPair = 0;
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = $i + 1; $j < $N; $j++)
        {

            // find OR operation
            // check odd or even
            if (($A[$i] | $A[$j]) % 2 == 0)
                $evenPair++;
        }
    }
    // return count of even pair
    return $evenPair;
}

// Driver Code
$A = array(5, 6, 2, 8);
$N = count($A);
echo findEvenPair($A, $N);

// This code is contributed
// by inder_verma.
?>
```

## java 描述语言

```
<script>
// JavaScript program to count pairs with even OR

function findEvenPair(A, N)
{
    let evenPair = 0;
    for (let i = 0; i < N; i++) {
        for (let j = i + 1; j < N; j++) {

            // find OR operation
            // check odd or even
            if ((A[i] | A[j]) % 2 == 0)
                evenPair++;
        }
    }
    // return count of even pair
    return evenPair;
}
// Driver main

    let A = [5, 6, 2, 8 ];
    let N = A.length;
    document.write(findEvenPair(A, N));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
3
```