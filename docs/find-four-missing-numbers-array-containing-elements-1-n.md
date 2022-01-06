# 在包含从 1 到 N 的元素的数组中找到四个缺失的数字

> 原文:[https://www . geeksforgeeks . org/find-四-缺失数字-数组-包含元素-1-n/](https://www.geeksforgeeks.org/find-four-missing-numbers-array-containing-elements-1-n/)

给定一个唯一整数数组，其中给定数组的每个整数都在[1，N]范围内。数组的大小为(N-4)。没有重复的单个元素。因此，数组中缺少了从 1 到 N 的四个数字。按排序顺序找出 4 个缺少的数字。

**示例:**

```
Input : arr[] = {2, 5, 6, 3, 9}
Output : 1 4 7 8

Input : arr[] = {1, 7, 3, 13, 5, 10, 8, 4, 9}
Output : 2 6 11 12
```

一个简单的 O(N)解决方案是使用一个大小为 N 的辅助数组来标记被访问的元素。遍历输入数组并标记辅助数组中的元素。最后打印所有没有标记的索引。

**如何用 O(1)辅助空间求解？**
我们初始化一个长度为 4 的名为**助手**的数组，以补偿 4 个丢失的数字，并用零填充它们。然后我们从 i=0 迭代到给定数组的 i < length_of_array，取第 I 个元素的的绝对值，并将其存储在名为 **temp** 的变量中。现在我们将检查:

1.  如果元素的绝对值小于输入数组的长度，那么我们将数组[temp]元素乘以-1(以便标记被访问的元素)。
2.  如果元素的绝对值大于输入数组的长度，那么我们将把 helper[temp%array.length]元素的值设为-1(以便标记被访问的元素)。

然后我们迭代输入数组和那些值仍然大于零的索引，然后在输入数组中没有遇到这些元素。所以我们打印元素大于零的索引的 **(index+1)** 值。
然后我们将迭代助手数组和那些值仍然大于零的索引，然后在输入数组中没有遇到这些元素。所以我们打印元素大于零的索引的 **(index+array.length+1)** 值。

## C++

```
// CPP program to find missing 4 elements
// in an array of size N where elements are
// in range from 1 to N+4.
#include <bits/stdc++.h>
using namespace std;

// Finds missing 4 numbers in O(N) time
// and O(1) auxiliary space.
void missing4(int arr[], int n)
{
    // To keep track of 4 possible numbers
    // greater than length of input array
    // In Java, helper is automatically
    // initialized as 0.
    int helper[4];

    // Traverse the input array and mark
    // visited elements either by marking
    // them as negative in arr[] or in
    // helper[].
    for (int i = 0; i < n; i++) {
        int temp = abs(arr[i]);

        // If element is smaller than or
        // equal to length, mark its
        // presence in arr[]
        if (temp <= n)
            arr[temp - 1] *= (-1);

        // Mark presence in helper[]
        else if (temp > n) {
            if (temp % n != 0)
                helper[temp % n - 1] = -1;
            else
                helper[(temp % n) + n - 1] = -1;
        }
    }

    // Print all those elements whose presence
    // is not marked.
    for (int i = 0; i < n; i++)
        if (arr[i] > 0)
            cout << (i + 1) << " ";
    for (int i = 0; i < 4; i++)
        if (helper[i] >= 0)
            cout << (n + i + 1) << " ";

    return;
}

// Driver code
int main()
{
    int arr[] = { 1, 7, 3, 12, 5, 10, 8, 4, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);
    missing4(arr, n);
    return 0;
}

// This code is contributed by Nikita Tiwari.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find missing 4 elements
// in an array of size N where elements are
// in range from 1 to N+4.
class Missing4 {

    // Finds missing 4 numbers in O(N) time
    // and O(1) auxiliary space.
    public static void missing4(int[] arr)
    {
        // To keep track of 4 possible numbers
        // greater than length of input array
        // In Java, helper is automatically
        // initialized as 0.
        int[] helper = new int[4];

        // Traverse the input array and mark
        // visited elements either by marking
        // them as negative in arr[] or in
        // helper[].
        for (int i = 0; i < arr.length; i++) {
            int temp = Math.abs(arr[i]);

            // If element is smaller than or
            // equal to length, mark its
            // presence in arr[]
            if (temp <= arr.length)
                arr[temp - 1] *= (-1);

             // Mark presence in helper[]
             else if (temp > arr.length) {
                if (temp % arr.length != 0)
                    helper[temp % arr.length - 1] = -1;
                else
                    helper[(temp % arr.length) +
                                   arr.length - 1] = -1;
            }
        }

        // Print all those elements whose presence
        // is not marked.  
        for (int i = 0; i < arr.length; i++)
            if (arr[i] > 0)
                System.out.print(i + 1 + " ");     
        for (int i = 0; i < helper.length; i++)
            if (helper[i] >= 0)
                System.out.print(arr.length + i + 1 + " ");           

        return;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 1, 7, 3, 12, 5, 10, 8, 4, 9 };
        missing4(arr);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find missing 4 elements
# in an array of size N where elements are
# in range from 1 to N+4.

# Finds missing 4 numbers in O(N) time
# and O(1) auxiliary space.
def missing4( arr) :

    # To keep track of 4 possible numbers
    # greater than length of input array
    # In Java, helper is automatically
    # initialized as 0.
    helper = [0]*4

    # Traverse the input array and mark
    # visited elements either by marking
    # them as negative in arr[] or in
    # helper[].
    for i in range(0,len(arr)) :
        temp = abs(arr[i])

        # If element is smaller than or
        # equal to length, mark its
        # presence in arr[]
        if (temp <= len(arr)) :
            arr[temp - 1] = arr[temp - 1] * (-1)

        # Mark presence in helper[]
        elif (temp > len(arr)) :
            if (temp % len(arr)) :
                helper[temp % len(arr) - 1] = -1
            else :
                helper[(temp % len(arr)) +len(arr) - 1] = -1

    # Print all those elements whose presence
    # is not marked.  
    for i in range(0, len(arr) ) :
        if (arr[i] > 0) :
            print((i + 1) , end=" ")
    for i in range(0, len(helper)) :
        if (helper[i] >= 0) :
            print((len(arr) + i + 1) , end=" ")

# Driver code
arr = [ 1, 7, 3, 12, 5, 10, 8, 4, 9 ]
missing4(arr)

# This code is contributed
# by Nikita Tiwari.
```

## C#

```
// C# program to find missing 4 elements
// in an array of size N where elements are
// in range from 1 to N+4.
using System;

class Missing4 {

    // Finds missing 4 numbers in O(N) time
    // and O(1) auxiliary space.
    public static void missing4(int[] arr)
    {
        // To keep track of 4 possible numbers
        // greater than length of input array
        // In Java, helper is automatically
        // initialized as 0.
        int[] helper = new int[4];

        // Traverse the input array and mark
        // visited elements either by marking
        // them as negative in arr[] or in
        // helper[].
        for (int i = 0; i < arr.Length; i++) {
            int temp = Math.Abs(arr[i]);

            // If element is smaller than or
            // equal to length, mark its
            // presence in arr[]
            if (temp <= arr.Length)
                arr[temp - 1] *= (-1);

             // Mark presence in helper[]
             else if (temp > arr.Length) {
                if (temp % arr.Length != 0)
                    helper[temp % arr.Length - 1] = -1;
                else
                    helper[(temp % arr.Length) +
                                   arr.Length - 1] = -1;
            }
        }

        // Print all those elements whose presence
        // is not marked.  
        for (int i = 0; i < arr.Length; i++)
            if (arr[i] > 0)
                Console.Write(i + 1 + " ");     
        for (int i = 0; i < helper.Length; i++)
            if (helper[i] >= 0)
                Console.Write(arr.Length + i + 1 + " ");           

        return;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 7, 3, 12, 5, 10, 8, 4, 9 };
        missing4(arr);
    }
}

//This code is contributed by Anant Agarwal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find missing 4 elements
// in an array of size N where elements
// are in range from 1 to N+4.

// Finds missing 4 numbers in O(N) time
// and O(1) auxiliary space.
function missing4($arr, $n)
{
    // To keep track of 4 possible numbers
    // greater than length of input array
    // initialized as 0.
    $helper = array(0, 0, 0, 0);

    // Traverse the input array and mark
    // visited elements either by marking
    // them as negative in arr[] or in
    // helper[].
    for ($i = 0; $i < $n; $i++)
    {
        $temp = abs($arr[$i]);

        // If element is smaller than or
        // equal to length, mark its
        // presence in arr[]
        if ($temp <= $n)
            $arr[$temp - 1] = $arr[$temp - 1] * (-1);

        // Mark presence in helper[]
        else if ($temp > $n)
        {
            if ($temp % $n != 0)
                $helper[$temp % $n - 1] = -1;
            else
                $helper[($temp % $n) + $n - 1] = -1;
        }
    }

    // Print all those elements whose
    // presence is not marked.
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] > 0)
        {
            $a = $i + 1;
            echo "$a", " ";
        }
    for ($i = 0; $i < 4; $i++)
        if ($helper[$i] >= 0)
        {
            $b = $n + $i + 1;
            echo "$b", " ";
        }
        echo "\n";

    return;
}

// Driver code
$arr = array(1, 7, 3, 12, 5, 10, 8, 4, 9);
$n = sizeof($arr);
missing4($arr, $n);

// This code is contributed by iAyushRaj
?>
```

## java 描述语言

```
<script>

// Javascript program to find missing 4 elements
// in an array of size N where elements are
// in range from 1 to N+4.

// Finds missing 4 numbers in O(N) time
// and O(1) auxiliary space.
function missing4(arr)
{

    // To keep track of 4 possible numbers
    // greater than length of input array
    // In Java, helper is automatically
    // initialized as 0.
    let helper =[];
    for(let i = 0; i < 4; i++)
    {
        helper[i] = 0;
    }

    // Traverse the input array and mark
    // visited elements either by marking
    // them as negative in arr[] or in
    // helper[].
    for(let i = 0; i < arr.length; i++)
    {
        let temp = Math.abs(arr[i]);

        // If element is smaller than or
        // equal to length, mark its
        // presence in arr[]
        if (temp <= arr.length)
            arr[temp - 1] = Math.floor(arr[temp - 1] * (-1));

         // Mark presence in helper[]
         else if (temp > arr.length)
         {
            if (temp % arr.length != 0)
                helper[temp % arr.length - 1] = -1;
            else
                helper[(temp % arr.length) +
                               arr.length - 1] = -1;
        }
    }

    // Print all those elements whose presence
    // is not marked.  
    for(let i = 0; i < arr.length; i++)
        if (arr[i] > 0)
            document.write(i + 1 + " ");     
    for(let i = 0; i < helper.length; i++)
        if (helper[i] >= 0)
            document.write(arr.length + i + 1 + " ");           

    return;
}

// Driver code
let arr = [ 1, 7, 3, 12, 5, 10, 8, 4, 9 ];
missing4(arr);

// This code is contributed by susmitakundugoaldanga  

</script>
```

**输出:**

```
2 6 11 13 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)

本文由 [**桑凯特·辛格 2**](https://auth.geeksforgeeks.org/profile.php?user=Sanket Singh 2) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。