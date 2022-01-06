# 最大和交替子序列

> 原文:[https://www . geesforgeks . org/maximum-sum-alternative-subsequence-sum/](https://www.geeksforgeeks.org/maximum-sum-alternating-subsequence-sum/)

给定一个数组，任务是从第一个元素开始寻找最大和交替子序列的和。这里的交替序列是指先递减，再递增，再递减……例如 10，5，14，3 是交替序列。
注意，此处不考虑相反类型的序列(递增-递减-递增-…)交替。
**例:**

```
Input :  arr[] = {4, 3, 8, 5, 3, 8}  
Output :  28
Explanation:
The alternating subsequence (starting with first element) 
that has above maximum sum is {4, 3, 8, 5, 8}

Input : arr[] = {4, 8, 2, 5, 6, 8} 
Output :  14
The alternating subsequence (starting with first element) 
that has above maximum sum is {4, 2, 8}
```

这个问题类似于[最长递增子序列(LIS)问题。](https://www.geeksforgeeks.org/dynamic-programming-set-3-longest-increasing-subsequence/)并且可以使用动态规划求解。

```
Create two empty array that store result of maximum
sum  of alternate sub-sequence
inc[] : inc[i] stores results of maximum sum alternating
        subsequence ending with arr[i] such that arr[i]
        is greater than previous element of the subsequence 
dec[] : dec[i] stores results of maximum sum alternating
        subsequence ending with arr[i] such that arr[i]
        is less than previous element of the subsequence 

Include first element of 'arr' in both inc[] and dec[] 
inc[0] = dec[0] = arr[0]

// Maintain a flag i.e. it will makes the greater
// elements count only if the first decreasing element
// is counted.
flag  = 0 

Traversal two loops
  i goes from 1 to  n-1 
    j goes 0 to i-1
      IF arr[j] > arr[i]
        dec[i] = max(dec[i], inc[j] + arr[i])

        // Denotes first decreasing is found
        flag = 1 

      ELSE IF arr[j] < arr[i] && flag == 1 
        inc[i] = max(inc[i], dec[j]+arr[i]);

Final Last Find maximum value inc[] and dec[] .
```

下面是上述想法的实现。
注意:-对于数组的第一个元素是数组中最小元素的情况。输出将只是第一个元素。这是一个需要检查的边缘案例。取一个变量，用数组的第一个值初始化它，然后与其他值进行比较，就会得到最小值。检查最小值是否等于 arr[0]。如果为真，则返回 arr[0]，因为没有递减步长可用于寻找交替子序列。

## C++

```
// C++ program to find sum of maximum
// sum alternating sequence starting with
// first element.
#include <bits/stdc++.h>
using namespace std;

// Return sum of maximum sum alternating
// sequence starting with arr[0] and is first
// decreasing.
int maxAlternateSum(int arr[], int n)
{
    if (n == 1)
        return arr[0];
    // handling the edge case
    int min = arr[0];
    for (int i = 1; i < n; i++) {
        if (min > arr[i])
            min = arr[i];
    }
    if (min == arr[0]) {
        return arr[0];
    }
    // create two empty array that store result of
    // maximum sum of alternate sub-sequence

    // stores sum of decreasing and increasing
    // sub-sequence
    int dec[n];
    memset(dec, 0, sizeof(dec));

    // store sum of increasing and decreasing sun-sequence
    int inc[n];
    memset(inc, 0, sizeof(inc));

    // As per question, first element must be part
    // of solution.
    dec[0] = inc[0] = arr[0];

    int flag = 0;

    // Traverse remaining elements of array
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            // IF current sub-sequence is decreasing the
            // update dec[j] if needed. dec[i] by current
            // inc[j] + arr[i]
            if (arr[j] > arr[i]) {
                dec[i] = max(dec[i], inc[j] + arr[i]);

                // Revert the flag , if first decreasing
                // is found
                flag = 1;
            }

            // If next element is greater but flag should be
            // 1 i.e. this element should be counted after
            // the first decreasing element gets counted
            else if (arr[j] < arr[i] && flag == 1)

                // If current sub-sequence is increasing
                // then update inc[i]
                inc[i] = max(inc[i], dec[j] + arr[i]);
        }
    }

    // find maximum sum in b/w inc[] and dec[]
    int result = INT_MIN;
    for (int i = 0; i < n; i++) {
        if (result < inc[i])
            result = inc[i];
        if (result < dec[i])
            result = dec[i];
    }

    // return maximum sum alternate sun-sequence
    return result;
}

// Driver program
int main()
{
    int arr[] = { 8, 2, 3, 5, 7, 9, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum sum = " << maxAlternateSum(arr, n)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find sum of maximum
// sum alternating sequence starting with
// first element.

public class GFG {
    // Return sum of maximum sum alternating
    // sequence starting with arr[0] and is first
    // decreasing.
    static int maxAlternateSum(int arr[], int n)
    {
        if (n == 1)
            return arr[0];
        // handling the edge case
        int min = arr[0];
        for (int i = 1; i < n; i++) {
            if (min > arr[i])
                min = arr[i];
        }
        if (min == arr[0]) {
            return arr[0];
        }
        // create two empty array that store result of
        // maximum sum of alternate sub-sequence

        // stores sum of decreasing and increasing
        // sub-sequence
        int dec[] = new int[n];

        // store sum of increasing and decreasing
        // sun-sequence
        int inc[] = new int[n];

        // As per question, first element must be part
        // of solution.
        dec[0] = inc[0] = arr[0];

        int flag = 0;

        // Traverse remaining elements of array
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                // IF current sub-sequence is decreasing the
                // update dec[j] if needed. dec[i] by
                // current inc[j] + arr[i]
                if (arr[j] > arr[i]) {
                    dec[i]
                        = Math.max(dec[i], inc[j] + arr[i]);

                    // Revert the flag , if first decreasing
                    // is found
                    flag = 1;
                }

                // If next element is greater but flag
                // should be 1 i.e. this element should be
                // counted after the first decreasing
                // element gets counted
                else if (arr[j] < arr[i] && flag == 1)

                    // If current sub-sequence is increasing
                    // then update inc[i]
                    inc[i]
                        = Math.max(inc[i], dec[j] + arr[i]);
            }
        }

        // find maximum sum in b/w inc[] and dec[]
        int result = Integer.MIN_VALUE;
        for (int i = 0; i < n; i++) {
            if (result < inc[i])
                result = inc[i];
            if (result < dec[i])
                result = dec[i];
        }

        // return maximum sum alternate sun-sequence
        return result;
    }

    // Driver Method
    public static void main(String[] args)
    {
        int arr[] = { 8, 2, 3, 5, 7, 9, 10 };
        System.out.println(
            "Maximum sum = "
            + maxAlternateSum(arr, arr.length));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find sum of maximum
# sum alternating sequence starting with
# first element.

# Return sum of maximum sum alternating
# sequence starting with arr[0] and is
# first decreasing.

def maxAlternateSum(arr, n):

    if (n == 1):
        return arr[0]
    min = arr[0]
    for i in range(1, n):
        if(min > arr[i]):
            min = arr[i]
    if(arr[0] == min):
        return arr[0]
    # Create two empty array that
    # store result of maximum sum
    # of alternate sub-sequence

    # Stores sum of decreasing and
    # increasing sub-sequence
    dec = [0 for i in range(n + 1)]

    # store sum of increasing and
    # decreasing sun-sequence
    inc = [0 for i in range(n + 1)]

    # As per question, first element
    # must be part of solution.
    dec[0] = inc[0] = arr[0]

    flag = 0

    # Traverse remaining elements of array
    for i in range(1, n):

        for j in range(i):

            # IF current sub-sequence is decreasing the
            # update dec[j] if needed. dec[i] by current
            # inc[j] + arr[i]
            if (arr[j] > arr[i]):

                dec[i] = max(dec[i], inc[j] + arr[i])

                # Revert the flag, if first
                # decreasing is found
                flag = 1

            # If next element is greater but flag should be 1
            # i.e. this element should be counted after the
            # first decreasing element gets counted
            elif (arr[j] < arr[i] and flag == 1):

                # If current sub-sequence is
                # increasing then update inc[i]
                inc[i] = max(inc[i], dec[j] + arr[i])

    # Find maximum sum in b/w inc[] and dec[]
    result = -2147483648
    for i in range(n):

        if (result < inc[i]):
            result = inc[i]
        if (result < dec[i]):
            result = dec[i]

    # Return maximum sum
    # alternate sun-sequence
    return result

# Driver program
arr = [8, 2, 3, 5, 7, 9, 10]
n = len(arr)
print("Maximum sum = ",
      maxAlternateSum(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to find sum of maximum
// sum alternating sequence starting with
// first element.
using System;
class GFG {

    // Return sum of maximum
    // sum alternating
    // sequence starting with
    // arr[0] and is first
    // decreasing.
    static int maxAlternateSum(int[] arr, int n)
    {
        if (n == 1)
            return arr[0];
        // handling the edge case
        int min = arr[0];
        for (int i = 1; i < n; i++) {
            if (min > arr[i])
                min = arr[i];
        }
        if (min == arr[0]) {
            return arr[0];
        }
        // create two empty array that
        // store result of maximum sum
        // of alternate sub-sequence
        // stores sum of decreasing
        // and increasing sub-sequence
        int[] dec = new int[n];

        // store sum of increasing and
        // decreasing sun-sequence
        int[] inc = new int[n];

        // As per question, first
        // element must be part
        // of solution.
        dec[0] = inc[0] = arr[0];

        int flag = 0;

        // Traverse remaining elements of array
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {

                // IF current sub-sequence
                // is decreasing the
                // update dec[j] if needed.
                // dec[i] by current
                // inc[j] + arr[i]
                if (arr[j] > arr[i]) {
                    dec[i]
                        = Math.Max(dec[i], inc[j] + arr[i]);

                    // Revert the flag , if
                    // first decreasing
                    // is found
                    flag = 1;
                }

                // If next element is greater
                // but flag should be 1
                // i.e. this element should
                // be counted after the
                // first decreasing element
                // gets counted
                else if (arr[j] < arr[i] && flag == 1)

                    // If current sub-sequence
                    // is increasing then update
                    // inc[i]
                    inc[i]
                        = Math.Max(inc[i], dec[j] + arr[i]);
            }
        }

        // find maximum sum in b/w
        // inc[] and dec[]
        int result = int.MinValue;
        for (int i = 0; i < n; i++) {
            if (result < inc[i])
                result = inc[i];
            if (result < dec[i])
                result = dec[i];
        }

        // return maximum sum
        // alternate sun-sequence
        return result;
    }

    // Driver Method
    public static void Main()
    {
        int[] arr = { 8, 2, 3, 5, 7, 9, 10 };
        Console.Write("Maximum sum = "
                      + maxAlternateSum(arr, arr.Length));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find sum of maximum
// sum alternating sequence starting
// with first element.

// Return sum of maximum sum alternating
// sequence starting with arr[0] and is
// first decreasing.
function maxAlternateSum($arr, $n)
{
    if ($n == 1)
        return $arr[0];
    $min = $arr[0];
     for ($i = 1; $i < $n; $i++)
    { $min = max($min,$arr[$i]);}
  if($arr[0]==$min)
    return $arr[0];
    // create two empty array that store result
    // of maximum sum of alternate sub-sequence

    // stores sum of decreasing and 
    // increasing sub-sequence
    $dec = array_fill(0, $n, 0);

    // store sum of increasing and
    // decreasing sun-sequence
    $inc = array_fill(0, $n, 0);

    // As per question, first element
    // must be part of solution.
    $dec[0] = $inc[0] = $arr[0];

    $flag = 0;

    // Traverse remaining elements of array
    for ($i = 1; $i < $n; $i++)
    {
        for ($j = 0; $j < $i; $j++)
        {
            // IF current sub-sequence is decreasing
            // the update dec[j] if needed. dec[i] 
            // by current inc[j] + arr[i]
            if ($arr[$j] > $arr[$i])
            {
                $dec[$i] = max($dec[$i], $inc[$j] +
                                         $arr[$i]);

                // Revert the flag , if first
                // decreasing is found
                $flag = 1;
            }

            // If next element is greater but flag
            // should be 1 i.e. this element should
            // be counted after the first decreasing
            // element gets counted
            else if ($arr[$j] < $arr[$i] && $flag == 1)

                // If current sub-sequence is increasing
                // then update inc[i]
                $inc[$i] = max($inc[$i], $dec[$j] +
                                         $arr[$i]);
        }
    }

    // find maximum sum in b/w inc[] and dec[]
    $result = -(PHP_INT_MAX - 1);
    for ($i = 0 ; $i < $n; $i++)
    {
        if ($result < $inc[$i])
            $result = $inc[$i];
        if ($result < $dec[$i])
            $result = $dec[$i];
    }

    // return maximum sum alternate sun-sequence
    return $result;
}

// Driver Code
$arr = array(8, 2, 3, 5, 7, 9, 10);
$n = sizeof($arr);
echo "Maximum sum = ",
      maxAlternateSum($arr, $n );

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript program to find sum of maximum
    // sum alternating sequence starting with
    // first element.

    // Return sum of maximum sum alternating
    // sequence starting with arr[0] and is first
    // decreasing.
    function maxAlternateSum(arr, n)
    {
        if (n == 1)
            return arr[0];

        //handling the edge case
        int min = arr[0];
        for (int i=1; i<n; i++){
        if (min>arr[i])
          min = arr[i];
        }
        if (min==arr[0]){
         return arr[0];
         }

       // create two empty array that store result of
       // maximum sum of alternate sub-sequence

        // stores sum of decreasing and increasing
        // sub-sequence
        let dec = new Array(n);
        dec.fill(0);

        // store sum of increasing and decreasing sun-sequence
        let inc = new Array(n);
        inc.fill(0);

        // As per question, first element must be part
        // of solution.
        dec[0] = inc[0] = arr[0];

        let flag = 0 ;

        // Traverse remaining elements of array
        for (let i=1; i<n; i++)
        {
            for (let j=0; j<i; j++)
            {
                // IF current sub-sequence is decreasing the
                // update dec[j] if needed. dec[i] by current
                // inc[j] + arr[i]
                if (arr[j] > arr[i])
                {
                    dec[i] = Math.max(dec[i], inc[j]+arr[i]);

                    // Revert the flag , if first decreasing
                    // is found
                    flag = 1;
                }

                // If next element is greater but flag should be 1
                // i.e. this element should be counted after the
                // first decreasing element gets counted
                else if (arr[j] < arr[i] && flag == 1)

                    // If current sub-sequence is increasing
                    // then update inc[i]
                    inc[i] = Math.max(inc[i], dec[j]+arr[i]);
            }
        }

        // find maximum sum in b/w inc[] and dec[]
        let result = Number.MIN_VALUE;
        for (let i = 0 ; i < n; i++)
        {
            if (result < inc[i])
                result = inc[i];
            if (result < dec[i])
                result = dec[i];
        }

        // return maximum sum alternate sun-sequence
        return result;
    }

    let arr = [8, 2, 3, 5, 7, 9, 10];
    document.write("Maximum sum = " +
                       maxAlternateSum(arr , arr.length));

</script>
```

**Output**

```
Maximum sum = 25

```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n)
本文由[**Sahil Chhabra(KILLER)**](https://www.facebook.com/sahil.chhabra.965)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。