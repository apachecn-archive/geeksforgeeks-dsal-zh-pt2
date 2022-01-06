# 找到一个数组 B，其中 B 中至少有 arr[i]个元素不等于 B[i]

> 原文:[https://www . geeksforgeeks . org/find-a-array-b-with-arri-elements-in-b-不等于-bi/](https://www.geeksforgeeks.org/find-an-array-b-with-at-least-arri-elements-in-b-not-equal-to-the-bi/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到一个大小为 **N** 的数组，这样对于数组 **arr【】的每个**I**元素，**输出数组应该至少包含不等于输出的 **i <sup>th</sup>** 元素的**arr【I】**元素如果不存在这样的数组，那么打印“**不可能**”。

**示例:**

> **输入:** N = 5，arr[] = {4，4，4，4，4}
> **输出:** 1 2 3 4 5
> 
> **输入:** N = 10，arr[] = {7，7，7，7，9，8，8，7，9 }
> T3】输出:4 4 5 1 3 5 2

**方法:**给定的问题可以基于这样的观察来解决，即应该有最大数量的**N-arr【I】**元素等于输出数组的 **i <sup>th</sup>** 元素。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)，比如说 **res[]** 大小 **N+5，**来存储输出数组。
*   另外，初始化一个对的[数组](https://www.geeksforgeeks.org/given-an-array-of-pairs-find-all-symmetric-pairs-in-it/)，比如大小为 **N+5 的 **V** ，其中**V【I】**存储等于**RES【I】**的元素计数对，以及索引 **i.****
*   [使用变量 **i、**在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**中迭代，并在每次迭代中将对 **{N-arr[i]，i}** 的值赋给 **V[i]。**
*   [按升序对配对数组](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)进行排序。
*   初始化两个变量，说 **l** 和 **r** 为 **0** 到[遍历数组。](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
*   [使用变量 **l** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**，并执行以下步骤:
    *   [使用变量 **r** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【l，N-1】**，并执行以下操作:
        *   如果 **V[r + 1]。首先**不等于**V【r】。先**，再破环。
    *   如果相同元素的计数即 **(r-l+1)** 不能被**V【l】整除。先**再打印“**不可能**”返回。
    *   初始化一个变量，比如说 **X** ，作为 **1** 来给数组 **res[]赋值。**
    *   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【l，r】**，并执行以下步骤:
        *   迭代范围 **[i，i+V[l]。首先]使用变量 **j** 进行**，然后在每次迭代中将 **X** 指定给 **res[V[j]。第二】**。
        *   将 **i** 增加**V【l】。先将**和 **X** 换成 **1** 。
    *   将 **l** 的值更新为 **r+1** 。
*   最后，完成以上步骤后，[打印数组，](https://www.geeksforgeeks.org/c-program-to-print-an-array-using-recursion/)T2】RES[]。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the possible
// output array
void findPossibleArray(int N, int arr[])
{
    pair<int, int> V[N + 5];

    // Stores the output array
    int res[N + 5];

    int cnt = 0;
    // Iterate over the range [1, N]
    for (int i = 0; i < N; i++) {
        // Update V[i]
        V[i].first = N - arr[i];
        V[i].second = i;
    }

    // Sort the the array
    sort(V, V + N);

    // Iterate in the range [1, N]
    for (int l = 0, r = 0; l < N; l = r + 1) {

        // Iterate until r is less than N
        for (r = l; r < N - 1; ++r) {

            // If V[i+1].first is equal to
            // V[r].first
            if (V[r + 1].first != V[r].first) {
                break;
            }
        }

        // If r-l+1 is divisible by V[i].first
        if ((r - l + 1) % V[l].first) {
            cout << "Impossible" << endl;
            return;
        }

        // Otherwise,
        for (int i = l; i <= r; i += V[l].first) {
            cnt++;
            // Traverse the array over the range
            // [i, i+V[l].second]
            for (int j = i; j < i + V[l].first && j < N;
                 ++j)
                res[V[j].second] = cnt;
        }
    }

    // Print the array res[]
    for (int i = 0; i < N; i++)
        cout << res[i] << ' ';
}

// Driver Code
int main()
{

    int arr[] = { 4, 4, 4, 4, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    findPossibleArray(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG {

    // Function to find the possible
    // output array
    public static void findPossibleArray(int N, int arr[]) {
        int[][] V = new int[N][2];

        // Stores the output array
        int[] res = new int[N + 5];

        int cnt = 0;
        // Iterate over the range [1, N]
        for (int i = 0; i < N; i++) {
            // Update V[i]
            V[i][0] = N - arr[i];
            V[i][1] = i;
        }

        // Sort the the array
        Arrays.sort(V, (a, b) -> a[0] - b[0]);

        // Iterate in the range [1, N]
        for (int l = 0, r = 0; l < N; l = r + 1) {

            // Iterate until r is less than N
            for (r = l; r < N - 1; ++r) {

                // If V[i+1][0] is equal to
                // V[r][0]
                if (V[r + 1][0] != V[r][0]) {
                    break;
                }
            }

            // If r-l+1 is divisible by V[i][0]
            if (V[l][0] == 0 || ((r - l + 1) % V[l][0]) > 0) {
                System.out.println("Impossible");
                return;
            }

            // Otherwise,
            for (int i = l; i <= r; i += V[l][0]) {
                cnt++;
                // Traverse the array over the range
                // [i, i+V[l][1]]
                for (int j = i; j < i + V[l][0] && j < N; ++j)
                    res[V[j][1]] = cnt;
            }
        }

        // Print the array res[]
        for (int i : res) {
            if (i > 0) {
                System.out.print(i + " ");
            }
        }
    }

    // Driver Code
    public static void main(String args[]) {

        int arr[] = { 4, 4, 4, 4, 4 };
        int N = arr.length;

        findPossibleArray(N, arr);
    }
}

//This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the possible
// output array
function findPossibleArray(N, arr)
{
    let V = new Array(N + 5).fill(0).map(() => new Array(2));

    // Stores the output array
    let res = new Array(N + 5);

    let cnt = 0;

    // Iterate over the range [1, N]
    for (let i = 0; i < N; i++)
    {

        // Update V[i]
        V[i][0] = N - arr[i];
        V[i][1] = i;
    }

    // Sort the the array
    V.sort((a, b) => a[0] - b[0]);

    // Iterate in the range [1, N]
    for (let l = 0, r = 0; l < N; l = r + 1) {

        // Iterate until r is less than N
        for (r = l; r < N - 1; ++r) {

            // If V[i+1][0] is equal to
            // V[r][0]
            if (V[r + 1][0] != V[r][0]) {
                break;
            }
        }

        // If r-l+1 is divisible by V[i][0]
        if ((r - l + 1) % V[l][0]) {
            document.write("Impossible" + "<br>");
            return;
        }

        // Otherwise,
        for (let i = l; i <= r; i += V[l][0]) {
            cnt++;
            // Traverse the array over the range
            // [i, i+V[l][1]]
            for (let j = i; j < i + V[l][0] && j < N; ++j)
                res[V[j][1]] = cnt;
        }
    }

    // Print the array res[]
    for (let i = 0; i < N; i++)
        document.write(res[i] + ' ');
}

// Driver Code
let arr = [4, 4, 4, 4, 4];
let N = arr.length

findPossibleArray(N, arr);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
1 2 3 4 5 
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*