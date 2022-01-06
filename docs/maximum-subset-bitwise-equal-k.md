# 按位“或”等于 k 的最大子集

> 原文:[https://www . geesforgeks . org/maximum-subset-bitwise-equal-k/](https://www.geeksforgeeks.org/maximum-subset-bitwise-equal-k/)

给定一个非负整数数组和一个整数 k，求按位 OR 等于 k 的最大长度子集。

**示例:**

```
Input : arr[] = [1, 4, 2]
        k = 3
Output : [1, 2]
Explanation: The bitwise OR of 
1 and 2 equals 3\. It is not possible to obtain 
a subset of length greater than 2.

Input : arr[] = [1, 2, 5]
        k = 4
Output : []
No subset's bitwise OR equals 4\. 
```

**方法 1(简单):**
天真的方法是考虑所有子集。考虑子集时，计算其按位“或”。如果它等于 k，将子集的长度与迄今为止的最大长度进行比较，并在需要时更新最大长度。

**方法 2(有效):**
0 OR 0 = 0
1 OR 0 = 1
1 OR 1 = 1
因此，对于比特等于 0 的 k 的二进制表示中的所有位置，所得到的子集中所有元素的二进制表示中的对应位置应该必然是 0。
另一方面，对于 k 中位等于 1 的位置，必须至少有一个元素在对应位置带有 1。其余元素在该位置可以有 0 或 1。没关系。
因此，要获得结果子集，遍历初始数组。在决定元素是否应该在结果子集中时，检查 k 的二进制表示中是否有任何位置为 0，并且该元素中的对应位置为 1。如果存在这样的位置，则忽略该元素，否则将其包含在结果子集中。
如何确定 k 的二进制表示中是否存在位置为 0，元素中对应的位置为 1？
只需对 k 和该元素进行按位“或”运算。如果它不等于 k，那么就存在这样一个位置，这个元素必须被忽略。如果它们的按位“或”等于 k，则在结果子集中包含当前元素。
最后一步是确定是否至少有一个元素在 k 的相应位置上有 1，在 k 的相应位置上有 1。
只需计算结果子集的按位或即可。如果它等于 k，那么这就是最终答案。否则不存在满足条件的子集。

## C++

```
// CPP Program to find the maximum subset
// with bitwise OR equal to k
#include <bits/stdc++.h>
using namespace std;

// function to find the maximum subset with
// bitwise OR equal to k
void subsetBitwiseORk(int arr[], int n, int k)
{
    vector<int> v;

    for (int i = 0; i < n; i++) {

        // If the bitwise OR of k and element
        // is equal to k, then include that element
        // in the subset
        if ((arr[i] | k) == k)
            v.push_back(arr[i]);
    }

    // Store the bitwise OR of elements in v
    int ans = 0;

    for (int i = 0; i < v.size(); i++)
        ans |= v[i];

    // If ans is not equal to k, subset doesn't exist
    if (ans != k) {
        cout << "Subset does not exist" << endl;
        return;
    }

    for (int i = 0; i < v.size(); i++)
        cout << v[i] << ' ';
}

// Driver Code
int main()
{
    int k = 3;
    int arr[] = { 1, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    subsetBitwiseORk(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the maximum subset
// with bitwise OR equal to k
import java.util.*;

class GFG {

    // function to find the maximum subset
    // with bitwise OR equal to k
    static void subsetBitwiseORk(int arr[],
                              int n, int k)
    {
        ArrayList<Integer> v =
                  new ArrayList<Integer>();

        for (int i = 0; i < n; i++) {

            // If the bitwise OR of k and
            // element is equal to k, then
            // include that element in the
            // subset
            if ((arr[i] | k) == k){
                v.add(arr[i]);
            }
        }

        // Store the bitwise OR of elements
        // in v
        int ans = 0;

        for (int i = 0; i < v.size(); i++)
            ans = ans|v.get(i);

        // If ans is not equal to k, subset
        // doesn't exist
        if (ans != k) {
            System.out.println("Subset does"
                           + " not exist" );
            return;
        }

        for (int i = 0; i < v.size(); i++)
            System.out.print(v.get(i) + " " );
    }

    // main function
    public static void main(String[] args)
    {
        int k = 3;
        int arr[] = { 1, 4, 2 };
        int n = arr.length;

        subsetBitwiseORk(arr, n, k);

    }
}

// This code is contributed by Arnab Kundu.
```

## 蟒蛇 3

```
# Python3 Program to find the
# maximum subset with bitwise
# OR equal to k

# function to find the maximum
# subset with bitwise OR equal to k
def subsetBitwiseORk(arr, n, k) :
    v = []

    for i in range(0, n) :
        # If the bitwise OR of k
        # and element is equal to k,
        # then include that element
        # in the subset
        if ((arr[i] | k) == k) :
            v.append(arr[i])

    # Store the bitwise OR
    # of elements in v
    ans = 0

    for i in range(0, len(v)) :
        ans |= v[i]

    # If ans is not equal to
    # k, subset doesn't exist
    if (ans != k) :
        print ("Subset does not exist\n")
        return

    for i in range(0, len(v)) :
        print ("{} ".format(v[i]), end="")

# Driver Code
k = 3
arr = [1, 4, 2]
n = len(arr)

subsetBitwiseORk(arr, n, k)

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# Program to find the maximum subset
// with bitwise OR equal to k
using System;
using System.Collections;

class GFG {

    // function to find the maximum subset
    // with bitwise OR equal to k
    static void subsetBitwiseORk(int []arr,
                              int n, int k)
    {
        ArrayList v = new ArrayList();

        for (int i = 0; i < n; i++) {

            // If the bitwise OR of k and
            // element is equal to k, then
            // include that element in the
            // subset
            if ((arr[i] | k) == k){
                v.Add(arr[i]);
            }
        }

        // Store the bitwise OR of
        // elements in v
        int ans = 0;

        for (int i = 0; i < v.Count; i++)
            ans = ans|(int)v[i];

        // If ans is not equal to k, subset
        // doesn't exist
        if (ans != k) {
            Console.WriteLine("Subset does"
                          + " not exist" );
            return;
        }

        for (int i = 0; i < v.Count; i++)
            Console.Write((int)v[i] + " " );
    }

    // main function
    static public void Main(String []args)
    {
        int k = 3;
        int []arr = { 1, 4, 2 };
        int n = arr.Length;

        subsetBitwiseORk(arr, n, k);

    }
}

// This code is contributed by Arnab Kundu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the
// maximum subset with bitwise
// OR equal to k

// function to find the maximum
// subset with bitwise OR equal to k
function subsetBitwiseORk($arr, $n, $k)
{
    $v = array();

    for ($i = 0; $i < $n; $i++)
    {

        // If the bitwise OR of k
        // and element is equal to k,
        // then include that element
        // in the subset
        if (($arr[$i] | $k) == $k)
            array_push($v, $arr[$i]);
    }

    // Store the bitwise OR
    // of elements in v
    $ans = 0;

    for ($i = 0; $i < count($v); $i++)
        $ans |= $v[$i];

    // If ans is not equal to
    // k, subset doesn't exist
    if ($ans != $k)
    {
        echo ("Subset does not exist\n");
        return;
    }

    for ($i = 0; $i < count($v); $i++)
        echo ($v[$i]." ");
}

// Driver Code
$k = 3;
$arr = array(1, 4, 2);
$n = count($arr);

subsetBitwiseORk($arr, $n, $k);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript Program to find the maximum subset
// with bitwise OR equal to k

// function to find the maximum subset with
// bitwise OR equal to k
function subsetBitwiseORk(arr, n, k)
{
    var v = [];

    for (var i = 0; i < n; i++) {

        // If the bitwise OR of k and element
        // is equal to k, then include that element
        // in the subset
        if ((arr[i] | k) == k)
            v.push(arr[i]);
    }

    // Store the bitwise OR of elements in v
    var ans = 0;

    for (var i = 0; i < v.length; i++)
        ans |= v[i];

    // If ans is not equal to k, subset doesn't exist
    if (ans != k) {
        document.write( "Subset does not exist" );
        return;
    }

    for (var i = 0; i < v.length; i++)
        document.write( v[i] + ' ');
}

// Driver Code
var k = 3;
var arr = [1, 4, 2];
var n = arr.length;
subsetBitwiseORk(arr, n, k);

</script>
```

**输出:**

```
1 2
```

**时间复杂度:** O(N)，其中 N 是数组的大小。