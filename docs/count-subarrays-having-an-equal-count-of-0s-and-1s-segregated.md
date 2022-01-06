# 计数相等的 0 和 1 分离的子阵列

> 原文:[https://www . geeksforgeeks . org/count-subarrays-具有相等的 0s 和 1s 计数-隔离/](https://www.geeksforgeeks.org/count-subarrays-having-an-equal-count-of-0s-and-1s-segregated/)

给定一个二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算具有相同计数的 **0** s 和 **1** s 的子阵列的数量，并且所有的 **0** s 和 **1** s 被连续放置在该子阵列中。

**示例:**

> **输入:** arr[] = {1，0，1，1}
> **输出:** 2
> **说明:**满足给定条件的子阵为{1，0}和{0，1}。因此，这种子阵列的数量是 2。
> 
> **输入:** arr[] = {1，1，0，0，1，0}
> **输出:** 4
> **说明:**满足给定条件的子阵为{1，1，0，0}、{1，0}、{0，1}、{1，0}。因此，这种子阵列的数量是 4。

**天真方法:**最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每对不相等的相邻元素，迭代当前索引的左右，检查 **1** s 和 **0** s 的计数是否相等。增加子阵列的计数，直到发现为假。完成数组遍历后，打印子数组的总数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count subarrays
// having equal count of 0s and 1s
// with all 0s and all 1s grouped together
void countSubarrays(int A[], int N)
{
    // Stores the count of subarrays
    int ans = 0;

    for (int i = 0; i < N - 1; i++) {

        // If current element is different
        // from the next array element
        if (A[i] != A[i + 1]) {

            // Increment count
            ans++;

            // Count the frequency of
            // 1s and 0s
            for (int j = i - 1, k = i + 2;
                 j >= 0 && k < N
                 && A[j] == A[i]
                 && A[k] == A[i + 1];
                 j--, k++) {

                // Increment count
                ans++;
            }
        }
    }

    // Print the final count
    cout << ans << "\n";
}

// Driver Code
int main()
{
    int A[] = { 1, 1, 0, 0, 1, 0 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    countSubarrays(A, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to count subarrays
// having equal count of 0s and 1s
// with all 0s and all 1s grouped together
static void countSubarrays(int A[], int N)
{

    // Stores the count of subarrays
    int ans = 0;

    for (int i = 0; i < N - 1; i++)
    {

        // If current element is different
        // from the next array element
        if (A[i] != A[i + 1])
        {

            // Increment count
            ans++;

            // Count the frequency of
            // 1s and 0s
            for (int j = i - 1, k = i + 2;
                 j >= 0 && k < N
                 && A[j] == A[i]
                 && A[k] == A[i + 1];
                 j--, k++)
            {

                // Increment count
                ans++;
            }
        }
    }

    // Print the final count
    System.out.print(ans+ "\n");
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 1, 1, 0, 0, 1, 0 };
    int N = A.length;

    // Function Call
    countSubarrays(A, N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count subarrays
# having equal count of 0s and 1s
# with all 0s and all 1s grouped together
def countSubarrays(A, N) :

    # Stores the count of subarrays
    ans = 0;

    for i in range(N - 1) :

        # If current element is different
        # from the next array element
        if (A[i] != A[i + 1]) :

            # Increment count
            ans += 1;

            # Count the frequency of
            # 1s and 0s
            j = i - 1; k = i + 2;
            while (j >= 0 and k < N and A[j] == A[i] and A[k] == A[i + 1]) :

                # Increment count
                ans += 1;

                j -= 1;
                k += 1;

    # Print the final count
    print(ans);

# Driver Code
if __name__ == "__main__" :

    A = [ 1, 1, 0, 0, 1, 0 ];
    N = len(A);

    # Function Call
    countSubarrays(A, N);

    # This code is contributed by AnkitRai01
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count subarrays
// having equal count of 0s and 1s
// with all 0s and all 1s grouped together
static void countSubarrays(int[] A, int N)
{

    // Stores the count of subarrays
    int ans = 0;

    for(int i = 0; i < N - 1; i++)
    {

        // If current element is different
        // from the next array element
        if (A[i] != A[i + 1])
        {

            // Increment count
            ans++;

            // Count the frequency of
            // 1s and 0s
            for(int j = i - 1, k = i + 2;
                    j >= 0 && k < N &&
                       A[j] == A[i] &&
                       A[k] == A[i + 1];
                    j--, k++)
            {

                // Increment count
                ans++;
            }
        }
    }

    // Print the final count
    Console.Write(ans + "\n");
}

// Driver Code
public static void Main()
{
    int[] A = { 1, 1, 0, 0, 1, 0 };
    int N = A.Length;

    // Function Call
    countSubarrays(A, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the above approach

// Function to count subarrays
// having equal count of 0s and 1s
// with all 0s and all 1s grouped together
function countSubarrays(A, N)
{

    // Stores the count of subarrays
    let ans = 0;

    for (let i = 0; i < N - 1; i++)
    {

        // If current element is different
        // from the next array element
        if (A[i] != A[i + 1])
        {

            // Increment count
            ans++;

            // Count the frequency of
            // 1s and 0s
            for (let j = i - 1, k = i + 2;
                 j >= 0 && k < N
                 && A[j] == A[i]
                 && A[k] == A[i + 1];
                 j--, k++)
            {

                // Increment count
                ans++;
            }
        }
    }

    // Print the final count
    document.write(ans+ "<br/>");
}

// Driver Code

    let A = [ 1, 1, 0, 0, 1, 0 ];
    let N = A.length;

    // Function Call
    countSubarrays(A, N);

</script>
```

**Output:** 

```
4
```

**时间复杂度:***O(N<sup>2</sup>)*
*T8】辅助空间: O(1)*

**高效方法:**要优化上述方法，请执行以下步骤:

*   初始化一个变量，比如 **res** ，来存储子阵列的计数。
*   用数组的第一个值和数组 **cnt[]** 初始化一个变量，比如 **curr** ，以跟踪连续的元素。
*   [遍历数组](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)并执行以下步骤:
    *   如果当前元素等于 **curr** ，则增加**CNT【】**的最后一个值。
    *   否则，将 **curr** 更新到当前元素，并将 **1** 追加到数组 **cnt[]** 。
*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**CNT【】**求相邻元素的最小值之和，并将其加入变量 **res** 。这确保了元素的频率相等。
*   完成上述步骤后，打印 **res** 的值作为子阵列的合成计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count subarrays
// having equal count of 0s and 1s
// with all 0s and all 1s grouped together
void countSubarrays(int A[], int N)
{

    // Stores the count
    int res = 0;

    // Initialize cur with first element
    int curr = A[0];
    vector<int> cnt = {1};
    for (int c = 1; c < N; c++)
    {

        // If the next element is same
        // as the current element
        if (A == curr)

            // Increment count
            cnt[cnt.size() - 1]++;
        else

            // Update curr
            curr = A;
        cnt.push_back(1);
    }

    // Iterate over the array count
    for (int i = 1; i < cnt.size(); i++)
    {

        // Consider the minimum
        res += min(cnt[i - 1], cnt[i]);
    }
    cout << (res - 1);
}

// Driver code
int main()
{
    // Given arr[]
    int A[] = { 1, 1, 0, 0, 1, 0 };   
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    countSubarrays(A, N);
    return 0;
}

// This code is contributed by divyesh072019
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Vector;

// Java program for the above approach
class GFG {

    // Function to count subarrays
    // having equal count of 0s and 1s
    // with all 0s and all 1s grouped together
    static void countSubarrays(int[] A)
    {

        // Stores the count
        int res = 0;

        // Initialize cur with first element
        int curr = A[0];
        int[] cnt = new int[A.length];
        cnt[0] = 1;
        for (int c = 1; c < A.length; c++) {

            // If the next element is same
            // as the current element
            if (A == curr)

                // Increment count

                cnt++;
            else

                // Update curr
                curr = A;
            cnt = 1;
        }

        // Iterate over the array count
        for (int i = 1; i < cnt.length; i++) {

            // Consider the minimum
            res += Math.min(cnt[i - 1], cnt[i]);
        }
        System.out.println(res - 1);
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given arr[]
        int[] A = { 1, 1, 0, 0, 1, 0 };

        // Function Call
        countSubarrays(A);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count subarrays
# having equal count of 0s and 1s
# with all 0s and all 1s grouped together
def countSubarrays(A):

    # Stores the count
    res = 0

    # Initialize cur with first element
    curr, cnt = A[0], [1]
    for c in A[1:]:

        # If the next element is same
        # as the current element
        if c == curr:

            # Increment count
            cnt[-1] += 1
        else:

            # Update curr
            curr = c
        cnt.append(1)

    # Iterate over the array count
    for i in range(1, len(cnt)):

        # Consider the minimum
        res += min(cnt[i - 1], cnt[i])

    print(res - 1)

# Given arr[]
A = [1, 1, 0, 0, 1, 0]

# Function Call
countSubarrays(A)
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count subarrays
// having equal count of 0s and 1s
// with all 0s and all 1s grouped together
static void countSubarrays(int[] A)
{

    // Stores the count
    int res = 0;

    // Initialize cur with first element
    int curr = A[0];
    int[] cnt = new int[A.Length];
    cnt[0] = 1;

    for(int c = 1; c < A.Length; c++)
    {

        // If the next element is same
        // as the current element
        if (A == curr)

            // Increment count
            cnt++;
        else

            // Update curr
            curr = A;

        cnt = 1;
    }

    // Iterate over the array count
    for(int i = 1; i < cnt.Length; i++)
    {

        // Consider the minimum
        res += Math.Min(cnt[i - 1], cnt[i]);
    }
    Console.WriteLine(res - 1);
}

// Driver code
public static void Main(String[] args)
{

    // Given []arr
    int[] A = { 1, 1, 0, 0, 1, 0 };

    // Function Call
    countSubarrays(A);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to count subarrays
// having equal count of 0s and 1s
// with all 0s and all 1s grouped together
function countSubarrays( A, N)
{

    // Stores the count
    var res = 0;

    // Initialize cur with first element
    var curr = A[0];
    var cnt = [];
    cnt.fill(1)
    for (var c = 1; c < N; c++)
    {

        // If the next element is same
        // as the current element
        if (A == curr)

            // Increment count
            cnt[cnt.length - 1]++;
        else

            // Update curr
            curr = A;
        cnt.push(1);
    }

    // Iterate over the array count
    for (var i = 1; i < cnt.length; i++)
    {

        // Consider the minimum
        res += Math.min(cnt[i - 1], cnt[i]);
    }
    document.write (res);
}

var A = [ 1, 1, 0, 0, 1, 0 ];   
var N = A.length;

    // Function Call
    countSubarrays(A, N);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)