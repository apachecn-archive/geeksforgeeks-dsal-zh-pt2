# 在给定的二进制数组中最大化要翻转的 0，使得两个 1 之间至少有 K 个 0

> 原文:[https://www . geesforgeks . org/maximum-0s-待翻转给定二进制数组-这样-两个 1 之间至少有-k-0s/](https://www.geeksforgeeks.org/maximize-0s-to-be-flipped-in-given-binary-array-such-that-there-are-at-least-k-0s-between-two-1s/)

给定一个二进制数组 **arr[]** 和一个整数 **K** ，任务是计算可以翻转到 **1 的**的 **0 的最大数量**，使得两个 **1 的**之间至少有**K**T10】0 的。

**示例:**

> **输入:** arr[] = {0，0，1，0，0，0}，K = 1
> **输出:** 2
> **解释:**数组 arr[]中的第一个和第五个索引可以翻转，使得任意两个 1 之间至少有 1 个零。因此，翻转后的数组是 arr[] = {1，0，1，0，1，0}。
> 
> **输入:** arr[] = {1，0，0，0，0，0，1，0}，K = 2
> **输出:** 1
> **说明:**上述数组中的第 4 个索引是唯一可以翻转的有效索引

**方法:**给定的问题可以通过迭代数组并找到两个 1 之间的连续零的[计数](https://www.geeksforgeeks.org/maximum-0s-two-immediate-1s-binary-representation/)来解决。假设两个**1**之间的**0**的数量为 **X** 。然后可以观察到 **0 之间可以翻转的**数量为 **(X-K) / (K+1)** 。因此，遍历数组并跟踪两个**1**之间的连续**0**的数量，类似于这里[讨论的算法](https://www.geeksforgeeks.org/maximum-0s-two-immediate-1s-binary-representation/)，并添加**0**的计数，该计数可以翻转为变量 **cnt** ，这是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of 1s that can be placed in array arr[]
int maximumOnes(int arr[], int N, int K)
{

    // Stores the count of 1's
    int cnt = 0;

    // Stores the last index of 1
    int last = -(K + 1);

    // Loop to iterate through the array
    for (int i = 0; i < N; i++) {

        // If the current element is 1
        if (arr[i] == 1) {

            // Check if there are sufficient
            // 0's between consecutive 1's to
            // insert more 1's between them
            if (i - last - 1 >= 2 * (K - 1)) {
                cnt += (i - last - 1 - K) / (K + 1);
            }

            // Update the index of last 1
            last = i;
        }
    }

    // Condition to include the segment of
    // 0's in the last
    cnt += (N - last - 1) / (K + 1);

    // Return answer
    return cnt;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 0, 0, 0, 0, 0, 0, 1, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 2;

    cout << maximumOnes(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

    // Function to find the maximum number
    // of 1s that can be placed in array arr[]
    static int maximumOnes(int arr[], int N, int K)
    {

        // Stores the count of 1's
        int cnt = 0;

        // Stores the last index of 1
        int last = -(K + 1);

        // Loop to iterate through the array
        for (int i = 0; i < N; i++) {

            // If the current element is 1
            if (arr[i] == 1) {

                // Check if there are sufficient
                // 0's between consecutive 1's to
                // insert more 1's between them
                if (i - last - 1 >= 2 * (K - 1)) {
                    cnt += (i - last - 1 - K) / (K + 1);
                }

                // Update the index of last 1
                last = i;
            }
        }

        // Condition to include the segment of
        // 0's in the last
        cnt += (N - last - 1) / (K + 1);

        // Return answer
        return cnt;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 0, 0, 0, 0, 0, 0, 0, 1, 0 };
        int N = arr.length;
        int K = 2;

        System.out.println(maximumOnes(arr, N, K));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum number
# of 1s that can be placed in array arr[]
def maximumOnes(arr, N, K) :

    # Stores the count of 1's
    cnt = 0;

    # Stores the last index of 1
    last = -(K + 1);

    # Loop to iterate through the array
    for i in range(N) :

        # If the current element is 1
        if (arr[i] == 1) :

            # Check if there are sufficient
            # 0's between consecutive 1's to
            # insert more 1's between them
            if (i - last - 1 >= 2 * (K - 1)) :
                cnt += (i - last - 1 - K) // (K + 1);
            # Update the index of last 1
            last = i;

    # Condition to include the segment of
    # 0's in the last
    cnt += (N - last - 1) // (K + 1);

    # Return answer
    return cnt;

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 0, 0, 0, 0, 0, 0, 0, 1, 0 ];
    N = len(arr);
    K = 2;

    print(maximumOnes(arr, N, K));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

    // Function to find the maximum number
    // of 1s that can be placed in array arr[]
    static int maximumOnes(int []arr, int N, int K)
    {

        // Stores the count of 1's
        int cnt = 0;

        // Stores the last index of 1
        int last = -(K + 1);

        // Loop to iterate through the array
        for (int i = 0; i < N; i++) {

            // If the current element is 1
            if (arr[i] == 1) {

                // Check if there are sufficient
                // 0's between consecutive 1's to
                // insert more 1's between them
                if (i - last - 1 >= 2 * (K - 1)) {
                    cnt += (i - last - 1 - K) / (K + 1);
                }

                // Update the index of last 1
                last = i;
            }
        }

        // Condition to include the segment of
        // 0's in the last
        cnt += (N - last - 1) / (K + 1);

        // Return answer
        return cnt;
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int []arr = { 1, 0, 0, 0, 0, 0, 0, 0, 1, 0 };
        int N = arr.Length;
        int K = 2;

        Console.WriteLine(maximumOnes(arr, N, K));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum number
// of 1s that can be placed in array arr[]
function maximumOnes(arr, N, K)
{

    // Stores the count of 1's
    var cnt = 0;

    // Stores the last index of 1
    var last = -(K + 1);

    // Loop to iterate through the array
    for (var i = 0; i < N; i++) {

        // If the current element is 1
        if (arr[i] == 1) {

            // Check if there are sufficient
            // 0's between consecutive 1's to
            // insert more 1's between them
            if (i - last - 1 >= 2 * (K - 1)) {
                cnt += parseInt((i - last - 1 - K) / (K + 1));
            }

            // Update the index of last 1
            last = i;
        }
    }

    // Condition to include the segment of
    // 0's in the last
    cnt += parseInt((N - last - 1) / (K + 1));

    // Return answer
    return cnt;
}

// Driver Code
var arr = [1, 0, 0, 0, 0, 0, 0, 0, 1, 0 ];
var N = arr.length;
var K = 2;
document.write(maximumOnes(arr, N, K));

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)