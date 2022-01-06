# 找到一个数组，使得这个数组和给定数组的平均值加起来等于 K

> 原文:[https://www . geeksforgeeks . org/find-a-array-so-mean-of-this-and-given-array-together-to-k/](https://www.geeksforgeeks.org/find-an-array-such-that-mean-of-this-and-given-array-together-equals-to-k/)

给定两个整数 **N** 、 **K** ，以及一个由正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**。任务是找到任何可能的大小为 **N** 的数组，使得[表示**arr【】**的](https://www.geeksforgeeks.org/program-average-array-iterative-recursive/)和要一起找到的数组为 **K** 。

**示例:**

> **输入:** arr[] = {1，5，6}，N = 4，K = 3
> **输出:** {1，2，3，3}
> **解释:**将{1，5，6}和{1，2，3，3}加起来的平均值如下:
> (1 + 5 + 6 + 1 + 2 + 3 + 3) / (3+4) = 3。
> 因此{1，2，3，3}有可能数组使平均值= 3。
> 
> **输入:** arr[] = {7，8，6}，N = 2，K = 3
> T3】输出:不可能

**方法:**这个问题可以用简单的[数系平均](https://www.geeksforgeeks.org/average/)概念来解决。假设**sumar**为数组的[和**new _ arr[]****M**为 **new_arr[]** 的大小。然后根据](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)[平均概念](https://www.geeksforgeeks.org/average/)方程可以形成为:

> **(sumar+X)/(N+M)= K**，其中 **X** 为所需数组之和。
> 
> **X = K *(N+M)–sumar。**

因此，所需数组的和应为 **X** ，使平均值等于 **K** 。如果 **X** 小于 **N** ，那么阵就没有办法形成了。
形成所需阵列的最简单方法是

> 1，1，1，…(M-1 次)，X-(M-1)

。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Find the required array such that mean of both
// the arrays is equal to K
vector<int> findArray(vector<int> arr,
                      int N, int K)
{

    // To store sum of elements in arr[]
    int sumArr = 0;

    int M = int(arr.size());

    // Iterate to find sum
    for (int i = 0; i < M; i++) {
        sumArr += arr[i];
    }

    // According to the formula derived above
    int X = K * (N + M) - sumArr;

    // If requiredSum if less than N
    if (X < N) {
        cout << "Not Possible";
        return {};
    }

    // Otherwise create an array to store answer
    vector<int> res(N);

    // Putting all 1s till N-1
    for (int i = 0; i < N - 1; i++) {
        res[i] = 1;
    }

    res[N - 1] = X - (N - 1);

    // Return res as the final result
    return res;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 5, 6 };
    int N = 4, K = 3;

    vector<int> ans = findArray(arr, N, K);

    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Find the required array such that mean of both
    // the arrays is equal to K
    static void findArray(int []arr,
                          int N, int K)
    {

        // To store sum of elements in arr[]
        int sumArr = 0;
        int M = arr.length;

        // Iterate to find sum
        for (int i = 0; i < M; i++) {
            sumArr += arr[i];
        }

        // According to the formula derived above
        int X = K * (N + M) - sumArr;

        // If requiredSum if less than N
        if (X < N) {
            System.out.println("Not Possible");
        }

        // Otherwise create an array to store answer
        int []res = new int[N];

        // Putting all 1s till N-1
        for (int i = 0; i < N - 1; i++) {
            res[i] = 1;
        }

        res[N - 1] = X - (N - 1);

        // Return res as the final result
        for (int i = 0; i < res.length; i++)
            System.out.print(res[i] + " ");
    }

    // Driver Code
    public static void main (String[] args)
    {
        int []arr = { 1, 5, 6 };
        int N = 4, K = 3;

        findArray(arr, N, K);
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# python program for the above approach

# Find the required array such that mean of both
# the arrays is equal to K
def findArray(arr, N, K):

    # To store sum of elements in arr[]
    sumArr = 0
    M = len(arr)

    # Iterate to find sum
    for i in range(0, M):
        sumArr += arr[i]

    # According to the formula derived above
    X = K * (N + M) - sumArr

    # If requiredSum if less than N
    if (X < N):
        print("Not Possible")
        return []

    # Otherwise create an array to store answer
    res = [0 for _ in range(N)]

    # Putting all 1s till N-1
    for i in range(0, N-1):
        res[i] = 1

    res[N - 1] = X - (N - 1)

    # Return res as the final result
    return res

# Driver Code
if __name__ == "__main__":

    arr = [1, 5, 6]
    N = 4
    K = 3

    ans = findArray(arr, N, K)

    for i in range(0, len(ans)):
        print(ans[i], end=" ")

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Find the required array such that mean of both
    // the arrays is equal to K
    static void findArray(int []arr,
                          int N, int K)
    {

        // To store sum of elements in arr[]
        int sumArr = 0;
        int M = arr.Length;

        // Iterate to find sum
        for (int i = 0; i < M; i++) {
            sumArr += arr[i];
        }

        // According to the formula derived above
        int X = K * (N + M) - sumArr;

        // If requiredSum if less than N
        if (X < N) {
            Console.WriteLine("Not Possible");
        }

        // Otherwise create an array to store answer
        int []res = new int[N];

        // Putting all 1s till N-1
        for (int i = 0; i < N - 1; i++) {
            res[i] = 1;
        }

        res[N - 1] = X - (N - 1);

        // Return res as the final result
        for (int i = 0; i < res.Length; i++)
            Console.Write(res[i] + " ");
    }

    // Driver Code
    public static void Main (string[] args)
    {
        int []arr = { 1, 5, 6 };
        int N = 4, K = 3;

        findArray(arr, N, K);
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Find the required array such that mean of both
// the arrays is equal to K
function findArray(arr, N, K) {

  // To store sum of elements in arr[]
  let sumArr = 0;

  let M = (arr.length);

  // Iterate to find sum
  for (let i = 0; i < M; i++) {
    sumArr += arr[i];
  }

  // According to the formula derived above
  let X = K * (N + M) - sumArr;

  // If requiredSum if less than N
  if (X < N) {
    document.write("Not Possible");
    return [];
  }

  // Otherwise create an array to store answer
  let res = new Array(N);

  // Putting all 1s till N-1
  for (let i = 0; i < N - 1; i++) {
    res[i] = 1;
  }

  res[N - 1] = X - (N - 1);

  // Return res as the final result
  return res;
}

// Driver Code

let arr = [1, 5, 6];
let N = 4, K = 3;

let ans = findArray(arr, N, K);

for (let i = 0; i < ans.length; i++)
  document.write(ans[i] + " ");

  // This code is contributed by gfgking.
</script>
```

**Output**

```
1 1 1 6 
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)