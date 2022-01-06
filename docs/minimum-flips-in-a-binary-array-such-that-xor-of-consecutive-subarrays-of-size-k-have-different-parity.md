# 二进制数组中的最小翻转，使得大小为 K 的连续子数组的异或具有不同的奇偶性

> 原文:[https://www . geeksforgeeks . org/二进制数组中最小翻转大小为 k 的连续子数组的异或具有不同的奇偶校验/](https://www.geeksforgeeks.org/minimum-flips-in-a-binary-array-such-that-xor-of-consecutive-subarrays-of-size-k-have-different-parity/)

给定长度为 **N** 的二进制数组 **arr[]** ，任务是找到数组中所需的最小翻转，使得大小为 K 的连续子数组的异或具有不同的奇偶性。
**例:**

> **输入:** arr[] = {0，1，0，1，1}，K = 2
> **输出:** 2
> **解释:**
> 对于上述给定的数组 XOR，大小为 2 的连续子数组为:{(0，1): 1，(1，0): 1，(0，1): 1，(1，1): 0}
> 需要两次翻转，可对以下索引进行:
> **索引 0:** 是
> **索引 1:** 需要翻转 1 <sup>st</sup> 索引的位，使得第二子阵列的异或变为 0。
> **输入:** arr[]={0，0，1，1，0，0}，K = 3
> **输出:** 1
> **解释:**
> 对于上述给定的数组，大小为 2 的连续子数组的异或为:{(0，0，1): 1，(0，1，1): 0，(1，1，0): 1}
> 需要一个翻转，可以在上面完成

**方法:**为了使连续子阵列具有不同的[奇偶性](https://www.geeksforgeeks.org/program-to-find-parity/)，整个阵列依赖于大小为 K 的第一个子阵列。也就是说，大小为 K 的每个下一个子阵列应该是前一个子阵列的否定。
**例如:**对于大小为 4 的阵列，使得大小为 2 的连续子阵列具有不同的奇偶性:

```
Let the first subarray of size 2 be {1, 1}
Then the next subarray can be {0, 0}

Consecutive subarrays of size 2 in this array:
{(1, 1): 0, (1, 0): 1, (0, 0): 0} 
```

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum flips required such that
// alternate subarrays have
// different parity

#include <iostream>
#include <limits.h>
using namespace std;

// Function to find the minimum
// flips required in binary array
int count_flips(int a[], int n, int k)
{
    // Boolean value to indicate
    // odd or even value of 1's
    bool set = false;
    int ans = 0, min_diff = INT_MAX;

    // Loop to iterate over
    // the subarrays of size K
    for (int i = 0; i < k; i++) {

        // curr_index is used to iterate
        // over all the subarrays
        int curr_index = i, segment = 0,
          count_zero = 0, count_one = 0;

        // Loop to iterate over the array
        // at the jump of K to
        // consider every parity       
        while (curr_index < n) {

            // Condition to check if the
            // subarray is at even position
            if (segment % 2 == 0) {

                // The value needs to be
                // same as the first subarray
                if (a[curr_index] == 1)
                    count_zero++;
                else
                    count_one++;
            }
            else {
                // The value needs to be
                // opposite of the first subarray
                if (a[curr_index] == 0)
                    count_zero++;
                else
                    count_one++;
            }
            curr_index = curr_index + k;
            segment++;
        }
        ans += min(count_one, count_zero);
        if (count_one < count_zero)
            set = !set;
        // Update the minimum difference
        min_diff = min(min_diff,
         abs(count_zero - count_one));
    }

    // Condition to check if the 1s
    // in the subarray is odd
    if (set)
        return ans;
    else
        return ans + min_diff;
}

// Driver Code
int main()
{
    int n = 6, k = 3;
    int a[] = { 0, 0, 1, 1, 0, 0 };
    cout << count_flips(a, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the minimum flips
// required such that alternate subarrays
// have different parity

import java.util.*;

class Count_Flips {

    // Function to find the minimum
    // flips required in binary array
    public static int count_flips(
              int a[], int n, int k){

        // Boolean value to indicate
        // odd or even value of 1's
        boolean set = false;
        int ans = 0,
           min_diff = Integer.MAX_VALUE;

        // Loop to iterate over
        // the subarrays of size K
        for (int i = 0; i < k; i++) {

            // curr_index is used to iterate
            // over all the subarrays
            int curr_index = i, segment = 0,
               count_zero = 0, count_one = 0;

            // Loop to iterate over the array
            // at the jump of K to
            // consider every parity
            while (curr_index < n) {

                // Condition to check if the
                // subarray is at even position
                if (segment % 2 == 0) {

                    // The value needs to be
                    // same as the first subarray
                    if (a[curr_index] == 1)
                        count_zero++;
                    else
                        count_one++;
                }
                else {
                    // The value needs to be
                    // opposite of the first subarray
                    if (a[curr_index] == 0)
                        count_zero++;
                    else
                        count_one++;
                }
                curr_index = curr_index + k;
                segment++;
            }
            ans += Math.min(count_one, count_zero);
            if (count_one < count_zero)
                set = !set;
            // Update the minimum difference
            min_diff = Math.min(min_diff,
             Math.abs(count_zero - count_one));
        }
        // Condition to check if the 1s
        // in the subarray is odd
        if (set)
            return ans;
        else
            return ans + min_diff;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 6, k = 3;
        int a[] = { 0, 0, 1, 1, 0, 0 };
        System.out.println(count_flips(a, n, k));
    }
}
```

## 蟒蛇 3

```
# Python implementation to find the
# minimum flips required such that
# alternate subarrays have
# different parity

# Function to find the minimum
# flips required in binary array
def count_flips(a, n, k):
    min_diff, ans, set = n, 0, False

    # Loop to iterate over
    # the subarrays of size K
    for i in range(k):
        # curr_index is used to iterate
        # over all the subarrays
        curr_index, segment,\
        count_zero, count_one =\
                   i, 0, 0, 0

        # Loop to iterate over the array
        # at the jump of K to
        # consider every parity
        while curr_index < n:

            # Condition to check if the
            # subarray is at even position
            if segment % 2 == 0:
                # The value needs to be
                # same as the first subarray
                if a[curr_index] == 1:
                    count_zero += 1
                else:
                    count_one += 1
            else:
                # The value needs to be
                # opposite of the first subarray
                if a[curr_index] == 0:
                    count_zero += 1
                else:
                    count_one += 1
            curr_index += k
            segment+= 1
        ans += min(count_zero, count_one)
        if count_one<count_zero:
            set = not set
        min_diff = min(min_diff,\
         abs(count_zero-count_one))
    # Condition to check if the 1s
    # in the subarray is odd
    if set:
        return ans
    else:
        return ans + min_diff

# Driver Code
if __name__ == "__main__":
    n, k = 6, 3
    a =[0, 0, 1, 1, 0, 0]
    print(count_flips(a, n, k))
```

## C#

```
// C# implementation to find the minimum flips
// required such that alternate subarrays
// have different parity
using System;

class Count_Flips
{

    // Function to find the minimum
    // flips required in binary array
    static int count_flips(int []a, int n, int k)
    {

        // Boolean value to indicate
        // odd or even value of 1's
        bool set = false;
        int ans = 0, min_diff = int.MaxValue;

        // Loop to iterate over
        // the subarrays of size K
        for (int i = 0; i < k; i++) {

            // curr_index is used to iterate
            // over all the subarrays
            int curr_index = i, segment = 0,
            count_zero = 0, count_one = 0;

            // Loop to iterate over the array
            // at the jump of K to
            // consider every parity
            while (curr_index < n) {

                // Condition to check if the
                // subarray is at even position
                if (segment % 2 == 0) {

                    // The value needs to be
                    // same as the first subarray
                    if (a[curr_index] == 1)
                        count_zero++;
                    else
                        count_one++;
                }
                else {
                    // The value needs to be
                    // opposite of the first subarray
                    if (a[curr_index] == 0)
                        count_zero++;
                    else
                        count_one++;
                }
                curr_index = curr_index + k;
                segment++;
            }
            ans += Math.Min(count_one, count_zero);
            if (count_one < count_zero)
                set = !set;

            // Update the minimum difference
            min_diff = Math.Min(min_diff,
            Math.Abs(count_zero - count_one));
        }

        // Condition to check if the 1s
        // in the subarray is odd
        if (set)
            return ans;
        else
            return ans + min_diff;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int n = 6, k = 3;
        int []a = { 0, 0, 1, 1, 0, 0 };
        Console.WriteLine(count_flips(a, n, k));
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>

// Javascript implementation to find the minimum flips
// required such that alternate subarrays
// have different parity

    // Function to find the minimum
    // flips required in binary array
    function count_flips(a , n , k) {

        // Boolean value to indicate
        // odd or even value of 1's
        var set = false;
        var ans = 0, min_diff = Number.MAX_VALUE;

        // Loop to iterate over
        // the subarrays of size K
        for (i = 0; i < k; i++) {

            // curr_index is used to iterate
            // over all the subarrays
            var curr_index = i, segment = 0, count_zero = 0, count_one = 0;

            // Loop to iterate over the array
            // at the jump of K to
            // consider every parity
            while (curr_index < n) {

                // Condition to check if the
                // subarray is at even position
                if (segment % 2 == 0) {

                    // The value needs to be
                    // same as the first subarray
                    if (a[curr_index] == 1)
                        count_zero++;
                    else
                        count_one++;
                } else {
                    // The value needs to be
                    // opposite of the first subarray
                    if (a[curr_index] == 0)
                        count_zero++;
                    else
                        count_one++;
                }
                curr_index = curr_index + k;
                segment++;
            }
            ans += Math.min(count_one, count_zero);
            if (count_one < count_zero)
                set = !set;
            // Update the minimum difference
            min_diff = Math.min(min_diff, Math.abs(count_zero - count_one));
        }
        // Condition to check if the 1s
        // in the subarray is odd
        if (set)
            return ans;
        else
            return ans + min_diff;
    }

    // Driver Code

        var n = 6, k = 3;
        var a = [ 0, 0, 1, 1, 0, 0 ];
        document.write(count_flips(a, n, k));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
1
```

**业绩分析:**

*   **时间复杂度:**和上面的方法一样，在最坏的情况下，只有一个占用 O(N)时间的循环。因此时间复杂性将是 **O(N)** 。
*   **辅助空间复杂度:**和上面的方法一样，没有使用额外的空间。因此辅助空间的复杂性将是 **O(1)** 。