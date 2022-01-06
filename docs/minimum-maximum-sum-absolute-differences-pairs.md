# 对的绝对差的最小和最大和

> 原文:[https://www . geesforgeks . org/最小-最大-和-绝对-差-对/](https://www.geeksforgeeks.org/minimum-maximum-sum-absolute-differences-pairs/)

给定 N 个整数的数组，其中 N 是偶数，求每个元素与另一个元素配对形成的 N/2 对绝对差的最小和最大和。

**示例:**

```
Input: a[] = {10, -10, 20, -40} 
Output: min_sum = 40, max_sum = 80
Explanation: Pairs selected for minimum sum 
             (-10, -40) and (10, 20) 
             min_sum = |-10 - -40| + |20 - 10| = 40 
             Pairs selected for maximum sum 
             (-10, 20) and (-40, 10) 
             max_sum = |-10 - 20| + |10 - -40| = 80

Input: a[] = {20, -10, -1, 30} 
Output: min_sum = 19, max_sum = 61 
Explanation: Pairs selected for minimum sum
             (-1, -10) and (20, 30) 
             min_sum = |-1 - -10| + |20 - 30| = 19 
             Pairs selected for maximum sum
             (-1, 30) and (-10, 20) 
             max_sum = |-1 - 30| + |-10 - 20| = 61 
```

**方法:**
最常见的观察结果是，对于差异的最小和，我们需要最接近的元素作为一对，对于最大和，我们需要最远的元素作为一对。因此，我们可以简单地对给定的元素列表进行排序，最接近的对将是 a[i]，a[i+1]，它们的绝对差和将产生最小和。最远的将是(a[0]、a[n-1])和(a[1]、a[n-2])等等，它们的绝对差和将产生我们的最大和。

## C++

```
// CPP program to find minimum and maximum
// sum of absolute differences of pairs
#include <bits/stdc++.h>
using namespace std;

// function to calculate minimum sum
int calculate_min_sum(int a[], int n)
{
    // sorts the array c++ stl
    sort(a, a + n);

    // initially min=0 and max=0
    int min_sum = 0;

    // traverse to find the minimum sum
    for (int i = 1; i < n; i += 2) {

        // the adjacent elements difference
        // will always be smaller
        min_sum += abs(a[i] - a[i - 1]);
    }
    return min_sum;
}

// function to calculate maximum sum
int calculate_max_sum(int a[], int n)
{
    // sorts the array c++ stl
    sort(a, a + n);

    int max_sum = 0;

    // traverse to find the maximum sum
    for (int i = 0; i < n / 2; i++) {

        // the farthest distant elements sum
        // will always be maximum
        max_sum += abs(a[n - 1 - i] - a[i]);
    }
    return max_sum;
}

// Driver program to test above function
int main()
{
    int a[] = { 10, -10, 20, -40};

    int n = sizeof(a) / sizeof(a[0]);

    cout << "The minimum sum of pairs is "
         << calculate_min_sum(a, n) << endl;

    cout << "The maximum sum of pairs is "
         << calculate_max_sum(a, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum and maximum
// sum of absolute differences of pairs
import java.util.Arrays;

class GFG
{
    // function to calculate minimum sum
    static int calculate_min_sum(int[] a, int n)
    {
        // sorts the array c++ stl
        Arrays.sort(a);

        // initially min=0 and max=0
        int min_sum = 0;

        // traverse to find the minimum sum
        for (int i = 1; i < n; i += 2) {

            // the adjacent elements difference
            // will always be smaller
            min_sum += Math.abs(a[i] - a[i - 1]);
        }
        return min_sum;
    }

    // function to calculate maximum sum
    static int calculate_max_sum(int[] a, int n)
    {
        // sorts the array c++ stl
        Arrays.sort(a);

        int max_sum = 0;

        // traverse to find the maximum sum
        for (int i = 0; i < n / 2; i++) {

            // the farthest distant elements sum
            // will always be maximum
            max_sum += Math.abs(a[n - 1 - i] - a[i]);
        }
        return max_sum;
    }

    // Driver program to test above function   
    public static void main (String[] args) {
    int[] a = { 10, -10, 20, -40};

    int n = a.length;

    System.out.println("The minimum sum of pairs is " +
                          calculate_min_sum(a, n));

    System.out.println("The maximum sum of pairs is " +
                           calculate_max_sum(a, n));

    }
}

/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Python 3 program to find minimum and maximum
# sum of absolute differences of pairs

# function to calculate minimum sum
def calculate_min_sum( a, n):

    # sorts the array c++ stl
    a.sort()

    # initially min=0 and max=0
    min_sum = 0

    # traverse to find the minimum sum
    for i in range(1, n, 2):

        # the adjacent elements difference
        # will always be smaller
        min_sum += abs(a[i] - a[i - 1])

    return min_sum

# function to calculate maximum sum
def calculate_max_sum(a, n):

    # sorts the array c++ stl
    a.sort()

    max_sum = 0

    # traverse to find the maximum sum
    for i in range(n // 2):

        # the farthest distant elements sum
        max_sum += abs(a[n - 1 - i] - a[i])
    return max_sum

# Driver Code
if __name__ == "__main__":

    a = [ 10, -10, 20, -40]

    n = len(a)

    print("The minimum sum of pairs is",
                calculate_min_sum(a, n))

    print( "The maximum sum of pairs is",
                 calculate_max_sum(a, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to find minimum and maximum
// sum of absolute differences of pairs
using System;

class GFG
{
    // function to calculate minimum sum
    static int calculate_min_sum(int []a, int n)
    {
        // sorts the array c++ stl
        Array.Sort(a);

        // initially min=0 and max=0
        int min_sum = 0;

        // traverse to find the minimum sum
        for (int i = 1; i < n; i += 2) {

            // the adjacent elements difference
            // will always be smaller
            min_sum += Math.Abs(a[i] - a[i - 1]);
        }
        return min_sum;
    }

    // Function to calculate maximum sum
    static int calculate_max_sum(int []a, int n)
    {
        // sorts the array c++ stl
        Array.Sort(a);

        int max_sum = 0;

        // Traverse to find the maximum sum
        for (int i = 0; i < n / 2; i++) {

            // the farthest distant elements sum
            // will always be maximum
            max_sum += Math.Abs(a[n - 1 - i] - a[i]);
        }
        return max_sum;
    }

    // Driver Code
    public static void Main ()
    {
    int []a = { 10, -10, 20, -40};

    int n = a.Length;

    Console.WriteLine("The minimum sum of pairs is " +
                            calculate_min_sum(a, n));

    Console.Write("The maximum sum of pairs is " +
                         calculate_max_sum(a, n));

    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum and maximum
// sum of absolute differences of pairs

// function to calculate minimum sum
function calculate_min_sum($a, $n)
{

    // sorts the array c++ stl
    sort($a);

    // initially min=0 and max=0
    $min_sum = 0;

    // traverse to find the minimum sum
    for ($i = 1; $i < $n; $i += 2)
    {

        // the adjacent elements difference
        // will always be smaller
        $min_sum += abs($a[$i] -
                    $a[$i - 1]);
    }
    return $min_sum;
}

// function to calculate maximum sum
function calculate_max_sum($a, $n)
{

    // sorts the array c++ stl
    sort($a);

    $max_sum = 0;

    // traverse to find the maximum sum
    for ($i = 0; $i < $n / 2; $i++)
    {

        // the farthest distant elements sum
        // will always be maximum
        $max_sum += abs($a[$n - 1 - $i] -
                                  $a[$i]);
    }
    return $max_sum;
}

// Driver Code
$a = array(10, -10, 20, -40);

$n = sizeof($a);

echo("The minimum sum of pairs is "
        . calculate_min_sum($a, $n) . "\n");

echo("The maximum sum of pairs is "
        . calculate_max_sum($a, $n));

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum and maximum
// sum of absolute differences of pairs

// Function to calculate minimum sum
function calculate_min_sum(a, n)
{

    // Sorts the array c++ stl
    a.sort();

    // Initially min=0 and max=0
    let min_sum = 0;

    // Traverse to find the minimum sum
    for(let i = 1; i < n; i += 2)
    {

        // The adjacent elements difference
        // will always be smaller
        min_sum += Math.abs(a[i] - a[i - 1]);
    }
    return min_sum;
}

// Function to calculate maximum sum
function calculate_max_sum(a, n)
{

    // Sorts the array c++ stl
    a.sort();

    let max_sum = 0;

    // Traverse to find the maximum sum
    for(let i = 0; i < parseInt(n / 2, 10); i++)
    {

        // The farthest distant elements sum
        // will always be maximum
        max_sum += Math.abs(a[n - 1 - i] - a[i]);
    }
    return max_sum;
}

// Driver code
let a = [ 10, -10, 20, -40 ];
let n = a.length;

document.write("The minimum sum of pairs is " +
               calculate_min_sum(a, n) + "</br>");

document.write("The maximum sum of pairs is " +
               calculate_max_sum(a, n));

// This code is contributed by decode2207

</script>
```

**输出:**

```
The minimum sum of pairs is 40
The maximum sum of pairs is 80
```

**时间复杂度:** O(n log n)

本文由 **Raja Vikramaditya** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。