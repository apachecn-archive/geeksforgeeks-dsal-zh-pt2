# 通过在每第 I 次运算中将 2^i 加到一个子集来使数组不减少所需的最小运算次数

> 原文:[https://www . geeksforgeeks . org/最小操作数-制作阵列所需的操作数-每 I 次操作中向子集添加 2i 非递减/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-make-an-array-non-decreasing-by-adding-2i-to-a-subset-in-every-i-th-operation/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】**，任务是通过选择数组**arr【】**的任意[子集，并在 **i <sup>th</sup>** 步骤中将 **2 <sup>i</sup>** 添加到子集的所有元素中，找到使数组不递减所需的最小操作数。](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)

**示例:**

> **输入:** arr[ ] = {1，7，6，5}
> **输出:** 2
> **解释:**
> 使数组不递减的一种方法是:
> 
> 1.  将 arr[1]和 arr[3]增加 2 <sup>0</sup> 。此后，数组修改为{2，7，6，6}。
> 2.  将 arr[2]和 arr[3]增加 2 <sup>1</sup> 。此后，数组修改为{2，7，8，8}。
> 
> 因此，需要两个操作来使数组不递减。此外，这是最小操作数。
> 
> **输入:** arr[ ] = {1，2，3，4，5}
> **输出:** 0

**方法:**给定的问题可以基于以下观察来解决:

> 假设 **A[]** 为原阵， **B[]** 为终阵，那么:
> 
> 1.  只有一种方法可以得到最终的非递减数组，因为只有一种方法可以对一个数进行特定的加法运算。因此，任务将是最小化**最大值(B1-A1**、**B<sub>2</sub>A<sub>2</sub>、…、B<sub>n</sub>A<sub>n</sub>)**，因为较小的差异导致使用较短的时间使阵列不递减。
> 2.  当 **B[i]** 是 **B <sub>1</sub> 、B <sub>2</sub> 、…、B[I]1**和 **A[i]** 之间的最大值时，B[] 是最佳的，因为对于每个位置 **i** 、**B[I]—A[I]**应该尽可能小，而 **B[i-1] ≤ B[i]**
> 3.  如果执行 **X** 运算，则任意数组元素可以增加**【0，2 <sup>X</sup> -1】范围内的任意整数。**

按照以下步骤解决问题:

*   初始化一个变量，比如说**值**为 **0** ，在相同的索引下存储最终数组元素和原始数组元素之间的**最大**差值。
*   初始化另一个变量，比如说 **mx** 为 **INT_MIN，**来存储数组前缀的**最大值**。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，arr【】，在每次迭代中更新 **mx** 到 **max(mx，arr[i])** 和 **val** 到 **max(val，MX–arr[I])**。
*   [2 的最高次方，小于整数](https://www.geeksforgeeks.org/highest-power-of-2-less-than-or-equal-to-given-integer/)、 **val、**然后存储在变量中，比如说 **res** 。
*   最后，完成以上步骤后，打印 **res** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of steps required to make arr non-
// decreasing
int countMinSteps(int arr[], int N)
{
    // Stores differences
    int val = 0;

    // Stores the max number
    int mx = INT_MIN;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        int curr = arr[i];

        // Update mx
        mx = max(mx, curr);

        // Update val
        val = max(val, mx - curr);
    }

    // Stores the result
    long long res = 0;

    // Iterate until 2^res-1 is less
    // than val
    while ((1LL << res) - 1 < val) {
        ++res;
    }

    // Return the answer
    return res;
}

// Driver Code
int main()
{
    // Given input
    int arr[] = { 1, 7, 6, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << countMinSteps(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to count the minimum number
    // of steps required to make arr non-
    // decreasing
    static int countMinSteps(int arr[], int N)
    {

        // Stores differences
        int val = 0;

        // Stores the max number
        int mx = Integer.MIN_VALUE;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            int curr = arr[i];

            // Update mx
            mx = Math.max(mx, curr);

            // Update val
            val = Math.max(val, mx - curr);
        }

        // Stores the result
        long res = 0;

        // Iterate until 2^res-1 is less
        // than val
        while ((1 << res) - 1 < val) {
            ++res;
        }

        // Return the answer
        return (int)res;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given input
        int arr[] = { 1, 7, 6, 5 };
        int N = arr.length;

        // Function call
        System.out.println(countMinSteps(arr, N));

    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum number
# of steps required to make arr non-
# decreasing
def countMinSteps(arr, N):

    # Stores differences
    val = 0

    # Stores the max number
    mx = -10**9

    # Traverse the array arr[]
    for i in range(N):
        curr = arr[i]

        # Update mx
        mx = max(mx, curr)

        # Update val
        val = max(val, mx - curr)

    # Stores the result
    res = 0

    # Iterate until 2^res-1 is less
    # than val
    while ((1 << res) - 1 < val):
        res += 1

    # Return the answer
    return res

# Driver Code
if __name__ == '__main__':

    # Given input
    arr = [ 1, 7, 6, 5 ]
    N = len(arr)

    # Function call
    print(countMinSteps(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the minimum number
// of steps required to make arr non-
// decreasing
static int countMinSteps(int []arr, int N)
{
    // Stores differences
    int val = 0;

    // Stores the max number
    int mx = Int32.MinValue;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        int curr = arr[i];

        // Update mx
        mx = Math.Max(mx, curr);

        // Update val
        val = Math.Max(val, mx - curr);
    }

    // Stores the result
    int res = 0;

    // Iterate until 2^res-1 is less
    // than val
    while ((1 << res) - 1 < val) {
        ++res;
    }

    // Return the answer
    return res;
}

// Driver Code
public static void Main()
{
    // Given input
    int []arr = { 1, 7, 6, 5 };
    int N = arr.Length;

    // Function call
    Console.Write(countMinSteps(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the minimum number
// of steps required to make arr non-
// decreasing
function countMinSteps(arr, N) {
    // Stores differences
    let val = 0;

    // Stores the max number
    let mx = Number.MIN_SAFE_INTEGER;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {

        let curr = arr[i];

        // Update mx
        mx = Math.max(mx, curr);

        // Update val
        val = Math.max(val, mx - curr);
    }

    // Stores the result
    let res = 0;

    // Iterate until 2^res-1 is less
    // than val
    while ((1 << res) - 1 < val) {
        ++res;
    }

    // Return the answer
    return res;
}

// Driver Code

// Given input
let arr = [1, 7, 6, 5];
let N = arr.length;

// Function call

document.write(countMinSteps(arr, N));

</script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)