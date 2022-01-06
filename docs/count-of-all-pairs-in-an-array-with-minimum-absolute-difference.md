# 绝对差值最小的数组中所有对的计数

> 原文:[https://www . geesforgeks . org/绝对差值最小的阵列中所有对的计数/](https://www.geeksforgeeks.org/count-of-all-pairs-in-an-array-with-minimum-absolute-difference/)

给定大小为 **N** 的整数[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算具有最小绝对差的不同对的总数。
**举例:**

> **输入:** arr[] = {4，2，1，3}
> **输出:** 3
> **解释:**
> 对{1，2}、{2，3}、{3，4}之间的最小绝对差为 1。
> **输入:** arr[] = {1，3，8，10，15}
> **输出:** 2
> **解释:**
> 对{1，3}、{8，10}之间的最小绝对差为 2。

**方法:**思路是统计给定数组排序元素相邻元素最小绝对差的出现频率。按照以下步骤解决问题:

1.  [排序](https://www.geeksforgeeks.org/sorting-algorithms/)给定数组 **arr[]** 。
2.  比较排序数组中的所有相邻对，找出所有相邻对之间的最小绝对差。
3.  最后，计算所有具有等于最小差的差的相邻对。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of all
// pairs having minimal absolute difference
int numberofpairs(int arr[], int N)
{
    // Stores the count of pairs
    int answer = 0;

    // Sort the array
    sort(arr, arr + N);

    // Stores the minimum difference
    // between adjacent pairs
    int minDiff = INT_MAX;
    for (int i = 0; i < N - 1; i++)

        // Update the minimum
        // difference between pairs
        minDiff = min(minDiff,
                      arr[i + 1] - arr[i]);

    for (int i = 0; i < N - 1; i++) {

        if (arr[i + 1] - arr[i] == minDiff)

            // Increase count of
            // pairs with difference
            // equal to that of
            // minimum difference
            answer++;
    }

    // Return the final count
    return answer;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 4, 2, 1, 3 };
    int N = (sizeof arr) / (sizeof arr[0]);

    // Function Call
    cout << numberofpairs(arr, N) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above
import java.util.Arrays;
class GFG{

// Function to return the count of all
// pairs having minimal absolute difference
static int numberofpairs(int []arr, int N)
{
    // Stores the count of pairs
    int answer = 0;

    // Sort the array
    Arrays.sort(arr);

    // Stores the minimum difference
    // between adjacent pairs
    int minDiff = 10000000;
    for (int i = 0; i < N - 1; i++)

        // Update the minimum
        // difference between pairs
        minDiff = Math.min(minDiff,
                           arr[i + 1] - arr[i]);

    for (int i = 0; i < N - 1; i++)
    {
        if (arr[i + 1] - arr[i] == minDiff)

            // Increase count of
            // pairs with difference
            // equal to that of
            // minimum difference
            answer++;
    }

    // Return the final count
    return answer;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 4, 2, 1, 3 };
    int N = arr.length;

    // Function Call
    System.out.print(numberofpairs(arr, N));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return the count of all
# pairs having minimal absolute difference
def numberofpairs(arr, N):

    # Stores the count of pairs
    answer = 0

    # Sort the array
    arr.sort()

    # Stores the minimum difference
    # between adjacent pairs
    minDiff = 10000000
    for i in range(0, N - 1):

        # Update the minimum
        # difference between pairs
        minDiff = min(minDiff,
                      arr[i + 1] - arr[i])

    for i in range(0, N - 1):
        if arr[i + 1] - arr[i] == minDiff:

            # Increase count of pairs
            # with difference equal to
            # that of minimum difference
            answer += 1

    # Return the final count
    return answer

# Driver code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 4, 2, 1, 3 ]
    N = len(arr)

    # Function call
    print(numberofpairs(arr,N))

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to return the count of all
// pairs having minimal absolute difference
static int numberofpairs(int []arr, int N)
{

    // Stores the count of pairs
    int answer = 0;

    // Sort the array
    Array.Sort(arr);

    // Stores the minimum difference
    // between adjacent pairs
    int minDiff = 10000000;
    for(int i = 0; i < N - 1; i++)

        // Update the minimum
        // difference between pairs
        minDiff = Math.Min(minDiff,
                           arr[i + 1] -
                           arr[i]);

    for(int i = 0; i < N - 1; i++)
    {
        if (arr[i + 1] - arr[i] == minDiff)

            // Increase count of
            // pairs with difference
            // equal to that of
            // minimum difference
            answer++;
    }

    // Return the final count
    return answer;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array arr[]
    int []arr = { 4, 2, 1, 3 };
    int N = arr.Length;

    // Function Call
    Console.Write(numberofpairs(arr, N));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to return the count of all
    // pairs having minimal absolute difference
    function numberofpairs(arr, N)
    {
        // Stores the count of pairs
        let answer = 0;

        // Sort the array
        arr.sort();

        // Stores the minimum difference
        // between adjacent pairs
        let minDiff = Number.MAX_VALUE;
        for (let i = 0; i < N - 1; i++)

            // Update the minimum
            // difference between pairs
            minDiff = Math.min(minDiff,
                          arr[i + 1] - arr[i]);

        for (let i = 0; i < N - 1; i++) {

            if (arr[i + 1] - arr[i] == minDiff)

                // Increase count of
                // pairs with difference
                // equal to that of
                // minimum difference
                answer++;
        }

        // Return the final count
        return answer;
    }

    // Given array arr[]
    let arr = [ 4, 2, 1, 3 ];
    let N = arr.length;

    // Function Call
    document.write(numberofpairs(arr, N));

</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(N * log N)*
T5】辅助空间: *O(1)*