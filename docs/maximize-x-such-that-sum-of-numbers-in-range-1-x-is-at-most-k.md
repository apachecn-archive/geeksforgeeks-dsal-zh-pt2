# 最大化 X，使得[1，X]范围内的数字之和最多为 K

> 原文:[https://www . geesforgeks . org/maximize-x-so-numbers-in-range-1-x-is-顶多-k/](https://www.geeksforgeeks.org/maximize-x-such-that-sum-of-numbers-in-range-1-x-is-at-most-k/)

给定两个整数 **N** 和一个整数 **K** ，任务是找出小于或等于 **N** 的整数个数，使得自然数到该整数的[和小于或等于 **K** 。](https://www.geeksforgeeks.org/sum-of-all-natural-numbers-in-range-l-to-r/)

**示例:**

> **输入:** N = 5，K = 10
> **输出:** 4
> **说明:**
> 整数 1、2、3、4 满足条件。
> 
> 1.  整数 1 以内的自然数之和等于 1。少于 10 个。
> 2.  整数 2 以内的自然数之和等于(1+2 =) 3。少于 10 个。
> 3.  整数 3 以内的自然数之和等于(1+2+3 =) 6。少于 10 个。
> 4.  整数 4 以内的自然数之和等于(1+2+3+4 =) 10。等于 10。
> 
> **输入:** N=3，K = 0
> T3】输出: 0

**方法:**最简单的方法是遍历**【1，N】**范围，统计其和小于等于 **K** 的元素个数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the elements with
// sum of the first that many natural
// numbers less than or equal to K

int Count(int N, int K)
{
    // If K equals to 0
    if (K == 0)
        return 0;

    // Stores sum of first i natural
    // numbers
    int sum = 0;

    // Stores the result
    int res = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {
        // Increment sum by i
        sum += i;

        // Is sum is less than or
        // equal to K
        if (sum <= K)
            res++;

        // Otherwise,
        else
            break;
    }
    // Return res
    return res;
}
// Driver Code
int main()
{
    // Input
    int N = 6, K = 14;

    // Function call
    cout << Count(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

// Function to count the elements with
// sum of the first that many natural
// numbers less than or equal to K
static int Count(int N, int K)
{
    // If K equals to 0
    if (K == 0)
        return 0;

    // Stores sum of first i natural
    // numbers
    int sum = 0;

    // Stores the result
    int res = 0;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++)
    {
        // Increment sum by i
        sum += i;

        // Is sum is less than or
        // equal to K
        if (sum <= K)
            res++;

        // Otherwise,
        else
            break;
    }

    // Return res
    return res;
}

// Driver Code
 public static void main(String args[])
{
    // Input
    int N = 6, K = 14;

    // Function call
    System.out.println(Count(N, K));
    }
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the elements with
# sum of the first that many natural
# numbers less than or equal to K
def Count(N, K):

    # If K equals to 0
    if (K == 0):
        return 0

    # Stores sum of first i natural
    # numbers
    sum = 0

    # Stores the result
    res = 0

    # Iterate over the range [1, N]
    for i in range(1, N + 1, 1):

        # Increment sum by i
        sum += i

        # Is sum is less than or
        # equal to K
        if (sum <= K):
            res += 1

        # Otherwise,
        else:
            break

    # Return res
    return res

# Driver Code
if __name__ == '__main__':

    # Input
    N = 6
    K = 14

    # Function call
    print(Count(N, K))

# This code is contributed by bgangwar59
```

## C#

```
// C# program for the above approach
using System;

class GFG {

    // Function to count the elements with
    // sum of the first that many natural
    // numbers less than or equal to K
    static int Count(int N, int K)
    {
        // If K equals to 0
        if (K == 0)
            return 0;

        // Stores sum of first i natural
        // numbers
        int sum = 0;

        // Stores the result
        int res = 0;

        // Iterate over the range [1, N]
        for (int i = 1; i <= N; i++) {
            // Increment sum by i
            sum += i;

            // Is sum is less than or
            // equal to K
            if (sum <= K)
                res++;

            // Otherwise,
            else
                break;
        }

        // Return res
        return res;
    }

    // Driver Code
    public static void Main()
    {
        // Input
        int N = 6, K = 14;

        // Function call
        Console.WriteLine(Count(N, K));
    }
}

// This code is contributed by subhammahato348.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count the elements with
// sum of the first that many natural
// numbers less than or equal to K

function Count(N, K) {
    // If K equals to 0
    if (K == 0)
        return 0;

    // Stores sum of first i natural
    // numbers
    let sum = 0;

    // Stores the result
    let res = 0;

    // Iterate over the range [1, N]
    for (let i = 1; i <= N; i++) {
        // Increment sum by i
        sum += i;

        // Is sum is less than or
        // equal to K
        if (sum <= K)
            res++;

        // Otherwise,
        else
            break;
    }
    // Return res
    return res;
}
// Driver Code

// Input
let N = 6, K = 14;

// Function call
document.write(Count(N, K));

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**有效方法:**上述方法可以通过使用[二分搜索法算法](https://www.geeksforgeeks.org/binary-search/)进行优化。按照以下步骤解决问题:

*   初始化一个变量，将 **res** 设为 **0** 来存储结果。
*   另外，初始化两个变量，说**低**和**高**，分别为 **1** 和 **N** 。
*   重复直到**低电平**小于或等于**高电平**，并执行以下步骤:
    *   找到范围的中间值**【低，高】**并将其存储在变量中，比如**中间**。
    *   计算自然数到**中间**的[和，并将其存储在一个变量中，比如**和**。](https://www.geeksforgeeks.org/sum-of-all-natural-numbers-in-range-l-to-r/)
    *   如果**之和**小于或等于 **K** ，则将 **res** 更新为**最大(res，mid)** ，并将 **mid+1** 分配给**低**。
    *   否则，将**中间 1** 指定为**高**。
*   最后，完成以上步骤后，打印 **res** 的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the elements with
// sum of the first that many natural
// numbers less than or equal to K

int Count(int N, int K)
{
    // If K equals to 0
    if (K == 0)
        return 0;

    // Stores the result
    int res = 0;

    int low = 1, high = N;

    // Iterate until low is less than
    // or equal to high
    while (low <= high) {

        int mid = (low + high) / 2;

        // Stores the sum of first mid
        // natural numbers

        int sum = (mid * mid + mid) / 2;
        // If sum is less than or equal
        // to K
        if (sum <= K) {
            // Update res and low
            res = max(res, mid);
            low = mid + 1;
        }
        // Otherwise,
        else {
            // Update
            high = mid - 1;
        }
    }

    // Return res
    return res;
}
// Driver Code
int main()
{
    // Input
    int N = 6, K = 14;

    // Function call
    cout << Count(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
class GFG{

// Function to count the elements with
// sum of the first that many natural
// numbers less than or equal to K
    static int Count(int N, int K)
    {

        // If K equals to 0
        if (K == 0)
            return 0;

        // Stores the result
        int res = 0;

        int low = 1, high = N;

        // Iterate until low is less than
        // or equal to high
        while (low <= high) {

            int mid = (low + high) / 2;

            // Stores the sum of first mid
            // natural numbers

            int sum = (mid * mid + mid) / 2;
            // If sum is less than or equal
            // to K
            if (sum <= K)
            {

                // Update res and low
                res = Math.max(res, mid);
                low = mid + 1;
            }

            // Otherwise,
            else
            {

                // Update
                high = mid - 1;
            }
        }

        // Return res
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Input
        int N = 6, K = 14;

        // Function call
        System.out.println(Count(N, K));
    }
}

// This code is contributed by hritikrommie.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the elements with
# sum of the first that many natural
# numbers less than or equal to K
def Count(N, K):

    # If K equals to 0
    if (K == 0):
        return 0

    # Stores the result
    res = 0

    low = 1
    high = N

    # Iterate until low is less than
    # or equal to high
    while (low <= high):
        mid = (low + high) // 2

        # Stores the sum of first mid
        # natural numbers
        sum = (mid * mid + mid) // 2

        # If sum is less than or equal
        # to K
        if (sum <= K):

            # Update res and low
            res = max(res, mid)
            low = mid + 1

        # Otherwise,
        else:

            # Update
            high = mid - 1

    # Return res
    return res

# Driver Code
if __name__ == '__main__':

    # Input
    N = 6
    K = 14

    # Function call
    print(Count(N, K))

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to count the elements with
// sum of the first that many natural
// numbers less than or equal to K
static int Count(int N, int K)
{

    // If K equals to 0
    if (K == 0)
        return 0;

    // Stores the result
    int res = 0;

    int low = 1, high = N;

    // Iterate until low is less than
    // or equal to high
    while (low <= high)
    {
        int mid = (low + high) / 2;

        // Stores the sum of first mid
        // natural numbers

        int sum = (mid * mid + mid) / 2;

        // If sum is less than or equal
        // to K
        if (sum <= K)
        {

            // Update res and low
            res = Math.Max(res, mid);
            low = mid + 1;
        }

        // Otherwise,
        else
        {

            // Update
            high = mid - 1;
        }
    }

    // Return res
    return res;
}

// Driver Code
public static void Main(String[] args)
{

    // Input
    int N = 6, K = 14;

    // Function call
    Console.Write (Count(N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
// JavaScript program for above approach

// Function to count the elements with
// sum of the first that many natural
// numbers less than or equal to K
function Count( N,  K)
    {

        // If K equals to 0
        if (K == 0)
            return 0;

        // Stores the result
        var res = 0;

        var low = 2, high = N;

        // Iterate until low is less than
        // or equal to high
        while (low <= high) {

            var mid = (low + high) / 2;

            // Stores the sum of first mid
            // natural numbers

            var sum = (mid * mid + mid) / 2;
            // If sum is less than or equal
            // to K
            if (sum <= K)
            {

                // Update res and low
                res = Math.max(res, mid);
                low = mid + 1;
            }

            // Otherwise,
            else
            {

                // Update
                high = mid - 1;
            }
        }

        // Return res
        return res;
    }

    // Driver Code
        // Input
        var N = 6, K = 14;

        // Function call
        document.write(Count(N, K));

// This code is contributed by shivanisinghss2110.
</script>
```

**Output**

```
4
```

***时间复杂度:** O(log(N))*
***辅助空间:** O(1)*