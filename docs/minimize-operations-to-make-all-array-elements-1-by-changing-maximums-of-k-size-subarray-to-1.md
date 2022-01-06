# 通过将 K 尺寸子阵列的最大值改为-1

，使所有阵列元素变为-1 的操作最小化

> 原文:[https://www . geeksforgeeks . org/通过将 k 尺寸子阵列的最大值更改为 1 来最小化所有阵列元素的操作/](https://www.geeksforgeeks.org/minimize-operations-to-make-all-array-elements-1-by-changing-maximums-of-k-size-subarray-to-1/)

给定一个由 **N** 个整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找到制作所有数组元素 **-1** 所需的最小操作数，以便在每次操作中，选择一个大小为 **K** 的子数组，并将子数组中的所有[个最大元素更改为 **-1** 。](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)

**示例:**

> **输入:** arr[] = {18，11，18，11，18}，K = 3
> **输出:** 3
> **解释:**
> 执行如下操作:
> 
> 1.  从索引 0 到 2 选择子数组，并通过应用该操作，将数组修改为{-1，11，-1，11，18}。
> 2.  选择子数组形式索引 1 到 3，并通过应用操作，将数组修改为{-1，-1，-1，-1，18}。
> 3.  选择子数组形式索引 2 到 4，并通过应用操作，将数组修改为{-1，-1，-1，-1，-1}。
> 
> 在上述操作之后，所有的数组元素变成-1。因此，所需的最小操作数是 3。
> 
> **输入:** arr[] = {2，1，1}，K = 2
> T3】输出: 2

**方法:**给定的问题可以通过[用索引对数组 **arr[]**](https://www.geeksforgeeks.org/sorting-algorithms/) 进行排序，然后通过从索引之间的差**小于 K** 的末端选择数组元素来计算运算次数来解决。按照以下步骤解决问题:

*   初始化一个[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说 **vp[]** ，它存储数组元素及其索引。
*   初始化一个变量，比如说 **minCnt** 为 **0** ，存储最小操作次数的计数。
*   [遍历数组 **arr[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) 并在向量 **vp** 中推动**arr【I】**及其索引 **i** 。
*   [根据第一个值](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)对向量对 **vp[]** 进行排序。
*   [遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **vp[]** 直到不为空，并执行以下步骤:
    *   将 **minCnt** 的值增加 **1** 。
    *   [从后面弹出向量](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)**VP【】**中具有相同值(每对的第一个元素)并且指数之间的差异小于 **K** 的所有元素。
*   完成以上步骤后，打印 **minCnt** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum the number
// of operations required to make all
// the array elements to -1
int minOperations(int arr[], int N, int K)
{

    // Stores the array elements with
    // their corresponding indices
    vector<pair<int, int> > vp;
    for (int i = 0; i < N; i++) {

        // Push the array element
        // and it's index
        vp.push_back({ arr[i], i });
    }

    // Sort the elements according
    // to it's first value
    sort(vp.begin(), vp.end());

    // Stores the minimum number of
    // operations required
    int minCnt = 0;

    // Traverse until vp is not empty
    while (!vp.empty()) {
        int val, ind;

        // Stores the first value of vp
        val = vp.back().first;

        // Stores the second value of vp
        ind = vp.back().second;

        // Update the minCnt
        minCnt++;

        // Pop the back element from the
        // vp until the first value is
        // same as val and difference
        // between indices is less than K
        while (!vp.empty()
               && vp.back().first == val
               && ind - vp.back().second + 1 <= K)
            vp.pop_back();
    }

    // Return the minCnt
    return minCnt;
}

// Driver Code
int main()
{
    int arr[] = { 18, 11, 18, 11, 18 };
    int K = 3;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minOperations(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }

// Function to find minimum the number
// of operations required to make all
// the array elements to -1
static int minOperations(int arr[], int N, int K)
{

    // Stores the array elements with
    // their corresponding indices
    Vector<pair> vp = new Vector<pair>();
    for (int i = 0; i < N; i++) {

        // Push the array element
        // and it's index
        vp.add(new pair( arr[i], i ));
    }

    // Sort the elements according
    // to it's first value
    Collections.sort(vp,(a,b)->a.first-b.first);

    // Stores the minimum number of
    // operations required
    int minCnt = 0;

    // Traverse until vp is not empty
    while (!vp.isEmpty()) {
        int val, ind;

        // Stores the first value of vp
        val = vp.get(vp.size()-1).first;

        // Stores the second value of vp
        ind = vp.get(vp.size()-1).second;

        // Update the minCnt
        minCnt++;

        // Pop the back element from the
        // vp until the first value is
        // same as val and difference
        // between indices is less than K
        while (!vp.isEmpty()
               && vp.get(vp.size()-1).first == val
               && ind - vp.get(vp.size()-1).second + 1 <= K)
            vp.remove(vp.size()-1);
    }

    // Return the minCnt
    return minCnt;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 18, 11, 18, 11, 18 };
    int K = 3;
    int N = arr.length;

    System.out.print(minOperations(arr, N, K));

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find minimum the number
# of operations required to make all
# the array elements to -1
def minOperations(arr, N, K):

    # Stores the array elements with
    # their corresponding indices
    vp = []
    for i in range(N):

        # Push the array element
        # and it's index
        vp.append([arr[i], i])

    # Sort the elements according
    # to it's first value
    vp.sort()

    # Stores the minimum number of
    # operations required
    minCnt = 0

    # Traverse until vp is not empty
    while (len(vp) != 0):

        # Stores the first value of vp
        val = vp[-1][0]

        # Stores the second value of vp
        ind = vp[-1][1]

        # Update the minCnt
        minCnt += 1

        # Pop the back element from the
        # vp until the first value is
        # same as val and difference
        # between indices is less than K
        while (len(vp) != 0
               and vp[-1][0] == val
               and ind - vp[-1][1] + 1 <= K):
            vp.pop()

    # Return the minCnt
    return minCnt

# Driver Code
if __name__ == "__main__":

    arr = [18, 11, 18, 11, 18]
    K = 3
    N = len(arr)

    print(minOperations(arr, N, K))

    # This code is contributed by mukesh07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{
    class pair : IComparable<pair>
    {
        public int first,second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }

        public int CompareTo(pair p)
        {
            return this.first - p.first;
        }
    }

// Function to find minimum the number
// of operations required to make all
// the array elements to -1
static int minOperations(int []arr, int N, int K)
{

    // Stores the array elements with
    // their corresponding indices
    List<pair> vp = new List<pair>();
    for (int i = 0; i < N; i++) {

        // Push the array element
        // and it's index
        vp.Add(new pair( arr[i], i ));
    }

    // Sort the elements according
    // to it's first value
    vp.Sort();

    // Stores the minimum number of
    // operations required
    int minCnt = 0;

    // Traverse until vp is not empty
    while (vp.Count!=0) {
        int val, ind;

        // Stores the first value of vp
        val = vp[vp.Count-1].first;

        // Stores the second value of vp
        ind = vp[vp.Count-1].second;

        // Update the minCnt
        minCnt++;

        // Pop the back element from the
        // vp until the first value is
        // same as val and difference
        // between indices is less than K
        while (vp.Count!=0
               && vp[vp.Count-1].first == val
               && ind - vp[vp.Count-1].second + 1 <= K)
            vp.RemoveAt(vp.Count-1);
    }

    // Return the minCnt
    return minCnt;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 18, 11, 18, 11, 18 };
    int K = 3;
    int N = arr.Length;

    Console.Write(minOperations(arr, N, K));

}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find minimum the number
       // of operations required to make all
       // the array elements to -1
       function minOperations(arr, N, K)
       {

           // Stores the array elements with
           // their corresponding indices
           let vp = [];
           for (let i = 0; i < N; i++)
           {

               // Push the array element
               // and it's index
               vp.push({ "first": arr[i], "second": i });
           }

           // Sort the elements according
           // to it's first value
           vp.sort(function (a, b) { return a.first - b.first; });

           // Stores the minimum number of
           // operations required
           let minCnt = 0;

           // Traverse until vp is not empty
           while (vp.length > 0) {
               let val, ind;

               // Stores the first value of vp
               val = vp[vp.length - 1].first;

               // Stores the second value of vp
               ind = vp[vp.length - 1].second;

               // Update the minCnt
               minCnt++;

               // Pop the back element from the
               // vp until the first value is
               // same as val and difference
               // between indices is less than K
               while (vp.length > 0
                   && (vp[vp.length - 1].first == val)
                   && (ind - vp[vp.length - 1].second + 1 <= K)) {
                   vp.pop();
               }
           }

           // Return the minCnt
           return minCnt;
       }

       // Driver Code
       let arr = [18, 11, 18, 11, 18];
       let K = 3;
       let N = arr.length;

       document.write(minOperations(arr, N, K));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)