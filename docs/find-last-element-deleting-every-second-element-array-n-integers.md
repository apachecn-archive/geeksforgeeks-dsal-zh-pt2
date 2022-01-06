# 删除 n 个整数数组中的第二个元素后找到最后一个元素

> 原文:[https://www . geesforgeks . org/find-last-element-deleting-隔一秒-element-array-n-integers/](https://www.geeksforgeeks.org/find-last-element-deleting-every-second-element-array-n-integers/)

给定一个大小为 n 的循环数组，其中包含从 1 到 n 的整数。从第一个元素开始，每擦除第二个元素后，找到列表中最后一个元素。

**示例:**

```
Input: 5
Output: 3
Explanation
Element in circular array are:
1 2 3 4 5
Starting from first element i.e, '1'
delete every second element like this,
1 0 3 4 5
1 0 3 0 5
0 0 3 0 5
0 0 3 0 0
For demonstration purpose erased element
would be treated as '0'. 
Thus at the end of list, the last element
remains is 3.

Input: 10
Output: 5
```

**天真的方法**是从数组中移除每一秒的元素，直到数组的大小等于“1”。这种方法的时间复杂度为 0(n<sup>2</sup>)，这对于大的“n”值是不可行的。

有效的方法是使用递归。让我们认为 n 是偶数。在一次遍历中，数字 2，4，6 … N 将被移除，我们从 1 开始。因此，正好去掉了 n/2 个数字，我们就好像从 N/2 的数组中的 1 开始，该数组只包含奇数 1，3，5，… n/2。
因此，凭这种直觉，他们的递归公式可以写成:

```
If n is even:
  solve(n) = 2 * solve(n/2) - 1
else
  solve(n) = 2 * solve((n-1) / 2) + 1

Base condition would occur when n = 1, then
answer would be 1.
```

## C++

```
// C++ program return last number
// after removing every second
// element from circular array
#include<iostream>
using namespace std;

// Utility function to return last
// number after removing element
int removeAlternate(int n)
{
    if (n == 1)
        return 1;

    if (n % 2 == 0)
        return 2
               * removeAlternate(n / 2)
               - 1;
    else
        return 2
               * removeAlternate(((n - 1) / 2))
               + 1;
}

// Driver code
int main()
{
    int n = 5;
    cout << removeAlternate(n) << "\n";

    n = 10;
    cout << removeAlternate(n) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program return
// last number after
// removing every second
// element from circular
// array
import java.util.*;

class Circular {

    // Utility function to
    // return last number
    // number after removing
    // element
    public static int removeAlternate(int n)
    {
        if (n == 1)
            return 1;

        if (n % 2 == 0)
            return 2
                   * removeAlternate(n / 2)
                   - 1;
        else
            return 2 *
                   removeAlternate(((n - 1) / 2))
                   + 1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        System.out.print(removeAlternate(n));
        n = 10;
        System.out.print("\n" + removeAlternate(n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python program return last number
# after removing every second
# element from circular array

# Utility function to return last
# number after removing element

def removeAlternate(n):
    if (n == 1):
        return 1

    if (n % 2 == 0):
        return 2
               * removeAlternate(n / 2)
               - 1
    else:
        return 2
               * removeAlternate(((n - 1) / 2))
               + 1

# Driver code
n = 5
print(removeAlternate(n))
n = 10
print(removeAlternate(n))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program return last number after
// removing every second element from
// circular array
using System;

class Circular {

    // Utility function to return last number
    // number after removing element
    public static int removeAlternate(int n)
    {
        if (n == 1)
            return 1;

        if (n % 2 == 0)
            return 2
                   * removeAlternate(n / 2)
                   - 1;
        else
            return 2
                   * removeAlternate(((n - 1) / 2))
                   + 1;
    }

    // Driver Code
    public static void Main()
    {
        int n = 5;
        Console.WriteLine(removeAlternate(n));

        n = 10;
        Console.WriteLine(removeAlternate(n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program return last number
// after removing every second
// element from circular array

// Utility function to return last
// number after removing element
function removeAlternate($n)
{
    if ($n == 1)
        return 1;

    if ($n % 2 == 0)
        return 2 * removeAlternate($n / 2) - 1;
    else
        return 2 * removeAlternate((($n - 1) /
                                      2)) + 1;
}

    // Driver code
    $n = 5;
    echo removeAlternate($n) , "\n";
    $n = 10;
    echo removeAlternate($n) , "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

//Javascript program return last number
// after removing every second
// element from circular array

// Utility function to return last
// number after removing element
function removeAlternate(n)
{
    if (n == 1)
        return 1;

    if (n % 2 == 0)
        return 2
            * removeAlternate(n / 2)
            - 1;
    else
        return 2
            * removeAlternate(((n - 1) / 2))
            + 1;
}

// Driver code

    let n = 5;
    document.write(removeAlternate(n) + "<br>");

    n = 10;
    document.write(removeAlternate(n) + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output**

```
3
5
```

**时间复杂度:** O(log(n))
**辅助空间:** O(1)

**最另一种方法:**
另一种方法是通过观察数字重复的模式。我观察到，每当 n 值增加 1，并且该值以 2 的幂重置为“1”时，输出都是增加 2 的奇数。

例如，对于从 1 到 16 的 n 值，输出分别是 1 1 3 1 3 5 7 1 3 5 7 9 11 13 15 1。

因此，这种方法使用小于或等于给定输入的最接近的 2 次方值。

## C++

```
#include <iostream>
#include<bits/stdc++.h>
using namespace std;

// find the value nearest
// to power of 2
int nearestPowerof2(int n)
{
     int p = (int)log2(n);
     return p; 
}

// eliminate n
int circularElimination(int n)
{
    // power of 2
    int power=nearestPowerof2(n);
    int result=1+2*(n-pow(2,power));
    return result;
}

// Driver Code
int main() {

    int n=5;

    // Function call
    int result=circularElimination(n);
    cout<<result<<"\n";
    n=10;
    result=circularElimination(n);
    cout<<result<<"\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG
{
    // find the power of 2
    static int highestPowerof2(int n)
    {
        int p = (int)(Math.log(n) / Math.log(2));
        return p;
    }

    // eliminate the element n
    static int circularElimination(int n)
    {
        // power of 2
        int power = highestPowerof2(n);
        int res = 1 + 2 * (int)(n - Math.pow(2, power));
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;

        // Function call
        System.out.println(circularElimination(n));
        n = 10;
        System.out.println(circularElimination(n));
    }
}
```

## 蟒蛇 3

```
# Find the value nearest
# to power of 2
import math
def nearestPowerof2(n):

    p = int(math.log2(n))
    return p

# Eliminate n
def circularElimination(n):

    # power of 2
    power = nearestPowerof2(n);
    result = (1 + 2 *
             (n - pow(2,power)))
    return result

n = 5

# Driver code
# Function call
result = circularElimination(n)
print(result)
n = 10
result = circularElimination(n)
print(result)

# This code is contributed by divyeshrabadiya07
```

## C#

```
using System;

class GFG{

// Find the power of 2
static int highestPowerof2(int n)
{
    int p = (int)(Math.Log(n) /
                  Math.Log(2));

    return p;
}

// Eliminate the element n
static int circularElimination(int n)
{

    // Power of 2
    int power = highestPowerof2(n);
    int res = 1 + 2 * (int)(
              n - Math.Pow(2, power));

    return res;
}

// Driver Code
public static void Main(string[] args)
{
    int n = 5;

    // Function call
    Console.WriteLine(circularElimination(n));

    n = 10;

    Console.WriteLine(circularElimination(n));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
    // Find the power of 2
    function highestPowerof2(n)
    {
        let p = parseInt(Math.log(n) / Math.log(2), 10);

        return p;
    }

    // Eliminate the element n
    function circularElimination(n)
    {

        // Power of 2
        let power = highestPowerof2(n);
        let res = 1 + 2 * (n - Math.pow(2, power));

        return res;
    }

    let n = 5;

    // Function call
    document.write(circularElimination(n) + "</br>");

    n = 10;

    document.write(circularElimination(n));

</script>
```

**Output**

```
3
5
```

**时间复杂度:**O(1)
T3】空间复杂度: O(1)