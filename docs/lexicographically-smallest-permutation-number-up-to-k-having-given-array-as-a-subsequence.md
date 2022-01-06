# 字典上最小的排列数，最多 K 个，给定数组作为子序列

> 原文:[https://www . geesforgeks . org/按字典顺序排列的最小排列数最多 k 个给定数组作为子序列/](https://www.geeksforgeeks.org/lexicographically-smallest-permutation-number-up-to-k-having-given-array-as-a-subsequence/)

给定整数 **K** 和具有范围**【1，K】**中的 **N** 成对不同整数的数组 **arr[]** ，任务是找到第一个 **K** 正整数的[字典最小排列](https://www.geeksforgeeks.org/lexicographically-n-th-permutation-string/)，使得给定数组 **arr[]** 是排列的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。

**示例:**

> **输入:** arr[] = {1，3，5，7}，K = 8
> **输出:** 1 2 3 4 5 6 7 8
> **解释:** {1，2，3，4，5，6，7，8}是前 8 个正整数的字典上最小的置换，这样给定的数组{1，3，5，7}也是置换的子序列。
> 
> **输入:** arr[] = {6，4，2，1}，K=7
> **输出:**3 5 6 2 1 7

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。以下是要遵循的步骤:

*   使用本文中讨论的方法，创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **【缺失】【】**，该向量以递增顺序存储给定数组**中不存在的范围**【1，K】**中的整数。**
*   创建[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/) **p1** 和 **p2** ，分别将当前索引存储在**arr【】**和**missing【】**中。最初，两者都等于 **0** 。
*   贪婪地将**arr【P1】**和**missing【p2】**的最小值取并存储到一个向量中，比如说 **ans[]** ，并将各自的指针递增到下一个位置，直到存储的整数的计数小于 **K** 。
*   为了让事情变得更简单，在数组末尾追加[INT _ MAX](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/)**missing[]**和 **arr[]** ，这样可以避免让[出界。](https://www.geeksforgeeks.org/accessing-array-bounds-ccpp/)
*   完成上述步骤后，存储在**ans【】**中的所有值即为所需结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the lexicographically
// smallest permutation such that the
// given array is a subsequence of it
void findPermutation(int K, vector<int> arr)
{
    // Stores the missing elements in
    // arr in the range [1, K]
    vector<int> missing;

    // Stores if the ith element is
    // present in arr or not
    vector<bool> visited(K + 1, 0);

    // Loop to mark all integers present
    // in the array as visited
    for (int i = 0; i < arr.size(); i++) {
        visited[arr[i]] = 1;
    }

    // Loop to insert all the integers
    // not visited into missing
    for (int i = 1; i <= K; i++) {
        if (!visited[i]) {
            missing.push_back(i);
        }
    }
    // Append INT_MAX at end in order
    // to prevent going out of bounds
    arr.push_back(INT_MAX);
    missing.push_back(INT_MAX);

    // Pointer to the current element
    int p1 = 0;

    // Pointer to the missing element
    int p2 = 0;

    // Stores the required permutation
    vector<int> ans;

    // Loop to construct the permutation
    // using greedy approach
    while (ans.size() < K) {

        // If missing element is smaller
        // that the current element insert
        // missing element
        if (arr[p1] < missing[p2]) {
            ans.push_back(arr[p1]);
            p1++;
        }

        // Insert current element
        else {
            ans.push_back(missing[p2]);
            p2++;
        }
    }

    // Print the required Permutation
    for (int i = 0; i < K; i++) {
        cout << ans[i] << " ";
    }
}

// Driver Code
int main()
{
    int K = 7;
    vector<int> arr = { 6, 4, 2, 1 };

    // Function Call
    findPermutation(K, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the lexicographically
// smallest permutation such that the
// given array is a subsequence of it
static void findPermutation(int K, Vector<Integer> arr)
{
    // Stores the missing elements in
    // arr in the range [1, K]
    Vector<Integer> missing = new Vector<Integer>();

    // Stores if the ith element is
    // present in arr or not
    boolean visited[] = new boolean[K + 1];

    // Loop to mark all integers present
    // in the array as visited
    for (int i = 0; i < arr.size(); i++) {
        visited[arr.get(i)] = true;
    }

    // Loop to insert all the integers
    // not visited into missing
    for (int i = 1; i <= K; i++) {
        if (!visited[i]) {
            missing.add(i);
        }
    }
    // Append Integer.MAX_VALUE at end in order
    // to prevent going out of bounds
    arr.add(Integer.MAX_VALUE);
    missing.add(Integer.MAX_VALUE);

    // Pointer to the current element
    int p1 = 0;

    // Pointer to the missing element
    int p2 = 0;

    // Stores the required permutation
    Vector<Integer> ans = new Vector<Integer>();

    // Loop to conthe permutation
    // using greedy approach
    while (ans.size() < K) {

        // If missing element is smaller
        // that the current element insert
        // missing element
        if (arr.get(p1) < missing.get(p2)) {
            ans.add(arr.get(p1));
            p1++;
        }

        // Insert current element
        else {
            ans.add(missing.get(p2));
            p2++;
        }
    }

    // Print the required Permutation
    for (int i = 0; i < K; i++) {
        System.out.print(ans.get(i)+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int K = 7;
    Integer []a = {6, 4, 2, 1};
    Vector<Integer> arr = new Vector<>(Arrays.asList(a));

    // Function Call
    findPermutation(K, arr);

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the lexicographically
# smallest permutation such that the
#  given array is a subsequence of it
def findPermutation(K, arr):

    # Stores the missing elements in
        # arr in the range [1, K]
    missing = []

    # Stores if the ith element is
    # present in arr or not
    visited = [0]*(K+1)

    # Loop to mark all integers present
    # in the array as visited
    for i in range(4):
        visited[arr[i]] = 1

    # Loop to insert all the integers
    # not visited into missing
    for i in range(1, K+1):
        if(not visited[i]):
            missing.append(i)

    # Append INT_MAX at end in order
        # to prevent going out of bounds
    INT_MAX = 2147483647
    arr.append(INT_MAX)
    missing.append(INT_MAX)

    # Pointer to the current element
    p1 = 0

    # Pointer to the missing element
    p2 = 0

    # Stores the required permutation
    ans = []

    # Loop to construct the permutation
    # using greedy approach

    while (len(ans) < K):
        # If missing element is smaller
                # that the current element insert
        # missing element
        if (arr[p1] < missing[p2]):
            ans.append(arr[p1])
            p1 = p1 + 1

        # Insert current element
        else:
            ans.append(missing[p2])
            p2 = p2 + 1

    # Print the required Permutation
    for i in range(0, K):
        print(ans[i], end=" ")

# Driver Code
if __name__ == "__main__":
    K = 7
    arr = [6, 4, 2, 1]

    # Function Call
    findPermutation(K, arr)

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
class GFG{

// Function to find the lexicographically
// smallest permutation such that the
// given array is a subsequence of it
static void findPermutation(int K, ArrayList arr)
{

    // Stores the missing elements in
    // arr in the range [1, K]
    ArrayList missing = new ArrayList();

    // Stores if the ith element is
    // present in arr or not
    bool [] visited = new bool[K + 1];

    // Loop to mark all integers present
    // in the array as visited
    for (int i = 0; i < arr.Count; i++) {
        visited[(int)arr[i]] = true;
    }

    // Loop to insert all the integers
    // not visited into missing
    for (int i = 1; i <= K; i++) {
        if (!visited[i]) {
            missing.Add(i);
        }
    }
    // Append Int32.MaxValue at end in order
    // to prevent going out of bounds
    arr.Add(Int32.MaxValue);
    missing.Add(Int32.MaxValue);

    // Pointer to the current element
    int p1 = 0;

    // Pointer to the missing element
    int p2 = 0;

    // Stores the required permutation
    ArrayList ans = new ArrayList();

    // Loop to conthe permutation
    // using greedy approach
    while (ans.Count < K) {

        // If missing element is smaller
        // that the current element insert
        // missing element
        if ((int)arr[p1] < (int)missing[p2]) {
            ans.Add(arr[p1]);
            p1++;
        }

        // Insert current element
        else {
            ans.Add(missing[p2]);
            p2++;
        }
    }

    // Print the required Permutation
    for (int i = 0; i < K; i++) {
        Console.Write(ans[i]+ " ");
    }
}

// Driver Code
public static void Main()
{
    int K = 7;
    int [] a = {6, 4, 2, 1};
    ArrayList arr = new ArrayList(a);

    // Function Call
    findPermutation(K, arr);
}
}

// This code is contributed by ihritik.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find the lexicographically
    // smallest permutation such that the
    // given array is a subsequence of it
    const findPermutation = (K, arr) => {

        // Stores the missing elements in
        // arr in the range [1, K]
        let missing = [];

        // Stores if the ith element is
        // present in arr or not
        let visited = new Array(K + 1).fill(0);

        // Loop to mark all integers present
        // in the array as visited
        for (let i = 0; i < arr.length; i++) {
            visited[arr[i]] = 1;
        }

        // Loop to insert all the integers
        // not visited into missing
        for (let i = 1; i <= K; i++) {
            if (!visited[i]) {
                // missing.push_back(i);
                missing.push(i);
            }
        }
        // Append INT_MAX at end in order
        // to prevent going out of bounds
        const INT_MAX = 2147483647;
        arr.push(INT_MAX);
        missing.push(INT_MAX);

        // Pointer to the current element
        let p1 = 0;

        // Pointer to the missing element
        let p2 = 0;

        // Stores the required permutation
        let ans = [];

        // Loop to construct the permutation
        // using greedy approach
        while (ans.length < K) {

            // If missing element is smaller
            // that the current element insert
            // missing element
            if (arr[p1] < missing[p2]) {
                ans.push(arr[p1]);
                p1++;
            }

            // Insert current element
            else {
                ans.push(missing[p2]);
                p2++;
            }
        }

        // Print the required Permutation
        for (let i = 0; i < K; i++) {
            document.write(`${ans[i]} `);
        }
    }

    // Driver Code
    let K = 7;
    let arr = [6, 4, 2, 1];

    // Function Call
    findPermutation(K, arr);

    // This code is contributed by rakeshsahni.
</script>
```

**Output:** 

```
3 5 6 4 2 1 7
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)