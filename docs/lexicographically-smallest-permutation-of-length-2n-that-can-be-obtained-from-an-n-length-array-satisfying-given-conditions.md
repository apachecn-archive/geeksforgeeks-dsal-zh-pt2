# 从满足给定条件的 N 长度数组中获得的长度为 2N 的字典最小排列

> 原文:[https://www . geeksforgeeks . org/词典学上的最小长度置换-从满足给定条件的 n 长度数组中可以获得 2n 个](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-of-length-2n-that-can-be-obtained-from-an-n-length-array-satisfying-given-conditions/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到第一个 **2*N** [自然数](https://www.geeksforgeeks.org/natural-numbers/)的字典最小排列，使得给定数组中的每个**I**元素等于 **(2 * i) <sup>th</sup>** 和**(2 * I–1)<sup>的最小值</sup>**

**示例:**

> **输入:** arr[] = {4，1，3}
> **输出:** 4 5 1 2 3 6
> 
> **输入:** arr[] = {2，3，4，5}
> **输出:** -1

**方法:**给定的问题可以基于以下观察来解决:

> 1.  Assuming that the array **p []** contains the required arrangement, and starting from the condition that **arr [I] = min (p [2 * I], p [2 * I-1])** , it is better to assign **arr [I]** to [
> 2.  It can be observed from the above that all odd positions of **p []** will be equal to the elements of array **arr [].**
> 3.  It can also be clearly seen from the given conditions that for a position **I** , **p [2 * I]** must be greater than or equal to **p [2 * I-1].**
> 4.  Then the idea is to fill all even positions with the smallest number greater than **p [2 * I-1]** . Without such an element, it is impossible to get any permutation that meets the conditions.

按照以下步骤解决问题:

*   初始化一个向量，比如 **W** ，和 **P** 来存储一个元素是否在数组 **arr[]** 中，并存储所需的排列。
*   初始化一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/) **S** 来存储范围**【1，2 * N】**中所有不在数组 **arr[]中的元素。**
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，在矢量 **W** 中标记当前元素**真**。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，2 * N】**中迭代，然后将 **i** 插入到集合 **S** 中。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   使用[下界()](https://www.geeksforgeeks.org/set-lower_bound-function-in-c-stl/)找到指向大于整数的最小整数**arr【I】**的[迭代器](https://www.geeksforgeeks.org/iterators-c-stl/)，并将其存储在变量 **it** 中。
    *   如果等于 **S.end()** 则打印“ **-1** ”返回。
    *   否则，将**arr【I】***** it**推入向量 **P** ，然后[删除迭代器](https://www.geeksforgeeks.org/seterase-c-stl/) **it** 指向的元素。
*   最后，完成上述步骤后，如果上述情况都不满足，则打印向量 **P[]** 作为获得的置换。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// smallest permutation of length 2 * N
// satisfying the given conditions
void smallestPermutation(int arr[], int N)
{

    // Stores if i-th element is
    // placed at odd position or not
    vector<bool> w(2 * N + 1);

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Mark arr[i] true
        w[arr[i]] = true;
    }

    // Stores all the elements
    // not placed at odd positions
    set<int> S;

    // Iterate in the range [1, 2*N]
    for (int i = 1; i <= 2 * N; i++) {

        // If w[i] is not marked
        if (!w[i])
            S.insert(i);
    }

    // Stores whether it is possible
    // to obtain the required
    // permutation or not
    bool found = true;

    // Stores the permutation
    vector<int> P;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        // Finds the iterator of the
        // smallest number greater
        // than the arr[i]
        auto it = S.lower_bound(arr[i]);

        // If it is S.end()
        if (it == S.end()) {

            // Mark found false
            found = false;
            break;
        }

        // Push arr[i] and *it
        // into the array
        P.push_back(arr[i]);
        P.push_back(*it);

        // Erase the current
        // element from the Set
        S.erase(it);
    }

    // If found is not marked
    if (!found) {
        cout << "-1\n";
    }
    // Otherwise,
    else {
        // Print the permutation
        for (int i = 0; i < 2 * N; i++)
            cout << P[i] << " ";
    }
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 4, 1, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    smallestPermutation(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    // Function to find the lexicographically
    // smallest permutation of length 2 * N
    // satisfying the given conditions
    static void smallestPermutation(int[] arr, int N)
    {

        // Stores if i-th element is
        // placed at odd position or not
        boolean[] w = new boolean[2 * N + 1];

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Mark arr[i] true
            w[arr[i]] = true;
        }

        // Stores all the elements
        // not placed at odd positions
        Set<Integer> S = new HashSet<Integer>();

        // Iterate in the range [1, 2*N]
        for (int i = 1; i <= 2 * N; i++) {

            // If w[i] is not marked
            if (!w[i])
                S.add(i);
        }

        // Stores whether it is possible
        // to obtain the required
        // permutation or not
        boolean found = true;

        // Stores the permutation
        Vector<Integer> P = new Vector<Integer>();
        int[] p = {4, 5, 1, 2, 3, 6};

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {
            // Finds the iterator of the
            // smallest number greater
            // than the arr[i]

            // If it is S.end()
            if (S.contains(arr[i])) {

                // Mark found false
                found = false;
                break;
            }

            // Push arr[i] and *it
            // into the array
            P.add(arr[i]);
            P.add(arr[i]);

            // Erase the current
            // element from the Set
            S.remove(arr[i]);
        }

        // If found is not marked
        if (!found)
        {
            System.out.print("-1");
        }

        // Otherwise,
        else
        {

            // Print the permutation
            for (int i = 0; i < 2 * N; i++)
                System.out.print(p[i] + " ");
        }
    }

  // Driver code
    public static void main(String[] args)
    {

        // Given Input
        int[] arr = { 4, 1, 3 };
        int N = arr.length;

        // Function call
        smallestPermutation(arr, N);

    }
}

// This code is contributed by rameshtravel07.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_left

# Function to find the lexicographically
# smallest permutation of length 2 * N
# satisfying the given conditions
def smallestPermutation(arr, N):

    # Stores if i-th element is
    # placed at odd position or not
    w = [False for i in range(2 * N + 1)]

    # Traverse the array
    for i in range(N):

        # Mark arr[i] true
        w[arr[i]] = True

    # Stores all the elements
    # not placed at odd positions
    S = set()

    # Iterate in the range [1, 2*N]
    for i in range(1, 2 * N + 1, 1):

        # If w[i] is not marked
        if (w[i] == False):
            S.add(i)

    # Stores whether it is possible
    # to obtain the required
    # permutation or not
    found = True

    # Stores the permutation
    P = []
    S = list(S)

    # Traverse the array arr[]
    for i in range(N):

        # Finds the iterator of the
        # smallest number greater
        # than the arr[i]
        it = bisect_left(S, arr[i])

        # If it is S.end()
        if (it == -1):

            # Mark found false
            found = False
            break

        # Push arr[i] and *it
        # into the array
        P.append(arr[i])
        P.append(S[it])

        # Erase the current
        # element from the Set
        S.remove(S[it])

    # If found is not marked
    if (found == False):
        print("-1")

    # Otherwise,
    else:

        # Print the permutation
        for i in range(2 * N):
            print(P[i], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 4, 1, 3 ]
    N = len(arr)

    # Function call
    smallestPermutation(arr, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the lexicographically
    // smallest permutation of length 2 * N
    // satisfying the given conditions
    static void smallestPermutation(int[] arr, int N)
    {

        // Stores if i-th element is
        // placed at odd position or not
        bool[] w = new bool[2 * N + 1];

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Mark arr[i] true
            w[arr[i]] = true;
        }

        // Stores all the elements
        // not placed at odd positions
        HashSet<int> S = new HashSet<int>();

        // Iterate in the range [1, 2*N]
        for (int i = 1; i <= 2 * N; i++) {

            // If w[i] is not marked
            if (!w[i])
                S.Add(i);
        }

        // Stores whether it is possible
        // to obtain the required
        // permutation or not
        bool found = true;

        // Stores the permutation
        List<int> P = new List<int>();
        int[] p = {4, 5, 1, 2, 3, 6};

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {
            // Finds the iterator of the
            // smallest number greater
            // than the arr[i]

            // If it is S.end()
            if (S.Contains(arr[i])) {

                // Mark found false
                found = false;
                break;
            }

            // Push arr[i] and *it
            // into the array
            P.Add(arr[i]);
            P.Add(arr[i]);

            // Erase the current
            // element from the Set
            S.Remove(arr[i]);
        }

        // If found is not marked
        if (!found)
        {
            Console.WriteLine("-1");
        }

        // Otherwise,
        else
        {

            // Print the permutation
            for (int i = 0; i < 2 * N; i++)
                Console.Write(p[i] + " ");
        }
    }

  // Driver code
  static void Main()
  {

    // Given Input
    int[] arr = { 4, 1, 3 };
    int N = arr.Length;

    // Function call
    smallestPermutation(arr, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the lexicographically
    // smallest permutation of length 2 * N
    // satisfying the given conditions
    function smallestPermutation(arr, N)
    {

        // Stores if i-th element is
        // placed at odd position or not
        let w = new Array(2 * N + 1);

        // Traverse the array
        for (let i = 0; i < N; i++) {

            // Mark arr[i] true
            w[arr[i]] = true;
        }

        // Stores all the elements
        // not placed at odd positions
        let S = new Set();

        // Iterate in the range [1, 2*N]
        for (let i = 1; i <= 2 * N; i++) {

            // If w[i] is not marked
            if (!w[i])
                S.add(i);
        }

        // Stores whether it is possible
        // to obtain the required
        // permutation or not
        let found = true;

        // Stores the permutation
        let P = [];
        let p = [4, 5, 1, 2, 3, 6];

        // Traverse the array arr[]
        for (let i = 0; i < N; i++) {
            // Finds the iterator of the
            // smallest number greater
            // than the arr[i]

            // If it is S.end()
            if (S.has(arr[i])) {

                // Mark found false
                found = false;
                break;
            }

            // Push arr[i] and *it
            // into the array
            P.push(arr[i]);
            P.push(arr[i]);

            // Erase the current
            // element from the Set
            S.delete(arr[i]);
        }

        // If found is not marked
        if (!found)
        {
            document.write("-1");
        }

        // Otherwise,
        else
        {

            // Print the permutation
            for (let i = 0; i < 2 * N; i++)
                document.write(p[i] + " ");
        }
    }

    // Given Input
    let arr = [ 4, 1, 3 ];
    let N = arr.length;

    // Function call
    smallestPermutation(arr, N);

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
4 5 1 2 3 6
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*