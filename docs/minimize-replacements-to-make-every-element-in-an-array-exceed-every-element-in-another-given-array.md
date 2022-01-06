# 尽量减少替换，使一个数组中的每个元素都超过另一个给定数组中的每个元素

> 原文:[https://www . geeksforgeeks . org/最小化替换使数组中的每个元素超过另一个给定数组中的每个元素/](https://www.geeksforgeeks.org/minimize-replacements-to-make-every-element-in-an-array-exceed-every-element-in-another-given-array/)

给定两个大小分别为 **N** 和 **M** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**A【】**和**B【】**，其中每个元素都在**【0，9】**的范围内，任务是通过将任意元素从任意数组更改为**范围内的任意数字，使数组**A【】**的每个元素严格大于或小于数组**B【】**中的每个元素**

****示例:****

> ****输入:** A[] = [0，1，0]，B[] = [2，0，0]
> **输出:** 2
> **解释:**
> 将数组 B[]修改为[2，2，2]会使数组 A[]中的每个元素严格小于数组 B[]中的每个元素。
> 因此，所需的最小更改次数= 2。**
> 
> ****输入:** A[] = [0，0，1，3，3]，B[] = [0，2，3]
> **输出:** 3
> **解释:**
> 将数组 B[]修改为[4，4，4]会使数组 A[]中的每个元素严格小于数组 B[]中的每个元素。
> 因此，所需的最小更改次数= 3。**

****方法:**解决给定问题的思路是使用大小为 **10** 的两个辅助数组**前缀 _a[]** 和**前缀 _b[]** ，其中**前缀 _a[i]** 和**前缀 _b[i]** 分别存储数组中的元素个数 **A[] ≤ i** 和数组中的元素个数 **B[] ≤ i** 按照以下步骤解决问题:**

*   **用 **{0}** 初始化两个数组，**前缀 _a[]** 和**前缀 _b[]** 大小为 **10** 。**
*   **[将数组 **A[]** 和 **B[]** 中每个元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率分别存储在数组**前缀 _a** 和**前缀 _b** 中。**
*   **通过使用变量 **i** 在范围**【1，9】**中迭代[对数组](https://www.geeksforgeeks.org/range-based-loop-c/) **前缀 _a** 执行[前缀求和，并将**前缀 _a[i]** 更新为**(前缀[i] +前缀 _ a[I–1])**。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)**
*   **对数组**前缀 _b[]** 重复上述步骤。**
*   **[使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)****【0，9】**中迭代

    *   存储操作数，使数组中的每个元素 **A[]** 严格大于数字 **i** ，使数组中的每个元素 **B[]** 小于数字 **i** 在一个变量中，比如说 **X** 。
    *   用**前缀 _ a[I]+M–前缀 _b[i]** 初始化。
    *   同样，存储操作数，使数组中的每个元素 **B[]** 严格大于数字 **i** ，并使数组中的每个元素 **A[]** 小于数字 **i** 在一个变量中，比如 **Y.**
    *   用**前缀 _ b[I]+N–前缀 _a[i]** 初始化。
    *   将整体最小操作数更新为 **X** 和**Y**T5 的[最小值。将获得的最小值存储在一个变量中，比如**和**。](https://www.geeksforgeeks.org/stdmin-in-cpp/)**** 
*   ****完成上述步骤后，打印**和**的值作为结果。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimize
// replacements to make every element
// in the array A[] strictly greater
// than every element in B[] or vice-versa
void MinTime(int* a, int* b, int n, int m)
{

    // Store the final result
    int ans = INT_MAX;

    // Create two arrays and
    // initialize with 0s
    int prefix_a[10] = { 0 };
    int prefix_b[10] = { 0 };

    // Traverse the array a[]
    for (int i = 0; i < n; i++) {

        // Increment prefix_a[a[i]] by 1
        prefix_a[a[i]]++;
    }

    // Traverse the array b[]
    for (int i = 0; i < m; i++) {

        // Increment prefix_b[b[i]] by 1
        prefix_b[b[i]]++;
    }

    // Calculate prefix sum
    // of the array a[]
    for (int i = 1; i <= 9; i++) {
        prefix_a[i] += prefix_a[i - 1];
    }

    // Calculate prefix sum
    // of the array b[]
    for (int i = 1; i <= 9; i++) {
        prefix_b[i] += prefix_b[i - 1];
    }

    // Iterate over the range [0, 9]
    for (int i = 0; i <= 9; i++) {

        // Make every element in array
        // a[] strictly greater than digit
        // i and make every element in the
        // array b[] less than digit i
        ans = min(ans, prefix_a[i] + m
                           - prefix_b[i]);

        // Make every element in array
        // b[] strictly greater than digit
        // i and make every element in
        // array a[] less than digit i
        ans = min(ans, n - prefix_a[i]
                           + prefix_b[i]);
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    int A[] = { 0, 0, 1, 3, 3 };
    int B[] = { 2, 0, 3 };
    int N = sizeof(A) / sizeof(A[0]);
    int M = sizeof(B) / sizeof(B[0]);

    MinTime(A, B, N, M);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;

class GFG{

 // Function to find the minimize
// replacements to make every element
// in the array A[] strictly greater
// than every element in B[] or vice-versa
static void MinTime(int []a, int []b, int n, int m)
{

    // Store the final result
    int ans = 2147483647;

    // Create two arrays and
    // initialize with 0s
    int []prefix_a = new int[10];
    int []prefix_b = new int[10];

    // Traverse the array a[]
    for (int i = 0; i < n; i++) {

        // Increment prefix_a[a[i]] by 1
        prefix_a[a[i]]++;
    }

    // Traverse the array b[]
    for (int i = 0; i < m; i++) {

        // Increment prefix_b[b[i]] by 1
        prefix_b[b[i]]++;
    }

    // Calculate prefix sum
    // of the array a[]
    for (int i = 1; i <= 9; i++) {
        prefix_a[i] += prefix_a[i - 1];
    }

    // Calculate prefix sum
    // of the array b[]
    for (int i = 1; i <= 9; i++) {
        prefix_b[i] += prefix_b[i - 1];
    }

    // Iterate over the range [0, 9]
    for (int i = 0; i <= 9; i++) {

        // Make every element in array
        // a[] strictly greater than digit
        // i and make every element in the
        // array b[] less than digit i
        ans = Math.min(ans, prefix_a[i] + m
                           - prefix_b[i]);

        // Make every element in array
        // b[] strictly greater than digit
        // i and make every element in
        // array a[] less than digit i
        ans = Math.min(ans, n - prefix_a[i]
                           + prefix_b[i]);
    }

    // Print the answer
    System.out.println(ans);
}

// Driver Code
public static void main(String [] args)
{
    int []A = { 0, 0, 1, 3, 3 };
    int []B = { 2, 0, 3 };
    int N = A.length;
    int M = B.length;

    MinTime(A, B, N, M);
}
}

// This code is contributed by chitranayal.**
```

## ****蟒蛇 3****

```
**# Python program for the above approach

# Function to find the minimize
# replacements to make every element
# in the array A[] strictly greater
# than every element in B[] or vice-versa
def MinTime(a, b, n, m):

    # Store the final result
    ans = float('inf')

    # Create two arrays and
    # initialize with 0s
    prefix_a = [ 0 ]*10
    prefix_b = [ 0 ]*10

    # Traverse the array a[]
    for i in range(n):

        # Increment prefix_a[a[i]] by 1
        prefix_a[a[i]] += 1

    # Traverse the array b[]
    for i in range(m):

        # Increment prefix_b[b[i]] by 1
        prefix_b[b[i]] += 1

    # Calculate prefix sum
    # of the array a[]
    for i in range(1, 10):
        prefix_a[i] += prefix_a[i - 1]

    # Calculate prefix sum
    # of the array b[]
    for i in range(1, 10):
        prefix_b[i] += prefix_b[i - 1]

    # Iterate over the range [0, 9]
    for i in range(1, 10):

        # Make every element in array
        # a[] strictly greater than digit
        # i and make every element in the
        # array b[] less than digit i
        ans = min(ans, prefix_a[i] + m- prefix_b[i])

        # Make every element in array
        # b[] strictly greater than digit
        # i and make every element in
        # array a[] less than digit i
        ans = min(ans, n - prefix_a[i] + prefix_b[i])

    # Print the answer
    print(ans)

# Driver Code
A = [ 0, 0, 1, 3, 3 ]
B = [ 2, 0, 3 ]
N = len(A)
M = len(B)
MinTime(A, B, N, M)

# This code is contributed by rohitsingh07052.**
```

## ****C#****

```
**// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG{

 // Function to find the minimize
// replacements to make every element
// in the array A[] strictly greater
// than every element in B[] or vice-versa
static void MinTime(int []a, int []b, int n, int m)
{

    // Store the final result
    int ans = 2147483647;

    // Create two arrays and
    // initialize with 0s
    int []prefix_a = new int[10];
    int []prefix_b = new int[10];
    Array.Clear(prefix_a,0,prefix_a.Length);
    Array.Clear(prefix_b,0,prefix_b.Length);

    // Traverse the array a[]
    for (int i = 0; i < n; i++) {

        // Increment prefix_a[a[i]] by 1
        prefix_a[a[i]]++;
    }

    // Traverse the array b[]
    for (int i = 0; i < m; i++) {

        // Increment prefix_b[b[i]] by 1
        prefix_b[b[i]]++;
    }

    // Calculate prefix sum
    // of the array a[]
    for (int i = 1; i <= 9; i++) {
        prefix_a[i] += prefix_a[i - 1];
    }

    // Calculate prefix sum
    // of the array b[]
    for (int i = 1; i <= 9; i++) {
        prefix_b[i] += prefix_b[i - 1];
    }

    // Iterate over the range [0, 9]
    for (int i = 0; i <= 9; i++) {

        // Make every element in array
        // a[] strictly greater than digit
        // i and make every element in the
        // array b[] less than digit i
        ans = Math.Min(ans, prefix_a[i] + m
                           - prefix_b[i]);

        // Make every element in array
        // b[] strictly greater than digit
        // i and make every element in
        // array a[] less than digit i
        ans = Math.Min(ans, n - prefix_a[i]
                           + prefix_b[i]);
    }

    // Print the answer
    Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{
    int []A = { 0, 0, 1, 3, 3 };
    int []B = { 2, 0, 3 };
    int N = A.Length;
    int M = B.Length;

    MinTime(A, B, N, M);
}
}

// This code is contributed by bgangwar59.**
```

## ****java 描述语言****

```
**<script>

// Javascript program for the above approach

// Function to find the minimize
// replacements to make every element
// in the array A[] strictly greater
// than every element in B[] or vice-versa
function Mletime(a, b, n, m)
{

    // Store the final result
    let ans = 2147483647;

    // Create two arrays and
    // initialize with 0s
    let prefix_a = [];
    for (let i = 0; i < 10; i++) {
        prefix_a[i] = 0;
    }

    let prefix_b = [];
    for (let i = 0; i < 10; i++) {
        prefix_b[i] = 0;
    }

    // Traverse the array a[]
    for (let i = 0; i < n; i++) {

        // Increment prefix_a[a[i]] by 1
        prefix_a[a[i]]++;
    }

    // Traverse the array b[]
    for (let i = 0; i < m; i++) {

        // Increment prefix_b[b[i]] by 1
        prefix_b[b[i]]++;
    }

    // Calculate prefix sum
    // of the array a[]
    for (let i = 1; i <= 9; i++) {
        prefix_a[i] += prefix_a[i - 1];
    }

    // Calculate prefix sum
    // of the array b[]
    for (let i = 1; i <= 9; i++) {
        prefix_b[i] += prefix_b[i - 1];
    }

    // Iterate over the range [0, 9]
    for (let i = 0; i <= 9; i++) {

        // Make every element in array
        // a[] strictly greater than digit
        // i and make every element in the
        // array b[] less than digit i
        ans = Math.min(ans, prefix_a[i] + m
                           - prefix_b[i]);

        // Make every element in array
        // b[] strictly greater than digit
        // i and make every element in
        // array a[] less than digit i
        ans = Math.min(ans, n - prefix_a[i]
                           + prefix_b[i]);
    }

    // Print the answer
    document.write(ans);
}

// Driver Code

    let A = [ 0, 0, 1, 3, 3 ];
    let B = [ 2, 0, 3 ];
    let N = A.length;
    let M = B.length;

    Mletime(A, B, N, M);

</script>**
```

******Output:** 

```
3
```**** 

*******时间复杂度:** O(N + M)*
***辅助空间:** O(1)*****