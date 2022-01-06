# 将绝对指数差与 K 的乘积最大化

> 原文:[https://www . geeksforgeeks . org/最大化绝对指数与 k 之差/](https://www.geeksforgeeks.org/maximize-product-of-absolute-index-difference-with-k/)

给定一个由 **N** 整数组成的数组**A【】**，任务是找出 **K** 的最大可能值，使得**K * | I–j |<= min(A<sub>I</sub>，A <sub>j</sub> )** ，其中(0？i < j < N。

> 给定表达式，**k * | I–j |<= min(A<sub>I</sub>、A <sub>j</sub> )** 也可以写成 **k = floor( min(A <sub>i</sub> 、A<sub>j</sub>)/| I–j |)**

**示例:**

> **输入:** N = 5，A[ ] = {80，10，12，15，90}
> **输出:** 20
> **说明:**
> 对于 i = 0 和 j = 4，可以得到 K 的最大可能值。
> 最大 k =最小值(A[0]，A[4])/| 0–4 | =最小值(80，90) / |-4| = 80/4 = 20
> 
> **输入:** N = 5，A[ ] = {10，5，12，15，8}
> **输出:** 12
> **说明:**
> 对于 i = 2，j = 3，可以得到 K 的最大可能值。
> 最大 k =最小值(A[2]，A[3])/| 2–3 | =最小值(12，15) / |-1| = 12/1 = 12

**天真法:**
解决这个问题最简单的方法就是[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，对于每一对，找到 K 的值并不断更新得到的最大值 **K** 。最后打印得到的 **K** 的最大值。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效进场:**
要优化上述进场，使用[两点](https://www.geeksforgeeks.org/two-pointers-technique/)手法。遵循以下步骤:

*   初始化三个变量 **i** 、 **j** 和 **k** 。初始设置 **i = 0** 和 **k = 0** 。
*   迭代数组，从 **j = 1** 到 **j = N-1** 开始。
*   现在，对于每对 **A[i]** 和 **A[j]** ，找到 **min(A[i]，A[j])/(j–I)。**如果大于 **K** ，则更新 **K** 。
*   如果**A[j]>= A[I]/(j–I)**，则将指针 **i** 更新为 **j** ，以确保在所有达到 **i** 的元素中， **A[i]** 将产生最大值 **K** 以及所有即将到来的 **A[j]**
*   最后，遍历完数组后，打印 **K** 的最大值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function returns maximum
// possible value of k
int solve(int A[], int N)
{

    // Pointer i make sure that
    // A[i] will result in max k
    int i = 0;

    // Stores maximum possible k
    int k = 0;

    for (int j = 1; j < N; j++) {

        // Possible value of k for
        // current pair (A[i] and A[j])
        int tempK = min(A[i], A[j])
                    / (j - i);

        // If current value exceeds k
        if (tempK > k) {
            // Update the value of k
            k = tempK;
        }

        // Update pointer i
        if (A[j] >= A[i] / (j - i))
            i = j;
    }

    // Return the maxm possible k
    return k;
}

// Driver Code
int main()
{
    int A[] = { 10, 5, 12, 15, 8 };

    int N = sizeof(A) / sizeof(A[0]);

    cout << solve(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function returns maximum
// possible value of k
static int solve(int A[], int N)
{

    // Pointer i make sure that
    // A[i] will result in max k
    int i = 0;

    // Stores maximum possible k
    int k = 0;

    for(int j = 1; j < N; j++)
    {

        // Possible value of k for
        // current pair (A[i] and A[j])
        int tempK = Math.min(A[i], A[j]) /
                              (j - i);

        // If current value exceeds k
        if (tempK > k)
        {

            // Update the value of k
            k = tempK;
        }

        // Update pointer i
        if (A[j] >= A[i] / (j - i))
            i = j;
    }

    // Return the maxm possible k
    return k;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 10, 5, 12, 15, 8 };
    int N = A.length;

    System.out.println(solve(A, N));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function returns maximum
# possible value of k
def solve(A, N):

    # Pointer i make sure that
    # A[i] will result in max k
    i = 0

    # Stores maximum possible k
    k = 0

    for j in range(1, N):

        # Possible value of k for
        # current pair (A[i] and A[j])
        tempK = (min(A[i], A[j]) // (j - i))

        # If current value exceeds k
        if (tempK > k):

            # Update the value of k
            k = tempK

        # Update pointer i
        if (A[j] >= A[i] // (j - i)):
            i = j

    # Return the maxm possible k
    return k

# Driver Code
if __name__ == "__main__":

    A = [ 10, 5, 12, 15, 8 ]
    N = len(A);

    print(solve(A, N))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function returns maximum
// possible value of k
static int solve(int[] A, int N)
{

    // Pointer i make sure that
    // A[i] will result in max k
    int i = 0;

    // Stores maximum possible k
    int k = 0;

    for(int j = 1; j < N; j++)
    {

        // Possible value of k for
        // current pair (A[i] and A[j])
        int tempK = Math.Min(A[i], A[j]) /
                              (j - i);

        // If current value exceeds k
        if (tempK > k)
        {

            // Update the value of k
            k = tempK;
        }

        // Update pointer i
        if (A[j] >= A[i] / (j - i))
            i = j;
    }

    // Return the maxm possible k
    return k;
}

// Driver Code
public static void Main(string[] args)
{
    int[] A = { 10, 5, 12, 15, 8 };
    int N = A.Length;

    Console.Write(solve(A, N));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function returns maximum
// possible value of k
function solve(A, N)
{

    // Pointer i make sure that
    // A[i] will result in max k
    let i = 0;

    // Stores maximum possible k
    let k = 0;

    for(let j = 1; j < N; j++)
    {

        // Possible value of k for
        // current pair (A[i] and A[j])
        let tempK = Math.min(A[i], A[j]) / (j - i);

        // If current value exceeds k
        if (tempK > k)
        {

            // Update the value of k
            k = tempK;
        }

        // Update pointer i
        if (A[j] >= A[i] / (j - i))
            i = j;
    }

    // Return the maxm possible k
    return k;
}

// Driver code
let A = [ 10, 5, 12, 15, 8 ];
let N = A.length;

document.write(solve(A, N));

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
12
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*