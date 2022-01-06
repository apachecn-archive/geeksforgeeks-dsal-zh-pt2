# 分割数组的最小组，使得它们的每对值差和位置差相同

> 原文:[https://www . geeksforgeeks . org/最小分组拆分数组，这样它们的每对值差和位置差都是相同的/](https://www.geeksforgeeks.org/minimum-groups-to-split-array-such-that-their-each-pair-value-difference-and-position-difference-are-same/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是将数组分割成最小数量的不相交的组，使得一个组中任意一对元素之间的差异等于它们在该组中的位置差异。

**示例:**

> **输入:** arr[] = {30，32，44，31，45，32，31，33}
> **输出:** 3
> **解释:**
> 拆分数组的一种可能方式是:
> 
> *   第一组:{30，31，32，33}
> *   第二组:{31，32}
> *   第三组:{44，45}
> 
> 因此，组的数量是 3，这是满足条件的阵列可以被分割的最小组的数量。
> 
> **输入:** arr[] = {1，5，3，1，7，7，9 }
> T3】输出: 7

**天真法:**最简单的方法是，[将数组拆分成 K 个子集](https://www.geeksforgeeks.org/print-all-possible-ways-to-split-an-array-into-k-subsets/)对于每一个小于等于 **N** 的整数 **K** ，然后检查数组的所有子集是否满足给定条件。如果发现为真，则打印分区的最小大小。

***时间复杂度:**O(N<sup>(N+2)</sup>)*
***辅助空间:** O(N)*

**高效途径:**上述途径可以基于观察到每组中的元素必须是[排序的](https://www.geeksforgeeks.org/sorting-algorithms/)，相邻元素之间的差异应该是 **1** 进行优化。按照以下步骤解决问题:

*   [给定数组按升序排序。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   初始化一张[图，](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)说 **mp** 存储数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   初始化一个变量，说**计数**为 **0** 存储形成的不相交组的最小数量的计数。
*   [遍历给定数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**，增加地图中每个元素的频率 **mp** 。**
*   **[使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]、【T3]，并执行以下步骤:**

    *   如果地图 **mp** 中 **arr[i]** 的计数至少为 **1** ，地图 **mp** 中**(arr[I]–1)**的计数则:
        *   将**计数**的值增加 **1** 。
        *   [迭代直到](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)在 **mp** 中**arr【I】**的计数大于 **0** ，在每次迭代中，将**MP【arr【I】】**递减 **1** 并将**arr【I】**递增 **1** 。** 
*   **最后，完成以上步骤后，打印**计数**的值作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to split the array into
// minimum number of disjoint groups
// satisfying the conditions
int numberOfSplit(int arr[], int N)
{
    // Sort the array in ascending order
    sort(arr, arr + N);

    // Stores frequency of array elements
    unordered_map<int, int> mp;

    // Traverse the array, arr[]
    for (int i = 0; i < N; i++)
        mp[arr[i]]++;

    // Stores the number of groups
    int count = 0;

    // Traverse the array, arr[]
    for (int i = 0; i < N; i++) {

        // If mp[arr[i]] is at least 1
        // and  mp[arr[i]-1] is 0
        if (mp[arr[i]] > 0 && mp[arr[i] - 1] == 0) {

            // Increment the count by 1
            count++;

            // Iterate until mp[arr[i]]
            // is greater than 0
            while (mp[arr[i]] != 0) {

                // Decrement mp[arr[i]]
                // by 1
                mp[arr[i]]--;

                // Increment arr[i] by 1
                arr[i]++;
            }
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 30, 32, 44, 31, 45, 32, 31, 33 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << numberOfSplit(arr, N);

    return 0;
}
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to split the array into
// minimum number of disjoint groups
// satisfying the conditions
static int numberOfSplit(int []arr, int N)
{

    // Sort the array in ascending order
    Array.Sort(arr);

    // Stores frequency of array elements
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse the array, arr[]
    for(int i = 0; i < N; i++)
    {
        if (mp.ContainsKey(arr[i]))
            mp[arr[i]] += 1;
        else
            mp.Add(arr[i], 0);
    }

    // Stores the number of groups
    int count = 2;

    // Traverse the array, arr[]
    for(int i = 0; i < N; i++)
    {

        // If mp[arr[i]] is at least 1
        // and  mp[arr[i]-1] is 0
        if (mp[arr[i]] > 0 && mp[arr[i] - 1] == 0)
        {

            // Increment the count by 1
            count++;

            // Iterate until mp[arr[i]]
            // is greater than 0
            while (mp[arr[i]] != 0)
            {

                // Decrement mp[arr[i]]
                // by 1
                mp[arr[i]]--;

                // Increment arr[i] by 1
                arr[i]++;
            }
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
public static void Main()
{
    int []arr = { 30, 32, 44, 31,
                  45, 32, 31, 33 };
    int N = arr.Length;

    Console.Write(numberOfSplit(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to split the array into
// minimum number of disjoint groups
// satisfying the conditions
function numberOfSplit(arr, N)
{
    // Sort the array in ascending order
    arr.sort();

    // Stores frequency of array elements
    var mp = new Map();

    // Traverse the array, arr[]
    for (var i = 0; i < N; i++)
    {
        if(mp.has(arr[i]))
         mp.set(arr[i], mp.get(arr[i])+1)
        else
         mp.set(arr[i], 1)
    }

    // Stores the number of groups
    var count = 0;

    // Traverse the array, arr[]
    for (var i = 0; i < N; i++) {

        // If mp[arr[i]] is at least 1
        // and  mp[arr[i]-1] is 0
        if (mp.has(arr[i]) && mp.get(arr[i])>0 && (!mp.has(arr[i] - 1) || (mp.has(arr[i]-1) && mp.get(arr[i]-1)==0))) {

            // Increment the count by 1
            count++;

            // Iterate until mp[arr[i]]
            // is greater than 0
            while (mp.get(arr[i]) > 0) {

                // Decrement mp[arr[i]]
                // by 1
                mp.set(arr[i], mp.get(arr[i])-1);

                // Increment arr[i] by 1
                arr[i]++;
            }
        }
    }

    // Return the resultant count
    return count;
}

// Driver Code
var arr = [30, 32, 44, 31, 45, 32, 31, 33];
var N = arr.length;
document.write(numberOfSplit(arr, N));

// This code is contributed by itsok.
</script>
```

****Output**

```
3
```** 

*****时间复杂度:** O(N*log N)*
***辅助空间:** O(N)***