# 最小化给定阵列中的移除量，使最大值小于最小值的两倍

> 原文:[https://www . geeksforgeeks . org/最小化-给定阵列中的移除-最大化-小于两倍的最小值/](https://www.geeksforgeeks.org/minimize-removals-in-given-array-to-make-max-less-than-twice-of-min/)

给定一个整数[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是最小化所需的移除次数，以使 **arr[]** 中的最大元素小于最小值的两倍。

**示例**

> **输入:** arr[] = {4，6，21，7，5，9，12}
> **输出:**移除操作的最小次数为 4。
> **说明:**新修剪的数组为[7，5，9]，其中 9 为最大，5 为最小；9 < 2 × 5。
> 
> **输入:** arr[] = {14，21，62，43，39，57}
> **输出:**移除操作的最小次数为 2。
> **说明:**新修剪的数组为【62，43，39，57】
> ，其中 62 为最大，39 为最小；62 < 2 × 39。

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。这个想法非常简单有效，把这个问题看作是寻找最大元素小于最小元素两倍的最大子阵列，而不是从阵列中移除元素。按照以下步骤解决给定的问题。

*   从左到右遍历给定的数组，并将每个元素视为子数组的起点。
*   用选定的子阵起始指数，贪婪地尽可能选择子阵的另一端。
*   向右展开子阵列，一次一个元素，这样新添加的元素就满足给定的条件。
*   对所有子阵列遵循相同的过程，以找到最大尺寸的子阵列。
*   子阵列和输入阵列的大小之差将是所需的最小移除次数。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <iostream>
using namespace std;

// Function to return minimum
int Min(int a, int b)
{
    if (a < b)
        return a;
    else
        return b;
}

// Function to return maximum
int Max(int a, int b)
{
    if (a > b)
        return a;
    else
        return b;
}

// Function to find minimum removal operations.
int findMinRemovals(int arr[], int n)
{
    // Stores the length of the maximum
    // size subarray
    int max_range = 0;

    // To keep track of the minimum and
    // the maximum elements
    // in a subarray
    int minimum, maximum;

    // Traverse the array and consider
    // each element as a
    // starting point of a subarray
    for (int i = 0; i < n && n - i >
         max_range; i++) {
        // Reset the minimum and the
        // maximum elements
        minimum = maximum = arr[i];

        // Find the maximum size subarray
        // `arr[i…j]`
        for (int j = i; j < n; j++) {
            // Find the minimum and the
            // maximum elements in the current
            // subarray. We must do this in
            // constant time.
            minimum = Min(minimum, arr[j]);
            maximum = Max(maximum, arr[j]);

            // Discard the subarray if the
            // invariant is violated
            if (2 * minimum <= maximum) {
                break;
            }

            // Update `max_range` when a
            // bigger subarray is found
            max_range = Max(max_range, j - i + 1);
        }
    }

    // Return array size - length of
    // the maximum size subarray
    return n - max_range;
}

// Driver Code
int main()
{
    int arr[] = { 4, 6, 21, 7, 5, 9, 12 };
    int N = sizeof(arr) / sizeof(int);

    int res = findMinRemovals(arr, N);

    // Print the result
    cout << res;

    return 0;
}
```

## 蟒蛇 3

```
# python3 program for above approach

# Function to return minimum
def Min(a, b):

    if (a < b):
        return a
    else:
        return b

# Function to return maximum
def Max(a, b):

    if (a > b):
        return a
    else:
        return b

# Function to find minimum removal operations.
def findMinRemovals(arr, n):

    # Stores the length of the maximum
    # size subarray
    max_range = 0

    # To keep track of the minimum and
    # the maximum elements
    # in a subarray

    # Traverse the array and consider
    # each element as a
    # starting point of a subarray
    for i in range(0, n):
        if n - i <= max_range:
            break

        # Reset the minimum and the
        # maximum elements
        minimum = arr[i]
        maximum = arr[i]

        # Find the maximum size subarray
        # `arr[i…j]`
        for j in range(i, n):
            # Find the minimum and the
            # maximum elements in the current
            # subarray. We must do this in
            # constant time.
            minimum = Min(minimum, arr[j])
            maximum = Max(maximum, arr[j])

            # Discard the subarray if the
            # invariant is violated
            if (2 * minimum <= maximum):
                break

                # Update `max_range` when a
                # bigger subarray is found
            max_range = Max(max_range, j - i + 1)

        # Return array size - length of
        # the maximum size subarray
    return n - max_range

# Driver Code
if __name__ == "__main__":

    arr = [4, 6, 21, 7, 5, 9, 12]
    N = len(arr)

    res = findMinRemovals(arr, N)

    # Print the result
    print(res)

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to return minimum
function Min(a, b)
{
    if (a < b)
        return a;
    else
        return b;
}

// Function to return maximum
function Max(a, b)
{
    if (a > b)
        return a;
    else
        return b;
}

// Function to find minimum removal operations.
function findMinRemovals(arr, n)
{

    // Stores the length of the maximum
    // size subarray
    let max_range = 0;

    // To keep track of the minimum and
    // the maximum elements
    // in a subarray
    let minimum, maximum;

    // Traverse the array and consider
    // each element as a
    // starting point of a subarray
    for(let i = 0; i < n && n - i > max_range; i++)
    {

        // Reset the minimum and the
        // maximum elements
        minimum = maximum = arr[i];

        // Find the maximum size subarray
        // `arr[i…j]`
        for(let j = i; j < n; j++)
        {

            // Find the minimum and the
            // maximum elements in the current
            // subarray. We must do this in
            // constant time.
            minimum = Min(minimum, arr[j]);
            maximum = Max(maximum, arr[j]);

            // Discard the subarray if the
            // invariant is violated
            if (2 * minimum <= maximum)
            {
                break;
            }

            // Update `max_range` when a
            // bigger subarray is found
            max_range = Max(max_range, j - i + 1);
        }
    }

    // Return array size - length of
    // the maximum size subarray
    return n - max_range;
}

// Driver Code
let arr = [ 4, 6, 21, 7, 5, 9, 12 ];
let N = arr.length;

let res = findMinRemovals(arr, N);

// Print the result
document.write(res);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
4
```

***时间复杂度:*** O(N*N)
***辅助空间:*** O(1)