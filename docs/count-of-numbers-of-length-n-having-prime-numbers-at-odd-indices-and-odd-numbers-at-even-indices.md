# 奇数索引的素数和偶数索引的奇数的长度为 N 的数的计数

> 原文:[https://www . geeksforgeeks . org/长度为 n 的素数在奇数索引处和奇数在偶数索引处/](https://www.geeksforgeeks.org/count-of-numbers-of-length-n-having-prime-numbers-at-odd-indices-and-odd-numbers-at-even-indices/)

给定一个数 **N** ，任务是计算**长度 N** 在**奇数索引**处有**质数**的数和在**偶数索引**处有**奇数的数。**

**例**:

> **输入** : N = 1
> **输出** : 5
> **说明**:所有有效数字长度 1 都是 1、3、5、7、9，这里我们只有 1 个奇数索引，所以我们有 5 个有效数字。
> 
> **输入** : N = 2
> **输出** : 20
> **说明:**长度 2 的有效数字有 20 个。

**逼近**:借助[组合数学](https://www.geeksforgeeks.org/combinatorics-gq/)可以解决问题。奇数指数的数字有 4 个选择，偶数指数的数字有 5 个选择。
按照步骤解决问题:

*   偶数索引有 5 个选择(1，3，5，7，9)，奇数索引有 4 个选择(2，3，5，7)。
*   对于若干长度 **N、**将有 **N/2** 奇数指数和( **N/2 + N%2** 偶数指数。
*   所以，N/2 奇数指数的填充方式为**4<sup>N/2</sup>T3。**
*   偶数指数的填充方式为 **5 <sup>(N/2 + N%2)</sup>** 。
*   因此，所有有效数字的总数将为**4<sup>N/2</sup>* 5<sup>(N/2+N % 2)</sup>**。

下面是上述方法的实现:

## C++

```
// c++ program to Count of numbers of length
// N having prime numbers at odd indices and
// odd numbers at even indices
#include<bits/stdc++.h>
using namespace std;
// function to find total number of ways
int find_Numb_ways(int n)
{
    // No of odd indices in n-digit number
    int odd_indices = n/2;

    // No of even indices in n-digit number
    int even_indices = (n / 2) + (n % 2);

    //  No of ways of arranging prime number
    //  digits in odd indices
    int arr_odd = pow(4, odd_indices);

    //   No of ways of arranging odd number
    //  digits in even indices
    int arr_even = pow(5, even_indices);

    // returning the total number of ways
    return arr_odd * arr_even;
}

// drive code
int main()
{
    int n = 4;
    cout << find_Numb_ways(n) << endl;
    return 0;
}

// This code is contributed by kondamrohan02.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count of numbers of length
// N having prime numbers at odd indices and
// odd numbers at even indices
import java.util.*;

class GFG
{

// function to find total number of ways
static int find_Numb_ways(int n)
{

    // No of odd indices in n-digit number
    int odd_indices = n/2;

    // No of even indices in n-digit number
    int even_indices = (n / 2) + (n % 2);

    //  No of ways of arranging prime number
    //  digits in odd indices
    int arr_odd = (int)Math.pow(4, odd_indices);

    //   No of ways of arranging odd number
    //  digits in even indices
    int arr_even = (int)Math.pow(5, even_indices);

    // returning the total number of ways
    return arr_odd * arr_even;
}

    // Driver Code
    public static void main(String[] args) {
        int n = 4;
     System.out.print(find_Numb_ways(n));

    }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# python program for above approach
def count(N):

    # No of odd indices in N-digit number
    odd_indices = N//2

    # No of even indices in N-digit number
    even_indices = N//2 + N % 2

    # No of ways of arranging prime number
    # digits in odd indices
    arrange_odd = 4 ** odd_indices

    # No of ways of arranging odd number
    # digits in even indices
    arrange_even = 5 ** even_indices

    # returning the total number of ways
    return arrange_odd * arrange_even

# Driver code
if __name__ == "__main__":

    N = 4
    # calling the function
    print(count(N))
```

## C#

```
// C# program to Count of numbers of length
// N having prime numbers at odd indices and
// odd numbers at even indices
using System;
using System.Collections.Generic;

class GFG{

// function to find total number of ways
static int find_Numb_ways(int n)
{
    // No of odd indices in n-digit number
    int odd_indices = n/2;

    // No of even indices in n-digit number
    int even_indices = (n / 2) + (n % 2);

    //  No of ways of arranging prime number
    //  digits in odd indices
    int arr_odd = (int)Math.Pow(4, odd_indices);

    //   No of ways of arranging odd number
    //  digits in even indices
    int arr_even = (int)Math.Pow(5, even_indices);

    // returning the total number of ways
    return arr_odd * arr_even;
}

// drive code
public static void Main()
{
    int n = 4;
    Console.Write(find_Numb_ways(n));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program to Count of numbers of length
// N having prime numbers at odd indices and
// odd numbers at even indices

// function to find total number of ways
function find_Numb_ways(n)
{
    // No of odd indices in n-digit number
    var odd_indices = n/2;

    // No of even indices in n-digit number
    var even_indices = (n / 2) + (n % 2);

    //  No of ways of arranging prime number
    //  digits in odd indices
    var arr_odd = Math.pow(4, odd_indices);

    //   No of ways of arranging odd number
    //  digits in even indices
    var arr_even = Math.pow(5, even_indices);

    // returning the total number of ways
    return arr_odd * arr_even;
}

// drive code
    var n = 4;
    document.write(find_Numb_ways(n));

// This code is contributed by ipg2016107.
</script>
```

**Output**

```
400
```

**时间复杂度** : O(1)，(恒定时间操作)
**辅助空间** : O(1)，(不需要额外空间)