# 最小化交换以重新排列数组，使得任何元素的剩余部分及其索引与 3 相同

> 原文:[https://www . geeksforgeeks . org/minimum-swap-to-重排-array-so-任何元素的余数及其索引与 3 相同/](https://www.geeksforgeeks.org/minimize-swaps-to-rearrange-array-such-that-remainder-of-any-element-and-its-index-with-3-are-same/)

给定一个[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T2【arr】。任务是尽量减少所需的[交换](https://www.geeksforgeeks.org/c-program-swap-two-numbers/)的数量，使得对于**arr【】**中的每个 **i** ， **arr[i]%3 = i%3** 。如果这种重新排列是不可能的，打印-1。

**示例:**

> **输入:** arr[ ] = {4，3，5，2，9，7}
> **输出:** 3
> **解释:**以下是在 arr[]
> 中执行的操作最初，索引% 3 = {0，1，2，0，1，2}和 arr[i] % 3 = {1，0，2，2，0，1}。
> 交换 arr[0]和 arr[1]将 arr[]更新为 arr[] % 3 = {0，1，2，2，0，1}
> 交换 arr[3]和 arr[4]将 arr[]更新为 arr[] % 3 = {0，1，2，0，2，2，2，1}
> 交换 arr[4]和 arr[5]将 arr[]更新为 arr[] % 3 = {0，1，2，0，1，2}
> 因此，需要 3 次交换才能得到最小的结果数组
> 
> **输入:** arr[] = {0，1，2，3，4}
> **输出:0**

**方法:**这个问题是基于实现的，与[模属性](https://www.geeksforgeeks.org/modular-arithmetic/)有关。按照以下步骤解决给定的问题。

*   [用 **i** 迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，从 **i = 0** 到 **i=n-1**
    *   如果 **arr[i] % 3** 等于 **0** ，则继续。
    *   否则，找到从 **i+1** 到 **n-1** 的索引 **j** ，其中 **i % 3 = arr[j] % 3** 和 **j % 3 = arr[i] % 3** 。
    *   通过以上步骤，将两个数组元素移动到它们想要的位置。
    *   如果没有找到这样的 **j** ，则找到一个索引 **k** 形式 **i+1** 到 **n-1** ，其中 **i % 3 = arr[k] % 3** ，并交换元素。
    *   基本情况是对索引进行计数，使得**索引%3 = arr[i] % 3** 。
*   返回最终计数作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ Program for above approach
#include <iostream>
using namespace std;

// Function to swap two array elements.
void swapping(int arr[], int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

// Function to count the Swaps required such that
// for all i in arr[] arr[]% 3 = i % 3
int CountMinSwaps(int arr[], int n)
{

    // index_mod_i = count of indexes which
    // give i on modulo 3: index%3==i
    int index_mod_0 = 0,
        index_mod_1 = 0,
        index_mod_2 = 0;

    // array_mod_i = count of array elements
    // which give i on modulo 3: arr[i]%3==i
    int array_mod_0 = 0,
        array_mod_1 = 0,
        array_mod_2 = 0;

    int i, j, count = 0;

    for (i = 0; i < n; i++) {
        if (i % 3 == 0)
            index_mod_0 += 1;

        else if (i % 3 == 1)
            index_mod_1 += 1;

        else if (i % 3 == 2)
            index_mod_2 += 1;

        if (arr[i] % 3 == 0)
            array_mod_0 += 1;

        else if (arr[i] % 3 == 1)
            array_mod_1 += 1;

        else if (arr[i] % 3 == 2)
            array_mod_2 += 1;
    }

    // check for base condition.
    if (index_mod_0 != array_mod_0
        || index_mod_1 != array_mod_1
        || index_mod_2 != array_mod_2)
        return -1;

    // count the swaps now.
    for (i = 0; i < n; i++) {

        // If already in right format
        // Then goto next index
        if (i % 3 == arr[i] % 3)
            continue;

        int index_org = i % 3;
        int array_org = arr[i] % 3;

        // Initially set swapped to false
        bool swapped = false;

        for (j = i + 1; j < n; j++) {
            int index_exp = j % 3;
            int array_exp = arr[j] % 3;

            if (index_org == array_exp
                && array_org == index_exp) {
                swapping(arr, i, j);

                // Set swapped to true to make sure
                // any value is swapped
                swapped = true;

                // Increment the count
                count += 1;
                break;
            }
        }

        // Check if element is swapped or not
        if (swapped == false) {
            for (j = i + 1; j < n; j++) {
                int array_exp = arr[j] % 3;
                if (index_org == array_exp) {
                    // Swap indices i and j
                    swapping(arr, i, j);

                    // Increment the count of swaps
                    count += 1;
                    break;
                }
            }
        }
    }

    // Return the final result
    return count;
}

// Driver Code
int main()
{
    int arr[6] = { 4, 3, 5, 2, 9, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int swaps = CountMinSwaps(arr, n);

    cout << swaps << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;

class GFG {

// Function to swap two array elements.
static void swapping(int arr[], int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

// Function to count the Swaps required such that
// for all i in arr[] arr[]% 3 = i % 3
static int CountMinSwaps(int arr[], int n)
{

    // index_mod_i = count of indexes which
    // give i on modulo 3: index%3==i
    int index_mod_0 = 0,
        index_mod_1 = 0,
        index_mod_2 = 0;

    // array_mod_i = count of array elements
    // which give i on modulo 3: arr[i]%3==i
    int array_mod_0 = 0,
        array_mod_1 = 0,
        array_mod_2 = 0;

    int i, j, count = 0;

    for (i = 0; i < n; i++) {
        if (i % 3 == 0)
            index_mod_0 += 1;

        else if (i % 3 == 1)
            index_mod_1 += 1;

        else if (i % 3 == 2)
            index_mod_2 += 1;

        if (arr[i] % 3 == 0)
            array_mod_0 += 1;

        else if (arr[i] % 3 == 1)
            array_mod_1 += 1;

        else if (arr[i] % 3 == 2)
            array_mod_2 += 1;
    }

    // check for base condition.
    if (index_mod_0 != array_mod_0
        || index_mod_1 != array_mod_1
        || index_mod_2 != array_mod_2)
        return -1;

    // count the swaps now.
    for (i = 0; i < n; i++) {

        // If already in right format
        // Then goto next index
        if (i % 3 == arr[i] % 3)
            continue;

        int index_org = i % 3;
        int array_org = arr[i] % 3;

        // Initially set swapped to false
        boolean swapped = false;

        for (j = i + 1; j < n; j++) {
            int index_exp = j % 3;
            int array_exp = arr[j] % 3;

            if (index_org == array_exp
                && array_org == index_exp) {
                swapping(arr, i, j);

                // Set swapped to true to make sure
                // any value is swapped
                swapped = true;

                // Increment the count
                count += 1;
                break;
            }
        }

        // Check if element is swapped or not
        if (swapped == false) {
            for (j = i + 1; j < n; j++) {
                int array_exp = arr[j] % 3;
                if (index_org == array_exp) {
                    // Swap indices i and j
                    swapping(arr, i, j);

                    // Increment the count of swaps
                    count += 1;
                    break;
                }
            }
        }
    }

    // Return the final result
    return count;
}

    public static void main (String[] args) {
      int arr[] = { 4, 3, 5, 2, 9, 7 };
    int n = arr.length;

    int swaps = CountMinSwaps(arr, n);

        System.out.println(swaps );
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python Program for above approach

# Function to swap two array elements.
def swapping(arr, i, j):
    temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp

# Function to count the Swaps required such that
# for all i in arr[] arr[]% 3 = i % 3
def CountMinSwaps(arr, n):

    # index_mod_i = count of indexes which
    # give i on modulo 3: index%3==i
    index_mod_0 = 0
    index_mod_1 = 0
    index_mod_2 = 0

    # array_mod_i = count of array elements
    # which give i on modulo 3: arr[i]%3==i
    array_mod_0 = 0
    array_mod_1 = 0
    array_mod_2 = 0

    count = 0

    for i in range(0, n):
        if (i % 3 == 0):
            index_mod_0 += 1

        elif (i % 3 == 1):
            index_mod_1 += 1

        elif (i % 3 == 2):
            index_mod_2 += 1

        if (arr[i] % 3 == 0):
            array_mod_0 += 1

        elif (arr[i] % 3 == 1):
            array_mod_1 += 1

        elif (arr[i] % 3 == 2):
            array_mod_2 += 1

    # check for base condition.
    if (index_mod_0 != array_mod_0 or index_mod_1 != array_mod_1 or index_mod_2 != array_mod_2):
        return -1

        # count the swaps now.
    for i in range(0, n):

                # If already in right format
                # Then goto next index
        if (i % 3 == arr[i] % 3):
            continue

        index_org = i % 3
        array_org = arr[i] % 3

        # Initially set swapped to false
        swapped = False

        for j in range(i+1, n):
            index_exp = j % 3
            array_exp = arr[j] % 3

            if (index_org == array_exp and array_org == index_exp):
                swapping(arr, i, j)

                # Set swapped to true to make sure
                # any value is swapped
                swapped = True

                # Increment the count
                count += 1
                break

                # Check if element is swapped or not
        if (swapped == False):
            for j in range(i+1, n):
                array_exp = arr[j] % 3
                if (index_org == array_exp):
                                        # Swap indices i and j
                    swapping(arr, i, j)

                    # Increment the count of swaps
                    count += 1
                    break

        # Return the final result
    return count

# Driver Code
if __name__ == "__main__":

    arr = [4, 3, 5, 2, 9, 7]
    n = len(arr)

    swaps = CountMinSwaps(arr, n)
    print(swaps)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# code for the above approach
using System;
class GFG
{

    // Function to swap two array elements.
    static void swapping(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Function to count the Swaps required such that
    // for all i in arr[] arr[]% 3 = i % 3
    static int CountMinSwaps(int[] arr, int n)
    {

        // index_mod_i = count of indexes which
        // give i on modulo 3: index%3==i
        int index_mod_0 = 0,
            index_mod_1 = 0,
            index_mod_2 = 0;

        // array_mod_i = count of array elements
        // which give i on modulo 3: arr[i]%3==i
        int array_mod_0 = 0,
            array_mod_1 = 0,
            array_mod_2 = 0;

        int i, j, count = 0;

        for (i = 0; i < n; i++)
        {
            if (i % 3 == 0)
                index_mod_0 += 1;

            else if (i % 3 == 1)
                index_mod_1 += 1;

            else if (i % 3 == 2)
                index_mod_2 += 1;

            if (arr[i] % 3 == 0)
                array_mod_0 += 1;

            else if (arr[i] % 3 == 1)
                array_mod_1 += 1;

            else if (arr[i] % 3 == 2)
                array_mod_2 += 1;
        }

        // check for base condition.
        if (index_mod_0 != array_mod_0
            || index_mod_1 != array_mod_1
            || index_mod_2 != array_mod_2)
            return -1;

        // count the swaps now.
        for (i = 0; i < n; i++)
        {

            // If already in right format
            // Then goto next index
            if (i % 3 == arr[i] % 3)
                continue;

            int index_org = i % 3;
            int array_org = arr[i] % 3;

            // Initially set swapped to false
            Boolean swapped = false;

            for (j = i + 1; j < n; j++)
            {
                int index_exp = j % 3;
                int array_exp = arr[j] % 3;

                if (index_org == array_exp
                    && array_org == index_exp)
                {
                    swapping(arr, i, j);

                    // Set swapped to true to make sure
                    // any value is swapped
                    swapped = true;

                    // Increment the count
                    count += 1;
                    break;
                }
            }

            // Check if element is swapped or not
            if (swapped == false)
            {
                for (j = i + 1; j < n; j++)
                {
                    int array_exp = arr[j] % 3;
                    if (index_org == array_exp)
                    {
                        // Swap indices i and j
                        swapping(arr, i, j);

                        // Increment the count of swaps
                        count += 1;
                        break;
                    }
                }
            }
        }

        // Return the final result
        return count;
    }

    public static void Main()
    {
        int[] arr = { 4, 3, 5, 2, 9, 7 };
        int n = arr.Length;

        int swaps = CountMinSwaps(arr, n);

        Console.Write(swaps);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
    // JavaScript Program for above approach

    // Function to swap two array elements.
    const swapping = (arr, i, j) => {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Function to count the Swaps required such that
    // for all i in arr[] arr[]% 3 = i % 3
    const CountMinSwaps = (arr, n) => {

        // index_mod_i = count of indexes which
        // give i on modulo 3: index%3==i
        let index_mod_0 = 0,
            index_mod_1 = 0,
            index_mod_2 = 0;

        // array_mod_i = count of array elements
        // which give i on modulo 3: arr[i]%3==i
        let array_mod_0 = 0,
            array_mod_1 = 0,
            array_mod_2 = 0;

        let i, j, count = 0;

        for (i = 0; i < n; i++) {
            if (i % 3 == 0)
                index_mod_0 += 1;

            else if (i % 3 == 1)
                index_mod_1 += 1;

            else if (i % 3 == 2)
                index_mod_2 += 1;

            if (arr[i] % 3 == 0)
                array_mod_0 += 1;

            else if (arr[i] % 3 == 1)
                array_mod_1 += 1;

            else if (arr[i] % 3 == 2)
                array_mod_2 += 1;
        }

        // check for base condition.
        if (index_mod_0 != array_mod_0
            || index_mod_1 != array_mod_1
            || index_mod_2 != array_mod_2)
            return -1;

        // count the swaps now.
        for (i = 0; i < n; i++) {

            // If already in right format
            // Then goto next index
            if (i % 3 == arr[i] % 3)
                continue;

            let index_org = i % 3;
            let array_org = arr[i] % 3;

            // Initially set swapped to false
            let swapped = false;

            for (j = i + 1; j < n; j++) {
                let index_exp = j % 3;
                let array_exp = arr[j] % 3;

                if (index_org == array_exp
                    && array_org == index_exp) {
                    swapping(arr, i, j);

                    // Set swapped to true to make sure
                    // any value is swapped
                    swapped = true;

                    // Increment the count
                    count += 1;
                    break;
                }
            }

            // Check if element is swapped or not
            if (swapped == false) {
                for (j = i + 1; j < n; j++) {
                    let array_exp = arr[j] % 3;
                    if (index_org == array_exp) {
                        // Swap indices i and j
                        swapping(arr, i, j);

                        // Increment the count of swaps
                        count += 1;
                        break;
                    }
                }
            }
        }

        // Return the final result
        return count;
    }

    // Driver Code
    let arr = [4, 3, 5, 2, 9, 7];
    let n = arr.length;
    let swaps = CountMinSwaps(arr, n);
    document.write(swaps);

    // This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N <sup>2</sup> ，其中 N 是 arr[]的大小。

**辅助空间:** O(1)。