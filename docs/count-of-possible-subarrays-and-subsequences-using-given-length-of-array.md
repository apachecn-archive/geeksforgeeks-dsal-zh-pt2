# 使用给定长度的数组对可能的子数组和子序列进行计数

> 原文:[https://www . geeksforgeeks . org/使用给定数组长度的可能子数组和子序列的计数/](https://www.geeksforgeeks.org/count-of-possible-subarrays-and-subsequences-using-given-length-of-array/)

给定一个整数 **N** ，它表示一个数组的长度，任务是计算给定数组长度下可能的子数组和子序列的数量。
**例:**

> **输入:** N = 5
> **输出:**
> 子阵列计数= 15
> 子序列计数= 32
> **输入:** N = 3
> **输出:**
> 子阵列计数= 6
> 子序列计数= 8

**方法:**子阵列计数的关键观察事实是阵列的每个索引元素可能的末端位置的数量可以是(N–I)，因此大小为 **N** 的阵列的子阵列计数可以是:

```
Count of Sub-arrays = (N) * (N + 1)
                     ---------------
                            2
```

可能的子序列计数的关键观察事实是数组的每个元素可以包含在子序列中，也可以不包含在子序列中。因此，每个元素的选择是 2。

```
Count of subsequences = 2N
```

以下是上述方法的实现:

## C++

```
// C++ implementation to count
// the subarray and subsequence of
// given length of the array
#include <bits/stdc++.h>
using namespace std;

// Function to count the subarray
// for the given array
int countSubarray(int n){
    return ((n)*(n + 1))/2;
}

// Function to count the subsequence
// for the given array length
int countSubsequence(int n){
    return pow(2, n);
}

// Driver Code
int main()
{
    int n = 5;
    cout << (countSubarray(n)) << endl;
    cout << (countSubsequence(n)) << endl;
    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count
// the subarray and subsequence of
// given length of the array
class GFG{

// Function to count the subarray
// for the given array
static int countSubarray(int n){
    return ((n)*(n + 1))/2;
}

// Function to count the subsequence
// for the given array length
static int countSubsequence(int n){
    return (int) Math.pow(2, n);
}

// Driver Code
public static void main(String[] args)
{
    int n = 5;
    System.out.print((countSubarray(n)) +"\n");
    System.out.print((countSubsequence(n)) +"\n");
}
}

// This code is contributed by Princi Singh
```

## 计算机编程语言

```
# Python implementation to count
# the subarray and subsequence of
# given length of the array

# Function to count the subarray
# for the given array
def countSubarray(n):
    return ((n)*(n + 1))//2

# Function to count the subsequence
# for the given array length
def countSubsequence(n):
    return (2**n)

# Driver Code   
if __name__ == "__main__":
    n = 5
    print(countSubarray(n))
    print(countSubsequence(n))
```

## C#

```
// C# implementation to count
// the subarray and subsequence of
// given length of the array
using System;

class GFG{

// Function to count the subarray
// for the given array
static int countSubarray(int n){
    return ((n)*(n + 1))/2;
}

// Function to count the subsequence
// for the given array length
static int countSubsequence(int n){
    return (int) Math.Pow(2, n);
}

// Driver Code
public static void Main(String[] args)
{
    int n = 5;
    Console.Write((countSubarray(n)) +"\n");
    Console.Write((countSubsequence(n)) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation to count
// the subarray and subsequence of
// given length of the array

// Function to count the subarray
// for the given array
function countSubarray(n){
    return ((n)*(n + 1))/2;
}

// Function to count the subsequence
// for the given array length
function countSubsequence(n){
    return  Math.pow(2, n);
}

// Driver Code

    let n = 5;
    document.write((countSubarray(n)) +"<br/>");
   document.write((countSubsequence(n)) +"\n");

</script>
```

**Output:** 

```
15
32
```

时间复杂度:0(对数 n)

辅助空间:0(1)