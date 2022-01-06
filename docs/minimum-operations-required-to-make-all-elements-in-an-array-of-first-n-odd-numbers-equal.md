# 使前 N 个奇数数组中的所有元素相等所需的最小运算

> 原文:[https://www . geeksforgeeks . org/最小运算-使数组中所有元素的第一个 n 个奇数相等/](https://www.geeksforgeeks.org/minimum-operations-required-to-make-all-elements-in-an-array-of-first-n-odd-numbers-equal/)

给定一个由[第一个 **N** 奇数](https://www.geeksforgeeks.org/sum-first-n-odd-numbers-o1-complexity/)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，任务是通过重复选择一对元素，并将该对中的一个元素递增和另一个元素递减 **1** ，找到使[所有数组元素相等所需的最小操作数。](https://www.geeksforgeeks.org/all-elements-in-an-array-are-same-or-not/)

**示例:**

> **输入:** N = 3
> **输出:** 2
> **说明:**
> 最初，数组为{1，3，5}。执行以下操作:
> **操作 1:** 将 arr[2]减少 1，将 arr[0]增加 1。数组修改为{2，3，4}。
> **操作 2:** 将 arr[2]递减 1，将 arr[0]递增 1。数组修改为{3，3，3}。
> 因此，所需的最小操作次数为 2 次。
> 
> **输入:**N = 6
> T3】输出: 9

**天真方法:**给定的问题可以基于以下观察来解决:

*   可以观察到，使所有数组元素等于数组的中间元素需要最少的操作次数。
*   因此，想法是使用变量 **i** 遍历数组，并在每个操作中选择索引 **i** 和**(N–I–1)**处的元素，使它们等于中间元素。

按照以下步骤解决问题:

*   初始化一个变量，比如说**中间的**，它存储了数组的中间元素[。](https://www.geeksforgeeks.org/start-end-start2-preferrable-method-calculating-middle-array-start-end2/)
*   初始化一个数组 **arr[]** ，将数组元素存储为 **arr[i] = 2 * i + 1。**
*   [求数组](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)**arr【】**的和，并将其存储在一个变量中，比如 **sum** 。
*   如果 [**N** 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则将**中间**的值更新为**arr【N/2】**。否则，将**中间**的值更新为**总和/ N** 。
*   初始化一个变量，比如说**和**为 **0** ，存储最小的操作数。
*   [在范围**【0，N/2】**内遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并将**和**的值增加值**(mid-arr[I])**。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations required to make the
// array elements equal
int minOperations(int N)
{

    // Stores the array elements
    int arr[N];

    // Stores the sum of the array
    int sum = 0;

    // Iterate over the range [0, N]
    for(int i = 0; i < N; i++)
    {

        // Update the value arr[i]
        arr[i] = (2 * i) + 1;

        // Increment the sum by
        // the value arr[i]
        sum = sum + arr[i];
    }

    // Stores the middle element
    int mid = 0;

    // If N is even
    if (N % 2 == 0)
    {
        mid = sum / N;
    }

    // Otherwise
    else {
        mid = arr[N / 2];
    }

    // Stores the result
    int ans = 0;

    // Traverse the range [0, N / 2]
    for(int i = 0; i < N / 2; i++)
    {

        // Update the value of ans
        ans += mid - arr[i];
    }

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    int N = 6;
    cout << minOperations(N);

    return 0;
}

// This code is contributed by susmitakundugoaldanga
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find the minimum number
    // of operations required to make the
    // array elements equal
    public static int minOperations(int N)
    {
        // Stores the array elements
        int[] arr = new int[N];

        // Stores the sum of the array
        int sum = 0;

        // Iterate over the range [0, N]
        for (int i = 0; i < N; i++) {

            // Update the value arr[i]
            arr[i] = (2 * i) + 1;

            // Increment the sum by
            // the value arr[i]
            sum = sum + arr[i];
        }

        // Stores the middle element
        int mid = 0;

        // If N is even
        if (N % 2 == 0) {
            mid = sum / N;
        }

        // Otherwise
        else {
            mid = arr[N / 2];
        }

        // Stores the result
        int ans = 0;

        // Traverse the range [0, N / 2]
        for (int i = 0; i < N / 2; i++) {

            // Update the value of ans
            ans += mid - arr[i];
        }

        // Return the result
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 6;
        System.out.println(
            minOperations(N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of operations required to make the
# array elements equal
def minOperations(N):

    # Stores the array elements
    arr = [0] * N

    # Stores the sum of the array
    sum = 0

    # Iterate over the range [0, N]
    for i in range(N) :

        # Update the value arr[i]
        arr[i] = (2 * i) + 1

        # Increment the sum by
        # the value arr[i]
        sum = sum + arr[i]

    # Stores the middle element
    mid = 0

    # If N is even
    if N % 2 == 0 :
        mid = sum / N

    # Otherwise
    else:
        mid = arr[int(N / 2)]

    # Stores the result
    ans = 0

    # Traverse the range [0, N / 2]
    for i in range(int(N / 2)):

        # Update the value of ans
        ans += mid - arr[i]

    # Return the result
    return int(ans)

# Driver Code
N = 6
print(minOperations(N))

# This code is contributed by Dharanendra L V.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// of operations required to make the
// array elements equal
public static int minOperations(int N)
{

    // Stores the array elements
    int[] arr = new int[N];

    // Stores the sum of the array
    int sum = 0;

    // Iterate over the range [0, N]
    for(int i = 0; i < N; i++)
    {

        // Update the value arr[i]
        arr[i] = (2 * i) + 1;

        // Increment the sum by
        // the value arr[i]
        sum = sum + arr[i];
    }

    // Stores the middle element
    int mid = 0;

    // If N is even
    if (N % 2 == 0)
    {
        mid = sum / N;
    }

    // Otherwise
    else
    {
        mid = arr[N / 2];
    }

    // Stores the result
    int ans = 0;

    // Traverse the range [0, N / 2]
    for(int i = 0; i < N / 2; i++)
    {

        // Update the value of ans
        ans += mid - arr[i];
    }

    // Return the result
    return ans;
}

// Driver Code
public static void Main(string[] args)
{
    int N = 6;

    Console.WriteLine(minOperations(N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to find the minimum number
// of operations required to make the
// array elements equal
function minOperations(N)
{

    // Stores the array elements
    let arr = Array.from({length: N}, (_, i) => 0);

    // Stores the sum of the array
    let sum = 0;

    // Iterate over the range [0, N]
    for(let i = 0; i < N; i++)
    {

        // Update the value arr[i]
        arr[i] = (2 * i) + 1;

        // Increment the sum by
        // the value arr[i]
        sum = sum + arr[i];
    }

    // Stores the middle element
    let mid = 0;

    // If N is even
    if (N % 2 == 0)
    {
        mid = sum / N;
    }

    // Otherwise
    else
    {
        mid = arr[N / 2];
    }

    // Stores the result
    let ans = 0;

    // Traverse the range [0, N / 2]
    for(let i = 0; i < N / 2; i++)
    {

        // Update the value of ans
        ans += mid - arr[i];
    }

    // Return the result
    return ans;
}

// Driver Code

    let N = 6;
    document.write(minOperations(N));

</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**高效方法:**上述方法可以基于以下观察进行优化:

*   如果 [N 为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则结果为第一个 **N / 2** 偶数的[和，即 **(K * (K + 1)) / 2，**其中 **K = (N / 2)** 。](https://www.geeksforgeeks.org/sum-first-n-even-numbers/)
*   否则，结果为第一个 **K** 奇数的[和，即 **K * K，**，其中**K =((N–1)/2)**。](https://www.geeksforgeeks.org/sum-first-n-odd-numbers-o1-complexity/)

所以如果[的 **N** 的值是偶数](https://www.geeksforgeeks.org/sum-first-n-even-numbers/)，那么打印 **(N / 2) <sup>2</sup>** 的值。否则，打印 **K * (K + 1) / 2** 的值，其中**K =((N–1)/2)**作为合成运算。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
    // of operations required to make the
    // array elements equal
    int minOperation(int N)
    {
        // If the value of N is even
        if (N % 2 == 0) {

            // Return the value
            return (N / 2) * (N / 2);
        }

        // Otherwise, N is odd
        int k = (N - 1) / 2;

        // Return the value
        return k * (k + 1);
    }

// Driver Code
int main()
{
     int N = 6;
     cout << minOperation(N);

    return 0;
}

// This code is contributed by code_hunt.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find the minimum number
    // of operations required to make the
    // array elements equal
    public static int minOperation(int N)
    {
        // If the value of N is even
        if (N % 2 == 0) {

            // Return the value
            return (N / 2) * (N / 2);
        }

        // Otherwise, N is odd
        int k = (N - 1) / 2;

        // Return the value
        return k * (k + 1);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 6;
        System.out.println(
            minOperation(N));
    }
}
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to find the minimum number
// of operations required to make the
// array elements equal
public static int minOperation(int N)
{

    // If the value of N is even
    if (N % 2 == 0)
    {

        // Return the value
        return (N / 2) * (N / 2);
    }

    // Otherwise, N is odd
    int k = (N - 1) / 2;

    // Return the value
    return k * (k + 1);
}

// Driver code
static void Main()
{
    int N = 6;

    Console.WriteLine(minOperation(N));
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of operations required to make the
# array elements equal
def minOperation(N) :

    # If the value of N is even
    if (N % 2 == 0) :

        # Return the value
        return (N / 2) * (N / 2)

    # Otherwise, N is odd
    k = (N - 1) / 2

    # Return the value
    return (k * (k + 1))

# Driver Code

N = 6
print(int(minOperation(N)))

# This code is contributed by souravghosh0416.
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

  // Function to find the minimum number
    // of operations required to make the
    // array elements equal
    function minOperation(N)
    {
        // If the value of N is even
        if (N % 2 == 0) {

            // Return the value
            return (N / 2) * (N / 2);
        }

        // Otherwise, N is odd
        let k = (N - 1) / 2;

        // Return the value
        return k * (k + 1);
    }

// Driver Code

        let N = 6;
         document.write(
            minOperation(N));

 // This code is contributed by splevel62.
</script>
```

**Output:** 

```
9
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)