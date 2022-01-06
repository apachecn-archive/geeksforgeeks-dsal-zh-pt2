# 通过所有数组元素的最多一个增量或减量来最大化一个元素的频率

> 原文:[https://www . geeksforgeeks . org/按所有数组元素最多递增或递减一次来最大化元素频率/](https://www.geeksforgeeks.org/maximize-frequency-of-an-element-by-at-most-one-increment-or-decrement-of-all-array-elements/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过将每个数组元素递增或递减 **1** 至多一次来找到任意数组元素[的最大频率。](https://www.geeksforgeeks.org/frequent-element-array/)

**示例:**

> **输入:** arr[] = { 3，1，4，1，5，9，2 }
> **输出:** 4
> **解释:**
> 将 arr[0]的值减 1 会将 arr[]修改为{ 2，1，4，1，5，9，2 }
> 将 arr[1]的值增加 1 会将 arr[]修改为{ 2，2，4，1，5，9，2 }
> 将 arr[3]的值增加
> 
> **输入:** arr[] = { 0，1，2，3，4，5，6 }
> **输出:** 3
> **解释:**
> 将 arr[0]的值增加 1 会将 arr[]修改为{ 1，1，2，3，4，5，6 }
> 将 arr[2]的值减少 1 会将 arr[]修改为{ 1，1，3，4，5，6 }
> 因此，数组元素(即

**进场:**使用 [**贪婪手法**](https://www.geeksforgeeks.org/greedy-algorithms/) 可以解决问题。其思想是找出数组中存在的[最大](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)和[最小的元素，并通过迭代数组元素范围内的所有数字来计算三个连续数字的频率的最大和。最后，打印得到的最大和。按照以下步骤解决问题:](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)

*   [找到阵中最大的元素](https://www.geeksforgeeks.org/max_element-in-cpp/)说， **Max** 。
*   [找到数组中最小的元素](https://www.geeksforgeeks.org/stdmin_element-in-cpp/)说， **Min** 。
*   计算数组中所有数组元素在**【最小值，最大值】**范围内的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   迭代范围**【Min，Max】**，计算三个连续数字的频率的最大和。
*   最后，打印得到的最大和。

下面是上述方法的实现。

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to maximize the frequency
// of an array element by incrementing or
// decrementing array elements at most once
void max_freq(int arr[], int N)
{

    // Stores the largest array element
    int Max = *max_element(arr, arr + N);

    // Stores the smallest array element
    int Min = *min_element(arr, arr + N);

    // freq[i]: Stores frequency of
    // (i + Min) in the array
    int freq[Max - Min + 1] = { 0 };

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update frequency
        // of arr[i]
        freq[arr[i] - Min]++;
    }

    // Stores maximum frequency of an
    // array element by incrementing
    // or decrementing array elements
    int maxSum = 0;

    // Iterate all the numbers over
    // the range [Min, Max]
    for (int i = 0;
         i < (Max - Min - 1); i++) {

        // Stores sum of three
        // consecutive numbers
        int val = freq[i] + freq[i + 1] + freq[i + 2];

        // Update maxSum
        maxSum = max(maxSum, val);
    }

    // Print maxSum
    cout << maxSum << "\n";
}

// Driver Code
int main()
{

    int arr[] = { 3, 1, 4, 1, 5, 9, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    max_freq(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.Arrays;

class GFG{

// Function to maximize the frequency
// of an array element by incrementing or
// decrementing array elements at most once
static void max_freq(int arr[], int N)
{
    Arrays.sort(arr);

    // Stores the largest array element
    int Max = arr[N - 1];

    // Stores the smallest array element
    int Min = arr[0];

    // freq[i]: Stores frequency of
    // (i + Min) in the array
    int freq[] = new int[Max - Min + 1];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency
        // of arr[i]
        freq[arr[i] - Min]++;
    }

    // Stores maximum frequency of an
    // array element by incrementing
    // or decrementing array elements
    int maxSum = 0;

    // Iterate all the numbers over
    // the range [Min, Max]
    for(int i = 0; i < (Max - Min - 1); i++)
    {

        // Stores sum of three
        // consecutive numbers
        int val = freq[i] + freq[i + 1] +
                            freq[i + 2];

        // Update maxSum
        maxSum = Math.max(maxSum, val);
    }

    // Print maxSum
    System.out.println(maxSum);
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 3, 1, 4, 1, 5, 9, 2 };
    int N = arr.length;

    // Function call
    max_freq(arr, N);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to maximize the frequency
# of an array element by incrementing or
# decrementing array elements at most once
def max_freq(arr, N):

    # Stores the largest array element
    Max = max(arr)

    # Stores the smallest array element
    Min = min(arr)

    # freq[i]: Stores frequency of
    # (i + Min) in the array
    freq = [0] * (Max - Min + 1)

    # Traverse the array
    for i in range(N):

        # Update frequency
        # of arr[i]
        freq[arr[i] - Min] += 1

    # Stores maximum frequency of an
    # array element by incrementing
    # or decrementing array elements
    maxSum = 0

    # Iterate all the numbers over
    # the range [Min, Max]
    for i in range( Max - Min - 1):

        # Stores sum of three
        # consecutive numbers
        val = freq[i] + freq[i + 1] + freq[i + 2]

        # Update maxSum
        maxSum = max(maxSum, val)

    # Print maxSum
    print(maxSum)

# Driver Code
if __name__ == "__main__" :

    arr = [ 3, 1, 4, 1, 5, 9, 2 ]
    N = len(arr)

    # Function call
    max_freq(arr, N)

# This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to maximize the frequency
// of an array element by incrementing or
// decrementing array elements at most once
static void max_freq(int[] arr, int N)
{
    Array.Sort(arr);

    // Stores the largest array element
    int Max = arr[N - 1];

    // Stores the smallest array element
    int Min = arr[0];

    // freq[i]: Stores frequency of
    // (i + Min) in the array
    int[] freq = new int[Max - Min + 1];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update frequency
        // of arr[i]
        freq[arr[i] - Min]++;
    }

    // Stores maximum frequency of an
    // array element by incrementing
    // or decrementing array elements
    int maxSum = 0;

    // Iterate all the numbers over
    // the range [Min, Max]
    for(int i = 0; i < (Max - Min - 1); i++)
    {

        // Stores sum of three
        // consecutive numbers
        int val = freq[i] + freq[i + 1] +
                            freq[i + 2];

        // Update maxSum
        maxSum = Math.Max(maxSum, val);
    }

    // Print maxSum
    Console.WriteLine(maxSum);
}

// Driver Code
public static void Main()
{
    int[] arr = { 3, 1, 4, 1, 5, 9, 2 };
    int N = arr.Length;

    // Function call
    max_freq(arr, N);
}
}

// This code is contributed by code_hunt.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to maximize the frequency
// of an array element by incrementing or
// decrementing array elements at most once
function max_freq(arr, N)
{
    arr.sort();

    // Stores the largest array element
    let Max = arr[N - 1];

    // Stores the smallest array element
    let Min = arr[0];

    // freq[i]: Stores frequency of
    // (i + Min) in the array
    let freq = [];
    for(let i = 0; i < Max - Min + 1 ; i++)
    {
        freq[i] = 0;
    }

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Update frequency
        // of arr[i]
        freq[arr[i] - Min]++;
    }

    // Stores maximum frequency of an
    // array element by incrementing
    // or decrementing array elements
    let maxSum = 0;

    // Iterate all the numbers over
    // the range [Min, Max]
    for(let i = 0; i < (Max - Min - 1); i++)
    {

        // Stores sum of three
        // consecutive numbers
        let val = freq[i] + freq[i + 1] +
                            freq[i + 2];

        // Update maxSum
        maxSum = Math.max(maxSum, val);
    }

    // Prlet maxSum
    document.write(maxSum);
}

// Driver Code

      let arr = [ 3, 1, 4, 1, 5, 9, 2 ];
    let N = arr.length;

    // Function call
    max_freq(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N+| Max–Min |)，其中 **Max、Min** 分别表示最大和最小的数组元素*
***辅助空间:**O(| Max–Min |)*