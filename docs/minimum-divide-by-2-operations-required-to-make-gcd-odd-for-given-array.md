# 给定数组使 GCD 为奇数所需的最小除以 2 运算

> 原文:[https://www . geesforgeks . org/最小二乘运算-给定数组需要生成 gcd-奇数/](https://www.geeksforgeeks.org/minimum-divide-by-2-operations-required-to-make-gcd-odd-for-given-array/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到使数组元素的 [GCD 为奇数所需的最小操作数，这样在每个操作中，一个数组元素可以除以 **2** 。](https://www.geeksforgeeks.org/gcd-two-array-numbers/)

**示例:**

> **输入:** arr[] = {4，6}
> **输出:** 1
> **解释:**
> 下面是执行的操作:
> **操作 1:** 将数组元素 arr[0](= 4)除以 2 将数组修改为{2，6}。
> **操作 2:** 将数组元素 arr[0](= 2)除以 2 会将数组修改为{1，6}。
> 经过上述运算后，数组元素的 GCD 为 1，为奇数。因此，所需的最小操作数是 2。
> 
> **输入:** arr[] = {2，4，1 }
> T3】输出: 0

**方法:**给定的问题可以基于[的观察来解决，对于每个数组元素找到 2](https://www.geeksforgeeks.org/highest-power-2-less-equal-given-number/) 的幂的计数和 2 的最小[幂(比如说 **C** )将给出最小的运算，因为在将该元素除以 **2 <sup>C</sup>** 之后，该元素变成奇数，这导致数组](https://www.geeksforgeeks.org/program-to-find-whether-a-no-is-power-of-two/)的 [GCD 为](https://www.geeksforgeeks.org/gcd-two-array-numbers/) [**奇数**](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/) 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations to make the GCD of
// the array odd
int minimumOperations(int arr[], int N)
{
    // Stores the minimum operations
    // required
    int mini = INT_MAX;

    for (int i = 0; i < N; i++) {

        // Stores the powers of two for
        // the current array element
        int count = 0;

        // Dividing by 2
        while (arr[i] % 2 == 0) {
            arr[i] = arr[i] / 2;

            // Increment the count
            count++;
        }

        // Update the minimum operation
        // required
        if (mini > count) {
            mini = count;
        }
    }

    // Return the result required
    return mini;
}

// Driver Code
int main()
{
    int arr[] = { 4, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minimumOperations(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to find the minimum number
// of operations to make the GCD of
// the array odd
public static int minimumOperations(int arr[], int N)
{

    // Stores the minimum operations
    // required
    int mini = Integer.MAX_VALUE;

    for (int i = 0; i < N; i++) {

        // Stores the powers of two for
        // the current array element
        int count = 0;

        // Dividing by 2
        while (arr[i] % 2 == 0) {
            arr[i] = arr[i] / 2;

            // Increment the count
            count++;
        }

        // Update the minimum operation
        // required
        if (mini > count) {
            mini = count;
        }
    }

    // Return the result required
    return mini;
}

// Driver Code
public static void  main(String args[])
{
    int arr[] = { 4, 6 };
    int N = arr.length;

    System.out.println(minimumOperations(arr, N));

}
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for the above approac
INT_MAX = 2147483647

# Function to find the minimum number
# of operations to make the GCD of
# the array odd
def minimumOperations(arr, N):

    # Stores the minimum operations
    # required
    mini = INT_MAX

    for i in range(0, N):

        # Stores the powers of two for
        # the current array element
        count = 0

        # Dividing by 2
        while (arr[i] % 2 == 0):
            arr[i] = arr[i] // 2

            # Increment the count
            count += 1

        # Update the minimum operation
        # required
        if (mini > count):
            mini = count

    # Return the result required
    return mini

# Driver Code
if __name__ == "__main__":

    arr = [4, 6]
    N = len(arr)

    print(minimumOperations(arr, N))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to find the minimum number
    // of operations to make the GCD of
    // the array odd
    public static int minimumOperations(int[] arr, int N)
    {

        // Stores the minimum operations
        // required
        int mini = Int32.MaxValue;

        for (int i = 0; i < N; i++) {

            // Stores the powers of two for
            // the current array element
            int count = 0;

            // Dividing by 2
            while (arr[i] % 2 == 0) {
                arr[i] = arr[i] / 2;

                // Increment the count
                count++;
            }

            // Update the minimum operation
            // required
            if (mini > count) {
                mini = count;
            }
        }

        // Return the result required
        return mini;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int[] arr = { 4, 6 };
        int N = arr.Length;

        Console.WriteLine(minimumOperations(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum number
// of operations to make the GCD of
// the array odd
function minimumOperations(arr, N)
{

  // Stores the minimum operations
  // required
  let mini = Number.MAX_SAFE_INTEGER;

  for (let i = 0; i < N; i++)
  {

    // Stores the powers of two for
    // the current array element
    let count = 0;

    // Dividing by 2
    while (arr[i] % 2 == 0) {
      arr[i] = Math.floor(arr[i] / 2);

      // Increment the count
      count++;
    }

    // Update the minimum operation
    // required
    if (mini > count) {
      mini = count;
    }
  }

  // Return the result required
  return mini;
}

// Driver Code

let arr = [4, 6];
let N = arr.length;

document.write(minimumOperations(arr, N));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*