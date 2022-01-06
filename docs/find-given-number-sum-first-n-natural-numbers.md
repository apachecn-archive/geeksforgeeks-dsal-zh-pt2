# 判断给定的数是否是前 n 个自然数的和

> 原文:[https://www . geesforgeks . org/find-给定数字-sum-first-n-自然数/](https://www.geeksforgeeks.org/find-given-number-sum-first-n-natural-numbers/)

给定一个数字 s(1)<= s <= 1000000000). If this number is the sum of first n natural number then print, otherwise print -1. 
**举例:**

```
Input: s = 10
Output: n = 4
Explanation:
1 + 2 + 3 + 4 = 10

Input: s = 17
Output: n = -1
Explanation:
17 can't be expressed as a 
sum of consecutive from 1.
```

**方法 1(简单):**

开始把 i = 1 的数字加到 n。

*   检查总和是否等于 n，返回 I。
*   否则，如果 sum > n，返回-1。

下面是上述方法的实现:

## C++

```
// C++ program for above implementation
#include <iostream>
using namespace std;

// Function to find no. of elements
// to be added from 1 to get n
int findS(int s)
{
    int sum = 0;

    // Start adding numbers from 1
    for (int n = 1; sum < s; n++) {
        sum += n;

        // If sum becomes equal to s
        // return n
        if (sum == s)
            return n;
    }

    return -1;
}

// Drivers code
int main()
{
    int s = 15;
    int n = findS(s);
    n == -1 ? cout << "-1"
            : cout << n;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above implementation
class GFG {

    // Function to find no. of elements
    // to be added from 1 to get n
    static int findS(int s)
    {
        int sum = 0;

        // Start adding numbers from 1
        for (int n = 1; sum < s; n++)
        {
            sum += n;

            // If sum becomes equal to s
            // return n
            if (sum == s)
                return n;
        }

        return -1;
    }

    // Drivers code
    public static void main(String[]args)
    {

        int s = 15;
        int n = findS(s);
        if(n == -1)
            System.out.println("-1");
        else
            System.out.println(n);
    }
}

//This code is contributed by Azkia Anam.
```

## 蟒蛇 3

```
# Python3 program to check if
# given number is sum of first n
# natural numbers

# Function to find no. of elements
# to be added from 1 to get n
def findS (s):
    _sum = 0
    n = 1

    # Start adding numbers from 1
    while(_sum < s):
        _sum += n
        n+=1
    n-=1

    # If sum becomes equal to s
    # return n
    if _sum == s:
        return n
    return -1

# Driver code
s = 15
n = findS (s)
if n == -1:
    print("-1")
else:
    print(n)

# This code is contributed by "Abhishek Sharma 44".
```

## C#

```
// C# program for above implementation
using System;

class GFG {

    // Function to find no. of elements
    // to be added from 1 to get n
    static int findS(int s)
    {
        int sum = 0;

        // Start adding numbers from 1
        for (int n = 1; sum < s; n++)
        {
            sum += n;

            // If sum becomes equal to s
            // return n
            if (sum == s)
                return n;
        }

        return -1;
    }

    // Drivers code
    public static void Main()
    {

        int s = 15;
        int n = findS(s);

        if(n == -1)
            Console.WriteLine("-1");
        else
            Console.WriteLine(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for above implementation

// Function to find no. of elements
// to be added from 1 to get n
function findS($s)
{
    $sum = 0;

    // Start adding numbers from 1
    for ($n = 1; $sum < $s; $n++)
    {
        $sum += $n;

        // If sum becomes equal
        // to s return n
        if ($sum == $s)
            return $n;
    }

    return -1;
}

// Drivers code
$s = 15;
$n = findS($s);
if($n == -1)
echo "-1";
else
echo $n;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program for above implementation   

// Function to find no. of elements
// to be added from 1 to get n
    function findS(s) {
        var sum = 0;

        // Start adding numbers from 1
        for (n = 1; sum < s; n++) {
            sum += n;

            // If sum becomes equal to s
            // return n
            if (sum == s)
                return n;
        }

        return -1;
    }

    // Drivers code

        var s = 15;
        var n = findS(s);
        if (n == -1)
            document.write("-1");
        else
            document.write(n);

// This code is contributed by Rajput-Ji

</script>
```

**Output**

```
5
```

***时间复杂度:** O(s)* ，其中 s 是从 1 到 s 的连续数字的个数
***辅助空间:** O(1)*

**方法 2(二分搜索法):**

```
1- Initialize l = 1 and r = n / 2.
2- Apply binary search from l to r.
  a) Find mid = (l+r) / 2
  b) Find sum from 1 to mid using formula 
         mid*(mid+1)/2
  c) If sum of mid natural numbers is equal 
      to n, return mid.
  d) Else if sum > n, r = mid - 1.
  e) Else sum < n, l = mid + 1.
3- Return -1, if not possible.
```

下面是上述方法的实现:

## C++

```
// C++ program for finding s such
// that sum from 1 to s equals to n
#include <iostream>
using namespace std;

// Function to find no. of elements
// to be added to get s
int findS(int s)
{
    int l = 1, r = (s / 2) + 1;

    // Apply Binary search
    while (l <= r) {

        // Find mid
        int mid = (l + r) / 2;

        // find sum of 1 to mid natural numbers
        // using formula
        int sum = mid * (mid + 1) / 2;

        // If sum is equal to n
        // return mid
        if (sum == s)
            return mid;

        // If greater than n
        // do r = mid-1
        else if (sum > s)
            r = mid - 1;

        // else do l = mid + 1
        else
            l = mid + 1;
    }

    // If not possible, return -1
    return -1;
}

// Drivers code
int main()
{
    int s = 15;
    int n = findS(s);
    n == -1 ? cout << "-1"
            : cout << n;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for finding s such
// that sum from 1 to s equals to n
import java.io.*;

public class GFG {

    // Function to find no. of elements
    // to be added to get s
    static int findS(int s)
    {
        int l = 1, r = (s / 2) + 1;

        // Apply Binary search
        while (l <= r) {

            // Find mid
            int mid = (l + r) / 2;

            // find sum of 1 to mid natural
            // numbers using formula
            int sum = mid * (mid + 1) / 2;

            // If sum is equal to n
            // return mid
            if (sum == s)
                return mid;

            // If greater than n
            // do r = mid-1
            else if (sum > s)
                r = mid - 1;

            // else do l = mid + 1
            else
                l = mid + 1;
        }

        // If not possible, return -1
        return -1;
    }

    // Drivers code
    static public void main (String[] args)
    {
        int s = 15;
        int n = findS(s);

        if(n==-1)
            System.out.println("-1");
        else
            System.out.println(n);
    }
}

// This code is contributed by vt_m.
```

## 蟒蛇 3

```
# python program for finding s such
# that sum from 1 to s equals to n

# Function to find no. of elements
# to be added to get s
def findS(s):

    l = 1
    r = int(s / 2) + 1

    # Apply Binary search
    while (l <= r) :
        # Find mid
        mid = int((l + r) / 2)

        # find sum of 1 to mid natural numbers
        # using formula
        sum = int(mid * (mid + 1) / 2)

        # If sum is equal to n
        # return mid
        if (sum == s):
            return mid

        # If greater than n
        # do r = mid-1
        elif (sum > s):
            r = mid - 1

        # else do l = mid + 1
        else:
            l = mid + 1

    # If not possible, return -1
    return -1

s = 15
n = findS(s)
if(n == -1):
    print( "-1")
else:
    print( n )

# This code is contributed by Sam007
```

## C#

```
// C# program for finding s such
// that sum from 1 to s equals to n
using System;

public class GFG {

    // Function to find no. of elements
    // to be added to get s
    static int findS(int s)
    {
        int l = 1, r = (s / 2) + 1;

        // Apply Binary search
        while (l <= r) {

            // Find mid
            int mid = (l + r) / 2;

            // find sum of 1 to mid natural
            // numbers using formula
            int sum = mid * (mid + 1) / 2;

            // If sum is equal to n
            // return mid
            if (sum == s)
                return mid;

            // If greater than n
            // do r = mid-1
            else if (sum > s)
                r = mid - 1;

            // else do l = mid + 1
            else
                l = mid + 1;
        }

        // If not possible, return -1
        return -1;
    }

    // Drivers code
    static public void Main ()
    {
        int s = 15;
        int n = findS(s);

        if(n==-1)
            Console.WriteLine("-1");
        else
            Console.WriteLine(n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding
// s such that sum from 1
// to s equals to n

// Function to find no.
// of elements to be added
// to get s
function findS($s)
{
    $l = 1;
    $r = 1 + (int)$s / 2;

    // Apply Binary search
    while ($l <= $r)
    {

        // Find mid
        $mid = (int)(($l + $r) / 2);

        // find sum of 1 to mid natural
        // numbers using formula
        $sum = (int)($mid *
                    ($mid + 1) / 2);

        // If sum is equal to n
        // return mid
        if ($sum == $s)
            return $mid;

        // If greater than n
        // do r = mid-1
        else if ($sum > $s)
            $r = $mid - 1;

        // else do l = mid + 1
        else
            $l = $mid + 1;
    }

    // If not possible,
    // return -1
    return -1;
}

// Drivers code
$s = 15;
$n = findS($s);
if($n == -1 )
echo "-1";
else
echo $n;

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program for finding s such
// that sum from 1 to s equals to n public

    // Function to find no. of elements
    // to be added to get s
    function findS(s) {
        var l = 1, r = parseInt((s / 2) + 1);

        // Apply Binary search
        while (l <= r) {

            // Find mid
            var mid = parseInt( (l + r) / 2);

            // find sum of 1 to mid natural
            // numbers using formula
            var sum = mid * parseInt((mid + 1) / 2);

            // If sum is equal to n
            // return mid
            if (sum == s)
                return mid;

            // If greater than n
            // do r = mid-1
            else if (sum > s)
                r = mid - 1;

            // else do l = mid + 1
            else
                l = mid + 1;
        }

        // If not possible, return -1
        return -1;
    }

    // Drivers code
        var s = 15;
        var n = findS(s);

        if (n == -1)
            document.write("-1");
        else
            document.write(n);

// This code contributed by Rajput-Ji

</script>
```

**Output**

```
5
```

***时间复杂度:** O(log n)*
***辅助空间:** O(1)*

**方法三:使用数学公式**

其思想是利用前 N 个自然数之和[的公式来计算 N 的值，如下图所示:](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)

> ⇾ 1 + 2 + 3 + ….n = s
> ⇾(n *(n+1))/2 = s
> ⇾n *(n+1)= 2 * s
> ⇾n<sup>2</sup>+n–2 * s = 0

因此[检查二次方程](https://www.geeksforgeeks.org/python-program-to-solve-quadratic-equation/)的解是否等于整数。如果是，则解决方案存在。否则，给定的数不是前 N 个自然数的和。

下面是上述方法的实现:

## C++

```
// C++ program of the above
// approach

#include <bits/stdc++.h>

# define ll long long

using namespace std;

// Function to check if the
// s is the sum of first N
// natural number
ll int isvalid(ll int s)
{
    // Solution of Quadratic Equation
    float k=(-1+sqrt(1+8*s))/2;

    // Condition to check if the
    // solution is a integer
    if(ceil(k)==floor(k))
        return k;
    else
      return -1;
}

// Driver Code
int main()
{
    int s = 15;

    // Function Call
    cout<< isvalid(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above
// approach
import java.util.*;

class GFG{

// Function to check if the
// s is the sum of first N
// natural number
public static int isvalid(int s)
{

    // Solution of Quadratic Equation
    double k = (-1.0 + Math.sqrt(1 + 8 * s)) / 2;

    // Condition to check if the
    // solution is a integer
    if (Math.ceil(k) == Math.floor(k))
        return (int)k;
    else
      return -1;
}

// Driver code
public static void main(String[] args)
{
    int s = 15;

    // Function call
    System.out.print(isvalid(s));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program of the above
# approach
import math

# Function to check if the
# s is the sum of first N
# natural number
def isvalid(s):

    # Solution of Quadratic Equation
    k = (-1 + math.sqrt(1 + 8 * s)) / 2

    # Condition to check if the
    # solution is a integer
    if (math.ceil(k) == math.floor(k)):
        return int(k)
    else:
        return -1

# Driver Code
s = 15

# Function Call
print(isvalid(s))

# This code is contributed by vishu2908
```

## C#

```
// C# program of the above
// approach
using System;
class GFG{

// Function to check if the
// s is the sum of first N
// natural number
public static int isvalid(int s)
{
  // Solution of Quadratic Equation
  double k = (-1.0 + Math.Sqrt
             (1 + 8 * s)) / 2;

  // Condition to check if the
  // solution is a integer
  if (Math.Ceiling(k) ==
      Math.Floor(k))
    return (int)k;
  else
    return -1;
}

// Driver code
public static void Main(string[] args)
{
  int s = 15;

  // Function call
  Console.Write(isvalid(s));
}
}

// This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// Javascript program of the above
// approach

// Function to check if the
// s is the sum of first N
// natural number
function isvalid(s)
{

    // Solution of Quadratic Equation
    let k = (-1.0 + Math.sqrt(1 + 8 * s)) / 2;

    // Condition to check if the
    // solution is a integer
    if (Math.ceil(k) == Math.floor(k))
        return k;
    else
      return -1;
}
// Driver code

        let s = 15;

    // Function call
    document.write(isvalid(s));

</script>
```

**Output**

```
5
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)