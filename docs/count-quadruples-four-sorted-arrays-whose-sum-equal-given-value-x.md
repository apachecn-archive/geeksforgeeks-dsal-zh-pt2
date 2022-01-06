# 从四个排序数组中计数四倍，其和等于给定值 x

> 原文:[https://www . geesforgeks . org/count-四倍-四排序-数组-其和等于给定值-x/](https://www.geeksforgeeks.org/count-quadruples-four-sorted-arrays-whose-sum-equal-given-value-x/)

给定四个排序数组，每个数组大小为不同元素的 **n** 。给定值 **x** 。问题是从总和等于 **x** 的所有四个数组中计算所有**四倍**(四个数组)。
**注:**四重数组各有一个元素。

**示例:**

```
Input : arr1 = {1, 4, 5, 6},
        arr2 = {2, 3, 7, 8},
        arr3 = {1, 4, 6, 10},
        arr4 = {2, 4, 7, 8} 
        n = 4, x = 30
Output : 4
The quadruples are:
(4, 8, 10, 8), (5, 7, 10, 8),
(5, 8, 10, 7), (6, 7, 10, 7)

Input : For the same above given fours arrays
        x = 25
Output : 14
```

**方法 1(天真方法):**

使用四个嵌套循环生成所有四元组，并检查四元组中的元素总和是否达到 **x** 。

## C++

```

// C++ implementation to count quadruples from four sorted arrays
// whose sum is equal to a given value x
#include <bits/stdc++.h>

using namespace std;

// function to count all quadruples from
// four sorted arrays whose sum is equal
// to a given value x
int countQuadruples(int arr1[], int arr2[],
                    int arr3[], int arr4[], int n, int x)
{
    int count = 0;

    // generate all possible quadruples from
    // the four sorted arrays
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            for (int k = 0; k < n; k++)
                for (int l = 0; l < n; l++)
                    // check whether elements of
                    // quadruple sum up to x or not
                    if ((arr1[i] + arr2[j] + arr3[k] + arr4[l]) == x)
                        count++;

    // required count of quadruples
    return count;
}

// Driver program to test above
int main()
{
    // four sorted arrays each of size 'n'
    int arr1[] = { 1, 4, 5, 6 };
    int arr2[] = { 2, 3, 7, 8 };
    int arr3[] = { 1, 4, 6, 10 };
    int arr4[] = { 2, 4, 7, 8 };

    int n = sizeof(arr1) / sizeof(arr1[0]);
    int x = 30;
    cout << "Count = "
         << countQuadruples(arr1, arr2, arr3,
                            arr4, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count quadruples from four sorted arrays
// whose sum is equal to a given value x
class GFG {
// function to count all quadruples from
// four sorted arrays whose sum is equal
// to a given value x

    static int countQuadruples(int arr1[], int arr2[],
            int arr3[], int arr4[], int n, int x) {
        int count = 0;

        // generate all possible quadruples from
        // the four sorted arrays
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                for (int k = 0; k < n; k++) {
                    for (int l = 0; l < n; l++) // check whether elements of
                    // quadruple sum up to x or not
                    {
                        if ((arr1[i] + arr2[j] + arr3[k] + arr4[l]) == x) {
                            count++;
                        }
                    }
                }
            }
        }

        // required count of quadruples
        return count;
    }

// Driver program to test above
    public static void main(String[] args) {

        // four sorted arrays each of size 'n'
        int arr1[] = {1, 4, 5, 6};
        int arr2[] = {2, 3, 7, 8};
        int arr3[] = {1, 4, 6, 10};
        int arr4[] = {2, 4, 7, 8};

        int n = arr1.length;
        int x = 30;
        System.out.println("Count = "
                + countQuadruples(arr1, arr2, arr3,
                        arr4, n, x));

    }
}
//This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# A Python3 implementation to count
# quadruples from four sorted arrays
# whose sum is equal to a given value x

# function to count all quadruples
# from four sorted arrays whose sum
# is equal to a given value x
def countQuuadruples(arr1, arr2,
                     arr3, arr4, n, x):
    count = 0

    # generate all possible
    # quadruples from the four
    # sorted arrays
    for i in range(n):
        for j in range(n):
            for k in range(n):
                for l in range(n):

                    # check whether elements of
                    # quadruple sum up to x or not
                    if (arr1[i] + arr2[j] +
                        arr3[k] + arr4[l] == x):
                        count += 1

    # required count of quadruples
    return count

# Driver Code
arr1 = [1, 4, 5, 6]
arr2 = [2, 3, 7, 8]
arr3 = [1, 4, 6, 10]
arr4 = [2, 4, 7, 8 ]
n = len(arr1)
x = 30
print("Count = ", countQuuadruples(arr1, arr2,
                                   arr3, arr4, n, x))

# This code is contributed
# by Shrikant13
```

## C#

```
// C# implementation to count quadruples from four sorted arrays
// whose sum is equal to a given value x
using System;
public class GFG {
// function to count all quadruples from
// four sorted arrays whose sum is equal
// to a given value x

    static int countQuadruples(int []arr1, int []arr2,
            int []arr3, int []arr4, int n, int x) {
        int count = 0;

        // generate all possible quadruples from
        // the four sorted arrays
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                for (int k = 0; k < n; k++) {
                    for (int l = 0; l < n; l++) // check whether elements of
                    // quadruple sum up to x or not
                    {
                        if ((arr1[i] + arr2[j] + arr3[k] + arr4[l]) == x) {
                            count++;
                        }
                    }
                }
            }
        }

        // required count of quadruples
        return count;
    }

// Driver program to test above
    public static void Main() {

        // four sorted arrays each of size 'n'
        int []arr1 = {1, 4, 5, 6};
        int []arr2 = {2, 3, 7, 8};
        int []arr3 = {1, 4, 6, 10};
        int []arr4 = {2, 4, 7, 8};

        int n = arr1.Length;
        int x = 30;
        Console.Write("Count = "
                + countQuadruples(arr1, arr2, arr3,
                        arr4, n, x));

    }
}

// This code is contributed by PrinciRaj19992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count quadruples
// from four sorted arrays whose sum is
// equal to a given value x

// function to count all quadruples from
// four sorted arrays whose sum is equal
// to a given value x
function countQuadruples(&$arr1, &$arr2,
                         &$arr3, &$arr4,
                          $n, $x)
{
    $count = 0;

    // generate all possible quadruples
    // from the four sorted arrays
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $n; $j++)
            for ($k = 0; $k < $n; $k++)
                for ($l = 0; $l < $n; $l++)

                    // check whether elements of
                    // quadruple sum up to x or not
                    if (($arr1[$i] + $arr2[$j] +
                         $arr3[$k] + $arr4[$l]) == $x)
                        $count++;

    // required count of quadruples
    return $count;
}

// Driver Code

// four sorted arrays each of size 'n'
$arr1 = array( 1, 4, 5, 6 );
$arr2 = array( 2, 3, 7, 8 );
$arr3 = array( 1, 4, 6, 10 );
$arr4 = array( 2, 4, 7, 8 );

$n = sizeof($arr1);
$x = 30;
echo "Count = " . countQuadruples($arr1, $arr2, $arr3,
                                       $arr4, $n, $x);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript implementation to count quadruples from four sorted arrays
// whose sum is equal to a given value x

    // function to count all quadruples from
// four sorted arrays whose sum is equal
// to a given value x
    function countQuadruples(arr1,arr2,arr3,arr4,n,x)
    {
        let count = 0;

        // generate all possible quadruples from
        // the four sorted arrays
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < n; j++) {
                for (let k = 0; k < n; k++) {
                    for (let l = 0; l < n; l++) // check whether elements of
                    // quadruple sum up to x or not
                    {
                        if ((arr1[i] + arr2[j] + arr3[k] + arr4[l]) == x) {
                            count++;
                        }
                    }
                }
            }
        }

        // required count of quadruples
        return count;
    }

    // Driver program to test above
    let arr1=[1, 4, 5, 6];
    let arr2=[2, 3, 7, 8];
    let arr3=[1, 4, 6, 10];
    let arr4=[2, 4, 7, 8];
    let n = arr1.length;
    let x = 30;
    document.write("Count = "
                + countQuadruples(arr1, arr2, arr3,
                        arr4, n, x));

    //This code is contributed by rag2127

</script>
```

**输出:**

```
Count = 4
```

**时间复杂度:**O(n<sup>4</sup>)
T5】辅助空间: O(1)

**方法 2(二分搜索法):**从前三个数组生成所有三元组。对于这样生成的每个三元组，求该三元组中元素的和。让它成为 **T** 。现在，在第四个数组中搜索值**(x–T)**。如果在第四个数组中找到该值，则递增**计数**。对从前三个数组生成的所有三元组重复这个过程。

## C++

```
// C++ implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x
#include <bits/stdc++.h>

using namespace std;

// find the 'value' in the given array 'arr[]'
// binary search technique is applied
bool isPresent(int arr[], int low, int high, int value)
{
    while (low <= high) {
        int mid = (low + high) / 2;

        // 'value' found
        if (arr[mid] == value)
            return true;
        else if (arr[mid] > value)
            high = mid - 1;
        else
            low = mid + 1;
    }

    // 'value' not found
    return false;
}

// function to count all quadruples from four
// sorted arrays whose sum is equal to a given value x
int countQuadruples(int arr1[], int arr2[], int arr3[],
                    int arr4[], int n, int x)
{
    int count = 0;

    // generate all triplets from the 1st three arrays
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            for (int k = 0; k < n; k++) {

                // calculate the sum of elements in
                // the triplet so generated
                int T = arr1[i] + arr2[j] + arr3[k];

                // check if 'x-T' is present in 4th
                // array or not
                if (isPresent(arr4, 0, n, x - T))

                    // increment count
                    count++;
            }

    // required count of quadruples
    return count;
}

// Driver program to test above
int main()
{
    // four sorted arrays each of size 'n'
    int arr1[] = { 1, 4, 5, 6 };
    int arr2[] = { 2, 3, 7, 8 };
    int arr3[] = { 1, 4, 6, 10 };
    int arr4[] = { 2, 4, 7, 8 };

    int n = sizeof(arr1) / sizeof(arr1[0]);
    int x = 30;
    cout << "Count = "
         << countQuadruples(arr1, arr2, arr3, arr4, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x
class GFG
{

    // find the 'value' in the given array 'arr[]'
    // binary search technique is applied
    static boolean isPresent(int[] arr, int low,
                            int high, int value)
    {
        while (low <= high)
        {
            int mid = (low + high) / 2;

            // 'value' found
            if (arr[mid] == value)
                return true;
            else if (arr[mid] > value)
                high = mid - 1;
            else
                low = mid + 1;
        }

        // 'value' not found
        return false;
    }

    // function to count all quadruples from four
    // sorted arrays whose sum is equal to a given value x
    static int countQuadruples(int[] arr1, int[] arr2,
                               int[] arr3, int[] arr4,
                               int n, int x)
    {
        int count = 0;

        // generate all triplets from the 1st three arrays
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                for (int k = 0; k < n; k++)
                {

                    // calculate the sum of elements in
                    // the triplet so generated
                    int T = arr1[i] + arr2[j] + arr3[k];

                    // check if 'x-T' is present in 4th
                    // array or not
                    if (isPresent(arr4, 0, n-1, x - T))

                        // increment count
                        count++;
                }

        // required count of quadruples
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        // four sorted arrays each of size 'n'
        int[] arr1 = { 1, 4, 5, 6 };
        int[] arr2 = { 2, 3, 7, 8 };
        int[] arr3 = { 1, 4, 6, 10 };
        int[] arr4 = { 2, 4, 7, 8 };
        int n = 4;
        int x = 30;
        System.out.println( "Count = "
        + countQuadruples(arr1, arr2, arr3, arr4, n, x));
    }
}

// This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x
using System;

class GFG
{

    // find the 'value' in the given array 'arr[]'
    // binary search technique is applied
    static bool isPresent(int[] arr, int low,
                            int high, int value)
    {
        while (low <= high)
        {
            int mid = (low + high) / 2;

            // 'value' found
            if (arr[mid] == value)
                return true;
            else if (arr[mid] > value)
                high = mid - 1;
            else
                low = mid + 1;
        }

        // 'value' not found
        return false;
    }

    // function to count all quadruples from four
    // sorted arrays whose sum is equal to a given value x
    static int countQuadruples(int[] arr1, int[] arr2,
                            int[] arr3, int[] arr4,
                            int n, int x)
    {
        int count = 0;

        // generate all triplets from the 1st three arrays
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                for (int k = 0; k < n; k++)
                {

                    // calculate the sum of elements in
                    // the triplet so generated
                    int T = arr1[i] + arr2[j] + arr3[k];

                    // check if 'x-T' is present in 4th
                    // array or not
                    if (isPresent(arr4, 0, n-1, x - T))

                        // increment count
                        count++;
                }

        // required count of quadruples
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // four sorted arrays each of size 'n'
        int[] arr1 = { 1, 4, 5, 6 };
        int[] arr2 = { 2, 3, 7, 8 };
        int[] arr3 = { 1, 4, 6, 10 };
        int[] arr4 = { 2, 4, 7, 8 };
        int n = 4;
        int x = 30;
        Console.WriteLine( "Count = "
        + countQuadruples(arr1, arr2, arr3, arr4, n, x));
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x

// find the 'value' in the given array 'arr[]'
// binary search technique is applied
function isPresent($arr, $low, $high, $value)
{
    while ($low <= $high)
    {
        $mid = ($low + $high) / 2;

        // 'value' found
        if ($arr[$mid] == $value)
            return true;
        else if ($arr[$mid] > $value)
            $high = $mid - 1;
        else
            $low = $mid + 1;
    }

    // 'value' not found
    return false;
}

// function to count all quadruples from
// four sorted arrays whose sum is equal
// to a given value x
function countQuadruples($arr1, $arr2, $arr3,
                         $arr4, $n, $x)
{
    $count = 0;

    // generate all triplets from the
    // 1st three arrays
    for ($i = 0; $i < $n; $i++)
        for ($j = 0; $j < $n; $j++)
            for ($k = 0; $k < $n; $k++)
            {

                // calculate the sum of elements in
                // the triplet so generated
                $T = $arr1[$i] + $arr2[$j] + $arr3[$k];

                // check if 'x-T' is present in 4th
                // array or not
                if (isPresent($arr4, 0, $n, $x - $T))

                    // increment count
                    $count++;
            }

    // required count of quadruples
    return $count;
}

// Driver Code

// four sorted arrays each of size 'n'
$arr1 = array(1, 4, 5, 6);
$arr2 = array(2, 3, 7, 8);
$arr3 = array(1, 4, 6, 10);
$arr4 = array(2, 4, 7, 8);

$n = sizeof($arr1);
$x = 30;
echo "Count = " . countQuadruples($arr1, $arr2, $arr3,
                                  $arr4, $n, $x);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
    // Javascript implementation to count quadruples from
    // four sorted arrays whose sum is equal to a
    // given value x

    // find the 'value' in the given array 'arr[]'
    // binary search technique is applied
    function isPresent(arr, low, high, value)
    {
        while (low <= high)
        {
            let mid = parseInt((low + high) / 2, 10);

            // 'value' found
            if (arr[mid] == value)
                return true;
            else if (arr[mid] > value)
                high = mid - 1;
            else
                low = mid + 1;
        }

        // 'value' not found
        return false;
    }

    // function to count all quadruples from four
    // sorted arrays whose sum is equal to a given value x
    function countQuadruples(arr1, arr2, arr3, arr4, n, x)
    {
        let count = 0;

        // generate all triplets from the 1st three arrays
        for (let i = 0; i < n; i++)
            for (let j = 0; j < n; j++)
                for (let k = 0; k < n; k++)
                {

                    // calculate the sum of elements in
                    // the triplet so generated
                    let T = arr1[i] + arr2[j] + arr3[k];

                    // check if 'x-T' is present in 4th
                    // array or not
                    if (isPresent(arr4, 0, n-1, x - T))

                        // increment count
                        count++;
                }

        // required count of quadruples
        return count;
    }

    // four sorted arrays each of size 'n'
    let arr1 = [ 1, 4, 5, 6 ];
    let arr2 = [ 2, 3, 7, 8 ];
    let arr3 = [ 1, 4, 6, 10 ];
    let arr4 = [ 2, 4, 7, 8 ];
    let n = 4;
    let x = 30;
    document.write( "Count = " + countQuadruples(arr1, arr2, arr3, arr4, n, x));

</script>
```

**输出:**

```
Count = 4
```

**时间复杂度:**O(n<sup>3</sup>logn)
T5】辅助空间: O(1)

**方法 3(使用两个指针):**从前两个数组生成所有对。对于这样生成的每一对，求该对中元素的和。让它成为 **p_sum** 。对于每个 **p_sum** ，[从第 3 个和第 4 个排序数组中计数对，其和等于**(x–p _ sum)**](https://www.geeksforgeeks.org/count-pairs-two-sorted-arrays-whose-sum-equal-given-value-x/)。将这些计数累加到四倍的 **total_count** 中。

## C++

```
// C++ implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x
#include <bits/stdc++.h>

using namespace std;

// count pairs from the two sorted array whose sum
// is equal to the given 'value'
int countPairs(int arr1[], int arr2[], int n, int value)
{
    int count = 0;
    int l = 0, r = n - 1;

    // traverse 'arr1[]' from left to right
    // traverse 'arr2[]' from right to left
    while (l < n & amp; &r >= 0) {
        int sum = arr1[l] + arr2[r];

        // if the 'sum' is equal to 'value', then
        // increment 'l', decrement 'r' and
        // increment 'count'
        if (sum == value) {
            l++, r--;
            count++;
        }

        // if the 'sum' is greater than 'value', then
        // decrement r
        else if (sum > value)
            r--;

        // else increment l
        else
            l++;
    }

    // required count of pairs
    return count;
}

// function to count all quadruples from four sorted arrays
// whose sum is equal to a given value x
int countQuadruples(int arr1[], int arr2[], int arr3[],
                    int arr4[], int n, int x)
{
    int count = 0;

    // generate all pairs from arr1[] and arr2[]
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {
            // calculate the sum of elements in
            // the pair so generated
            int p_sum = arr1[i] + arr2[j];

            // count pairs in the 3rd and 4th array
            // having value 'x-p_sum' and then
            // accumulate it to 'count'
            count += countPairs(arr3, arr4, n, x - p_sum);
        }

    // required count of quadruples
    return count;
}

// Driver program to test above
int main()
{
    // four sorted arrays each of size 'n'
    int arr1[] = { 1, 4, 5, 6 };
    int arr2[] = { 2, 3, 7, 8 };
    int arr3[] = { 1, 4, 6, 10 };
    int arr4[] = { 2, 4, 7, 8 };

    int n = sizeof(arr1) / sizeof(arr1[0]);
    int x = 30;
    cout << "Count = "
         << countQuadruples(arr1, arr2, arr3,
                            arr4, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x

class GFG {

// count pairs from the two sorted array whose sum
// is equal to the given 'value'
static int countPairs(int arr1[], int arr2[], int n, int value)
{
    int count = 0;
    int l = 0, r = n - 1;

    // traverse 'arr1[]' from left to right
    // traverse 'arr2[]' from right to left
    while (l < n & r >= 0) {
        int sum = arr1[l] + arr2[r];

        // if the 'sum' is equal to 'value', then
        // increment 'l', decrement 'r' and
        // increment 'count'
        if (sum == value) {
            l++; r--;
            count++;
        }

        // if the 'sum' is greater than 'value', then
        // decrement r
        else if (sum > value)
            r--;

        // else increment l
        else
            l++;
    }

    // required count of pairs
    return count;
}

// function to count all quadruples from four sorted arrays
// whose sum is equal to a given value x
static int countQuadruples(int arr1[], int arr2[], int arr3[],
                    int arr4[], int n, int x)
{
    int count = 0;

    // generate all pairs from arr1[] and arr2[]
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++) {
            // calculate the sum of elements in
            // the pair so generated
            int p_sum = arr1[i] + arr2[j];

            // count pairs in the 3rd and 4th array
            // having value 'x-p_sum' and then
            // accumulate it to 'count'
            count += countPairs(arr3, arr4, n, x - p_sum);
        }

    // required count of quadruples
    return count;
}
// Driver program to test above
    static public void main(String[] args) {
        // four sorted arrays each of size 'n'
        int arr1[] = {1, 4, 5, 6};
        int arr2[] = {2, 3, 7, 8};
        int arr3[] = {1, 4, 6, 10};
        int arr4[] = {2, 4, 7, 8};

        int n = arr1.length;
        int x = 30;
        System.out.println("Count = "
                + countQuadruples(arr1, arr2, arr3, arr4, n, x));
    }
}

// This code is contributed by PrinciRaj19992
```

## 蟒蛇 3

```
# Python3 implementation to
# count quadruples from four
# sorted arrays whose sum is
# equal to a given value x
# count pairs from the two
# sorted array whose sum
# is equal to the given 'value'
def countPairs(arr1, arr2,
               n, value):

     count = 0
     l = 0
     r = n - 1

     # traverse 'arr1[]' from
     # left to right
     # traverse 'arr2[]' from
     # right to left
     while (l < n and r >= 0):
          sum = arr1[l] + arr2[r]

          # if the 'sum' is equal
          # to 'value', then
          # increment 'l', decrement
          # 'r' and increment 'count'
          if (sum == value):
               l += 1
               r -= 1
               count += 1

               # if the 'sum' is greater
               # than 'value', then decrement r
          elif (sum > value):
               r -= 1

          # else increment l
          else:
               l += 1

     # required count of pairs
     # print(count)
     return count

# function to count all quadruples
# from four sorted arrays whose sum
# is equal to a given value x
def countQuadruples(arr1, arr2,
                    arr3, arr4,
                    n, x):
     count = 0

     # generate all pairs from
     # arr1[] and arr2[]
     for i in range(0, n):
          for j in range(0, n):

               # calculate the sum of
               # elements in the pair
               # so generated
               p_sum = arr1[i] + arr2[j]

               # count pairs in the 3rd
               # and 4th array having
               # value 'x-p_sum' and then
               # accumulate it to 'count
               count += int(countPairs(arr3, arr4,
                                       n, x - p_sum))
     # required count of quadruples
     return count

# Driver code
arr1 = [1, 4, 5, 6]
arr2 = [2, 3, 7, 8]
arr3 = [1, 4, 6, 10]
arr4 = [2, 4, 7, 8]
n = len(arr1)
x = 30
print("Count = ", countQuadruples(arr1, arr2,
                                  arr3, arr4,
                                  n, x))

# This code is contributed by Stream_Cipher
```

## C#

```

// C# implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x
 using System;
public class GFG {

    // count pairs from the two sorted array whose sum
    // is equal to the given 'value'
    static int countPairs(int []arr1, int []arr2, int n, int value)
    {
        int count = 0;
        int l = 0, r = n - 1;

        // traverse 'arr1[]' from left to right
        // traverse 'arr2[]' from right to left
        while (l < n & r >= 0) {
            int sum = arr1[l] + arr2[r];

            // if the 'sum' is equal to 'value', then
            // increment 'l', decrement 'r' and
            // increment 'count'
            if (sum == value) {
                l++; r--;
                count++;
            }

            // if the 'sum' is greater than 'value', then
            // decrement r
            else if (sum > value)
                r--;

            // else increment l
            else
                l++;
        }

        // required count of pairs
        return count;
    }

    // function to count all quadruples from four sorted arrays
    // whose sum is equal to a given value x
    static int countQuadruples(int []arr1, int []arr2, int []arr3,
                        int []arr4, int n, int x)
    {
        int count = 0;

        // generate all pairs from arr1[] and arr2[]
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++) {
                // calculate the sum of elements in
                // the pair so generated
                int p_sum = arr1[i] + arr2[j];

                // count pairs in the 3rd and 4th array
                // having value 'x-p_sum' and then
                // accumulate it to 'count'
                count += countPairs(arr3, arr4, n, x - p_sum);
            }

        // required count of quadruples
        return count;
    }
    // Driver program to test above
    static public void Main() {
        // four sorted arrays each of size 'n'
        int []arr1 = {1, 4, 5, 6};
        int []arr2 = {2, 3, 7, 8};
        int []arr3 = {1, 4, 6, 10};
        int []arr4 = {2, 4, 7, 8};

        int n = arr1.Length;
        int x = 30;
        Console.Write("Count = "
                + countQuadruples(arr1, arr2, arr3, arr4, n, x));
    }
}

// This code is contributed by PrinciRaj19992
```

## java 描述语言

```
<script>
// Javascript implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x

// count pairs from the two sorted array whose sum
// is equal to the given 'value'
function countPairs(arr1,arr2,n,value)
{
    let count = 0;
    let l = 0, r = n - 1;

    // traverse 'arr1[]' from left to right
    // traverse 'arr2[]' from right to left
    while (l < n & r >= 0) {
        let sum = arr1[l] + arr2[r];

        // if the 'sum' is equal to 'value', then
        // increment 'l', decrement 'r' and
        // increment 'count'
        if (sum == value) {
            l++; r--;
            count++;
        }

        // if the 'sum' is greater than 'value', then
        // decrement r
        else if (sum > value)
            r--;

        // else increment l
        else
            l++;
    }

    // required count of pairs
    return count;
}

// function to count all quadruples from four sorted arrays
// whose sum is equal to a given value x
function countQuadruples(arr1,arr2,arr3,arr4,n,x)
{
    let count = 0;

    // generate all pairs from arr1[] and arr2[]
    for (let i = 0; i < n; i++)
        for (let j = 0; j < n; j++) {
            // calculate the sum of elements in
            // the pair so generated
            let p_sum = arr1[i] + arr2[j];

            // count pairs in the 3rd and 4th array
            // having value 'x-p_sum' and then
            // accumulate it to 'count'
            count += countPairs(arr3, arr4, n, x - p_sum);
        }

    // required count of quadruples
    return count;
}

// Driver program to test above
// four sorted arrays each of size 'n'
let arr1=[1, 4, 5, 6];
let arr2=[2, 3, 7, 8];
let arr3=[1, 4, 6, 10];
let arr4=[2, 4, 7, 8];
let n = arr1.length;
let x = 30;
document.write("Count = "
                + countQuadruples(arr1, arr2, arr3, arr4, n, x));

// This code is contributed by ab2127
</script>
```

**输出:**

```
Count = 4
```

**时间复杂度:**O(n<sup>3</sup>)
T5】辅助空间: O(1)

**方法 4 高效方法(哈希):**创建哈希表，其中**(键，值)**元组表示为**(和，频率)**元组。这里，总和是从第一和第二阵列对获得的，它们的频率计数保存在散列表中。哈希表使用 C++中的[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)实现。现在，从第三个和第四个数组中生成所有对。对于这样生成的每一对，求该对中元素的和。让它成为 **p_sum** 。对于每个 **p_sum** ，检查哈希表中是否存在**(x–p _ sum)**。如果存在，则将**(x–p _ sum)**的频率加到四倍的**计数**上。

## C++

```
// C++ implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x
#include <bits/stdc++.h>

using namespace std;

// function to count all quadruples from four sorted
// arrays whose sum is equal to a given value x
int countQuadruples(int arr1[], int arr2[], int arr3[],
                    int arr4[], int n, int x)
{
    int count = 0;

    // unordered_map 'um' implemented as hash table
    // for <sum, frequency> tuples
    unordered_map<int, int> um;

    // count frequency of each sum obtained from the
    // pairs of arr1[] and arr2[] and store them in 'um'
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            um[arr1[i] + arr2[j]]++;

    // generate pair from arr3[] and arr4[]
    for (int k = 0; k < n; k++)
        for (int l = 0; l < n; l++) {

            // calculate the sum of elements in
            // the pair so generated
            int p_sum = arr3[k] + arr4[l];

            // if 'x-p_sum' is present in 'um' then
            // add frequency of 'x-p_sum' to 'count'
            if (um.find(x - p_sum) != um.end())
                count += um[x - p_sum];
        }

    // required count of quadruples
    return count;
}

// Driver program to test above
int main()
{
    // four sorted arrays each of size 'n'
    int arr1[] = { 1, 4, 5, 6 };
    int arr2[] = { 2, 3, 7, 8 };
    int arr3[] = { 1, 4, 6, 10 };
    int arr4[] = { 2, 4, 7, 8 };

    int n = sizeof(arr1) / sizeof(arr1[0]);
    int x = 30;
    cout << "Count = "
         << countQuadruples(arr1, arr2, arr3, arr4, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x
import java.util.*;

class GFG
{

// function to count all quadruples from four sorted
// arrays whose sum is equal to a given value x
static int countQuadruples(int arr1[], int arr2[], int arr3[],
                                    int arr4[], int n, int x)
{
    int count = 0;

    // unordered_map 'um' implemented as hash table
    // for <sum, frequency> tuples
    Map<Integer,Integer> m = new HashMap<>();

    // count frequency of each sum obtained from the
    // pairs of arr1[] and arr2[] and store them in 'um'
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            if(m.containsKey(arr1[i] + arr2[j]))
                m.put((arr1[i] + arr2[j]), m.get((arr1[i] + arr2[j]))+1);
            else
                m.put((arr1[i] + arr2[j]), 1);

    // generate pair from arr3[] and arr4[]
    for (int k = 0; k < n; k++)
        for (int l = 0; l < n; l++)
        {

            // calculate the sum of elements in
            // the pair so generated
            int p_sum = arr3[k] + arr4[l];

            // if 'x-p_sum' is present in 'um' then
            // add frequency of 'x-p_sum' to 'count'
            if (m.containsKey(x - p_sum))
                count += m.get(x - p_sum);
        }

    // required count of quadruples
    return count;
}

// Driver program to test above
public static void main(String[] args)
{
    // four sorted arrays each of size 'n'
    int arr1[] = { 1, 4, 5, 6 };
    int arr2[] = { 2, 3, 7, 8 };
    int arr3[] = { 1, 4, 6, 10 };
    int arr4[] = { 2, 4, 7, 8 };

    int n = arr1.length;
    int x = 30;
    System.out.println("Count = "
        + countQuadruples(arr1, arr2, arr3, arr4, n, x));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation to count quadruples from
# four sorted arrays whose sum is equal to a
# given value x

# function to count all quadruples from four sorted
# arrays whose sum is equal to a given value x
def countQuadruples(arr1, arr2, arr3, arr4, n, x):
    count = 0

    # unordered_map 'um' implemented as hash table
    # for <sum, frequency> tuples  
    m = {}

    # count frequency of each sum obtained from the
    # pairs of arr1[] and arr2[] and store them in 'um'
    for i in range(n):
        for j in range(n):
            if (arr1[i] + arr2[j]) in m:
                m[arr1[i] + arr2[j]] += 1
            else:
                m[arr1[i] + arr2[j]] = 1

    # generate pair from arr3[] and arr4[]
    for k in range(n):
        for l in range(n):

            # calculate the sum of elements in
            # the pair so generated
            p_sum = arr3[k] + arr4[l]

            # if 'x-p_sum' is present in 'um' then
            # add frequency of 'x-p_sum' to 'count'
            if (x - p_sum) in m:
                count += m[x - p_sum]

    # required count of quadruples
    return count

# Driver program to test above

# four sorted arrays each of size 'n'
arr1 = [1, 4, 5, 6]
arr2 = [2, 3, 7, 8 ]
arr3 = [1, 4, 6, 10]
arr4 = [2, 4, 7, 8 ]

n = len(arr1)
x = 30
print("Count =", countQuadruples(arr1, arr2, arr3, arr4, n, x))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x
using System;
using System.Collections.Generic;

class GFG
{

// function to count all quadruples from four sorted
// arrays whose sum is equal to a given value x
static int countQuadruples(int []arr1, int []arr2, int []arr3,
                                    int []arr4, int n, int x)
{
    int count = 0;

    // unordered_map 'um' implemented as hash table
    // for <sum, frequency> tuples
    Dictionary<int,int> m = new Dictionary<int,int>();

    // count frequency of each sum obtained from the
    // pairs of arr1[] and arr2[] and store them in 'um'
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            if(m.ContainsKey(arr1[i] + arr2[j])){
                var val = m[arr1[i] + arr2[j]];
                m.Remove(arr1[i] + arr2[j]);
                m.Add((arr1[i] + arr2[j]), val+1);
            }
            else
                m.Add((arr1[i] + arr2[j]), 1);

    // generate pair from arr3[] and arr4[]
    for (int k = 0; k < n; k++)
        for (int l = 0; l < n; l++)
        {

            // calculate the sum of elements in
            // the pair so generated
            int p_sum = arr3[k] + arr4[l];

            // if 'x-p_sum' is present in 'um' then
            // add frequency of 'x-p_sum' to 'count'
            if (m.ContainsKey(x - p_sum))
                count += m[x - p_sum];
        }

    // required count of quadruples
    return count;
}

// Driver code
public static void Main(String[] args)
{
    // four sorted arrays each of size 'n'
    int []arr1 = { 1, 4, 5, 6 };
    int []arr2 = { 2, 3, 7, 8 };
    int []arr3 = { 1, 4, 6, 10 };
    int []arr4 = { 2, 4, 7, 8 };

    int n = arr1.Length;
    int x = 30;
    Console.WriteLine("Count = "
        + countQuadruples(arr1, arr2, arr3, arr4, n, x));
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation to count quadruples from
// four sorted arrays whose sum is equal to a
// given value x

// function to count all quadruples from four sorted
// arrays whose sum is equal to a given value x
function countQuadruples(arr1,arr2,arr3,arr4,n,X)
{
    let count = 0;

    // unordered_map 'um' implemented as hash table
    // for <sum, frequency> tuples
    let m = new Map();

    // count frequency of each sum obtained from the
    // pairs of arr1[] and arr2[] and store them in 'um'
    for (let i = 0; i < n; i++)
        for (let j = 0; j < n; j++)
            if(m.has(arr1[i] + arr2[j]))
                m.set((arr1[i] + arr2[j]), m.get((arr1[i] + arr2[j]))+1);
            else
                m.set((arr1[i] + arr2[j]), 1);

    // generate pair from arr3[] and arr4[]
    for (let k = 0; k < n; k++)
        for (let l = 0; l < n; l++)
        {

            // calculate the sum of elements in
            // the pair so generated
            let p_sum = arr3[k] + arr4[l];

            // if 'x-p_sum' is present in 'um' then
            // add frequency of 'x-p_sum' to 'count'
            if (m.has(x - p_sum))
                count += m.get(x - p_sum);
        }

    // required count of quadruples
    return count;
}

// Driver program to test above
// four sorted arrays each of size 'n'
let arr1 = [ 1, 4, 5, 6 ];
let arr2 = [ 2, 3, 7, 8 ];
let arr3 = [ 1, 4, 6, 10 ];
let arr4 = [ 2, 4, 7, 8 ];

let n = arr1.length;
let x = 30;
document.write("Count = "
                   + countQuadruples(arr1, arr2, arr3, arr4, n, x));

// This code is contributed by unknown2108
</script>
```

**输出:**

```
Count = 4
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n <sup>2</sup>

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
对第 3 个和第 4 个排序数组中的对进行计数，总和等于**(x–p _ sum)**
如果您发现任何不正确的地方，或者您想分享关于上面讨论的主题的更多信息，请写评论。