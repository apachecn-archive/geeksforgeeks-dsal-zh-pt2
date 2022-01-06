# 最小化由 N 个数字组成的 N/2 对的和的平方和

> 原文:[https://www . geesforgeks . org/最小化 n-2 对 n-数字形成的平方和/](https://www.geeksforgeeks.org/minimize-the-sum-of-squares-of-sum-of-n-2-paired-formed-by-n-numbers/)

给定 N 个数字(N 是偶数)。将 N 个数分成 N/2 对，使成对数之和的平方和最小。任务是打印最小和。
**例:**

```
Input: a[] = {8, 5, 2, 3}
Output: 164 
Divide them into two groups of {2, 8} and {3, 5}
to give (2+8)2 + (3+5)2 = 164   

Input: a[] = {1, 1, 1, 2, 2, 2}
Output: 27 
```

**方法:**任务是最小化平方和，因此我们在第一组中划分最小和最大的数，在第二组中划分第二小和第二大的数，以此类推，直到形成 N/2 组。将数字相加，并存储它们的平方和，这将是最终答案。
以下是上述办法的实施情况:

## C++

```
// C++ program to minimize the sum
// of squares of sum of numbers
// of N/2 groups of N numbers

#include <bits/stdc++.h>
using namespace std;

// Function that returns the minimize sum
// of square of sum of numbers of every group
int findMinimal(int a[], int n)
{
    // Sort the array elements
    sort(a, a + n);

    int sum = 0;

    // Iterate for the first half of array
    for (int i = 0; i < n / 2; i++)
        sum += (a[i] + a[n - i - 1])
                * (a[i] + a[n - i - 1]);

    return sum;
}

// Driver Code
int main()
{
    int a[] = { 8, 5, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << findMinimal(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimize the sum
// of squares of sum of numbers
// of N/2 groups of N numbers
import java.util.Arrays;

class GFG
{

    // Function that returns the minimize sum
    // of square of sum of numbers of every group
    static int findMinimal(int []a, int n)
    {
        // Sort the array elements
        Arrays.sort(a);

        int sum = 0;

        // Iterate for the first half of array
        for (int i = 0; i < n / 2; i++)
            sum += (a[i] + a[n - i - 1]) *
                (a[i] + a[n - i - 1]);

        return sum;
    }

    // Driver Code
    public static void main(String str[])
    {
        int []a = { 8, 5, 2, 3 };
        int n = a.length;
        System.out.println(findMinimal(a, n));
    }
}

// This code is contributed by Ryuga
```

## 蟒蛇 3

```
# Python 3 program to minimize the sum
# of squares of sum of numbers
# of N/2 groups of N numbers

# Function that returns the minimize sum
# of square of sum of numbers of every group
def findMinimal(a, n):

    # Sort the array elements
    a.sort()

    sum = 0

    # Iterate for the first half of array
    for i in range( n // 2):
        sum += ((a[i] + a[n - i - 1]) *
                (a[i] + a[n - i - 1]))

    return sum

# Driver Code
if __name__ == "__main__":

    a = [ 8, 5, 2, 3 ]
    n = len(a)

    print(findMinimal(a, n))

# This code is contributed by ita_c
```

## C#

```
// C# program to minimize the sum
// of squares of sum of numbers
// of N/2 groups of N numbers
using System;

class GFG
{

// Function that returns the minimize sum
// of square of sum of numbers of every group
static int findMinimal(int []a, int n)
{
    // Sort the array elements
    Array.Sort(a);

    int sum = 0;

    // Iterate for the first half of array
    for (int i = 0; i < n / 2; i++)
        sum += (a[i] + a[n - i - 1]) *
               (a[i] + a[n - i - 1]);

    return sum;
}

// Driver Code
public static void Main()
{
    int []a = { 8, 5, 2, 3 };
    int n = a.Length;

    Console.Write(findMinimal(a, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to minimize the sum
// of squares of sum of numbers
// of N/2 groups of N numbers

// Function that returns the minimize sum
// of square of sum of numbers of every group
function findMinimal($a, $n)
{
    // Sort the array elements
    sort($a);

    $sum = 0;

    // Iterate for the first half of array
    for ($i = 0; $i < $n / 2; $i++)
        $sum += ($a[$i] + $a[$n - $i - 1]) *
                ($a[$i] + $a[$n - $i - 1]);

    return $sum;
}

// Driver Code
$a = array(8, 5, 2, 3 );
$n = sizeof($a);

echo findMinimal($a, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
// java script  program to minimize the sum
// of squares of sum of numbers
// of N/2 groups of N numbers

// Function that returns the minimize sum
// of square of sum of numbers of every group
function findMinimal(a, n)
{

    // Sort the array elements
    a.sort();

    let sum = 0;

    // Iterate for the first half of array
    for (let i = 0; i < n / 2; i++)
        sum += (a[i] + a[n - i - 1]) *
                (a[i] + a[n - i - 1]);

    return sum;
}

// Driver Code
let a = [8,5,2,3];
let n = a.length;

document.write( findMinimal(a, n));

// This code is contributed by sravan kumar G
</script>
```

**Output:** 

```
164
```

**时间复杂度:**O(N log N)
T3】辅助空间: O(N)