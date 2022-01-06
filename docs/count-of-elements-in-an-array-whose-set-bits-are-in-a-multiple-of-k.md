# 数组中设置位为 K 倍数的元素的计数

> 原文:[https://www . geeksforgeeks . org/数组中元素的计数-其位集是 k 的倍数/](https://www.geeksforgeeks.org/count-of-elements-in-an-array-whose-set-bits-are-in-a-multiple-of-k/)

给定一个由 **N** 元素和一个整数 **K** 组成的数组 **arr[]** ，任务是对所有其[设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)的数量是 **K** 的倍数的元素进行计数。
**举例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 2
> **输出:** 2
> **说明:**
> 设置位数为 2 的倍数的两个数为{3，5}。
> **输入:** arr[] = {10，20，30，40}，K = 4
> **输出:** 1
> **说明:**
> 有个集合位数是 4 的倍数的数是{30}。

**进场:**

1.  逐一遍历数组中的数字。
2.  [统计数组中每个数字的设定位](https://www.geeksforgeeks.org/program-to-count-number-of-set-bits-in-an-big-array/)。
3.  检查设置位计数是否是 K 的倍数。

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the count of numbers
int find_count(vector<int> arr, int k)
{

    int ans = 0;
    for (int i : arr) {

        // Get the set-bits count of each element
        int x = __builtin_popcount(i);

        // Check if the setbits count
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
    vector<int> arr = { 12, 345, 2, 68, 7896 };
    int K = 2;

    cout << find_count(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach

class GFG{

// Function to find the count of numbers
static int find_count(int []arr, int k)
{

    int ans = 0;
    for (int i : arr) {

        // Get the set-bits count of each element
        int x = Integer.bitCount(i);

        // Check if the setbits count
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

# Function to count total set bits
def bitsoncount(x):
    return bin(x).count('1')

# Function to find the count of numbers
def find_count(arr, k) :

    ans = 0
    for i in arr:

        # Get the set-bits count of each element
        x = bitsoncount(i)

        # Check if the setbits count
        # is divisible by K
        if (x % k == 0) :
            # Increment the count
            # of required numbers by 1
            ans += 1
    return ans

# Driver code
arr = [ 12, 345, 2, 68, 7896 ]
K = 2
print(find_count(arr, K))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation of above approach
using System;

class GFG{

// Function to find the count of numbers
static int find_count(int []arr, int k)
{
    int ans = 0;
    foreach(int i in arr)
    {

        // Get the set-bits count of each element
        int x = countSetBits(i);

        // Check if the setbits count
        // is divisible by K
        if (x % k == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}

static int countSetBits(long x)
{
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }

    return setBits;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 12, 345, 2, 68, 7896 };
    int K = 2;

    Console.Write(find_count(arr, K));
}
}
// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript implementation of above approach

// Function to find the count of numbers
function find_count(arr, k)
{
    var ans = 0;
    for(var i = 0; i <= arr.length; i++)
    {

        // Get the set-bits count of each element
        var x = countSetBits(i);

        // Check if the setbits count
        // is divisible by K
        if (x % k == 0)

            // Increment the count
            // of required numbers by 1
            ans += 1;
    }

    return ans;
}

function countSetBits(x)
{
    var setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }

    return setBits;
}

    var arr = [ 12, 345, 2, 68, 7896 ];
    var K = 2;

    document.write(find_count(arr, K));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
3
```

**时间复杂度:O(N * M)** ，其中 N 为数组的大小，M 为数组中最大数的位数。
**辅助空间复杂度:O(1)**