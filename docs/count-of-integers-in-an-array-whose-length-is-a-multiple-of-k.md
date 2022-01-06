# 长度为 K 倍数的数组中整数的计数

> 原文:[https://www . geesforgeks . org/长度为 k 的倍数的数组中整数的计数/](https://www.geeksforgeeks.org/count-of-integers-in-an-array-whose-length-is-a-multiple-of-k/)

给定一个由 **N** 个元素组成的数组**和一个整数 **K** ，任务是计算所有长度为 **K** 倍数的元素。
**举例:**** 

```
Input: arr[]={1, 12, 3444, 544, 9}, K = 2
Output: 2
Explanation:
There are 2 numbers whose digit count is multiple of 2 {12, 3444}.

Input: arr[]={12, 345, 2, 68, 7896}, K = 3
Output: 1
Explanation:
There is 1 number whose digit count is multiple of 3 {345}.
```

**进场:**

1.  逐一遍历数组中的数字
2.  计算数组中每个数字的位数
3.  检查其位数是否为 K 的倍数。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find
// digit count of numbers
int digit_count(int x)
{
    int sum = 0;
    while (x) {
        sum++;
        x = x / 10;
    }
    return sum;
}

// Function to find the count of numbers
int find_count(vector<int> arr, int k)
{

    int ans = 0;
    for (int i : arr) {

        // Get the digit count of each element
        int x = digit_count(i);

        // Check if the digit count
        // is divisible by K
        if (x % k == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}

// Driver code
int main()
{
    vector<int> arr
        = { 12, 345, 2, 68, 7896 };
    int K = 2;

    cout << find_count(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG{

// Function to find
// digit count of numbers
static int digit_count(int x)
{
    int sum = 0;
    while (x > 0) {
        sum++;
        x = x / 10;
    }
    return sum;
}

// Function to find the count of numbers
static int find_count(int []arr, int k)
{

    int ans = 0;
    for (int i : arr) {

        // Get the digit count of each element
        int x = digit_count(i);

        // Check if the digit count
        // is divisible by K
        if (x % k == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 12, 345, 2, 68, 7896 };
    int K = 2;

    System.out.print(find_count(arr, K));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to find
# digit count of numbers
def digit_count(x):
    sum = 0
    while (x):
        sum += 1
        x = x // 10
    return sum

# Function to find the count of numbers
def find_count(arr,k):
    ans = 0
    for i in arr:
        # Get the digit count of each element
        x = digit_count(i)

        # Check if the digit count
        # is divisible by K
        if (x % k == 0):
            # Increment the count
            # of required numbers by 1
            ans += 1

    return ans

# Driver code
if __name__ == '__main__':
    arr  =  [12, 345, 2, 68, 7896]
    K = 2

    print(find_count(arr, K))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of above approach

using System;

public class GFG{

// Function to find
// digit count of numbers
static int digit_count(int x)
{
    int sum = 0;
    while (x > 0) {
        sum++;
        x = x / 10;
    }
    return sum;
}

// Function to find the count of numbers
static int find_count(int []arr, int k)
{

    int ans = 0;
    foreach (int i in arr) {

        // Get the digit count of each element
        int x = digit_count(i);

        // Check if the digit count
        // is divisible by K
        if (x % k == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 12, 345, 2, 68, 7896 };
    int K = 2;

    Console.Write(find_count(arr, K));

}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of above approach

// Function to find
// digit count of numbers
function digit_count(x)
{
    let sum = 0;
    while (x) {
        sum++;
        x = x / 10;
    }
    return sum;
}

// Function to find the count of numbers
function find_count(arr, k)
{

    let ans = 0;
    for (let i of arr) {

        // Get the digit count of each element
        let x = digit_count(i);

        // Check if the digit count
        // is divisible by K
        if (x % k == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}

// Driver code

let arr = [ 12, 345, 2, 68, 7896 ];
let K = 2;

document.write(find_count(arr, K));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
3
```

***时间复杂度:-** O(N*M)* ，其中 N 为数组的大小，M 为数组中最大数的位数。
***空间复杂度:-** O(1)*