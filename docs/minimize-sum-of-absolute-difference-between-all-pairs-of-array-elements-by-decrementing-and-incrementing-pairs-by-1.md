# 通过将数组元素对递减和递增 1

来最小化所有数组元素对之间的绝对差之和

> 原文:[https://www . geeksforgeeks . org/将所有数组元素对之间的绝对差之和减 1 加 1/](https://www.geeksforgeeks.org/minimize-sum-of-absolute-difference-between-all-pairs-of-array-elements-by-decrementing-and-incrementing-pairs-by-1/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**(*基于 1 的索引*)，任务是通过将任意一对元素递减和递增 **1** 任意次数来找到所有数组元素对之间绝对差的[最小和。](https://www.geeksforgeeks.org/minimum-sum-absolute-difference-pairs-two-arrays/)

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 0
> **解释:**
> 通过执行以下操作修改数组元素:
> 
> *   选择元素对(arr[1]，arr[3])，增加和减少元素对会将数组修改为{2，2，2}。
> 
> 经过以上运算，绝对差之和为| 2–2 |+| 2–2 |+| 2–2 | = 0。因此，打印 0。
> 
> **输入:** arr[] = {0，1，0，1}
> **输出:** 4

**方法:**给定的问题可以通过使用 [**贪婪方法**](https://www.geeksforgeeks.org/greedy-algorithms/) 来解决。可以观察到，为了最小化每对数组元素之间的绝对差之和 **arr[]** ，使每个数组元素彼此接近的思想。按照以下步骤解决问题:

*   找到数组元素 **arr[]** 的[和，并将其存储在一个变量中，比如**和**。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   现在，如果 **sum % N** 的值是 **0** ，那么打印 **0** ，因为所有的数组元素可以相等，表达式的合成值总是 **0** 。否则，找到 **sum % N** 的值并存储在一个变量中，比如 **R** 。
*   现在，如果所有的数组元素都是**和/N** ，那么我们可以将 **R** 的数组元素个数设为 **1** ，其余的数组元素设为 **0** 来最小化结果值。
*   经过上述步骤后，绝对差的最小和由**R *(N–R)**给出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum value
// of the sum of absolute difference
// between all pairs of arrays
int minSumDifference(int ar[], int n)
{
    // Stores the sum of array elements
    int sum = 0;

    // Find the sum of array element
    for (int i = 0; i < n; i++)
        sum += ar[i];

    // Store the value of sum%N
    int rem = sum % n;

    // Return the resultant value
    return rem * (n - rem);
}

// Driver Code
int main()
{
    int arr[] = { 3, 6, 8, 5, 2,
                  1, 11, 7, 10, 4 };
    int N = sizeof(arr) / sizeof(int);
    cout << minSumDifference(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to find the minimum value
    // of the sum of absolute difference
    // between all pairs of arrays
    public static int minSumDifference(int ar[], int n) {
        // Stores the sum of array elements
        int sum = 0;

        // Find the sum of array element
        for (int i = 0; i < n; i++)
            sum += ar[i];

        // Store the value of sum%N
        int rem = sum % n;

        // Return the resultant value
        return rem * (n - rem);
    }

    // Driver Code
    public static void main(String args[]) {
        int[] arr = { 3, 6, 8, 5, 2, 1, 11, 7, 10, 4 };
        int N = arr.length;
        System.out.println(minSumDifference(arr, N));

    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum value
# of the sum of absolute difference
# between all pairs of arrays
def minSumDifference(ar, n):
    # Stores the sum of array elements
    sum = 0

    # Find the sum of array element
    for i in range(n):
        sum += ar[i]

    # Store the value of sum%N
    rem = sum % n

    # Return the resultant value
    return rem * (n - rem)

# Driver Code
if __name__ == '__main__':
    arr = [3, 6, 8, 5, 2, 1, 11, 7, 10, 4]
    N = len(arr)
    print(minSumDifference(arr, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum value
// of the sum of absolute difference
// between all pairs of arrays
public static int minSumDifference(int[] ar, int n)
{

    // Stores the sum of array elements
    int sum = 0;

    // Find the sum of array element
    for(int i = 0; i < n; i++)
        sum += ar[i];

    // Store the value of sum%N
    int rem = sum % n;

    // Return the resultant value
    return rem * (n - rem);
}

// Driver Code
public static void Main()
{
    int[] arr = { 3, 6, 8, 5, 2,
                  1, 11, 7, 10, 4 };
    int N = arr.Length;

    Console.Write(minSumDifference(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum value
// of the sum of absolute difference
// between all pairs of arrays
function minSumDifference(ar, n) {
  // Stores the sum of array elements
  let sum = 0;

  // Find the sum of array element
  for (let i = 0; i < n; i++) sum += ar[i];

  // Store the value of sum%N
  let rem = sum % n;

  // Return the resultant value
  return rem * (n - rem);
}

// Driver Code

let arr = [3, 6, 8, 5, 2, 1, 11, 7, 10, 4];
let N = arr.length;
document.write(minSumDifference(arr, N));

</script>
```

**Output:** 

```
21
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)