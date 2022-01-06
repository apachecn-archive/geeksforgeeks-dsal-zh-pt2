# 一个数组的两个子集之和的最大可能差|集合 2

> 原文:[https://www . geeksforgeeks . org/数组集 2 的两个子集的最大可能差值/](https://www.geeksforgeeks.org/maximum-possible-difference-of-two-subsets-of-an-array-set-2/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[ ]** ，任务是找出通过将数组划分为任意两个非空子集而获得的两个子集之和的最大差值。
***注意:**子集不能有任何公共元素。子集可以包含重复元素。*

示例:

> **输入:** arr[] = {1，3，2，4，5}
> **输出:** 13
> **解释:**分区{3，2，4，5}和{1}最大化了子集之间的差异。
> 
> **输入:** arr[] = {1，-5，3，2，-7}
> **输出:** 18
> **解释**:分区{1，3，2}和{-5，-7}最大化了子集之间的差异。

**进场:**这个问题可以用 [**贪婪进场**](https://www.geeksforgeeks.org/greedy-algorithms/) 解决。在这个问题中，子集 A 和 B 都必须是非空的。所以我们必须在两者中至少放入一个元素。我们试图使子集 A 中的元素之和尽可能大，子集 B 中的元素之和尽可能小。最后我们打印总和(A)–总和(B)。

按照下面给出的步骤解决问题:

*   当 **arr[ ]** 同时包含非负数和负数时，将所有非负数放入子集 A，负数放入子集 B，打印**和(A)–和(B)** 。
*   当所有数字都是正数时，将除最小正数之外的所有数字放入子集 A，将最小正数放入子集 B，打印**sum(A)–sum(B)**。
*   当所有数字都为负数时，将除最大负数外的所有数字放在子集 B 中，将最大负数放在子集 A 中，并打印**sum(A)–sum(B)。**

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;

int maxSumAfterPartition(int arr[], int n)
{
    // Stores the positive elements
    vector<int> pos;

    // Stores the negative elements
    vector<int> neg;

    // Stores the count of 0s
    int zero = 0;

    // Sum of all positive numbers
    int pos_sum = 0;

    // Sum of all negative numbers
    int neg_sum = 0;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (arr[i] > 0) {

            pos.push_back(arr[i]);
            pos_sum += arr[i];
        }
        else if (arr[i] < 0) {

            neg.push_back(arr[i]);
            neg_sum += arr[i];
        }
        else {

            zero++;
        }
    }

    // Stores the difference
    int ans = 0;

    // Sort the positive numbers
    // in ascending order
    sort(pos.begin(), pos.end());

    // Sort the negative numbers
    // in decreasing order
    sort(neg.begin(), neg.end(), greater<int>());

    // Case 1: Include both positive
    // and negative numbers
    if (pos.size() > 0 && neg.size() > 0) {

        ans = (pos_sum - neg_sum);
    }
    else if (pos.size() > 0) {

        if (zero > 0) {

            // Case 2:  When all numbers are
            // positive and array contains 0s

              //Put all numbers in subset A and
              //one 0 in subset B
            ans = (pos_sum);
        }
        else {

            // Case 3: When all numbers are positive

              //Put all numbers in subset A except the 
              //smallest positive number which is put in B
            ans = (pos_sum - 2 * pos[0]);
        }
    }
    else {
        if (zero > 0) {

            // Case 4: When all numbers are
            // negative and array contains 0s

            // Put all numbers in subset B
            // and one 0 in subset A
            ans = (-1 * neg_sum);
        }
        else {
            // Case 5: When all numbers are negative

            // Place the largest negative number
            // in subset A and remaining in B
            ans = (neg[0] - (neg_sum - neg[0]));
        }
    }

    return ans;
}
int main()
{
    int arr[] = { 1, 2, 3, -5, -7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxSumAfterPartition(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;
class GFG {
    static int maxSumAfterPartition(int arr[], int n)
    {
        // Stores the positive elements
       ArrayList<Integer> pos
            = new ArrayList<Integer>();

        // Stores the negative elements
         ArrayList<Integer> neg
            = new ArrayList<Integer>();

        // Stores the count of 0s
        int zero = 0;

        // Sum of all positive numbers
        int pos_sum = 0;

        // Sum of all negative numbers
        int neg_sum = 0;

        // Iterate over the array
        for (int i = 0; i < n; i++) {

            if (arr[i] > 0) {

                pos.add(arr[i]);
                pos_sum += arr[i];
            }
            else if (arr[i] < 0) {

                neg.add(arr[i]);
                neg_sum += arr[i];
            }
            else {

                zero++;
            }
        }

        // Stores the difference
        int ans = 0;

        // Sort the positive numbers
        // in ascending order
        Collections.sort(pos);

        // Sort the negative numbers
        // in decreasing order
        Collections.sort(neg);

        // Case 1: Include both positive
        // and negative numbers
        if (pos.size() > 0 && neg.size() > 0) {

            ans = (pos_sum - neg_sum);
        }
        else if (pos.size() > 0) {

            if (zero > 0) {

                // Case 2:  When all numbers are
                // positive and array contains 0s

                // Put all numbers in subset A and
                // one 0 in subset B
                ans = (pos_sum);
            }
            else {

                // Case 3: When all numbers are positive

                // Put all numbers in subset A except the
                // smallest positive number which is put in
                // B
                ans = (pos_sum - 2 * pos.get(0));
            }
        }
        else {
            if (zero > 0) {

                // Case 4: When all numbers are
                // negative and array contains 0s

                // Put all numbers in subset B
                // and one 0 in subset A
                ans = (-1 * neg_sum);
            }
            else {
                // Case 5: When all numbers are negative

                // Place the largest negative number
                // in subset A and remaining in B
                ans = (neg.get(0) - (neg_sum - neg.get(0)));
            }
        }

        return ans;
    }

  // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, -5, -7 };
        int n = 5;
        System.out.println(maxSumAfterPartition(arr, n));
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python 3 Program for the above approach

def maxSumAfterPartition(arr, n):
    # Stores the positive elements
    pos = []

    # Stores the negative elements
    neg = []

    # Stores the count of 0s
    zero = 0

    # Sum of all positive numbers
    pos_sum = 0

    # Sum of all negative numbers
    neg_sum = 0

    # Iterate over the array
    for i in range(n):
        if (arr[i] > 0):
            pos.append(arr[i])
            pos_sum += arr[i]

        elif(arr[i] < 0):
            neg.append(arr[i])
            neg_sum += arr[i]

        else:
            zero += 1

    # Stores the difference
    ans = 0

    # Sort the positive numbers
    # in ascending order
    pos.sort()

    # Sort the negative numbers
    # in decreasing order
    neg.sort(reverse=True)

    # Case 1: Include both positive
    # and negative numbers
    if (len(pos) > 0 and len(neg) > 0):

        ans = (pos_sum - neg_sum)
    elif(len(pos) > 0):
        if (zero > 0):

            # Case 2:  When all numbers are
            # positive and array contains 0s

              #Put all numbers in subset A and
              #one 0 in subset B
            ans = (pos_sum)
        else:

            # Case 3: When all numbers are positive

              #Put all numbers in subset A except the 
              #smallest positive number which is put in B
            ans = (pos_sum - 2 * pos[0])
    else:
        if (zero > 0):
            # Case 4: When all numbers are
            # negative and array contains 0s

            # Put all numbers in subset B
            # and one 0 in subset A
            ans = (-1 * neg_sum)
        else:
            # Case 5: When all numbers are negative

            # Place the largest negative number
            # in subset A and remaining in B
            ans = (neg[0] - (neg_sum - neg[0]))

    return ans

if __name__ == '__main__':
    arr = [1, 2, 3, -5, -7]
    n = len(arr)
    print(maxSumAfterPartition(arr, n))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# Program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int maxSumAfterPartition(int []arr, int n)
{
    // Stores the positive elements
    List<int> pos = new List<int>();

    // Stores the negative elements
    List<int> neg = new List<int>();

    // Stores the count of 0s
    int zero = 0;

    // Sum of all positive numbers
    int pos_sum = 0;

    // Sum of all negative numbers
    int neg_sum = 0;

    // Iterate over the array
    for (int i = 0; i < n; i++) {

        if (arr[i] > 0) {

            pos.Add(arr[i]);
            pos_sum += arr[i];
        }
        else if (arr[i] < 0) {

            neg.Add(arr[i]);
            neg_sum += arr[i];
        }
        else {

            zero++;
        }
    }

    // Stores the difference
    int ans = 0;

    // Sort the positive numbers
    // in ascending order
    pos.Sort();

    // Sort the negative numbers
    // in decreasing order
    neg.Sort();
    neg.Reverse();

    // Case 1: Include both positive
    // and negative numbers
    if (pos.Count > 0 && neg.Count > 0) {

        ans = (pos_sum - neg_sum);
    }
    else if (pos.Count > 0) {

        if (zero > 0) {

            // Case 2:  When all numbers are
            // positive and array contains 0s

              //Put all numbers in subset A and
              //one 0 in subset B
            ans = (pos_sum);
        }
        else {

            // Case 3: When all numbers are positive

              //Put all numbers in subset A except the 
              //smallest positive number which is put in B
            ans = (pos_sum - 2 * pos[0]);
        }
    }
    else {
        if (zero > 0) {

            // Case 4: When all numbers are
            // negative and array contains 0s

            // Put all numbers in subset B
            // and one 0 in subset A
            ans = (-1 * neg_sum);
        }
        else {
            // Case 5: When all numbers are negative

            // Place the largest negative number
            // in subset A and remaining in B
            ans = (neg[0] - (neg_sum - neg[0]));
        }
    }

    return ans;
}

public static void Main()
{
    int []arr = { 1, 2, 3, -5, -7 };
    int n = arr.Length;

    Console.Write(maxSumAfterPartition(arr, n));
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        function maxSumAfterPartition(arr, n) {
            // Stores the positive elements
            let pos = [];

            // Stores the negative elements
            let neg = [];

            // Stores the count of 0s
            let zero = 0;

            // Sum of all positive numbers
            let pos_sum = 0;

            // Sum of all negative numbers
            let neg_sum = 0;

            // Iterate over the array
            for (let i = 0; i < n; i++) {

                if (arr[i] > 0) {

                    pos.push(arr[i]);
                    pos_sum += arr[i];
                }
                else if (arr[i] < 0) {

                    neg.push(arr[i]);
                    neg_sum += arr[i];
                }
                else {

                    zero++;
                }
            }

            // Stores the difference
            let ans = 0;

            // Sort the positive numbers
            // in ascending order
            pos.sort(function (a, b) { return a - b })

            // Sort the negative numbers
            // in decreasing order
            neg.sort(function (a, b) { return b - a })

            // Case 1: Include both positive
            // and negative numbers
            if (pos.length > 0 && neg.length > 0) {

                ans = (pos_sum - neg_sum);
            }
            else if (pos.length > 0) {

                if (zero > 0) {

                    // Case 2:  When all numbers are
                    // positive and array contains 0s

                    //Put all numbers in subset A and
                    //one 0 in subset B
                    ans = (pos_sum);
                }
                else {

                    // Case 3: When all numbers are positive

                    //Put all numbers in subset A except the 
                    //smallest positive number which is put in B
                    ans = (pos_sum - 2 * pos[0]);
                }
            }
            else {
                if (zero > 0) {

                    // Case 4: When all numbers are
                    // negative and array contains 0s

                    // Put all numbers in subset B
                    // and one 0 in subset A
                    ans = (-1 * neg_sum);
                }
                else {
                    // Case 5: When all numbers are negative

                    // Place the largest negative number
                    // in subset A and remaining in B
                    ans = (neg[0] - (neg_sum - neg[0]));
                }
            }

            return ans;
        }

        let arr = [1, 2, 3, -5, -7];
        let n = arr.length;

        document.write(maxSumAfterPartition(arr, n));

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
18
```

***时间复杂度:*** O(NlogN)
***辅助空间:*** O(N)