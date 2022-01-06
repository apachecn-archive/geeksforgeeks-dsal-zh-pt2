# 最小对和运算，使数组每个元素可被 4 整除

> 原文:[https://www . geeksforgeeks . org/最小对和运算生成每个元素可被 4 整除的数组/](https://www.geeksforgeeks.org/minimum-pair-sum-operations-to-make-array-each-element-divisible-by-4/)

给定长度为 **n** 的正整数数组。我们的任务是找到转换数组的最小操作数，以便每个 **i** 的 **arr[i] % 4** 为零。在每个操作中，我们可以从数组中取出任意两个元素，将它们都移除，并将它们的总和放回数组中。
**举例:**

> 输入:arr = {2，2，2，3，3}
> 输出:3
> 说明:在 1 次操作中，我们选择 2 和 2，并将它们的总和放回数组，在 2 次操作中，我们选择 3 和 3，并为此做同样的事情，现在在 3 次操作中，我们选择 6 和 2，因此总体上需要 3 次操作。
> 输入:arr = {4，2，2，6，6}
> 输出:2
> 说明:在操作 1 中，我们可以取 2 和 2，放回它们的和即 4。在操作 2 中，我们可以取 6 和 6，并放回它们的总和，即 12。数组变成{4，4，12}。

**方法:**假设当除以 **4** 时，剩余 **1、2、3** 的元素数为**brr【1】**、**brr【2】**和**brr【3】**。
如果**(brr[1]+2 * brr[2]+3 * brr[3])**不是 **4** 的倍数，则解不存在。
现在贪婪地将 **brr[2]** 的元素与 **brr[2]** 配对，将 **brr[1]** 的元素与 **brr[3]** 配对。这有助于我们一次最多固定 **2** 个元件。现在，我们要么只剩下**1****brr【2】**元素，要么什么都没有。如果我们剩下**1****brr【2】**元素，那么我们可以和剩余的**2**brr【1】或**brr【3】**元素配对。这将导致总共 **2** 次操作。
最后，我们将只剩下 **brr[1]** 或 **brr[3]** 元素(如果可能的话)。这只能我们用一种方法解决。即取其中的 **4** ，在 **3** 操作中全部固定在一起。因此，我们能够修复数组的所有元素。
下面是实现:

## C++

```
// CPP program to find Minimum number
// of operations to convert an array
// so that arr[i] % 4 is zero.
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum operations.
int minimumOperations(int arr[], int n)
{  
    // Counting of all the elements
    // leaving remainder 1, 2, 3 when
    // divided by 4 in the array brr.
    // at positions 1, 2 and 3 respectively.
    int brr[] = { 0, 0, 0, 0 };
    for (int i = 0; i < n; i++)
        brr[arr[i] % 4]++;

    // If it is possible to convert the
    // array so that arr[i] % 4 is zero.
    if ((brr[1] + 2 * brr[2] + 3 * brr[3]) % 4 == 0)
    {
        // Pairing the elements of brr3 and brr1.
        int min_opr = min(brr[3], brr[1]);
        brr[3] -= min_opr;
        brr[1] -= min_opr;

        // Pairing the brr2 elements.
        min_opr += brr[2] / 2;

        // Assigning the remaining brr2 elements.
        brr[2] %= 2;

        // If we are left with one brr2 element.
        if (brr[2]) {

            // Here we need only two operations
            // to convert the remaining one
            // brr2 element to convert it.
            min_opr += 2;

            // Now there is no brr2 element.
            brr[2] = 0;

            // Remaining brr3 elements.
            if (brr[3])            
                brr[3] -= 2;           

            // Remaining brr1 elements.
            if (brr[1])
                brr[1] -= 2;           
        }

        // If we are left with brr1 and brr2
        // elements then, we have to take four
        // of them and fixing them all together
        // in 3 operations.
        if (brr[1])       
            min_opr += (brr[1] / 4) * 3;       
        if (brr[3])       
            min_opr += (brr[3] / 4) * 3;       

        // Returns the minimum operations.
        return min_opr;
    }

    // If it is not possible to convert the array.
    return -1;   
}

// Driver function
int main()
{
    int arr[] = { 1, 2, 3, 1, 2, 3, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minimumOperations(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Minimum number
// of operations to convert an array
// so that arr[i] % 4 is zero.

class GFG {

// Function to find minimum operations.
static int minimumOperations(int arr[], int n)
{  

    // Counting of all the elements
    // leaving remainder 1, 2, 3 when
    // divided by 4 in the array brr.
    // at positions 1, 2 and 3 respectively.
    int brr[] = { 0, 0, 0, 0 };
    for (int i = 0; i < n; i++)
        brr[arr[i] % 4]++;

    // If it is possible to convert the
    // array so that arr[i] % 4 is zero.
    if ((brr[1] + 2 * brr[2] + 3 * brr[3]) % 4 == 0)
    {
        // Pairing the elements of brr3 and brr1.
        int min_opr = Math.min(brr[3], brr[1]);
        brr[3] -= min_opr;
        brr[1] -= min_opr;

        // Pairing the brr2 elements.
        min_opr += brr[2] / 2;

        // Assigning the remaining brr2 elements.
        brr[2] %= 2;

        // If we are left with one brr2 element.
        if (brr[2] == 1) {

            // Here we need only two operations
            // to convert the remaining one
            // brr2 element to convert it.
            min_opr += 2;

            // Now there is no brr2 element.
            brr[2] = 0;

            // Remaining brr3 elements.
            if (brr[3] == 1)            
                brr[3] -= 2;           

            // Remaining brr1 elements.
            if (brr[1]== 1)
                brr[1] -= 2;           
        }

        // If we are left with brr1 and brr2
        // elements then, we have to take four
        // of them and fixing them all together
        // in 3 operations.
        if (brr[1] == 1)       
            min_opr += (brr[1] / 4) * 3;       
        if (brr[3] == 1)       
            min_opr += (brr[3] / 4) * 3;       

        // Returns the minimum operations.
        return min_opr;
    }

    // If it is not possible to convert the array.
    return -1;   
}

// Driver function
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 1, 2, 3, 8 };
    int n = arr.length;
    System.out.println(minimumOperations(arr, n));
}
}

// This code is contributed by Prerna Saini.
```

## 蟒蛇 3

```
# Python program to
# find Minimum number
# of operations to
# convert an array
# so that arr[i] % 4 is zero.

# Function to find
# minimum operations.
def minimumOperations(arr,n):

    # Counting of all the elements
    # leaving remainder 1, 2, 3 when
    # divided by 4 in the array brr.
    # at positions 1, 2 and 3 respectively.
    brr = [ 0, 0, 0, 0 ]
    for i in range(n):
        brr[arr[i] % 4]+=1;

    # If it is possible to convert the
    # array so that arr[i] % 4 is zero.
    if ((brr[1] + 2 * brr[2] + 3 * brr[3]) % 4 == 0):

        # Pairing the elements
        # of brr3 and brr1.
        min_opr = min(brr[3], brr[1])
        brr[3] -= min_opr
        brr[1] -= min_opr

        # Pairing the brr2 elements.
        min_opr += brr[2] // 2

        # Assigning the remaining
        # brr2 elements.
        brr[2] %= 2

        # If we are left with
        # one brr2 element.
        if (brr[2]):

            # Here we need only two operations
            # to convert the remaining one
            # brr2 element to convert it.
            min_opr += 2

            # Now there is no brr2 element.
            brr[2] = 0

            # Remaining brr3 elements.
            if (brr[3]):            
                brr[3] -= 2           

            # Remaining brr1 elements.
            if (brr[1]):
                brr[1] -= 2           

        # If we are left with brr1 and brr2
        # elements then, we have to take four
        # of them and fixing them all together
        # in 3 operations.
        if (brr[1]):       
            min_opr += (brr[1] // 4) * 3       
        if (brr[3]):       
            min_opr += (brr[3] // 4) * 3       

        # Returns the minimum operations.
        return min_opr

    # If it is not possible to convert the array.
    return -1   

# Driver function

arr = [ 1, 2, 3, 1, 2, 3, 8 ]
n =len(arr)

print(minimumOperations(arr, n))

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to find Minimum number
// of operations to convert an array
// so that arr[i] % 4 is zero.
using System;

class GFG {

    // Function to find minimum operations.
    static int minimumOperations(int []arr, int n)
    {

        // Counting of all the elements
        // leaving remainder 1, 2, 3 when
        // divided by 4 in the array brr.
        // at positions 1, 2 and 3 respectively.
        int []brr = { 0, 0, 0, 0 };
        for (int i = 0; i < n; i++)
            brr[arr[i] % 4]++;

        // If it is possible to convert the
        // array so that arr[i] % 4 is zero.
        if ((brr[1] + 2 * brr[2] + 3 * brr[3]) % 4 == 0)
        {
            // Pairing the elements of brr3 and brr1.
            int min_opr = Math.Min(brr[3], brr[1]);
            brr[3] -= min_opr;
            brr[1] -= min_opr;

            // Pairing the brr2 elements.
            min_opr += brr[2] / 2;

            // Assigning the remaining brr2 elements.
            brr[2] %= 2;

            // If we are left with one brr2 element.
            if (brr[2] == 1) {

                // Here we need only two operations
                // to convert the remaining one
                // brr2 element to convert it.
                min_opr += 2;

                // Now there is no brr2 element.
                brr[2] = 0;

                // Remaining brr3 elements.
                if (brr[3] == 1)            
                    brr[3] -= 2;        

                // Remaining brr1 elements.
                if (brr[1]== 1)
                    brr[1] -= 2;        
            }

            // If we are left with brr1 and brr2
            // elements then, we have to take four
            // of them and fixing them all together
            // in 3 operations.
            if (brr[1] == 1)    
                min_opr += (brr[1] / 4) * 3;    
            if (brr[3] == 1)    
                min_opr += (brr[3] / 4) * 3;    

            // Returns the minimum operations.
            return min_opr;
        }

        // If it is not possible to convert the array.
        return -1;
    }

    // Driver function
    public static void Main()
    {
        int []arr = { 1, 2, 3, 1, 2, 3, 8 };
        int n = arr.Length;
        Console.WriteLine(minimumOperations(arr, n));
    }
}

// This code is contributed by  vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find
// Minimum number of
// operations to convert
// an array so that
// arr[i] % 4 is zero.

// Function to find
// minimum operations.
function minimumOperations($arr, $n)
{
    // Counting of all the
    // elements leaving remainder
    // 1, 2, 3 when divided by 4
    // in the array brr at positions
    // 1, 2 and 3 respectively.
    $brr = array(0, 0, 0, 0);
    for ($i = 0; $i < $n; $i++)
        $brr[$arr[$i] % 4]++;

    // If it is possible to
    // convert the array so
    // that arr[i] % 4 is zero.
    if (($brr[1] + 2 *
         $brr[2] + 3 *
         $brr[3]) % 4 == 0)
    {
        // Pairing the elements
        // of brr3 and brr1.
        $min_opr = min($brr[3],
                       $brr[1]);
        $brr[3] -= $min_opr;
        $brr[1] -= $min_opr;

        // Pairing the
        // brr2 elements.
        $min_opr += $brr[2] / 2;

        // Assigning the remaining
        // brr2 elements.
        $brr[2] %= 2;

        // If we are left with
        // one brr2 element.
        if ($brr[2])
        {

            // Here we need only two
            // operations to convert
            // the remaining one brr2
            // element to convert it.
            $min_opr += 2;

            // Now there is no
            // brr2 element.
            $brr[2] = 0;

            // Remaining brr3 elements.
            if ($brr[3])            
                $brr[3] -= 2;        

            // Remaining brr1 elements.
            if ($brr[1])
                $brr[1] -= 2;        
        }

        // If we are left with brr1
        // and brr2 elements then,
        // we have to take four of
        // them and fixing them all
        // together in 3 operations.
        if ($brr[1])    
            $min_opr += ($brr[1] / 4) * 3;    
        if ($brr[3])    
            $min_opr += ($brr[3] / 4) * 3;    

        // Returns the
        // minimum operations.
        return $min_opr;
    }

    // If it is not possible
    // to convert the array.
    return -1;
}

// Driver Code
$arr = array(1, 2, 3,
             1, 2, 3, 8);
$n = count($arr);
echo (minimumOperations($arr, $n));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>
// Java Script program to find Minimum number
// of operations to convert an array
// so that arr[i] % 4 is zero.

// Function to find minimum operations.
function minimumOperations(arr,n)
{  

    // Counting of all the elements
    // leaving remainder 1, 2, 3 when
    // divided by 4 in the array brr.
    // at positions 1, 2 and 3 respectively.
    let brr = [0, 0, 0, 0 ];
    for (let i = 0; i < n; i++)
        brr[arr[i] % 4]++;

    // If it is possible to convert the
    // array so that arr[i] % 4 is zero.
    if ((brr[1] + 2 * brr[2] + 3 * brr[3]) % 4 == 0)
    {
        // Pairing the elements of brr3 and brr1.
        let min_opr = Math.min(brr[3], brr[1]);
        brr[3] -= min_opr;
        brr[1] -= min_opr;

        // Pairing the brr2 elements.
        min_opr += brr[2] / 2;

        // Assigning the remaining brr2 elements.
        brr[2] %= 2;

        // If we are left with one brr2 element.
        if (brr[2] == 1) {

            // Here we need only two operations
            // to convert the remaining one
            // brr2 element to convert it.
            min_opr += 2;

            // Now there is no brr2 element.
            brr[2] = 0;

            // Remaining brr3 elements.
            if (brr[3] == 1)            
                brr[3] -= 2;           

            // Remaining brr1 elements.
            if (brr[1]== 1)
                brr[1] -= 2;           
        }

        // If we are left with brr1 and brr2
        // elements then, we have to take four
        // of them and fixing them all together
        // in 3 operations.
        if (brr[1] == 1)       
            min_opr += (brr[1] / 4) * 3;       
        if (brr[3] == 1)       
            min_opr += (brr[3] / 4) * 3;       

        // Returns the minimum operations.
        return min_opr;
    }

    // If it is not possible to convert the array.
    return -1;   
}

// Driver function

    let arr= [1, 2, 3, 1, 2, 3, 8 ];
    let n = arr.length;
    document.write(minimumOperations(arr, n));

// This code is contributed by Bobby
</script>
```

**输出:**

```
3
```