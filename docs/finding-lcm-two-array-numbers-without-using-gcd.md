# 不使用 GCD 查找两个以上(或数组)数的 LCM

> 原文:[https://www . geesforgeks . org/find-LCM-two-array-numbers-not-use-gcd/](https://www.geeksforgeeks.org/finding-lcm-two-array-numbers-without-using-gcd/)

给定一个正整数数组，求数组中元素的 LCM。
**例:**

```
Input : arr[] = {1, 2, 3, 4, 28}
Output : 84

Input  : arr[] = {4, 6, 12, 24, 30}
Output : 120
```

我们已经讨论了使用 GCD 的阵列的 [LCM。
在这篇文章中，我们讨论了一种不需要计算 GCD 的不同方法。以下是步骤。](https://www.geeksforgeeks.org/lcm-of-given-array-elements/) 

1.  初始化结果= 1
2.  找出两个或多个数组元素的公共因子。
3.  将结果乘以公因数，并将所有数组元素除以该公因数。
4.  当有两个或更多元素的公共因子时，重复步骤 2 和 3。
5.  将结果乘以简化(或划分)的数组元素。

插图:

```
Let we have to find the LCM of 
arr[] = {1, 2, 3, 4, 28}

We initialize result = 1.

2 is a common factor that appears in
two or more elements. We divide all
multiples by two and multiply result
with 2.
arr[] = {1, 1, 3, 2, 14}
result = 2

2 is again a common factor that appears 
in two or more elements. We divide all
multiples by two and multiply result
with 2.
arr[] = {1, 1, 3, 1, 7}
result = 4

Now there is no common factor that appears
in two or more array elements. We multiply
all modified array elements with result, we
get.
result = 4 * 1 * 1 * 3 * 1 * 7
       = 84
```

下面是上述算法的实现。

## C++

```
// C++ program to find LCM of array without
// using GCD.
#include<bits/stdc++.h>
using namespace std;

// Returns LCM of arr[0..n-1]
unsigned long long int LCM(int arr[], int n)
{
    // Find the maximum value in arr[]
    int max_num = 0;
    for (int i=0; i<n; i++)
        if (max_num < arr[i])
            max_num = arr[i];

    // Initialize result
    unsigned long long int res = 1;

    // Find all factors that are present in
    // two or more array elements.
    int x = 2;  // Current factor.
    while (x <= max_num)
    {
        // To store indexes of all array
        // elements that are divisible by x.
        vector<int> indexes;
        for (int j=0; j<n; j++)
            if (arr[j]%x == 0)
                indexes.push_back(j);

        // If there are 2 or more array elements
        // that are divisible by x.
        if (indexes.size() >= 2)
        {
            // Reduce all array elements divisible
            // by x.
            for (int j=0; j<indexes.size(); j++)
                arr[indexes[j]] = arr[indexes[j]]/x;

            res = res * x;
        }
        else
            x++;
    }

    // Then multiply all reduced array elements
    for (int i=0; i<n; i++)
        res = res*arr[i];

    return res;
}

// Driver code
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 10, 20, 35};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << LCM(arr, n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Vector;

// Java program to find LCM of array without
// using GCD.
class GFG {

// Returns LCM of arr[0..n-1]
    static long LCM(int arr[], int n) {
        // Find the maximum value in arr[]
        int max_num = 0;
        for (int i = 0; i < n; i++) {
            if (max_num < arr[i]) {
                max_num = arr[i];
            }
        }

        // Initialize result
        long res = 1;

        // Find all factors that are present in
        // two or more array elements.
        int x = 2; // Current factor.
        while (x <= max_num) {
            // To store indexes of all array
            // elements that are divisible by x.
            Vector<Integer> indexes = new Vector<>();
            for (int j = 0; j < n; j++) {
                if (arr[j] % x == 0) {
                    indexes.add(indexes.size(), j);
                }
            }

            // If there are 2 or more array elements
            // that are divisible by x.
            if (indexes.size() >= 2) {
                // Reduce all array elements divisible
                // by x.
                for (int j = 0; j < indexes.size(); j++) {
                    arr[indexes.get(j)] = arr[indexes.get(j)] / x;
                }

                res = res * x;
            } else {
                x++;
            }
        }

        // Then multiply all reduced array elements
        for (int i = 0; i < n; i++) {
            res = res * arr[i];
        }

        return res;
    }

// Driver code
    public static void main(String[] args) {
        int arr[] = {1, 2, 3, 4, 5, 10, 20, 35};
        int n = arr.length;
        System.out.println(LCM(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find LCM of array
# without using GCD.

# Returns LCM of arr[0..n-1]
def LCM(arr, n):

    # Find the maximum value in arr[]
    max_num = 0;
    for i in range(n):
        if (max_num < arr[i]):
            max_num = arr[i];

    # Initialize result
    res = 1;

    # Find all factors that are present
    # in two or more array elements.
    x = 2; # Current factor.
    while (x <= max_num):

        # To store indexes of all array
        # elements that are divisible by x.
        indexes = [];
        for j in range(n):
            if (arr[j] % x == 0):
                indexes.append(j);

        # If there are 2 or more array
        # elements that are divisible by x.
        if (len(indexes) >= 2):

            # Reduce all array elements
            # divisible by x.
            for j in range(len(indexes)):
                arr[indexes[j]] = int(arr[indexes[j]] / x);

            res = res * x;
        else:
            x += 1;

    # Then multiply all reduced
    # array elements
    for i in range(n):
        res = res * arr[i];

    return res;

# Driver code
arr = [1, 2, 3, 4, 5, 10, 20, 35];
n = len(arr);
print(LCM(arr, n));

# This code is contributed by chandan_jnu
```

## C#

```
// C# program to find LCM of array
// without using GCD.
using System;
using System.Collections;
class GFG
{

// Returns LCM of arr[0..n-1]
static long LCM(int []arr, int n)
{
    // Find the maximum value in arr[]
    int max_num = 0;
    for (int i = 0; i < n; i++)
    {
        if (max_num < arr[i])
        {
            max_num = arr[i];
        }
    }

    // Initialize result
    long res = 1;

    // Find all factors that are present
    // in two or more array elements.
    int x = 2; // Current factor.
    while (x <= max_num)
    {
        // To store indexes of all array
        // elements that are divisible by x.
        ArrayList indexes = new ArrayList();
        for (int j = 0; j < n; j++)
        {
            if (arr[j] % x == 0)
            {
                indexes.Add(j);
            }
        }

        // If there are 2 or more array elements
        // that are divisible by x.
        if (indexes.Count >= 2)
        {
            // Reduce all array elements divisible
            // by x.
            for (int j = 0; j < indexes.Count; j++)
            {
                arr[(int)indexes[j]] = arr[(int)indexes[j]] / x;
            }

            res = res * x;
        } else
        {
            x++;
        }
    }

    // Then multiply all reduced
    // array elements
    for (int i = 0; i < n; i++)
    {
        res = res * arr[i];
    }

    return res;
}

// Driver code
public static void Main()
{
    int []arr = {1, 2, 3, 4, 5, 10, 20, 35};
    int n = arr.Length;
    Console.WriteLine(LCM(arr, n));
}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find LCM of array
// without using GCD.

// Returns LCM of arr[0..n-1]
function LCM($arr, $n)
{
    // Find the maximum value in arr[]
    $max_num = 0;
    for ($i = 0; $i < $n; $i++)
        if ($max_num < $arr[$i])
            $max_num = $arr[$i];

    // Initialize result
    $res = 1;

    // Find all factors that are present
    // in two or more array elements.
    $x = 2; // Current factor.
    while ($x <= $max_num)
    {
        // To store indexes of all array
        // elements that are divisible by x.
        $indexes = array();
        for ($j = 0; $j < $n; $j++)
            if ($arr[$j] % $x == 0)
                array_push($indexes, $j);

        // If there are 2 or more array
        // elements that are divisible by x.
        if (count($indexes) >= 2)
        {
            // Reduce all array elements
            // divisible by x.
            for ($j = 0; $j < count($indexes); $j++)
                $arr[$indexes[$j]] = (int)($arr[$indexes[$j]] / $x);

            $res = $res * $x;
        }
        else
            $x++;
    }

    // Then multiply all reduced
    // array elements
    for ($i = 0; $i < $n; $i++)
        $res = $res * $arr[$i];

    return $res;
}

// Driver code
$arr = array(1, 2, 3, 4, 5, 10, 20, 35);
$n = count($arr);
echo LCM($arr, $n) . "\n";

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>
// Javascript program to find LCM of array without
// using GCD.

// Returns LCM of arr[0..n-1]
function LCM(arr, n)
{
    // Find the maximum value in arr[]
    var max_num = 0;
    for (var i = 0; i < n; i++)
        if (max_num < arr[i])
            max_num = arr[i];

    // Initialize result
    var res = 1;

    // Find all factors that are present in
    // two or more array elements.
    var x = 2;  // Current factor.
    while (x <= max_num)
    {
        // To store indexes of all array
        // elements that are divisible by x.
        var indexes = [];
        for (var j = 0; j < n; j++)
            if (arr[j] % x == 0)
                indexes.push(j);

        // If there are 2 or more array elements
        // that are divisible by x.
        if (indexes.length >= 2)
        {
            // Reduce all array elements divisible
            // by x.
            for (var j = 0; j < indexes.length; j++)
                arr[indexes[j]] = arr[indexes[j]]/x;

            res = res * x;
        }
        else
            x++;
    }

    // Then multiply all reduced array elements
    for (var i = 0; i < n; i++)
        res = res*arr[i];

    return res;
}

// Driver code
var arr = [1, 2, 3, 4, 5, 10, 20, 35];
var n = arr.length;
document.write( LCM(arr, n) + "<br>");

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
420
```

本文由**阿迪蒂亚·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。