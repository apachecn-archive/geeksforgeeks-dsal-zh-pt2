# 用给定的和计数配对|设置 2

> 原文:[https://www . geesforgeks . org/count-pairs-with-given-sum-set-2/](https://www.geeksforgeeks.org/count-pairs-with-given-sum-set-2/)

给定一个数组 **arr[]** 和一个整数**和**，任务是找出数组中和等于**和**的整数对的个数。
**举例:**

> **输入:** arr[] = {1，5，7，-1}，和= 6
> **输出:** 2
> 和 6 的对是(1，5)和(7，-1)
> **输入:** arr[] = {1，5，7，-1，5}，和= 6
> **输出:** 3
> 和 6 的对是(1，5)，(7，-1) & (1，5)

**方法:**两种不同的方法已经讨论过了[这里](https://www.geeksforgeeks.org/count-pairs-with-given-sum/)。这里将讨论一种基于[排序](https://www.geeksforgeeks.org/sorting-algorithms/)的方法。

1.  对数组进行排序，取两个指针 **i** 和 **j** ，一个指针指向数组的开头即 **i = 0** ，另一个指针指向数组的结尾即**j = n–1**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of pairs
// from arr[] with the given sum
int pairs_count(int arr[], int n, int sum)
{
    // To store the count of pairs
    int ans = 0;

    // Sort the given array
    sort(arr, arr + n);

    // Take two pointers
    int i = 0, j = n - 1;

    while (i < j) {
        // If sum is greater
        if (arr[i] + arr[j] < sum)
            i++;

        // If sum is lesser
        else if (arr[i] + arr[j] > sum)
            j--;

        // If sum is equal
        else {
            // Find the frequency of arr[i]
            int x = arr[i], xx = i;
            while (i < j and arr[i] == x)
                i++;

            // Find the frequency of arr[j]
            int y = arr[j], yy = j;
            while (j >= i and arr[j] == y)
                j--;

            // If arr[i] and arr[j] are same
            // then remove the extra number counted
            if (x == y) {
                int temp = i - xx + yy - j - 1;
                ans += (temp * (temp + 1)) / 2;
            }
            else
                ans += (i - xx) * (yy - j);
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 5, 7, 5, -1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int sum = 6;

    cout << pairs_count(arr, n, sum);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach
import java.util.Arrays;
import java.io.*;

class GFG
{

// Function to return the count of pairs
// from arr[] with the given sum
static int pairs_count(int arr[], int n, int sum)
{
    // To store the count of pairs
    int ans = 0;

    // Sort the given array
    Arrays.sort(arr);

    // Take two pointers
    int i = 0, j = n - 1;

    while (i < j)
    {

        // If sum is greater
        if (arr[i] + arr[j] < sum)
            i++;

        // If sum is lesser
        else if (arr[i] + arr[j] > sum)
            j--;

        // If sum is equal
        else
        {

            // Find the frequency of arr[i]
            int x = arr[i], xx = i;
            while ((i < j ) && (arr[i] == x))
                i++;

            // Find the frequency of arr[j]
            int y = arr[j], yy = j;
            while ((j >= i )&& (arr[j] == y))
                j--;

            // If arr[i] and arr[j] are same
            // then remove the extra number counted
            if (x == y)
            {
                int temp = i - xx + yy - j - 1;
                ans += (temp * (temp + 1)) / 2;
            }
            else
                ans += (i - xx) * (yy - j);
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 5, 7, 5, -1 };
    int n = arr.length;
    int sum = 6;

    System.out.println (pairs_count(arr, n, sum));
}
}

// The code is contributed by ajit..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of pairs
# from arr with the given sum
def pairs_count(arr, n, sum):

    # To store the count of pairs
    ans = 0

    # Sort the given array
    arr = sorted(arr)

    # Take two pointers
    i, j = 0, n - 1

    while (i < j):

        # If sum is greater
        if (arr[i] + arr[j] < sum):
            i += 1

        # If sum is lesser
        elif (arr[i] + arr[j] > sum):
            j -= 1

        # If sum is equal
        else:

            # Find the frequency of arr[i]
            x = arr[i]
            xx = i
            while (i < j and arr[i] == x):
                i += 1

            # Find the frequency of arr[j]
            y = arr[j]
            yy = j
            while (j >= i and arr[j] == y):
                j -= 1

            # If arr[i] and arr[j] are same
            # then remove the extra number counted
            if (x == y):
                temp = i - xx + yy - j - 1
                ans += (temp * (temp + 1)) // 2
            else:
                ans += (i - xx) * (yy - j)

    # Return the required answer
    return ans

# Driver code
arr = [1, 5, 7, 5, -1]
n = len(arr)
sum = 6

print(pairs_count(arr, n, sum))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count of pairs
// from arr[] with the given sum
static int pairs_count(int []arr,
                       int n, int sum)
{
    // To store the count of pairs
    int ans = 0;

    // Sort the given array
    Array.Sort(arr);

    // Take two pointers
    int i = 0, j = n - 1;

    while (i < j)
    {

        // If sum is greater
        if (arr[i] + arr[j] < sum)
            i++;

        // If sum is lesser
        else if (arr[i] + arr[j] > sum)
            j--;

        // If sum is equal
        else
        {

            // Find the frequency of arr[i]
            int x = arr[i], xx = i;
            while ((i < j) && (arr[i] == x))
                i++;

            // Find the frequency of arr[j]
            int y = arr[j], yy = j;
            while ((j >= i) && (arr[j] == y))
                j--;

            // If arr[i] and arr[j] are same
            // then remove the extra number counted
            if (x == y)
            {
                int temp = i - xx + yy - j - 1;
                ans += (temp * (temp + 1)) / 2;
            }
            else
                ans += (i - xx) * (yy - j);
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
public static void Main (String[] args)
{
    int []arr = { 1, 5, 7, 5, -1 };
    int n = arr.Length;
    int sum = 6;

    Console.WriteLine (pairs_count(arr, n, sum));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of pairs
// from arr[] with the given sum
function pairs_count(arr, n, sum)
{
    // To store the count of pairs
    let ans = 0;

    // Sort the given array
    arr.sort();

    // Take two pointers
    let i = 0, j = n - 1;

    while (i < j) {
        // If sum is greater
        if (arr[i] + arr[j] < sum)
            i++;

        // If sum is lesser
        else if (arr[i] + arr[j] > sum)
            j--;

        // If sum is equal
        else {
            // Find the frequency of arr[i]
            let x = arr[i], xx = i;
            while (i < j && arr[i] == x)
                i++;

            // Find the frequency of arr[j]
            let y = arr[j], yy = j;
            while (j >= i && arr[j] == y)
                j--;

            // If arr[i] and arr[j] are same
            // then remove the extra number counted
            if (x == y) {
                let temp = i - xx + yy - j - 1;
                ans += (temp * (temp + 1)) / 2;
            }
            else
                ans += (i - xx) * (yy - j);
        }
    }

    // Return the required answer
    return ans;
}

// Driver code
    let arr = [ 1, 5, 7, 5, -1 ];
    let n = arr.length;
    let sum = 6;

    document.write(pairs_count(arr, n, sum));

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
3
```