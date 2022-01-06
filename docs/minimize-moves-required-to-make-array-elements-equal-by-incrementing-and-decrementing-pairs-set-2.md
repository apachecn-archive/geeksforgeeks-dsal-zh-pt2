# 通过增加和减少对来最小化使数组元素相等所需的移动|设置 2

> 原文:[https://www . geesforgeks . org/minimum-moves-make-array-elements-equal-by-递增-递减-pairs-set-2/](https://www.geeksforgeeks.org/minimize-moves-required-to-make-array-elements-equal-by-incrementing-and-decrementing-pairs-set-2/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过选择**任意一对不同的索引**来打印使所有数组元素相等所需的最小移动次数，然后**每次将**第一个索引**处的元素增加**，将**第二个索引**处的元素减少**第一个索引**处的元素。如果不可能使所有数组元素相等，则打印**-1”。**

**示例:**

> **输入:** arr[] = {5，4，1，10}
> **输出:** 5
> **解释:**
> 执行操作的一种可能方式是:
> 操作 1:选择索引 1 和 3，然后将 arr[1]递增 1，将 arr[3]递减 1。此后，数组修改为{5，5，1，9}。
> 操作 2:选择索引 2 和 3，然后将 arr[2]增加 1，将 arr[3]减少 1。此后，数组修改为{5，5，2，8}。
> 操作 3:选择索引 2 和 3，然后将 arr[2]增加 1，将 arr[3]减少 1。此后，数组修改为{5，5，3，7}。
> 操作 4:选择索引 2 和 3，然后将 arr[2]增加 1，将 arr[3]减少 1。此后，数组修改为{5，5，4，6}。
> 操作 5:选择索引 2 和 3，然后将 arr[2]增加 1，将 arr[3]减少 1。此后，数组修改为{5，5，5，5}。
> 因此，需要的移动总数为 5。此外，这是所需的最小可能的移动。
> 
> **输入:** arr[] = {1，4}
> **输出:** -1

**天真的做法:**参考[之前的帖子](https://www.geeksforgeeks.org/minimize-moves-to-make-array-elements-equal-by-incrementing-and-decrementing-pairs/)最简单的解决问题的方法。
***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

*   可以观察到，在每次操作中，数组的[和保持不变。因此，如果数组的和不能被 **N** 整除，那么就不可能使所有的数组元素相等。](https://www.geeksforgeeks.org/python-program-to-find-sum-of-array/)
*   否则，每个数组元素将等于数组的**和除以 N** ，比如说 **k** 。
*   所以思路是[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)求当前元素和 **k** 的绝对差，加上 **ans** 。
*   因为在每个操作中，增量和减量都是一起执行的，所以 **ans / 2** 是所需的操作数。

按照以下步骤解决问题:

*   初始化一个变量，比如说**和**为 0，以存储所需操作的计数。
*   求数组的[和并存储在变量中，比如**和**。](https://www.geeksforgeeks.org/python-program-to-find-sum-of-array/)
*   现在，如果总和不能被 **N** 整除，那么打印**-1”**。否则，储存 **k =总和/ N** 。
*   初始化变量，说 **i = 0** ，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
*   当 **i** 小于 **N** 时迭代，将当前元素与 **k** 的绝对差值加到 **ans** 上:
*   最后，完成上述步骤后，打印 **ans / 2** 。

下面是上述方法的实现:

## C++

```
// cpp program for the above approach

// Function to find the minimum number
// of increment and decrement of pairs
// required to make all array elements equal
#include<bits/stdc++.h>
using namespace std;
int find(vector<int>arr, int N)
{

    // Stores the sum of the array
    int Sum = 0;
    for(auto i:arr)
        Sum += i;

    // If sum is not divisible by N
    if (Sum % N)
        return -1;

   // Update sum
    int k = Sum / N;
    int ans = 0;

    // Store the minimum
    // number of operations
    int i = 0;

    // Iterate while i
    // is less than N
    while (i < N){

        // Add absolute difference
        // of current element with
        // k to ans
        ans = ans + abs(k-arr[i]);

        // Increase i bye 1
        i += 1;
    }

    // Return the value in ans//2
    return ans /2;
}

// Driver Code
int main()
{

    // Given Input
    vector<int>arr = {5, 4, 1, 10};
    int N = arr.size();

    // Function Call
    cout<<(find(arr, N));
}

// This code is contributed by amreshkumar3.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

static int find(ArrayList<Integer>arr, int N)
{

    // Stores the sum of the array
    int Sum = 0;
    for(int item : arr)
        Sum += item;

    // If sum is not divisible by N
    if (Sum % N==1)
        return -1;

   // Update sum
    int k = Sum / N;
    int ans = 0;

    // Store the minimum
    // number of operations
    int i = 0;

    // Iterate while i
    // is less than N
    while (i < N){

        // Add absolute difference
        // of current element with
        // k to ans
        ans = ans + Math.abs(k-arr.get(i));

        // Increase i bye 1
        i += 1;
    }

    // Return the value in ans//2
    return ans /2;
}

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
    ArrayList<Integer>arr = new ArrayList<>();
    arr.add(5);
    arr.add(4);
    arr.add(1);
    arr.add(10);

    int N = arr.size();

    // Function Call
    System.out.println(find(arr, N));
    }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum number
# of increment and decrement of pairs
# required to make all array elements equal
def find(arr, N):

    # Stores the sum of the array
    Sum = sum(arr)

    # If sum is not divisible by N
    if Sum % N:
        return -1
    else:

       # Update sum
        k = Sum // N

        # Store the minimum
        # number of operations
        ans = 0

        i = 0

        # Iterate while i
        # is less than N
        while i < N:

            # Add absolute difference
            # of current element with
            # k to ans
            ans = ans + abs(k-arr[i])

            # Increase i bye 1
            i += 1

        # Return the value in ans//2
        return ans // 2

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [5, 4, 1, 10]
    N = len(arr)

    # Function Call
    print(find(arr, N))
```

## C#

```
// C# program for the above approach

// Function to find the minimum number
// of increment and decrement of pairs
// required to make all array elements equal
using System;
using System.Collections.Generic;

class GFG{

static int find(List<int>arr, int N)
{

    // Stores the sum of the array
    int Sum = 0;
    foreach(int item in arr)
        Sum += item;

    // If sum is not divisible by N
    if (Sum % N==1)
        return -1;

   // Update sum
    int k = Sum / N;
    int ans = 0;

    // Store the minimum
    // number of operations
    int i = 0;

    // Iterate while i
    // is less than N
    while (i < N){

        // Add absolute difference
        // of current element with
        // k to ans
        ans = ans + Math.Abs(k-arr[i]);

        // Increase i bye 1
        i += 1;
    }

    // Return the value in ans//2
    return ans /2;
}

// Driver Code
public static void Main()
{

    // Given Input
    List<int>arr = new List<int>(){5, 4, 1, 10};
    int N = arr.Count;

    // Function Call
    Console.Write(find(arr, N));
}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the minimum number
// of increment and decrement of pairs
// required to make all array elements equal
function find(arr, N)
{

    // Stores the sum of the array
    let Sum = 0;
    let i = 0;
    let ans = 0;

    for(i = 0; i < N; i++)
    {
        Sum += arr[i];
    }

    // If sum is not divisible by N
    if (Sum % N)
    {
        return -1;
    }
    else
    {

        // Update sum
        k = Math.floor(Sum / N);

        // Store the minimum
        // number of operations
        ans = 0;

        i = 0;

        // Iterate while i
        // is less than N
        while (i < N)
        {

            // Add absolute difference
            // of current element with
            // k to ans
            ans = ans + Math.abs(k - arr[i]);

            // Increase i bye 1
            i += 1;
        }
    }

    // Return the value in ans//2
    return Math.floor(ans / 2);
}

// Driver Code

// Given Input
let arr = [ 5, 4, 1, 10 ]
let N = arr.length;

// Function Call
document.write(find(arr, N));

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)