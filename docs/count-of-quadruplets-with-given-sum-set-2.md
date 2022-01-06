# 给定总和的四胞胎计数|第 2 组

> 原文:[https://www . geesforgeks . org/给定和集的四胞胎计数-2/](https://www.geeksforgeeks.org/count-of-quadruplets-with-given-sum-set-2/)

给定四个包含整数元素的数组和一个整数**和**，任务是对四胞胎进行计数，使得每个元素从不同的数组中选择，并且所有四个元素的和等于给定的和。
**例:**

> **输入:** P[] = {0，2}，Q[] = {-1，-2}，R[] = {2，1}，S[] = {2，-1}，和= 0
> **输出:** 2
> (0，-1，2，-1)和(2，-2，1，-1)是必需的四胞胎。
> **输入:** P[] = {1，-1，2，3，4}，Q[] = {3，2，4}，R[] = {-2，-1，2，1}，S[] = {4，-1}，和= 3
> **输出:** 10

**方法:**我们选择任意两个数组，计算所有可能的和，并将它们的计数保存在地图中。使用剩下的两个数组，我们计算所有可能的和，并检查它们的加法逆在映射中存在多少次，这将是所需四胞胎的计数。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of the required quadruplets
int countQuadruplets(int arr1[], int n1, int arr2[], int n2,
                     int arr3[], int n3, int arr4[], int n4, int value)
{
    int cnt = 0;
    unordered_map<int, int> sum;

    // All possible sums from arr1[] and arr2[]
    for (int i = 0; i < n1; i++)
        for (int j = 0; j < n2; j++)
            sum[arr1[i] + arr2[j]]++;

    // Find the count of quadruplets
    for (int i = 0; i < n3; i++)
        for (int j = 0; j < n4; j++)
            cnt += sum[value - (arr3[i] + arr4[j])];

    return cnt;
}

// Driver code
int main()
{

    int arr1[] = { 0, 2 };
    int arr2[] = { -1, -2 };
    int arr3[] = { 2, 1 };
    int arr4[] = { 2, -1 };
    int sum = 0;
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    int n2 = sizeof(arr2) / sizeof(arr2[0]);
    int n3 = sizeof(arr3) / sizeof(arr3[0]);
    int n4 = sizeof(arr4) / sizeof(arr4[0]);

    cout << countQuadruplets(arr1, n1, arr2, n2, arr3, n3, arr4, n4, sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return the count of the required quadruplets
    static int countQuadruplets(int arr1[], int n1, int arr2[], int n2,
                                int arr3[], int n3, int arr4[], int n4, int value)
    {
        int cnt = 0;
        Map<Integer, Integer> sum = new HashMap<>();

        // All possible sums from arr1[] and arr2[]
        for (int i = 0; i < n1; i++)
            for (int j = 0; j < n2; j++) {
                if (sum.containsKey(arr1[i] + arr2[j])) {
                    sum.put(arr1[i] + arr2[j], sum.get(arr1[i] + arr2[j]) + 1);
                }
                else {
                    sum.put(arr1[i] + arr2[j], 1);
                }
            }

        // Find the count of quadruplets
        for (int i = 0; i < n3; i++)
            for (int j = 0; j < n4; j++)
                if (sum.containsKey(value - (arr3[i] + arr4[j])))
                    cnt += sum.get(value - (arr3[i] + arr4[j]));

        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr1[] = { 0, 2 };
        int arr2[] = { -1, -2 };
        int arr3[] = { 2, 1 };
        int arr4[] = { 2, -1 };
        int sum = 0;
        int n1 = arr1.length;
        int n2 = arr2.length;
        int n3 = arr3.length;
        int n4 = arr4.length;

        System.out.println(countQuadruplets(arr1, n1, arr2, n2,
                                            arr3, n3, arr4, n4, sum));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count
# of the required quadruplets
def countQuadruplets(arr1, n1, arr2, n2,
                     arr3, n3, arr4, n4, value):
    cnt = 0
    sum = {i:0 for i in range(-4, 10, 1)}

    # All possible sums from arr1[] and arr2[]
    for i in range(n1):
        for j in range(n2):
            sum[arr1[i] + arr2[j]] += 1

    # Find the count of quadruplets
    for i in range(n3):
        for j in range(n4):
            cnt += sum[value - (arr3[i] + arr4[j])]

    return cnt

# Driver code
if __name__ == '__main__':
    arr1 = [0, 2]
    arr2 = [-1, -2]
    arr3 = [2, 1]
    arr4 = [2, -1]
    sum = 0
    n1 = len(arr1)
    n2 = len(arr2)
    n3 = len(arr3)
    n4 = len(arr4)

    print(countQuadruplets(arr1, n1, arr2, n2,
                           arr3, n3, arr4, n4, sum))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to return the count of the required quadruplets
    static int countQuadruplets(int[] arr1, int n1,
                                int[] arr2, int n2,
                                int[] arr3, int n3,
                                int[] arr4, int n4, int value)
    {
        int cnt = 0;
        Dictionary<int, int> sum = new Dictionary<int, int>();

        // All possible sums from arr1[] and arr2[]
        for (int i = 0; i < n1; i++)
            for (int j = 0; j < n2; j++) {
                if (sum.ContainsKey(arr1[i] + arr2[j])) {
                    var obj = sum[arr1[i] + arr2[j]] + 1;
                    sum.Remove(arr1[i] + arr2[j]);
                    sum.Add(arr1[i] + arr2[j], obj);
                }
                else {
                    sum.Add(arr1[i] + arr2[j], 1);
                }
            }

        // Find the count of quadruplets
        for (int i = 0; i < n3; i++)
            for (int j = 0; j < n4; j++)
                if (sum.ContainsKey(value - (arr3[i] + arr4[j])))
                    cnt += sum[value - (arr3[i] + arr4[j])];

        return cnt;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr1 = { 0, 2 };
        int[] arr2 = { -1, -2 };
        int[] arr3 = { 2, 1 };
        int[] arr4 = { 2, -1 };
        int sum = 0;
        int n1 = arr1.Length;
        int n2 = arr2.Length;
        int n3 = arr3.Length;
        int n4 = arr4.Length;

        Console.WriteLine(countQuadruplets(arr1, n1, arr2, n2,
                                           arr3, n3, arr4, n4, sum));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of the required quadruplets
function countQuadruplets($arr1, $n1, $arr2, $n2,
                    $arr3, $n3, $arr4, $n4, $value)
{
    $cnt = 0;
    $sum = array();

    for ($i = 0; $i < $n1; $i++)
        for ($j = 0; $j < $n2; $j++)
            $sum[$arr1[$i] + $arr2[$j]] = 0 ;

    // All possible sums from arr1[] and arr2[]
    for ($i = 0; $i < $n1; $i++)
        for ($j = 0; $j < $n2; $j++)
            $sum[$arr1[$i] + $arr2[$j]]++;

    // Find the count of quadruplets
    for ($i = 0; $i < $n3; $i++)
        for ($j = 0; $j < $n4; $j++)
            $cnt += $sum[$value - ($arr3[$i] + $arr4[$j])];

    return $cnt;
}

    // Driver code
    $arr1 = array(0, 2 );
    $arr2 = array( -1, -2 );
    $arr3 = array( 2, 1 );
    $arr4 = array( 2, -1 );
    $sum = 0;
    $n1 = count($arr1) ;
    $n2 = count($arr2) ;
    $n3 = count($arr3) ;
    $n4 = count($arr4) ;

    echo countQuadruplets($arr1, $n1, $arr2, $n2,
                        $arr3, $n3, $arr4, $n4, $sum);

    // This code is contributed by Ryuga

?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of the required quadruplets
function countQuadruplets(arr1, n1, arr2, n2, arr3, n3, arr4, n4, value)
{
    var cnt = 0;
    var sum = new Map();

    // All possible sums from arr1[] and arr2[]
    for (var i = 0; i < n1; i++)
    {
        for (var j = 0; j < n2; j++)
        {
            if(sum.has(arr1[i] + arr2[j]))
            {
                sum.set(arr1[i] + arr2[j], sum.get(arr1[i] + arr2[j])+1);
            }
            else
            {
                sum.set(arr1[i] + arr2[j], 1);
            }
        }
    }

    // Find the count of quadruplets
    for (var i = 0; i < n3; i++)
        for (var j = 0; j < n4; j++)
            if(sum.has((value - (arr3[i] + arr4[j]))))
            {
                cnt += sum.get((value - (arr3[i] + arr4[j])));
            }

    return cnt;
}

// Driver code
var arr1 = [0, 2];
var arr2 = [-1, -2];
var arr3 = [2, 1];
var arr4 = [2, -1];
var sum = 0;
var n1 = arr1.length;
var n2 = arr2.length;
var n3 = arr3.length;
var n4 = arr4.length;
document.write( countQuadruplets(arr1, n1, arr2, n2, arr3, n3, arr4, n4, sum));

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
2
```