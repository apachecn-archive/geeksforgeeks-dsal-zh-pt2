# 任意排列绝对差的最大和

> 原文:[https://www . geesforgeks . org/max-sum-绝对值差-array/](https://www.geeksforgeeks.org/maximum-sum-absolute-difference-array/)

给定一个数组，我们需要找到给定数组的任意排列的绝对差的最大和。
**例:**

```
Input : { 1, 2, 4, 8 }
Output : 18
Explanation : For the given array there are 
several sequence possible
like : {2, 1, 4, 8}
       {4, 2, 1, 8} and some more.
Now, the absolute difference of an array sequence will be
like for this array sequence {1, 2, 4, 8}, the absolute
difference sum is 
= |1-2| + |2-4| + |4-8| + |8-1|
= 14
For the given array, we get the maximum value for
the sequence {1, 8, 2, 4}
= |1-8| + |8-2| + |2-4| + |4-1|
= 18
```

要解决这个问题，就要贪婪地思考，怎样才能最大化元素的差值，这样才能有最大的和。只有当我们计算一些非常高的值和一些非常低的值(最高–最低)之间的差值时，这才是可能的。这是我们必须用来解决这个问题的想法。让我们看看上面的例子，我们将有序列{1，8，2，4}的最大可能差值，因为在这个序列中我们将得到一些高差值，(|1-8| = 7，|8-2| = 6..).这里，用 8(最高元素)代替 1 和 2，我们得到两个高差值。同样，对于其他值，我们将在其他值之间放置次高的值，因为我们只剩下一个值，即最后放置的 4。
**算法:** *为了得到最大和，我们应该有一个大小元素交替出现的序列。这样做是为了获得最大差异。*
**为上述算法的实现- >**
1。我们将对数组进行排序。
2。从排序的数组中取一个最小的元素和一个最大的元素，构成这个最终序列的一个向量数组，从而计算出最终序列。
3。最后，计算数组元素之间的绝对差之和。
**下面是上面思路的实现:**

## C++

```
// CPP implementation of
// above algorithm
#include <bits/stdc++.h>
using namespace std;

int MaxSumDifference(int a[], int n)
{
    // final sequence stored in the vector
    vector<int> finalSequence;

    // sort the original array
    // so that we can retrieve
    // the large elements from
    // the end of array elements
    sort(a, a + n);

    // In this loop first we will insert
    // one smallest element not entered
    // till that time in final sequence
    // and then enter a highest element
    // (not entered till that time) in
    // final sequence so that we
    // have large difference value. This
    // process is repeated till all array
    // has completely entered in sequence.
    // Here, we have loop till n/2 because
    // we are inserting two elements at a
    // time in loop.
    for (int i = 0; i < n / 2; ++i) {
        finalSequence.push_back(a[i]);
        finalSequence.push_back(a[n - i - 1]);
    }

    // If there are odd elements, push the
    // middle element at the end.
    if (n % 2 != 0)
        finalSequence.push_back(a[n/2]);

    // variable to store the
    // maximum sum of absolute
    // difference
    int MaximumSum = 0;

    // In this loop absolute difference
    // of elements for the final sequence
    // is calculated.
    for (int i = 0; i < n - 1; ++i) {
        MaximumSum = MaximumSum + abs(finalSequence[i] -
                                  finalSequence[i + 1]);
    }

    // absolute difference of last element
    // and 1st element
    MaximumSum = MaximumSum + abs(finalSequence[n - 1] -
                                      finalSequence[0]);

    // return the value
    return MaximumSum;
}

// Driver function
int main()
{
    int a[] = { 1, 2, 4, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << MaxSumDifference(a, n) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above algorithm
import java.io.*;
import java.util.*;

public class GFG {

    static int MaxSumDifference(Integer []a, int n)
    {

        // final sequence stored in the vector
        List<Integer> finalSequence =
                        new ArrayList<Integer>();

        // sort the original array
        // so that we can retrieve
        // the large elements from
        // the end of array elements
        Arrays.sort(a);

        // In this loop first we will insert
        // one smallest element not entered
        // till that time in final sequence
        // and then enter a highest element
        // (not entered till that time) in
        // final sequence so that we
        // have large difference value. This
        // process is repeated till all array
        // has completely entered in sequence.
        // Here, we have loop till n/2 because
        // we are inserting two elements at a
        // time in loop.
        for (int i = 0; i < n / 2; ++i) {
            finalSequence.add(a[i]);
            finalSequence.add(a[n - i - 1]);
        }

        // If there are odd elements, push the
        // middle element at the end.
        if (n % 2 != 0)
            finalSequence.add(a[n/2]);

        // variable to store the
        // maximum sum of absolute
        // difference
        int MaximumSum = 0;

        // In this loop absolute difference
        // of elements for the final sequence
        // is calculated.
        for (int i = 0; i < n - 1; ++i) {
            MaximumSum = MaximumSum +
                  Math.abs(finalSequence.get(i)
                   - finalSequence.get(i + 1));
        }

        // absolute difference of last element
        // and 1st element
        MaximumSum = MaximumSum +
              Math.abs(finalSequence.get(n - 1)
                       - finalSequence.get(0));

        // return the value
        return MaximumSum;
    }

    // Driver Code
    public static void main(String args[])
    {
        Integer []a = { 1, 2, 4, 8 };
        int n = a.length;

        System.out.print(MaxSumDifference(a, n));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 蟒蛇 3

```
import numpy as np
class GFG:

    def MaxSumDifference(a,n):
        # sort the original array
        # so that we can retrieve
        # the large elements from
        # the end of array elements
        np.sort(a);

        # In this loop first we will
        # insert one smallest element
        # not entered till that time
        # in final sequence and then
        # enter a highest element(not
        # entered till that time) in
        # final sequence so that we
        # have large difference value.
        # This process is repeated till
        # all array has completely
        # entered in sequence. Here,
        # we have loop till n/2 because
        # we are inserting two elements
        # at a time in loop.
        j = 0
        finalSequence = [0 for x in range(n)]
        for i in range(0, int(n / 2)):
            finalSequence[j] = a[i]
            finalSequence[j + 1] = a[n - i - 1]
            j = j + 2

        # If there are odd elements, push the
        # middle element at the end.
        if (n % 2 != 0):
           finalSequence[n-1] = a[n//2 + 1]

        # variable to store the
        # maximum sum of absolute
        # difference
        MaximumSum = 0

        # In this loop absolute
        # difference of elements
        # for the final sequence
        # is calculated.
        for i in range(0, n - 1):
            MaximumSum = (MaximumSum +
                          abs(finalSequence[i] -
                              finalSequence[i + 1]))

        # absolute difference of last
        # element and 1st element
        MaximumSum = (MaximumSum +
                      abs(finalSequence[n - 1] -
                         finalSequence[0]));

        # return the value
        print (MaximumSum)

# Driver Code
a = [ 1, 2, 4, 8 ]
n = len(a)
GFG.MaxSumDifference(a, n);

# This code is contributed
# by Prateek Bajaj
```

## C#

```
// C# implementation of
// above algorithm
using System;
using System.Collections.Generic;
class GFG {

    static int MaxSumDifference(int []a, int n)
    {

        // final sequence stored in the vector
        List<int> finalSequence = new List<int>();

        // sort the original array
        // so that we can retrieve
        // the large elements from
        // the end of array elements
        Array.Sort(a);

        // In this loop first we will insert
        // one smallest element not entered
        // till that time in final sequence
        // and then enter a highest element
        // (not entered till that time) in
        // final sequence so that we
        // have large difference value. This
        // process is repeated till all array
        // has completely entered in sequence.
        // Here, we have loop till n/2 because
        // we are inserting two elements at a
        // time in loop.
        for (int i = 0; i < n / 2; ++i) {
            finalSequence.Add(a[i]);
            finalSequence.Add(a[n - i - 1]);
        }

        // If there are odd elements, push the
        // middle element at the end.
        if (n % 2 != 0)
            finalSequence.Add(a[n/2]);

        // variable to store the
        // maximum sum of absolute
        // difference
        int MaximumSum = 0;

        // In this loop absolute difference
        // of elements for the final sequence
        // is calculated.
        for (int i = 0; i < n - 1; ++i) {
            MaximumSum = MaximumSum + Math.Abs(finalSequence[i] -
                                    finalSequence[i + 1]);
        }

        // absolute difference of last element
        // and 1st element
        MaximumSum = MaximumSum + Math.Abs(finalSequence[n - 1] -
                                        finalSequence[0]);

        // return the value
        return MaximumSum;
    }

    // Driver Code
    public static void Main()
    {
        int []a = { 1, 2, 4, 8 };
        int n = a.Length;

        Console.WriteLine(MaxSumDifference(a, n));
    }
}

// This code is contributed by
// Manish Shaw (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above algorithm

function MaxSumDifference(&$a, $n)
{
    // final sequence stored in the vector
    $finalSequence = array();

    // sort the original array so that we
    // can retrieve the large elements from
    // the end of array elements
    sort($a);

    // In this loop first we will insert one
    // smallest element not entered till that
    // time in final sequence and then enter
    // a highest element (not entered till
    // that time) in final sequence so that we
    // have large difference value. This process
    // is repeated till all array has completely 
    // entered in sequence.
    // Here, we have loop till n/2 because
    // we are inserting two elements at a
    // time in loop.
    for ($i = 0; $i < $n / 2; ++$i)
    {
        array_push($finalSequence, $a[$i]);
        array_push($finalSequence, $a[$n - $i - 1]);
    }

    // If there are odd elements, push the
    // middle element at the end.
    if ($n % 2 != 0)
        array_push($finalSequence, $a[$n-1]);

    // variable to store the maximum sum
    // of absolute difference
    $MaximumSum = 0;

    // In this loop absolute difference
    // of elements for the final sequence
    // is calculated.
    for ($i = 0; $i < $n - 1; ++$i)
    {
        $MaximumSum = $MaximumSum + abs($finalSequence[$i] -
                                        $finalSequence[$i + 1]);
    }

    // absolute difference of last element
    // and 1st element
    $MaximumSum = $MaximumSum + abs($finalSequence[$n - 1] -
                                    $finalSequence[0]);

    // return the value
    return $MaximumSum;
}

// Driver Code
$a = array(1, 2, 4, 8 );
$n = sizeof($a);
echo MaxSumDifference($a, $n) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript implementation of
// above algorithm

    function MaxSumDifference(a,n)
    {
        // final sequence stored in the vector
        let finalSequence = [];

        // sort the original array
        // so that we can retrieve
        // the large elements from
        // the end of array elements
        a.sort(function(a,b){return a-b;});

        // In this loop first we will insert
        // one smallest element not entered
        // till that time in final sequence
        // and then enter a highest element
        // (not entered till that time) in
        // final sequence so that we
        // have large difference value. This
        // process is repeated till all array
        // has completely entered in sequence.
        // Here, we have loop till n/2 because
        // we are inserting two elements at a
        // time in loop.
        for (let i = 0; i < n / 2; ++i) {
            finalSequence.push(a[i]);
            finalSequence.push(a[n - i - 1]);
        }

        // If there are odd elements, push the
        // middle element at the end.
        if (n % 2 != 0)
            finalSequence.push(a[Math.floor(n/2)]);

        // variable to store the
        // maximum sum of absolute
        // difference
        let MaximumSum = 0;

        // In this loop absolute difference
        // of elements for the final sequence
        // is calculated.
        for (let i = 0; i < n - 1; ++i) {
            MaximumSum = MaximumSum +
                  Math.abs(finalSequence[i]
                   - finalSequence[i+1]);
        }

        // absolute difference of last element
        // and 1st element
        MaximumSum = MaximumSum +
              Math.abs(finalSequence[n-1]
                       - finalSequence[0]);

        // return the value
        return MaximumSum;
    }

    // Driver Code
    let a=[1, 2, 4, 8 ];
    let n = a.length;
    document.write(MaxSumDifference(a, n));

    // This code is contributed by rag2127
</script>
```

**输出:**

```
18
```