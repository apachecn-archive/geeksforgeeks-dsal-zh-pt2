# 0 和 1 相等的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列-等数-0-1/](https://www.geeksforgeeks.org/longest-subsequence-equal-numbers-0-1/)

给定一个二进制数组，任务是找出具有相同数量的 0 和 1 的最大子序列的大小。
**例:**

```
Input : arr[] = { 1, 0, 0, 1, 0, 0, 0, 1 } 
Output: 6

Input : arr[] = { 0, 0, 1, 1, 1, 1, 1, 0, 0 }
Output : 8
```

**简单的解决方案**是我们生成所有可能的子序列，并找出哪个子序列具有相等数量的零&1(它的大小应该是最大的)。
以下是以上想法的实现

## C++

```
#include <bits/stdc++.h>
using namespace std;

int generateSubsequences(int arr[],
                         int n)
{
    // store the maximum length
    // sub_sequence having equal
    // number of zeros and ones
    int result = 0;

    // Number of subsequences is (2**n -1)
    unsigned int opsize = pow(2, n);

    // Run from counter 000..1 to 111..1
    for (int counter = 1; counter < opsize;
                          counter++)
    {

        // store count of zeros and one
        int countzero = 0;
        int countone = 0, current_size = 0;

        for (int j = 0; j < n; j++)
        {

            // Check if jth bit in the
            // counter is set. If set
            // then print jth element
            // from arr[]
            if (counter & (1 << j))

            {
                if (arr[j])
                    countone++;
                else
                    countzero++;
                current_size++;
            }
        }

        // update maximum size
        if (countzero == countone)
            result = max(current_size,
                              result);
    }
    return result;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 0, 1,
                0, 0, 0, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "largest Subsequences having "
            "equal number of 0 & 1 is "
         << generateSubsequences(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for Longest subsequence
// having equal numbers of 0 and 1
import java.io.*;
class GFG {

static int generateSubsequences(int arr[],
                                   int n)
{

    // store the maximum length
    // sub_sequence having equal
    // number of zeros and ones
    int result = 0;

    // Number of subsequences
    // is (2**n -1)
    long opsize = (long) Math.pow(2, n);

    // Run from counter
    // 000..1 to 111..1
    for (int counter = 1; counter < opsize;
                                counter++)
    {

        // store count of zeros and one
        int countzero = 0;
        int countone = 0, current_size = 0;

        for (int j = 0; j < n; j++)
        {

            // Check if jth bit in the
            // counter is set. If set
            // then print jth element
            // from arr[]
            if ((counter & (1 << j))>0)

            {
                if (arr[j]>0)
                    countone++;
                else
                    countzero++;
                current_size++;
            }
        }

        // update maximum size
        if (countzero == countone)
            result = Math.max(current_size,
                                   result);
    }
    return result;
}

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { 1, 0, 0, 1,
                0, 0, 0, 1 };
        int n = arr.length;
        System.out.println( "largest Subsequences having "+
                             "equal number of 0 & 1 is "+
                            generateSubsequences(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python code to find the
# length of longest subsequence
# having equal no of 1 and 0

def generateSubsequences(a, n):
    result = 0

    # Number of subsequences
    # is (2**n -1)
    opsize = 2**n

    # Run from counter
    # 000..1 to 111..1
    for counter in range(opsize):

        # store count of zeros and one
        countzero, countone = 0, 0
        current_size = 0

        for j in range(n):

            # Check if jth bit in the
            # counter is set. If set then
            # print jth element from arr[]
            if counter & (1 << j):
                if arr[j] == True:
                    countone += 1
                else:
                    countzero += 1
                current_size += 1

        # update maximum size
        if countzero == countone:
            result = max(current_size,
                         result)
    return result

# Driver code
arr = [ 1, 0, 0, 1, 0, 0, 0, 1 ]
n = len(arr)
print("largest Subsequences having" +
        " equal number of 0 & 1 is ",
        generateSubsequences(arr, n))

# This code is contributed
# by "Abhishek Sharma 44"
```

## C#

```
// C# program for Longest subsequence
// having equal numbers of 0 and 1
using System;
class GFG {

static int generateSubsequences(int []arr,
                                int n)
{

    // store the maximum length
    // sub_sequence having equal
    // number of zeros and ones
    int result = 0;

    // Number of subsequences
    // is (2**n -1)
    uint opsize = (uint) Math.Pow(2, n);

    // Run from counter
    // 000..1 to 111..1
    for (int counter = 1; counter < opsize;
                                counter++)
    {

        // store count of zeros and one
        int countzero = 0;
        int countone = 0, current_size = 0;

        for (int j = 0; j < n; j++)
        {

            // Check if jth bit in the
            // counter is set. If set
            // then print jth element
            // from arr[]
            if ((counter & (1 << j))>0)

            {
                if (arr[j]>0)
                    countone++;
                else
                    countzero++;
                current_size++;
            }
        }

        // update maximum size
        if (countzero == countone)
            result = Math.Max(current_size,
                                result);
    }
    return result;
}

    // Driver Code
    public static void Main ()
    {
        int []arr = { 1, 0, 0, 1,
                         0, 0, 0, 1 };
        int n = arr.Length;
        Console.WriteLine("largest Subsequences having "+
                          "equal number of 0 & 1 is "+
                           generateSubsequences(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the length
// of longest subsequence have
// equal no of 1 and 0

function generateSubsequences($arr,
                              $n)
{

    // store the maximum length
    // sub_sequence having equal
    // number of zeros and ones
    $result = 0;

    // Number of subsequences
    // is (2**n -1)
    $opsize = pow(2, $n);

    // Run from counter 000..1
    // to 111..1
    for ($counter = 1; $counter < $opsize;
                       $counter++)
    {

        // store count of zeros and one
        $countzero = 0;
        $countone = 0; $current_size = 0;

        for ($j = 0; $j < $n; $j++)
        {

            // Check if jth bit in
            // the counter is set
            // If set then print jth
            // element from arr[]
            if ($counter & (1 << $j))
            {
                if ($arr[$j])
                    $countone++;
                else
                    $countzero++;
                $current_size++;
            }
        }

        // update maximum size
        if ($countzero == $countone)
            $result = max($current_size,
                          $result);
    }
    return $result;
}

// Driver Code
$arr = array(1, 0, 0, 1, 0, 0, 0, 1);
$n = count($arr);
echo "largest Subsequences having " ,
        "equal number of 0 & 1 is " ,
      generateSubsequences($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program for Longest subsequence
// having equal numbers of 0 and 1

function generateSubsequences(arr, n)
{
    // store the maximum length
    // sub_sequence having equal
    // number of zeros and ones
    var result = 0;

    // Number of subsequences is (2**n -1)
    var opsize = Math.pow(2, n);

    // Run from counter 000..1 to 111..1
    for (var counter = 1; counter < opsize;
                          counter++)
    {

        // store count of zeros and one
        var countzero = 0;
        var countone = 0, current_size = 0;

        for (var j = 0; j < n; j++)
        {

            // Check if jth bit in the
            // counter is set. If set
            // then print jth element
            // from arr[]
            if (counter & (1 << j))

            {
                if (arr[j])
                    countone++;
                else
                    countzero++;
                current_size++;
            }
        }

        // update maximum size
        if (countzero == countone)
            result = Math.max(current_size,
                              result);
    }
    return result;
}

// Driver Code
var arr = [ 1, 0, 0, 1,
            0, 0, 0, 1 ];
var n = arr.length;
document.write( "largest Subsequences having "+
        "equal number of 0 & 1 is "
     + generateSubsequences(arr, n));

</script>
```

**输出:**

```
largest Subsequences having equal number of 0 & 1 is 6
```

时间复杂度:(n*2^n)
**高效的解决方案**是对二进制数组中的 0&1 进行计数，并通过将其与 2 相乘，最后返回 0&1 计数之间的最小值。

```
 arr[] = { 1, 0, 0, 1, 0, 0, 0, 1 } 
 output : 6
    here larges sub_sequencer :
           { 1  0  0  1  0 1} or {1 0 1 0 0 1 }  
  If we observe carefully then we notice that 
  we just have to find minimum counts between 
  zeros & ones and multiplying it with 2
  ( because we always get even length sub_sequence)
```

以下是以上想法的实现

## C++

```
// Efficient CPP program to find
// length of the longest subsequence
// with equal number of 0s and 1s.
#include <bits/stdc++.h>
using namespace std;

int largestSubsequences(int arr[], int n)
{
    // store count of zeros and one
    int countzero = 0, countone = 0;

    // traverse binary array and count
    // zeros and ones
    for (int i = 0; i < n; i++)
        if (arr[i])
            countone++;
        else
            countzero++;

    return min(countone, countzero) * 2;
}

// Driver program
int main()
{
    int arr[] = { 1, 0, 0, 1, 0, 0, 0, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "largest Subsequences having "
         << "equal number of 0 & 1 is "
         << largestSubsequences(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find
// length of the longest subsequence
// with equal number of 0s and 1s.
import java.io.*;
import java.math.*;

class GFG
{
    static int largestSubsequences(int arr[],
                                   int n)
    {
        // store count of zeros and one
        int countzero = 0, countone = 0;

        // traverse binary array and count
        // zeros and ones
        for (int i = 0; i < n; i++)
            if (arr[i] == 1)
                countone++;
            else
                countzero++;

        return Math.min(countone, countzero) * 2;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 1, 0, 0, 1, 0, 0, 0, 1 };
        int n = arr.length;
        System.out.println("largest Subsequences having " +
                              "equal number of 0 & 1 is " +
                              largestSubsequences(arr, n));
    }
}

// This code is contributed by Nikita Tiwari
```

## 蟒蛇 3

```
# Efficient Pyhton code to find
# length of the longest subsequence
# with equal number of 0s and 1s.

def largestSubsequence(arr,n):

    # store count of zeros and one
    countzero = 0
    countone = 0

    # traverse binary array and count
    # zeros and ones
    for i in range(n):
        if arr[i]:
            countone += 1
        else:
            countzero += 1
    return min(countone, countzero) * 2

# Driver Code
arr = [ 1, 0, 0, 1, 0, 0, 0, 1 ]
n = len(arr)
print("largest Subsequences having" +
        " equal number of 0 & 1 is ",
        largestSubsequence(arr, n))

# This code is contributed
# by "Abhishek Sharma 44"
```

## C#

```
// Efficient C# program to find
// length of the longest subsequence
// with equal number of 0s and 1s.
using System;

class GFG
{
    static int largestSubsequences(int[] arr,
                                   int n)
    {
        // store count of zeros and one
        int countzero = 0, countone = 0;

        // traverse binary array and
        // count zeros and ones
        for (int i = 0; i < n; i++)
            if (arr[i] != 0)
                countone++;
            else
                countzero++;

        return Math.Min(countone,
                        countzero) * 2;
    }

    // Driver Code
    static void Main()
    {
        int[] arr = { 1, 0, 0, 1, 0, 0, 0, 1 };

        int n = 8 ;
        Console.Write("largest Subsequences having" +
                       " equal number of 0 & 1 is " +
                        largestSubsequences(arr, n));

    }
}

// This code is contributed by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Efficient PHP program to find
// length of the longest subsequence
// with equal number of 0s and 1s.

function largestSubsequences( $arr, $n)
{
    // store count of zeros and one
    $countzero = 0; $countone = 0;

    // traverse binary array and
    // count zeros and ones
    for ( $i = 0; $i < $n; $i++)
        if ($arr[$i])
            $countone++;
        else
            $countzero++;

    return min($countone, $countzero) * 2;
}

// Driver Code
$arr = array(1, 0, 0, 1,
             0, 0, 0, 1);
$n = count($arr);
echo "largest Subsequences having " ,
        "equal number of 0 & 1 is " ,
       largestSubsequences($arr, $n);

// This code is contributed by Anuj_67.
?>
```

## java 描述语言

```
<script>

// Efficient Javascript program to find
// length of the longest subsequence
// with equal number of 0s and 1s.

function largestSubsequences(arr, n)
{
    // store count of zeros and one
    var countzero = 0, countone = 0;

    // traverse binary array and count
    // zeros and ones
    for (var i = 0; i < n; i++)
        if (arr[i])
            countone++;
        else
            countzero++;

    return Math.min(countone, countzero) * 2;
}

// Driver program
var arr = [1, 0, 0, 1, 0, 0, 0, 1 ];
var n = arr.length;
document.write( "largest Subsequences having "
     + "equal number of 0 & 1 is "
     + largestSubsequences(arr, n));

</script>
```

**输出:**

```
largest Subsequences having equal number of 0 & 1 is 6
```

**时间复杂度:** O(n)