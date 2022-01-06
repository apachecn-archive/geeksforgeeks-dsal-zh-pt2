# 求除数组最大元素个数的整数

> 原文:[https://www . geeksforgeeks . org/find-整数-除-最大数组元素数/](https://www.geeksforgeeks.org/find-integers-that-divides-maximum-number-of-elements-of-the-array/)

给定一个整数数组 **arr[]** ，任务是找到数组中最大元素数的因子元素(除了 1)。如果存在多个此类因素，请按升序打印所有因素。

**示例:**

> **输入:** arr[] = {10，20 }
> T3】输出:2 5 10
> 10 的因子是 1，2，5，10。
> 20 的因子是 1、2、4、5、10、20。
> 除 1 以外出现次数最多(两次)的因子为 2、5、10。
> 
> **输入:** arr[] = {120，15，24，63，18 }
> T3】输出: 3

**进场:**

*   初始化两个列表，一个存储因子的等级(整数是因子的元素数)，另一个存储因子。
*   从 **2** 开始，直到数组的最大元素。
*   计算数组中元素的数量。当前整数是的因子。
*   将计数添加到等级列表，将整数添加到因子列表。
*   求秩最大的整数。
*   打印所有具有相同等级的元素。

下面是上述方法的实现:

## C++

```
// CPP implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to print the integers that divide
// the maximum number of elements from the array
void maximumFactor(vector<int>arr)
{
    // Initialize two lists
    // to store rank and factors
    int n = arr.size();
    vector<int> rank;
    vector<int> factors;
    int max = *max_element(arr.begin(), arr.end());

    // Start from 2 till the maximum element in arr
    for (int i = 2; i <= max; i++)
    {
        // Initialize a variable
        // to count the number of elements
        // it is a factor of
        int count = 0;
        for (int j = 0; j < n; j++)
        {
            if (arr[j] % i == 0)
                count+= 1;
            rank.push_back(count);
            factors.push_back(i);
        }

    }

    // Maximum rank in the rank list
    int m = *max_element(rank.begin(),rank.end());
    for (int i = 0; i < rank.size(); i++)
    {
        // Print all the elements with rank m
        if (rank[i] == m)
            cout << factors[i] <<" ";
    }

}

// Driver code
int main()
{
    vector<int>arr = {120, 15, 24, 63, 18};
    maximumFactor(arr);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Function to print the integers that
// divide the maximum number of
// elements from the array
static void maximumFactor(int []arr)
{

    // Initialize two lists to store
    // rank and factors
    int[] rank = new int[Arrays.stream(arr).max().getAsInt() + 1];
    int[] factors = new int[Arrays.stream(arr).max().getAsInt() + 1];
    int g = 0;

    // Start from 2 till the maximum
    // element in arr
    for (int i = 2;
             i <= Arrays.stream(arr).max().getAsInt(); i++)
    {
        // Initialize a variable to count
        // the number of elements it is a
        // factor of
        int count = 0;
        for (int j = 0; j < arr.length; j++)
            if (arr[j] % i == 0)
                count += 1;

        rank[g] = count;
        factors[g] = i;
        g++;
    }

    // Maximum rank in the rank list
    int m = Arrays.stream(rank).max().getAsInt();
    for (int i = 0; i < rank.length; i++)
    {
        // Print all the elements with rank m
        if (rank[i] == m)
            System.out.print(factors[i] + " ");
    }
}

// Driver code
public static void main (String[] args)
{
    int []arr = {120, 15, 24, 63, 18};
    maximumFactor(arr);
}
}

// This code is contributed by
// chandan_jnu
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to print the integers that divide
# the maximum number of elements from the array
def maximumFactor(arr):

    # Initialize two lists
    # to store rank and factors
    rank, factors = [], []

    # Start from 2 till the maximum element in arr
    for i in range(2, max(arr)+1):

        # Initialize a variable
        # to count the number of elements
        # it is a factor of
        count = 0
        for j in arr:
            if j % i == 0:count+= 1
        rank.append(count)
        factors.append(i)

    # Maximum rank in the rank list
    m = max(rank)
    for i in range(len(rank)):

        # Print all the elements with rank m
        if rank[i]== m:
            print(factors[i], end =" ")

# Driver code
arr = [120, 15, 24, 63, 18]

maximumFactor(arr)
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections;
using System.Linq;

class GFG
{

// Function to print the integers that
// divide the maximum number of
// elements from the array
static void maximumFactor(int []arr)
{

    // Initialize two lists to store
    // rank and factors
    int[] rank = new int[arr.Max() + 1];
    int[] factors = new int[arr.Max() + 1];
    int g = 0;

    // Start from 2 till the maximum
    // element in arr
    for (int i = 2; i <= arr.Max(); i++)
    {
        // Initialize a variable to count
        // the number of elements it is a
        // factor of
        int count = 0 ;
        for (int j = 0; j < arr.Length; j++)
            if (arr[j] % i == 0)
                count += 1;

        rank[g]=count;
        factors[g]=i;
        g++;
    }

    // Maximum rank in the rank list
    int m = rank.Max();
    for (int i = 0; i < rank.Length; i++)
    {
        // Print all the elements with rank m
        if ((int)rank[i] == m)
            Console.Write(factors[i]+" ");
    }
}

// Driver code
static void Main()
{

int []arr = {120, 15, 24, 63, 18};
maximumFactor(arr);
}
}

// This code is contributed by chandan_jnu
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the integers that
// divide the maximum number of
// elements from the array
function maximumFactor($arr)
{

    // Initialize two lists to store
    // rank and factors
    $rank = array();
    $factors = array();

    // Start from 2 till the maximum
    // element in arr
    for ($i = 2; $i <= max($arr); $i++)
    {
        // Initialize a variable to count
        // the number of elements it is a
        // factor of
        $count = 0 ;
        for ($j = 0; $j < sizeof($arr); $j++)
            if ($arr[$j] % $i == 0)
                $count += 1;

        array_push($rank, $count);
        array_push($factors, $i);
    }

    // Maximum rank in the rank list
    $m = max($rank);
    for ($i = 0; $i < sizeof($rank); $i++)
    {
        // Print all the elements with rank m
        if ($rank[$i] == $m)
            echo $factors[$i], " ";
    }
}

// Driver code
$arr = array(120, 15, 24, 63, 18);

maximumFactor($arr)

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print the integers that divide
// the maximum number of elements from the array
function maximumFactor(arr)
{
    // Initialize two lists
    // to store rank and factors
    var n = arr.length;
    var rank = [];
    var factors = [];
    var max = arr.reduce((a,b)=> Math.max(a,b));

    // Start from 2 till the maximum element in arr
    for (var i = 2; i <= max; i++)
    {
        // Initialize a variable
        // to count the number of elements
        // it is a factor of
        var count = 0;
        for (var j = 0; j < n; j++)
        {
            if (arr[j] % i == 0)
                count+= 1;
            rank.push(count);
            factors.push(i);
        }

    }

    // Maximum rank in the rank list
    var m = rank.reduce((a,b)=>Math.max(a,b));
    for (var i = 0; i < rank.length; i++)
    {
        // Print all the elements with rank m
        if (rank[i] == m)
            document.write( factors[i] + " ");
    }

}

// Driver code
var arr = [120, 15, 24, 63, 18];
maximumFactor(arr);

</script>
```

**Output:** 

```
3
```