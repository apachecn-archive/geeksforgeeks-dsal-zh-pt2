# 在不影响初始数组平均值的情况下可以删除的元素数

> 原文:[https://www . geeksforgeeks . org/可删除但不干扰初始数组平均值的元素计数/](https://www.geeksforgeeks.org/count-of-elements-that-can-be-deleted-without-disturbing-the-mean-of-the-initial-array/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出数组中元素的个数，这样在从数组中单独删除它们(只能删除一个元素)后，就不会干扰数组的初始平均值。
**例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 1
> 3 是唯一不影响数组均值的元素移除。
> 即(1 + 2 + 4 + 5) / 4 = 12 / 4 = 3
> 即原始数组的平均值。
> **输入:** arr[] = {5，4，3，6}
> **输出:** 0

**进场:**

*   求数组元素的初始均值和和，分别存储在变量**均值**和**和**中。
*   现在，初始化**计数= 0** 并且对于每个元素 **arr[i]** 如果**(sum–arr[I])/(N–1)=意味着**则增加计数。
*   最后打印计数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the elements
// which do not change the mean on removal
int countElements(int arr[], int n)
{

    // To store the sum of the array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // To store the initial mean
    float mean = (float)sum / n;

    // to store the count of required elements
    int cnt = 0;
    // Iterate over the array
    for (int i = 0; i < n; i++) {

        // Finding the new mean
        float newMean = (float)(sum - arr[i]) / (n - 1);

        // If the new mean equals to the initial mean
        if (newMean == mean)
            cnt++;
    }

    return cnt;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the elements
// which do not change the mean on removal
static int countElements(int arr[], int n)
{

    // To store the sum of the array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // To store the initial mean
    float mean = (float)sum / n;

    // to store the count of required elements
    int cnt = 0;

    // Iterate over the array
    for (int i = 0; i < n; i++)
    {

        // Finding the new mean
        float newMean = (float)(sum - arr[i]) /
                                      (n - 1);

        // If the new mean equals to
        // the initial mean
        if (newMean == mean)
            cnt++;
    }
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;
    System.out.println(countElements(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the elements
# which do not change the mean on removal
def countElements(arr, n):

    # To store the Sum of the array elements
    Sum = 0
    for i in range(n):
        Sum += arr[i]

    # To store the initial mean
    mean = Sum / n

    # to store the count of required elements
    cnt = 0

    # Iterate over the array
    for i in range(n):

        # Finding the new mean
        newMean = (Sum - arr[i]) / (n - 1)

        # If the new mean equals to
        # the initial mean
        if (newMean == mean):
            cnt += 1

    return cnt

# Driver code
arr = [1, 2, 3, 4, 5]
n = len(arr)

print(countElements(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to find the elements
// which do not change the mean on removal
static int countElements(int []arr, int n)
{

    // To store the sum of the array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += arr[i];

    // To store the initial mean
    float mean = (float)sum / n;

    // to store the count of required elements
    int cnt = 0;

    // Iterate over the array
    for (int i = 0; i < n; i++)
    {

        // Finding the new mean
        float newMean = (float)(sum - arr[i]) /
                                      (n - 1);

        // If the new mean equals to
        // the initial mean
        if (newMean == mean)
            cnt++;
    }
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;
    Console.WriteLine(countElements(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the elements
// which do not change the mean on removal
function countElements(arr, n)
{

    // To store the sum of the array elements
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += arr[i];

    // To store the initial mean
    let mean = sum / n;

    // to store the count of required elements
    let cnt = 0;
    // Iterate over the array
    for (let i = 0; i < n; i++) {

        // Finding the new mean
        let newMean = (sum - arr[i]) / (n - 1);

        // If the new mean equals to the initial mean
        if (newMean == mean)
            cnt++;
    }

    return cnt;
}

// Driver code
    let arr = [ 1, 2, 3, 4, 5 ];
    let n = arr.length;

    document.write(countElements(arr, n));

</script>
```

**Output:** 

```
1
```

**时间复杂度:** O(N)