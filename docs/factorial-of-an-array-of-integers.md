# 整数数组的阶乘

> 原文:[https://www . geesforgeks . org/整数数组阶乘/](https://www.geeksforgeeks.org/factorial-of-an-array-of-integers/)

给定一个正整数数组。任务是找到所有数组元素的阶乘。
**注**:数字会很大，用 10 <sup>9</sup> +7 取模打印出来。

**示例:**

```
Input: arr[] = {3, 10, 200, 20, 12}
Output: 6 3628800 722479105 146326063 479001600

Input: arr[] = {5, 7, 10}
Output: 120 5040 3628800 
```

**天真的方法:**我们知道有一种[简单的方法可以计算一个数的阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)。我们可以对所有数组值运行一个循环，并可以使用上述方法找到每个数字的阶乘。
**时间复杂度**将是 **O(N <sup>2</sup> )**
**空间复杂度**将是 **O(1)**

**有效方法:**我们知道一个数的阶乘:

```
N! = N*(N-1)*(N-2)*(N-3)*****3*2*1
```

计算一个数的阶乘的递归公式是:

```
fact(N) = N*fact(N-1).
```

因此，我们将使用上面的递归以自底向上的方式构建一个数组。一旦我们将值存储在数组中，我们就可以在 O(1)时间内回答查询。因此，总的时间复杂度为 0(N)。只有当数组值小于 10^6.时，我们才能使用这个方法否则，我们将无法将它们存储在数组中。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int MOD = 1000000007 ;
int SIZE = 10000;

// vector to store the factorial values
// max_element(arr) should be less than SIZE
vector<long> fact;

// Function to calculate the factorial
// using dynamic programming
void factorial()
{
    int i;
    fact.push_back((long)1);
    for (i = 1; i <= SIZE; i++)
    {

        // Calculation of factorial
        // As fact[i-1] stores the factorial of n-1
        // so factorial of n is fact[i] = (fact[i-1]*i)
        fact.push_back((fact[i - 1] * i) % MOD);
    }
}

// Function to print factorial of every element
// of the array
void PrintFactorial(int arr[],int n)
{
    for(int i = 0; i < n; i += 1)
    {

        // Printing the stored value of arr[i]!
        cout << fact[arr[i]] << " ";
    }
}

int main()
{
    int arr[] = {3, 10, 200, 20, 12};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function to store factorial values mod 10**9+7
    factorial();

    // Function to print the factorial values mod 10**9+7
    PrintFactorial(arr,n);

    return 0;
}

// This code is contributed by decode2207.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
<script>
// Java implementation of the approach
import java.util.*;

class Sol
{

static int MOD = 1000000007 ;
static int SIZE = 10000;

// vector to store the factorial values
// max_element(arr) should be less than SIZE
static Vector<Long> fact = new Vector<Long>();

// Function to calculate the factorial
// using dynamic programming
static void factorial()
{
    int i;
    fact.add((long)1);
    for (i = 1; i <= SIZE; i++)
    {

        // Calculation of factorial
        // As fact[i-1] stores the factorial of n-1
        // so factorial of n is fact[i] = (fact[i-1]*i)
        fact.add((fact.get(i - 1) * i) % MOD);
    }
}

// Function to print factorial of every element
// of the array
static void PrintFactorial(int arr[],int n)
{
    for(int i = 0; i < n; i += 1)
    {

        // Printing the stored value of arr[i]!
        System.out.print(fact.get(arr[i])+" ");
    }
}

// Driver code
public static void main(String args[])
{

    int arr[] = {3, 10, 200, 20, 12};
    int n = arr.length;

    // Function to store factorial values mod 10**9+7
    factorial();

    // Function to print the factorial values mod 10**9+7
    PrintFactorial(arr,n);
}
}

// This code is contributed by Arnab Kundu
</script>
```

## 蟒蛇 3

```
# Python implementation of the above Approach
mod = 1000000007
SIZE = 10000

# declaring list initially and making
# it 1 i.e for every index
fact = [1]*SIZE

# Calculation of factorial using Dynamic programming
def factorial():   
    for i in range(1, SIZE):    

        # Calculation of factorial
        # As fact[i-1] stores the factorial of n-1
        # so factorial of n is fact[i] = (fact[i-1]*i)       
        fact[i] = (fact[i-1]*i) % mod

# function call
factorial()

# Driver code
arr=[3,10,200,20,12]
for i in arr:
    print(fact[i])
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

$MOD = 1000000007 ;
$SIZE = 10000 ;

// Function to calculate the factorial
// using dynamic programming
function factorial($fact)
{
    $fact[0] = 1;
    for ($i = 1; $i <= $GLOBALS['SIZE']; $i++)
    {

        // Calculation of factorial
        // As fact[i-1] stores the factorial of n-1
        // so factorial of n is fact[i] = (fact[i-1]*i)
        $fact[$i] = ($fact[$i - 1] * $i) % $GLOBALS['MOD'];
    }
    return $fact;
}

// Function to print factorial of every element
// of the array
function PrintFactorial($fact, $arr, $n)
{
    for($i = 0; $i < $n; $i++)
    {

        // Printing the stored value of arr[i]!
        echo $fact[$arr[$i]]," ";
    }
}

    // Driver code
    // vector to store the factorial values
    // max_element(arr) should be less than SIZE
    $fact = array_fill(0,$SIZE + 1, 0);

    $arr = array(3, 10, 200, 20, 12);
    $n = count($arr);

    // Function to store factorial values mod 10**9+7
    $fact = factorial($fact);

    // Function to print the factorial values mod 10**9+7
    PrintFactorial($fact,$arr,$n);

    // This code is contributed by AnkitRai01
?>
```

## C#

```
// C# implementation of above approach
using System.Collections.Generic;
using System;

class Sol
{

static int MOD = 1000000007 ;
static int SIZE = 10000;

// vector to store the factorial values
// max_element(arr) should be less than SIZE
static List<long> fact = new List<long>();

// Function to calculate the factorial
// using dynamic programming
static void factorial()
{
    int i;
    fact.Add((long)1);
    for (i = 1; i <= SIZE; i++)
    {

        // Calculation of factorial
        // As fact[i-1] stores the factorial of n-1
        // so factorial of n is fact[i] = (fact[i-1]*i)
        fact.Add((fact[i - 1] * i) % MOD);
    }
}

// Function to print factorial of every element
// of the array
static void PrintFactorial(int []arr,int n)
{
    for(int i = 0; i < n; i += 1)
    {

        // Printing the stored value of arr[i]!
        Console.Write(fact[arr[i]]+" ");
    }
}

// Driver code
public static void Main(String []args)
{

    int []arr = {3, 10, 200, 20, 12};
    int n = arr.Length;

    // Function to store factorial values mod 10**9+7
    factorial();

    // Function to print the factorial values mod 10**9+7
    PrintFactorial(arr,n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
// Javascript implementation of the approach

let MOD = 1000000007;
let SIZE = 10000;

// Function to calculate the factorial
// using dynamic programming
function factorial(fact)
{
    fact[0] = 1;
    for (let i = 1; i <= SIZE; i++)
    {

        // Calculation of factorial
        // As fact[i-1] stores the factorial of n-1
        // so factorial of n is fact[i] = (fact[i-1]*i)
        fact[i] = (fact[i - 1] * i) % MOD;
    }
    return fact;
}

// Function to print factorial of every element
// of the array
function PrintFactorial(fact, arr, n)
{
    for(let i = 0; i < n; i++)
    {

        // Printing the stored value of arr[i]!
        document.write(fact[arr[i]] + " ");
    }
}

    // Driver code
    // vector to store the factorial values
    // max_element(arr) should be less than SIZE
    let fact = new Array(SIZE + 1).fill(0);

    let arr = new Array(3, 10, 200, 20, 12);
    let n = arr.length;

    // Function to store factorial values mod 10**9+7
    fact = factorial(fact);

    // Function to print the factorial values mod 10**9+7
    PrintFactorial(fact,arr,n);

    // This code is contributed by gfgking
```

**Output:** 

```
6 3628800 722479105 146326063 479001600
```

**时间复杂度**:O(N)
T3】空间复杂度 : O(N)