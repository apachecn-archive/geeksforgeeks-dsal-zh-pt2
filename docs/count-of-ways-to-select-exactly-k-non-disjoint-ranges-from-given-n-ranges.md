# 从给定的 N 个范围中精确选择 K 个不相交范围的方法数

> 原文:[https://www . geeksforgeeks . org/从给定的 n 个范围中选择精确 k 个非不相交范围的方法数/](https://www.geeksforgeeks.org/count-of-ways-to-select-exactly-k-non-disjoint-ranges-from-given-n-ranges/)

给定两个大小为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **L[]** 和 **R[]** 以及一个整数 **K、**，任务是找出选择精确的 **K** 不相交范围的方法数，这些不相交范围是通过从数组 **L[]** 和 **R[]中获取相同索引处的元素而形成的。**

***例*** :

> **输入:** N = 7，K = 3，L[] = {1，3，4，6，1，5，8}，R[] = {7，8，5，7，3，10，9}
> **输出:** 9
> **解释:**
> 选择 K 范围的可能方式有:
> 
> 1.  选择范围{1，7}、{3，8}和{4，5}
> 2.  选择范围{1，7}、{3，8}和{6，7}
> 3.  选择范围{1，7}、{3，8}和{1，3}
> 4.  选择范围{1，7}、{3，8}和{5，10}
> 5.  选择范围{1，7}、{4，5}和{5，10}
> 6.  选择范围{1，7}、{6，7}和{5，10}
> 7.  选择范围{3，8}、{4，5}和{5，10}
> 8.  选择范围{3，8}、{6，7}和{5，10}
> 9.  选择范围{3，8}、{5，10}和{8，9}
> 
> **输入:** N = 2，K = 2，L[] = {100，200}，R[] ={ 201，300 }
> T3】输出: 0

**天真方法:**解决问题最简单的方法是选择每一个可能的不同的 **K** 对，并检查它们对于所有范围的每一对是否不相交。

***时间复杂度:** O(N！)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过为每个范围检查可用于当前范围的**非不相交**范围的数量来优化。按照以下步骤优化上述方法:

*   初始化一个变量，比如 **cnt** 来计算每个当前范围的非分离范围的数量。
*   初始化一对的[向量，说**预处理**将所有的左边界存储为一个范围的 **{L[i]，1}** ，右边界存储为 **{R[i]+1，-1}** 。](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)
*   使用变量 **i** 迭代范围**【0，N】**，并执行以下步骤:
    *   将对 **{L[i]，1}** 和 **{R[i]+1，-1}** 推入向量**预处理**。
*   [按非递减顺序对向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)、**预处理**进行排序。
*   初始化变量，说 **ans** 和 **cnt** 为 **0** 存储答案并存储与当前范围相交的线段。
*   [使用变量 **i** 迭代向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **预处理**，并执行以下操作:
    *   如果[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的第二个**元素是 **1** 和 **cnt > = K-1，**则通过**<sup>CNT</sup>C<sub>K-1</sub>**增加 **ans** ，并将 **cnt** 更新为 **cnt+1。****
    *   否则，将 **cnt** 更新为 **cnt+1。**
*   最后，完成以上步骤后，打印 **ans** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to calculate nCr
int nCr(int n, int r, int* f)
{
    return f[n] / f[r] * f[n - r];
}

// Function to calculate number of ways
// to choose K ranges such that no two of
// them are disjoint.
int NumberOfWaysToChooseKRanges(int L[], int R[],
                                int N, int K)
{
    // Stores the factorials
    int f[N + 1];
    f[0] = 1;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {
        f[i] = f[i - 1] * i;
    }

    // Preprocessing the ranges into
    // new vector
    vector<pair<int, int> > preprocessed;

    // Traverse the given ranges
    for (int i = 0; i < N; i++) {
        preprocessed.push_back(make_pair(L[i], 1));
        preprocessed.push_back(make_pair(R[i] + 1, -1));
    }

    // Sorting the preprocessed vector
    sort(preprocessed.begin(), preprocessed.end());

    // Stores the result
    int ans = 0;

    // Stores the count of non-disjoint ranges
    int Cnt = 0;

    // Traverse the proeprocesse vector of pairs
    for (int i = 0; i < preprocessed.size(); i++) {

        // If current point is a left boundary
        if (preprocessed[i].second == 1) {
            if (Cnt >= K - 1) {
                // Update the answer
                ans += nCr(Cnt, K - 1, f);
            }

            // Increment cnt by 1
            Cnt++;
        }
        else {
            // Decrement cnt by 1
            Cnt--;
        }
    }

    // Return the ans
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    int N = 7, K = 3;
    int L[] = { 1, 3, 4, 6, 1, 5, 8 };
    int R[] = { 7, 8, 5, 7, 3, 10, 9 };

    // Function Call
    cout << NumberOfWaysToChooseKRanges(L, R, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

static class pair
{
    int first, second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }  
}

// Utility function to calculate nCr
static int nCr(int n, int r, int f[])
{
    return f[n] / f[r] * f[n - r];
}

// Function to calculate number of ways
// to choose K ranges such that no two of
// them are disjoint.
static int NumberOfWaysToChooseKRanges(int L[], int R[],
                                int N, int K)
{
    // Stores the factorials
    int f[] = new int[N + 1];
    f[0] = 1;

    // Iterate over the range [1, N]
    for (int i = 1; i <= N; i++) {
        f[i] = f[i - 1] * i;
    }

    // Preprocessing the ranges into
    // new vector
    Vector<pair > preprocessed = new Vector<pair >();

    // Traverse the given ranges
    for (int i = 0; i < N; i++) {
        preprocessed.add(new pair(L[i], 1));
        preprocessed.add(new pair(R[i] + 1, -1));
    }

    // Sorting the preprocessed vector
    Collections.sort(preprocessed, new Comparator<pair>() {
            @Override public int compare(pair p1, pair p2)
            {
                  if (p1.first != p2.first)
                    return (p1.first - p2.first);
                  return p1.second - p2.second;
            }
        });

    // Stores the result
    int ans = 0;

    // Stores the count of non-disjoint ranges
    int Cnt = 0;

    // Traverse the proeprocesse vector of pairs
    for (int i = 0; i < preprocessed.size(); i++) {

        // If current point is a left boundary
        if (preprocessed.elementAt(i).second == 1) {
            if (Cnt >= K - 1) {
                // Update the answer
                ans += nCr(Cnt, K - 1, f);
            }

            // Increment cnt by 1
            Cnt++;
        }
        else {
            // Decrement cnt by 1
            Cnt--;
        }
    }

    // Return the ans
    return ans;
}

// Driver Code
public static void main (String[] args) {
    // Given Input
    int N = 7, K = 3;
    int L[] = { 1, 3, 4, 6, 1, 5, 8 };
    int R[] = { 7, 8, 5, 7, 3, 10, 9 };

    // Function Call
    System.out.println(NumberOfWaysToChooseKRanges(L, R, N, K));
}
}

// This code is contributed by Dharanendra L V.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Utility function to calculate nCr
def nCr(n, r, f):

    return f[n] // f[r] * f[n - r]

# Function to calculate number of ways
# to choose K ranges such that no two of
# them are disjoint.
def NumberOfWaysToChooseKRanges(L, R, N, K):

    # Stores the factorials
    f = [0 for i in range(N + 1)]
    f[0] = 1

    # Iterate over the range [1, N]
    for i in range(1, N + 1, 1):
        f[i] = f[i - 1] * i

    # Preprocessing the ranges into
    # new vector
    preprocessed = []

    # Traverse the given ranges
    for i in range(N):
        preprocessed.append([L[i], 1])
        preprocessed.append([R[i] + 1, -1])

    # Sorting the preprocessed vector
    preprocessed.sort()

    # Stores the result
    ans = 0

    # Stores the count of non-disjoint ranges
    Cnt = 0

    # Traverse the proeprocesse vector of pairs
    for i in range(len(preprocessed)):

        # If current point is a left boundary
        if (preprocessed[i][1] == 1):
            if (Cnt >= K - 1):

                # Update the answer
                ans += nCr(Cnt, K - 1, f)

            # Increment cnt by 1
            Cnt += 1
        else:

            # Decrement cnt by 1
            Cnt -= 1

    # Return the ans
    return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 7
    K = 3
    L = [ 1, 3, 4, 6, 1, 5, 8 ]
    R = [ 7, 8, 5, 7, 3, 10, 9 ]

    # Function Call
    print(NumberOfWaysToChooseKRanges(L, R, N, K))

# This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Utility function to calculate nCr
function nCr(n, r, f) {
    return f[n] / f[r] * f[n - r];
}

// Function to calculate number of ways
// to choose K ranges such that no two of
// them are disjoint.
function NumberOfWaysToChooseKRanges(L, R, N, K) {
    // Stores the factorials
    let f = new Array(N + 1);
    f[0] = 1;

    // Iterate over the range [1, N]
    for (let i = 1; i <= N; i++) {
        f[i] = f[i - 1] * i;
    }

    // Preprocessing the ranges into
    // new vector
    let preprocessed = [];

    // Traverse the given ranges
    for (let i = 0; i < N; i++) {
        preprocessed.push([L[i], 1]);
        preprocessed.push([R[i] + 1, -1]);
    }

    // Sorting the preprocessed vector
    preprocessed.sort((a, b) => {
        if (a[0] != b[0])
            return a[0] - b[0]
        return a[1] - b[1]
    });

    // Stores the result
    let ans = 0;

    // Stores the count of non-disjoint ranges
    let Cnt = 0;

    // Traverse the proeprocesse vector of pairs
    for (let i = 0; i < preprocessed.length; i++) {

        // If current point is a left boundary
        if (preprocessed[i][1] == 1) {
            console.log("Hello babe")

            if (Cnt >= K - 1) {
                // Update the answer
                ans += nCr(Cnt, K - 1, f);
            }

            // Increment cnt by 1
            Cnt++;
        }
        else {
            // Decrement cnt by 1
            Cnt--;
        }
    }

    // Return the ans
    return ans;
}

// Driver Code

// Given Input
let N = 7, K = 3;
let L = [1, 3, 4, 6, 1, 5, 8];
let R = [7, 8, 5, 7, 3, 10, 9];

// Function Call
document.write(NumberOfWaysToChooseKRanges(L, R, N, K));

</script>
```

**Output**

```
9
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*