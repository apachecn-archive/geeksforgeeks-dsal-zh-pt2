# 最小化相邻阵列元素间绝对差之和所需的最小交换次数

> 原文:[https://www . geeksforgeeks . org/最小交换次数-需要最小化相邻数组元素之间的绝对差之和/](https://www.geeksforgeeks.org/minimum-number-of-swaps-required-to-minimize-sum-of-absolute-differences-between-adjacent-array-elements/)

给定一个由 **N** 个不同正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到需要交换的最小元素数，以最小化每对相邻元素的绝对差之和[。](https://www.geeksforgeeks.org/sum-absolute-differences-pairs-given-array/)

**示例:**

> **输入:** arr[] = {8，50，11，2}
> **输出:** 2
> **解释:**
> **操作 1:** 交换元素 8 和 2，将数组 arr[]修改为{2，50，11，8}。
> **操作 2:** 交换元素 8 和 50，将数组 arr[]修改为{2，8，11，50}。
> 修改后数组相邻元素的绝对差之和为 48，最小。
> 因此，要求的最少互换次数为 2 次。
> 
> **输入:** arr[] = {3，4，2，5，1}
> **输出:** 2

**方法:**给定的问题可以基于这样的观察来解决，即如果[数组按照升序或降序排序，相邻元素的绝对差之和将最小。](https://www.geeksforgeeks.org/check-if-an-array-is-increasing-or-decreasing/)按照步骤解决问题。

*   使用本文中讨论的方法，找到按升序排列给定数组所需的最小交换次数。让伯爵成为 **S1** 。
*   使用本文中讨论的方法，找到按降序对给定数组进行排序所需的最小交换次数[。让伯爵成为 **S2** 。](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)
*   完成上述步骤后，打印值 **S1** 和 **S2** 中的最小值，作为所需交换的最小数量。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Comparator to sort in the descending
// order
bool mycmp(pair<int, int> a,
           pair<int, int> b)
{
    return a.first > b.first;
}

// Function to find the minimum number
// of swaps required to sort the array
// in increasing order
int minSwapsAsc(vector<int> arr, int n)
{
    // Stores the array elements with
    // its index
    pair<int, int> arrPos[n];
    for (int i = 0; i < n; i++) {
        arrPos[i].first = arr[i];
        arrPos[i].second = i;
    }

    // Sort the array in the
    // increasing order
    sort(arrPos, arrPos + n);

    // Keeps the track of
    // visited elements
    vector<bool> vis(n, false);

    // Stores the count of swaps required
    int ans = 0;

    // Traverse array elements
    for (int i = 0; i < n; i++) {

        // If the element is already
        // swapped or at correct position
        if (vis[i] || arrPos[i].second == i)
            continue;

        // Find out the number of
        // nodes in this cycle
        int cycle_size = 0;

        // Update the value of j
        int j = i;

        while (!vis[j]) {
            vis[j] = 1;

            // Move to the next element
            j = arrPos[j].second;

            // Increment cycle_size
            cycle_size++;
        }

        // Update the ans by adding
        // current cycle
        if (cycle_size > 0) {
            ans += (cycle_size - 1);
        }
    }

    return ans;
}

// Function to find the minimum number
// of swaps required to sort the array
// in decreasing order
int minSwapsDes(vector<int> arr, int n)
{
    // Stores the array elements with
    // its index
    pair<int, int> arrPos[n];

    for (int i = 0; i < n; i++) {
        arrPos[i].first = arr[i];
        arrPos[i].second = i;
    }

    // Sort the array in the
    // descending order
    sort(arrPos, arrPos + n, mycmp);

    // Keeps track of visited elements
    vector<bool> vis(n, false);

    // Stores the count of resultant
    // swap required
    int ans = 0;

    // Traverse array elements
    for (int i = 0; i < n; i++) {

        // If the element is already
        // swapped or at correct
        // position
        if (vis[i] || arrPos[i].second == i)
            continue;

        // Find out the number of
        // node in this cycle
        int cycle_size = 0;

        // Update the value of j
        int j = i;

        while (!vis[j]) {

            vis[j] = 1;

            // Move to the next element
            j = arrPos[j].second;

            // Increment the cycle_size
            cycle_size++;
        }

        // Update the ans by adding
        // current cycle size
        if (cycle_size > 0) {
            ans += (cycle_size - 1);
        }
    }

    return ans;
}

// Function to find minimum number of
// swaps required to minimize the sum
// of absolute difference of adjacent
// elements
int minimumSwaps(vector<int> arr)
{
    // Sort in ascending order
    int S1 = minSwapsAsc(arr, arr.size());

    // Sort in descending order
    int S2 = minSwapsDes(arr, arr.size());

    // Return the minimum value
    return min(S1, S2);
}

// Drive Code
int main()
{
    vector<int> arr{ 3, 4, 2, 5, 1 };
    cout << minimumSwaps(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.lang.*;
import java.util.*;

// Pair class
class pair
{
    int first, second;
    pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

class GFG{

// Function to find the minimum number
// of swaps required to sort the array
// in increasing order
static int minSwapsAsc(int[] arr, int n)
{

    // Stores the array elements with
    // its index
    pair[] arrPos = new pair[n];
    for(int i = 0; i < n; i++)
    {
        arrPos[i] = new pair(arr[i], i);
    }

    // Sort the array in the
    // increasing order
    Arrays.sort(arrPos, (a, b)-> a.first - b.first);

    // Keeps the track of
    // visited elements
    boolean[] vis= new boolean[n];

    // Stores the count of swaps required
    int ans = 0;

    // Traverse array elements
    for(int i = 0; i < n; i++)
    {

        // If the element is already
        // swapped or at correct position
        if (vis[i] || arrPos[i].second == i)
            continue;

        // Find out the number of
        // nodes in this cycle
        int cycle_size = 0;

        // Update the value of j
        int j = i;

        while (!vis[j])
        {
            vis[j] = true;

            // Move to the next element
            j = arrPos[j].second;

            // Increment cycle_size
            cycle_size++;
        }

        // Update the ans by adding
        // current cycle
        if (cycle_size > 0)
        {
            ans += (cycle_size - 1);
        }
    }
    return ans;
}

// Function to find the minimum number
// of swaps required to sort the array
// in decreasing order
static int minSwapsDes(int[] arr, int n)
{

    // Stores the array elements with
    // its index
    pair[] arrPos = new pair[n];

    for(int i = 0; i < n; i++)
    {
        arrPos[i] = new pair(arr[i], i);
    }

    // Sort the array in the
    // descending order
    Arrays.sort(arrPos, (a, b)-> b.first - a.first);

    // Keeps track of visited elements
    boolean[] vis = new boolean[n];

    // Stores the count of resultant
    // swap required
    int ans = 0;

    // Traverse array elements
    for(int i = 0; i < n; i++)
    {

        // If the element is already
        // swapped or at correct
        // position
        if (vis[i] || arrPos[i].second == i)
            continue;

        // Find out the number of
        // node in this cycle
        int cycle_size = 0;

        // Update the value of j
        int j = i;

        while (!vis[j])
        {

            vis[j] = true;

            // Move to the next element
            j = arrPos[j].second;

            // Increment the cycle_size
            cycle_size++;
        }

        // Update the ans by adding
        // current cycle size
        if (cycle_size > 0)
        {
            ans += (cycle_size - 1);
        }
    }
    return ans;
}

// Function to find minimum number of
// swaps required to minimize the sum
// of absolute difference of adjacent
// elements
static int minimumSwaps(int[] arr)
{

    // Sort in ascending order
    int S1 = minSwapsAsc(arr, arr.length);

    // Sort in descending order
    int S2 = minSwapsDes(arr, arr.length);

    // Return the minimum value
    return Math.min(S1, S2);
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 3, 4, 2, 5, 1 };
    System.out.println(minimumSwaps(arr));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# of swaps required to sort the array
# in increasing order
def minSwapsAsc(arr, n):

    # Stores the array elements with
    # its index
    arrPos = [[arr[i], i] for i in range(n)]

    # Sort the array in the
    # increasing order
    arrPos = sorted(arrPos)

    # Keeps the track of
    # visited elements
    vis = [False] * (n)

    # Stores the count of swaps required
    ans = 0

    # Traverse array elements
    for i in range(n):

        # If the element is already
        # swapped or at correct position
        if (vis[i] or arrPos[i][1] == i):
            continue

        # Find out the number of
        # nodes in this cycle
        cycle_size = 0

        # Update the value of j
        j = i

        while (not vis[j]):
            vis[j] = 1

            # Move to the next element
            j = arrPos[j][1]

            # Increment cycle_size
            cycle_size += 1

        # Update the ans by adding
        # current cycle
        if (cycle_size > 0):
            ans += (cycle_size - 1)

    return ans

# Function to find the minimum number
# of swaps required to sort the array
# in decreasing order
def minSwapsDes(arr, n):

    # Stores the array elements with
    # its index
    arrPos = [[0, 0] for i in range(n)]

    for i in range(n):
        arrPos[i][0] = arr[i]
        arrPos[i][1] = i

    # Sort the array in the
    # descending order
    arrPos = sorted(arrPos)[::-1]

    # Keeps track of visited elements
    vis = [False] * n

    # Stores the count of resultant
    # swap required
    ans = 0

    # Traverse array elements
    for i in range(n):

        # If the element is already
        # swapped or at correct
        # position
        if (vis[i] or arrPos[i][1] == i):
            continue

        # Find out the number of
        # node in this cycle
        cycle_size = 0

        # Update the value of j
        j = i

        while (not vis[j]):
            vis[j] = 1

            # Move to the next element
            j = arrPos[j][1]

            # Increment the cycle_size
            cycle_size += 1

        # Update the ans by adding
        # current cycle size
        if (cycle_size > 0):
            ans += (cycle_size - 1)

    return ans

# Function to find minimum number of
# swaps required to minimize the sum
# of absolute difference of adjacent
# elements
def minimumSwaps(arr):

    # Sort in ascending order
    S1 = minSwapsAsc(arr, len(arr))

    # Sort in descending order
    S2 = minSwapsDes(arr, len(arr))

    # Return the minimum value
    return min(S1, S2)

# Drive Code
if __name__ == '__main__':

    arr = [ 3, 4, 2, 5, 1 ]
    print (minimumSwaps(arr))

# This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>
        // Javascript program for the above approach

        // Comparator to sort in the descending
        // order
        function mycmp(a, b) {
            return a[0] > b[0];
        }

        // Function to find the minimum number
        // of swaps required to sort the array
        // in increasing order
        function minSwapsAsc(arr, n) {
            // Stores the array elements with
            // its index
            let arrPos = new Array(n);
            for (let i = 0; i < n; i++)
                arrPos[i] = new Array(2);

            for (let i = 0; i < n; i++) {
                arrPos[i][0] = arr[i];
                arrPos[i][1] = i;
            }

            // Sort the array in the
            // increasing order
            arrPos.sort(function (a, b) { return a[0] - b[0] })

            // Keeps the track of
            // visited elements
            let vis = new Array(n);
            for (let i = 0; i < n; i++)
                vis[i] = false

            // Stores the count of swaps required
            let ans = 0;

            // Traverse array elements
            for (let i = 0; i < n; i++) {

                // If the element is already
                // swapped or at correct position
                if (vis[i] || arrPos[i][1] == i)
                    continue;

                // Find out the number of
                // nodes in this cycle
                let cycle_size = 0;

                // Update the value of j
                let j = i;

                while (!vis[j]) {
                    vis[j] = 1;

                    // Move to the next element
                    j = arrPos[j][1];

                    // Increment cycle_size
                    cycle_size++;
                }

                // Update the ans by adding
                // current cycle
                if (cycle_size > 0) {
                    ans += (cycle_size - 1);
                }
            }

            return ans;
        }

        // Function to find the minimum number
        // of swaps required to sort the array
        // in decreasing order
        function minSwapsDes(arr, n) {
            // Stores the array elements with
            // its index
            let arrPos = new Array(n);
            for (let i = 0; i < n; i++)
                arrPos[i] = new Array(2);

            for (let i = 0; i < n; i++) {
                arrPos[i][0] = arr[i];
                arrPos[i][1] = i;
            }

            // Sort the array in the
            // descending order
            arrPos.sort(function (a, b) { return b[0] - a[0] })

            // Keeps track of visited elements
            let vis = new Array(n);
            for (let i = 0; i < n; i++)
                vis[i] = false

            // Stores the count of resultant
            // swap required
            let ans = 0;

            // Traverse array elements
            for (let i = 0; i < n; i++) {

                // If the element is already
                // swapped or at correct
                // position
                if (vis[i] || arrPos[i][1] == i)
                    continue;

                // Find out the number of
                // node in this cycle
                let cycle_size = 0;

                // Update the value of j
                let j = i;

                while (!vis[j]) {

                    vis[j] = 1;

                    // Move to the next element
                    j = arrPos[j][1];

                    // Increment the cycle_size
                    cycle_size++;
                }

                // Update the ans by adding
                // current cycle size
                if (cycle_size > 0) {
                    ans += (cycle_size - 1);
                }
            }

            return ans;
        }

        // Function to find minimum number of
        // swaps required to minimize the sum
        // of absolute difference of adjacent
        // elements
        function minimumSwaps(arr) {
            // Sort in ascending order
            let S1 = minSwapsAsc(arr, arr.length);

            // Sort in descending order
            let S2 = minSwapsDes(arr, arr.length);

            // Return the minimum value
            return Math.min(S1, S2);
        }

        // Drive Code

        let arr = [ 3, 4, 2, 5, 1 ];
        document.write(minimumSwaps(arr));

        // This code is contributed by Hritik
    </script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*