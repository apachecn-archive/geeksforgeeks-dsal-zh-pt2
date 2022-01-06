# 计数偶数和奇数位置元素之和相等的子阵列

> 原文:[https://www . geeksforgeeks . org/count-subarrays-在偶数和奇数位置具有元素和-equal/](https://www.geeksforgeeks.org/count-subarrays-having-sum-of-elements-at-even-and-odd-positions-equal/)

给定整数数组 **arr[]** ，任务是找到子数组的总数，使得偶数位置的元素的[和奇数位置的元素的和相等](https://www.geeksforgeeks.org/sum-even-odd-elements-array/)。

**示例:**

> **输入:** arr[] = {1，2，3，4，1}
> **输出:** 1
> **解释:**
> {3，4，1}是唯一偶数位置{3，1}元素之和=奇数位置{4}元素之和的子阵列
> 
> **输入:** arr[] = {2，4，6，4，2}
> **输出:** 2
> **说明:**
> 有两个子阵{2，4，6，4}和{4，6，4，2}。

**方法:**想法是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)。对于形成的每个子阵列，求偶数索引处元素的和，减去奇数索引处的元素。如果总和为 0，计算这个子阵列，否则检查下一个子阵列。

下面是上述方法的实现:

## C++

```
// C program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count subarrays in
// which sum of elements at even
// and odd positions are equal
void countSubarrays(int arr[], int n)
{

    // Initialize variables
    int count = 0;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {
        int sum = 0;

        for(int j = i; j < n; j++)
        {

            // Check if position is
            // even then add to sum
            // then add it to sum
            if ((j - i) % 2 == 0)
                sum += arr[j];

            // Else subtract it to sum
            else
                sum -= arr[j];

            // Increment the count
            // if the sum equals 0
            if (sum == 0)
                count++;
        }
    }

    // Print the count of subarrays
    cout << " " << count ;
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 2, 4, 6, 4, 2 };

    // Size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    countSubarrays(arr, n);
    return 0;
}

// This code is contributed by shivanisinghss2110
```

## C

```
// C program for the above approach
#include <stdio.h>

// Function to count subarrays in
// which sum of elements at even
// and odd positions are equal
void countSubarrays(int arr[], int n)
{

    // Initialize variables
    int count = 0;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {
        int sum = 0;

        for(int j = i; j < n; j++)
        {

            // Check if position is
            // even then add to sum
            // then add it to sum
            if ((j - i) % 2 == 0)
                sum += arr[j];

            // Else subtract it to sum
            else
                sum -= arr[j];

            // Increment the count
            // if the sum equals 0
            if (sum == 0)
                count++;
        }
    }

    // Print the count of subarrays
    printf("%d", count);
}

// Driver Code
int main()
{

    // Given array arr[]
    int arr[] = { 2, 4, 6, 4, 2 };

    // Size of the array
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    countSubarrays(arr, n);
    return 0;
}

// This code is contributed by piyush3010
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

    // Function to count subarrays in
    // which sum of elements at even
    // and odd positions are equal
    static void countSubarrays(int arr[],
                               int n)
    {
        // Initialize variables
        int count = 0;

        // Iterate over the array
        for (int i = 0; i < n; i++) {
            int sum = 0;

            for (int j = i; j < n; j++) {

                // Check if position is
                // even then add to sum
                // then add it to sum
                if ((j - i) % 2 == 0)
                    sum += arr[j];

                // else subtract it to sum
                else
                    sum -= arr[j];

                // Increment the count
                // if the sum equals 0
                if (sum == 0)

                    count++;
            }
        }

        // Print the count of subarrays
        System.out.println(count);
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Given array arr[]
        int arr[] = { 2, 4, 6, 4, 2 };

        // Size of the array
        int n = arr.length;

        // Function call
        countSubarrays(arr, n);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count subarrays in
# which sum of elements at even
# and odd positions are equal
def countSubarrays(arr, n):

    # Initialize variables
    count = 0

    # Iterate over the array
    for i in range(n):
        sum = 0

        for j in range(i, n):

            # Check if position is
            # even then add to sum
            # hen add it to sum
            if ((j - i) % 2 == 0):
                sum += arr[j]

            # else subtract it to sum
            else:
                sum -= arr[j]

            # Increment the count
            # if the sum equals 0
            if (sum == 0):
                count += 1

    # Print the count of subarrays
    print(count)

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 2, 4, 6, 4, 2 ]

    # Size of the array
    n = len(arr)

    # Function call
    countSubarrays(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count subarrays in
// which sum of elements at even
// and odd positions are equal
static void countSubarrays(int []arr, int n)
{

    // Initialize variables
    int count = 0;

    // Iterate over the array
    for(int i = 0; i < n; i++)
    {
        int sum = 0;

        for(int j = i; j < n; j++)
        {

            // Check if position is
            // even then add to sum
            // then add it to sum
            if ((j - i) % 2 == 0)
                sum += arr[j];

            // else subtract it to sum
            else
                sum -= arr[j];

            // Increment the count
            // if the sum equals 0
            if (sum == 0)
                count++;
        }
    }

    // Print the count of subarrays
    Console.WriteLine(count);
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 2, 4, 6, 4, 2 };

    // Size of the array
    int n = arr.Length;

    // Function call
    countSubarrays(arr, n);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to count subarrays in
// which sum of elements at even
// and odd positions are equal
function countSubarrays(arr, n)
{

    // Initialize variables
    var count = 0;
    var i,j;
    // Iterate over the array
    for(i = 0; i < n; i++)
    {
        var sum = 0;

        for(j = i; j < n; j++)
        {

            // Check if position is
            // even then add to sum
            // then add it to sum
            if ((j - i) % 2 == 0)
                sum += arr[j];

            // Else subtract it to sum
            else
                sum -= arr[j];

            // Increment the count
            // if the sum equals 0
            if (sum == 0)
                count++;
        }
    }

    // Print the count of subarrays
    document.write(count);
}

// Driver Code

    // Given array arr[]
    var arr = [2, 4, 6, 4, 2];

    // Size of the array
    var n = arr.length;

    // Function call
    countSubarrays(arr, n);

</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间: *O(1)*