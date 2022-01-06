# 满足给定等式

的三胞胎计数

> 原文:[https://www . geesforgeks . org/满足给定等式的三元组计数/](https://www.geeksforgeeks.org/count-of-triplets-that-satisfy-the-given-equation/)

给定非负整数的数组**arr[]****N**。任务是计算三元组(I，j，k)的数量，其中 **0 ≤ i < j ≤ k < N** 使得**a【I】^ a【I+1】^…^ a【j–1】= a【j】^ a【j+1】^…^ a【k】**其中 **^** 是按位异或。
**举例:**

> **输入:** arr[] = {2，5，6，4，2}
> **输出:** 2
> 有效的三元组是(2，3，4)和(2，4，4)。
> **输入:** arr[] = {5，2，7}
> **输出:** 2

**天真方法:**考虑每一个三元组，检查所需元素的 xor 是否相等。
**有效方法:**如果**arr[I]^ arr[I+1]^…^ arr[j–1]= arr[j]^ arr[j+1]^…^ arr[k]**则**arr[I]^ arr[I+1]^…arr[k]= 0**因为**x = 0**。现在问题简化为寻找异或为 0 的子阵列。但是每个这样的子阵列可以具有多个这样的三元组，即

> 如果**arr[I]^ arr[I+1]^…^ arr[k]= 0**
> 那么，**(arr[I])**^(arr[I+1]^…^ arr[k])= 0
> 以及，arr[I]^**(arr[I+1])**^…arr[k]= 0
> arr[I]arr[I+1]**(arr[I+2])**…arr

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of required triplets
int CountTriplets(int* arr, int n)
{
    int ans = 0;
    for (int i = 0; i < n - 1; i++) {

        // First element of the
        // current sub-array
        int first = arr[i];
        for (int j = i + 1; j < n; j++) {

            // XOR every element of
            // the current sub-array
            first ^= arr[j];

            // If the XOR becomes 0 then
            // update the count of triplets
            if (first == 0)
                ans += (j - i);
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 6, 4, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << CountTriplets(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of required triplets
static int CountTriplets(int[] arr, int n)
{
    int ans = 0;
    for (int i = 0; i < n - 1; i++)
    {

        // First element of the
        // current sub-array
        int first = arr[i];
        for (int j = i + 1; j < n; j++)
        {

            // XOR every element of
            // the current sub-array
            first ^= arr[j];

            // If the XOR becomes 0 then
            // update the count of triplets
            if (first == 0)
                ans += (j - i);
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = {2, 5, 6, 4, 2};
    int n = arr.length;

    System.out.println(CountTriplets(arr, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of required triplets
def CountTriplets(arr, n):

    ans = 0
    for i in range(n - 1):

        # First element of the
        # current sub-array
        first = arr[i]
        for j in range(i + 1, n):

            # XOR every element of
            # the current sub-array
            first ^= arr[j]

            # If the XOR becomes 0 then
            # update the count of triplets
            if (first == 0):
                ans += (j - i)

    return ans

# Driver code
arr = [2, 5, 6, 4, 2 ]
n = len(arr)
print(CountTriplets(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of required triplets
    static int CountTriplets(int[] arr, int n)
    {
        int ans = 0;
        for (int i = 0; i < n - 1; i++)
        {

            // First element of the
            // current sub-array
            int first = arr[i];
            for (int j = i + 1; j < n; j++)
            {

                // XOR every element of
                // the current sub-array
                first ^= arr[j];

                // If the XOR becomes 0 then
                // update the count of triplets
                if (first == 0)
                    ans += (j - i);
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int []arr = {2, 5, 6, 4, 2};
        int n = arr.Length;

        Console.WriteLine(CountTriplets(arr, n));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the count
// of required triplets
function CountTriplets(arr, n)
{
    let ans = 0;
    for (let i = 0; i < n - 1; i++) {

        // First element of the
        // current sub-array
        let first = arr[i];
        for (let j = i + 1; j < n; j++) {

            // XOR every element of
            // the current sub-array
            first ^= arr[j];

            // If the XOR becomes 0 then
            // update the count of triplets
            if (first == 0)
                ans += (j - i);
        }
    }
    return ans;
}

// Driver code
    let arr = [ 2, 5, 6, 4, 2 ];
    let n = arr.length;

    document.write(CountTriplets(arr, n));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(n <sup>2</sup> )。
**辅助空间** : O(1)。