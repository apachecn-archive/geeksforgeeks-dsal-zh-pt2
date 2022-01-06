# 大小为 K 的最大圆子阵和

> 原文:[https://www . geesforgeks . org/maximum-circular-subarray-sum-size-k/](https://www.geeksforgeeks.org/maximum-circular-subarray-sum-of-size-k/)

给定一个大小为 **N** 的数组 **arr** 和一个整数 **K** ，任务是在所有相邻子数组(也考虑圆形子数组)中找到大小为 **k** 的最大和子数组。

**示例:**

> **输入:** arr = {18，4，3，4，5，6，7，8，2，10}，k = 3
> **输出:**
> 最大圆和= 32
> 起始指数= 9
> 结束指数= 1
> **说明:**
> 最大圆和= 10 + 18 + 4 = 32
> 
> **输入:** arr = {8，2，5，9}，k = 4
> **输出:**
> 最大循环和= 24
> 开始指数= 0
> 结束指数= 3

**进场:**

*   重复循环直到(n + k)次，然后
*   取(i % n)来处理数组索引大于 n 的情况。

下面是上述方法的实现:

## C++

```
// C++ program to find maximum circular
// subarray sum of size k

#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// maximum sum
void maxCircularSum(int arr[], int n, int k)
{
    // k must be greater
    if (n < k) {
        cout << "Invalid";
        return;
    }

    int sum = 0, start = 0, end = k - 1;

    // calculate the sum of first k elements.
    for (int i = 0; i < k; i++) {
        sum += arr[i];
    }

    int ans = sum;

    for (int i = k; i < n + k; i++) {

        // add current element to sum
        // and subtract the first element
        // of the previous window.
        sum += arr[i % n] - arr[(i - k) % n];

        if (sum > ans) {
            ans = sum;
            start = (i - k + 1) % n;
            end = i % n;
        }
    }

    cout << "max circular sum = "
         << ans << endl;
    cout << "start index = " << start
         << "\nend index = " << end << endl;
}

// Driver Code
int main()
{
    int arr[] = { 18, 4, 3, 4, 5, 6, 7, 8, 2, 10 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    maxCircularSum(arr, n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum circular
// subarray sum of size k

import java.util.*;

class GFG
{

    // Function to calculate
    // maximum sum
    static void maxCircularSum(int[] arr, int n, int k)
    {

        // k must be greater
        if (n < k)
        {
            System.out.println("Invalid");
            return;
        }

        int sum = 0, start = 0, end = k - 1;

        // calculate the sum of first k elements.
        for (int i = 0; i < k; i++)
            sum += arr[i];

        int ans = sum;

        for (int i = k; i < n + k; i++)
        {

            // add current element to sum
            // and subtract the first element
            // of the previous window.
            sum += arr[i % n] - arr[(i - k) % n];

            if (sum > ans)
            {
                ans = sum;
                start = (i - k + 1) % n;
                end = i % n;
            }
        }

        System.out.println("max circular sum = " + ans);
        System.out.println("start index = " + start + "\nend index = " + end);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 18, 4, 3, 4, 5, 6, 7, 8, 2, 10 };
        int n = arr.length;
        int k = 3;

        maxCircularSum(arr, n, k);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find maximum circular
# subarray sum of size k

# Function to calculate
# maximum sum
def maxCircularSum(arr, n, k) :

    # k must be greater
    if (n < k) :
        print("Invalid");
        return;

    sum = 0; start = 0; end = k - 1;

    # calculate the sum of first k elements.
    for i in range(k) :
        sum += arr[i];

    ans = sum;

    for i in range(k, n + k) :

        # add current element to sum
        # and subtract the first element
        # of the previous window.
        sum += arr[i % n] - arr[(i - k) % n];

        if (sum > ans) :
            ans = sum;
            start = (i - k + 1) % n;
            end = i % n;

    print("max circular sum = ",ans);
    print("start index = ", start,
          "\nend index = ", end);

# Driver Code
if __name__ == "__main__" :

    arr = [ 18, 4, 3, 4, 5, 6, 7, 8, 2, 10 ];
    n = len(arr);
    k = 3;

    maxCircularSum(arr, n, k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find maximum circular
// subarray sum of size k
using System;

class GFG
{

    // Function to calculate
    // maximum sum
    static void maxCircularSum(int[] arr,
                               int n, int k)
    {

        // k must be greater
        if (n < k)
        {
            Console.WriteLine("Invalid");
            return;
        }

        int sum = 0, start = 0, end = k - 1;

        // calculate the sum of first k elements.
        for (int i = 0; i < k; i++)
            sum += arr[i];

        int ans = sum;

        for (int i = k; i < n + k; i++)
        {

            // add current element to sum
            // and subtract the first element
            // of the previous window.
            sum += arr[i % n] - arr[(i - k) % n];

            if (sum > ans)
            {
                ans = sum;
                start = (i - k + 1) % n;
                end = i % n;
            }
        }

        Console.WriteLine("max circular sum = " + ans);
        Console.WriteLine("start index = " + start +
                          "\nend index = " + end);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 18, 4, 3, 4, 5,
                      6, 7, 8, 2, 10 };
        int n = arr.Length;
        int k = 3;

        maxCircularSum(arr, n, k);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find maximum circular
// subarray sum of size k

// Function to calculate
// maximum sum
function maxCircularSum(arr, n, k)
{

    // k must be greater
    if (n < k)
    {
        document.write("Invalid");
        return;
    }

    let sum = 0, start = 0, end = k - 1;

    // Calculate the sum of first k elements.
    for(let i = 0; i < k; i++)
    {
        sum += arr[i];
    }

    let ans = sum;

    for(let i = k; i < n + k; i++)
    {

        // Add current element to sum
        // and subtract the first element
        // of the previous window.
        sum += arr[i % n] - arr[(i - k) % n];

        if (sum > ans)
        {
            ans = sum;
            start = (i - k + 1) % n;
            end = i % n;
        }
    }

    document.write("max circular sum = " +
                   ans + "<br>");
    document.write("start index = " + start +
                   "<br>end index = " + end +
                   "<br>");
}

// Driver Code
let arr = [ 18, 4, 3, 4, 5,
            6, 7, 8, 2, 10 ];
let n = arr.length
let k = 3;

maxCircularSum(arr, n, k);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
max circular sum = 32
start index = 9
end index = 1
```

**时间复杂度:** ![O(N)  ](img/49a9eabbb27564e25ba8e2b64e1e7e4b.png "Rendered by QuickLaTeX.com")