# 数组中的最小增量，这样 arr[i]可以使所有其他元素相等

> 原文:[https://www . geeksforgeeks . org/最小增量-数组中完成-这样 arri-可以使所有其他元素相等/](https://www.geeksforgeeks.org/minimum-increments-done-in-array-such-that-arri-can-make-all-other-elements-equal/)

给定一个 **N** 大小的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到数组中元素所需的**最小**增量，这样如果有任何元素表示 **arr[i]** 分布在其他元素中，则使**N–1**元素相等。

**示例:**

> **输入:** arr[] = {0，0，3}，N = 3
> **输出:** 3
> **说明:**增量可以通过以下方式完成:
> 
> *   将索引 0 处的元素增加 1，因此 arr[]变成{1，0，3}
> *   将索引 1 处的元素增加 2。所以 arr[]变成了{1，2，3}
> 
> 现在，如果任何元素被选择并分布在其他元素中，会使所有 N-1 个元素相等。
> 
> 假设，
> 
> *   选择 1，将其添加到 2，这样 N-1 个元素就变成了{3，3}
> *   选择 2，将其添加到 1，这样 N-1 个元素就变成了{3，3}
> *   选择 3，将 3 中的 2 与 1 相加，将 3 中的 1 与 2 相加，这样 N-1 个元素就变成了{3，3}
> 
> 所以，总增量= (1 + 2) = 3
> 
> **输入:** arr[] = {4，3，1，6}，N = 4
> T3】输出: 4

**方法:**解决这个问题的思路是基于这样的观察:如果 **(N-1)*mx** 其中 **mx** 是数组的[最大元素大于数组](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)的 [**之和**，那么答案就是简单的**(N-1)* MX–sum。**否则，如果 **(N-1)*mx** 小于或等于总和，则取一个临时变量，比如 **temp** ，用**sum/N–1**赋值。如果**总和 mod N -1** 不等于 **0** 将温度增加 **1** ，取一个计数器表示**计数**，其中**计数**是温度与 **mx** 的差值。更新**ans =(count+MX)*(N–1)**并按计数递增总和。如果**和**等于 **(N-1)*mx** 返回**计数**，否则返回计数按 **(N-1)*mx** 和**和**之差递增。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   初始化变量 **mx** 和 **sum** 为 **0** ，求数组的和和最大元素。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N)** ，并执行以下任务:
    *   将 **mx** 的值更新为 **mx** 或**arr【I】**的最大值，并将**arr【I】**的值加到变量**和中。**
*   将变量**和**初始化为 **(N-1)*mx。**
*   如果 **ans** 大于**总和**，则返回**ans-总和**作为答案。
*   否则，将变量**温度**初始化为**和/(N-1) +和%(N-1)。**
*   将变量**计数**初始化为**温度–MX**。
*   将**和**的值设置为**(计数+ mx)*(N-1)。**
*   将**计数**的值加到变量**的和上。**
*   如果**和**等于 **ans，**则返回**计数的值**作为答案，否则返回**计数+ans–和。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum increment
// required to an element to make N-1
// elements equal by distributing
// any element
int minIncrement(int arr[], int N)
{
    // Variable for max element
    // and sum
    int mx = 0, sum = 0;
    for (int i = 0; i < N; i++) {
        mx = max(mx, arr[i]);
        sum += arr[i];
    }

    // Calculate ans
    int ans = (N - 1) * mx;

    // If ans is greater than sum
    // return its difference
    if (ans > sum) {
        return (ans - sum);
    }

    // If ans is less or equal to sum
    else {
        int temp = sum / (N - 1);
        if (sum % (N - 1) != 0) {
            temp++;
        }
        int count = temp - mx;
        ans = (count + mx) * (N - 1);
        sum += count;

        // If sum is equal to ans
        // return the count
        if (sum == ans) {
            return count;
        }

        // Else return the summation
        // of count and difference
        // of ans and sum
        else {
            return (count + (ans - sum));
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 3, 1, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minIncrement(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find minimum increment
// required to an element to make N-1
// elements equal by distributing
// any element
static int minIncrement(int arr[], int N)
{

    // Variable for max element
    // and sum
    int mx = 0, sum = 0;
    for (int i = 0; i < N; i++) {
        mx = Math.max(mx, arr[i]);
        sum += arr[i];
    }

    // Calculate ans
    int ans = (N - 1) * mx;

    // If ans is greater than sum
    // return its difference
    if (ans > sum) {
        return (ans - sum);
    }

    // If ans is less or equal to sum
    else {
        int temp = sum / (N - 1);
        if (sum % (N - 1) != 0) {
            temp++;
        }
        int count = temp - mx;
        ans = (count + mx) * (N - 1);
        sum += count;

        // If sum is equal to ans
        // return the count
        if (sum == ans) {
            return count;
        }

        // Else return the summation
        // of count and difference
        // of ans and sum
        else {
            return (count + (ans - sum));
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 3, 1, 6 };
    int N = arr.length;

    System.out.print(minIncrement(arr, N));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find minimum increment
# required to an element to make N-1
# elements equal by distributing
# any element
def minIncrement(arr, N):

        # Variable for max element
        # and sum
    mx = 0
    sum = 0
    for i in range(0, N):
        mx = max(mx, arr[i])
        sum += arr[i]

        # Calculate ans
    ans = (N - 1) * mx

    # If ans is greater than sum
    # return its difference
    if (ans > sum):
        return (ans - sum)

        # If ans is less or equal to sum
    else:
        temp = sum // (N - 1)
        if (sum % (N - 1) != 0):
            temp += 1

        count = temp - mx
        ans = (count + mx) * (N - 1)
        sum += count

        # If sum is equal to ans
        # return the count
        if (sum == ans):
            return count

            # Else return the summation
            # of count and difference
            # of ans and sum
        else:
            return (count + (ans - sum))

# Driver Code
if __name__ == "__main__":

    arr = [4, 3, 1, 6]
    N = len(arr)

    print(minIncrement(arr, N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG {

// Function to find minimum increment
// required to an element to make N-1
// elements equal by distributing
// any element
static int minIncrement(int []arr, int N)
{

    // Variable for max element
    // and sum
    int mx = 0, sum = 0;
    for (int i = 0; i < N; i++) {
        mx = Math.Max(mx, arr[i]);
        sum += arr[i];
    }

    // Calculate ans
    int ans = (N - 1) * mx;

    // If ans is greater than sum
    // return its difference
    if (ans > sum) {
        return (ans - sum);
    }

    // If ans is less or equal to sum
    else {
        int temp = sum / (N - 1);
        if (sum % (N - 1) != 0) {
            temp++;
        }
        int count = temp - mx;
        ans = (count + mx) * (N - 1);
        sum += count;

        // If sum is equal to ans
        // return the count
        if (sum == ans) {
            return count;
        }

        // Else return the summation
        // of count and difference
        // of ans and sum
        else {
            return (count + (ans - sum));
        }
    }
}

// Driver Code
public static void Main()
{
    int []arr = { 4, 3, 1, 6 };
    int N = arr.Length;

    Console.Write(minIncrement(arr, N));

}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to find minimum increment
        // required to an element to make N-1
        // elements equal by distributing
        // any element
        function minIncrement(arr, N)
        {

            // Variable for max element
            // and sum
            let mx = 0, sum = 0;
            for (let i = 0; i < N; i++) {
                mx = Math.max(mx, arr[i]);
                sum += arr[i];
            }

            // Calculate ans
            let ans = (N - 1) * mx;

            // If ans is greater than sum
            // return its difference
            if (ans > sum) {
                return (ans - sum);
            }

            // If ans is less or equal to sum
            else {
                let temp = sum / (N - 1);
                if (sum % (N - 1) != 0) {
                    temp++;
                }
                let count = temp - mx;
                ans = (count + mx) * (N - 1);
                sum += count;

                // If sum is equal to ans
                // return the count
                if (sum == ans) {
                    return count;
                }

                // Else return the summation
                // of count and difference
                // of ans and sum
                else {
                    return (count + (ans - sum));
                }
            }
        }

        // Driver Code
        let arr = [4, 3, 1, 6];
        let N = arr.length;

        document.write(minIncrement(arr, N));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)