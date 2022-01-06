# 最多 K 次变化后，最大化数组中不同元素的数量

> 原文:[https://www . geeksforgeeks . org/最多 k 次更改后最大化数组中不同元素的数量/](https://www.geeksforgeeks.org/maximize-the-count-of-distinct-elements-in-array-after-at-most-k-changes/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是在**最多 K 次变化后找到 **arr** 中不同数字的最大个数。**在每次更改中，从 **arr** 中选择任意元素 **X** ，并将其更改为 **Y** ，使得 **L < = Y < = R** 。

示例:

> **输入:** arr[] = {1，2，1，4，6，4，4}，L = 1，R = 5 和 K = 2
> T3】输出:6
> T6】解释:
> 
> 以下是对给定数组元素执行的操作:
> 
> 1.将 arr[2]更改为 3 会将数组修改为{1，2，3，4，6，4，4}
> 2。将 arr[3]到 5 的 modies 数组更改为{1，2，3，5，6，4，4}
> 
> 由于 K = 2，不能再做任何改变
> 因此，distinct 元素为{1，2，3，5，6，4}，最大 Distinct 元素数为 6。
> 
> **输入:** arr[] = {1，2，1，4，6，4，4}，L = 1，R = 5 和 K = 1
> T3】输出:5
> T6】解释:
> 
> 以下是对给定数组元素执行的操作:
> 
> 1.将 arr[2]更改为 3 会将数组修改为{1，2，3，4，6，4，4}
> 
> 由于 K = 1，不能再做任何改变
> 因此，distinct 元素为{1，2，3，6，4}，最大 Distinct 元素个数为 5。

**方法:**这个问题可以通过使用[无序地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)来解决。存储地图中所有元素的频率，然后从 **L** 遍历到 **R** ，看看哪个数字还没有出现在地图中，我们可以用这个数字来替换 **arr** 中的任何重复元素。

*   首先，存储地图中所有元素的频率。
*   不同元素的总数将等于地图的大小。
*   额外元素的数量将等于**(数组大小–地图大小)**。
*   然后从 **L** 迭代到 **R** ，检查这个范围内有多少元素可以用来替换数组中存在的额外元素。
*   将任何额外元素的每次更改映射更新为任何其他值。
*   最后，地图的大小将包含所有不同的元素。
*   返回地图的大小作为答案。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate
// maximum distinct elements possible
// after at most K changes
int maxDistinctElements(int* arr, int K,
                        int L, int R, int n)
{
    // Map to store frequency of all the elements
    unordered_map<int, int> frequency;

    // Count frequency of each element
    for (int x = 0; x < n; x++) {
        frequency[arr[x]] += 1;
    }

    // To store number of extra elements
    // that needs to be changed
    int extra = (n - frequency.size());

    // Traverse from L to R
    // and see which number is not
    // present in map, use that number
    // to change extra duplicate element
    for (int i = L;
         i <= R and K != 0 and extra != 0;
         i++) {
        if (!frequency[i]) {
            frequency[i] = 1;
            K--;
            extra--;
        }
    }

    // Total distinct element will be equal
    // to the size of updated frequency map.
    int ans = frequency.size();

    // Return answer
    return ans;
}

// Driver Code
int main()
{
    // Test case 1
    int N = 7, L = 1, R = 5, K = 2;
    int arr[7] = { 1, 2, 1, 4, 6, 4, 4 };
    cout << maxDistinctElements(arr, K, L, R, N)
         << endl;

    // Test case 2
    K = 1;
    cout << maxDistinctElements(arr, K, L, R, N)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG {

    // Function to calculate
    // maximum distinct elements possible
    // after at most K changes
    static int maxDistinctElements(int[] arr, int K, int L, int R, int n)
    {

        // Map to store frequency of all the elements
        HashMap<Integer, Integer> frequency = new HashMap<Integer, Integer>();

        // Count frequency of each element
        for (int x = 0; x < n; x++) {
            if (frequency.containsKey(arr[x])) {
                frequency.put(arr[x], frequency.get(arr[x]) + 1);
            } else {
                frequency.put(arr[x], 1);
            }
        }

        // To store number of extra elements
        // that needs to be changed
        int extra = (n - frequency.size());

        // Traverse from L to R
        // and see which number is not
        // present in map, use that number
        // to change extra duplicate element
        for (int i = L; i <= R && K != 0 && extra != 0; i++) {
            if (!frequency.containsKey(i)) {
                frequency.put(i, 1);
                K--;
                extra--;
            }
        }

        // Total distinct element will be equal
        // to the size of updated frequency map.
        int ans = frequency.size();

        // Return answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args) {
        // Test case 1
        int N = 7, L = 1, R = 5, K = 2;
        int arr[] = { 1, 2, 1, 4, 6, 4, 4 };
        System.out.print(maxDistinctElements(arr, K, L, R, N) + "\n");

        // Test case 2
        K = 1;
        System.out.print(maxDistinctElements(arr, K, L, R, N) + "\n");
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for above approach

# Function to calculate
# maximum distinct elements possible
# after at most K changes
def maxDistinctElements(arr, K, L, R, n):

    # Map to store frequency of all the elements
    frequency = {}

    # Count frequency of each element
    for x in range(n):
        if arr[x] in frequency:
            frequency[arr[x]] += 1
        else:
            frequency[arr[x]] = 1

    # To store number of extra elements
    # that needs to be changed
    extra = (n - len(frequency))

    # Traverse from L to R
    # and see which number is not
    # present in map, use that number
    # to change extra duplicate element
    i = L
    while(i <= R and K != 0 and extra != 0):
        if (i not in frequency):
            frequency[i] = 1
            K -= 1
            extra -= 1
        else:
            frequency[i] = 1

        i += 1

    # Total distinct element will be equal
    # to the size of updated frequency map.
    ans = len(frequency)

    # Return answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Test case 1
    N = 7
    L = 1
    R = 5
    K = 2
    arr = [1, 2, 1, 4, 6, 4, 4]
    print(maxDistinctElements(arr, K, L, R, N))

    # Test case 2
    K = 1
    print(maxDistinctElements(arr, K, L, R, N))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for above approach
using System;
using System.Collections.Generic;
class GFG {
    // Function to calculate
    // maximum distinct elements possible
    // after at most K changes
    static int maxDistinctElements(int[] arr, int K, int L,
                                   int R, int n)
    {
        // Map to store frequency of all the elements
        Dictionary<int, int> frequency
            = new Dictionary<int, int>();

        // Count frequency of each element
        for (int x = 0; x < n; x++) {
            if (frequency.ContainsKey(arr[x]))
                frequency[arr[x]] += 1;
            else
                frequency[arr[x]] = 1;
        }

        // To store number of extra elements
        // that needs to be changed
        int extra = (n - frequency.Count);

        // Traverse from L to R
        // and see which number is not
        // present in map, use that number
        // to change extra duplicate element
        for (int i = L; i <= R && K != 0 && extra != 0;
             i++) {
            if (!frequency.ContainsKey(i)) {
                frequency[i] = 1;
                K--;
                extra--;
            }
        }

        // Total distinct element will be equal
        // to the size of updated frequency map.
        int ans = frequency.Count;

        // Return answer
        return ans;
    }

    // Driver Code
    public static void Main()
    {
        // Test case 1
        int N = 7, L = 1, R = 5, K = 2;
        int[] arr = { 1, 2, 1, 4, 6, 4, 4 };
        Console.WriteLine(
            maxDistinctElements(arr, K, L, R, N));

        // Test case 2
        K = 1;
        Console.WriteLine(
            maxDistinctElements(arr, K, L, R, N));
    }
}

// Tis code is contributed by decode2207.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to calculate
        // maximum distinct elements possible
        // after at most K changes
        function maxDistinctElements(arr, K, L, R, n) {
            // Map to store frequency of all the elements
            let frequency = new Map();

            // Count frequency of each element
            for (let x = 0; x < n; x++) {
                if (frequency.has(arr[x])) {
                    frequency.set(frequency.get(arr[x]), frequency.get(arr[x]) + 1);
                }
                else {
                    frequency.set(arr[x], 1)
                }
            }

            // To store number of extra elements
            // that needs to be changed
            let extra = (n - frequency.size);

            // Traverse from L to R
            // and see which number is not
            // present in map, use that number
            // to change extra duplicate element

            for (let i = L;
                i <= R && K != 0 && extra != 0;
                i++) {
                if (!frequency.has(i)) {
                    frequency.set(i, 1);
                    K--;
                    extra--;
                }
            }

            // Total distinct element will be equal
            // to the size of updated frequency map.
            let ans = frequency.size;

            // Return answer
            return ans;
        }

        // Driver Code

        // Test case 1
        let N = 7, L = 1, R = 5, K = 2;
        let arr = [1, 2, 1, 4, 6, 4, 4];
        document.write(maxDistinctElements(arr, K, L, R, N) + "<br>");

        // Test case 2
        K = 1;
        document.write(maxDistinctElements(arr, K, L, R, N) + "<br>");

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
6
5
```

***时间复杂度:** O(N)。*

***辅助空间:** O(N)。*