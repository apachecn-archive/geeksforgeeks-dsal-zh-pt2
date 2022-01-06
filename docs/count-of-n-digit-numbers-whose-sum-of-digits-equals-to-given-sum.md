# 位数总和等于给定总和的 n 位数计数

> 原文:[https://www . geesforgeks . org/n 位数计数-其位数总和等于给定总和/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-whose-sum-of-digits-equals-to-given-sum/)

给定两个整数“n”和“sum”，求所有 n 个数字的计数，数字之和为“sum”。前导 0 不计算为数字。
1<= n<= 100
1<=总和< = 500

**示例:**

```
Input:  n = 2, sum = 2
Output: 2
Explanation: Numbers are 11 and 20

Input:  n = 2, sum = 5
Output: 5
Explanation: Numbers are 14, 23, 32, 41 and 50

Input:  n = 3, sum = 6
Output: 21
```

这个想法很简单，我们从给定的和中减去从 0 到 9 的所有值，并重复求和减去那个数字。下面是递归公式。

```
    countRec(n, sum) = ∑countRec(n-1, sum-x)
                            where 0 =< x = 0

    One important observation is, leading 0's must be
    handled explicitly as they are not counted as digits.
    So our final count can be written as below.
    finalCount(n, sum) = ∑countRec(n-1, sum-x)
                           where 1 =< x = 0
```

下面是基于上述递归公式的简单递归解法。

## C++

```
// A C++ program using recursive to count numbers
// with sum of digits as given 'sum'
#include<bits/stdc++.h>
using namespace std;

// Recursive function to count 'n' digit numbers
// with sum of digits as 'sum'. This function
// considers leading 0's also as digits, that is
// why not directly called
unsigned long long int countRec(int n, int sum)
{
    // Base case
    if (n == 0)
    return sum == 0;

    if (sum == 0)
    return 1;

    // Initialize answer
    unsigned long long int ans = 0;

    // Traverse through every digit and count
    // numbers beginning with it using recursion
    for (int i=0; i<=9; i++)
    if (sum-i >= 0)
        ans += countRec(n-1, sum-i);

    return ans;
}

// This is mainly a wrapper over countRec. It
// explicitly handles leading digit and calls
// countRec() for remaining digits.
unsigned long long int finalCount(int n, int sum)
{
    // Initialize final answer
    unsigned long long int ans = 0;

    // Traverse through every digit from 1 to
    // 9 and count numbers beginning with it
    for (int i = 1; i <= 9; i++)
    if (sum-i >= 0)
        ans += countRec(n-1, sum-i);

    return ans;
}

// Driver program
int main()
{
    int n = 2, sum = 5;
    cout << finalCount(n, sum);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program using recursive to count numbers
// with sum of digits as given 'sum'
class sum_dig
{
    // Recursive function to count 'n' digit numbers
    // with sum of digits as 'sum'. This function
    // considers leading 0's also as digits, that is
    // why not directly called
    static int countRec(int n, int sum)
    {
        // Base case
        if (n == 0)
        return sum == 0 ?1:0;

            if (sum == 0)
            return 1;

        // Initialize answer
        int ans = 0;

        // Traverse through every digit and count
        // numbers beginning with it using recursion
        for (int i=0; i<=9; i++)
        if (sum-i >= 0)
            ans += countRec(n-1, sum-i);

        return ans;
    }

    // This is mainly a wrapper over countRec. It
    // explicitly handles leading digit and calls
    // countRec() for remaining digits.
    static int finalCount(int n, int sum)
    {
        // Initialize final answer
        int ans = 0;

        // Traverse through every digit from 1 to
        // 9 and count numbers beginning with it
        for (int i = 1; i <= 9; i++)
        if (sum-i >= 0)
            ans += countRec(n-1, sum-i);

        return ans;
    }

    /* Driver program to test above function */
    public static void main (String args[])
    {
        int n = 2, sum = 5;
        System.out.println(finalCount(n, sum));
    }
}/* This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# A python 3 program using recursive to count numbers
# with sum of digits as given 'sum'

# Recursive function to count 'n' digit
# numbers with sum of digits as 'sum'
# This function considers leading 0's
# also as digits, that is why not
# directly called
def countRec(n, sum) :

    # Base case
    if (n == 0) :
        return (sum == 0)

    if (sum == 0) :
        return 1

    # Initialize answer
    ans = 0

    # Traverse through every digit and
    # count numbers beginning with it
    # using recursion
    for i in range(0, 10) :
        if (sum-i >= 0) :
            ans = ans + countRec(n-1, sum-i)

    return ans

# This is mainly a wrapper over countRec. It
# explicitly handles leading digit and calls
# countRec() for remaining digits.
def finalCount(n, sum) :

    # Initialize final answer
    ans = 0

    # Traverse through every digit from 1 to
    # 9 and count numbers beginning with it
    for i in range(1, 10) :
        if (sum-i >= 0) :
            ans = ans + countRec(n-1, sum-i)

    return ans

# Driver program
n = 2
sum = 5
print(finalCount(n, sum))

# This code is contributed by Nikita tiwari.
```

## C#

```
// A C# program using recursive to count numbers
// with sum of digits as given 'sum'
using System;
class GFG {

    // Recursive function to
    // count 'n' digit numbers
    // with sum of digits as
    // 'sum'. This function
    // considers leading 0's
    // also as digits, that is
    // why not directly called
    static int countRec(int n, int sum)
    {

        // Base case
        if (n == 0)
        return sum == 0 ? 1 : 0;

            if (sum == 0)
            return 1;

        // Initialize answer
        int ans = 0;

        // Traverse through every
        // digit and count numbers
        // beginning with it using
        // recursion
        for (int i = 0; i <= 9; i++)
        if (sum - i >= 0)
            ans += countRec(n - 1, sum - i);

        return ans;
    }

    // This is mainly a
    // wrapper over countRec. It
    // explicitly handles leading
    // digit and calls countRec()
    // for remaining digits.
    static int finalCount(int n, int sum)
    {

        // Initialize final answer
        int ans = 0;

        // Traverse through every
        // digit from 1 to 9 and
        // count numbers beginning
        // with it
        for (int i = 1; i <= 9; i++)
        if (sum - i >= 0)
            ans += countRec(n - 1, sum - i);

        return ans;
    }

    // Driver Code
    public static void Main ()
    {
        int n = 2, sum = 5;
        Console.Write(finalCount(n, sum));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program using recursive to count numbers
// with sum of digits as given 'sum'

// Recursive function to count 'n' digit numbers
// with sum of digits as 'sum'. This function
// considers leading 0's also as digits, that is
// why not directly called
function countRec($n, $sum)
{

    // Base case
    if ($n == 0)
    return $sum == 0;

    if ($sum == 0)
    return 1;

    // Initialize answer
    $ans = 0;

    // Traverse through every
    // digit and count
    // numbers beginning with
    // it using recursion
    for ($i = 0; $i <= 9; $i++)
    if ($sum-$i >= 0)
        $ans += countRec($n-1, $sum-$i);

    return $ans;
}

// This is mainly a wrapper
// over countRec. It
// explicitly handles leading
// digit and calls
// countRec() for remaining digits.
function finalCount($n, $sum)
{

    // Initialize final answer
    $ans = 0;

    // Traverse through every
    // digit from 1 to
    // 9 and count numbers
    // beginning with it
    for ($i = 1; $i <= 9; $i++)
    if ($sum - $i >= 0)
        $ans += countRec($n - 1, $sum - $i);

    return $ans;
}

    // Driver Code
    $n = 2;
    $sum = 5;
    echo finalCount($n, $sum);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// A JavaScript program using
// recursive to count numbers 
// with sum of digits as given 'sum'

    // Recursive function to
    // count 'n' digit numbers
    // with sum of digits as 'sum'.
    //This function
    // considers leading 0's also as digits,
    //that is why not directly called
    function countRec(n, sum) {
        // Base case
        if (n == 0)
            return sum == 0;

        if (sum == 0)
            return 1;

        // Initialize answer
        let ans = 0;

    // Traverse through every
    // digit and count
    // numbers beginning with
    // it using recursion
        for (let i = 0; i <= 9; i++) {
            if (sum - i >= 0)
                ans += countRec(n - 1, sum - i);
        }
           return ans;
    }

    // This is mainly a wrapper over countRec.
    // It explicitly handles leading digit 
    // and calls countRec() for remaining digits.
    function finalCount(n, sum) {
        // Initialize final answer
        let ans = 0;

        // Traverse through every digit from 1 to
        // 9 and count numbers beginning with it
        for (let i = 1; i <= 9; i++) {
            if (sum - i >= 0)
                ans += countRec(n - 1, sum - i);
        }

         return ans;
    }

    // Driver program
    let n = 2, sum = 5;
    document.write(finalCount(n, sum));

//This code is contributed by Surbhi Tyagi
</script>
```

**输出:**

```
5
```

上述解的时间复杂度是指数的。如果我们画出完整的递归树，我们可以观察到许多子问题被一次又一次地解决。例如，如果我们从 n = 3 和 sum = 10 开始，通过考虑数字序列 1，1 或 2，0，我们可以达到 n = 1，sum = 8。
由于相同的子问题被再次调用，该问题具有重叠子问题的性质。所以最小二乘和问题同时具有动态规划问题的两个性质(参见[这个](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[这个](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/))。

下面是基于内存化的实现。

## C++

```
// A C++ memoization based recursive program to count
// numbers with sum of n as given 'sum'
#include<bits/stdc++.h>
using namespace std;

// A lookup table used for memoization
unsigned long long int lookup[101][501];

// Memoization based implementation of recursive
// function
unsigned long long int countRec(int n, int sum)
{
    // Base case
    if (n == 0)
    return sum == 0;

    // If this subproblem is already evaluated,
    // return the evaluated value
    if (lookup[n][sum] != -1)
    return lookup[n][sum];

    // Initialize answer
    unsigned long long int ans = 0;

    // Traverse through every digit and
    // recursively count numbers beginning
    // with it
    for (int i=0; i<10; i++)
    if (sum-i >= 0)
        ans += countRec(n-1, sum-i);

    return lookup[n][sum] = ans;
}

// This is mainly a wrapper over countRec. It
// explicitly handles leading digit and calls
// countRec() for remaining n.
unsigned long long int finalCount(int n, int sum)
{
    // Initialize all entries of lookup table
    memset(lookup, -1, sizeof lookup);

    // Initialize final answer
    unsigned long long int ans = 0;

    // Traverse through every digit from 1 to
    // 9 and count numbers beginning with it
    for (int i = 1; i <= 9; i++)
    if (sum-i >= 0)
        ans += countRec(n-1, sum-i);
    return ans;
}

// Driver program
int main()
{
    int n = 3, sum = 5;
    cout << finalCount(n, sum);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java memoization based recursive program to count
// numbers with sum of n as given 'sum'
class sum_dig
{
    // A lookup table used for memoization
    static int lookup[][] = new int[101][501];

    // Memoization based implementation of recursive
    // function
    static int countRec(int n, int sum)
    {
        // Base case
        if (n == 0)
        return sum == 0 ? 1 : 0;

        // If this subproblem is already evaluated,
        // return the evaluated value
        if (lookup[n][sum] != -1)
        return lookup[n][sum];

        // Initialize answer
        int ans = 0;

        // Traverse through every digit and
        // recursively count numbers beginning
        // with it
        for (int i=0; i<10; i++)
        if (sum-i >= 0)
            ans += countRec(n-1, sum-i);

        return lookup[n][sum] = ans;
    }

    // This is mainly a wrapper over countRec. It
    // explicitly handles leading digit and calls
    // countRec() for remaining n.
    static int finalCount(int n, int sum)
    {
        // Initialize all entries of lookup table
        for(int i = 0; i <= 100; ++i){
            for(int j = 0; j <= 500; ++j){
                lookup[i][j] = -1;
            }
        }

        // Initialize final answer
        int ans = 0;

        // Traverse through every digit from 1 to
        // 9 and count numbers beginning with it
        for (int i = 1; i <= 9; i++)
        if (sum-i >= 0)
            ans += countRec(n-1, sum-i);
        return ans;
    }

    /* Driver program to test above function */
    public static void main (String args[])
    {
        int n = 3, sum = 5;
        System.out.println(finalCount(n, sum));
    }
}/* This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# A Python3 memoization based recursive
# program to count numbers with Sum of n
# as given 'Sum'

# A lookup table used for memoization
lookup = [[-1 for i in range(501)]
              for i in range(101)]

# Memoization based implementation
# of recursive function
def countRec(n, Sum):

    # Base case
    if (n == 0):
        return Sum == 0

    # If this subproblem is already evaluated,
    # return the evaluated value
    if (lookup[n][Sum] != -1):
        return lookup[n][Sum]

    # Initialize answer
    ans = 0

    # Traverse through every digit and
    # recursively count numbers beginning
    # with it
    for i in range(10):
        if (Sum-i >= 0):
            ans += countRec(n - 1, Sum-i)
    lookup[n][Sum] = ans    

    return lookup[n][Sum]

# This is mainly a wrapper over countRec. It
# explicitly handles leading digit and calls
# countRec() for remaining n.
def finalCount(n, Sum):

    # Initialize final answer
    ans = 0

    # Traverse through every digit from 1 to
    # 9 and count numbers beginning with it
    for i in range(1, 10):
        if (Sum - i >= 0):
            ans += countRec(n - 1, Sum - i)
    return ans

# Driver Code
n, Sum = 3, 5
print(finalCount(n, Sum))

# This code is contributed by mohit kumar 29
```

## C#

```
// A C# memoization based recursive program to count
// numbers with sum of n as given 'sum'

using System;
class sum_dig
{
    // A lookup table used for memoization
    static int [,]lookup = new int[101,501];

    // Memoization based implementation of recursive
    // function
    static int countRec(int n, int sum)
    {
        // Base case
        if (n == 0)
        return sum == 0 ? 1 : 0;

        // If this subproblem is already evaluated,
        // return the evaluated value
        if (lookup[n,sum] != -1)
        return lookup[n,sum];

        // Initialize answer
        int ans = 0;

        // Traverse through every digit and
        // recursively count numbers beginning
        // with it
        for (int i=0; i<10; i++)
        if (sum-i >= 0)
            ans += countRec(n-1, sum-i);

        return lookup[n,sum] = ans;
    }

    // This is mainly a wrapper over countRec. It
    // explicitly handles leading digit and calls
    // countRec() for remaining n.
    static int finalCount(int n, int sum)
    {
        // Initialize all entries of lookup table
        for(int i = 0; i <= 100; ++i){
            for(int j = 0; j <= 500; ++j){
                lookup[i,j] = -1;
            }
        }

        // Initialize final answer
        int ans = 0;

        // Traverse through every digit from 1 to
        // 9 and count numbers beginning with it
        for (int i = 1; i <= 9; i++)
        if (sum-i >= 0)
            ans += countRec(n-1, sum-i);
        return ans;
    }

    /* Driver program to test above function */
    public static void Main ()
    {
        int n = 3, sum = 5;
        Console.Write(finalCount(n, sum));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP memoization based recursive program
// to count numbers with sum of n as given 'sum'

// A lookup table used for memoization
$lookup = array_fill(0, 101,
          array_fill(0, 501, -1));

// Memoization based implementation
// of recursive function
function countRec($n, $sum)
{
    global $lookup;

    // Base case
    if ($n == 0)
    return $sum == 0;

    // If this subproblem is already evaluated,
    // return the evaluated value
    if ($lookup[$n][$sum] != -1)
    return $lookup[$n][$sum];

    // Initialize answer
    $ans = 0;

    // Traverse through every digit and
    // recursively count numbers beginning
    // with it
    for ($i = 0; $i < 10; $i++)
    if ($sum - $i >= 0)
        $ans += countRec($n - 1, $sum - $i);

    return $lookup[$n][$sum] = $ans;
}

// This is mainly a wrapper over countRec. It
// explicitly handles leading digit and calls
// countRec() for remaining n.
function finalCount($n, $sum)
{
    // Initialize all entries of lookup table

    // Initialize final answer
    $ans = 0;

    // Traverse through every digit from 1 to
    // 9 and count numbers beginning with it
    for ($i = 1; $i <= 9; $i++)
    if ($sum-$i >= 0)
        $ans += countRec($n - 1, $sum - $i);
    return $ans;
}

// Driver Code
$n = 3;
$sum = 5;
echo finalCount($n, $sum);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// A Javascript memoization based
// recursive program to count numbers
// with sum of n as given 'sum'

// A lookup table used for memoization
let lookup = new Array(101);

// Memoization based implementation
// of recursive function
function countRec(n, sum)
{

    // Base case
    if (n == 0)
        return sum == 0 ? 1 : 0;

    // If this subproblem is already evaluated,
    // return the evaluated value
    if (lookup[n][sum] != -1)
        return lookup[n][sum];

    // Initialize answer
    let ans = 0;

    // Traverse through every digit and
    // recursively count numbers beginning
    // with it
    for(let i = 0; i < 10; i++)
        if (sum - i >= 0)
            ans += countRec(n - 1, sum - i);

    return lookup[n][sum] = ans;
}

// This is mainly a wrapper over countRec. It
// explicitly handles leading digit and calls
// countRec() for remaining n.
function finalCount(n, sum)
{

    // Initialize all entries of lookup table
    for(let i = 0; i < 101; i++)
    {  
        lookup[i] = new Array(501);
        for(let j = 0; j < 501; j++)
        {
            lookup[i][j] = -1;
        }
    }

    // Initialize final answer
    let ans = 0;

    // Traverse through every digit from 1 to
    // 9 and count numbers beginning with it
    for(let i = 1; i <= 9; i++)
        if (sum - i >= 0)
            ans += countRec(n - 1, sum - i);

    return ans;
}

// Driver code
let n = 3, sum = 5;

document.write(finalCount(n, sum));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
15
```

感谢 Gaurav Ahirwar 提出上述解决方案。

**另一种方法**
我们可以通过迭代所有 n 个数字，检查当前 n 个数字的和是否等于给定的和，很容易地计算出 n 个数字的和等于给定的和，如果是，那么我们将从 9 开始增加数字，直到它达到数字的和大于给定的和的数字，然后我们将再次增加 1，直到我们找到另一个具有给定和的数字。

## C++

```
// C++ program to Count of n digit numbers
// whose sum of digits equals to given sum
#include <bits/stdc++.h>
#include <iostream>
using namespace std;
 void findCount(int n, int sum) {

        //in case n = 2 start is 10 and end is (100-1) = 99
        int start = pow(10, n-1);
        int end = pow(10, n)-1;

        int count = 0;
        int i = start;

                while(i <= end) {

            int cur = 0;
            int temp = i;

            while( temp != 0) {
                cur += temp % 10;
                temp = temp / 10;
            }

            if(cur == sum) {            
                count++;            
                i += 9;        
            }else
                i++;

        }    
            cout << count;

        /* This code is contributed by Anshuman */
    }
int main() {
        int n = 3;
        int sum = 5;    
        findCount(n,sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Count of n digit numbers
// whose sum of digits equals to given sum

public class GFG {

    public static void main(String[] args) {

        int n = 3;
        int sum = 5;    
        findCount(n,sum);

    }

    private static void findCount(int n, int sum) {

        //in case n = 2 start is 10 and end is (100-1) = 99
        int start = (int) Math.pow(10, n-1);
        int end = (int) Math.pow(10, n)-1;

        int count = 0;
        int i = start;

                while(i < end) {

            int cur = 0;
            int temp = i;

            while( temp != 0) {
                cur += temp % 10;
                temp = temp / 10;
            }

            if(cur == sum) {            
                count++;            
                i += 9;        
            }else
                i++;

        }    
        System.out.println(count);

        /* This code is contributed by Anshuman */
    }
}
```

## 蟒蛇 3

```
# Python3 program to Count of n digit numbers
# whose sum of digits equals to given sum
import math

def findCount(n, sum):

    # in case n = 2 start is 10 and
    # end is (100-1) = 99
    start = math.pow(10, n - 1);
    end = math.pow(10, n) - 1;

    count = 0;
    i = start;

    while(i <= end):

        cur = 0;
        temp = i;

        while(temp != 0):
            cur += temp % 10;
            temp = temp // 10;

        if(cur == sum):    
            count = count + 1;        
            i += 9;    
        else:
            i = i + 1;

    print(count);

# Driver Code
n = 3;
sum = 5;    
findCount(n, sum);

# This code is contributed
# by Akanksha Rai
```

## C#

```
// C# program to Count of n digit numbers
// whose sum of digits equals to given sum
using System;

class GFG
{
private static void findCount(int n,
                              int sum)
{

    // in case n = 2 start is 10 and
    // end is (100-1) = 99
    int start = (int) Math.Pow(10, n - 1);
    int end = (int) Math.Pow(10, n) - 1;

    int count = 0;
    int i = start;

    while(i < end)
    {

        int cur = 0;
        int temp = i;

        while( temp != 0)
        {
            cur += temp % 10;
            temp = temp / 10;
        }

        if(cur == sum)
        {        
            count++;            
            i += 9;    
        }
        else
            i++;

    }
    Console.WriteLine(count);
}

// Driver Code
public static void Main()
{
    int n = 3;
    int sum = 5;    
    findCount(n,sum);
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to Count of n digit numbers
// whose sum of digits equals to given sum

function findCount($n, $sum)
{

// In case n = 2 start is 10 and
// end is (100-1) = 99
$start = (int)pow(10, $n - 1);
$end = (int)pow(10, $n) - 1;

$count = 0;
$i = $start;

while($i < $end)
{

    $cur = 0;
    $temp = $i;

    while( $temp != 0)
    {
        $cur += $temp % 10;
        $temp = (int) $temp / 10;
    }

    if($cur == $sum)
    {        
        $count++;        
        $i += 9;        
    }
    else
        $i++;

}
echo ($count);
}

// Driver Code
$n = 3;
$sum = 5;
findCount($n,$sum);

// This code is contributed
// by jit_t
?>
```

## java 描述语言

```
<script>

// Javascript program to Count of n digit numbers
// whose sum of digits equals to given sum
 function findCount(n, sum) {

        // in case n = 2 start is 10 and end is (100-1) = 99
        let start = Math.pow(10, n-1);
        let end = Math.pow(10, n)-1;

        let count = 0;
        let i = start;

        while(i <= end)
        {

            let cur = 0;
            let temp = i;

            while( temp != 0)
            {
                cur += temp % 10;
                temp = parseInt(temp / 10);
            }

            if(cur == sum)
            {            
                count++;            
                i += 9;        
            }else
                i++;

        }    
            document.write(count);
    }
        let n = 3;
        let sum = 5;    
        findCount(n,sum);

// This code is contributed by souravmahato348.
</script>
```

**输出:**

```
15
```

**时间复杂度:** O(sum)
**空间复杂度:** O(1)
如有不正确的地方请写评论，或者想分享以上讨论话题的更多信息