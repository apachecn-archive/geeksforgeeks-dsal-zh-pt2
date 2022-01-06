# 利用模 3 下的增量均衡数组

> 原文:[https://www . geeksforgeeks . org/均衡-数组-使用-增量-低于-模-3/](https://www.geeksforgeeks.org/equalizing-array-using-increment-under-modulo-3/)

给定一个包含 N 个非负整数的数组 A。只能对数组执行以下操作:
**A[i] = ( A[i] + 1 ) % 3**
其中 A[i]是索引 I 处数组 A 的元素，执行此操作一次花费 1 个单位。找到使所有元素相等的最小成本。

**示例:**

```
Input : 1 0 3 2
Output : 4 units
Explanation: First 3 is converted to 1(3 + 1 % 3 = 1). 
Then, if we try to make all elements equal to 1, then
converting 0 to 1 will cost "1" and 2 to 1 will cost "2". 
Therefore, in total cost=3 + 1(to convert 3 to 1) = 4, 
which is minimum.  

Input : 98 4 3 1
Output : 6 units
Explanation: 98, 4 and 3 are converted to 0, 2 and 1.
So, now array becomes {0, 2, 1, 1}. If we try to convert
every element in our new array equal to 1, then converting
0 to 1 will cost "1" and 2 to 1 will cost "2". So, total
cost= 3+ 3(conversion of 98, 4 and 3) = 6, which is the minimum cost.
```

**逼近**:首先我们尝试将所有大于 2 的数字转换成 0 到 2 之间的数字。因为，使用唯一允许的运算 A(i)=(A(i)+1) % 3，从 0 到 2 的数字不会超过 2(无论我们做这个运算多少次)。然后，我们将固定 3 个可能值中的一个(0 到 2)，并找到使所有元素等于它的成本。

三个中的最小成本+将所有大于 2 的数字转换为 0 到 2 之间的数字的额外成本将是我们的答案。这里我们需要看的一个特殊情况是，如果所有元素在默认情况下是相等的(就像在数组{7，7，7，7}中)，那么我们的答案将是零。

## C++

```
// CPP program to find minimum cost to
// equalize an array with increment under
// modulo 3 operation.
#include <bits/stdc++.h>
using namespace std;

int mincost(int a[], int n)
{
    int c = 1;

    // loop to check whether all
    // elements are equal or not
    for (int i = 0; i < n; i++)
        if (a[i] == a[i + 1])
            c++;

    // A special case when all
    // elements are equal
    if (c == n)
        return 0;

    // variable that counts total
    // numbers greater 2
    int x = 0;

    // loop to convert all numbers greater
    // than 2 to a range between 0 to 2.
    for (int i = 0; i < n; i++)
    {
        if (a[i] > 2) {

            // number greater than 2 gets
            // converted to a number between 0 to 2.
            a[i] = (a[i] + 1) % 3;
            x += 1;
        }
    }

    // variables to count 3 possible ways
    // to make all elements equal after
    // reducing them to range [0, 2]
    int c0 = 0, c1 = 0, c2 = 0;

    // loop that counts total cost to
    // make all elements equal to 0.
    for (int i = 0; i < n; i++)
    {
        if (a[i] == 1) {

            // since we will have to use the
            // operation 2 times to convert 1 to 0
            // (1+1)%3=2 and then (2+1)%3=0
            c0 += 2;
        }

        // here we use it once since (2+1%3=0)       
        else if (a[i] == 2)
            c0 += 1;
    }

    // loop that counts total cost to
    // make all elements equal to 1
    for (int i = 0; i < n; i++)
    {
        // since (2+1%3=0) and (0+1%3=1)
        if (a[i] == 2)
            c1 += 2;

        // since (0+1%3=1)
        else if (a[i] == 0)   
            c1 += 1;
    }

    // loop that counts total cost
    // to make all elements equal to 2
    for (int i = 0; i < n; i++) {

        // since 0+1%3=1 and 1+1%3=2
        if (a[i] == 0)
            c2 += 2;       
        else if (a[i] == 1)
            c2 += 1;        
    }

    // finally the one with minimum
    // cost will be our answer
    return x + min({ c0, c1, c2 });
}

// Driver program to run above function
int main()
{
    int a[] = { 98, 4, 3, 1 };
    int n = sizeof(a)/sizeof(a[0]);
    cout << mincost(a, n)<<" units";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// cost to equalize an array
// with increment under
// modulo 3 operation.
import java.io.*;

class GFG
{

// Function to find minimum cost
static int mincost(int a[], int n)
{
    int c = 1;

    // loop to check whether all
    // elements are equal or not
    for (int i = 0; i < n - 1; i++)
        if (a[i] == a[i + 1])
            c++;

    // A special case when all
    // elements are equal
    if (c == n)
        return 0;

    // variable that counts total
    // numbers greater 2
    int x = 0;

    // loop to convert all numbers
    // greater than 2 to a range
    // between 0 to 2.
    for (int i = 0; i < n - 1; i++)
    {
        if (a[i] > 2)
        {

            // number greater than 2
            // gets converted to a
            // number between 0 to 2.
            a[i] = (a[i] + 1) % 3;
            x += 1;
        }
    }

    // variables to count 3 possible
    // ways to make all elements equal
    // after reducing them to range [0, 2]
    int c0 = 0, c1 = 0, c2 = 0;

    // loop that counts total cost to
    // make all elements equal to 0.
    for (int i = 0; i < n - 1; i++)
    {
        if (a[i] == 1)
        {

            // since we will have to
            // use the operation 2
            // times to convert 1 to 0
            // (1+1)%3=2 and then (2+1)%3=0
            c0 += 2;
        }

        // here we use it
        // once since (2+1%3=0)
        else if (a[i] == 2)
            c0 += 1;
    }

    // loop that counts total cost to
    // make all elements equal to 1
    for (int i = 0; i < n - 1; i++)
    {
        // since (2+1%3=0)
        // and (0+1%3=1)
        if (a[i] == 2)
            c1 += 2;

        // since (0+1%3=1)
        else if (a[i] == 0)
            c1 += 1;
    }

    // loop that counts total cost
    // to make all elements equal to 2
    for (int i = 0; i < n - 1; i++)
    {

        // since 0+1%3=1
        // and 1+1%3=2
        if (a[i] == 0)
            c2 += 2;    
        else if (a[i] == 1)
            c2 += 1;        
    }

    // finally the one with minimum
    // cost will be our answer
    return x + Math.min(c0,
               Math.min(c1, c2));
}

// Driver Code
public static void main (String[] args)
{
    int a[] = new int[]{98, 4, 3, 1};
    int n = a.length;
    System.out.println(mincost(a, n) +
                       " " + "units");
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python code to illustrate above approach
# function to calculate minimum cost
def mincost(a, n):

    # loop to check whether all elements
    # are equal or not
    c = 1
    for i in range(0, n-1):
        if (a[i] == a[i + 1]):
            c += 1

    # A special case when all elements
    # are equal
    if (c == n):
        return 0

    # loop to count total no of conversion
    # of numbers greater than 2 to a
    # number between 0 to 2.
    x = 0
    for i in range(n):
        if a[i]>2:
            a[i]=(a[i]+1)% 3
            x += 1

    # variables to count 3 possible ways
    # to make all elements equal after
    # reducing them to range [0, 2]
    c0 = c1 = c2 = 0   

    # loop that counts total cost to
    # make all elements equal to 0.
    for i in a:
        if (i == 1):
            c0+= 2
        elif (i == 2):
            c0+= 1

    # loop that counts total cost to
    # make all elements equal to 1.    
    for i in a:
        if (i == 0):
            c1+= 1
        elif (i == 2):
            c1+= 2

    # loop that counts total cost to
    # make all elements equal to 2.
    for i in a:
        if (i == 0):
            c2+= 2
        elif (i == 1):
            c2+= 1

    # finally the one with minimum cost
    # plus the extra cost to convert numbers
    # greater than 2 will be our answer
    return min(c1, c2, c0)+x

# Driver code
n = 4
a = [98, 4, 3, 1]
c = 1
print(mincost(a, n), "units")
```

## C#

```
// C# program to find minimum cost to
// equalize an array with increment
// under modulo 3 operation.
using System;

class GFG {

// Function to find minimum cost   
static int mincost(int []a, int n)
{
    int c = 1;

    // loop to check whether all
    // elements are equal or not
    for (int i = 0; i < n - 1; i++)
        if (a[i] == a[i + 1])
            c++;

    // A special case when all
    // elements are equal
    if (c == n)
        return 0;

    // variable that counts total
    // numbers greater 2
    int x = 0;

    // loop to convert all numbers greater
    // than 2 to a range between 0 to 2.
    for (int i = 0; i < n - 1; i++)
    {
        if (a[i] > 2) {

            // number greater than 2 gets
            // converted to a number
            // between 0 to 2.
            a[i] = (a[i] + 1) % 3;
            x += 1;
        }
    }

    // variables to count 3 possible ways
    // to make all elements equal after
    // reducing them to range [0, 2]
    int c0 = 0, c1 = 0, c2 = 0;

    // loop that counts total cost to
    // make all elements equal to 0.
    for (int i = 0; i < n - 1; i++)
    {
        if (a[i] == 1)
        {

            // since we will have to use the
            // operation 2 times to convert 1 to 0
            // (1+1)%3=2 and then (2+1)%3=0
            c0 += 2;
        }

        // here we use it once since (2+1%3=0)    
        else if (a[i] == 2)
            c0 += 1;
    }

    // loop that counts total cost to
    // make all elements equal to 1
    for (int i = 0; i < n - 1; i++)
    {
        // since (2+1%3=0) and (0+1%3=1)
        if (a[i] == 2)
            c1 += 2;

        // since (0+1%3=1)
        else if (a[i] == 0)
            c1 += 1;
    }

    // loop that counts total cost
    // to make all elements equal to 2
    for (int i = 0; i < n - 1; i++)
    {

        // since 0+1%3=1 and 1+1%3=2
        if (a[i] == 0)
            c2 += 2;    
        else if (a[i] == 1)
            c2 += 1;        
    }

    // finally the one with minimum
    // cost will be our answer
    return x + Math.Min(c0,
               Math.Min(c1, c2) );
}

// Driver Code
public static void Main()
{
        int []a = new int[]{98, 4, 3, 1};
        int n = a.Length;
        Console.Write(mincost(a, n) +
                      " " + "units");

}
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// cost to equalize an array
// with increment under modulo
// 3 operation.
function mincost($a, $n)
{
    $c = 1;

    // loop to check whether all
    // elements are equal or not
    for ($i = 0; $i < $n; $i++)
            $c++;

    // A special case when all
    // elements are equal
    if ($c == $n)
        return 0;

    // variable that counts
    // total numbers greater 2
    $x = 0;

    // loop to convert all
    // numbers greater than 2
    // to a range between 0 to 2.
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] > 2)
        {

            // number greater than 2
            // gets converted to a
            // number between 0 to 2.
            $a[$i] = ($a[$i] + 1) % 3;
            $x += 1;
        }
    }

    // variables to count 3
    // possible ways to make
    // all elements equal after
    // reducing them to range [0, 2]
    $c0 = 0; $c1 = 0; $c2 = 0;

    // loop that counts total
    // cost to make all elements
    // equal to 0.
    for ($i = 0; $i < $n; $i++)
    {
        if ($a[$i] == 1)
        {

            // since we will have to
            // use the operation 2
            // times to convert 1 to 0
            // (1+1)%3=2 and then (2+1)%3=0
            $c0 += 2;
        }

        // here we use it
        // once since (2+1%3=0)
        else if ($a[$i] == 2)
            $c0 += 1;
    }

    // loop that counts total
    // cost to make all
    // elements equal to 1
    for ($i = 0; $i < $n; $i++)
    {
        // since (2+1%3=0) and
        // (0+1%3=1)
        if ($a[$i] == 2)
            $c1 += 2;

        // since (0+1%3=1)
        else if ($a[$i] == 0)
            $c1 += 1;
    }

    // loop that counts total
    // cost to make all
    // elements equal to 2
    for ($i = 0; $i < $n; $i++)
    {

        // since 0+1%3=1
        // and 1+1%3=2
        if ($a[$i] == 0)
            $c2 += 2;
        else if ($a[$i] == 1)
            $c2 += 1;    
    }

    // finally the one with
    // minimum cost will
    // be our answer
    return $x + min($c0, $c1, $c2 );
}

// Driver Code
$a = array(98, 4, 3, 1);
$n = sizeof($a);
echo mincost($a, $n), " units";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum cost to
// equalize an array with increment under
// modulo 3 operation.
function mincost(a, n)
{
    let c = 1;

    // Loop to check whether all
    // elements are equal or not
    for(let i = 0; i < n; i++)
        if (a[i] == a[i + 1])
            c++;

    // A special case when all
    // elements are equal
    if (c == n)
        return 0;

    // Variable that counts total
    // numbers greater 2
    let x = 0;

    // Loop to convert all numbers greater
    // than 2 to a range between 0 to 2.
    for(let i = 0; i < n; i++)
    {
        if (a[i] > 2)
        {

            // Number greater than 2 gets
            // converted to a number between 0 to 2.
            a[i] = (a[i] + 1) % 3;
            x += 1;
        }
    }

    // Variables to count 3 possible ways
    // to make all elements equal after
    // reducing them to range [0, 2]
    let c0 = 0, c1 = 0, c2 = 0;

    // Loop that counts total cost to
    // make all elements equal to 0.
    for(let i = 0; i < n; i++)
    {
        if (a[i] == 1)
        {

            // Since we will have to use the
            // operation 2 times to convert 1 to 0
            // (1+1)%3=2 and then (2+1)%3=0
            c0 += 2;
        }

        // Here we use it once since (2+1%3=0)       
        else if (a[i] == 2)
            c0 += 1;
    }

    // Loop that counts total cost to
    // make all elements equal to 1
    for(let i = 0; i < n; i++)
    {

        // Since (2+1%3=0) and (0+1%3=1)
        if (a[i] == 2)
            c1 += 2;

        // Since (0+1%3=1)
        else if (a[i] == 0)   
            c1 += 1;
    }

    // Loop that counts total cost
    // to make all elements equal to 2
    for(let i = 0; i < n; i++)
    {

        // Since 0+1%3=1 and 1+1%3=2
        if (a[i] == 0)
            c2 += 2;       
        else if (a[i] == 1)
            c2 += 1;        
    }

    // Finally the one with minimum
    // cost will be our answer
    let y = Math.min(c0, c1);
    return x + Math.min(y, c2);
}

// Driver code
let a = [ 98, 4, 3, 1 ];
let n = a.length;

document.write(mincost(a, n) + " units");

// This code is contributed by subham348

</script>
```

**输出:**

```
6 units
```

**时间复杂度:** O(n)