# Q 范围查询数组中偶和三元组的计数

> 原文:[https://www . geeksforgeeks . org/q 范围查询数组中的偶和三元组计数/](https://www.geeksforgeeks.org/count-of-even-sum-triplets-in-the-array-for-q-range-queries/)

给定一个大小为 **N** 和 **Q** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】】**，查询的形式为 **(L，R)** ，任务是对每个查询的 **L** 和 **R** 范围内的元素进行**三元组**的计数。

**示例:**

> **输入:** N = 6 **，** arr[ ] = {1，2，3，4，5，6}，Q[ ] = {{1，3}，{2，5}}
> **输出:** 1 2
> **解释:**
> 对于查询(1，3):只有偶和的三元组(1，2，3)存在
> 对于查询(2，5):三元组(2，3，5)和(3，4，5)
> 因此输出分别为 1 和 2
> 
> **输入:** N = 3 **，** arr[ ] = {1，2，5}，Q[ ] = {{1，2 } }
> T5】输出: 0

**方法:**上述问题可以通过以下观察来解决:为了使三重和为偶数，元素必须是以下模式之一:

*   **偶+偶+偶=偶**
*   **奇数+奇数+偶数=偶数**

按照以下步骤解决问题:

*   初始化两个[数组](https://www.geeksforgeeks.org/array-data-structure/)，比如**arr _ 偶数[]** 和**arr _ 奇数[]** 长度**大小+ 1** 。
*   初始化变量，比如**偶数= 0** 和**奇数= 0** ，存储偶数和奇数的计数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个 **i** 在**arr _ 偶数[i]** 中存储偶数直到索引 **i** ，在**arr _ 奇数[i]** 中存储奇数直到索引 **i** 。
*   迭代查询 **Q[]** 和每对查询 **(l，r)** :
    *   将 **(l，r)** 中的偶数计数作为**arr _ 偶数[r]–arr _ 偶数[l-1]** ，将 **(l，r)** 中的奇数计数作为**arr _ 奇数[r]–arr _ 奇数[l-1]。**
    *   在变量 say **和**中找到三元组的计数，作为**(偶数*(偶数-1)*(偶数-2))/6** 和**(奇数*(奇数-1)/2)*偶数的和。**
    *   最后，打印每个查询的**和**。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number of triplets
// with even sum in range l, r for each
// query
void countTriplets(int size, int queries,
                   int arr[], int Q[][2])
{

    // Initialization of array
    int arr_even[size + 1], arr_odd[size + 1];

    // Initialization of variables
    int even = 0, odd = 0;
    arr_even[0] = 0;
    arr_odd[0] = 0;

    // Traversing array
    for (int i = 0; i < size; i++) {

        // If element is odd
        if (arr[i] % 2) {
            odd++;
        }

        // If element is even
        else {
            even++;
        }

        // Storing count of even and odd
        // till each i
        arr_even[i + 1] = even;
        arr_odd[i + 1] = odd;
    }

    // Traversing each query
    for (int i = 0; i < queries; i++) {
        int l = Q[i][0], r = Q[i][1];

        // Count of odd numbers in l to r
        int odd = arr_odd[r] - arr_odd[l - 1];

        // Count of even numbers in l to r
        int even = arr_even[r] - arr_even[l - 1];

        // Finding the ans
        int ans = (even * (even - 1)
                   * (even - 2))
                      / 6
                  + (odd * (odd - 1) / 2)
                        * even;

        // Printing the ans
        cout << ans << " ";
    }
}

// Driver Code
int main()
{
    // Given Input
    int N = 6, Q = 2;
    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int queries[][2] = { { 1, 3 }, { 2, 5 } };

    // Function Call
    countTriplets(N, Q, arr, queries);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {
    // Function to count number of triplets
    // with even sum in range l, r for each
    // query
    static void countTriplets(int size, int queries,
                              int[] arr, int[][] Q)
    {

        // Initialization of array
        int[] arr_even = new int[size + 1];
        int []arr_odd = new int[size + 1];

        // Initialization of variables
        int even = 0;
      int odd = 0;
        arr_even[0] = 0;
        arr_odd[0] = 0;

        // Traversing array
        for (int i = 0; i < size; i++) {

            // If element is odd
            if (arr[i] % 2 == 1) {
                odd++;
            }

            // If element is even
            else {
                even++;
            }

            // Storing count of even and odd
            // till each i
            arr_even[i + 1] = even;
            arr_odd[i + 1] = odd;
        }

        // Traversing each query
        for (int i = 0; i < queries; i++) {
            int l = Q[i][0], r = Q[i][1];

            // Count of odd numbers in l to r
             odd = arr_odd[r] - arr_odd[l - 1];

            // Count of even numbers in l to r
             even = arr_even[r] - arr_even[l - 1];

            // Finding the ans
            int ans = (even * (even - 1) * (even - 2)) / 6
                      + (odd * (odd - 1) / 2) * even;

            // Printing the ans
            System.out.print(ans + " ");
        }
    }

    // Driver Code

    public static void main(String[] args)
    {
        // Given Input
        int N = 6, Q = 2;
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int[][] queries = { { 1, 3 }, { 2, 5 } };
        countTriplets(N, Q, arr, queries);
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python 3 program for above approach

# Function to count number of triplets
# with even sum in range l, r for each
# query
def countTriplets(size, queries, arr, Q):

    # Initialization of array
    arr_even = [0 for i in range(size + 1)]
    arr_odd = [0 for i in range(size + 1)]

    # Initialization of variables
    even = 0
    odd = 0
    arr_even[0] = 0
    arr_odd[0] = 0

    # Traversing array
    for i in range(size):

        # If element is odd
        if (arr[i] % 2):
            odd += 1

        # If element is even
        else:
            even += 1

        # Storing count of even and odd
        # till each i
        arr_even[i + 1] = even
        arr_odd[i + 1] = odd

    # Traversing each query
    for i in range(queries):
        l = Q[i][0]
        r = Q[i][1]

        # Count of odd numbers in l to r
        odd = arr_odd[r] - arr_odd[l - 1]

        # Count of even numbers in l to r
        even = arr_even[r] - arr_even[l - 1]

        # Finding the ans
        ans = (even * (even - 1)*(even - 2)) // 6 + (odd * (odd - 1) // 2)* even

        # Printing the ans
        print(ans,end = " ")

# Driver Code
if __name__ == '__main__':
    # Given Input
    N = 6
    Q = 2
    arr = [1, 2, 3, 4, 5, 6]
    queries = [[1, 3],[2, 5]]

    # Function Call
    countTriplets(N, Q, arr, queries)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for above approach
using System;

class GFG
{

    // Function to count number of triplets
    // with even sum in range l, r for each
    // query
    static void countTriplets(int size, int queries,
                              int[] arr, int[, ] Q)
    {

        // Initialization of array
        int[] arr_even = new int[size + 1];
        int[] arr_odd = new int[size + 1];

        // Initialization of variables
        int even = 0;
        int odd = 0;
        arr_even[0] = 0;
        arr_odd[0] = 0;

        // Traversing array
        for (int i = 0; i < size; i++) {

            // If element is odd
            if (arr[i] % 2 == 1) {
                odd++;
            }

            // If element is even
            else {
                even++;
            }

            // Storing count of even and odd
            // till each i
            arr_even[i + 1] = even;
            arr_odd[i + 1] = odd;
        }

        // Traversing each query
        for (int i = 0; i < queries; i++) {
            int l = Q[i, 0], r = Q[i, 1];

            // Count of odd numbers in l to r
            odd = arr_odd[r] - arr_odd[l - 1];

            // Count of even numbers in l to r
            even = arr_even[r] - arr_even[l - 1];

            // Finding the ans
            int ans = (even * (even - 1) * (even - 2)) / 6
                      + (odd * (odd - 1) / 2) * even;

            // Printing the ans
            Console.Write(ans + " ");
        }
    }

    // Driver Code
    public static void Main()
    {

        // Given Input
        int N = 6, Q = 2;
        int[] arr = { 1, 2, 3, 4, 5, 6 };
        int[, ] queries = { { 1, 3 }, { 2, 5 } };
        countTriplets(N, Q, arr, queries);
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
  <script>
        // JavaScript Program to implement
        // the above approach

    // Function to count number of triplets
    // with even sum in range l, r for each
    // query
    function countTriplets(size, queries, arr, Q)
    {

        // Initialization of array
        let arr_even = new Array(size + 1);
        let arr_odd = new Array(size + 1);

        // Initialization of variables
        let even = 0;
      let odd = 0;
        arr_even[0] = 0;
        arr_odd[0] = 0;

        // Traversing array
        for (let i = 0; i < size; i++) {

            // If element is odd
            if (arr[i] % 2 == 1) {
                odd++;
            }

            // If element is even
            else {
                even++;
            }

            // Storing count of even and odd
            // till each i
            arr_even[i + 1] = even;
            arr_odd[i + 1] = odd;
        }

        // Traversing each query
        for (let i = 0; i < queries; i++) {
            let l = Q[i][0], r = Q[i][1];

            // Count of odd numbers in l to r
             odd = arr_odd[r] - arr_odd[l - 1];

            // Count of even numbers in l to r
             even = arr_even[r] - arr_even[l - 1];

            // Finding the ans
            let ans = (even * (even - 1) * (even - 2)) / 6
                      + (odd * (odd - 1) / 2) * even;

            // Printing the ans
            document.write(ans + " ");
        }
    }

 // Driver Code

      // Given Input
        let N = 6, Q = 2;
        let arr = [ 1, 2, 3, 4, 5, 6 ];
        let queries = [[ 1, 3 ], [ 2, 5 ]];
        countTriplets(N, Q, arr, queries);

// This code is contributed by sanjoy_62.
    </script>
```

**Output:** 

```
1 2
```

***时间复杂度:** O(N*Q)*
***辅助空间:** O(N)*