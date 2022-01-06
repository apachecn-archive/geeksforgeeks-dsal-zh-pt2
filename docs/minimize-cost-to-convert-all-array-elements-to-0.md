# 最小化将所有数组元素转换为 0 的成本

> 原文:[https://www . geeksforgeeks . org/最小化将所有数组元素转换为 0 的成本/](https://www.geeksforgeeks.org/minimize-cost-to-convert-all-array-elements-to-0/)

给定两个整数 **X** 和 **Y** 和一个长度为 **N** 的二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，其第一个和最后一个元素为 **1** ，任务是最小化将所有数组元素转换为 **0** 的成本，其中 **X** 和 **Y** 表示转换所有**的一个[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的成本**

**示例:**

> **输入:** arr[] = {1，1，1，0，1，1}，X = 10，Y = 4
> **输出:** 14
> **解释:**为了最小化将所有元素转换为 0 的成本，请执行以下操作:
> 
> 1.  将索引 3 处的元素更改为 1。现在数组修改为{1，1，1，1，1，1}。这次手术的费用是 4 英镑。
> 2.  将数组的所有元素更改为 0。这次手术的费用是 10 英镑。
>     因此，总成本为 4 + 10 + 14。
> 
> **输入:** arr[] = {1，0，0，1，1，0，1}，X = 2，Y = 3
> **输出:** 6
> **解释:**为了将所有数组元素更改为 0 的成本降至最低，请执行以下操作:
> 
> 1.  将子阵列的所有元素从[3，4]更改为 0。现在数组修改为{1，0，0，0，0，0，1}。这次手术的费用是 2 英镑。
> 2.  将子阵列的所有元素从[0，0]更改为 0。现在数组修改为{0，0，0，0，0，0，1}。这次手术的费用是 2 英镑。
> 3.  将子阵列的所有元素从[6，6]更改为 0。现在数组修改为{0，0，0，0，0，0，0}。这次手术的费用是 2 英镑。
> 
> 所以总成本是 2 + 2 + 2 = 3。

**进场:**按照步骤进行:

*   初始化一个变量，比如**和**，以存储将所有数组元素转换为 **0** 的最小成本。
*   计算并存储仅由 **0** 组成的所有[子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的长度，并将其存储在一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)和[中，按照递增顺序](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)对向量进行排序。
*   现在，只计算由 **1** s 组成的子阵数量。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，其中 **i** 表示 **Y** 成本运算的次数，并执行以下操作:
    *   对于成本 **Y** 的每一个可能的操作次数，通过执行 **X** 操作来计算成本。
    *   因为在两组 **1s** 之间设置位时，组的总数减少，所以首先合并两组连续的 **1** s，以减少最小操作数。
    *   为每个索引找到完成上述步骤的最小成本为 **currCost** 并更新 **ans** 以存储 **ans** 和 **currCost** 的最小值。
*   完成上述步骤后，打印**和**的值作为最小成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum cost
// of converting all array elements to 0s
void minimumCost(int* binary, int n,
                 int a, int b)
{
    // Stores subarrays of 0s only
    vector<int> groupOfZeros;

    int len = 0, i = 0;
    bool increment_need = true;

    // Traverse the array
    while (i < n) {
        increment_need = true;

        // If consecutive 0s occur
        while (i < n && binary[i] == 0) {
            len++;
            i++;
            increment_need = false;
        }

        // Increment if needed
        if (increment_need == true) {
            i++;
        }

        // Push the current length of
        // consecutive 0s in a vector
        if (len != 0) {
            groupOfZeros.push_back(len);
        }

        // Update lengths as 0
        len = 0;
    }

    // Sorting vector
    sort(groupOfZeros.begin(),
         groupOfZeros.end());

    i = 0;
    bool found_ones = false;

    // Stores the number of
    // subarrays consisting of 1s
    int NumOfOnes = 0;

    // Traverse the array
    while (i < n) {
        found_ones = false;

        // If current element is 1
        while (i < n && binary[i] == 1) {
            i++;
            found_ones = true;
        }
        if (found_ones == false)
            i++;

        // Otherwise
        else

            // Increment count of
            // consecutive ones
            NumOfOnes++;
    }

    // Stores the minimum cost
    int ans = INT_MAX;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        int curr = 0, totalOnes = NumOfOnes;

        // First element
        if (i == 0) {
            curr = totalOnes * a;
        }
        else {

            int mark = i, num_of_changes = 0;

            // Traverse the subarray sizes
            for (int x : groupOfZeros) {

                if (mark >= x) {
                    totalOnes--;
                    mark -= x;

                    // Update cost
                    num_of_changes += x;
                }
                else {
                    break;
                }
            }

            // Cost of performing X
            // and Y operations
            curr = (num_of_changes * b)
                   + (totalOnes * a);
        }

        // Find the minimum cost
        ans = min(ans, curr);
    }

    // Print the minimum cost
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 1, 1, 0, 1, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int X = 10, Y = 4;

    // Function Call
    minimumCost(arr, N, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to calculate the minimum cost
// of converting all array elements to 0s
public static void minimumCost(int[] binary, int n,
                               int a, int b)
{

    // Stores subarrays of 0s only
    List<Integer> groupOfZeros = new ArrayList<Integer>();

    int len = 0, i = 0;
    boolean increment_need = true;

    // Traverse the array
    while (i < n)
    {
        increment_need = true;

        // If consecutive 0s occur
        while (i < n && binary[i] == 0)
        {
            len++;
            i++;
            increment_need = false;
        }

        // Increment if needed
        if (increment_need == true)
        {
            i++;
        }

        // Push the current length of
        // consecutive 0s in a vector
        if (len != 0)
        {
            groupOfZeros.add(len);
        }

        // Update lengths as 0
        len = 0;
    }

    // Sorting List
    Collections.sort(groupOfZeros);

    i = 0;
    boolean found_ones = false;

    // Stores the number of
    // subarrays consisting of 1s
    int NumOfOnes = 0;

    // Traverse the array
    while (i < n)
    {
        found_ones = false;

        // If current element is 1
        while (i < n && binary[i] == 1)
        {
            i++;
            found_ones = true;
        }
        if (found_ones == false)
            i++;

        // Otherwise
        else

            // Increment count of
            // consecutive ones
            NumOfOnes++;
    }

    // Stores the minimum cost
    int ans = Integer.MAX_VALUE;

    // Traverse the array
    for(int i1 = 0; i1 < n; i1++)
    {
        int curr = 0, totalOnes = NumOfOnes;

        // First element
        if (i1 == 0)
        {
            curr = totalOnes * a;
        }
        else
        {
            int mark = i1, num_of_changes = 0;

            // Traverse the subarray sizes
            for(int x : groupOfZeros)
            {
                if (mark >= x)
                {
                    totalOnes--;
                    mark -= x;

                    // Update cost
                    num_of_changes += x;
                }
                else
                {
                    break;
                }
            }

            // Cost of performing X
            // and Y operations
            curr = (num_of_changes * b) +
                        (totalOnes * a);
        }

        // Find the minimum cost
        ans = Math.min(ans, curr);
    }

    // Print the minimum cost
    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 1, 0, 1, 1 };
    int N = 6;
    int X = 10, Y = 4;

    // Function Call
    minimumCost(arr, N, X, Y);
}
}

// This code is contributed by RohitOberoi
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to calculate the minimum cost
# of converting all array elements to 0s
def minimumCost(binary, n,
                a,  b):

    # Stores subarrays of 0s only
    groupOfZeros = []

    length = 0
    i = 0
    increment_need = True

    # Traverse the array
    while (i < n):
        increment_need = True

        # If consecutive 0s occur
        while (i < n and binary[i] == 0):
            length += 1
            i += 1
            increment_need = False

        # Increment if needed
        if (increment_need == True):
            i += 1

        # Push the current length of
        # consecutive 0s in a vector
        if (length != 0):
            groupOfZeros.append(length)

        # Update lengths as 0
        length = 0

    # Sorting vector
    groupOfZeros.sort()

    i = 0
    found_ones = False

    # Stores the number of
    # subarrays consisting of 1s
    NumOfOnes = 0

    # Traverse the array
    while (i < n):
        found_ones = False

        # If current element is 1
        while (i < n and binary[i] == 1):
            i += 1
            found_ones = True

        if (found_ones == False):
            i += 1

        # Otherwise
        else:

            # Increment count of
            # consecutive ones
            NumOfOnes += 1

    # Stores the minimum cost
    ans = sys.maxsize

    # Traverse the array
    for i in range(n):

        curr = 0
        totalOnes = NumOfOnes

        # First element
        if (i == 0):
            curr = totalOnes * a

        else:

            mark = i
            num_of_changes = 0

            # Traverse the subarray sizes
            for x in groupOfZeros:

                if (mark >= x):
                    totalOnes -= 1
                    mark -= x

                    # Update cost
                    num_of_changes += x

                else:
                    break

            # Cost of performing X
            # and Y operations
            curr = ((num_of_changes * b)
                    + (totalOnes * a))

        # Find the minimum cost
        ans = min(ans, curr)

    # Print the minimum cost
    print(ans)

# Driver Code
if __name__ == "__main__":
    arr = [1, 1, 1, 0, 1, 1]
    N = len(arr)
    X = 10
    Y = 4

    # Function Call
    minimumCost(arr, N, X, Y)

    # This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate the minimum cost
// of converting all array elements to 0s
public static void minimumCost(int[] binary, int n,
                               int a, int b)
{

    // Stores subarrays of 0s only
    List<int> groupOfZeros = new List<int>();

    int len = 0, i = 0;
    bool increment_need = true;

    // Traverse the array
    while (i < n)
    {
        increment_need = true;

        // If consecutive 0s occur
        while (i < n && binary[i] == 0)
        {
            len++;
            i++;
            increment_need = false;
        }

        // Increment if needed
        if (increment_need == true)
        {
            i++;
        }

        // Push the current length of
        // consecutive 0s in a vector
        if (len != 0)
        {
            groupOfZeros.Add(len);
        }

        // Update lengths as 0
        len = 0;
    }

    // Sorting List
    groupOfZeros.Sort();

    i = 0;
    bool found_ones = false;

    // Stores the number of
    // subarrays consisting of 1s
    int NumOfOnes = 0;

    // Traverse the array
    while (i < n)
    {
        found_ones = false;

        // If current element is 1
        while (i < n && binary[i] == 1)
        {
            i++;
            found_ones = true;
        }
        if (found_ones == false)
            i++;

        // Otherwise
        else

            // Increment count of
            // consecutive ones
            NumOfOnes++;
    }

    // Stores the minimum cost
    int ans = int.MaxValue;

    // Traverse the array
    for(int i1 = 0; i1 < n; i1++)
    {
        int curr = 0, totalOnes = NumOfOnes;

        // First element
        if (i1 == 0)
        {
            curr = totalOnes * a;
        }
        else
        {
            int mark = i1, num_of_changes = 0;

            // Traverse the subarray sizes
            foreach(int x in groupOfZeros)
            {
                if (mark >= x)
                {
                    totalOnes--;
                    mark -= x;

                    // Update cost
                    num_of_changes += x;
                }
                else
                {
                    break;
                }
            }

            // Cost of performing X
            // and Y operations
            curr = (num_of_changes * b) +
                        (totalOnes * a);
        }

        // Find the minimum cost
        ans = Math.Min(ans, curr);
    }

    // Print the minimum cost
    Console.WriteLine(ans);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 1, 1, 0, 1, 1 };
    int N = 6;
    int X = 10, Y = 4;

    // Function Call
    minimumCost(arr, N, X, Y);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the minimum cost
// of converting all array elements to 0s
function minimumCost(binary, n, a, b)
{
    // Stores subarrays of 0s only
    var groupOfZeros = [];

    var len = 0, i = 0;
    var increment_need = true;

    // Traverse the array
    while (i < n) {
        increment_need = true;

        // If consecutive 0s occur
        while (i < n && binary[i] == 0) {
            len++;
            i++;
            increment_need = false;
        }

        // Increment if needed
        if (increment_need == true) {
            i++;
        }

        // Push the current length of
        // consecutive 0s in a vector
        if (len != 0) {
            groupOfZeros.push(len);
        }

        // Update lengths as 0
        len = 0;
    }

    // Sorting vector
    groupOfZeros.sort((a,b)=>a-b);

    i = 0;
    var found_ones = false;

    // Stores the number of
    // subarrays consisting of 1s
    var NumOfOnes = 0;

    // Traverse the array
    while (i < n) {
        found_ones = false;

        // If current element is 1
        while (i < n && binary[i] == 1) {
            i++;
            found_ones = true;
        }
        if (found_ones == false)
            i++;

        // Otherwise
        else

            // Increment count of
            // consecutive ones
            NumOfOnes++;
    }

    // Stores the minimum cost
    var ans = 1000000000;

    // Traverse the array
    for (var i = 0; i < n; i++) {

        var curr = 0, totalOnes = NumOfOnes;

        // First element
        if (i == 0) {
            curr = totalOnes * a;
        }
        else {

            var mark = i, num_of_changes = 0;

            // Traverse the subarray sizes
            groupOfZeros.forEach(x => {

                if (mark >= x) {
                    totalOnes--;
                    mark -= x;

                    // Update cost
                    num_of_changes += x;
                }

            });

            // Cost of performing X
            // and Y operations
            curr = (num_of_changes * b)
                   + (totalOnes * a);
        }

        // Find the minimum cost
        ans = Math.min(ans, curr);
    }

    // Print the minimum cost
    document.write( ans);
}

// Driver Code

var arr = [ 1, 1, 1, 0, 1, 1 ];
var N = arr.length;
var X = 10, Y = 4;

// Function Call
minimumCost(arr, N, X, Y);

</script>
```

**Output:** 

```
14
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*