# 矩阵中每行元素的最大和

> 原文:[https://www . geesforgeks . org/maximum-sum-elements-row-matrix/](https://www.geeksforgeeks.org/maximum-sum-elements-row-matrix/)

给定一个矩阵，从每一行中选择一个元素，找到我们能得到的最大和。条件是从第 n 行中选择的元素必须严格大于从第(n-1)行中选择的元素，否则不得从行中提取任何元素。如果可能，打印总和，否则打印-1。
**例:**

```
Input : 
1 2 3
1 2 3
7 8 9 
Output : 14 (2 + 3 + 9) (values we
are adding are strictly increasing)

Input :
4 2 3
3 2 1
1 2 2
Output : -1 
(No subsequent increasing elements
can be picked from consecutive rows)
```

**方法:-** 可以简单地从最后一行开始运行循环，从那里获取最大的元素，称之为 prev_max，并记录它正上方的行的元素之间的最小差异，如果发现任何具有正差异的元素，则将其添加到 prev_max else print -1。对每一行继续相同的过程。

## C++

```
// CPP Program to find row-wise maximum element
// sum considering elements in increasing order.
#include <bits/stdc++.h>
#define N 3
using namespace std;

// Function to perform given task
int getGreatestSum(int a[][N])
{
    // Getting the maximum element from last row
    int prev_max = 0;
    for (int j = 0; j < N; j++)
        if (prev_max < a[N - 1][j])
            prev_max = a[N - 1][j];

    // Comparing it with the elements of above rows
    int sum = prev_max;
    for (int i = N - 2; i >= 0; i--) {

        // Maximum of current row.
        int curr_max = INT_MIN;
        for (int j = 0; j < N; j++)
            if (prev_max > a[i][j] && a[i][j] > curr_max)
                curr_max = a[i][j];

        // If we could not an element smaller
        // than prev_max.
        if (curr_max == INT_MIN)
            return -1;

        prev_max = curr_max;
        sum += prev_max;
    }
    return sum;
}

// Driver code
int main()
{
    int a[3][3] = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
    cout << getGreatestSum(a) << endl;
    int b[3][3] = { { 4, 5, 6 }, { 4, 5, 6 }, { 4, 5, 6 } };
    cout << getGreatestSum(b) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find row-wise maximum
// element sum considering elements in
// increasing order.
class GFG {

    static final int N = 3;

    // Function to perform given task
    static int getGreatestSum(int a[][])
    {

        // Getting the maximum element from
        // last row
        int prev_max = 0;

        for (int j = 0; j < N; j++)
            if (prev_max < a[N - 1][j])
                prev_max = a[N - 1][j];

        // Comparing it with the elements
        // of above rows
        int sum = prev_max;

        for (int i = N - 2; i >= 0; i--) {

            // Maximum of current row.
            int curr_max = -2147483648;

            for (int j = 0; j < N; j++)
                if (prev_max > a[i][j] && a[i][j] > curr_max)
                    curr_max = a[i][j];

            // If we could not an element smaller
            // than prev_max.
            if (curr_max == -2147483648)
                return -1;

            prev_max = curr_max;
            sum += prev_max;
        }

        return sum;
    }

    // Driver Program to test above function
    public static void main(String arg[])
    {

        int a[][] = { { 1, 2, 3 },
                      { 4, 5, 6 },
                      { 7, 8, 9 } };
        System.out.println(getGreatestSum(a));

        int b[][] = { { 4, 5, 6 },
                      { 4, 5, 6 },
                      { 4, 5, 6 } };
        System.out.println(getGreatestSum(b));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python Program to find
# row-wise maximum element
# sum considering elements
# in increasing order.

N = 3

# Function to perform given task
def getGreatestSum(a):

    # Getting the maximum
    # element from last row
    prev_max = 0
    for j in range(N):
        if (prev_max < a[N - 1][j]):
            prev_max = a[N - 1][j]

    # Comparing it with the
    # elements of above rows
    sum = prev_max
    for i in range(N - 2, -1, -1):

        # Maximum of current row.
        curr_max = -2147483648
        for j in range(N):
            if (prev_max > a[i][j] and a[i][j] > curr_max):
                curr_max = a[i][j]

        # If we could not an element smaller
        # than prev_max.
        if (curr_max == -2147483648):
            return -1

        prev_max = curr_max
        sum = sum + prev_max

    return sum

# Driver code

a = [ [ 1, 2, 3 ],
    [ 4, 5, 6 ],
    [ 7, 8, 9 ] ]

print(getGreatestSum(a))

b = [ [ 4, 5, 6 ],
    [ 4, 5, 6 ],
    [ 4, 5, 6 ] ]

print(getGreatestSum(b))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# Program to find row-wise maximum
// element sum considering elements in
// increasing order.
using System;

class GFG {

    static int N = 3;

    // Function to perform given task
    static int getGreatestSum(int[, ] a)
    {

        // Getting the maximum element from
        // last row
        int prev_max = 0;

        for (int j = 0; j < N; j++)
            if (prev_max < a[N - 1, j])
                prev_max = a[N - 1, j];

        // Comparing it with the elements
        // of above rows
        int sum = prev_max;

        for (int i = N - 2; i >= 0; i--) {

            // Maximum of current row.
            int curr_max = -2147483648;

            for (int j = 0; j < N; j++)
                if (prev_max > a[i, j] && a[i, j] > curr_max)
                    curr_max = a[i, j];

            // If we could not an element smaller
            // than prev_max.
            if (curr_max == -2147483648)
                return -1;

            prev_max = curr_max;
            sum += prev_max;
        }

        return sum;
    }

    // Driver Program
    public static void Main()
    {

        int[, ] a = { { 1, 2, 3 },
                      { 4, 5, 6 },
                      { 7, 8, 9 } };
        Console.WriteLine(getGreatestSum(a));

        int[, ] b = { { 4, 5, 6 },
                      { 4, 5, 6 },
                      { 4, 5, 6 } };
        Console.WriteLine(getGreatestSum(b));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find
// row-wise maximum element
// sum considering elements
// in increasing order.

$N = 3;

// Function to perform given task
function getGreatestSum( $a)
{
    global $N;

    // Getting the maximum
    // element from last row
    $prev_max = 0;

    for ($j = 0; $j < $N; $j++)
        if ($prev_max < $a[$N - 1][$j])
            $prev_max = $a[$N - 1][$j];

    // Comparing it with the
    // elements of above rows
    $sum = $prev_max;
    for ($i = $N - 2; $i >= 0; $i--)
    {

        // Maximum of current row.
        $curr_max = PHP_INT_MIN;
        for ( $j = 0; $j < $N; $j++)
            if ($prev_max > $a[$i][$j] and
                $a[$i][$j] > $curr_max)
                $curr_max = $a[$i][$j];

        // If we could not an element
        // smaller than prev_max.
        if ($curr_max == PHP_INT_MIN)
            return -1;

        $prev_max = $curr_max;
        $sum += $prev_max;
    }
    return $sum;
}

// Driver code
$a = array(array(1, 2, 3),
        array(4, 5, 6),
        array(7, 8, 9));

echo getGreatestSum($a), "\n";
$b = array(array(4, 5, 6),
        array(4, 5, 6),
        array(4, 5, 6));

echo getGreatestSum($b), "\n";

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript Program to find row-wise maximum
// element sum considering elements in
// increasing orderers

let N = 3;

    // Function to perform given task
    function getGreatestSum(a)
    {

        // Getting the maximum element from
        // last row
        let prev_max = 0;

        for (let j = 0; j < N; j++)
            if (prev_max < a[N - 1][j])
                prev_max = a[N - 1][j];

        // Comparing it with the elements
        // of above rows
        let sum = prev_max;

        for (let i = N - 2; i >= 0; i--) {

            // Maximum of current row.
            let curr_max = -2147483648;

            for (let j = 0; j < N; j++)
                if (prev_max > a[i][j] && a[i][j] > curr_max)
                    curr_max = a[i][j];

            // If we could not an element smaller
            // than prev_max.
            if (curr_max == -2147483648)
                return -1;

            prev_max = curr_max;
            sum += prev_max;
        }

        return sum;
    }

// Driver Code

        let a = [[ 1, 2, 3 ],
                      [ 4, 5, 6 ],
                      [ 7, 8, 9 ]];
        document.write(getGreatestSum(a) + "<br/>");

        let b = [[ 4, 5, 6 ],
                      [ 4, 5, 6 ],
                      [4, 5, 6 ]];
        document.write(getGreatestSum(b));

</script>
```

**输出:**

```
18
15
```