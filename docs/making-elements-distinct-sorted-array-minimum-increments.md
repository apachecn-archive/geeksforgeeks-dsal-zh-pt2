# 通过最小增量使排序数组中的元素不同

> 原文:[https://www . geesforgeks . org/making-elements-distinct-sorted-array-minimum-increments/](https://www.geeksforgeeks.org/making-elements-distinct-sorted-array-minimum-increments/)

给定一个排序的整数数组。我们需要通过增加值并尽可能保持数组和最小来使数组元素不同。我们需要打印最小可能的总和作为输出。

**示例:**

```
Input : arr[] = { 2, 2, 3, 5, 6 } ; 
Output : 20
Explanation : We make the array as {2, 
3, 4, 5, 6}. Sum becomes 2 + 3 + 4 + 
5 + 6 = 20

Input : arr[] = { 20, 20 } ; 
Output : 41
Explanation : We make {20, 21}

Input :  arr[] = { 3, 4, 6, 8 };
Output : 21
Explanation : All elements are unique 
so result is sum of each elements.  

```

**方法 1:**
1。遍历数组的每个元素。
2。如果 arr[i] == arr[i-1]，则通过从第 I 个(当前)位置向元素等于其前一个元素或变得小于前一个(因为前一个增加了)的位置添加 1 来更新数组的每个元素。
3。遍历每个元素后返回和。

## C++

```
// CPP program to make sorted array elements
// distinct by incrementing elements and keeping
// sum to minimum.
#include <iostream>
using namespace std;

// To find minimum sum of unique elements.
int minSum(int arr[], int n)
{
    int sum = arr[0];

    for (int i = 1; i < n; i++) {
        if (arr[i] == arr[i - 1]) {           

            // While current element is same as
            // previous or has become smaller
            // than previous.
            int j = i;
            while (j < n && arr[j] <= arr[j - 1]) {         
                arr[j] = arr[j] + 1;
                j++;
            }
        }
         sum = sum + arr[i];
     }

    return sum;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 3, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minSum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make sorted
// array elements distinct by
// incrementing elements and
// keeping sum to minimum.
import java.io.*;

class GFG
{
    // To find minimum sum
    // of unique elements.
    static int minSum(int arr[], int n)
    {
        int sum = arr[0];

        for (int i = 1; i < n; i++)
        {
            if (arr[i] == arr[i - 1]) {        

                // While current element is same as
                // previous or has become smaller
                // than previous.
                int j = i;
                while (j < n && arr[j] <= arr[j - 1])
                {        
                    arr[j] = arr[j] + 1;
                    j++;
                }
            }
            sum = sum + arr[i];
        }

        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 2, 2, 3, 5, 6 };
        int n = arr.length;
        System.out.println(minSum(arr, n));
    }
}

// This code is contributed by Ansu Kumari
```

## 蟒蛇 3

```
# Python3 program to make sorted array elements
# distinct by incrementing elements and keeping
# sum to minimum.

# To find minimum sum of unique elements.
def minSum(arr, n):
    sm = arr[0]

    for i in range(1, n):
        if arr[i] == arr[i - 1]:        

            # While current element is same as
            # previous or has become smaller
            # than previous.
            j = i
            while j < n and arr[j] <= arr[j - 1]:        
                arr[j] = arr[j] + 1
                j += 1

        sm = sm + arr[i]

    return sm

# Driver code
arr = [ 2, 2, 3, 5, 6 ]
n = len(arr)
print(minSum(arr, n))

# This code is contributed by Ansu Kumari
```

## C#

```
// C# program to make sorted
// array elements distinct by
// incrementing elements and
// keeping sum to minimum.
using System;

class GFG
{
    // To find minimum sum
    // of unique elements.
    static int minSum(int []arr, int n)
    {
        int sum = arr[0];

        for (int i = 1; i < n; i++)
        {
            if (arr[i] == arr[i - 1]) {    

                // While current element is same as
                // previous or has become smaller
                // than previous.
                int j = i;
                while (j < n && arr[j] <= arr[j - 1])
                {    
                    arr[j] = arr[j] + 1;
                    j++;
                }
            }
            sum = sum + arr[i];
        }

        return sum;
    }

    // Driver code
    public static void Main ()
    {
        int []arr = { 2, 2, 3, 5, 6 };
        int n = arr.Length;
        Console.WriteLine(minSum(arr, n));
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to make sorted array
// elements distinct by incrementing
// elements and keeping sum to minimum.

// To find minimum sum of unique
// elements.
function minSum($arr, $n)
{
    $sum = $arr[0];

    for ($i = 1; $i < $n; $i++) {
        if ($arr[$i] == $arr[$i - 1])
        {    

            // While current element is
            // same as previous or has
            // become smaller than
            // previous.
            $j = $i;
            while ($j < $n && $arr[$j]
                        <= $arr[$j - 1])
            {    
                $arr[$j] = $arr[$j] + 1;
                $j++;
            }
        }
        $sum = $sum + $arr[$i];
    }

    return $sum;
}

// Driver code
    $arr = array ( 2, 2, 3, 5, 6 );
    $n = sizeof($arr) ;
    echo minSum($arr, $n),"\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// JavaScript program to make sorted
// array elements distinct by
// incrementing elements and
// keeping sum to minimum.

    // To find minimum sum
    // of unique elements.
    function minSum(arr, n)
    {
        let sum = arr[0];

        for (let i = 1; i < n; i++)
        {
            if (arr[i] == arr[i - 1]) {        

                // While current element is same as
                // previous or has become smaller
                // than previous.
                let j = i;
                while (j < n && arr[j] <= arr[j - 1])
                {        
                    arr[j] = arr[j] + 1;
                    j++;
                }
            }
            sum = sum + arr[i];
        }

        return sum;
    }

// Driver code

        let arr = [ 2, 2, 3, 5, 6 ];
        let n = arr.length;
        document.write(minSum(arr, n));

</script>
```

**输出:**

```
20
```

时间复杂度: **O(n^2)**

**方法二:**
1。遍历数组的每个元素。
2。如果 arr[i] < = prev，则通过加 1 更新 prev，通过加 prev 更新和，
否则通过 cur 元素更新 prev，通过加 cur 元素更新和(arr[i])。
3。遍历每个元素后返回和。

## C++

```
// Efficient CPP program to make sorted array
// elements distinct by incrementing elements
// and keeping sum to minimum.
#include <iostream>
using namespace std;

// To find minimum sum of unique elements.
int minSum(int arr[], int n)
{
    int sum = arr[0], prev = arr[0];

    for (int i = 1; i < n; i++) {

        // If violation happens, make current
        // value as 1 plus previous value and
        // add to sum.
        if (arr[i] <= prev) {
            prev = prev + 1;
            sum = sum + prev;
        }

        // No violation.
        else {
            sum = sum + arr[i];
            prev = arr[i];
        }
    }

    return sum;
}

// Drivers code
int main()
{
    int arr[] = { 2, 2, 3, 5, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minSum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to make sorted array
// elements distinct by incrementing elements
// and keeping sum to minimum.
import java.io.*;

class GFG {

    // To find minimum sum of unique elements.
    static int minSum(int arr[], int n)
    {
        int sum = arr[0], prev = arr[0];

        for (int i = 1; i < n; i++) {

            // If violation happens, make current
            // value as 1 plus previous value and
            // add to sum.
            if (arr[i] <= prev) {
                prev = prev + 1;
                sum = sum + prev;
            }

            // No violation.

            else {
                sum = sum + arr[i];
                prev = arr[i];
            }
        }

        return sum;
    }

    // Drivers code
    public static void main (String[] args) {

        int arr[] = { 2, 2, 3, 5, 6 };
        int n = arr.length;

        System.out.println(minSum(arr, n));
    }
}

// This code is contributed by Ansu Kumari.
```

## 蟒蛇 3

```
# Efficient Python program to make sorted array
# elements distinct by incrementing elements
# and keeping sum to minimum.

# To find minimum sum of unique elements
def minSum(arr, n):

    sum = arr[0]; prev = arr[0]

    for i in range(1, n):

        # If violation happens, make current
        # value as 1 plus previous value and
        # add to sum.
        if arr[i] <= prev:
            prev = prev + 1
            sum = sum + prev

        # No violation.
        else :
            sum = sum + arr[i]
            prev = arr[i]

    return sum

# Drivers code
arr = [ 2, 2, 3, 5, 6 ]
n = len(arr)
print(minSum(arr, n))

# This code is contributed by Ansu Kumari
```

## C#

```
// Efficient C# program to make sorted array
// elements distinct by incrementing elements
// and keeping sum to minimum.
using System;

class GFG {

    // To find minimum sum of unique elements.
    static int minSum(int []arr, int n)
    {
        int sum = arr[0], prev = arr[0];

        for (int i = 1; i < n; i++) {

            // If violation happens, make current
            // value as 1 plus previous value and
            // add to sum.
            if (arr[i] <= prev) {
                prev = prev + 1;
                sum = sum + prev;
            }

            // No violation.

            else {
                sum = sum + arr[i];
                prev = arr[i];
            }
        }

        return sum;
    }

    // Drivers code
    public static void Main () {

        int []arr = { 2, 2, 3, 5, 6 };
        int n = arr.Length;

        Console.WriteLine(minSum(arr, n));
    }
}

// This code is contributed by vt_m .
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to
// make sorted array elements
// distinct by incrementing 
// elements and keeping sum
// to minimum.

// To find minimum sum
// of unique elements.
function minSum($arr, $n)
{
    $sum = $arr[0];
    $prev = $arr[0];

    for ( $i = 1; $i < $n; $i++)
    {

        // If violation happens,
        // make current value as
        // 1 plus previous value
        // and add to sum.
        if ($arr[$i] <= $prev)
        {
            $prev = $prev + 1;
            $sum = $sum + $prev;
        }

        // No violation.
        else
        {
            $sum = $sum + $arr[$i];
            $prev = $arr[$i];
        }
    }

    return $sum;
}

// Driver code
$arr = array(2, 2, 3, 5, 6);
$n = count($arr);
echo minSum($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program to make sorted array
// elements distinct by incrementing elements
// and keeping sum to minimum.

// To find minimum sum of unique elements.
function minSum(arr, n)
{
    let sum = arr[0], prev = arr[0];

    for(let i = 1; i < n; i++)
    {

        // If violation happens, make current
        // value as 1 plus previous value and
        // add to sum.
        if (arr[i] <= prev)
        {
            prev = prev + 1;
            sum = sum + prev;
        }

        // No violation.
        else
        {
            sum = sum + arr[i];
            prev = arr[i];
        }
    }
    return sum;
}

// Driver code
let arr = [ 2, 2, 3, 5, 6 ];
let n = arr.length;

document.write(minSum(arr, n));

// This code is contributed by decode2207

</script>
```

**输出:**

```
20
```

**时间复杂度:** O(n)