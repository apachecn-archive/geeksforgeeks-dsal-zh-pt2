# 将相似元素排列在一起的相邻交换的最小数量

> 原文:[https://www . geeksforgeeks . org/将相似元素排列在一起的最小相邻交换数/](https://www.geeksforgeeks.org/minimum-number-of-adjacent-swaps-for-arranging-similar-elements-together/)

给定一个由 2 * N 个正整数组成的数组，其中每个数组元素位于 1 到 N 之间，并且在数组中恰好出现两次。任务是找到将所有相似的数组元素排列在一起所需的相邻交换的最小数量。
**注**:最终数组(执行互换后)不需要排序。
**示例:**

> 输入:arr[] = { 1，2，3，3，1，2 }
> 输出:5
> 第一次交换后，数组将为 arr[] = { 1，2，3，1，3，2 }，
> 第二次 arr[] = { 1，2，1，3，3，2 }，第三次 arr[] = { 1，1，2，3，3，2，2 }，
> 第四次 arr[] = { 1，1，2，3，2，3 }，第五次 arr[] = { 1，1，2，3，}之后 3 }
> 输入:arr[] = { 1，2，1，2 }
> 输出:1
> arr[2]可以和 arr[1]对调，得到需要的位置。

**进场**:这个问题可以用贪心进场解决。以下是步骤:

1.  保留一个数组 *visited[]* ，如果尚未对 curr_ele 执行交换操作，则该数组告诉 visited[curr_ele]为 false。
2.  遍历原始数组，如果当前数组元素尚未被访问，即*访问了[arr[curr_ele]] = false* ，将其设置为 true，并在从当前位置开始到数组末尾的另一个循环中迭代。
3.  初始化一个变量计数，该计数将决定将当前元素的伙伴放置在其正确位置所需的交换次数。
4.  在嵌套循环中，只有当被访问的[curr_ele]为假时才增加计数(因为如果为真，则意味着 curr_ele 已经被放置在正确的位置)。
5.  如果在嵌套循环中找到当前元素的伙伴，则将 count 的值加到总答案中。

以下是上述方法的实现:

## C++

```
// C++ Program to find the minimum number of
// adjacent swaps to arrange similar items together

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum swaps
int findMinimumAdjacentSwaps(int arr[], int N)
{
    // visited array to check if value is seen already
    bool visited[N + 1];

    int minimumSwaps = 0;
    memset(visited, false, sizeof(visited));

    for (int i = 0; i < 2 * N; i++) {

        // If the arr[i] is seen first time
        if (visited[arr[i]] == false) {
            visited[arr[i]] = true;

            // stores the number of swaps required to
            // find the correct position of current
            // element's partner
            int count = 0;

            for (int j = i + 1; j < 2 * N; j++) {

                // Increment count only if the current
                // element has not been visited yet (if is
                // visited, means it has already been placed
                // at its correct position)
                if (visited[arr[j]] == false)
                    count++;

                // If current element's partner is found
                else if (arr[i] == arr[j])
                    minimumSwaps += count;
            }
        }
    }
    return minimumSwaps;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 3, 1, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    N /= 2;

    cout << findMinimumAdjacentSwaps(arr, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the minimum number of
// adjacent swaps to arrange similar items together
import java.util.*;

class solution
{

// Function to find minimum swaps
static int findMinimumAdjacentSwaps(int arr[], int N)
{
    // visited array to check if value is seen already
    boolean[] visited = new boolean[N + 1];

    int minimumSwaps = 0;
    Arrays.fill(visited,false);

    for (int i = 0; i < 2 * N; i++) {

        // If the arr[i] is seen first time
        if (visited[arr[i]] == false) {
            visited[arr[i]] = true;

            // stores the number of swaps required to
            // find the correct position of current
            // element's partner
            int count = 0;

            for (int j = i + 1; j < 2 * N; j++) {

                // Increment count only if the current
                // element has not been visited yet (if is
                // visited, means it has already been placed
                // at its correct position)
                if (visited[arr[j]] == false)
                    count++;

                // If current element's partner is found
                else if (arr[i] == arr[j])
                    minimumSwaps += count;
            }
        }
    }
    return minimumSwaps;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 2, 3, 3, 1, 2 };
    int N = arr.length;
    N /= 2;

    System.out.println(findMinimumAdjacentSwaps(arr, N));

}
}
// This code is contributed by
// Sanjit_Prasad
```

## 蟒蛇 3

```
# Python3 Program to find the minimum number of
# adjacent swaps to arrange similar items together

# Function to find minimum swaps
def findMinimumAdjacentSwaps(arr, N) :

    # visited array to check if value is seen already
    visited = [False] * (N + 1)

    minimumSwaps = 0

    for i in range(2 * N) :

        # If the arr[i] is seen first time
        if (visited[arr[i]] == False) :
            visited[arr[i]] = True

            # stores the number of swaps required to
            # find the correct position of current
            # element's partner
            count = 0

            for j in range( i + 1, 2 * N) :

                # Increment count only if the current
                # element has not been visited yet (if is
                # visited, means it has already been placed
                # at its correct position)
                if (visited[arr[j]] == False) :
                    count += 1

                # If current element's partner is found
                elif (arr[i] == arr[j]) :
                    minimumSwaps += count

    return minimumSwaps

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 3, 1, 2 ]
    N = len(arr)
    N //= 2

    print(findMinimumAdjacentSwaps(arr, N))

# This code is contributed by Ryuga
```

## C#

```
// C# Program to find the minimum
// number of adjacent swaps to
// arrange similar items together
using System;

class GFG
{

    // Function to find minimum swaps
    static int findMinimumAdjacentSwaps(int []arr, int N)
    {
        // visited array to check
        // if value is seen already
        bool[] visited = new bool[N + 1];

        int minimumSwaps = 0;

        for (int i = 0; i < 2 * N; i++)
        {

            // If the arr[i] is seen first time
            if (visited[arr[i]] == false)
            {
                visited[arr[i]] = true;

                // stores the number of swaps required to
                // find the correct position of current
                // element's partner
                int count = 0;

                for (int j = i + 1; j < 2 * N; j++)
                {

                    // Increment count only if the current
                    // element has not been visited yet (if is
                    // visited, means it has already been placed
                    // at its correct position)
                    if (visited[arr[j]] == false)
                        count++;

                    // If current element's partner is found
                    else if (arr[i] == arr[j])
                        minimumSwaps += count;
                }
            }
        }
        return minimumSwaps;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int []arr = { 1, 2, 3, 3, 1, 2 };
        int N = arr.Length;
        N /= 2;

        Console.WriteLine(findMinimumAdjacentSwaps(arr, N));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript Program to find the minimum number of
// adjacent swaps to arrange similar items together

// Function to find minimum swaps
function findMinimumAdjacentSwaps(arr, N)
{
    // visited array to check if value is seen already
    let visited = Array(N + 1).fill(false);

    let minimumSwaps = 0;    

    for (let i = 0; i < 2 * N; i++) {

        // If the arr[i] is seen first time
        if (visited[arr[i]] == false) {
            visited[arr[i]] = true;

            // stores the number of swaps required to
            // find the correct position of current
            // element's partner
            let count = 0;

            for (let j = i + 1; j < 2 * N; j++) {

                // Increment count only if the current
                // element has not been visited yet (if is
                // visited, means it has already been placed
                // at its correct position)
                if (visited[arr[j]] == false)
                    count++;

                // If current element's partner is found
                else if (arr[i] == arr[j])
                    minimumSwaps += count;
            }
        }
    }
    return minimumSwaps;
}

// driver code

     let arr = [ 1, 2, 3, 3, 1, 2 ];
     let N = arr.length;
     N = Math.floor(N / 2);

    document.write(findMinimumAdjacentSwaps(arr, N));

</script>
```

**Output:** 

```
5
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)