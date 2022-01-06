# 将每个元素 A[i]替换为(A[i]*D + B[i])

后，给定数组中的 0 最大化

> 原文:[https://www . geeksforgeeks . org/给定数组中最大化-0s-替换每个元素后-ai-aid-bi/](https://www.geeksforgeeks.org/maximize-0s-in-given-array-after-replacing-each-element-ai-with-aid-bi/)

给定由 **N** 个整数组成的两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**，任务是通过选择**D**的任意值，找到数组**A【】**中**0**的最大[个数，该个数可以在将每个数组元素 **A[i]** 替换为 **A[i]*D + B[i]** 后得到](https://www.geeksforgeeks.org/find-number-zeroes/)

**示例:**

> **输入:** A[] = {1，2，-1}，B[] = {-6，-12，6}
> **输出:** 3
> **说明:**
> 把 **D** 的值考虑为 6。现在数组 A[]修改为{ 1 * 6–6，2 * 6–12，-1*6 + 6} = {0，0，0}。
> 因此，D 的值为 6 时，所有数组元素 A[i]都为 0。因此，打印 3。
> 
> **输入:** A[] = {0，7，2}，B[] = {0，5，-4 }
> T3】输出: 2

**方法:**给定的问题可以通过计算制作每个数组元素**A【I】**到 **0** 所需的 **D** 的值并将这些值存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中来解决。按照以下步骤解决问题:

*   初始化一个地图，说 **M** 和两个整数，说 **cnt** 和 **ans** 为 **0** 。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N–1】**，并执行以下步骤:
    *   将两个整数 **num** 初始化为**-B【I】**，将 **den** 初始化为**A【I】**。
    *   如果 **den** 的值不等于 **0** ，则将数值 **num** 和 **den** 除以 **num** 和 **den** 的 [GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) 。
    *   如果 **num** 的值不大于 **0** ，则将 **num** 和 **den** 乘以 **-1** 。
    *   如果 **den** 和 **num** 的值都等于 **0** ，则将 **cnt** 的值增加 **1** ，如果 **den** 的值不等于 **0** ，则将**MP 【{ num，den }】**的值增加 **1** 并更新 **ans** 的值
*   完成上述步骤后，打印 **ans + cnt** 的值作为执行给定操作后给定数组**A【I】**中最大化 **0s** 计数的 **D** 的可能值。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of 0s in the array A[] after changing
// the array element to A[i]*D + B[i]
void maxZeroes(vector<int>& A,
               vector<int>& B)
{
    // Stores the frequency of fractions
    // needed to make each element 0
    map<pair<int, int>, int> mp;
    int N = A.size();

    // Stores the maximum number of 0
    int ans = 0;
    int cnt = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Find the numerator and
        // the denominator
        int num = -B[i];
        int den = A[i];

        int gc = __gcd(num, den);

        // Check if den is not equal
        // to 0
        if (den != 0) {

            // Divide num and den
            // by their gcd
            num /= gc;
            den /= gc;
        }

        // Check if num is not
        // greater than 0
        if (num <= 0) {
            num *= -1;
            den *= -1;
        }

        // Check if both num and den
        // are equal to 0
        if (den == 0 and num == 0)
            cnt++;

        if (den != 0) {

            // Increment the value of
            // {num, den} in the map
            mp[{ num, den }]++;

            // Update the value of ans
            ans = max(mp[{ num, den }], ans);
        }
    }

    // Print the value of ans+cnt
    cout << ans + cnt << endl;
}

// Driver Code
int main()
{
    vector<int> A = { 1, 2, -1 };
    vector<int> B = { -6, -12, 6 };
    maxZeroes(A, B);

    return 0;
}
```

## 蟒蛇 3

```
# Python program for the above approach
from math import gcd

# Function to find the maximum number
# of 0s in the array A[] after changing
# the array element to A[i]*D + B[i]
def maxZeroes(A,B):
    # Stores the frequency of fractions
    # needed to make each element 0
    mp = {}
    N = len(A)

    # Stores the maximum number of 0
    ans = 0
    cnt = 0

    # Traverse the array
    for i in range(N):
        # Find the numerator and
        # the denominator
        num = -B[i]
        den = A[i]

        gc = gcd(num, den)

        # Check if den is not equal
        # to 0
        if (den != 0):

            # Divide num and den
            # by their gcd
            num //= gc
            den //= gc

        # Check if num is not
        # greater than 0
        if (num <= 0):
            num *= -1
            den *= -1

        # Check if both num and den
        # are equal to 0
        if (den == 0 and num == 0):
            cnt+=1

        if (den != 0):

            # Increment the value of
            # {num, den} in the map
            mp[(num, den)] = mp.get((num, den),0)+1

            # Update the value of ans
            ans = max(mp[(num, den )], ans)

    # Prthe value of ans+cnt
    print (ans + cnt)

# Driver Code
if __name__ == '__main__':
    A = [1, 2, -1]
    B = [-6, -12, 6]
    maxZeroes(A, B)

# This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

function __gcd(a, b) {
    if (b == 0)
    return a;
    return __gcd(b, a % b);
 }

// Function to find the maximum number
// of 0s in the array A[] after changing
// the array element to A[i]*D + B[i]
function maxZeroes(A, B) {
    // Stores the frequency of fractions
    // needed to make each element 0
    let mp = new Map();
    let N = A.length;

    // Stores the maximum number of 0
    let ans = 0;
    let cnt = 0;

    // Traverse the array
    for (let i = 0; i < N; i++) {

        // Find the numerator and
        // the denominator
        let num = -B[i];
        let den = A[i];

        let gc = __gcd(num, den);

        // Check if den is not equal
        // to 0
        if (den != 0) {

            // Divide num and den
            // by their gcd
            num /= gc;
            den /= gc;
        }

        // Check if num is not
        // greater than 0
        if (num <= 0) {
            num *= -1;
            den *= -1;
        }

        // Check if both num and den
        // are equal to 0
        if (den == 0 && num == 0)
            cnt++;

        if (den != 0) {

            // Increment the value of
            // {num, den} in the map
            if (mp.has(`${num},${den}`)) {
                mp.set(`${num},${den}`, mp.get(`${num},${den}`) + 1)
            } else {
                mp.set(`${num},${den}`, 1)
            }

            // Update the value of ans
            ans = Math.max(mp.get(`${num},${den}`), ans);
        }
    }

     // Print the value of ans+cnt
    document.write(ans + cnt + "<br>");
}

// Driver Code

let A = [1, 2, -1];
let B = [-6, -12, 6];
maxZeroes(A, B);

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*