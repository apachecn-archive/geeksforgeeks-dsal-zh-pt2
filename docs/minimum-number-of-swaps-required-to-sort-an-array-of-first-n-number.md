# 对前 N 个数组进行排序所需的最小交换次数

> 原文:[https://www . geesforgeks . org/最小交换次数-需要对第一个 n-number 数组进行排序/](https://www.geeksforgeeks.org/minimum-number-of-swaps-required-to-sort-an-array-of-first-n-number/)

给定一个从 1 到 n 的不同整数的数组 **arr[]** ，任务是找到对数组进行排序所需的最小交换次数。

**示例:**

```
Input: arr[] = { 7, 1, 3, 2, 4, 5, 6 }
Output: 5
Explanation:
i           arr             swap (indices)
0   [7, 1, 3, 2, 4, 5, 6]   swap (0, 3)
1   [2, 1, 3, 7, 4, 5, 6]   swap (0, 1)
2   [1, 2, 3, 7, 4, 5, 6]   swap (3, 4)
3   [1, 2, 3, 4, 7, 5, 6]   swap (4, 5)
4   [1, 2, 3, 4, 5, 7, 6]   swap (5, 6)
5   [1, 2, 3, 4, 5, 6, 7]
Therefore, total number of swaps = 5

Input: arr[] = { 2, 3, 4, 1, 5 }
Output: 3
```

**进场:**

*   对于**arr【】**中的每个索引。
*   检查当前元素是否在正确的位置。由于数组包含从 1 到 N 的不同元素，我们可以简单地将元素与其在数组中的索引进行比较，以检查它是否在正确的位置。
*   如果当前元素不在它的正确位置，那么用已经占据了它的位置的元素交换这个元素。
*   否则检查下一个索引。

下面是上述方法的实现:

## C++

```
#include <iostream>
using namespace std;

// Function to find minimum swaps
int minimumSwaps(int arr[],int n)
{
    // Initialise count variable
    int count = 0;
    int i = 0;

    while (i < n)
    {

        // If current element is
        // not at the right position
        if (arr[i] != i + 1)
        {

            while (arr[i] != i + 1)
            {
                int temp = 0;

                // Swap current element
                // with correct position
                // of that element
                temp = arr[arr[i] - 1];
                arr[arr[i] - 1] = arr[i];
                arr[i] = temp;
                count++;
            }
        }

        // Increment for next index
        // when current element is at
        // correct position
        i++;
    }
    return count;
}

// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 1, 5 };

    int n = sizeof(arr)/sizeof(arr[0]);

    // Function to find minimum swaps
    cout << minimumSwaps(arr,n) ;
}

// This code is contributed by AnkitRai01
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum
// number of swaps required to sort
// the given array
import java.io.*;
import java.util.*;

class GfG {

    // Function to find minimum swaps
    static int minimumSwaps(int[] arr)
    {
        // Initialise count variable
        int count = 0;
        int i = 0;
        while (i < arr.length) {

            // If current element is
            // not at the right position
            if (arr[i] != i + 1) {

                while (arr[i] != i + 1) {
                    int temp = 0;

                    // Swap current element
                    // with correct position
                    // of that element
                    temp = arr[arr[i] - 1];
                    arr[arr[i] - 1] = arr[i];
                    arr[i] = temp;
                    count++;
                }
            }

            // Increment for next index
            // when current element is at
            // correct position
            i++;
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 3, 4, 1, 5 };

        // Function to find minimum swaps
        System.out.println(minimumSwaps(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# number of swaps required to sort
# the given array

# Function to find minimum swaps
def minimumSwaps(arr):

    # Initialise count variable
    count = 0;
    i = 0;
    while (i < len(arr)):

        # If current element is
        # not at the right position
        if (arr[i] != i + 1):

            while (arr[i] != i + 1):
                temp = 0;

                # Swap current element
                # with correct position
                # of that element
                temp = arr[arr[i] - 1];
                arr[arr[i] - 1] = arr[i];
                arr[i] = temp;
                count += 1;

        # Increment for next index
        # when current element is at
        # correct position
        i += 1;

    return count;

# Driver code
if __name__ == '__main__':
    arr = [ 2, 3, 4, 1, 5 ];

    # Function to find minimum swaps
    print(minimumSwaps(arr));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to find the minimum
// number of swaps required to sort
// the given array
using System;

class GfG
{

    // Function to find minimum swaps
    static int minimumSwaps(int[] arr)
    {
        // Initialise count variable
        int count = 0;
        int i = 0;
        while (i < arr.Length)
        {

            // If current element is
            // not at the right position
            if (arr[i] != i + 1)
            {

                while (arr[i] != i + 1)
                {
                    int temp = 0;

                    // Swap current element
                    // with correct position
                    // of that element
                    temp = arr[arr[i] - 1];
                    arr[arr[i] - 1] = arr[i];
                    arr[i] = temp;
                    count++;
                }
            }

            // Increment for next index
            // when current element is at
            // correct position
            i++;
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = { 2, 3, 4, 1, 5 };

        // Function to find minimum swaps
        Console.WriteLine(minimumSwaps(arr));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program to find the minimum
// number of swaps required to sort
// the given array

// Function to find minimum swaps
function minimumSwaps(arr)
{
    // Initialise count variable
    let count = 0;
    let i = 0;
    while (i < arr.length)
    {

        // If current element is
        // not at the right position
        if (arr[i] != i + 1)
        {

            while (arr[i] != i + 1)
            {
                let temp = 0;

                // Swap current element
                // with correct position
                // of that element
                temp = arr[arr[i] - 1];
                arr[arr[i] - 1] = arr[i];
                arr[i] = temp;
                count++;
            }
        }

        // Increment for next index
        // when current element is at
        // correct position
        i++;
    }
    return count;
}

// Driver code

let arr = [2, 3, 4, 1, 5 ];

// Function to find minimum swaps
document.write(minimumSwaps(arr));

</script>
```

**Output:** 

```
3
```

**时间复杂度** : O(N)，其中 N 是数组的大小。
**辅助空间:** O(1)