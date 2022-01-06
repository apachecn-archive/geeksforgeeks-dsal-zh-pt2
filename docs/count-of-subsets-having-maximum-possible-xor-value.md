# 具有最大可能异或值的子集计数

> 原文:[https://www . geesforgeks . org/具有最大可能异或值的子集计数/](https://www.geeksforgeeks.org/count-of-subsets-having-maximum-possible-xor-value/)

给定一个由正整数组成的数组 **arr[]** 。任务是计算具有最大位**异或**的 **arr[]** 的不同非空子集的数量。

**示例:**

> **输入:** arr[] = {3，1}
> **输出:** 1
> **解释:**子集的最大可能位异或是 3。
> 在 arr[]中，只有一个子集的按位异或为 3，即{3}。
> 所以，1 就是答案。
> 
> **输入:** arr[] = {3，2，1，5}
> **输出:** 2

**方法:**这个问题可以通过使用**位屏蔽**来解决。按照以下步骤解决给定的问题。

*   初始化一个变量，比如 **maxXorVal = 0** ，将子集的最大可能位异或存储在 arr[]。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**找到 **maxXorVal** 的值。
*   初始化一个变量，比如**计数子集= 0** ，用最大位异或来计数子集的数量。
*   之后[用 **maxXorVal**](https://www.geeksforgeeks.org/count-number-of-subsets-having-a-particular-xor-value/) 数值计算子集数量。
*   返回**count subset**作为最终答案。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find subsets having maximum XOR
int countMaxOrSubsets(vector<int>& nums)
{
    // Store the size of arr[]
    long long n = nums.size();

    // To sotre maximum possible
    // bitwise XOR subset in arr[]
    long long maxXorVal = 0;

    // Find the maximum bitwise xor value
    for (int i = 0; i < (1 << n); i++) {

        long long xorVal = 0;
        for (int j = 0; j < n; j++) {

            if (i & (1 << j)) {
                xorVal = (xorVal ^ nums[j]);
            }
        }

        // Take maximum of each value
        maxXorVal = max(maxXorVal, xorVal);
    }

    // Count the number
    // of subsets having bitwise
    // XOR value as maxXorVal
    long long count = 0;

    for (int i = 0; i < (1 << n); i++) {
        long long val = 0;
        for (int j = 0; j < n; j++) {
            if (i & (1 << j)) {
                val = (val ^ nums[j]);
            }
        }

        if (val == maxXorVal) {
            count++;
        }
    }
    return count;
}

// Driver Code
int main()
{
    int N = 4;
    vector<int> arr = { 3, 2, 1, 5 };

    // Print the answer
    cout << countMaxOrSubsets(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

public class GFG
{

// Function to find subsets having maximum XOR
static int countMaxOrSubsets(int []nums)
{
    // Store the size of arr[]
    long n = nums.length;

    // To sotre maximum possible
    // bitwise XOR subset in arr[]
    long maxXorVal = 0;

    // Find the maximum bitwise xor value
    for (int i = 0; i < (1 << n); i++) {

        long xorVal = 0;
        for (int j = 0; j < n; j++) {

            if ((i & (1 << j)) == 0) {
                xorVal = (xorVal ^ nums[j]);
            }
        }

        // Take maximum of each value
        maxXorVal = Math.max(maxXorVal, xorVal);
    }

    // Count the number
    // of subsets having bitwise
    // XOR value as maxXorVal
    long count = 0;

    for (int i = 0; i < (1 << n); i++) {
        long val = 0;
        for (int j = 0; j < n; j++) {
            if ((i & (1 << j)) == 0) {
                val = (val ^ nums[j]);
            }
        }

        if (val == maxXorVal) {
            count++;
        }
    }
    return (int)count;
}

// Driver Code
public static void main(String args[])
{
    int N = 4;
    int []arr = { 3, 2, 1, 5 };

    // Print the answer
    System.out.print(countMaxOrSubsets(arr));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for above approach

# Function to find subsets having maximum XOR
def countMaxOrSubsets(nums):

    # Store the size of arr[]
    n = len(nums)

    # To sotre maximum possible
    # bitwise XOR subset in arr[]
    maxXorVal = 0

    # Find the maximum bitwise xor value
    for i in range(0, (1 << n)):

        xorVal = 0
        for j in range(0, n):

            if (i & (1 << j)):
                xorVal = (xorVal ^ nums[j])

        # Take maximum of each value
        maxXorVal = max(maxXorVal, xorVal)

    # Count the number
    # of subsets having bitwise
    # XOR value as maxXorVal
    count = 0

    for i in range(0, (1 << n)):
        val = 0
        for j in range(0, n):
            if (i & (1 << j)):
                val = (val ^ nums[j])

        if (val == maxXorVal):
            count += 1
    return count

# Driver Code
if __name__ == "__main__":

    N = 4
    arr = [3, 2, 1, 5]

    # Print the answer
    print(countMaxOrSubsets(arr))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for above approach
using System;

public class GFG
{

// Function to find subsets having maximum XOR
static int countMaxOrSubsets(int []nums)
{

    // Store the size of []arr
    int n = nums.Length;

    // To sotre maximum possible
    // bitwise XOR subset in []arr
    int maxXorVal = 0;

    // Find the maximum bitwise xor value
    for (int i = 0; i < (1 << n); i++) {

        long xorVal = 0;
        for (int j = 0; j < n; j++) {

            if ((i & (1 << j)) == 0) {
                xorVal = (xorVal ^ nums[j]);
            }
        }

        // Take maximum of each value
        maxXorVal = (int)Math.Max(maxXorVal, xorVal);
    }

    // Count the number
    // of subsets having bitwise
    // XOR value as maxXorVal
    long count = 0;

    for (int i = 0; i < (1 << n); i++) {
        long val = 0;
        for (int j = 0; j < n; j++) {
            if ((i & (1 << j)) == 0) {
                val = (val ^ nums[j]);
            }
        }

        if (val == maxXorVal) {
            count++;
        }
    }
    return (int)count;
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 3, 2, 1, 5 };

    // Print the answer
    Console.Write(countMaxOrSubsets(arr));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to find subsets having maximum XOR
function countMaxOrSubsets(nums)
{

    // Store the size of arr[]
    let n = nums.length;

    // To sotre maximum possible
    // bitwise XOR subset in arr[]
    let maxXorVal = 0;

    // Find the maximum bitwise xor value
    for(let i = 0; i < (1 << n); i++)
    {
        let xorVal = 0;
        for(let j = 0; j < n; j++)
        {
            if (i & (1 << j))
            {
                xorVal = (xorVal ^ nums[j]);
            }
        }

        // Take maximum of each value
        maxXorVal = Math.max(maxXorVal, xorVal);
    }

    // Count the number
    // of subsets having bitwise
    // XOR value as maxXorVal
    let count = 0;

    for(let i = 0; i < (1 << n); i++)
    {
        let val = 0;
        for (let j = 0; j < n; j++)
        {
            if (i & (1 << j))
            {
                val = (val ^ nums[j]);
            }
        }

        if (val == maxXorVal)
        {
            count++;
        }
    }
    return count;
}

// Driver Code
let N = 4;
let arr = [ 3, 2, 1, 5 ];

// Print the answer
document.write(countMaxOrSubsets(arr));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
2
```

**时间复杂度:**O(2<sup>16</sup>)
T5】辅助空间 : O(1)