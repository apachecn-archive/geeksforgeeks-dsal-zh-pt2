# 对所有子阵列的相等元素的无序对进行计数

> 原文:[https://www . geeksforgeeks . org/count-无序-所有子阵列的相等元素对/](https://www.geeksforgeeks.org/count-unordered-pairs-of-equal-elements-for-all-subarrays/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出数组中无序对 **(i，j)** 的总数，使得给定数组的所有[子数组的**arr【I】**等于**arr【j】**和 **i < j** 。](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)

**示例:**

> **输入:** arr[] = {1，2，1，1}
> **输出:** 6
> **说明:**给定阵列中大于 1 的所有子阵列为:
> 
> 1.  **{1，2}:** 不存在满足给定标准的这样的对。因此，当前子阵列的对计数为 0。
> 2.  **{2，1}:** 不存在满足给定标准的这样的对。因此，当前子阵列的对计数为 0。
> 3.  **{1，1}:** 满足给定标准的对是(0，1)。因此，当前子阵列的对数是 1。
> 4.  **{1，2，1}:** 满足给定标准的对是(0，2)。因此，当前子阵列的对数是 1。
> 5.  **{2，1，1}:** 满足给定标准的对是(1，1)。因此，当前子阵列的对数是 1。
> 6.  **{1，2，1，1}:** 满足给定标准的对是(0，2)、(0，3)和(2，3)。因此，当前子阵列的对数是 3。
> 
> 因此，所有子阵列的总计数= 1 + 1 + 1 + 3 = 6。
> 
> **输入:** arr[] = {1，2，1，3}
> **输出:** 2

**天真法:**解决给定问题最简单的方法是生成所有可能的大小大于 1 的子阵列，并为给定阵列的所有可能的子阵列找到满足给定准则的对的计数之和。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**上述方法也可以通过将对应于每个不同元素的所有位置存储在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中来优化，然后，对于每个元素，遍历对应于该元素的位置，并计算每对出现的子阵列的数量。按照以下步骤解决问题:

*   初始化一个[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **M** 为一对，取值为一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)。
*   初始化另一个变量，比如说**和**为 **0** ，它存储满足给定标准的配对总数。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并将 **i** 的值附加到键**M【arr[I]】**上。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** ，执行以下步骤:
    *   初始化一个向量，说 **V** 作为当前键对应的值。
    *   初始化一个变量，说**将**求和为 **0** 。
    *   [遍历给定向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **V** 对于每个元素**V【j】**将**(总和*(N–V[j])的值)**添加到变量**和**并将值 **(V[j] + 1)** 添加到变量**总和**。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count all pairs (i, j)
// such that arr[i] equals arr[j] in
// all possible subarrays of the array
void countPairs(vector<int> arr)
{
    // Stores the size of the array
    int N = arr.size();
    int ans = 0;

    // Stores the positions of all
    // the distinct elements
    map<int, vector<int> > M;

    // Append index corresponding
    // to arr[i] in the map
    for (int i = 0;
         i < arr.size(); i++) {
        M[arr[i]].push_back(i);
    }

    // Traverse the map M
    for (auto it : M) {

        vector<int> v = it.second;
        int sum = 0;

        // Traverse the array
        for (int j = 0;
             j < v.size(); j++) {

            // Update the value of
            // ans
            ans += sum * (N - v[j]);

            // Update the value of
            // the sum
            sum += v[j] + 1;
        }
    }

    // Print the value of ans
    cout << ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 1, 1 };
    countPairs(arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
import java.util.List;
import com.google.common.collect.*;

class GFG {

    // Function to count all pairs (i, j)
    // such that arr[i] equals arr[j] in
    // all possible subarrays of the array
    static void countPairs(int[] arr)
    {
        // Stores the size of the array
        int N = arr.length;
        int ans = 0;

        // Stores the positions of all
        // the distinct elements
        ListMultimap<Integer, Integer> M = ArrayListMultimap.create();

        // Append index corresponding
        // to arr[i] in the map
        for (int i = 0;
             i < arr.length; i++) {
            M.put(arr[i], i);
        }

        // Traverse the map M
        for (var it: M.keySet()) {
            List<Integer> v = M.get(it);
            int sum = 0;

            // Traverse the array
            for (int j : v) {

                // Update the value of
                // ans
                ans += sum * (N - j);

                // Update the value of
                // the sum
                sum += j + 1;
            }
        }

        // Print the value of ans
        System.out.println(ans);
    }

    // Driver Code
    public static void main (String[] args) {
        int[] arr = { 1, 2, 1, 1 };
        countPairs(arr);
    }
}

// This Code is contributed by ShubhamSingh10
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count all pairs (i, j)
# such that arr[i] equals arr[j] in
# all possible subarrays of the array
def countPairs(arr):

    # Stores the size of the array
    N = len(arr)
    ans = 0

    # Stores the positions of all
    # the distinct elements
    M = {}

    # Append index corresponding
    # to arr[i] in the map
    for i in range(len(arr)):
        if arr[i] in M:
            M[arr[i]].append(i)
        else:
            M[arr[i]] = [i]

    # Traverse the map M
    for key, value in M.items():
        v = value
        sum1 = 0

        # Traverse the array
        for j in range(len(v)):

            # Update the value of
            # ans
            ans += (sum1 * (N - v[j]))

            # Update the value of
            # the sum
            sum1 += v[j] + 1

    # Print the value of ans
    print(ans)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 1, 1 ]

    countPairs(arr)

# This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count all pairs (i, j)
// such that arr[i] equals arr[j] in
// all possible subarrays of the array
function countPairs(arr) {
    // Stores the size of the array
    let N = arr.length;
    let ans = 0;

    // Stores the positions of all
    // the distinct elements
    let M = new Map();

    // Append index corresponding
    // to arr[i] in the map
    for (let i = 0; i < arr.length; i++) {
        if (M.has(arr[i])) {
            M.get(arr[i]).push(i);
        } else {
            M.set(arr[i], [i])
        }
    }

    // Traverse the map M
    for (let it of M) {

        let v = it[1];
        let sum = 0;

        // Traverse the array
        for (let j = 0; j < v.length; j++) {

            // Update the value of
            // ans
            ans += sum * (N - v[j]);

            // Update the value of
            // the sum
            sum += v[j] + 1;
        }
    }

    // Print the value of ans
    document.write(ans);
}

// Driver Code

let arr = [1, 2, 1, 1];
countPairs(arr);

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*