# 最小化数组中的插入，以获得直到

的所有和

> 原文:[https://www . geeksforgeeks . org/极小化-数组中的插入-获取所有总和-up-n/](https://www.geeksforgeeks.org/minimize-insertions-in-an-array-to-obtain-all-sums-upto-n/)

给定大小为 **K** 的正整数的排序数组 **arr[]** ，以及整数 **N** ，其中一些数字可以被插入到数组中，使得所有正整数**【1，N】**可以作为修改后的数组的子集的和来获得。任务是找到所需的最小插入次数。
**注意:**数组的最小长度可以是 1。
**举例:**

> **输入:** K = 2，arr = [1，2]，N = 4
> **输出:** 1
> **解释**我们需要在数组中插入 3 或者 4。
> **输入:** K = 4，arr = [1，2，4，8]，N = 15
> **输出:** 0

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。

1.  通过包含给定数组 arr[]中的一些元素和/或添加所需的其他缺失元素，形成一个总计为 N 的必要元素列表，如 **X[]** 。
2.  最初，从空列表 X[]开始，使用来自 X[]的数字的可能和的范围是[0，0]。
3.  假设范围**【1，m】**(m<N)中的元素可以表示为列表 **X[]** 中当时存在的元素的和，并且直到 arr[]的索引 I 的数字已经被添加。
    以下是以下可能性:

> *   If **(I+1)** of arr[] is = **(m+1)** , the possible additional sums are:
>     (m+1), (m+2), (m+3) ...
>     Therefore, the range becomes [1, ((2 * m)+1)]. Add the number arr[i+1] to X[]. Increase I.
> *   The value of if **(I+1) <sup>No.</sup>** of arr [] is < **(m+1)** , it is **k** , and the possible additional sum is
>     (1+k)
>     Therefore, the range becomes [1, (m+k)]. Add the number arr[i+1] to x [] to increase i. 。
> *   The value of if the number of **(I+1)** of arr [] is > **(m+1)** , then **(m+1)** **should be inserted into the array x []** , otherwise. Don't increase I.
> 
> 的值

2.  重复这个过程，直到范围越过给定的数字 n
3.  即使这样做了，如果数组 arr[]中的所有数字都被遍历，并且范围还没有越过 N，那么就需要继续向 X[]添加越来越多的数字，直到范围越过 N。
4.  **X[]** 和 **arr[]** 的尺寸之间的*差异是需要进行的**最小插入次数**。*
5.  在将所有基本元素包含在 **X[]** 中后，范围至少应为**【1，N】**，从给定列表之外插入的数量最少。

**注意:**可以将计数器变量**和**初始化为 0，而不是维护列表 X[]，并且每次添加新元素时，计数器值都可以增加。计数器变量的值是必需的答案。
以下是上述方法的实施:

## C++

```
// C++ code to minimize insertions
// such that sum of subsets of
// array elements form all numbers
// up to N
#include <bits/stdc++.h>
using namespace std;

#define N 100005

int minInsertions(vector<int>& v, int n)
{

    // initialised rangeEnd which
    // denotes the range covered,
    // [1, rangeEnd] ans denotes
    // the number of insertions made
    // so far
    int rangeEnd = 0, ans = 0;
    for (auto i : v) {

        // in the case where our next
        // number is greater than
        // rangeEnd+1, it is compulsory
        // to insert rangeEnd+1
        while (i > rangeEnd + 1) {

            ans++;
            rangeEnd = rangeEnd * 2 + 1;
            if (rangeEnd >= n) {
                return ans;
            }
        }

        // otherwise we just move
        // forward our rangeEnd
        rangeEnd += i;
        if (rangeEnd >= n) {
            return ans;
        }
    }

    // after we have included all
    // elements in the array and have
    // still not reached n, we insert
    // numbers = rangeEnd+1 till
    // we reach n
    while (rangeEnd < n) {
        ans++;
        rangeEnd = rangeEnd * 2 + 1;
    }
    return ans;
}

// Driver Program
signed main()
{
    // the size of the given array
    int k = 4;

    // the given number n
    int n = 15;
    std::vector<int> v = { 1, 6, 7, 9 };
    cout << minInsertions(v, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to minimize insertions
// such that sum of subsets of
// array elements form all numbers
// up to N
class GFG
{
      int N = 100005;

    static int minInsertions(int []v, int n)
    {

        // initialised rangeEnd which
        // denotes the range covered,
        // [1, rangeEnd] ans denotes
        // the number of insertions made
        // so far
        int rangeEnd = 0, ans = 0;
        for (int i : v)
        {

            // in the case where our next
            // number is greater than
            // rangeEnd+1, it is compulsory
            // to insert rangeEnd+1
            while (i > rangeEnd + 1)
            {
                ans++;
                rangeEnd = rangeEnd * 2 + 1;
                if (rangeEnd >= n)
                {
                    return ans;
                }
            }

            // otherwise we just move
            // forward our rangeEnd
            rangeEnd += i;
            if (rangeEnd >= n)
            {
                return ans;
            }
        }

        // after we have included all
        // elements in the array and have
        // still not reached n, we insert
        // numbers = rangeEnd+1 till
        // we reach n
        while (rangeEnd < n)
        {
            ans++;
            rangeEnd = rangeEnd * 2 + 1;
        }
        return ans;
    }

    // Driver Program
    public static void main (String[] args)
    {
        // the size of the given array
        int k = 4;

        // the given number n
        int n = 15;
        int v[] = { 1, 6, 7, 9 };
        System.out.println(minInsertions(v, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to minimize insertions
# such that sum of subsets of
# array elements form all numbers
# up to N
N = 100005

def minInsertions(v, n):

    # Initialised rangeEnd which
    # denotes the range covered,
    # [1, rangeEnd] ans denotes
    # the number of insertions made
    # so far
    rangeEnd, ans = 0, 0
    for i in v:

        # In the case where our next
        # number is greater than
        # rangeEnd+1, it is compulsory
        # to insert rangeEnd+1
        while (i > rangeEnd + 1):
            ans += 1
            rangeEnd = rangeEnd * 2 + 1
            if (rangeEnd >= n):
                return ans

        # Otherwise we just move
        # forward our rangeEnd
        rangeEnd += i
        if (rangeEnd >= n):
            return ans

    # After we have included all
    # elements in the array and have
    # still not reached n, we insert
    # numbers = rangeEnd+1 till
    # we reach n
    while (rangeEnd < n):
        ans += 1
        rangeEnd = rangeEnd * 2 + 1
    return ans

# Driver code
if __name__ == "__main__":

    # The size of the given array
    k = 4

    # The given number n
    n = 15
    v = [ 1, 6, 7, 9 ]

    print(minInsertions(v, n))

# This code is contributed by chitranayal
```

## C#

```
// C# program to minimize insertions
// such that sum of subsets of
// array elements form all numbers
// up to N
using System;

class GFG{

//int N = 100005;

static int minInsertions(int []v, int n)
{

    // Initialised rangeEnd which
    // denotes the range covered,
    // [1, rangeEnd] ans denotes
    // the number of insertions made
    // so far
    int rangeEnd = 0, ans = 0;

    foreach(int i in v)
    {

        // In the case where our next
        // number is greater than
        // rangeEnd+1, it is compulsory
        // to insert rangeEnd+1
        while (i > rangeEnd + 1)
        {
            ans++;
            rangeEnd = rangeEnd * 2 + 1;
            if (rangeEnd >= n)
            {
                return ans;
            }
        }

        // Otherwise we just move
        // forward our rangeEnd
        rangeEnd += i;
        if (rangeEnd >= n)
        {
            return ans;
        }
    }

    // After we have included all
    // elements in the array and have
    // still not reached n, we insert
    // numbers = rangeEnd+1 till
    // we reach n
    while (rangeEnd < n)
    {
        ans++;
        rangeEnd = rangeEnd * 2 + 1;
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    // The size of the given array
    //int k = 4;

    // The given number n
    int n = 15;
    int []v = { 1, 6, 7, 9 };

    Console.WriteLine(minInsertions(v, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript code to minimize insertions
// such that sum of subsets of
// array elements form all numbers
// up to N

      let N = 100005;

     function minInsertions(v, n)
    {

        // initialised rangeEnd which
        // denotes the range covered,
        // [1, rangeEnd] ans denotes
        // the number of insertions made
        // so far
        let rangeEnd = 0, ans = 0;
        for (let i in v)
        {

            // in the case where our next
            // number is greater than
            // rangeEnd+1, it is compulsory
            // to insert rangeEnd+1
            while (i > rangeEnd + 1)
            {
                ans++;
                rangeEnd = rangeEnd * 2 + 1;
                if (rangeEnd >= n)
                {
                    return ans;
                }
            }

            // otherwise we just move
            // forward our rangeEnd
            rangeEnd += i;
            if (rangeEnd >= n)
            {
                return ans;
            }
        }

        // after we have included all
        // elements in the array and have
        // still not reached n, we insert
        // numbers = rangeEnd+1 till
        // we reach n
        while (rangeEnd < n)
        {
            ans++;
            rangeEnd = rangeEnd * 2 + 1;
        }
        return ans;
    }

// Driver Code

        // the size of the given array
        let k = 4;

        // the given number n
        let n = 15;
        let v = [ 1, 6, 7, 9 ];
        document.write(minInsertions(v, n));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(K + log(N))*