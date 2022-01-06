# 将按位异或的对计数为奇数

> 原文:[https://www . geesforgeks . org/count-pairs-with-bitwise-xor-as-奇数/](https://www.geeksforgeeks.org/count-pairs-with-bitwise-xor-as-odd-number/)

给定一个 n 个整数的数组，任务是找到对(I，j)的数目，使得 A[i] ^ A[j]是奇数。
**例:**

```
Input : N = 5
        A[] =  { 5, 4, 7, 2, 1}
Output :6
Since pair of A[] =
( 5, 4 ) = 1( 5, 7 ) = 2( 5, 2 ) = 7( 5, 1 ) = 4
( 4, 7 ) = 3( 4, 2 ) = 6( 4, 1 ) = 5
( 7, 2 ) = 5( 7, 1 ) = 6
( 2, 1 ) = 3
Total XOR ODD pair  = 6

Input : N = 7
        A[] = { 7, 2, 8, 1, 0, 5, 11 }
Output :12
Since pair of A[] =
( 7, 2 ) = 5( 7, 8 ) = 15( 7, 1 ) = 6( 7, 0 ) = 7( 7, 5 ) = 2( 7, 11 ) = 12
( 2, 8 ) = 10( 2, 1 ) = 3( 2, 0 ) = 2( 2, 5 ) = 7( 2, 11 ) = 9
( 8, 1 ) = 9( 8, 0 ) = 8( 8, 5 ) = 13( 8, 11 ) = 3
( 1, 0 ) = 1( 1, 5 ) = 4( 1, 11 ) = 10
( 0, 5 ) = 5( 0, 11 ) = 11
( 5, 11 ) = 14
```

一种**天真的方法**是检查每一对并打印对的计数。
以下是上述办法的实施情况:

## C++

```
// C++ program to count pairs
// with XOR giving a odd number
#include <iostream>
using namespace std;

// Function to count number of odd pairs
int findOddPair(int A[], int N)
{
    int i, j;

    // variable for counting odd pairs
    int oddPair = 0;

    // find all pairs
    for (i = 0; i < N; i++) {
        for (j = i + 1; j < N; j++) {

            // find XOR operation
            // check odd or even
            if ((A[i] ^ A[j]) % 2 != 0)
                oddPair++;
        }
        cout << endl;
    }

    // return number of odd pair
    return oddPair;
}

// Driver Code
int main()
{

    int A[] = { 5, 4, 7, 2, 1 };
    int N = sizeof(A) / sizeof(A[0]);

    // calling function findOddPair
    // and print number of odd pair
    cout << findOddPair(A, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs
// with XOR giving a odd number

class GFG
{

// Function to count
// number of odd pairs
static int findOddPair(int A[],
                       int N)
{
    int i, j;

    // variable for counting
    // odd pairs
    int oddPair = 0;

    // find all pairs
    for (i = 0; i < N; i++)
    {
        for (j = i + 1; j < N; j++)
        {

            // find XOR operation
            // check odd or even
            if ((A[i] ^ A[j]) % 2 != 0)
                oddPair++;
        }

    }

    // return number
    // of odd pair
    return oddPair;
}

// Driver Code
public static void main(String args[])
{
    int A[] = { 5, 4, 7, 2, 1 };
    int N = A.length;

    // calling function findOddPair
    // and print number of odd pair
    System.out.println(findOddPair(A, N));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 蟒蛇 3

```
# Python3 program to count pairs
# with XOR giving a odd number

# Function to count number of odd pairs
def findOddPair(A, N) :

    # variable for counting odd pairs
    oddPair = 0

    # find all pairs
    for i in range(0, N) :
        for j in range(i+1, N) :

            # find XOR operation
            # check odd or even
            if ((A[i] ^ A[j]) % 2 != 0):
                oddPair+=1

    # return number of odd pair
    return oddPair

# Driver Code
if __name__=='__main__':
    A = [5, 4, 7, 2, 1 ]
    N = len(A)

# calling function findOddPair
# and print number of odd pair
    print(findOddPair(A, N))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to count pairs
// with XOR giving a odd number
using System;

class GFG
{

// Function to count
// number of odd pairs
static int findOddPair(int[] A,
                    int N)
{
    int i, j;

    // variable for counting
    // odd pairs
    int oddPair = 0;

    // find all pairs
    for (i = 0; i < N; i++)
    {
        for (j = i + 1; j < N; j++)
        {

            // find XOR operation
            // check odd or even
            if ((A[i] ^ A[j]) % 2 != 0)
                oddPair++;
        }

    }

    // return number
    // of odd pair
    return oddPair;
}

// Driver Code
public static void Main()
{
    int[] A = { 5, 4, 7, 2, 1 };
    int N = A.Length;

    // calling function findOddPair
    // and print number of odd pair
    Console.WriteLine(findOddPair(A, N));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)

# calling function findOddPair
# and print number of odd pair
print(findOddPair(a, n))
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP  program to count pairs
// with XOR giving a odd number

// Function to count number of odd pairs

function  findOddPair($A, $N)
{
     $i; $j;

    // variable for counting odd pairs
     $oddPair = 0;

    // find all pairs
    for ($i = 0; $i < $N; $i++) {
        for ($j = $i + 1; $j < $N; $j++) {

            // find XOR operation
            // check odd or even
            if (($A[$i] ^ $A[$j]) % 2 != 0)
                $oddPair++;
        }

    }

    // return number of odd pair
    return $oddPair;
}

// Driver Code

    $A = array( 5, 4, 7, 2, 1 );
    $N = sizeof($A) / sizeof($A[0]);

    // calling function findOddPair
    // and print number of odd pair
    echo  findOddPair($A, $N),"\n";

// This Code is Contributed by ajit   
?>
```

## java 描述语言

```
<script>
// JavaScript program to count pairs
// with XOR giving a odd number 

// Function to count number of odd pairs
function findOddPair(A, N)
{
    let i, j;

    // variable for counting odd pairs
    let oddPair = 0;

    // find all pairs
    for (i = 0; i < N; i++) {
        for (j = i + 1; j < N; j++) {

            // find XOR operation
            // check odd or even
            if ((A[i] ^ A[j]) % 2 != 0)
                oddPair++;
        }
    }

    // return number of odd pair
    return oddPair;
}

// Driver Code

    let A = [ 5, 4, 7, 2, 1 ];
    let N = A.length;

    // calling function findOddPair
    // and print number of odd pair
    document.write(findOddPair(A, N) + "<br>");

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
6
```

**时间复杂度:O(N^2)**
一个**高效的解决方案**是对偶数进行计数。然后返回计数*(N-计数)。

## C++

```
// C++ program to count pairs
// with XOR giving a odd number
#include <iostream>
using namespace std;

// Function to count number of odd pairs
int findOddPair(int A[], int N)
{
    int i, count = 0;

    // find all pairs
    for (i = 0; i < N; i++) {
        if (A[i] % 2 == 0)
            count++;
    }

    // return number of odd pair
    return count * (N - count);
}

// Driver Code
int main()
{
    int a[] = { 5, 4, 7, 2, 1 };
    int n = sizeof(a) / sizeof(a[0]);

    // calling function findOddPair
    // and print number of odd pair
    cout << findOddPair(a, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs
// with XOR giving a odd number
class GFG
{
// Function to count
// number of odd pairs
static int findOddPair(int A[],
                       int N)
{
    int i, count = 0;

    // find all pairs
    for (i = 0; i < N; i++)
    {
        if (A[i] % 2 == 0)
            count++;
    }

    // return number of odd pair
    return count * (N - count);
}

// Driver Code
public static void main(String[] arg)
{
    int a[] = { 5, 4, 7, 2, 1 };
    int n = a.length ;

    // calling function findOddPair
    // and print number of odd pair
    System.out.println(findOddPair(a, n));
}
}

// This code is contributed
// by Smitha
```

## 蟒蛇 3

```
# Python3 program to count pairs
# with XOR giving a odd number

# Function to count number of odd pairs
def findOddPair(A, N) :

    count = 0

    # find all pairs
    for i in range(0 , N) :
        if (A[i] % 2 == 0) :
            count+=1

    # return number of odd pair
    return count * (N - count)

# Driver Code
if __name__=='__main__':
    a = [5, 4, 7, 2, 1]
    n = len(a)
    print(findOddPair(a,n))

# this code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to count pairs
// with XOR giving a odd number
using System;

class GFG
{
// Function to count
// number of odd pairs
static int findOddPair(int []A,
                       int N)
{
    int i, count = 0;

    // find all pairs
    for (i = 0; i < N; i++)
    {
        if (A[i] % 2 == 0)
            count++;
    }

    // return number of odd pair
    return count * (N - count);
}

// Driver Code
public static void Main()
{
    int []a = { 5, 4, 7, 2, 1 };
    int n = a.Length ;

    // calling function findOddPair
    // and print number of odd pair
    Console.Write(findOddPair(a, n));
}
}

// This code is contributed
// by Smitha
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pairs
// with XOR giving a odd number

// Function to count number
// of odd pairs
function findOddPair($A, $N)
{
    $count = 0;

    // find all pairs
    for ($i = 0; $i < $N; $i++)
    {
        if ($A[$i] % 2 == 0)
            $count++;
    }

    // return number of odd pair
    return $count * ($N - $count);
}

// Driver Code
$a = array( 5, 4, 7, 2, 1 );
$n = count($a);

// calling function findOddPair
// and print number of odd pair
echo( findOddPair($a, $n));

// This code is contributed
// by Smitha
?>
```

## java 描述语言

```
<script>

// Javascript program to count pairs
// with XOR giving a odd number

// Function to count number of odd pairs
function findOddPair(A, N)
{
    let i, count = 0;

    // find all pairs
    for (i = 0; i < N; i++) {
        if (A[i] % 2 == 0)
            count++;
    }

    // return number of odd pair
    return count * (N - count);
}

// Driver Code
    let a = [ 5, 4, 7, 2, 1 ];
    let n = a.length;

    // calling function findOddPair
    // and print number of odd pair
    document.write(findOddPair(a, n));

</script>
```

**输出:**

```
6
```

**时间复杂度:O(N)**