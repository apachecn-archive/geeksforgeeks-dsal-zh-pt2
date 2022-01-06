# 用按位“与”作为奇数计数对

> 原文:[https://www . geesforgeks . org/count-pairs-with-bitwise-and-as-奇数/](https://www.geeksforgeeks.org/count-pairs-with-bitwise-and-as-odd-number/)

给定一个 N 个整数的数组。任务是找到配对数(I，j)，使得 A[i] & A[j]为奇数。
**例:**

> **输入:** N = 4
> A[] = { 5，1，3，2 }
> **输出:** 3
> 自对 A[] = ( 5，1)，(5，3)，(5，2)，(1，3)，(1，2)，(3，2 )
> 5 和 1 = 1，5 和 3 = 1，5 和 2 = 0，
> 1 和 3 = 1，1 和 2 = 0，
> 3 AND 2 = 2
> 总奇数对 A( i，j ) = 3
> **输入:** N = 6
> A[] = { 5，9，0，6，7，3 }
> **输出:** 6
> 自对 A[] =
> ( 5，9 ) = 1，(5，0 ) = 0，(5，6 ) = 4，(5，7 ) = 5，(5，3 ) = 1，【T29】 0 ) = 0，(9，6 ) = 0，(9，7 ) = 1，(9，3 ) = 1，
> ( 0，6 ) = 0，(0，7 ) = 0，(0，3 ) = 0，
> ( 6，7 ) = 6，(6，3 ) = 2，
> ( 7，3 ) = 3

一种**天真的方法**是检查每一对并打印对的计数。
以下是上述办法的实施情况:

## C++

```
// C++ program to count pairs
// with AND giving a odd number
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

            // find AND operation
            // check odd or even
            if ((A[i] & A[j]) % 2 != 0)
                oddPair++;
        }
    }
    // return number of odd pair
    return oddPair;
}
// Driver Code
int main()
{

    int a[] = { 5, 1, 3, 2 };
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
// with AND giving a odd number
class solution_1
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

            // find AND operation
            // check odd or even
            if ((A[i] & A[j]) % 2 != 0)
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
    int a[] = { 5, 1, 3, 2 };
    int n = a.length;

    // calling function findOddPair
    // and print number of odd pair
    System.out.println(findOddPair(a, n));
}
}

// This code is contributed
// by Arnab Kundu
```

## 计算机编程语言

```
# Python program to count pairs
# with AND giving a odd number

# Function to count number
# of odd pairs
def findOddPair(A, N):

    # variable for counting odd pairs
    oddPair = 0

    # find all pairs
    for i in range(0, N - 1):
        for j in range(i + 1, N - 1):

            # find AND operation
            # check odd or even
            if ((A[i] & A[j]) % 2 != 0):
                oddPair = oddPair + 1

    # return number of odd pair
    return oddPair

# Driver Code
a = [5, 1, 3, 2]
n = len(a)

# calling function findOddPair
# and print number of odd pair
print(findOddPair(a, n))

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to count pairs
// with AND giving a odd number
using System;
class GFG
{

// Function to count
// number of odd pairs
static int findOddPair(int []A,
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

            // find AND operation
            // check odd or even
            if ((A[i] & A[j]) % 2 != 0)
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
    int []a = { 5, 1, 3, 2 };
    int n = a.Length;

    // calling function findOddPair
    // and print number of odd pair
    Console.WriteLine(findOddPair(a, n));
}
}

// This code is contributed
// inder_verma.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pairs
// with AND giving a odd number

// Function to count
// number of odd pairs
function findOddPair(&$A, $N)
{

    // variable for counting
    // odd pairs
    $oddPair = 0;

    // find all pairs
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = $i + 1; $j < $N; $j++)
        {

            // find AND operation
            // check odd or even
            if (($A[$i] & $A[$j]) % 2 != 0)
                $oddPair = $oddPair + 1;
        }
    }

    // return number of odd pair
    return $oddPair;
}

// Driver Code
$a = array(5, 1, 3, 2);
$n = sizeof($a);

// calling function findOddPair
// and print number of odd pair
echo(findOddPair($a, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript program to count pairs
// with AND giving a odd number

// Function to count
// number of odd pairs
function findOddPair(A, N)
{
    var i, j;

    // variable for counting
    // odd pairs
    var oddPair = 0;

    // find all pairs
    for (i = 0; i < N; i++)
    {
        for (j = i + 1; j < N; j++)
        {

            // find AND operation
            // check odd or even
            if ((A[i] & A[j]) % 2 != 0)
                oddPair++;
        }
    }

    // return number
    // of odd pair
    return oddPair;
}

// Driver Code

var a = [ 5, 1, 3, 2 ];
var n = a.length;

// calling function findOddPair
// and print number of odd pair
document.write(findOddPair(a, n));

// This code is contributed by Amit Katiyar

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N^2)
一个**有效的解决方案**是对奇数进行计数。然后返回**计数*(计数–1)/2**，因为只有当两个数字中的一对都是奇数时，两个数字的“与”才能是奇数。

## C++

```
// C++ program to count pairs with Odd AND
#include <iostream>
using namespace std;

int findOddPair(int A[], int N)
{
    // Count total odd numbers in
    int count = 0;
    for (int i = 0; i < N; i++)
        if ((A[i] % 2 == 1))
            count++;

    // return count of even pair
    return count * (count - 1) / 2;
}

// Driver main
int main()
{
    int a[] = { 5, 1, 3, 2 };
    int n = sizeof(a) / sizeof(a[0]);

    // calling function findOddPair
    // and print number of odd pair
    cout << findOddPair(a, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// pairs with Odd AND
class solution_1
{
static int findOddPair(int A[],
                       int N)
{
    // Count total odd numbers in
    int count = 0;
    for (int i = 0; i < N; i++)
        if ((A[i] % 2 == 1))
            count++;

    // return count of even pair
    return count * (count - 1) / 2;
}

// Driver Code
public static void main(String args[])
{
    int a[] = { 5, 1, 3, 2 };
    int n = a.length;

    // calling function findOddPair
    // and print number of odd pair
    System.out.println(findOddPair(a, n));

}
}

// This code is contributed
// by Arnab Kundu
```

## 计算机编程语言

```
# Python program to count
# pairs with Odd AND
def findOddPair(A, N):

    # Count total odd numbers
    count = 0;
    for i in range(0, N - 1):
        if ((A[i] % 2 == 1)):
            count = count+1

    # return count of even pair
    return count * (count - 1) / 2

# Driver Code
a = [5, 1, 3, 2]
n = len(a)

# calling function findOddPair
# and print number of odd pair
print(int(findOddPair(a, n)))

# This code is contributed
# by Shivi_Aggarwal
```

## C#

```
// C# program to count
// pairs with Odd AND
using System;

class GFG
{
public static int findOddPair(int[] A,
                              int N)
{
    // Count total odd numbers in
    int count = 0;
    for (int i = 0; i < N; i++)
    {
        if ((A[i] % 2 == 1))
        {
            count++;
        }
    }

    // return count of even pair
    return count * (count - 1) / 2;
}

// Driver Code
public static void Main(string[] args)
{
    int[] a = new int[] {5, 1, 3, 2};
    int n = a.Length;

    // calling function findOddPair
    // and print number of odd pair
    Console.WriteLine(findOddPair(a, n));
}
}

// This code is contributed
// by Shrikant13
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count
// pairs with Odd AND
function findOddPair(&$A, $N)
{
    // Count total odd numbers
    $count = 0;
    for ($i = 0; $i < $N; $i++)
        if (($A[$i] % 2 == 1))
            $count++;

    // return count of even pair
    return $count * ($count - 1) / 2;
}

// Driver Code
$a = array(5, 1, 3, 2 );
$n = sizeof($a);

// calling function findOddPair
// and print number of odd pair
echo(findOddPair($a, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// JavaScript program to count pairs with Odd AND

function findOddPair( A, N)
{
    // Count total odd numbers in
    let count = 0;
    for (let i = 0; i < N; i++)
        if ((A[i] % 2 == 1))
            count++;

    // return count of even pair
    return count * (count - 1) / 2;
}

// Driver main

    let a = [ 5, 1, 3, 2 ];
    let n = a.length;

    // calling function findOddPair
    // and print number of odd pair

 document.write(findOddPair(a, n));

// This code contributed by aashish1995

</script>
```

**Output:** 

```
3
```

**时间复杂度:O(N)**