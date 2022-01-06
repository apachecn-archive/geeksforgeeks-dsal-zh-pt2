# 可以由范围

中的任意整数唯一表示的最大范围

> 原文:[https://www . geesforgeks . org/最大范围-可以由范围中的任意整数唯一表示的范围/](https://www.geeksforgeeks.org/maximum-ranges-that-can-be-uniquely-represented-by-any-integer-from-the-range/)

给定一个由形式为 **{L，R}** 的 **N** 个范围组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**，任务是找到最大化的范围数，使得每个范围可以由该范围内的任意整数唯一表示。

**示例:**

> **输入:** arr[] = {{1，2}，{2，3}，{3，4}}
> **输出:** 3
> **解释:**
> 范围的数量可以通过以下表示最大化:
> 
> 1.  范围{1，2}可以用 1 表示。
> 2.  范围{2，3}可以用 2 表示。
> 3.  范围{3，4}可以用 3 来表示。
> 
> 因此，范围的最大计数是 3。
> 
> **输入:** arr[] = {{1，4}，{4，4}，{2，2}，{3，4}，{1，1}}
> **输出:** 4

**天真方法:**解决给定问题最简单的方法是[对范围](https://www.geeksforgeeks.org/python-sort-by-range-inclusion/)进行排序，从 **L** 的最小值迭代到 **R** 的最大值，贪婪地为特定范围分配一个整数，并记录可能分配的整数的数量。完成上述步骤后，打印获得的计数作为结果。
***时间复杂度:** O(M * N)，其中 **M** 是给定范围* *中的* [*最大元素。*
***辅助空间:** O(1)*](https://www.geeksforgeeks.org/maximum-occurred-integer-n-ranges/)

**高效方法:**上述方法也可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)进行优化，其思想是通过按递增顺序选择给定的范围，从每个范围中分配最小唯一值。 [](https://www.geeksforgeeks.org/merge-sort-tree-for-range-order-statistics/) 按照步骤解决问题:

*   [按升序排列给定的范围数组](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)。
*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说 **prev** 为**arr【】**，它存储给定范围的先前赋值。
*   初始化一个变量，比如说**把**算作 **1** 来存储最大范围数，其中每个范围可以由该范围内的一个整数唯一表示。
*   [在范围**【1，N–1】**内遍历给定的数组 arr[]](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) ，并执行以下步骤:
    *   初始化一个向量，比如说**当前[]** 为 **arr[i]** ，它存储分配给当前范围的值。
    *   如果 **max(current[i][1]、prev[I][1])**–**max(current[I][0]、prev[I][0]–1)**的值为正，则更新 **prev** 的值为 **{1 + max(current[i][0]、prev[I][0]–1)、max(current[i][1]、prev[i][1])}** ，并增加**计数**的值
    *   否则，检查下一个范围。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of ranges where each range can be
// uniquely represented by an integer
int maxRanges(vector<vector<int> > arr,
              int N)
{
    // Sort the ranges in ascending order
    sort(arr.begin(), arr.end());

    // Stores the count of ranges
    int count = 1;

    // Stores previously assigned range
    vector<int> prev = arr[0];

    // Traverse the vector arr[]
    for (int i = 1; i < N; i++) {

        vector<int> last = arr[i - 1];
        vector<int> current = arr[i];

        // Skip the similar ranges
        // of size 1
        if (last[0] == current[0]
            && last[1] == current[1]
            && current[1] == current[0])
            continue;

        // Find the range of integer
        // available to be assigned
        int start = max(prev[0], current[0] - 1);
        int end = max(prev[1], current[1]);

        // Check if an integer is
        // available to be assigned
        if (end - start > 0) {

            // Update the previously
            // assigned range
            prev[0] = 1 + start;
            prev[1] = end;

            // Update the count of range
            count++;
        }
    }

    // Return the maximum count of
    // ranges
    return count;
}

// Driver Code
int main()
{
    vector<vector<int> > range = {
        { 1, 4 }, { 4, 4 },
        { 2, 2 }, { 3, 4 },
        { 1, 1 }
    };
    int N = range.size();
    cout << maxRanges(range, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Function to find the maximum number
    // of ranges where each range can be
    // uniquely represented by an integer
    static int maxRanges(Integer arr[][], int N)
    {
        // Sort the ranges in ascending order
        Arrays.sort(arr, (a, b) -> {
            if (a[0].equals(b[0]))
                return Integer.compare(a[1], b[1]);
            return Integer.compare(a[0], b[0]);
        });

        // Stores the count of ranges
        int count = 1;

        // Stores previously assigned range
        Integer prev[] = arr[0];

        // Traverse the vector arr[]
        for (int i = 1; i < N; i++) {

            Integer last[] = arr[i - 1];
            Integer current[] = arr[i];

            // Skip the similar ranges
            // of size 1
            if (last[0] == current[0]
                && last[1] == current[1]
                && current[1] == current[0])
                continue;

            // Find the range of integer
            // available to be assigned
            int start = Math.max(prev[0], current[0] - 1);
            int end = Math.max(prev[1], current[1]);

            // Check if an integer is
            // available to be assigned
            if (end - start > 0) {

                // Update the previously
                // assigned range
                prev[0] = 1 + start;
                prev[1] = end;

                // Update the count of range
                count++;
            }
        }

        // Return the maximum count of
        // ranges
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {

        Integer range[][] = {
            { 1, 4 }, { 4, 4 }, { 2, 2 }, { 3, 4 }, { 1, 1 }
        };
        int N = range.length;
        System.out.print(maxRanges(range, N));
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the maximum number
# of ranges where each range can be
# uniquely represented by an integer
def maxRanges(arr, N):

    # Sort the ranges in ascending order
    arr.sort()

    # Stores the count of ranges
    count = 1

    # Stores previously assigned range
    prev = arr[0]

    # Traverse the vector arr[]
    for i in range(1, N):

        last = arr[i - 1]
        current = arr[i]

        # Skip the similar ranges
        # of size 1
        if (last[0] == current[0]
            and last[1] == current[1]
                and current[1] == current[0]):
            continue

        # Find the range of integer
        # available to be assigned
        start = max(prev[0], current[0] - 1)
        end = max(prev[1], current[1])

        # Check if an integer is
        # available to be assigned
        if (end - start > 0):

            # Update the previously
            # assigned range
            prev[0] = 1 + start
            prev[1] = end

            # Update the count of range
            count += 1

    # Return the maximum count of
    # ranges
    return count

# Driver Code
if __name__ == "__main__":

    arr = [
        [1, 4], [4, 4],
        [2, 2], [3, 4],
        [1, 1]]
    N = len(arr)
    print(maxRanges(arr, N))

    # This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum number
// of ranges where each range can be
// uniquely represented by an integer
function maxRanges(arr, N) {
    // Sort the ranges in ascending order
    arr.sort((a, b) => {
        return b[0] - a[0]
    })

    // Stores the count of ranges
    let count = 1;

    // Stores previously assigned range
    let prev = arr[0];

    // Traverse the vector arr[]
    for (let i = 1; i < N; i++) {

        let last = arr[i - 1];
        let current = arr[i];

        // Skip the similar ranges
        // of size 1
        if (last[0] == current[0]
            && last[1] == current[1]
            && current[1] == current[0]) {
            continue;
        }
        // Find the range of integer
        // available to be assigned
        let start = Math.max(prev[0], current[0] - 1);
        let end = Math.max(prev[1], current[1]);

        // Check if an integer is
        // available to be assigned
        if ((end - start) > 0) {

            // Update the previously
            // assigned range
            prev[0] = 1 + start;
            prev[1] = end;

            // Update the count of range
            count++;
        }
    }

    // Return the maximum count of
    // ranges
    return count;
}

// Driver Code

let range = [
    [1, 4], [4, 4],
    [2, 2], [3, 4],
    [1, 1]];
let N = range.length;
document.write(maxRanges(range, N));

// This code is contributed by _Saurabh_jaiswal
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * log N)*
***辅助空间:*** *O(1)*