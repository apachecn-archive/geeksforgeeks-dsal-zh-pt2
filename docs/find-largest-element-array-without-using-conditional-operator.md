# 不使用条件运算符

从数组中找到最大的元素

> 原文:[https://www . geesforgeks . org/find-最大元素-数组-不使用条件运算符/](https://www.geeksforgeeks.org/find-largest-element-array-without-using-conditional-operator/)

给定一个 n 元素数组，我们必须在不使用任何条件运算符(如大于或小于)的情况下找到其中最大的元素。
**例:**

```
Input : arr[] = {5, 7, 2, 9}
Output : Largest element = 9

Input : arr[] = {15, 0, 2, 15}
Output : Largest element = 15
```

**第一种方法(散列的使用):**为了从数组中找到最大的元素，我们可以使用散列的概念，其中我们应该维护所有元素的哈希表，然后在处理完所有数组元素后，我们应该通过简单地从头到尾遍历哈希表来找到散列中最大的元素。
但是这种方法有一些缺点，比如在非常大的元素的情况下，维护一个散列表不是不可能就是不可行。
**更好的方法(按位 AND 的使用):**最近我们学习了如何从给定数组中找到最大的 AND 值对。此外，我们知道，如果我们对任何带有 INT_MAX(其所有位都是设置位)的数字进行按位“与”，那么结果将是该数字本身。现在，使用这个属性，我们将尝试从数组中找到最大的元素，而不使用任何条件运算符，如大于或小于。
为了找到最大的元素，我们将首先在数组中插入一个额外的元素，即 INT_MAX，然后我们将尝试从数组中找到任何对的最大 and 值。这个获得的最大值将包含 INT_MAX 的 AND 值和原始数组的最大元素，并且是我们需要的结果。
以下是上述方法的实施:

## C++

```
// C++ Program to find largest element from array
#include <bits/stdc++.h>
using namespace std;

// Utility function to check number of
// elements having set msb as of pattern
int checkBit(int pattern, vector<int> arr, int n)
{
    int count = 0;
    for (int i = 0; i < n; i++)
        if ((pattern & arr[i]) == pattern)
            count++;
    return count;
}

// Function for finding maximum and value pair
int largest(int arr[], int n)
{
    // Create a vector of given array
    vector<int> v(arr, arr + n);

    // Insert INT_MAX and update n
    v.push_back(INT_MAX);
    n++;

    int res = 0;

    // Iterate over total of 30bits from
    // msb to lsb
    for (int bit = 31; bit >= 0; bit--)
    {

        // Find the count of element having set msb
        int count = checkBit(res | (1 << bit), v, n);

        // if count | 1 != 1 set particular
        // bit in result
        if ((count | 1) != 1)
            res |= (1 << bit);
    }

    return res;
}

// Driver Code
int main()
{
    int arr[] = { 4, 8, 6, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Largest element = " << largest(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find largest element from array
import java.util.Vector;
import java.util.Arrays;

class GfG
{

// Utility function to check number of
// elements having set msb as of pattern
static int checkBit(int pattern, Vector<Integer> arr, int n)
{
    int count = 0;
    for (int i = 0; i < n; i++)
        if ((pattern & arr.get(i)) == pattern)
            count++;
    return count;
}

// Function for finding maximum and value pair
static int largest(int arr[], int n)
{
    // Create a vector of given array
    Vector<Integer> v = new Vector<>();
    for(Integer a:arr)
        v.add(a);

    // Insert INT_MAX and update n
    v.add(Integer.MAX_VALUE);
    n++;

    int res = 0;

    // Iterate over total of 30bits from
    // msb to lsb
    for (int bit = 31; bit >= 0; bit--)
    {

        // Find the count of element having set msb
        int count = checkBit(res | (1 << bit), v, n);

        // if count | 1 != 1 set particular
        // bit in result
        if ((count | 1) != 1)
            res |= (1 << bit);
    }

    return res;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 8, 6, 2 };
    int n = arr.length;
    System.out.println("Largest element = " +
                            largest(arr, n));
}
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 Program to find largest
# element from array
import math as mt

# Utility function to check number of
# elements having set msb as of pattern
def checkBit(pattern, arr, n):
    count = 0
    for i in range(n):
        if ((pattern & arr[i]) == pattern):
            count += 1
    return count

# Function for finding maximum
# and value pair
def largest(arr, n):

    # Create a vector of given array
    v = arr

    # Insert max value of Int and update n
    v.append(2**31 - 1)
    n = n + 1

    res = 0

    # Iterate over total of 30bits
    # from msb to lsb
    for bit in range(31, -1, -1):

        # Find the count of element
        # having set msb
        count = checkBit(res | (1 << bit), v, n)

        # if count | 1 != 1 set particular
        # bit in result
        if ((count | 1) != 1):
            res |= (1 << bit)

    return res

# Driver Code
arr = [4, 8, 6, 2]
n = len(arr)
print("Largest element =", largest(arr, n))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# Program to find largest element from array
using System;   
using System.Collections.Generic;   

class GfG
{

// Utility function to check number of
// elements having set msb as of pattern
static int checkBit(int pattern, List<int> arr, int n)
{
    int count = 0;
    for (int i = 0; i < n; i++)
        if ((pattern & arr[i]) == pattern)
            count++;
    return count;
}

// Function for finding maximum and value pair
static int largest(int []arr, int n)
{
    // Create a vector of given array
    List<int> v = new List<int>();
    foreach(int a in arr)
        v.Add(a);

    // Insert INT_MAX and update n
    v.Add(int.MaxValue);
    n++;

    int res = 0;

    // Iterate over total of 30bits from
    // msb to lsb
    for (int bit = 31; bit >= 0; bit--)
    {

        // Find the count of element having set msb
        int count = checkBit(res | (1 << bit), v, n);

        // if count | 1 != 1 set particular
        // bit in result
        if ((count | 1) != 1)
            res |= (1 << bit);
    }

    return res;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 4, 8, 6, 2 };
    int n = arr.Length;
    Console.WriteLine("Largest element = " +
                            largest(arr, n));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// php Program to find largest
// element from array

// Utility function to check
// number of elements having
// set msb as of pattern
function checkBit($pattern,$arr,$n)
{
    $count = 0;
    for ($i = 0; $i < $n; $i++)
        if (($pattern & $arr[$i]) == $pattern)
            $count++;
    return $count;
}

// Function for finding
// maximum and value pair
function largest($arr, $n)
{
    $res = 0;

    // Iterate over total of
    // 30bits from msb to lsb
    for ($bit = 31; $bit >= 0; $bit--)
    {

        // Find the count of element
        // having set msb
        $count = checkBit($res | (1 << $bit),$arr, $n);

        // if count | 1 != 1 set
        // particular bit in result
        if ($count | 1 != 1)
            $res |= (1 << $bit);
    }

    return $res;
}

    // Driver code
    $arr = array( 4, 8, 6, 2 );
    $n = sizeof($arr) / sizeof($arr[0]);
    echo "Largest element = ". largest($arr, $n);

// This code is contributed by mits 
?>
```

## java 描述语言

```
<script>
// javascript Program to find largest element from array

// Utility function to check number of
// elements having set msb as of pattern
function checkBit( pattern, arr, n){
    let count = 0;
    for (let i = 0; i < n; i++)
        if ((pattern & arr[i]) == pattern)
            count++;
    return count;
}

// Function for finding maximum and value pair
function largest( arr, n){
    // Create a vector of given array
    let v = [];
    for(let i = 0;i<n;i++){
        v.push(arr[i])
    }
    // Insert INT_MAX and update n
    v.push(Math.pow(2,31)-1);
    n++;

    let res = 0;

    // Iterate over total of 30bits from
    // msb to lsb
    for (let bit = 31; bit >= 0; bit--)
    {

        // Find the count of element having set msb
        let count = checkBit(res | (1 << bit), v, n);

        // if count | 1 != 1 set particular
        // bit in result
        if ((count | 1) != 1)
            res |= (1 << bit);
    }

    return res;
}

let a = [ 4, 8, 6, 2 ];
n = a.length;
document.write("Largest element = ");
document.write(largest(a, n));

// This code is contributed by rohitsingh07052.
</script>
```

**输出:**

```
Largest element = 8
```

**时间复杂度:** O(32)

**辅助空间:** O(N)