# 可被 2 整除的最大可能元素

> 原文:[https://www . geesforgeks . org/最大可能元素可被 2 整除/](https://www.geeksforgeeks.org/maximum-possible-elements-which-are-divisible-by-2/)

给定大小为 **N** 的整数数组 **arr** 。任务是在修改数组后找到数组中可被 2 整除的最大可能元素。可以任意多次(可能是零次)执行下面的操作。

> 用数组中任意两个元素的和替换它们。

**例:**

> **输入:** arr = [1，2，3，1，3]
> **输出:** 3
> 在索引 0 和 2 以及索引 3 和 4 处添加元素后，数组变成 arr=[4，2，4]。
> **输入:** arr = [1，2，3，4，5]
> **输出:** 3
> 加 1 和 3 后，数组变成 arr=[4，2，4，5]。

**逼近** :
首先，观察到我们不需要修改可被 2 整除的元素(即偶数)。然后我们带着奇数离开了。两个数相加将得到一个可被 2 整除的偶数。
所以最后的结果会是:

> **计数 _ 偶数** + **计数 _ 奇数** /2。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find maximum possible
// elements which divisible by 2
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum possible
// elements which divisible by 2
int Divisible(int arr[], int n)
{
    // To store count of even numbers
    int count_even = 0;

    for (int i = 0; i < n; i++)
        if (arr[i] % 2 == 0)
            count_even++;

    // All even numbers and half of odd numbers
    return count_even + (n - count_even) / 2;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << Divisible(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum possible
// elements which divisible by 2
class GFG
{

    // Function to find maximum possible
    // elements which divisible by 2
    static int Divisible(int arr[], int n)
    {
        // To store count of even numbers
        int count_even = 0;

        for (int i = 0; i < n; i++)
            if (arr[i] % 2 == 0)
                count_even++;

        // All even numbers and half of odd numbers
        return count_even + (n - count_even) / 2;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };

        int n = arr.length;

        // Function call
        System.out.println(Divisible(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find maximum possible
# elements which divisible by 2

# Function to find maximum possible
# elements which divisible by 2
def Divisible(arr, n):
    # To store count of even numbers
    count_even = 0

    for i in range(n):
        if (arr[i] % 2 == 0):
            count_even+=1

    # All even numbers and half of odd numbers
    return count_even + (n - count_even) // 2

# Driver code

arr=[1, 2, 3, 4, 5]

n = len(arr)

# Function call
print(Divisible(arr, n))

# This code is contribute by mohit kumar 29
```

## C#

```
// C# program to find maximum possible
// elements which divisible by 2
using System;

class GFG
{

    // Function to find maximum possible
    // elements which divisible by 2
    static int Divisible(int []arr, int n)
    {
        // To store count of even numbers
        int count_even = 0;

        for (int i = 0; i < n; i++)
            if (arr[i] % 2 == 0)
                count_even++;

        // All even numbers and half of odd numbers
        return count_even + (n - count_even) / 2;
    }

    // Driver code
    static public void Main ()
    {

        int []arr = { 1, 2, 3, 4, 5 };
        int n = arr.Length;

        // Function call
        Console.Write(Divisible(arr, n));
    }
}

// This code is contributed by ajit.
```

## java 描述语言

```
<script>
// Javascript program to find maximum possible
// elements which divisible by 2

// Function to find maximum possible
// elements which divisible by 2
function Divisible(arr, n)
{
    // To store count of even numbers
    let count_even = 0;

    for (let i = 0; i < n; i++)
        if (arr[i] % 2 == 0)
            count_even++;

    // All even numbers and half of odd numbers
    return count_even + parseInt((n - count_even) / 2);
}

// Driver code
    let arr = [ 1, 2, 3, 4, 5 ];

    let n = arr.length;

    // Function call
    document.write(Divisible(arr, n));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)。
**辅助空间** : O(1)。