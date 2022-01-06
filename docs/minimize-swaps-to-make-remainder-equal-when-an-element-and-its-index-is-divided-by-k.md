# 当一个元素及其索引除以 K 时，最小化交换以使余数相等

> 原文:[https://www . geesforgeks . org/当一个元素及其索引被 k 除时，最小化交换使余数相等/](https://www.geeksforgeeks.org/minimize-swaps-to-make-remainder-equal-when-an-element-and-its-index-is-divided-by-k/)

给定一个正整数的[数组](https://www.geeksforgeeks.org/array-class-c/)**arr【】**和一个正数 **K，**的任务是找到所需元素的最小交换，使得对于索引 **i，**处的每个元素，以下条件成立:

> **arr[i] % K = i % K**

**示例:**

> **输入:** arr = {4，3，5，2，9，7}，K=3
> **输出:** 3
> **解释:**指数% 3 = 0 1 2 0 1 2 和 arr[I]% 3 = 1 0 2 0 1
> 用指数 1 交换指数 0 =>0 1 2 0 1
> 用指数 4 =>0 1 2 0 2
> 用指数 5 =
> 交换指数 3
> 
> **输入:** arr = {0，1，2，3，4，5}，K = 1
> T3】输出: 0

**方法:**给定的问题可以用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。其思想是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并进行交换，使得两个元素在可能的情况下被带到它们的精确位置，否则正确的元素被带到当前位置。可以遵循以下步骤来解决问题:

*   通过比较**指数% k** 和**元素% k** 的频率，检查是否有可能完成任务
    *   如果频率不匹配，则返回-1
*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，在每个索引 **i** :
    *   如果 **arr[i] % 3 == i % 3** 则继续下一个索引
    *   否则如果 **arr[i] % 3！= i % 3** 然后找到从 **i+1** 到 **N-1、**的索引 **j** ，其中 **i % 3 = arr[j] % 3** 和 **j % 3 = arr[i] % 3** 将两个元素带到它们的精确位置
    *   否则，通过从 **i+1** 迭代到 **N-1、**找到索引 **k、**，其中 **i % 3 = arr[k] % 3、**并交换元素

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <iostream>
using namespace std;

// Function to swap the values
void swapping(int arr[], int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}

// Function to find the minimum swaps
// required such that arr[i] % k = i % k
int CountMinSwaps(int arr[], int N, int K)
{

    // initialize matrix with 0 values
    int mat[K][2] = { 0 };

    int i, j, count = 0;

    for (i = 0; i < N; i++) {

        // Count the frequency of
        // index % k
        mat[i % K][0] += 1;

        // Count the frequency of
        // index % k
        mat[arr[i] % K][1] += 1;
    }

    // If the count of indexes % k and
    // array elements % K are not same
    // then the task is not possible
    // therefore return -1
    for (i = 0; i < K; i++) {

        if (mat[i][0] != mat[i][1])
            return -1;
    }

    // Count the swaps
    for (i = 0; i < N; i++) {

        // If condition is already true
        // move to the next index
        if (i % K == arr[i] % K)
            continue;

        // Current index remainder
        int ind = i % K;

        // Current element remainder
        int ele = arr[i] % K;

        // Boolean variable to indicate
        // if the swap was made with the
        // element such that both the swapped
        // elements would be at correct place
        bool swapped = false;

        // Search for the element from
        // i + 1 till end of the array
        for (j = i + 1; j < N; j++) {

            // Expected index remainder
            int ind_exp = j % K;

            // Expected element remainder
            int ele_exp = arr[j] % K;

            if (ind == ele_exp
                && ele == ind_exp) {

                // Swap the element if found
                swapping(arr, i, j);

                // Update the boolean
                // variable swap to true
                swapped = true;

                // Increment count of swaps
                count++;

                break;
            }
        }

        // If the swap didnt take place
        if (swapped == false) {

            // Iterate from i+1 till end and
            // find the accurate element for
            // the current index
            for (j = i + 1; j < N; j++) {

                // Expected element remainder
                int ele_exp = arr[j] % K;

                if (ind == ele_exp) {

                    // Swap after finding
                    // the element
                    swapping(arr, i, j);

                    // Increment the count
                    count++;

                    break;
                }
            }
        }
    }

    // Return the result
    return count;
}

// Driver code
int main()
{

    int arr[6] = { 0, 1, 2, 3, 4, 5 };
    int K = 1;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Call the function
    int swaps = CountMinSwaps(arr, N, K);

    // Print the answer
    cout << swaps << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
public class GFG {

    // Function to swap the values
    static void swapping(int arr[], int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Function to find the minimum swaps
    // required such that arr[i] % k = i % k
    static int CountMinSwaps(int arr[], int N, int K)
    {

        // initialize matrix with 0 values
        int mat[][] = new int[K][2] ;
        int i, j, count = 0;

        for (i = 0; i < N; i++) {

            // Count the frequency of
            // index % k
            mat[i % K][0] += 1;

            // Count the frequency of
            // index % k
            mat[arr[i] % K][1] += 1;
        }

        // If the count of indexes % k and
        // array elements % K are not same
        // then the task is not possible
        // therefore return -1
        for (i = 0; i < K; i++) {

            if (mat[i][0] != mat[i][1])
                return -1;
        }

        // Count the swaps
        for (i = 0; i < N; i++) {

            // If condition is already true
            // move to the next index
            if (i % K == arr[i] % K)
                continue;

            // Current index remainder
            int ind = i % K;

            // Current element remainder
            int ele = arr[i] % K;

            // Boolean variable to indicate
            // if the swap was made with the
            // element such that both the swapped
            // elements would be at correct place
            boolean swapped = false;

            // Search for the element from
            // i + 1 till end of the array
            for (j = i + 1; j < N; j++) {

                // Expected index remainder
                int ind_exp = j % K;

                // Expected element remainder
                int ele_exp = arr[j] % K;

                if (ind == ele_exp
                    && ele == ind_exp) {

                    // Swap the element if found
                    swapping(arr, i, j);

                    // Update the boolean
                    // variable swap to true
                    swapped = true;

                    // Increment count of swaps
                    count++;

                    break;
                }
            }

            // If the swap didnt take place
            if (swapped == false) {

                // Iterate from i+1 till end and
                // find the accurate element for
                // the current index
                for (j = i + 1; j < N; j++) {

                    // Expected element remainder
                    int ele_exp = arr[j] % K;

                    if (ind == ele_exp) {

                        // Swap after finding
                        // the element
                        swapping(arr, i, j);

                        // Increment the count
                        count++;

                        break;
                    }
                }
            }
        }

        // Return the result
        return count;
    }

    // Driver code
    public static void main (String[] args)
    {

        int arr[] = { 0, 1, 2, 3, 4, 5 };
        int K = 1;
        int N = arr.length;

        // Call the function
        int swaps = CountMinSwaps(arr, N, K);

        // Print the answer
        System.out.println(swaps);
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python implementation for the above approach

# Function to swap the values
def swapping(arr, i, j):

    temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp

# Function to find the minimum swaps
# required such that arr[i] % k = i % k
def CountMinSwaps(arr, N, K):

    # initialize matrix with 0 values
    mat = [[0 for _ in range(2)] for _ in range(K)]

    count = 0

    for i in range(0, N):

        # Count the frequency of
        # index % k
        mat[i % K][0] += 1

        # Count the frequency of
        # index % k
        mat[arr[i] % K][1] += 1

    # If the count of indexes % k and
    # array elements % K are not same
    # then the task is not possible
    # therefore return -1
    for i in range(0, K):

        if (mat[i][0] != mat[i][1]):
            return -1

    # Count the swaps
    for i in range(0, N):

        # If condition is already true
        # move to the next index
        if (i % K == arr[i] % K):
            continue

        # Current index remainder
        ind = i % K

        # Current element remainder
        ele = arr[i] % K

        # Boolean variable to indicate
        # if the swap was made with the
        # element such that both the swapped
        # elements would be at correct place
        swapped = False

        # Search for the element from
        # i + 1 till end of the array
        for j in range(i+1, N):

            # Expected index remainder
            ind_exp = j % K

            # Expected element remainder
            ele_exp = arr[j] % K

            if (ind == ele_exp and ele == ind_exp):

                # Swap the element if found
                swapping(arr, i, j)

                # Update the boolean
                # variable swap to true
                swapped = True

                # Increment count of swaps
                count += 1

                break

        # If the swap didnt take place
        if (swapped == False):

            # Iterate from i+1 till end and
            # find the accurate element for
            # the current index
            for j in range(i+1, N):

                # Expected element remainder
                ele_exp = arr[j] % K

                if (ind == ele_exp):

                    # Swap after finding
                    # the element
                    swapping(arr, i, j)

                    # Increment the count
                    count += 1

                    break

    # Return the result
    return count

# Driver code
if __name__ == "__main__":

    arr = [0, 1, 2, 3, 4, 5]
    K = 1
    N = len(arr)

    # Call the function
    swaps = CountMinSwaps(arr, N, K)

    # Print the answer
    print(swaps)

# This code is contributed by rakeshsahni
```

## C#

```
// C# implementation for the above approach

using System;

public class GFG
{

    // Function to swap the values
    static void swapping(int[] arr, int i, int j)
    {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    // Function to find the minimum swaps
    // required such that arr[i] % k = i % k
    static int CountMinSwaps(int[] arr, int N, int K)
    {

        // initialize matrix with 0 values
        int[,] mat = new int[K, 2];
        int i, j, count = 0;

        for (i = 0; i < N; i++)
        {

            // Count the frequency of
            // index % k
            mat[i % K, 0] += 1;

            // Count the frequency of
            // index % k
            mat[arr[i] % K, 1] += 1;
        }

        // If the count of indexes % k and
        // array elements % K are not same
        // then the task is not possible
        // therefore return -1
        for (i = 0; i < K; i++)
        {

            if (mat[i, 0] != mat[i, 1])
                return -1;
        }

        // Count the swaps
        for (i = 0; i < N; i++)
        {

            // If condition is already true
            // move to the next index
            if (i % K == arr[i] % K)
                continue;

            // Current index remainder
            int ind = i % K;

            // Current element remainder
            int ele = arr[i] % K;

            // Boolean variable to indicate
            // if the swap was made with the
            // element such that both the swapped
            // elements would be at correct place
            bool swapped = false;

            // Search for the element from
            // i + 1 till end of the array
            for (j = i + 1; j < N; j++)
            {

                // Expected index remainder
                int ind_exp = j % K;

                // Expected element remainder
                int ele_exp = arr[j] % K;

                if (ind == ele_exp
                    && ele == ind_exp)
                {

                    // Swap the element if found
                    swapping(arr, i, j);

                    // Update the boolean
                    // variable swap to true
                    swapped = true;

                    // Increment count of swaps
                    count++;

                    break;
                }
            }

            // If the swap didnt take place
            if (swapped == false)
            {

                // Iterate from i+1 till end and
                // find the accurate element for
                // the current index
                for (j = i + 1; j < N; j++)
                {

                    // Expected element remainder
                    int ele_exp = arr[j] % K;

                    if (ind == ele_exp)
                    {

                        // Swap after finding
                        // the element
                        swapping(arr, i, j);

                        // Increment the count
                        count++;

                        break;
                    }
                }
            }
        }

        // Return the result
        return count;
    }

    // Driver code
    public static void Main()
    {

        int[] arr = { 0, 1, 2, 3, 4, 5 };
        int K = 1;
        int N = arr.Length;

        // Call the function
        int swaps = CountMinSwaps(arr, N, K);

        // Print the answer
        Console.Write(swaps);
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to swap the values
        function swapping(arr, i, j) {
            let temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }

        // Function to find the minimum swaps
        // required such that arr[i] % k = i % k
        function CountMinSwaps(arr, N, K) {

            // initialize matrix with 0 values
            let mat = new Array(K);

            for (let i = 0; i < mat.length; i++) {
                mat[i] = new Array(2).fill(0);
            }

            let i, j, count = 0;

            for (i = 0; i < N; i++) {

                // Count the frequency of
                // index % k
                mat[i % K][0] += 1;

                // Count the frequency of
                // index % k
                mat[arr[i] % K][1] += 1;
            }

            // If the count of indexes % k and
            // array elements % K are not same
            // then the task is not possible
            // therefore return -1
            for (i = 0; i < K; i++) {

                if (mat[i][0] != mat[i][1])
                    return -1;
            }

            // Count the swaps
            for (i = 0; i < N; i++) {

                // If condition is already true
                // move to the next index
                if (i % K == arr[i] % K)
                    continue;

                // Current index remainder
                let ind = i % K;

                // Current element remainder
                let ele = arr[i] % K;

                // Boolean variable to indicate
                // if the swap was made with the
                // element such that both the swapped
                // elements would be at correct place
                let swapped = false;

                // Search for the element from
                // i + 1 till end of the array
                for (j = i + 1; j < N; j++) {

                    // Expected index remainder
                    let ind_exp = j % K;

                    // Expected element remainder
                    let ele_exp = arr[j] % K;

                    if (ind == ele_exp
                        && ele == ind_exp) {

                        // Swap the element if found
                        swapping(arr, i, j);

                        // Update the boolean
                        // variable swap to true
                        swapped = true;

                        // Increment count of swaps
                        count++;

                        break;
                    }
                }

                // If the swap didnt take place
                if (swapped == false) {

                    // Iterate from i+1 till end and
                    // find the accurate element for
                    // the current index
                    for (j = i + 1; j < N; j++) {

                        // Expected element remainder
                        let ele_exp = arr[j] % K;

                        if (ind == ele_exp) {

                            // Swap after finding
                            // the element
                            swapping(arr, i, j);

                            // Increment the count
                            count++;

                            break;
                        }
                    }
                }
            }

            // Return the result
            return count;
        }

        // Driver code

        let arr = [0, 1, 2, 3, 4, 5];
        let K = 1;
        let N = arr.length;

        // Call the function
        let swaps = CountMinSwaps(arr, N, K);

        // Print the answer
        document.write(swaps + '<br>');

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
0
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(2 * K)