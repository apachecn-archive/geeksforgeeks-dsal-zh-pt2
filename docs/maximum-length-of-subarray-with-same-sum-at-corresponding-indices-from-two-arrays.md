# 两个阵列对应索引处和相同的子阵列的最大长度

> 原文:[https://www . geeksforgeeks . org/两个数组对应索引相同的子数组最大长度/](https://www.geeksforgeeks.org/maximum-length-of-subarray-with-same-sum-at-corresponding-indices-from-two-arrays/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**均由 **N** 个整数组成，任务是找到[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)**【I，j】**的最大长度，使得**A【I…j】**的和等于**B【I…j】**。

**示例:**

> **输入:** A[] = {1，1，0，1}，B[] = {0，1，1，0}
> **输出:** 3
> **解释:**对于(I，j) = (0，2)，A[0… 2]之和= B[0…2]之和(即 A[0]+A[1]+A[2]= B[0]+B[1]+B[2]=>1+1+0 = 0 类似地，对于(I，j) = (1，3)，A[1… 3] = B[1… 3]的和。因此，和相等的子阵列的长度是 3，这是最大可能。
> 
> **输入:** A[] = {1，2，3，4}，B[] = {4，3，2，1 }
> T3】输出: 4

**方法:**在[无序地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)的帮助下，使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决给定的问题。可以观察到，对于一对 **(i，j)** ，如果**A【I…j】**之和=**B【I…j】**之和，那么![\sum_{x=i}^{j} (A[x] - B[x]) = 0        ](img/605d52a3425bb3848eaa16b870fe192c.png "Rendered by QuickLaTeX.com")一定成立。因此，可以创建差**(A[x]–B[x])**的[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。可以观察到，前缀和数组中的重复值表示两个重复值之间的子数组之和必须为 0。因此，在变量**最大尺寸**中记录这些[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大尺寸，这将是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include "bits/stdc++.h"
using namespace std;

// Function to find maximum length of subarray
// of array A and B having equal sum
int maxLength(vector<int>& A, vector<int>& B)
{
    int n = A.size();

    // Stores the maximum size of valid subarray
    int maxSize = 0;

    // Stores the prefix sum of the difference
    // of the given arrays
    unordered_map<int, int> pre;
    int diff = 0;
    pre[0] = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // Add the difference of the
        // corresponding array element
        diff += (A[i] - B[i]);

        // If current difference is not present
        if (pre.find(diff) == pre.end()) {
            pre = i + 1;
        }

        // If current difference is present,
        // update the value of maxSize
        else {
            maxSize = max(maxSize, i - pre + 1);
        }
    }

    // Return the maximum length
    return maxSize;
}

// Driver Code
int main()
{
    vector<int> A = { 1, 2, 3, 4 };
    vector<int> B = { 4, 3, 2, 1 };

    cout << maxLength(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.HashMap;
class GFG {

    // Function to find maximum length of subarray
    // of array A and B having equal sum
    public static int maxLength(int[] A, int[] B) {
        int n = A.length;

        // Stores the maximum size of valid subarray
        int maxSize = 0;

        // Stores the prefix sum of the difference
        // of the given arrays
        HashMap<Integer, Integer> pre = new HashMap<Integer, Integer>();
        int diff = 0;
        pre.put(0, 0);

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // Add the difference of the
            // corresponding array element
            diff += (A[i] - B[i]);

            // If current difference is not present
            if (!pre.containsKey(diff)) {
                pre.put(diff, i + 1);
            }

            // If current difference is present,
            // update the value of maxSize
            else {
                maxSize = Math.max(maxSize, i - pre.get(diff));
            }
        }

        // Return the maximum length
        return maxSize;
    }

    // Driver Code
    public static void main(String args[]) {
        int[] A = { 1, 2, 3, 4 };
        int[] B = { 4, 3, 2, 1 };

        System.out.println(maxLength(A, B));

    }
}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find maximum length of subarray
# of array A and B having equal sum

def maxLength(A,  B):

    n = len(A)

    # Stores the maximum size of valid subarray
    maxSize = 0

    # Stores the prefix sum of the difference
    # of the given arrays
    pre = {}
    diff = 0
    pre[0] = 0

    # Traverse the given array
    for i in range(0, n):

        # Add the difference of the
        # corresponding array element
        diff += (A[i] - B[i])

        # If current difference is not present
        if (not (diff in pre)):
            pre = i + 1

        # If current difference is present,
        # update the value of maxSize
        else:
            maxSize = max(maxSize, i - pre + 1)

    # Return the maximum length
    return maxSize

# Driver Code
if __name__ == "__main__":

    A = [1, 2, 3, 4]
    B = [4, 3, 2, 1]

    print(maxLength(A, B))

# This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

    // Function to find maximum length of subarray
    // of array A and B having equal sum
    public static int maxLength(int[] A, int[] B) {
        int n = A.Length;

        // Stores the maximum size of valid subarray
        int maxSize = 0;

        // Stores the prefix sum of the difference
        // of the given arrays
        Dictionary<int, int> pre =
                new Dictionary<int, int>();

        int diff = 0;
        pre.Add(0, 0);

        // Traverse the given array
        for (int i = 0; i < n; i++) {

            // Add the difference of the
            // corresponding array element
            diff += (A[i] - B[i]);

            // If current difference is not present
            if (!pre.ContainsKey(diff)) {
                pre.Add(diff, i + 1);
            }

            // If current difference is present,
            // update the value of maxSize
            else {
                maxSize = Math.Max(maxSize, i - pre[(diff)]);
            }
        }

        // Return the maximum length
        return maxSize;
    }

// Driver Code
public static void Main()
{
    int[] A = { 1, 2, 3, 4 };
    int[] B = { 4, 3, 2, 1 };

    Console.Write(maxLength(A, B));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find maximum length of subarray
    // of array A and B having equal sum
    const maxLength = (A, B) => {
        let n = A.length;

        // Stores the maximum size of valid subarray
        let maxSize = 0;

        // Stores the prefix sum of the difference
        // of the given arrays
        let pre = {};
        let diff = 0;
        pre[0] = 0;

        // Traverse the given array
        for (let i = 0; i < n; i++) {

            // Add the difference of the
            // corresponding array element
            diff += (A[i] - B[i]);

            // If current difference is not present

            if (!(diff in pre)) {
                pre = i + 1;
            }

            // If current difference is present,
            // update the value of maxSize
            else {
                maxSize = Math.max(maxSize, i - pre + 1);
            }
        }

        // Return the maximum length
        return maxSize;
    }

    // Driver Code

    let A = [1, 2, 3, 4];
    let B = [4, 3, 2, 1];

    document.write(maxLength(A, B));

// This code is contributed by rakeshsahni.
</script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)