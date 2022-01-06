# 数组的每个索引要跳过的最小索引数，以保持总和，直到该索引最多为 T

> 原文:[https://www . geeksforgeeks . org/数组的每个索引都要跳过的最小索引数最多保留一个索引的总和/](https://www.geeksforgeeks.org/minimum-count-of-indices-to-be-skipped-for-every-index-of-array-to-keep-sum-till-that-index-at-most-t/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** 和一个整数 **T** 。任务是为每个指标找到最小数量的指标，如果直到**与**指标的总和不超过 **T** ，则应跳过这些指标。

**示例:**

> **输入:** N = 7，T = 15，arr[] = {1，2，3，4，5，6，7}
> **输出:**0 0 0 0 2 3
> **说明:**前 5 个指数不需要跳过指数:{1，2，3，4，5}，因为它们的和是 15，< = T.
> 对于第六个指数，指数 3 和 4 可以跳过，所以它的和=(1+2+5)
> 对于第七个，可以跳过索引 3、4 和 5，这样它的和= (1+2+3+7) = 13。
> 
> **输入:**N =**T3】2，T = 100，arr[] = {100，100 }
> T5】输出:** 0 1

**方法:**想法是在遍历时使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)以递增的顺序存储访问过的元素。按照以下步骤解决问题:

*   创建一个[有序地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)、 **M** 来记录带有索引的**之前的元素数量。**
*   将变量**和**初始化为 **0** 来存储前缀和。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]**
    *   将**和+arr【I】**与 **T** 的差值存储在变量 **d** 中。
    *   如果 **d > 0** ，[的值从终点](https://www.geeksforgeeks.org/how-to-traverse-a-stl-map-in-reverse-direction/)开始遍历地图，选择元素最大的索引，直到总和小于 **T** 。将所需元素的数量存储在变量 **k** 中。
    *   将 **M** 中的**A【I】**相加**arr【I】**加 **1** 。
    *   打印 **k** 的值。

下面是上述方法的实现:

## C++

```
// C++ approach for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum indices to be skipped
// so that sum till i remains smaller than T
void skipIndices(int N, int T, int arr[])
{
    // Store the sum of all indices before i
    int sum = 0;

    // Store the elements that can be skipped
    map<int, int> count;

    // Traverse the array, A[]
    for (int i = 0; i < N; i++) {

        // Store the total sum of elements that
        // needs to be skipped
        int d = sum + arr[i] - T;

        // Store the number of elements need
        // to be removed
        int k = 0;

        if (d > 0) {

            // Traverse from the back of map so
            // as to take bigger elements first
            for (auto u = count.rbegin(); u != count.rend();
                 u++) {
                int j = u->first;
                int x = j * count[j];
                if (d <= x) {
                    k += (d + j - 1) / j;
                    break;
                }
                k += count[j];
                d -= x;
            }
        }

        // Update sum
        sum += arr[i];

        // Update map with the current element
        count[arr[i]]++;

        cout << k << " ";
    }
}

// Driver code
int main()
{
    // Given Input
    int N = 7;
    int T = 15;
    int arr[] = { 1, 2, 3, 4, 5, 6, 7 };

    // Function Call
    skipIndices(N, T, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.ArrayList;
import java.util.Map;
import java.util.TreeMap;

// C++ approach for above approach

class GFG {
    // Function to calculate minimum indices to be skipped
    // so that sum till i remains smaller than T
public static void skipIndices(int N, int T, int arr[])
{
    // Store the sum of all indices before i
    int sum = 0;

    // Store the elements that can be skipped
    TreeMap<Integer, Integer> count = new TreeMap<Integer, Integer>();

    // Traverse the array, A[]
    for (int i = 0; i < N; i++) {

        // Store the total sum of elements that
        // needs to be skipped
        int d = sum + arr[i] - T;

        // Store the number of elements need
        // to be removed
        int k = 0;

        if (d > 0) {

            // Traverse from the back of map so
            // as to take bigger elements first
            for (Map.Entry<Integer, Integer> u : count.descendingMap().entrySet()) {
                int j = u.getKey();
                int x = j * count.get(j);
                if (d <= x) {
                    k += (d + j - 1) / j;
                    break;
                }
                k += count.get(j);
                d -= x;
            }
        }

        // Update sum
        sum += arr[i];

        // Update map with the current element
        if(count.containsKey(arr[i])){
            count.put(arr[i], count.get(arr[i]) + 1);
        }else{
            count.put(arr[i], 1);
        }

        System.out.print(k + " ");
    }
}

    // Driver code
    public static void main(String args[])
    {

        // Given Input
        int N = 7;
        int T = 15;
        int arr[] = { 1, 2, 3, 4, 5, 6, 7 };

        // Function Call
        skipIndices(N, T, arr);
    }

}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 approach for above approach

# Function to calculate minimum indices to be skipped
# so that sum till i remains smaller than T
def skipIndices(N, T, arr):
    # Store the sum of all indices before i
    sum = 0

    # Store the elements that can be skipped
    count = {}

    # Traverse the array, A[]
    for i in range(N):

        # Store the total sum of elements that
        # needs to be skipped
        d = sum + arr[i] - T

        # Store the number of elements need
        # to be removed
        k = 0

        if (d > 0):

            # Traverse from the back of map so
            # as to take bigger elements first
            for u in list(count.keys())[::-1]:
                j = u
                x = j * count[j]
                if (d <= x):
                    k += (d + j - 1) // j
                    break
                k += count[j]
                d -= x

        # Update sum
        sum += arr[i]

        # Update map with the current element
        count[arr[i]] = count.get(arr[i], 0) + 1

        print(k, end = " ")
# Driver code
if __name__ == '__main__':
    # Given Input
    N = 7
    T = 15
    arr = [1, 2, 3, 4, 5, 6, 7]

    # Function Call
    skipIndices(N, T, arr)

    # This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>

// Javascript approach for above approach

// Function to calculate minimum indices
// to be skipped so that sum till i
// remains smaller than T
function skipIndices(N, T, arr)
{

    // Store the sum of all indices before i
    let sum = 0;

    // Store the elements that can be skipped
    let count = new Map();

    // Traverse the array, A[]
    for(let i = 0; i < N; i++)
    {

        // Store the total sum of elements that
        // needs to be skipped
        let d = sum + arr[i] - T;

        // Store the number of elements need
        // to be removed
        let k = 0;

        if (d > 0)
        {

            // Traverse from the back of map so
            // as to take bigger elements first
            for(let u of [...count.keys()].reverse())
            {
                let j = u;
                let x = j * count.get(j);

                if (d <= x)
                {
                    k += Math.floor((d + j - 1) / j);
                    break;
                }
                k += count.get(j);
                d -= x;
            }
        }

        // Update sum
        sum += arr[i];

        // Update map with the current element
        if (count.has(arr[i]))
        {
            count.set(arr[i], count.get(i) + 1)
        }
        else
        {
            count.set(arr[i], 1)
        }
        document.write(k + " ");
    }
}

// Driver code

// Given Input
let N = 7;
let T = 15;
let arr = [ 1, 2, 3, 4, 5, 6, 7 ];

// Function Call
skipIndices(N, T, arr);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output**

```
0 0 0 0 0 2 3 
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间** : O(N)*