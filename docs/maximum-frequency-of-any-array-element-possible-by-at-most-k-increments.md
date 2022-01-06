# 任何数组元素的最大频率最多增加 K 次

> 原文:[https://www . geeksforgeeks . org/最多 k 个增量的任意数组元素的最大频率/](https://www.geeksforgeeks.org/maximum-frequency-of-any-array-element-possible-by-at-most-k-increments/)

给定一个大小为 **N** 的数组**arr【】**和一个整数 **K** ，任务是以最多 **K** 的增量找到任何数组元素的最大可能频率。

**示例:**

> **输入:** arr[] = {1，4，8，13}，N = 4，K = 5
> **输出:** 2
> **解释:**
> 递增 arr[0]两次将 arr[]修改为{4，4，8，13}。最大频率= 2。
> 将 arr[1]递增四次会将 arr[]修改为{1，8，8，13}。最大频率= 2。
> 将 arr[2]递增五次会将 arr[]修改为{1，4，13，13}。最大频率= 2。
> 因此，最多 5 次增量可以获得的任何数组元素的最大可能频率为 2。
> 
> **输入:** arr[] = {2，4，5}，N = 3，K = 4
> T3】输出: 3

**方法:**这个问题可以通过[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)和[排序](https://www.geeksforgeeks.org/sorting-algorithms/)来解决。按照步骤解决这个问题。

*   [排序数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 。
*   初始化变量**和= 0，开始= 0** 和合成频率 **res = 0** 。
*   [在索引范围**【0，N–1】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下步骤:
    *   将**和**加**等于【结束】**。
    *   迭代一个循环，直到 **[(结束–开始+1)* arr[结束]–sum]**的值小于 **K** ，并执行以下操作:
        *   将**和**的值减 **arr【开始】**。
        *   将**的值增加 **1** 开始**。
    *   完成上述步骤后，最多使用 **K** 操作，即可使**【开始，结束】**范围内的所有元素相等。因此，将 **res** 的值更新为 res 和(end–start+1)的**最大值。**
*   最后，执行 **K** 操作后，将 **res** 的值打印为最频繁元素的频率。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum possible
// frequency of a most frequent element
// after at most K increment operations
void maxFrequency(int arr[], int N, int K)
{
    // Sort the input array
    sort(arr, arr + N);

    int start = 0, end = 0;

    // Stores the sum of sliding
    // window and the maximum possible
    // frequency of any array element
    int sum = 0, res = 0;

    // Traverse the array
    for (end = 0; end < N; end++) {

        // Add the current element
        // to the window
        sum += arr[end];

        // Decrease the window size

        // If it is not possible to make the
        // array elements in the window equal
        while ((end - start + 1) * arr[end] - sum > K) {

            // Update the value of sum
            sum -= arr[start];

            // Increment the value of start
            start++;
        }

        // Update the maximum possible frequency
        res = max(res, end - start + 1);
    }

    // Print the frequency of
    // the most frequent array
    // element after K increments
    cout << res << endl;
}

// Driver code
int main()
{
    int arr[] = { 1, 4, 8, 13 };
    int N = 4;
    int K = 5;
    maxFrequency(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to find the maximum possible
// frequency of a most frequent element
// after at most K increment operations
static void maxFrequency(int arr[], int N, int K)
{

    // Sort the input array
    Arrays.sort(arr);

    int start = 0, end = 0;

    // Stores the sum of sliding
    // window and the maximum possible
    // frequency of any array element
    int sum = 0, res = 0;

    // Traverse the array
    for(end = 0; end < N; end++)
    {

        // Add the current element
        // to the window
        sum += arr[end];

        // Decrease the window size

        // If it is not possible to make the
        // array elements in the window equal
        while ((end - start + 1) *
                   arr[end] - sum > K)
        {

            // Update the value of sum
            sum -= arr[start];

            // Increment the value of start
            start++;
        }

        // Update the maximum possible frequency
        res = Math.max(res, end - start + 1);
    }

    // Print the frequency of
    // the most frequent array
    // element after K increments
    System.out.println(res);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 4, 8, 13 };
    int N = 4;
    int K = 5;

    maxFrequency(arr, N, K);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum possible
# frequency of a most frequent element
# after at most K increment operations
def maxFrequency(arr, N, K):

    # Sort the input array
    arr.sort()

    start = 0
    end = 0

    # Stores the sum of sliding
    # window and the maximum possible
    # frequency of any array element
    sum = 0
    res = 0

    # Traverse the array
    for end in range(N):

        # Add the current element
        # to the window
        sum += arr[end]

        # Decrease the window size

        # If it is not possible to make the
        # array elements in the window equal
        while ((end - start + 1) * arr[end] - sum > K):

            # Update the value of sum
            sum -= arr[start]

            # Increment the value of start
            start += 1

        # Update the maximum possible frequency
        res = max(res, end - start + 1)

    # Print the frequency of
    # the most frequent array
    # element after K increments
    print(res)

# Driver code
if __name__ == '__main__':

    arr = [ 1, 4, 8, 13 ]
    N = 4
    K = 5

    maxFrequency(arr, N, K)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum possible
// frequency of a most frequent element
// after at most K increment operations
static void maxFrequency(int[] arr, int N, int K)
{

    // Sort the input array
    Array.Sort(arr);

    int start = 0, end = 0;

    // Stores the sum of sliding
    // window and the maximum possible
    // frequency of any array element
    int sum = 0, res = 0;

    // Traverse the array
    for(end = 0; end < N; end++)
    {

        // Add the current element
        // to the window
        sum += arr[end];

        // Decrease the window size

        // If it is not possible to make the
        // array elements in the window equal
        while ((end - start + 1) *
           arr[end] - sum > K)
        {

            // Update the value of sum
            sum -= arr[start];

            // Increment the value of start
            start++;
        }

        // Update the maximum possible frequency
        res = Math.Max(res, end - start + 1);
    }

    // Print the frequency of
    // the most frequent array
    // element after K increments
    Console.WriteLine(res);
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 4, 8, 13 };
    int N = 4;
    int K = 5;

    maxFrequency(arr, N, K);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum possible
// frequency of a most frequent element
// after at most K increment operations
function maxFrequency(arr, N, K) {
    // Sort the input array
    arr.sort((a, b) => a - b);

    let start = 0, end = 0;

    // Stores the sum of sliding
    // window and the maximum possible
    // frequency of any array element
    let sum = 0, res = 0;

    // Traverse the array
    for (end = 0; end < N; end++) {

        // Add the current element
        // to the window
        sum += arr[end];

        // Decrease the window size

        // If it is not possible to make the
        // array elements in the window equal
        while ((end - start + 1) * arr[end] - sum > K) {

            // Update the value of sum
            sum -= arr[start];

            // Increment the value of start
            start++;
        }

        // Update the maximum possible frequency
        res = Math.max(res, end - start + 1);
    }

    // Print the frequency of
    // the most frequent array
    // element after K increments
    document.write(res + "<br>");
}

// Driver code

let arr = [1, 4, 8, 13];
let N = 4;
let K = 5;
maxFrequency(arr, N, K);

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(NlogN)
T3】辅助空间: O(1)