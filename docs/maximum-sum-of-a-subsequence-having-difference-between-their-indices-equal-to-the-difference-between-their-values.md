# 子序列的最大和，它们的指数之差等于它们的值之差

> 原文:[https://www . geeksforgeeks . org/子序列的最大和-它们的指数之间有差异-等于它们的值之间的差异/](https://www.geeksforgeeks.org/maximum-sum-of-a-subsequence-having-difference-between-their-indices-equal-to-the-difference-between-their-values/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**，任务是找到一个[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大和，使得对于[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中的每一对，它们在原始[数组](https://www.geeksforgeeks.org/array-data-structure/)中的索引之间的差等于它们的值之间的差。**

****示例:****

> ****输入:** A[] = {10，7，1，9，10，15}，N = 6
> **输出:** 26
> **解释:**
> 子序列:{7，9，10}。
> 原始数组中的索引分别为{1，3，4}。
> 所有对的指数和值之间的差值相等。
> 因此，最大可能和= (7 + 9 + 10) = 26。**
> 
> ****输入:** A[] = {100，2}，N = 2
> T3】输出: 100**

****方法:**对于具有指数 **i** 和 **j** 的两个元素，以及数值**A【I】**和**A【j】，**如果**I–j**等于**A【I】–A【j】，**则**A【I】–I**等于**A【j】–j**。因此，有效的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)将具有相同的**A[I]–I**值。按照以下步骤解决问题:**

*   **初始化一个变量，将**和**设为 **0，**以存储可能的所需[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大和。**
*   **初始化一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **mp，**来存储每个**A【I】–I**的值。**
*   **[使用变量在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**中迭代，比如说 **i** :

    *   将 **A[i]** 添加至**MP【A[I]–I】。**
    *   将 **ans** 更新为 **ans** 和**MP【A[I]–I】的最大值。**** 
*   **最后打印 **ans** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum of
// a subsequence having difference between
// indices equal to difference in their values
void maximumSubsequenceSum(int A[], int N)
{
    // Stores the maximum sum
    int ans = 0;

    // Stores the value for each A[i] - i
    map<int, int> mp;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update the value in map
        mp[A[i] - i] += A[i];

        // Update the answer
        ans = max(ans, mp[A[i] - i]);
    }

    // Finally, print the answer
    cout << ans << endl;
}

// Driver Code
int main()
{
    // Given Input
    int A[] = { 10, 7, 1, 9, 10, 1 };
    int N = sizeof(A) / sizeof(A[0]);

    // Function Call
    maximumSubsequenceSum(A, N);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.HashMap;
public class GFG
{

    // Function to find the maximum sum of
    // a subsequence having difference between
    // indices equal to difference in their values
    static void maximumSubsequenceSum(int A[], int N)
    {

        // Stores the maximum sum
        int ans = 0;

        // Stores the value for each A[i] - i
        HashMap<Integer, Integer> mp = new HashMap<>();

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Update the value in map
            mp.put(A[i] - i,
                   mp.getOrDefault(A[i] - i, 0) + A[i]);

            // Update the answer
            ans = Math.max(ans, mp.get(A[i] - i));
        }

        // Finally, print the answer
        System.out.println(ans);
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given Input
        int A[] = { 10, 7, 1, 9, 10, 1 };
        int N = A.length;

        // Function Call
        maximumSubsequenceSum(A, N);
    }
}

// This code is contributed by abhinavjain194
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the maximum sum of
# a subsequence having difference between
# indices equal to difference in their values
def maximumSubsequenceSum(A, N):

    # Stores the maximum sum
    ans = 0

    # Stores the value for each A[i] - i
    mp = {}

    # Traverse the array
    for i in range(N):
        if (A[i] - i in mp):

            # Update the value in map
            mp[A[i] - i] += A[i]
        else:
            mp[A[i] - i] = A[i]

        # Update the answer
        ans = max(ans, mp[A[i] - i])

    # Finally, print the answer
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given Input
    A = [ 10, 7, 1, 9, 10, 1 ]
    N = len(A)

    # Function Call
    maximumSubsequenceSum(A, N)

# This code is contributed by SURENDRA_GANGWAR
```

## **C#**

```
// C# program for the above approach
using System.Collections.Generic;
using System;

class GFG{

// Function to find the maximum sum of
// a subsequence having difference between
// indices equal to difference in their values
static void maximumSubsequenceSum(int []A, int N)
{

    // Stores the maximum sum
    int ans = 0;

    // Stores the value for each A[i] - i
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Update the value in map
        if (mp.ContainsKey(A[i] - i))
            mp[A[i] - i] += A[i];
        else
            mp[A[i] - i] = A[i]; 

        // Update the answer
        ans = Math.Max(ans, mp[A[i] - i]);
    }

    // Finally, print the answer
    Console.Write(ans);
}

// Driver code
public static void Main(String[] args)
{

    // Given Input
    int []A = { 10, 7, 1, 9, 10, 1 };
    int N = A.Length;

    // Function Call
    maximumSubsequenceSum(A, N);
}
}

// This code is contributed by amreshkumar3
```

## **java 描述语言**

```
<script>

// javascript program for the above approach

// Function to find the maximum sum of
// a subsequence having difference between
// indices equal to difference in their values
function maximumSubsequenceSum(A, N)
{
    // Stores the maximum sum
    var ans = 0;

    // Stores the value for each A[i] - i
    var mp = new Map();

    var i;
    // Traverse the array
    for(i = 0; i < N; i++) {

        // Update the value in map
        if(mp.has(A[i] - i))
            mp.set(A[i] - i,mp.get(A[i] - i)+A[i]);

        else
             mp.set(A[i] - i,A[i]);

        // Update the answer
        ans = Math.max(ans, mp.get(A[i] - i));
    }

    // Finally, print the answer
    document.write(ans);
}

    // Driver Code
    // Given Input
    var A = [10, 7, 1, 9, 10, 1];
    var N = A.length;

    // Function Call
    maximumSubsequenceSum(A, N);

</script>
```

****Output:** 

```
26
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**