# 排序数组中缺失数字的计数

> 原文:[https://www . geesforgeks . org/排序数组中缺少数字的计数/](https://www.geeksforgeeks.org/count-of-missing-numbers-in-a-sorted-array/)

给定一个排序数组 **arr[]，**，任务是计算排序数组的第一个和最后一个元素之间的[缺失数。](https://www.geeksforgeeks.org/find-the-missing-number-in-a-sorted-array/)

**示例:**

> **输入:** arr[] = { 1，4，5，8 }
> **输出:** 4
> **解释:**
> 数组中缺少的整数为{2，3，6，7}。
> 因此，计数为 4。
> 
> **输入:** arr[] = {5，10，20，40 }
> T3】输出: 32

**天真法:**
解决问题最简单的方法是迭代数组，计算数组元素所有相邻差的[和](https://www.geeksforgeeks.org/sum-absolute-differences-pairs-given-array/)。

***时间复杂度:** O(N)
**辅助空间:** O(1)*

**高效法:**
对上述方法进行优化，思路是观察**【arr[0]、arr[N–1]】**范围内的总数由**arr[N-1]–arr[0]+1**给出。由于数组的大小为 **N** ，数组中缺失整数的计数由**arr[N-1]–arr[0]+1–N**给出。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function that find the count of 
// missing numbers in array a[] 
void countMissingNum(int a[], int N) 
{ 
    // Calculate the count of missing 
    // numbers in the array 
    int count = a[N - 1] - a[0] + 1 - N; 

    cout << count << endl; 
} 

// Driver Code 
int main() 
{ 
    int arr[] = { 5, 10, 20, 40 }; 

    int N = sizeof(arr) / sizeof(arr[0]); 

    countMissingNum(arr, N); 

    return 0; 
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach 
class GFG{ 

// Function that find the count of 
// missing numbers in array a[] 
public static void countMissingNum(int[] a, 
                                int N) 
{ 

    // Calculate the count of missing 
    // numbers in the array 
    int count = a[N - 1] - a[0] + 1 - N; 

    System.out.println(count); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    int arr[] = { 5, 10, 20, 40 }; 

    int N = arr.length; 

    countMissingNum(arr, N); 
} 
} 

// This code is contributed by divyeshrabadiya07 
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that find the count of 
# missing numbers in array a[] 
def countMissingNum(a, N): 

    # Calculate the count of missing 
    # numbers in the array 
    count = a[N - 1] - a[0] + 1 - N 

    print(count) 

# Driver Code 
arr = [ 5, 10, 20, 40 ] 

N = len(arr) 

countMissingNum(arr, N) 

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach 
using System;

class GFG{

// Function that find the count of 
// missing numbers in array a[] 
public static void countMissingNum(int[] a,
                                   int N) 
{ 

    // Calculate the count of missing 
    // numbers in the array 
    int count = a[N - 1] - a[0] + 1 - N; 

    Console.Write(count); 
} 

// Driver code
public static void Main(string[] args)
{
    int []arr = { 5, 10, 20, 40 }; 
    int N = arr.Length; 

    countMissingNum(arr, N); 
}
}

// This code is contributed by rutvik_56
```

**Output:**

```
32

```

***时间复杂度:**O(1)
T4】辅助空间: O(1)*