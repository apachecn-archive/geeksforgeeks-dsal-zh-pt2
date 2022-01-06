# 阵列的最大周长三角形

> 原文:[https://www . geeksforgeeks . org/最大周长-从阵列三角形/](https://www.geeksforgeeks.org/maximum-perimeter-triangle-from-array/)

给定一个非负整数数组。从这个数组中找出三个组成最大周长三角形的元素。

**示例:**

```
Input : {6, 1, 6, 5, 8, 4}
Output : 20

Input : {2, 20, 7, 55, 1, 33, 12, 4}
Output : Triangle formation is not possible.

Input: {33, 6, 20, 1, 8, 12, 5, 55, 4, 9}
Output: 41 
```

**天真解:**
蛮力解是:检查 3 个元素的所有组合，是否形成三角形，如果形成三角形则更新最大周长。天真解决方案的复杂性是 O(n <sup>3</sup> )。下面是它的代码。

## C++

```
// Brute force solution to find
// out maximum perimeter triangle which
// can be formed using the elements
// of the given array
#include <iostream>
#include <algorithm>

using namespace std;

// Function to find out maximum perimeter
void maxPerimeter(int arr[], int n){

    // initialize maximum perimeter
    // as 0.
    int maxi = 0;

    // pick up 3 different elements
    // from the array.
    for (int i = 0; i < n - 2; i++){
        for (int j = i + 1; j < n - 1; j++){
            for (int k = j + 1; k < n; k++){

                // a, b, c are 3 sides of the triangle
                int a = arr[i];
                int b = arr[j];
                int c = arr[k];

                // check whether a, b, c forms
                // a triangle or not.
                if (a < b+c && b < c+a && c < a+b){

                    // if it forms a triangle
                    // then update the maximum value.
                    maxi = max(maxi, a+b+c);
                }
            }
        }
    }

    // If maximum perimeter is non-zero
    // then print it.
    if (maxi) cout << "Maximum Perimeter is: "
                   << maxi << endl;

    // otherwise no triangle formation
    // is possible.
    else cout << "Triangle formation "
        << "is not possible." << endl;
}

// Driver Program
int main()
{
    // test case 1
    int arr1[6] = {6, 1, 6, 5, 8, 4};
    maxPerimeter(arr1, 6);

    // test case 2
    int arr2[8] = {2, 20, 7, 55, 1,
                    33, 12, 4};
    maxPerimeter(arr2, 8);

    // test case 3
    int arr3[10] = {33, 6, 20, 1, 8,
                    12, 5, 55, 4, 9};
    maxPerimeter(arr3, 10);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Brute force solution to find out maximum
// perimeter triangle which can be formed
// using the elements of the given array
import java.io.*;

class GFG {

    // Function to find out maximum perimeter
    static void maxPerimeter(int arr[], int n)
    {

        // initialize maximum perimeter as 0.
        int maxi = 0;

        // pick up 3 different elements
        // from the array.
        for (int i = 0; i < n - 2; i++)
        {
            for (int j = i + 1; j < n - 1; j++)
            {
                for (int k = j + 1; k < n; k++)
                {

                    // a, b, c are 3 sides of
                    // the triangle
                    int a = arr[i];
                    int b = arr[j];
                    int c = arr[k];

                    // check whether a, b, c
                    // forms a triangle or not.
                    if (a < b+c && b < c+a && c < a+b)
                    {

                        // if it forms a triangle
                        // then update the maximum
                        // value.
                        maxi = Math.max(maxi, a+b+c);
                    }
                }
            }
        }

        // If maximum perimeter is non-zero
        // then print it.
        if (maxi > 0)
        System.out.println( "Maximum Perimeter is: "
                                             + maxi);

        // otherwise no triangle formation
        // is possible.
        else
        System.out.println( "Triangle formation "
                              + "is not possible." );
    }

    // Driver Program
    public static void main (String[] args)
    {

        // test case 1
        int arr1[] = {6, 1, 6, 5, 8, 4};
        maxPerimeter(arr1, 6);

        // test case 2
        int arr2[] = {2, 20, 7, 55, 1, 33, 12, 4};
        maxPerimeter(arr2, 8);

        // test case 3
        int arr3[] = {33, 6, 20, 1, 8,
                                12, 5, 55, 4, 9};
        maxPerimeter(arr3, 10);
    }
}

// This code is contributed by anuj_67.
```

## 计算机编程语言

```
# Brute force solution to find
# out maximum perimeter triangle
# which can be formed using the
# elements of the given array

# Function to find out
# maximum perimeter
def maxPerimeter(arr):
    maxi = 0
    n = len(arr)

    # pick up 3 different
    # elements from the array.
    for i in range(n - 2):
        for j in range(i + 1, n - 1):
            for k in range(j + 1, n):

                # a, b, c are 3 sides
                # of the triangle
                a = arr[i]
                b = arr[j]
                c = arr[k]
                if(a < b + c and b < a + c
                             and c < a + b):
                    maxi = max(maxi, a + b + c)

    if(maxi == 0):
        return "Triangle formation is not possible"
    else:
        return "Maximum Perimeter is: "+ str(maxi)

# Driver code
def main():
    arr1 = [6, 1, 6, 5, 8, 4]
    a = maxPerimeter(arr1)
    print(a)

    arr2 = [2, 20, 7, 55,
            1, 33, 12, 4]
    a = maxPerimeter(arr2)
    print(a)

    arr3 = [33, 6, 20, 1, 8,
            12, 5, 55, 4, 9]
    a = maxPerimeter(arr3)
    print(a)

if __name__=='__main__':
    main()

# This code is contributed
# by Pritha Updhayay
```

## C#

```
// Brute force solution to find out
// maximum perimeter triangle which
// can be formed using the elements
// of the given array
using System;

class GFG
{

    // Function to find out
    // maximum perimeter
    static void maxPerimeter(int []arr,    
                             int n)
    {

        // initialize maximum
        // perimeter as 0.
        int maxi = 0;

        // pick up 3 different elements
        // from the array.
        for (int i = 0; i < n - 2; i++)
        {
            for (int j = i + 1; j < n - 1; j++)
            {
                for (int k = j + 1; k < n; k++)
                {

                    // a, b, c are 3 sides of
                    // the triangle
                    int a = arr[i];
                    int b = arr[j];
                    int c = arr[k];

                    // check whether a, b, c
                    // forms a triangle or not.
                    if (a < b + c &&
                        b < c + a &&
                        c < a + b)
                    {

                        // if it forms a triangle
                        // then update the maximum
                        // value.
                        maxi = Math.Max(maxi, a + b + c);
                    }
                }
            }
        }

        // If maximum perimeter is
        // non-zero then print it.
        if (maxi > 0)
        Console.WriteLine("Maximum Perimeter is: "+ maxi);

        // otherwise no triangle
        // formation is possible.
        else
        Console.WriteLine("Triangle formation "+
                          "is not possible.");
    }

    // Driver Code
    public static void Main ()
    {

        // test case 1
        int []arr1 = {6, 1, 6,
                      5, 8, 4};
        maxPerimeter(arr1, 6);

        // test case 2
        int []arr2 = {2, 20, 7, 55,
                      1, 33, 12, 4};
        maxPerimeter(arr2, 8);

        // test case 3
        int []arr3 = {33, 6, 20, 1, 8,
                      12, 5, 55, 4, 9};
        maxPerimeter(arr3, 10);
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Brute force solution to find
// out maximum perimeter triangle which
// can be formed using the elements
// of the given array

// Function to find out
// maximum perimeter
function maxPerimeter($arr, $n)
{

    // initialize maximum
    // perimeter as 0.
    $maxi = 0;

    // pick up 3 different
    // elements from the array.
    for ($i = 0; $i < $n - 2; $i++)
    {
        for ( $j = $i + 1; $j < $n - 1; $j++)
        {
            for ( $k = $j + 1; $k < $n; $k++)
            {

                // a, b, c are 3 sides
                // of the triangle
                $a = $arr[$i];
                $b = $arr[$j];
                $c = $arr[$k];

                // check whether a, b, c
                // forms a triangle or not.
                if ($a < $b + $c and
                    $b < $c + $a and
                    $c < $a + $b)
                {

                    // if it forms a triangle
                    // then update the maximum value.
                    $maxi = max($maxi, $a + $b + $c);
                }
            }
        }
    }

    // If maximum perimeter is
    // non-zero then print it.
    if ($maxi)
    {
    echo "Maximum Perimeter is: ";
    echo $maxi ,"\n";
    }

    // otherwise no triangle
    // formation is possible.
    else
    {
    echo "Triangle formation ";
    echo "is not possible. \n";
    }
}

// Driver Code

// test case 1
$arr1 = array(6, 1, 6, 5, 8, 4);
maxPerimeter($arr1, 6);

// test case 2
$arr2 = array(2, 20, 7, 55,
              1, 33, 12, 4);
maxPerimeter($arr2, 8);

// test case 3
$arr3 = array(33, 6, 20, 1, 8,
              12, 5, 55, 4, 9);
maxPerimeter($arr3, 10);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find
// out maximum perimeter triangle which
// can be formed using the elements
// of the given array

    // Function to find out maximum perimeter
    function maxPerimeter(arr, n)
    {

        // initialize maximum perimeter as 0.
        let maxi = 0;

        // pick up 3 different elements
        // from the array.
        for (let i = 0; i < n - 2; i++)
        {
            for (let j = i + 1; j < n - 1; j++)
            {
                for (let k = j + 1; k < n; k++)
                {

                    // a, b, c are 3 sides of
                    // the triangle
                    let a = arr[i];
                    let b = arr[j];
                    let c = arr[k];

                    // check whether a, b, c
                    // forms a triangle or not.
                    if (a < b+c && b < c+a && c < a+b)
                    {

                        // if it forms a triangle
                        // then update the maximum
                        // value.
                        maxi = Math.max(maxi, a+b+c);
                    }
                }
            }
        }

        // If maximum perimeter is non-zero
        // then prlet it.
        if (maxi > 0)
        document.write( "Maximum Perimeter is: "
                                             + maxi + "<br/>");

        // otherwise no triangle formation
        // is possible.
        else
        document.write( "Triangle formation "
                              + "is not possible." + "<br/>" );
    }

// Driver code

        // test case 1
        let arr1 = [6, 1, 6, 5, 8, 4];
        maxPerimeter(arr1, 6);

        // test case 2
        let arr2 = [2, 20, 7, 55, 1, 33, 12, 4];
        maxPerimeter(arr2, 8);

        // test case 3
        let arr3 = [33, 6, 20, 1, 8,
                                12, 5, 55, 4, 9];
        maxPerimeter(arr3, 10);

// This code is contributed by splevel62.
</script>
```

**输出:**

```
Maximum Perimeter is: 20
Triangle formation is not possible.
Maximum Perimeter is: 41
```

**高效方法:**
首先，我们可以按非递增顺序对数组进行排序。所以，第一个元素是最大值，最后一个元素是最小值。现在，如果这个排序数组的前 3 个元素形成一个三角形，那么它将是最大周长三角形，至于所有其他组合，元素的总和(即该三角形的周长)将是= b > = c。a、b、c 不能形成三角形，所以 a > = b + c. As、b、c = c+d(如果我们降 b 取 d)或者 a > = b+d(如果我们降 c 取 d)。因此，我们必须放下 a，拿起 d
同样，对 b、c 和 d 进行同样的分析。我们可以继续这一过程，直到结束，每当我们发现一个三角形形成一个三重，然后我们可以停止检查，因为这个三重给出了最大周长。
因此，如果在排序的数组中 arr[i]<arr[i+1]+arr[i+2](0<= I<= n-3)，那么 arr[I]、arr[I+1]和 arr[I+2]形成一个三角形。
下面是这个概念的简单实现:

## C++

```
// Efficient solution to find
// out maximum perimeter triangle which
// can be formed using the elements
// of the given array
#include <iostream>
#include <algorithm>

using namespace std;

// Function to find out maximum perimeter
void maxPerimeter(int arr[], int n){

    // sort the array elements
    // in reversed order
    sort(arr, arr+n, greater<int>());

    // initialize maximum
    // perimeter to 0
    int maxi = 0;

    // loop through the sorted array
    // and check whether it forms a
    // triangle or not.
    for (int i = 0; i < n-2; i++){

        // Check whether arr[i], arr[i+1]
        // and arr[i+2] forms a triangle
        // or not.
        if (arr[i] < arr[i+1] + arr[i+2]){

            // if it forms a triangle then
            // it is the triangle with
            // maximum perimeter.
            maxi = max(maxi, arr[i] + arr[i+1] + arr[i+2]);
            break;
        }
    }

    // If maximum perimeter is non-zero
    // then print it.
    if (maxi)
        cout << "Maximum Perimeter is: "
        << maxi << endl;

    // otherwise no triangle formation
    // is possible.
    else
        cout << "Triangle formation"
        << "is not possible." << endl;
}

// Driver Program
int main()
{
    // test case 1
    int arr1[6] = {6, 1, 6, 5, 8, 4};
    maxPerimeter(arr1, 6);

    // test case 2
    int arr2[8] = {2, 20, 7, 55, 1,
                    33, 12, 4};
    maxPerimeter(arr2, 8);

    // test case 3
    int arr3[10] = {33, 6, 20, 1, 8,
                    12, 5, 55, 4, 9};
    maxPerimeter(arr3, 10);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient solution to find
// out maximum perimeter triangle which
// can be formed using the elements
// of the given array

import java.util.Arrays;

class GFG {

// Function to find out maximum perimeter
    static void maxPerimeter(int arr[], int n) {

        // sort the array elements
        // in reversed order
        arr = arrRevSort(arr);
        //sort(arr, arr+n, greater<int>());

        // initialize maximum
        // perimeter to 0
        int maxi = 0;

        // loop through the sorted array
        // and check whether it forms a
        // triangle or not.
        for (int i = 0; i < n - 2; i++) {

            // Check whether arr[i], arr[i+1]
            // and arr[i+2] forms a triangle
            // or not.
            if (arr[i] < arr[i + 1] + arr[i + 2]) {

                // if it forms a triangle then
                // it is the triangle with
                // maximum perimeter.
                maxi = Math.max(maxi, arr[i] + arr[i + 1] + arr[i + 2]);
                break;
            }
        }

        // If maximum perimeter is non-zero
        // then print it.
        if (maxi > 0) {
            System.out.println("Maximum Perimeter is: " + maxi);
        } // otherwise no triangle formation
        // is possible.
        else {
            System.out.println("Triangle formation is not possible.");
        }
    }
    //Function return sorted array in Decreasing

    static int[] arrRevSort(int[] arr) {
        Arrays.sort(arr, 0, arr.length);
        int j = arr.length - 1;
        for (int i = 0; i < arr.length / 2; i++, j--) {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
        return arr;
    }

// Driver Program
    public static void main(String[] args) {
        // test case 1
        int arr1[] = {6, 1, 6, 5, 8, 4};
        maxPerimeter(arr1, 6);

        // test case 2
        int arr2[] = {2, 20, 7, 55, 1, 33, 12, 4};
        maxPerimeter(arr2, 8);

        // test case 3
        int arr3[] = {33, 6, 20, 1, 8, 12, 5, 55, 4, 9};
        maxPerimeter(arr3, 10);
    }
}
/*This Java code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Efficient solution to find
# out maximum perimeter triangle which
# can be formed using the elements
# of the given array

# Function to find the
# maximum perimeter
def maxPerimeter(arr):
    maxi = 0
    n = len(arr)
    arr.sort(reverse = True)

    for i in range(0, n - 2):
        if arr[i] < (arr[i + 1] + arr[i + 2]):
            maxi = max(maxi, arr[i] +
                       arr[i + 1] + arr[i + 2])
            break

    if(maxi == 0):
        return "Triangle formation is not possible"
    else:
        return "Maximum Perimeter is: "+ str(maxi)

# Driver Code
def main():
    arr1 = [6, 1, 6, 5, 8, 4]
    a = maxPerimeter(arr1)
    print(a)

    arr2 = [2, 20, 7, 55,
            1, 33, 12, 4]
    a = maxPerimeter(arr2)
    print(a)

    arr3 = [33, 6, 20, 1, 8,
            12, 5, 55, 4, 9]
    a = maxPerimeter(arr3)
    print(a)

if __name__=='__main__':
    main()

# This code is contributed
# by Pritha Upadhyay
```

## C#

```
// Efficient solution to find
// out maximum perimeter triangle which
// can be formed using the elements
// of the given array

using System;

class GFG {

// Function to find out maximum perimeter
    static void maxPerimeter(int[] arr, int n) {

        // sort the array elements
        // in reversed order
        arr = arrRevSort(arr);
        //sort(arr, arr+n, greater<int>());

        // initialize maximum
        // perimeter to 0
        int maxi = 0;

        // loop through the sorted array
        // and check whether it forms a
        // triangle or not.
        for (int i = 0; i < n - 2; i++) {

            // Check whether arr[i], arr[i+1]
            // and arr[i+2] forms a triangle
            // or not.
            if (arr[i] < arr[i + 1] + arr[i + 2]) {

                // if it forms a triangle then
                // it is the triangle with
                // maximum perimeter.
                maxi = Math.Max(maxi, arr[i] + arr[i + 1] + arr[i + 2]);
                break;
            }
        }

        // If maximum perimeter is non-zero
        // then print it.
        if (maxi > 0) {
            Console.WriteLine("Maximum Perimeter is: " + maxi);
        } // otherwise no triangle formation
        // is possible.
        else {
            Console.WriteLine("Triangle formation is not possible.");
        }
    }
    //Function return sorted array in Decreasing

    static int[] arrRevSort(int[] arr) {
        Array.Sort(arr);
        int j = arr.Length - 1;
        for (int i = 0; i < arr.Length / 2; i++, j--) {
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
        return arr;
    }

// Driver Program
    public static void Main() {
        // test case 1
        int[] arr1 = {6, 1, 6, 5, 8, 4};
        maxPerimeter(arr1, 6);

        // test case 2
        int[] arr2 = {2, 20, 7, 55, 1, 33, 12, 4};
        maxPerimeter(arr2, 8);

        // test case 3
        int[] arr3 = {33, 6, 20, 1, 8, 12, 5, 55, 4, 9};
        maxPerimeter(arr3, 10);
    }
}
/*This Java code is contributed by mits*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient solution to find out maximum
// perimeter triangle which can be formed
// using the elements of the given array

// Function to find out maximum perimeter
function maxPerimeter(&$arr, $n)
{

    // sort the array elements in
    // reversed order
    rsort($arr);

    // initialize maximum perimeter to 0
    $maxi = 0;

    // loop through the sorted array
    // and check whether it forms a
    // triangle or not.
    for ($i = 0; $i < $n - 2; $i++)
    {

        // Check whether arr[i], arr[i+1]
        // and arr[i+2] forms a triangle
        // or not.
        if ($arr[$i] < $arr[$i + 1] +
                       $arr[$i + 2])
        {

            // if it forms a triangle then
            // it is the triangle with
            // maximum perimeter.
            $maxi = max($maxi, $arr[$i] +
                               $arr[$i + 1] +
                               $arr[$i + 2]);
            break;
        }
    }

    // If maximum perimeter is non-zero
    // then print it.
    if ($maxi)
    {
        echo ("Maximum Perimeter is: ");
        echo ($maxi) ;
        echo ("\n");
    }

    // otherwise no triangle formation
    // is possible.
    else
    {
        echo ("Triangle formation ");
        echo ("is not possible.");
        echo ("\n");
    }
}

// Driver Code

// test case 1
$arr1 = array(6, 1, 6, 5, 8, 4);
$s = sizeof($arr1);
maxPerimeter($arr1, $s);

// test case 2
$arr2 = array(2, 20, 7, 55, 1,33, 12, 4);
$st = sizeof($arr2);
maxPerimeter($arr2, $st);

// test case 3
$arr3 = array(33, 6, 20, 1, 8,
              12, 5, 55, 4, 9);
$st1 = sizeof($arr3);
maxPerimeter($arr3, $st1);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>   
    // Efficient solution to find
    // out maximum perimeter triangle which
    // can be formed using the elements
    // of the given array

    // Function to find out maximum perimeter
    function maxPerimeter(arr, n){

        // sort the array elements
        // in reversed order
        arr.sort(function(a, b){return a - b});
        arr.reverse();

        // initialize maximum
        // perimeter to 0
        let maxi = 0;

        // loop through the sorted array
        // and check whether it forms a
        // triangle or not.
        for (let i = 0; i < n-2; i++){

            // Check whether arr[i], arr[i+1]
            // and arr[i+2] forms a triangle
            // or not.
            if (arr[i] < arr[i+1] + arr[i+2]){

                // if it forms a triangle then
                // it is the triangle with
                // maximum perimeter.
                maxi = Math.max(maxi, arr[i] + arr[i+1] + arr[i+2]);
                break;
            }
        }

        // If maximum perimeter is non-zero
        // then print it.
        if (maxi)
            document.write("Maximum Perimeter is: " + maxi + "</br>");

        // otherwise no triangle formation
        // is possible.
        else
            document.write("Triangle formation is not possible." + "</br>");
    }

    // test case 1
    let arr1 = [6, 1, 6, 5, 8, 4];
    maxPerimeter(arr1, 6);

    // test case 2
    let arr2 = [2, 20, 7, 55, 1, 33, 12, 4];
    maxPerimeter(arr2, 8);

    // test case 3
    let arr3 = [33, 6, 20, 1, 8, 12, 5, 55, 4, 9];
    maxPerimeter(arr3, 10);

</script>
```

**输出:**

```
Maximum Perimeter is: 20
Triangle formation is not possible.
Maximum Perimeter is: 41
```

这种方法的时间复杂度为 O(n*log(n))。对数组进行排序需要这么多时间。