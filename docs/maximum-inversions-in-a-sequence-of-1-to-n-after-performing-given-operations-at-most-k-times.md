# 在最多 K 次执行给定操作后 1 到 N 的序列中的最大反转

> 原文:[https://www . geesforgeks . org/最多执行 k 次给定操作后的 1 到 n 序列中的最大反转数/](https://www.geeksforgeeks.org/maximum-inversions-in-a-sequence-of-1-to-n-after-performing-given-operations-at-most-k-times/)

给定两个整数 **N** 和 **K** ，任务是在执行最大 **K** 运算后，找到第一个 **N** 自然数序列中的最大反转数。在每个操作中，序列的任何两个元素都可以交换。注意:序列的元素按升序排列，序列中没有重复的元素。
**例:**

> **输入:** N = 5，K = 3
> **输出:** 10
> **解释:**
> 最初我们有序列为{1，2，3，4，5}。
> 在第一个操作中，我们可以交换 1 和 5，这样序列就变成了{5，2，3，4，1}。
> 在第二个操作中，我们可以交换 2 和 4，这样序列就变成了{5，4，3，2，1}。
> 我们不需要更多的操作。因此，上述序列中的反转数为 10
> **输入:** N = 4，K = 1
> **输出:** 5
> **解释:**
> 最初我们有序列为{ 1，2，3，4}。
> 在第一个操作中我们可以交换 1 和 4，这样序列就变成了{4，2，3，1 }。
> 由于我们只能进行 1 次操作，所以这是我们最后的顺序。因此，上述序列中的反转数是 5。

**进场:**

1.  由于按升序排列的元素是完美的，即它有 **0** 反转，而按降序排列的元素是最不完美的，即它有最大反转。
2.  因此，我们的想法是让序列在每次交换操作中更接近降序，以便获得最大反转。因此，在第一个操作中，我们需要交换最大和最小的元素。同样的，在**第 I 个**操作中，我们需要用序列中的**第 I 个最小的**元素替换**第 I 个最大的**元素。
3.  将升序转换为降序所需的交换次数为 **N/2** 。因此，执行的操作数量应小于或等于 **N/2** 。
    所以更新 K 为:

> **K = min ( K，N / 2 )**

1.  我们需要维护两个变量**‘左’**和**‘右’**来分别表示序列的第 I 个最小元素和第 I 个最大元素。
2.  将**【左】**初始化为**1****【右】**初始化为 **N** 。
3.  我们需要执行以下操作直到 **K** 变为 0:
    *   开启，反转序号中**【左】****【右】**的交换增加

> **2 *(左-右)–1**

*   所以，把这个值加到答案上。
    *   这是因为当我们交换“左”和“右”时，所有形式对(右，I)都有助于反转，所有形式对(I，左)也有助于反转，其中 left < i < right。
    *   表格的总对数**(右，i)** = >右–左，其中左< = i <右
    *   表格的总对数 **(i，左)** = >右–左，其中左<I<=右
    *   此类对的总数为 **2 *(右-左)**
    *   我们从中减去 1，因为在上面的计算中对**(右，左)**进行了两次计数。
*   将**K****的值减少 **1** ，将**的值增加 1。****

1.  ****打印答案的值****

****以下是上述方法的实现:**** 

## ****C++****

```
**// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function which computes the
// maximum number of inversions
int maximum_inversion(int n, int k)
{
    // 'answer' will store the required
    // number of inversions
    int answer = 0;

    // We do this because we will
    // never require more than
    // floor(n/2) operations
    k = min(k, n / 2);

    // left pointer in the array
    int left = 1;
    // right pointer in the array
    int right = n;

    // Doing k operations
    while (k--) {
        // Incrementing ans by number
        // of inversions increase due
        // to this swapping
        answer += 2 * (right - left) - 1;
        left++;
        right--;
    }
    cout << answer << endl;
}

// Driver code
int main()
{
    // Input 1
    int N = 5;
    int K = 3;
    maximum_inversion(N, K);

    // Input 2
    N = 4;
    K = 1;
    maximum_inversion(N, K);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach
import java.util.*;

class GFG{

// Function which computes the
// maximum number of inversions
static void maximum_inversion(int n, int k)
{

    // 'answer' will store the required
    // number of inversions
    int answer = 0;

    // We do this because we will
    // never require more than
    // floor(n/2) operations
    k = Math.min(k, n / 2);

    // left pointer in the array
    int left = 1;

    // right pointer in the array
    int right = n;

    // Doing k operations
    while (k != 0)
    {
        k--;

        // Incrementing ans by number
        // of inversions increase due
        // to this swapping
        answer += 2 * (right - left) - 1;
        left++;
        right--;
    }
    System.out.println(answer);
}

// Driver Code
public static void main(String s[])
{

    // Input 1
    int N = 5;
    int K = 3;
    maximum_inversion(N, K);

    // Input 2
    N = 4;
    K = 1;
    maximum_inversion(N, K);
}
}

// This code is contributed by rutvik_56**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Function which computes the
# maximum number of inversions
def maximum_inversion(n, k):

    # 'answer' will store the required
    # number of inversions
    answer = 0;

    # We do this because we will
    # never require more than
    # floor(n/2) operations
    k = min(k, n // 2);

    # left pointer in the array
    left = 1;

    # right pointer in the array
    right = n;

    # Doing k operations
    while (k > 0):
        k -= 1;

        # Incrementing ans by number
        # of inversions increase due
        # to this swapping
        answer += 2 * (right - left) - 1;
        left += 1;
        right -= 1;

    print(answer);

# Driver Code
if __name__ == '__main__':

    # Input 1
    N = 5;
    K = 3;
    maximum_inversion(N, K);

    # Input 2
    N = 4;
    K = 1;
    maximum_inversion(N, K);

# This code is contributed by amal kumar choubey**
```

## ****C#****

```
**// C# program for the above approach
using System;

class GFG{

// Function which computes the
// maximum number of inversions
static void maximum_inversion(int n, int k)
{

    // 'answer' will store the required
    // number of inversions
    int answer = 0;

    // We do this because we will
    // never require more than
    // floor(n/2) operations
    k = Math.Min(k, n / 2);

    // left pointer in the array
    int left = 1;

    // right pointer in the array
    int right = n;

    // Doing k operations
    while (k != 0)
    {
        k--;

        // Incrementing ans by number
        // of inversions increase due
        // to this swapping
        answer += 2 * (right - left) - 1;
        left++;
        right--;
    }
    Console.WriteLine(answer);
}

// Driver Code
public static void Main(String []s)
{

    // Input 1
    int N = 5;
    int K = 3;
    maximum_inversion(N, K);

    // Input 2
    N = 4;
    K = 1;
    maximum_inversion(N, K);
}
}

// This code is contributed by Rohit_ranjan**
```

## ****java 描述语言****

```
**<script>
// javascript program for the above approach

    // Function which computes the
    // maximum number of inversions
    function maximum_inversion(n, k) {

        // 'answer' will store the required
        // number of inversions
        var answer = 0;

        // We do this because we will
        // never require more than
        // floor(n/2) operations
        k = Math.min(k, parseInt(n / 2));

        // left pointer in the array
        var left = 1;

        // right pointer in the array
        var right = n;

        // Doing k operations
        while (k > 0)
        {
            k--;

            // Incrementing ans by number
            // of inversions increase due
            // to this swapping
            answer += 2 * (right - left) - 1;
            left++;
            right--;
        }
        document.write(answer + "<br/>");
    }

    // Driver Code

        // Input 1
        var N = 5;
        var K = 3;
        maximum_inversion(N, K);

        // Input 2
        N = 4;
        K = 1;
        maximum_inversion(N, K);

// This code is contributed by aashish1995
</script>**
```

******Output:** 

```
10
5
```**** 

******时间复杂度:***O(K)*
T5】辅助空间: *O(1)*****