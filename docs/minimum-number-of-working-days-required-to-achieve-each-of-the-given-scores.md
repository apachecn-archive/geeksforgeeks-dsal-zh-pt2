# 达到每个给定分数所需的最小工作日数

> 原文:[https://www . geesforgeks . org/达到每个给定分数所需的最小工作日数/](https://www.geeksforgeeks.org/minimum-number-of-working-days-required-to-achieve-each-of-the-given-scores/)

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和由 **M** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**P【】**，使得**P【I】**代表通过在 **i <sup>第</sup>天**工作获得的分数。任务是为每个数组元素**arr【I】**找到至少达到**arr【I】**分数所需的最小工作天数。

**示例:**

> **输入:** arr[] = {400，200，700}，P[] = {100，300，400，500，600}
> **输出:**2 3 4 5
> **解释:**
> 以下是每个数组元素所需的天数:
> 
> 1.  **arr[0](= 400):** 要获得 400 分，必须在前两天工作，使总积分等于 100 + 300 = 400( > = arr[0])。
> 2.  **arr[1](= 200):** 要获得 200 分，必须在前两天工作，使总积分= 100 + 300 = 400( > = arr[1])。
> 3.  **arr[2](= 700):** 要获得 700 分，你必须在前 3 天工作，使总积分= 100 + 300 + 400 = 800( > = arr[2])。
> 
> **输入:** arr[] = {1400}，P[] = {100，300}
> **输出:** -1

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr【】**并且对于每个数组，元素找到数组的最小索引**P【】**使得[子数组](https://www.geeksforgeeks.org/sum-of-all-subarrays/)在范围**【0，I】**上的和至少为**arr【I】**。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以通过找到**P【】**的[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)，然后使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到值至少为**的和【arr[i]** 。按照以下步骤解决问题:

*   [找到数组 **P[]**](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) 的前缀和数组。
*   [遍历给定数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr[]** ，并执行以下步骤:
    *   [在数组**P【】**a](https://www.geeksforgeeks.org/first-element-greater-than-or-equal-to-x-in-prefix-sum-of-n-numbers-using-binary-lifting/)中找到大于当前元素**arr【I】**的第一个元素的索引，并将其存储在一个变量中，比如说**索引**。
    *   如果**索引**的值为 **-1** ，则打印 **-1** 。否则，打印**(索引+ 1)** 的值作为当前索引的结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the lower bound
// of N using binary search
int binarySeach(vector<int> P, int N)
{

    // Stores the lower bound
    int i = 0;

    // Stores the upper bound
    int j = P.size() - 1;

    // Stores the minimum index
    // having value is at least N
    int index = -1;

    // Iterator while i<=j
    while (i <= j)
    {

        // Stores the mid index
        // of the range [i, j]
        int mid = i + (j - i) / 2;

        // If P[mid] is at least N
        if (P[mid] >= N)
        {

            // Update the value of
            // mid to index
            index = mid;

            // Update the value of j
            j = mid - 1;
        }

        // Update the value of i
        else
        {
            i = mid + 1;
        }
    }

    // Return the resultant index
    return index;
}

// Function to find the minimum number
// of days required to work to at least
// arr[i] points for every array element
void minDays(vector<int> P, vector<int> arr)
{

    // Traverse the array P[]
    for(int i = 1; i < P.size(); i++)
    {

        // Find the prefix sum
        P[i] += P[i] + P[i - 1];
    }

    // Traverse the array arr[]
    for(int i = 0; i < arr.size(); i++)
    {

        // Find the minimum index of
        // the array having value
        // at least arr[i]
        int index = binarySeach(P, arr[i]);

        // If the index is not -1
        if (index != -1)
        {
            cout << index + 1 << " ";
        }

        // Otherwise
        else
        {
            cout << -1 << " ";
        }
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 400, 200, 700, 900, 1400 };
    vector<int> P = { 100, 300, 400, 500, 600 };
    minDays(P, arr);

    return 0;
}

// This code is contributed by nirajgusain5
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GFG {

    // Function to find the minimum number
    // of days required to work to at least
    // arr[i] points for every array element
    static void minDays(int[] P, int[] arr)
    {
        // Traverse the array P[]
        for (int i = 1; i < P.length; i++) {

            // Find the prefix sum
            P[i] += P[i] + P[i - 1];
        }

        // Traverse the array arr[]
        for (int i = 0;
             i < arr.length; i++) {

            // Find the minimum index of
            // the array having value
            // at least arr[i]
            int index = binarySeach(
                P, arr[i]);

            // If the index is not -1
            if (index != -1) {
                System.out.print(
                    index + 1 + " ");
            }

            // Otherwise
            else {
                System.out.print(
                    -1 + " ");
            }
        }
    }

    // Function to find the lower bound
    // of N using binary search
    static int binarySeach(
        int[] P, int N)
    {
        // Stores the lower bound
        int i = 0;

        // Stores the upper bound
        int j = P.length - 1;

        // Stores the minimum index
        // having value is at least N
        int index = -1;

        // Iterator while i<=j
        while (i <= j) {

            // Stores the mid index
            // of the range [i, j]
            int mid = i + (j - i) / 2;

            // If P[mid] is at least N
            if (P[mid] >= N) {

                // Update the value of
                // mid to index
                index = mid;

                // Update the value of j
                j = mid - 1;
            }

            // Update the value of i
            else {
                i = mid + 1;
            }
        }

        // Return the resultant index
        return index;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 400, 200, 700, 900, 1400 };
        int[] P = { 100, 300, 400, 500, 600 };
        minDays(P, arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of days required to work to at least
# arr[i] points for every array element
def minDays(P, arr):

    # Traverse the array P[]
    for i in range(1, len(P)):

        # Find the prefix sum
        P[i] += P[i] + P[i - 1]

    # Traverse the array arr[]
    for i in range(len(arr)):

        # Find the minimum index of
        # the array having value
        # at least arr[i]
        index = binarySeach(P, arr[i])

        # If the index is not -1
        if (index != -1):
            print(index + 1, end = " ")
        # Otherwise
        else:
            print(-1, end = " ")

# Function to find the lower bound
# of N using binary search
def binarySeach(P, N):

    # Stores the lower bound
    i = 0

    # Stores the upper bound
    j = len(P) - 1

    # Stores the minimum index
    # having value is at least N
    index = -1

    # Iterator while i<=j
    while (i <= j):

        # Stores the mid index
        # of the range [i, j]
        mid = i + (j - i) // 2

        # If P[mid] is at least N
        if (P[mid] >= N):

            # Update the value of
            # mid to index
            index = mid

            # Update the value of j
            j = mid - 1

        # Update the value of i
        else:
            i = mid + 1

    # Return the resultant index
    return index

    # Driver Code
if __name__ == '__main__':
    arr = [400, 200, 700,900,1400 ]
    P =  [100, 300, 400, 500, 600 ]
    minDays(P, arr)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number
// of days required to work to at least
// arr[i] points for every array element
static void minDays(int[] P, int[] arr)
{

    // Traverse the array P[]
    for(int i = 1; i < P.Length; i++)
    {

        // Find the prefix sum
        P[i] += P[i] + P[i - 1];
    }

    // Traverse the array arr[]
    for(int i = 0; i < arr.Length; i++)
    {

        // Find the minimum index of
        // the array having value
        // at least arr[i]
        int index = binarySeach(P, arr[i]);

        // If the index is not -1
        if (index != -1)
        {
            Console.Write(index + 1 + " ");
        }

        // Otherwise
        else
        {
            Console.Write(-1 + " ");
        }
    }
}

// Function to find the lower bound
// of N using binary search
static int binarySeach(int[] P, int N)
{

    // Stores the lower bound
    int i = 0;

    // Stores the upper bound
    int j = P.Length - 1;

    // Stores the minimum index
    // having value is at least N
    int index = -1;

    // Iterator while i<=j
    while (i <= j)
    {

        // Stores the mid index
        // of the range [i, j]
        int mid = i + (j - i) / 2;

        // If P[mid] is at least N
        if (P[mid] >= N)
        {

            // Update the value of
            // mid to index
            index = mid;

            // Update the value of j
            j = mid - 1;
        }

        // Update the value of i
        else
        {
            i = mid + 1;
        }
    }

    // Return the resultant index
    return index;
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = { 400, 200, 700, 900, 1400 };
    int[] P = { 100, 300, 400, 500, 600 };

    minDays(P, arr);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the lower bound
// of N using binary search
function binarySeach(P, N)
{

    // Stores the lower bound
    var i = 0;

    // Stores the upper bound
    var j = P.length - 1;

    // Stores the minimum index
    // having value is at least N
    var index = -1;

    // Iterator while i<=j
    while (i <= j)
    {

        // Stores the mid index
        // of the range [i, j]
        var mid = i + parseInt((j - i) / 2);

        // If P[mid] is at least N
        if (P[mid] >= N)
        {

            // Update the value of
            // mid to index
            index = mid;

            // Update the value of j
            j = mid - 1;
        }

        // Update the value of i
        else
        {
            i = mid + 1;
        }
    }

    // Return the resultant index
    return index;
}

// Function to find the minimum number
// of days required to work to at least
// arr[i] points for every array element
function minDays(P, arr)
{

    // Traverse the array P[]
    for(var i = 1; i < P.length; i++)
    {

        // Find the prefix sum
        P[i] += P[i] + P[i - 1];
    }

    // Traverse the array arr[]
    for(var i = 0; i < arr.length; i++)
    {

        // Find the minimum index of
        // the array having value
        // at least arr[i]
        var index = binarySeach(P, arr[i]);

        // If the index is not -1
        if (index != -1)
        {
            document.write( (index + 1) + " ");
        }

        // Otherwise
        else
        {
            document.write( -1 + " ");
        }
    }
}

// Driver Code
var arr = [400, 200, 700, 900, 1400];
var P = [100, 300, 400, 500, 600];
minDays(P, arr);

</script>
```

**Output:** 

```
2 2 2 3 3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*