# 对数组中的对(I，j)进行计数，使得|arr[i]|和|arr[j]|都位于| arr[I]–arr[j]|和|arr[i] + arr[j]|

之间

> 原文:[https://www . geeksforgeeks . org/count-pairs-I-j-from-a-arri-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr-arr](https://www.geeksforgeeks.org/count-pairs-i-j-from-an-array-such-that-arri-and-arrj-both-lies-between-arri-arrj-and-arri-arrj/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算对的数量 **(arr[i]，arr[j])** ，使得 **|arr[i]|** 和 **|arr[j]|** 位于**| arr[I]–arr[j]|**和 **|arr[i] + arr[j]|** 之间。

**示例:**

> ***输入:** arr[] = {1，3，5，7}*
> ***输出:** 2*
> ***解释:***
> *Pair (arr[1]，arr[2]) (= (3，5))位于| 3–5 |(= 2)和|3 + 5| (= 8)之间。*
> *对(arr[2]，arr[3]) (= (5，7))位于| 5–7 |(= 2)和|5 + 7| (= 12)之间。*
> 
> ***输入:** arr[] = {-4，1，9，7，-1，2，8}*
> ***输出:** 9*

**方法:**给定的问题可以通过分析以下情况来解决:

*   **如果 X 为正，Y 为正:**
    *   **| X–Y |**依旧**| X–Y |。**
    *   **|X + Y|** 遗迹 **|X + Y|。**
*   **如果 X 为负，Y 为正:**
    *   **| X–Y |**变为 **|-(X + Y)|，**即 **|X + Y|。**
    *   **|X + Y|** 变为**|-(X–Y)|，**即**| X–Y |。**
*   **如果 X 为正，Y 为负:**
    *   **| X–Y |**变为 **|X + Y|。**
    *   **|X + Y|** 变为**| X–Y |。**
*   **如果 X 为负，Y 为负:**
    *   **| X–Y |**依旧**| X–Y |。**
    *   **|X + Y|** 遗迹 **|X + Y|。**

从以上案例中可以明显看出，**| X–Y |****| X+Y |**最多是互换数值，并不改变解。
因此，如果一对对 **(X，Y)**有效，那么它也将对上述任何情况有效，如 **(-X，Y)** 。因此，任务简化为在求解时只取 **X** 和 **Y** 的绝对值，即求 **(X，Y)**，其中**| X–Y |≤X，Y ≤ X + Y** 。

按照以下步骤解决问题:

*   取数组 **arr[]中所有元素的绝对值。**
*   [排序数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 。
*   初始化一个变量，说**左边**，为 **0。**
*   初始化一个变量，比如 **ans，**来存储有效对的计数。
*   [使用变量遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，说**右**，并执行以下步骤:
    *   增加**左**直到 **2 *arr【左】**小于 **arr【右】**。
    *   将值**(I–左)**添加到**和**中，以包括有效对的数量。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find pairs (i, j) such that
// |arr[i]| and |arr[j]| lies in between
// |arr[i] - arr[j]| and |arr[i] + arr[j]|
void findPairs(int arr[], int N)
{
    // Calculate absolute value
    // of all array elements
    for (int i = 0; i < N; i++)
        arr[i] = abs(arr[i]);

    // Sort the array
    sort(arr, arr + N);

    int left = 0;

    // Stores the count of pairs
    int ans = 0;

    // Traverse the array
    for (int right = 0; right < N; right++) {

        while (2 * arr[left] < arr[right])

            // Increment left
            left++;

        // Add to the current
        // count of pairs
        ans += (right - left);
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 5, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);

    findPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to find pairs (i, j) such that
// |arr[i]| and |arr[j]| lies in between
// |arr[i] - arr[j]| and |arr[i] + arr[j]|
static void findPairs(int arr[], int N)
{

    // Calculate absolute value
    // of all array elements
    for(int i = 0; i < N; i++)
        arr[i] = Math.abs(arr[i]);

    // Sort the array
    Arrays.sort(arr);

    int left = 0;

    // Stores the count of pairs
    int ans = 0;

    // Traverse the array
    for(int right = 0; right < N; right++)
    {
        while (2 * arr[left] < arr[right])

            // Increment left
            left++;

        // Add to the current
        // count of pairs
        ans += (right - left);
    }

    // Print the answer
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 5, 7 };
    int N = arr.length;

    findPairs(arr, N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find pairs (i, j) such that
# |arr[i]| and |arr[j]| lies in between
# |arr[i] - arr[j]| and |arr[i] + arr[j]|
def findPairs(arr,  N):

    # Calculate absolute value
    # of all array elements
    for i in range(N):
        arr[i] = abs(arr[i])

    # Sort the array
    arr.sort()
    left = 0

    # Stores the count of pairs
    ans = 0

    # Traverse the array
    for right in range(N):
        while (2 * arr[left] < arr[right]):

            # Increment left
            left += 1

        # Add to the current
        # count of pairs
        ans += (right - left)

    # Print the answer
    print(ans)

# Driver Code
if __name__ == "__main__":
    arr = [1, 3, 5, 7]
    N = len(arr)

    findPairs(arr, N)

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find pairs (i, j) such that
// |arr[i]| and |arr[j]| lies in between
// |arr[i] - arr[j]| and |arr[i] + arr[j]|
static void findPairs(int []arr, int N)
{

    // Calculate absolute value
    // of all array elements
    for(int i = 0; i < N; i++)
        arr[i] = Math.Abs(arr[i]);

    // Sort the array
    Array.Sort(arr);

    int left = 0;

    // Stores the count of pairs
    int ans = 0;

    // Traverse the array
    for(int right = 0; right < N; right++)
    {
        while (2 * arr[left] < arr[right])

            // Increment left
            left++;

        // Add to the current
        // count of pairs
        ans += (right - left);
    }

    // Print the answer
    Console.Write(ans);
}

// Driver Code
public static void Main(string[] args)
{
    int []arr = { 1, 3, 5, 7 };
    int N = arr.Length;

    findPairs(arr, N);
}
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find pairs (i, j) such that
// |arr[i]| and |arr[j]| lies in between
// |arr[i] - arr[j]| and |arr[i] + arr[j]|
function findPairs(arr, N)
{

    // Calculate absolute value
    // of all array elements
    for (let i = 0; i < N; i++)
        arr[i] = Math.abs(arr[i]);

    // Sort the array
    arr.sort((a, b) => a - b);

    let left = 0;

    // Stores the count of pairs
    let ans = 0;

    // Traverse the array
    for (let right = 0; right < N; right++) {

        while (2 * arr[left] < arr[right])

            // Increment left
            left++;

        // Add to the current
        // count of pairs
        ans += (right - left);
    }

    // Print the answer
    document.write(ans);
}

// Driver Code

    let arr = [ 1, 3, 5, 7 ];
    let N = arr.length;

    findPairs(arr, N);

// This code is contributed by Manoj.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*