# 最小化最大和最小元素之差不超过 K 的子集数

> 原文:[https://www . geesforgeks . org/最小化最大和最小元素差不超过-k 的子集数/](https://www.geeksforgeeks.org/minimize-count-of-subsets-with-difference-between-maximum-and-minimum-element-not-exceeding-k/)

给定一个数组 **arr[ ]** 和一个整数 **K** ，任务是将给定的数组分割成最小数量的子集，这些子集具有最大元素和最小元素之差≤ **K** 。

**示例:**

> **输入:** arr[ ] = {1，3，7，9，10}，K = 3
> **输出:** 2
> **解释:**
> arr[]的可能子集之一是 **{1，3}** 和 **{7，9，10}** ，其中最大和最小元素之间的差值不大于 K，即 3。
> 
> **输入:** arr[ ] = {1，10，8，3，9}，K = 3
> T3】输出: 2。

**方法:**按照以下步骤解决问题:

1.  按升序对数组进行排序。
2.  遍历数组，将 **currMin** 设置为数组的第一个元素，并使用遍历的元素不断更新 **currMax** 。
3.  如果在任何指标下 **currMax** 和 **currMin** 之间的差值超过 **K，**将**的答案**增加 1，并将 **currMax** 和 **currMin** 设置为**arr【I】。**
4.  最后，返回**回答**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count
// of subsets of required type
int findCount(int arr[], int N, int K)
{
    sort(arr, arr + N);

    // Stores the result
    int result = 1;

    // Store the maximum and minimum
      // element of the current subset
    int cur_max = arr[0];
    int cur_min = arr[0];

    for (int i = 1; i < N; i++) {

        // Update current maximum
        cur_max = arr[i];

        // If difference exceeds K
        if (cur_max - cur_min > K) {

            // Update count
            result++;

            // Update maximum and minimum
            // to the current subset
            cur_max = arr[i];
            cur_min = arr[i];
        }
    }

    return result;
}

// Driver Code
int main()
{
    int arr[] = { 1,10, 8, 3, 9 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findCount(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// above approach
import java.util.*;

class GFG{

// Function to find the minimum count
// of subsets of required type
static int findCount(int arr[], int N, int K)
{
    Arrays.sort(arr);

    // Stores the result
    int result = 1;

    // Store the maximum and minimum
    // element of the current subset
    int cur_max = arr[0];
    int cur_min = arr[0];

    for(int i = 1; i < N; i++)
    {

        // Update current maximum
        cur_max = arr[i];

        // If difference exceeds K
        if (cur_max - cur_min > K)
        {

            // Update count
            result++;

            // Update maximum and minimum
            // to the current subset
            cur_max = arr[i];
            cur_min = arr[i];
        }
    }
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 10, 8, 3, 9 };
    int K = 3;
    int N = arr.length;

    System.out.print(findCount(arr, N, K));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum count
# of subsets of required type
def findCount(arr, N, K):

    arr.sort()

    # Stores the result
    result = 1

    # Store the maximum and minimum
    # element of the current subset
    cur_max = arr[0]
    cur_min = arr[0]

    for i in range(1, N):

        # Update current maximum
        cur_max = arr[i]

        # If difference exceeds K
        if(cur_max - cur_min > K):

            # Update count
            result += 1

            # Update maximum and minimum
            # to the current subset
            cur_max = arr[i]
            cur_min = arr[i]

    return result

# Driver Code
arr = [ 1, 10, 8, 3, 9 ]
K = 3
N = len(arr)

# Function call
print(findCount(arr, N, K))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// above approach
using System;
class GFG{

// Function to find the minimum count
// of subsets of required type
static int findCount(int []arr,
                     int N, int K)
{
    Array.Sort(arr);

    // Stores the result
    int result = 1;

    // Store the maximum and minimum
    // element of the current subset
    int cur_max = arr[0];
    int cur_min = arr[0];

    for(int i = 1; i < N; i++)
    {

        // Update current maximum
        cur_max = arr[i];

        // If difference exceeds K
        if (cur_max - cur_min > K)
        {

            // Update count
            result++;

            // Update maximum and minimum
            // to the current subset
            cur_max = arr[i];
            cur_min = arr[i];
        }
    }
    return result;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 10, 8, 3, 9 };
    int K = 3;
    int N = arr.Length;

    Console.Write(findCount(arr, N, K));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

// Function to find the minimum count
// of subsets of required type
function findCount(arr, N, K)
{
    arr.sort();

    // Stores the result
    let result = 1;

    // Store the maximum and minimum
    // element of the current subset
    let cur_max = arr[0];
    let cur_min = arr[0];

    for(let i = 1; i < N; i++)
    {

        // Update current maximum
        cur_max = arr[i];

        // If difference exceeds K
        if (cur_max - cur_min > K)
        {

            // Update count
            result++;

            // Update maximum and minimum
            // to the current subset
            cur_max = arr[i];
            cur_min = arr[i];
        }
    }
    return result;
}

// Driver Code

     let arr = [ 1, 10, 8, 3, 9 ];
    let K = 3;
    let N = arr.length;

    document.write(findCount(arr, N, K));

 // This code is contributed by target_2.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(NLog(N))*
***辅助空间:** O(1)*