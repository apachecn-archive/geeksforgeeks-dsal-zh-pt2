# 给定数组按升序排序所需的最小跳转次数

> 原文:[https://www . geesforgeks . org/最小跳转次数-按升序对给定数组进行排序所需次数/](https://www.geeksforgeeks.org/minimum-number-of-jumps-required-to-sort-the-given-array-in-ascending-order/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和**jump【】**，每个长度 **N** ，其中**jump【I】**表示数组**arr【】**中的 **i** <sup>第</sup>元素可以向前移动的索引数量，任务是找到所需的最小跳转数量，使得数组按升序排序。

***注:***
*阵中所有元素**arr【】**各不相同。*
*跳跃时，数组元素可以重叠(即位于同一索引上)。*
*数组元素可以移动到超过* [*数组大小的索引中*](https://www.geeksforgeeks.org/how-to-find-size-of-array-in-cc-without-using-sizeof-operator/) *。*

**示例:**

> **输入:** arr[] = {3，1，2}，jump[] = {1，4，5}
> **输出:** 3
> **解释:**
> 以下序列需要最小数量的跳转才能按升序对数组进行排序:
> Jump 1: arr[0]跳转 1 ( = jump[0])索引到索引 1。
> 跳转 2: arr[0]跳转 1 ( =跳转[0])索引到索引 2。
> 跳转 3: arr[0]跳转 1 ( =跳转[0])索引到索引 3。
> 因此，所需的最小操作次数为 3 次。
> 
> **输入:** arr[] = {3，2，1}，jump[] = {1，1，1}
> **输出:** 6
> **解释:**
> 以下序列需要最小数量的跳转才能按升序对数组进行排序:
> Jump 1: arr[0]跳转 1 ( = jump[0])索引到索引 1。
> 跳转 2: arr[0]通过 1 ( =跳转[0])索引跳转到索引 2。
> 跳转 3: arr[0]通过 1 ( =跳转[0])索引跳转到索引 3。
> 跳转 4: arr[1]通过 1 ( =跳转[0])索引跳转到索引 2。
> 跳转 5: arr[1]通过 1 ( =跳转[0])索引跳转到索引 3。
> 跳转 6: arr[0]通过 1 ( =跳转[0])索引跳转到索引 4。
> 因此，所需的最小操作次数为 6 次。

**进场:**给定的问题可以解决[贪婪的](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决问题:

*   初始化一个变量，比如**跳跃= 0** ，以存储所需的最小跳跃次数。
*   初始化一个[数组，](https://www.geeksforgeeks.org/array-data-structure/)表示**temp【】**，其中**temp【arr[I]】**存储 **arr[i]** 可以跳跃的距离
*   初始化一对的[向量，比如**向量**，以存储](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的元素及其各自的索引，即 **{arr[i]，i + 1}**
*   [排序向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/) **向量。**
*   [在指数**【1，N–1】的范围内，遍历向量**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **向量**。更新 **vect[i]** 的值，同时 **vect[i]。第二个** ≤ **vect[i-1]。第二**，通过将跳跃距离加到 **vect[i]上。第二**。
*   通过 **1** 增加**跳跃**。
*   打印**跳跃**的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number
// of jumps required to sort the array
void minJumps(int arr[], int jump[], int N)
{
    // Stores minimum number of jumps
    int jumps = 0;

    // Stores distances of jumps
    int temp[1000];

    // Stores the array elements
    // with their starting indices
    vector<pair<int, int> > vect;

    // Push the pairs {arr[i], i+1}
    // into the vector of pairs vect
    for (int i = 0; i < N; i++) {

        // Update vect
        vect.push_back({ arr[i], i + 1 });
    }

    // Populate the array temp[]
    for (int i = 0; i < N; i++) {

        // Update temp[arr[i]]
        temp[arr[i]] = jump[i];
    }

    // Sort the vector in
    // the ascending order
    sort(vect.begin(), vect.end());

    for (int i = 1; i < N; i++) {
        // Jump till the previous
        // index <= current index
        while (vect[i].second <= vect[i - 1].second) {
            // Update vect[i]
            vect[i] = make_pair(vect[i].first,
                                vect[i].second
                                    + temp[vect[i].first]);

            // Increment the
            // number of jumps
            jumps++;
        }
    }

    // Print the minimum number
    // of jumps required
    cout << jumps << endl;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 3, 2, 1 };
    int jump[] = { 1, 1, 1 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    minJumps(arr, jump, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count minimum number
// of jumps required to sort the array
static void minJumps(int arr[], int jump[], int N)
{

    // Stores minimum number of jumps
    int jumps = 0;

    // Stores distances of jumps
    int temp[] = new int[1000];

    // Stores the array elements
    // with their starting indices
    int vect[][] = new int[N][2];

    // Push the pairs {arr[i], i+1}
    // into the vector of pairs vect
    for(int i = 0; i < N; i++)
    {

        // Update vect
        vect[i][0] = arr[i];
        vect[i][1] = i + 1;
    }

    // Populate the array temp[]
    for(int i = 0; i < N; i++)
    {

        // Update temp[arr[i]]
        temp[arr[i]] = jump[i];
    }

    // Sort the vector in
    // the ascending order
    Arrays.sort(vect, (a, b) -> {
        if (a[0] != b[0])
            return a[0] - b[0];

        return a[1] - b[1];
    });

    for(int i = 1; i < N; i++)
    {

        // Jump till the previous
        // index <= current index
        while (vect[i][1] <= vect[i - 1][1])
        {

            // Update vect[i]
            vect[i][0] = vect[i][0];
            vect[i][1] = vect[i][1] + temp[vect[i][0]];

            // Increment the
            // number of jumps
            jumps++;
        }
    }

    // Print the minimum number
    // of jumps required
    System.out.println(jumps);
}

// Driver Code
public static void main(String[] args)
{

    // Input
    int arr[] = { 3, 2, 1 };
    int jump[] = { 1, 1, 1 };

    // Size of the array
    int N = arr.length;

    minJumps(arr, jump, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count minimum number
# of jumps required to sort the array
def minJumps(arr, jump, N):

    # Stores minimum number of jumps
    jumps = 0

    # Stores distances of jumps
    temp = [0 for i in range(1000)]

    # Stores the array elements
    # with their starting indices
    vect = []

    # Push the pairs {arr[i], i+1}
    # into the vector of pairs vect
    for i in range(N):

        # Update vect
        vect.append([arr[i], i + 1])

    # Populate the array temp[]
    for i in range(N):

        # Update temp[arr[i]]
        temp[arr[i]] = jump[i]

    # Sort the vector in
    # the ascending order
    vect.sort(reverse = False)

    for i in range(N):

        # Jump till the previous
        # index <= current index
        while (vect[i][1] <= vect[i - 1][1]):

            # Update vect[i]
            vect[i] = [vect[i][0], vect[i][1] +
                  temp[vect[i][0]]]

            # Increment the
            # number of jumps
            jumps += 1

    # Print the minimum number
    # of jumps required
    print(jumps)

# Driver Code
if __name__ == '__main__':

    # Input
    arr =  [3, 2, 1]
    jump = [1, 1, 1]

    # Size of the array
    N = len(arr)

    minJumps(arr, jump, N)

# This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to count minimum number
    // of jumps required to sort the array
    const minJumps = (arr, jump, N) => {

        // Stores minimum number of jumps
        let jumps = 0;

        // Stores distances of jumps
        let temp = new Array(1000).fill(0);

        // Stores the array elements
        // with their starting indices
        let vect = [];

        // Push the pairs {arr[i], i+1}
        // into the vector of pairs vect
        for (let i = 0; i < N; i++) {

            // Update vect
            vect.push([arr[i], i + 1]);
        }

        // Populate the array temp[]
        for (let i = 0; i < N; i++) {

            // Update temp[arr[i]]
            temp[arr[i]] = jump[i];
        }

        // Sort the vector in
        // the ascending order
        vect.sort();

        for (let i = 1; i < N; i++) {
            // Jump till the previous
            // index <= current index
            while (vect[i][1] <= vect[i - 1][1]) {
                // Update vect[i]
                vect[i] = [vect[i][0],
                vect[i][1]
                + temp[vect[i][0]]];

                // Increment the
                // number of jumps
                jumps++;
            }
        }

        // Print the minimum number
        // of jumps required
        document.write(`${jumps}<br/>`);
    }

    // Driver Code

    // Input
    let arr = [3, 2, 1];
    let jump = [1, 1, 1];

    // Size of the array
    let N = arr.length;

    minJumps(arr, jump, N);

// This code is contributed by rakeshsahni

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*