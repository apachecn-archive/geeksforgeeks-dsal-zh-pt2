# 用按位“与”作为偶数计数对

> 原文:[https://www . geesforgeks . org/count-pairs-with-bitwise-and-as-偶数/](https://www.geeksforgeeks.org/count-pairs-with-bitwise-and-as-even-number/)

给定一组![N      ](img/1dfc4130ed524ab15c69922e5ff8a4dd.png "Rendered by QuickLaTeX.com")整数。任务是找到配对(I，j)的数量，使得**A【I】&A【j】**为偶数。

**示例**:

```
Input: N = 4, A[] = { 5, 1, 3, 2 }
Output: 3
Since pair of A[] are:
( 5, 1 ), ( 5, 3 ), ( 5, 2 ), ( 1, 3 ), ( 1, 2 ), ( 3, 2 )
5 AND 1 = 1, 5 AND 3 = 1, 5 AND 2 = 0,
1 AND 3 = 1, 1 AND 2 = 0,
3 AND 2 = 2
Total even pair A( i, j ) = 3

Input : N = 6, A[] = { 5, 9, 0, 6, 7, 3 }
Output : 9
Since pair of A[] =
( 5, 9 ) = 1, ( 5, 0 ) = 0, ( 5, 6 ) = 4, ( 5, 7 ) = 5, ( 5, 3 ) = 1,
( 9, 0 ) = 0, ( 9, 6 ) = 0, ( 9, 7 ) = 1, ( 9, 3 ) = 1,
( 0, 6 ) = 0, ( 0, 7 ) = 0, ( 0, 3 ) = 0,
( 6, 7 ) = 6, ( 6, 3 ) = 2,
( 7, 3 ) = 3
```

一种**天真的方法**是检查每一对并打印偶数对的计数。

下面是上述方法的实现:

## C++

```
// C++ program to count pair with
// bitwise-AND as even number

#include <iostream>
using namespace std;

// Function to count number of pairs EVEN bitwise AND
int findevenPair(int A[], int N)
{
    int i, j;

    // variable for counting even pairs
    int evenPair = 0;

    // find all pairs
    for (i = 0; i < N; i++) {
        for (j = i + 1; j < N; j++) {

            // find AND operation
            // to check evenpair
            if ((A[i] & A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return number of even pair
    return evenPair;
}

// Driver Code
int main()
{

    int a[] = { 5, 1, 3, 2 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << findevenPair(a, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pair with
// bitwise-AND as even number
import java.io.*;

class GFG
{

// Function to count number of
// pairs EVEN bitwise AND
static int findevenPair(int []A,
                        int N)
{
    int i, j;

    // variable for counting even pairs
    int evenPair = 0;

    // find all pairs
    for (i = 0; i < N; i++)
    {
        for (j = i + 1; j < N; j++)
        {

            // find AND operation
            // to check evenpair
            if ((A[i] & A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return number of even pair
    return evenPair;
}

// Driver Code
public static void main (String[] args)
{
    int []a = { 5, 1, 3, 2 };
    int n = a.length;

    System.out.println(findevenPair(a, n));
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to count pair with
# bitwise-AND as even number

# Function to count number of
# pairs EVEN bitwise AND
def findevenPair(A, N):

    # variable for counting even pairs
    evenPair = 0

    # find all pairs
    for i in range(0, N):
        for j in range(i + 1, N):

            # find AND operation to
            # check evenpair
            if ((A[i] & A[j]) % 2 == 0):
                evenPair += 1

    # return number of even pair
    return evenPair

# Driver Code
a = [ 5, 1, 3, 2 ]
n = len(a)

print(findevenPair(a, n))

# This code is contributed
# by PrinciRaj1992
```

## C#

```
// C# program to count pair with
// bitwise-AND as even number
using System;

class GFG
{

// Function to count number of
// pairs EVEN bitwise AND
static int findevenPair(int []A,
                        int N)
{
    int i, j;

    // variable for counting even pairs
    int evenPair = 0;

    // find all pairs
    for (i = 0; i < N; i++)
    {
        for (j = i + 1; j < N; j++)
        {

            // find AND operation
            // to check evenpair
            if ((A[i] & A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return number of even pair
    return evenPair;
}

// Driver Code
public static void Main ()
{
    int []a = { 5, 1, 3, 2 };
    int n = a.Length;

    Console.WriteLine(findevenPair(a, n));
}
}

// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pair with
// bitwise-AND as even number

// Function to count number of
// pairs EVEN bitwise AND
function findevenPair($A, $N)
{

    // variable for counting even pairs
    $evenPair = 0;

    // find all pairs
    for ($i = 0; $i < $N; $i++)
    {
        for ($j = $i + 1; $j < $N; $j++)
        {
            // find AND operation
            // to check evenpair
            if (($A[$i] & $A[$j]) % 2 == 0)
                $evenPair++;
        }
    }

    // return number of even pair
    return $evenPair;
}

// Driver Code
$a = array(5, 1, 3, 2 );
$n = sizeof($a);
echo findevenPair($a, $n);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
// Javascript program to count pair with
// bitwise-AND as even number

// Function to count number of pairs EVEN bitwise AND
function findevenPair(A, N)
{
    let i, j;

    // variable for counting even pairs
    let evenPair = 0;

    // find all pairs
    for (i = 0; i < N; i++) {
        for (j = i + 1; j < N; j++) {

            // find AND operation
            // to check evenpair
            if ((A[i] & A[j]) % 2 == 0)
                evenPair++;
        }
    }

    // return number of even pair
    return evenPair;
}

// Driver Code

let a = [ 5, 1, 3, 2 ];
let n = a.length;

document.write(findevenPair(a, n));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
3
```

一种有效的方法是观察两个数的按位“与”是偶数，即使两个数中至少有一个是偶数。所以，数数数组中所有的奇数说*数数*。现在，具有两个奇数元素的对的数量将是**计数*(计数-1)/2** 。

因此，至少有一个偶数元素的元素数量为:

```
Total Pairs - Count of pair with both odd elements
```

下面是上述方法的实现:

## C++

```
// C++ program to count pair with
// bitwise-AND as even number

#include <iostream>
using namespace std;

// Function to count number of pairs
// with EVEN bitwise AND
int findevenPair(int A[], int N)
{
    int count = 0;

    // count odd numbers
    for (int i = 0; i < N; i++)
        if (A[i] % 2 != 0)
            count++;

    // count odd pairs
    int oddCount = count * (count - 1) / 2;

    // return number of even pair
    return (N * (N - 1) / 2) - oddCount;
}

// Driver Code
int main()
{

    int a[] = { 5, 1, 3, 2 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << findevenPair(a, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pair with
// bitwise-AND as even number

import java.io.*;

class GFG {

// Function to count number of pairs
// with EVEN bitwise AND
static int findevenPair(int A[], int N)
{
    int count = 0;

    // count odd numbers
    for (int i = 0; i < N; i++)
        if (A[i] % 2 != 0)
            count++;

    // count odd pairs
    int oddCount = count * (count - 1) / 2;

    // return number of even pair
    return (N * (N - 1) / 2) - oddCount;
}

// Driver Code

    public static void main (String[] args) {
            int a[] = { 5, 1, 3, 2 };
    int n =a.length;

    System.out.print( findevenPair(a, n));
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to count pair with
# bitwise-AND as even number

# Function to count number of pairs
# with EVEN bitwise AND
def findevenPair(A, N):
    count = 0

    # count odd numbers
    for i in range(0, N):
        if (A[i] % 2 != 0):
            count += 1

    # count odd pairs
    oddCount = count * (count - 1) / 2

    # return number of even pair
    return (int)((N * (N - 1) / 2) - oddCount)

# Driver Code
a = [5, 1, 3, 2 ]
n = len(a)

print(findevenPair(a, n))

# This code is contributed
# by PrinciRaj1992
```

## C#

```
// C# program to count pair with
// bitwise-AND as even number

using System;

public class GFG{

// Function to count number of pairs
// with EVEN bitwise AND
static int findevenPair(int []A, int N)
{
    int count = 0;

    // count odd numbers
    for (int i = 0; i < N; i++)
        if (A[i] % 2 != 0)
            count++;

    // count odd pairs
    int oddCount = count * (count - 1) / 2;

    // return number of even pair
    return (N * (N - 1) / 2) - oddCount;
}

// Driver Code

    static public void Main (){
    int []a = { 5, 1, 3, 2 };
    int n =a.Length;
    Console.WriteLine( findevenPair(a, n));
    }
}
// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pair with
// bitwise-AND as even number

// Function to count number of pairs
// with EVEN bitwise AND
function findevenPair($A, $N)
{
    $count = 0;

    // count odd numbers
    for ($i = 0; $i < $N; $i++)
        if ($A[$i] % 2 != 0)
            $count++;

    // count odd pairs
    $oddCount = $count * ($count - 1) / 2;

    // return number of even pair
    return ($N * ($N - 1) / 2) - $oddCount;
}

// Driver Code
$a = array(5, 1, 3, 2);
$n = sizeof($a);

echo findevenPair($a, $n) . "\n";

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript program to count pair with
// bitwise-AND as even number

// Function to count number of pairs
// with EVEN bitwise AND
function findevenPair(A, N)
{
    let count = 0;

    // Count odd numbers
    for(let i = 0; i < N; i++)
        if (A[i] % 2 != 0)
            count++;

    // Count odd pairs
    let oddCount = parseInt((count *
                            (count - 1)) / 2);

    // Return number of even pair
    return parseInt((N * (N - 1)) / 2) - oddCount;
}

// Driver Code
let a = [ 5, 1, 3, 2 ];
let n = a.length;

document.write(findevenPair(a, n));

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
3
```

**时间复杂度** : O(N)