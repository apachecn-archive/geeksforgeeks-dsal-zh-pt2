# 给定总和的四胞胎数

> 原文:[https://www . geesforgeks . org/带给定总和的四胞胎计数/](https://www.geeksforgeeks.org/count-of-quadruplets-with-given-sum/)

给定四个包含整数元素的数组和一个整数**和**，任务是对四胞胎进行计数，使得每个元素从不同的数组中选择，并且所有四个元素的和等于给定的和。

**示例:**

> **输入:** P[] = {0，2}，Q[] = {-1，-2}，R[] = {2，1}，S[] = {2，-1}，和= 0
> **输出:** 2
> (0，-1，2，-1)和(2，-2，1，-1)是必需的四胞胎。
> **输入:** P[] = {1，-1，2，3，4}，Q[] = {3，2，4}，R[] = {-2，-1，2，1}，S[] = {4，-1}，和= 3
> **输出:** 10

**方法:**生成所有可能的四胞胎，并计算每个四胞胎的总和。计算所有这样的四胞胎，它们的总和等于给定的总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of the required quadruplets
int countQuadruplets(int arr1[], int n1, int arr2[], int n2,
                     int arr3[], int n3, int arr4[], int n4, int sum)
{

    // To store the count of required quadruplets
    int cnt = 0;

    // For arr1[]
    for (int i = 0; i < n1; i++) {

        // For arr2[]
        for (int j = 0; j < n2; j++) {

            // For arr3[]
            for (int k = 0; k < n3; k++) {

                // For arr4[]
                for (int l = 0; l < n4; l++) {

                    // If current quadruplet has the required sum
                    if (arr1[i] + arr2[j] + arr3[k] + arr4[l] == sum) {
                        cnt++;
                    }
                }
            }
        }
    }

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
// Java program to implement
// the above approach

class GFG
{

// Function to return the count of the required quadruplets
static int countQuadruplets(int arr1[], int n1, int arr2[], int n2,
                    int arr3[], int n3, int arr4[], int n4, int sum)
{

    // To store the count of required quadruplets
    int cnt = 0;

    // For arr1[]
    for (int i = 0; i < n1; i++)
    {

        // For arr2[]
        for (int j = 0; j < n2; j++)
        {

            // For arr3[]
            for (int k = 0; k < n3; k++)
            {

                // For arr4[]
                for (int l = 0; l < n4; l++)
                {

                    // If current quadruplet has the required sum
                    if (arr1[i] + arr2[j] + arr3[k] + arr4[l] == sum)
                    {
                        cnt++;
                    }
                }
            }
        }
    }

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
# Python implementation of the approach

# Function to return the count of the required quadruplets
def countQuadruplets(P, Q, R, S, sum):

    # To store the count of required quadruplets
    cnt = 0

    # Using four loops generate all possible quadruplets
    for elem1 in P:
        for elem2 in Q:
            for elem3 in R:
                for elem4 in S:
                    if elem1 + elem2 + elem3 + elem4 == sum:
                        cnt = cnt + 1
    return cnt

# Driver code
P = [ 0, 2]
Q = [-1, -2]
R = [2, 1]
S = [ 2, -1]
sum = 0

print(countQuadruplets(P, Q, R, S, sum))
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG
{

// Function to return the count of the required quadruplets
static int countQuadruplets(int []arr1, int n1, int []arr2, int n2,
                    int []arr3, int n3, int []arr4, int n4, int sum)
{

    // To store the count of required quadruplets
    int cnt = 0;

    // For arr1[]
    for (int i = 0; i < n1; i++)
    {

        // For arr2[]
        for (int j = 0; j < n2; j++)
        {

            // For arr3[]
            for (int k = 0; k < n3; k++)
            {

                // For arr4[]
                for (int l = 0; l < n4; l++)
                {

                    // If current quadruplet has the required sum
                    if (arr1[i] + arr2[j] + arr3[k] + arr4[l] == sum)
                    {
                        cnt++;
                    }
                }
            }
        }
    }

    return cnt;
}

// Driver code
static public void Main ()
{

    int []arr1 = { 0, 2 };
    int []arr2 = { -1, -2 };
    int []arr3 = { 2, 1 };
    int []arr4 = { 2, -1 };
    int sum = 0;
    int n1 = arr1.Length;
    int n2 = arr2.Length;
    int n3 = arr3.Length;
    int n4 = arr4.Length;
    Console.WriteLine(countQuadruplets(arr1, n1, arr2, n2,
                                    arr3, n3, arr4, n4, sum));

}
}

// This code contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of the required quadruplets
function countQuadruplets($arr1, $n1, $arr2,$n2,
                $arr3, $n3, $arr4, $n4, $sum)
{

    // To store the count of required quadruplets
    $cnt = 0;

    // For arr1[]
    for ($i = 0; $i < $n1; $i++)
    {

        // For arr2[]
        for ($j = 0; $j < $n2; $j++)
        {

            // For arr3[]
            for ($k = 0; $k < $n3; $k++)
            {

                // For arr4[]
                for ( $l = 0; $l < $n4; $l++)
                {

                    // If current quadruplet has the required sum
                    if ($arr1[$i] + $arr2[$j] + $arr3[$k] +
                                       $arr4[$l] == $sum)
                    {
                        $cnt++;
                    }
                }
            }
        }
    }

    return $cnt;
}

// Driver code
$arr1 = array (0, 2 );
$arr2 = array( -1, -2 );
$arr3 = array( 2, 1 );
$arr4 =array( 2, -1 );
$sum = 0;
$n1 = count($arr1);
$n2 =count($arr2);
$n3 = count($arr3);
$n4 = count($arr4);

echo countQuadruplets($arr1, $n1, $arr2, $n2,
                    $arr3, $n3, $arr4, $n4, $sum);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Function to return the count of the required quadruplets
    function countQuadruplets(arr1, n1, arr2, n2, arr3, n3, arr4, n4, sum)
    {

        // To store the count of required quadruplets
        let cnt = 0;

        // For arr1[]
        for (let i = 0; i < n1; i++)
        {

            // For arr2[]
            for (let j = 0; j < n2; j++)
            {

                // For arr3[]
                for (let k = 0; k < n3; k++)
                {

                    // For arr4[]
                    for (let l = 0; l < n4; l++)
                    {

                        // If current quadruplet has the required sum
                        if (arr1[i] + arr2[j] + arr3[k] + arr4[l] == sum)
                        {
                            cnt++;
                        }
                    }
                }
            }
        }

        return cnt;
    }

    let arr1 = [ 0, 2 ];
    let arr2 = [ -1, -2 ];
    let arr3 = [ 2, 1 ];
    let arr4 = [ 2, -1 ];
    let sum = 0;
    let n1 = arr1.length;
    let n2 = arr2.length;
    let n3 = arr3.length;
    let n4 = arr4.length;
    document.write(countQuadruplets(arr1, n1, arr2, n2,
                                    arr3, n3, arr4, n4, sum));

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(n<sup>4</sup>)
T5】空间复杂度: O(1)

**有效方法:**将来自两个不同数组的两个元素的所有可能和的频率存储在一个映射中。迭代其他两个数组，找到这两个数组中任意两个元素的和，让它成为 **cur_sum** 。如果图中存在**sum–cur _ sum**，这意味着在四个不同的数组中存在四个元素，其和等于**和。**

实施上述方法:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of the required quadruplets
int countQuadruplets(int arr1[], int n1, int arr2[], int n2,
                    int arr3[], int n3, int arr4[], int n4, int sum)
{

    // To store the count of required quadruplets
    int cnt = 0;
      // To store the frequency of sum of
    // two elements of two different arrays
    unordered_map<int,int> freq;
    // For arr1[]
    for (int i = 0; i < n1; i++) {

        // For arr2[]
        for (int j = 0; j < n2; j++) {

            freq[arr1[i]+arr2[j]]++;
        }
    }

      // for arr3[]
   for (int i = 0; i < n3; i++) {

        // For arr4[]
        for (int j = 0; j < n4; j++) {
            int cur_sum = arr3[i]+arr4[j];
            cnt+=freq[sum-cur_sum];
        }
    }
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

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of the required quadruplets
from collections import defaultdict

def countQuadruplets(arr1, n1, arr2, n2, arr, n3, arr4, n4, S):

    # To store the count of required quadruplets
    cnt = 0
    # To store the frequency of S of
    # two elements of two different arrays
    freq = defaultdict(int)
    # For arr1[]
    for i in range(n1):

        # For arr2[]
        for j in range(n2):

            freq[arr1[i] + arr2[j]] += 1

    # for arr3[]
    for i in range(n3):

        # For arr4[]
        for j in range(n4):
            cur_S = arr3[i] + arr4[j]
            cnt += freq[S - cur_S]

    return cnt

# Driver code
if __name__ == "__main__":

    arr1 = [0, 2]
    arr2 = [-1, -2]
    arr3 = [2, 1]
    arr4 = [2, -1]
    S = 0
    n1 = len(arr1)
    n2 = len(arr2)
    n3 = len(arr3)
    n4 = len(arr4)

    print(countQuadruplets(arr1, n1, arr2, n2, arr3, n3, arr4, n4, S))
```

**时间复杂度:** O(n*n)

**辅助空间:** O(n)