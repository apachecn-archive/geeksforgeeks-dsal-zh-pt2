# 移除一对连续的阵列元素后，最大化 1 的子阵列长度

> 原文:[https://www . geesforgeks . org/最大化一对连续数组元素移除后的 1s 子数组长度/](https://www.geeksforgeeks.org/maximize-length-of-subarray-of-1s-after-removal-of-a-pair-of-consecutive-array-elements/)

给定由 **N** 元素组成的二进制数组**arr【】**，任务是在删除单对**连续的**数组元素后，找到仅 **1** 的**子数组的**最大**可能长度。如果没有这样的子阵列，打印 **-1** 。**

**示例:**

> **输入:** arr[] = {1，1，1，0，0，1}
> **输出:** 4
> **解释:**
> 移除对{0，0}会将数组修改为{1，1，1，1}，从而最大化仅由 1 组成的最长可能子数组的长度。
> 
> **输入:** arr[] = {1，1，1，0，0，0，1}
> **输出:** 3
> **解释:**
> 从子阵列{0，0，0，1}中移除任何连续的子阵列对将保持 1 的最长可能子阵列，即{1，1，1}。

**天真方法:**
解决问题最简单的方法是[从数组中生成所有可能的连续元素对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，对于每一对，计算 **1** 的子数组的最大可能长度。最后，打印得到的这种子数组的最大可能长度。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**
按照下面给出的步骤解决问题:

*   初始化一个辅助 2D 向量 **V** 。
*   跟踪仅由 **1 的**组成的所有连续子阵列。
*   存储子阵列的**长度**、**起始索引**和**结束索引**。
*   现在，计算 **1** 的任意两个子阵之间**0**的个数。
*   根据获得的 0 计数，更新可能的子阵列最大长度:
    *   如果两个子阵列之间正好有两个 **0** ，通过比较两个子阵列的**组合长度来更新最大可能长度。**
    *   如果两个子阵列之间恰好存在一个 **0** ，通过比较两个子阵列的**组合长度–1 来更新最大可能长度。**
*   最后，打印获得的最大可能长度

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// subarray length of ones
int maxLen(int A[], int N)
{
    // Stores the length, starting
    // index and ending index of the
    // subarrays
    vector<vector<int> > v;

    for (int i = 0; i < N; i++) {

        if (A[i] == 1) {

            // S : starting index
            // of the sub-array
            int s = i, len;

            // Traverse only continuous 1s
            while (A[i] == 1 && i < N) {
                i++;
            }

            // Calculate length of the
            // sub-array
            len = i - s;

            // v[i][0] : Length of subarray
            // v[i][1] : Starting Index of subarray
            // v[i][2] : Ending Index of subarray
            v.push_back({ len, s, i - 1 });
        }
    }

    // If no such sub-array exists
    if (v.size() == 0) {
        return -1;
    }

    int ans = 0;

    // Traversing through the subarrays
    for (int i = 0; i < v.size() - 1; i++) {

        // Update maximum length
        ans = max(ans, v[i][0]);

        // v[i+1][1] : Starting index of
        // the next Sub-Array

        // v[i][2] : Ending Index of the
        // current Sub-Array

        // v[i+1][1] - v[i][2] - 1 : Count of
        // zeros between the two sub-arrays
        if (v[i + 1][1] - v[i][2] - 1 == 2) {

            // Update length of both subarrays
            // to the maximum
            ans = max(ans, v[i][0] + v[i + 1][0]);
        }
        if (v[i + 1][1] - v[i][2] - 1 == 1) {

            // Update length of both subarrays - 1
            // to the maximum
            ans = max(ans, v[i][0] + v[i + 1][0] - 1);
        }
    }

    // Check if the last subarray has
    // the maximum length
    ans = max(v[v.size() - 1][0], ans);

    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 0, 1, 0, 0, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maxLen(arr, N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the maximum
    // subarray length of ones
    static int maxLen(int A[], int N)
    {

        // Stores the length, starting
        // index and ending index of the
        // subarrays
        List<List<Integer> > v = new ArrayList<>();

        for (int i = 0; i < N; i++) {
            if (A[i] == 1) {

                // S : starting index
                // of the sub-array
                int s = i, len;

                // Traverse only continuous 1s
                while (i < N && A[i] == 1) {
                    i++;
                }

                // Calculate length of the
                // sub-array
                len = i - s;

                // v[i][0] : Length of subarray
                // v[i][1] : Starting Index of subarray
                // v[i][2] : Ending Index of subarray
                v.add(Arrays.asList(len, s, i - 1));
            }
        }

        // If no such sub-array exists
        if (v.size() == 0) {
            return -1;
        }

        int ans = 0;

        // Traversing through the subarrays
        for (int i = 0; i < v.size() - 1; i++) {

            // Update maximum length
            ans = Math.max(ans, v.get(i).get(0));

            // v[i+1][1] : Starting index of
            // the next Sub-Array

            // v[i][2] : Ending Index of the
            // current Sub-Array

            // v[i+1][1] - v[i][2] - 1 : Count of
            // zeros between the two sub-arrays
            if (v.get(i + 1).get(1) - v.get(i).get(2) - 1
                == 2) {

                // Update length of both subarrays
                // to the maximum
                ans = Math.max(ans,
                               v.get(i).get(0)
                                   + v.get(i + 1).get(0));
            }
            if (v.get(i + 1).get(1) - v.get(i).get(2) - 1
                == 1) {

                // Update length of both subarrays - 1
                // to the maximum
                ans = Math.max(
                    ans, v.get(i).get(0)
                             + v.get(i + 1).get(0) - 1);
            }
        }

        // Check if the last subarray has
        // the maximum length
        ans = Math.max(v.get(v.size() - 1).get(0), ans);

        return ans;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 1, 0, 1, 0, 0, 1 };
        int N = arr.length;

        System.out.println(maxLen(arr, N));
    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum
# subarray length of ones

def maxLen(A, N):

    # Stores the length, starting
    # index and ending index of the
    # subarrays
    v = []

    i = 0
    while i < N:
        if (A[i] == 1):

            # S : starting index
            # of the sub-array
            s = i

            # Traverse only continuous 1s
            while (i < N and A[i] == 1):
                i += 1

            # Calculate length of the
            # sub-array
            le = i - s

            # v[i][0] : Length of subarray
            # v[i][1] : Starting Index of subarray
            # v[i][2] : Ending Index of subarray
            v.append([le, s, i - 1])

        i += 1

    # If no such sub-array exists
    if (len(v) == 0):
        return -1

    ans = 0

    # Traversing through the subarrays
    for i in range(len(v) - 1):

        # Update maximum length
        ans = max(ans, v[i][0])

        # v[i+1][1] : Starting index of
        # the next Sub-Array

        # v[i][2] : Ending Index of the
        # current Sub-Array

        # v[i+1][1] - v[i][2] - 1 : Count of
        # zeros between the two sub-arrays
        if (v[i + 1][1] - v[i][2] - 1 == 2):

            # Update length of both subarrays
            # to the maximum
            ans = max(ans, v[i][0] + v[i + 1][0])

        if (v[i + 1][1] - v[i][2] - 1 == 1):

            # Update length of both subarrays - 1
            # to the maximum
            ans = max(ans, v[i][0] + v[i + 1][0] - 1)

    # Check if the last subarray has
    # the maximum length
    ans = max(v[len(v) - 1][0], ans)

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [1, 0, 1, 0, 0, 1]
    N = len(arr)

    print(maxLen(arr, N))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the maximum
    // subarray length of ones
    static int maxLen(int []A, int N)
    {

        // Stores the length, starting
        // index and ending index of the
        // subarrays
        List<List<int>> v = new List<List<int>>();

        for (int i = 0; i < N; i++)
        {
            if (A[i] == 1)
            {

                // S : starting index
                // of the sub-array
                int s = i, len;

                // Traverse only continuous 1s
                while (i < N && A[i] == 1)
                {
                    i++;
                }

                // Calculate length of the
                // sub-array
                len = i - s;

                // v[i,0] : Length of subarray
                // v[i,1] : Starting Index of subarray
                // v[i,2] : Ending Index of subarray
                List<int> l = new List<int>{len, s, i - 1};
                v.Add(l);
            }
        }

        // If no such sub-array exists
        if (v.Count == 0)
        {
            return -1;
        }

        int ans = 0;

        // Traversing through the subarrays
        for (int i = 0; i < v.Count - 1; i++)
        {

            // Update maximum length
            ans = Math.Max(ans, v[i][0]);

            // v[i+1,1] : Starting index of
            // the next Sub-Array

            // v[i,2] : Ending Index of the
            // current Sub-Array

            // v[i+1,1] - v[i,2] - 1 : Count of
            // zeros between the two sub-arrays
            if (v[i + 1][1] - v[i][2] - 1
                == 2) {

                // Update length of both subarrays
                // to the maximum
                ans = Math.Max(ans,
                               v[i][0]
                                   + v[i + 1][0]);
            }
            if (v[i + 1][1] - v[i][2] - 1
                == 1)
            {

                // Update length of both subarrays - 1
                // to the maximum
                ans = Math.Max(
                    ans, v[i][0]
                             + v[i + 1][0] - 1);
            }
        }

        // Check if the last subarray has
        // the maximum length
        ans = Math.Max(v[v.Count - 1][0], ans);

        return ans;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int []arr = { 1, 0, 1, 0, 0, 1 };
        int N = arr.Length;

        Console.WriteLine(maxLen(arr, N));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to find the maximum
// subarray length of ones
function maxLen(A, N)
{
    // Stores the length, starting
    // index and ending index of the
    // subarrays
    var v = [];

    for (var i = 0; i < N; i++) {

        if (A[i] == 1) {

            // S : starting index
            // of the sub-array
            var s = i, len;

            // Traverse only continuous 1s
            while (A[i] == 1 && i < N) {
                i++;
            }

            // Calculate length of the
            // sub-array
            len = i - s;

            // v[i][0] : Length of subarray
            // v[i][1] : Starting Index of subarray
            // v[i][2] : Ending Index of subarray
            v.push([len, s, i - 1]);
        }
    }

    // If no such sub-array exists
    if (v.length == 0) {
        return -1;
    }

    var ans = 0;

    // Traversing through the subarrays
    for (var i = 0; i < v.length - 1; i++) {

        // Update maximum length
        ans = Math.max(ans, v[i][0]);

        // v[i+1][1] : Starting index of
        // the next Sub-Array

        // v[i][2] : Ending Index of the
        // current Sub-Array

        // v[i+1][1] - v[i][2] - 1 : Count of
        // zeros between the two sub-arrays
        if (v[i + 1][1] - v[i][2] - 1 == 2) {

            // Update length of both subarrays
            // to the maximum
            ans = Math.max(ans, v[i][0] + v[i + 1][0]);
        }
        if (v[i + 1][1] - v[i][2] - 1 == 1) {

            // Update length of both subarrays - 1
            // to the maximum
            ans = Math.max(ans, v[i][0] + v[i + 1][0] - 1);
        }
    }

    // Check if the last subarray has
    // the maximum length
    ans = Math.max(v[v.length - 1][0], ans);

    return ans;
}

// Driver Code
var arr = [1, 0, 1, 0, 0, 1];
var N = arr.length;
document.write( maxLen(arr, N));

</script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**方法二:**

**前缀和后缀数组**

计算 0 出现之间的 1 的数量。如果我们找到 0，那么如果我们跳过这两个连续的元素，我们需要找到 1 的最大长度。我们可以使用前缀和后缀数组的概念来解决这个问题。

找出从数组开始的连续 1 的长度，并将计数存储在前缀数组中。找出从数组末尾开始的连续 1 的长度，并将计数存储在结束数组中。

我们遍历两个数组，找到 1 的最大个数。

**算法:**

1.  创建两个长度为 n 的数组前缀和后缀。
2.  初始化前缀[0]=0，前缀[1]=0 和后缀[n-1]=0，后缀[n-2]=0。这告诉我们在前 2 个元素之前和后 2 个元素之后没有 1。
3.  运行从 2 到 n-1 的循环:
    *   If arr[i-2]==1
        *   前缀[I]=前缀[i-1]+1
    *   否则如果 arr[i-2]==0:
        *   前缀[i]=0
4.  从 n-3 到 0 运行循环:
    *   If arr[i+2]==1
        *   后缀[I]=后缀[i+1]+1
    *   否则如果 arr[i-2]==0:
        *   后缀[i]=0
5.  初始化答案=INT_MIN
6.  对于 i=0 到 n-2://通过跳过当前元素和下一个元素来计算 1 的数量。
7.  答案=max(答案，前缀[I+1]+后缀[i]
8.  打印答案

**实施:**

## C++

```
// C++ program to find the maximum count of 1s
#include <bits/stdc++.h>
using namespace std;

void maxLengthOf1s(vector<int> arr, int n)
{
    vector<int> prefix(n, 0);
    for (int i = 2; i < n; i++)
    {
        // If arr[i-2]==1 then we increment the
        // count of occurences of 1's
        if (arr[i - 2]
            == 1)
            prefix[i] = prefix[i - 1] + 1;

        // else we initialise the count with 0
        else
            prefix[i] = 0;
    }
    vector<int> suffix(n, 0);
    for (int i = n - 3; i >= 0; i--)
    {
        // If arr[i+2]==1 then we increment the
        // count of occurences of 1's
        if (arr[i + 2] == 1)
            suffix[i] = suffix[i + 1] + 1;

        // else we initialise the count with 0
        else
            suffix[i] = 0;
    }
    int ans = 0;
    for (int i = 0; i < n - 1; i++)
    {
        // We get the maximum count by
        // skipping the current and the
        // next element.
        ans = max(ans, prefix[i + 1] + suffix[i]);
    }
    cout << ans << "\n";
}

// Driver Code
int main()
{
    int n = 6;
    vector<int> arr = { 1, 1, 1, 0, 1, 1 };
    maxLengthOf1s(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum count of 1s
class GFG{

public static void maxLengthOf1s(int arr[], int n)
{
    int prefix[] = new int[n];

    for(int i = 2; i < n; i++)
    {

        // If arr[i-2]==1 then we increment
        // the count of occurences of 1's
        if (arr[i - 2] == 1)
            prefix[i] = prefix[i - 1] + 1;

        // Else we initialise the count with 0
        else
            prefix[i] = 0;
    }
    int suffix[] = new int[n];
    for(int i = n - 3; i >= 0; i--)
    {

        // If arr[i+2]==1 then we increment
        // the count of occurences of 1's
        if (arr[i + 2] == 1)
            suffix[i] = suffix[i + 1] + 1;

        // Else we initialise the count with 0
        else
            suffix[i] = 0;
    }
    int ans = 0;
    for(int i = 0; i < n - 1; i++)
    {

        // We get the maximum count by
        // skipping the current and the
        // next element.
        ans = Math.max(ans, prefix[i + 1] +
                            suffix[i]);
    }
    System.out.println(ans);
}

// Driver code
public static void main(String[] args)
{
    int n = 6;
    int arr[] = { 1, 1, 1, 0, 1, 1 };

    maxLengthOf1s(arr, n);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python program to find the maximum count of 1s
def maxLengthOf1s(arr, n):
    prefix = [0 for i in range(n)]
    for i in range(2, n):

        # If arr[i-2]==1 then we increment
        # the count of occurences of 1's
        if(arr[i - 2] == 1):
            prefix[i] = prefix[i - 1] + 1

        # Else we initialise the count with 0
        else:
            prefix[i] = 0
    suffix = [0 for i in range(n)]
    for i in range(n - 3, -1, -1):

        # If arr[i+2]==1 then we increment
        # the count of occurences of 1's
        if(arr[i + 2] == 1):
            suffix[i] = suffix[i + 1] + 1

        # Else we initialise the count with 0
        else:
            suffix[i] = 0
    ans = 0
    for i in range(n - 1):

        # We get the maximum count by
        # skipping the current and the
        # next element.
        ans = max(ans, prefix[i + 1] + suffix[i])
    print(ans)

# Driver code
n = 6
arr = [1, 1, 1, 0, 1, 1]
maxLengthOf1s(arr, n)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to find the maximum count of 1s
using System;

class GFG{

static void maxLengthOf1s(int[] arr, int n)
{
    int[] prefix = new int[n];

    for(int i = 2; i < n; i++)
    {

        // If arr[i-2]==1 then we increment
        // the count of occurences of 1's
        if (arr[i - 2] == 1)
            prefix[i] = prefix[i - 1] + 1;

        // Else we initialise the count with 0
        else
            prefix[i] = 0;
    }
    int[] suffix = new int[n];
    for(int i = n - 3; i >= 0; i--)
    {

        // If arr[i+2]==1 then we increment
        // the count of occurences of 1's
        if (arr[i + 2] == 1)
            suffix[i] = suffix[i + 1] + 1;

        // Else we initialise the count with 0
        else
            suffix[i] = 0;
    }
    int ans = 0;
    for(int i = 0; i < n - 1; i++)
    {

        // We get the maximum count by
        // skipping the current and the
        // next element.
        ans = Math.Max(ans, prefix[i + 1] + suffix[i]);
    }
    Console.WriteLine(ans);
}

// Driver code
static void Main()
{
    int n = 6;
    int[] arr = { 1, 1, 1, 0, 1, 1 };

    maxLengthOf1s(arr, n);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript program to find
    // the maximum count of 1s

    function maxLengthOf1s(arr, n)
    {
        let prefix = new Array(n);
        prefix.fill(0);

        for(let i = 2; i < n; i++)
        {

            // If arr[i-2]==1 then we increment
            // the count of occurences of 1's
            if (arr[i - 2] == 1)
                prefix[i] = prefix[i - 1] + 1;

            // Else we initialise the count with 0
            else
                prefix[i] = 0;
        }
        let suffix = new Array(n);
        suffix.fill(0);
        for(let i = n - 3; i >= 0; i--)
        {

            // If arr[i+2]==1 then we increment
            // the count of occurences of 1's
            if (arr[i + 2] == 1)
                suffix[i] = suffix[i + 1] + 1;

            // Else we initialise the count with 0
            else
                suffix[i] = 0;
        }
        let ans = 0;
        for(let i = 0; i < n - 1; i++)
        {

            // We get the maximum count by
            // skipping the current and the
            // next element.
            ans = Math.max(ans, prefix[i + 1] + suffix[i]);
        }
        document.write(ans);
    }

    let n = 6;
    let arr = [ 1, 1, 1, 0, 1, 1 ];

    maxLengthOf1s(arr, n);

</script>
```

**Output**

```
4
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)