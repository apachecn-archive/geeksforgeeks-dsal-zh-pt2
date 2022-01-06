# 将按位异或的对计数为偶数

> 原文:[https://www . geesforgeks . org/count-pairs-with-bitwise-xor-as-偶数/](https://www.geeksforgeeks.org/count-pairs-with-bitwise-xor-as-even-number/)

给定一个 n 个整数的数组，任务是找到对(I，j)的数目，使得 A[i] ^ A[j]是偶数。
**例:**

```
Input: A[] =  { 5, 4, 7, 2, 1}
Output: 4
Since pair of A[] =
( 5, 4 ) = 1( 5, 7 ) = 2( 5, 2 ) = 7( 5, 1 ) = 4
( 4, 7 ) = 3( 4, 2 ) = 6( 4, 1 ) = 5
( 7, 2 ) = 5( 7, 1 ) = 6
( 2, 1 ) = 3
Total XOR even pair  = 4

Input: A[] = { 7, 2, 8, 1, 0, 5, 11 }
Output: 9
Since pair of A[] =
( 7, 2 ) = 5( 7, 8 ) = 15( 7, 1 ) = 6( 7, 0 ) = 7( 7, 5 ) = 2( 7, 11 ) = 12
( 2, 8 ) = 10( 2, 1 ) = 3( 2, 0 ) = 2( 2, 5 ) = 7( 2, 11 ) = 9
( 8, 1 ) = 9( 8, 0 ) = 8( 8, 5 ) = 13( 8, 11 ) = 3
( 1, 0 ) = 1( 1, 5 ) = 4( 1, 11 ) = 10
( 0, 5 ) = 5( 0, 11 ) = 11
( 5, 11 ) = 14
```

一种**天真的方法**是检查每一对并打印偶数对的计数。
以下是上述办法的实施情况:

## C++

```
// C++ program to count pairs
// with XOR giving a even number
#include <iostream>
using namespace std;

// Function to count number of even pairs
int findevenPair(int A[], int N)
{
    int i, j;

    // variable for counting even pairs
    int evenPair = 0;

    // find all pairs
    for (i = 0; i < N; i++) {
        for (j = i + 1; j < N; j++) {

            // find XOR operation
            // check even or even
            if ((A[i] ^ A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return number of even pair
    return evenPair;
}

// Driver Code
int main()
{

    int A[] = { 5, 4, 7, 2, 1 };
    int N = sizeof(A) / sizeof(A[0]);

    // calling function findevenPair
    // and print number of even pair
    cout << findevenPair(A, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs
// with XOR giving a even number
import java.io.*;

class GFG
{

// Function to count number of even pairs
static int findevenPair(int []A, int N)
{
    int i, j;

    // variable for counting even pairs
    int evenPair = 0;

    // find all pairs
    for (i = 0; i < N; i++)
    {
        for (j = i + 1; j < N; j++)
        {

            // find XOR operation
            // check even or even
            if ((A[i] ^ A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return number of even pair
    return evenPair;
}

// Driver Code
public static void main (String[] args)
{
    int A[] = { 5, 4, 7, 2, 1 };
    int N = A.length;

    // calling function findevenPair
    // and print number of even pair
    System.out.println(findevenPair(A, N));
}
}

// This code is contributed by inder_verma..
```

## 蟒蛇 3

```

# Python3 program to count pairs
# with XOR giving a even number

# Function to count number of even pairs
def findevenPair(A, N):

    # variable for counting even pairs
    evenPair = 0

    # find all pairs
    for i in range(0, N):
        for j in range(i+1, N):

            # find XOR operation
            # check even or even
            if ((A[i] ^ A[j]) % 2 == 0):
                evenPair+=1

    # return number of even pair
    return evenPair;

# Driver Code
def main():
    A = [ 5, 4, 7, 2, 1 ]
    N = len(A)

    # calling function findevenPair
    # and prnumber of even pair
    print(findevenPair(A, N))

if __name__ == '__main__':
    main()
# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to count pairs
// with XOR giving a even number
using System;

class GFG
{

// Function to count number of
// even pairs
static int findevenPair(int []A, int N)
{
    int i, j;

    // variable for counting even pairs
    int evenPair = 0;

    // find all pairs
    for (i = 0; i < N; i++)
    {
        for (j = i + 1; j < N; j++)
        {

            // find XOR operation
            // check even or even
            if ((A[i] ^ A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return number of even pair
    return evenPair;
}

// Driver Code
public static void Main ()
{
    int []A = { 5, 4, 7, 2, 1 };
    int N = A.Length;

    // calling function findevenPair
    // and print number of even pair
    Console.WriteLine(findevenPair(A, N));
}
}

// This code is contributed
// by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pairs
// with XOR giving a even number

// Function to count number
// of even pairs
function findevenPair(&$A, $N)
{

    // variable for counting even pairs
    $evenPair = 0;

    // find all pairs
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = $i + 1; $j < $N; $j++)
        {

            // find XOR operation
            // check even or even
            if (($A[$i] ^ $A[$j]) % 2 == 0)
                $evenPair++;
        }
    }

    // return number of even pair
    return $evenPair;
}

// Driver Code
$A = array(5, 4, 7, 2, 1 );
$N = sizeof($A);

// calling function findevenPair
// and print number of even pair
echo (findevenPair($A, $N));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to count pairs
// with XOR giving a even number

// Function to count number of even pairs
function findevenPair(A, N)
{
    let i, j;

    // variable for counting even pairs
    let evenPair = 0;

    // find all pairs
    for (i = 0; i < N; i++) {
        for (j = i + 1; j < N; j++) {

            // find XOR operation
            // check even or even
            if ((A[i] ^ A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return number of even pair
    return evenPair;
}

// Driver Code
let A = [ 5, 4, 7, 2, 1 ];
let N = A.length;

// calling function findevenPair
// and print number of even pair
document.write(findevenPair(A, N));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
4
```