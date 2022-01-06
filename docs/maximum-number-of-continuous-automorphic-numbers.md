# 连续自同构数的最大个数

> 原文:[https://www . geesforgeks . org/最大连续自同构数/](https://www.geeksforgeeks.org/maximum-number-of-continuous-automorphic-numbers/)

给定一个由 N 个元素组成的数组。任务是找到给定数组中连续自同构数的最大数量。
**自同构数:**当且仅当一个数的平方与数本身的位数相同时，该数称为自同构数。

**例如:**

```
-> 76 is automorphic, since 76*76 = 5776(ends in 76)
-> 5 is automorphic, since 5*5 = 25(ends in 5)
```

**示例:**

```
Input :  arr[] = {22, 6, 1, 625, 2, 1, 9376}
Output : 3

Input : arr[] = {99, 42, 31, 1, 5}
Output : 2
```

**进场:**

1.  使用两个名为 current_max 和 max_so_far 的变量遍历数组。用 0 初始化它们。
2.  检查每个元素是否是自同构的。
    *   计算当前数字的平方。
    *   继续从当前数字及其平方的末尾提取和比较数字。
    *   如果发现任何不匹配，则该数不是自同构的。
    *   否则，如果当前数字中的所有数字都被提取出来而没有任何不匹配，则该数字是自同构的。
3.  如果找到一个自同构数，那么增加 current_max，并与 max_so_far 进行比较
4.  如果当前最大值大于当前最大值，则将当前最大值赋给当前最大值
5.  每次发现非自同构元素时，将 current_max 复位为 0。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to check Automorphic number
bool isAutomorphic(int N)
{
    // Store the square
    int sq = N * N;

    // Start Comparing digits
    while (N > 0) {

        // Return false, if any digit of N doesn't
        // match with its square's digits from last
        if (N % 10 != sq % 10)
            return false;

        // Reduce N and square
        N /= 10;
        sq /= 10;
    }

    return true;
}

// Function to find the length of the maximum
// contiguous subarray of automorphic numbers
int maxAutomorphicSubarray(int arr[], int n)
{
    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++) {

        // check if element is non automorphic
        if (isAutomorphic(arr[i]) == false)
            current_max = 0;

        // If element is automorphic, than update
        // current_max and max_so_far accordingly.
        else {
            current_max++;
            max_so_far = max(current_max, max_so_far);
        }
    }

    return max_so_far;
}

// Driver Code
int main()
{
    int arr[] = { 0, 3, 2, 5, 1, 9 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxAutomorphicSubarray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to check Automorphic number
static boolean isAutomorphic(int N)
{
    // Store the square
    int sq = N * N;

    // Start Comparing digits
    while (N > 0)
    {

        // Return false, if any digit of N doesn't
        // match with its square's digits from last
        if (N % 10 != sq % 10)
            return false;

        // Reduce N and square
        N /= 10;
        sq /= 10;
    }

    return true;
}

// Function to find the length of the maximum
// contiguous subarray of automorphic numbers
static int maxAutomorphicSubarray(int []arr, int n)
{
    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++)
    {

        // check if element is non automorphic
        if (isAutomorphic(arr[i]) == false)
            current_max = 0;

        // If element is automorphic, than update
        // current_max and max_so_far accordingly.
        else
        {
            current_max++;
            max_so_far = Math.max(current_max,
                                  max_so_far);
        }
    }

    return max_so_far;
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 0, 3, 2, 5, 1, 9 };
    int n = arr.length;

    System.out.println(maxAutomorphicSubarray(arr, n));
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to check Automorphic number
def isAutomorphic(N) :

    # Store the square
    sq = N * N;

    # Start Comparing digits
    while (N > 0) :

        # Return false, if any digit of N doesn't
        # match with its square's digits from last
        if (N % 10 != sq % 10) :
            return False;

        # Reduce N and square
        N //= 10;
        sq //= 10;

    return True;

# Function to find the length of the maximum
# contiguous subarray of automorphic numbers
def maxAutomorphicSubarray(arr, n) :

    current_max = 0; max_so_far = 0;

    for i in range(n) :

        # check if element is non automorphic
        if (isAutomorphic(arr[i]) == False) :
            current_max = 0;

        # If element is automorphic, than update
        # current_max and max_so_far accordingly.
        else :
            current_max += 1;
            max_so_far = max(current_max,
                             max_so_far);

    return max_so_far;

# Driver Code
if __name__ == "__main__" :

    arr = [ 0, 3, 2, 5, 1, 9 ];
    n = len(arr) ;

    print(maxAutomorphicSubarray(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to check Automorphic number
static bool isAutomorphic(int N)
{
    // Store the square
    int sq = N * N;

    // Start Comparing digits
    while (N > 0)
    {

        // Return false, if any digit of N doesn't
        // match with its square's digits from last
        if (N % 10 != sq % 10)
            return false;

        // Reduce N and square
        N /= 10;
        sq /= 10;
    }

    return true;
}

// Function to find the length of the maximum
// contiguous subarray of automorphic numbers
static int maxAutomorphicSubarray(int []arr, int n)
{
    int current_max = 0, max_so_far = 0;

    for (int i = 0; i < n; i++)
    {

        // check if element is non automorphic
        if (isAutomorphic(arr[i]) == false)
            current_max = 0;

        // If element is automorphic, than update
        // current_max and max_so_far accordingly.
        else
        {
            current_max++;
            max_so_far = Math.Max(current_max, max_so_far);
        }
    }

    return max_so_far;
}

// Driver Code
static void Main()
{
    int []arr = { 0, 3, 2, 5, 1, 9 };
    int n = arr.Length;

    Console.WriteLine(maxAutomorphicSubarray(arr, n));

}
}

// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to check Automorphic number
function isAutomorphic($N)
{
    // Store the square
    $sq = $N * $N;

    // Start Comparing digits
    while ($N > 0)
    {

        // Return false, if any digit of N doesn't
        // match with its square's digits from last
        if ($N % 10 != $sq % 10)
            return false;

        // Reduce N and square
        $N = (int)($N / 10);
        $sq = (int)($sq / 10);
    }

    return true;
}

// Function to find the length of the maximum
// contiguous subarray of automorphic numbers
function maxAutomorphicSubarray($arr, $n)
{
    $current_max = 0; $max_so_far = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // check if element is non automorphic
        if (isAutomorphic($arr[$i]) == false)
            $current_max = 0;

        // If element is automorphic, than update
        // current_max and max_so_far accordingly.
        else
        {
            $current_max++;
            $max_so_far = max($current_max,
                              $max_so_far);
        }
    }

    return $max_so_far;
}

// Driver Code
$arr = array(0, 3, 2, 5, 1, 9 );
$n = sizeof($arr);

echo(maxAutomorphicSubarray($arr, $n));

// This code is contributed by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to check Automorphic number
function isAutomorphic(N)
{

    // Store the square
    var sq = N * N;

    // Start Comparing digits
    while (N > 0)
    {

        // Return false, if any digit of N doesn't
        // match with its square's digits from last
        if (N % 10 != sq % 10)
            return false;

        // Reduce N and square
        N = parseInt(N / 10);
        sq = parseInt(sq / 10);
    }
    return true;
}

// Function to find the length of the maximum
// contiguous subarray of automorphic numbers
function maxAutomorphicSubarray(arr, n)
{
    var current_max = 0, max_so_far = 0;

    for(var i = 0; i < n; i++)
    {

        // Check if element is non automorphic
        if (isAutomorphic(arr[i]) == false)
            current_max = 0;

        // If element is automorphic, than update
        // current_max and max_so_far accordingly.
        else
        {
            current_max++;
            max_so_far = Math.max(current_max,
                                  max_so_far);
        }
    }
    return max_so_far;
}

// Driver Code
var arr = [ 0, 3, 2, 5, 1, 9 ];
var n = arr.length;

document.write(maxAutomorphicSubarray(arr, n));

// This code is contributed by rrrtnx

</script>
```

**Output:** 

```
2
```