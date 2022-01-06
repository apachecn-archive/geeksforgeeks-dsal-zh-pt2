# 一个元素乘以另一个元素的不同对的计数

> 原文:[https://www . geeksforgeeks . org/count-of-distinct-pairs-with-one-element-as-k-times-the-other/](https://www.geeksforgeeks.org/count-of-distinct-pairs-having-one-element-as-k-times-the-other/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **K，**求一个元素是另一个元素的 **K** 倍的最大配对数，即 **arr[i]=K*arr[j]** 。

**示例:**

> **输入:** arr[] = {1，2，1，2，4} K = 2
> **输出:** 2
> **解释:**有两种可能的方法来构造对:({1，2}、{1，2})和({1，2}、{2，4})。
> 
> **输入:** a = {5，4，3，2，1} K = 2
> **输出:** 1
> **解释:**我们可以构造集合{1，2}或集合{2，4}。

**方法:** [排序](https://www.geeksforgeeks.org/quick-sort/)给定的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**并检查所有可能的[数组对](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**并检查给定的 **(i，j) arr[i]=2*arr[j]。**按照以下步骤解决问题:

*   [使用 C++ STL](https://www.geeksforgeeks.org/quick-sort/) 中的[排序功能对](https://www.geeksforgeeks.org/sort-c-stl/)[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**进行排序。
*   [初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **使用**来保持已经使用的元素的计数。
*   将变量**和**初始化为 **0** ，以存储所有可能的对的计数。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**，并执行以下步骤:
    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【l，N-1】**，并执行以下操作:
        *   如果**使用的【j】**和**使用的【I】**的值为**假**和**arr【j】= K * arr【I】**，则将**使用的【I】**和**使用的【j】**的值设置为**真**，并将 **ans** 的值增加 **1** 和[断开](https://www.geeksforgeeks.org/break-statement-cc/)
*   最后，完成上述步骤后，打印 **ans 的值。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach.
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of pairs.
int maxPairs(vector<int> a, int k)
{
    // Sort the array.
    sort(a.begin(), a.end());
    int n = a.size(), ans = 0;

    // mark as used
    vector<bool> used(n);

    // iterate over all elements
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // if condition is satisfied,
            // pair the elements
            if (!used[j]
                && a[j] == k * a[i]
                && !used[i]) {
                used[j] = used[i] = true;
                ans++;
                break;
            }
        }
    }

    return ans;
}

// Driver Code
int32_t main()
{
    vector<int> a{ 1, 2, 1, 2, 4 };
    int k = 2;
    cout << maxPairs(a, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach.

import java.util.Arrays;

class GFG {

    // Function to find the maximum number
    // of pairs.
public static int maxPairs(int[] a, int k)
{
    // Sort the array.
    Arrays.sort(a);
    int n = a.length, ans = 0;

    // mark as used
    boolean[] used = new boolean[n];

    // iterate over all elements
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // if condition is satisfied,
            // pair the elements
            if (!used[j]
                && a[j] == k * a[i]
                && !used[i]) {
                used[i] =  true;
                used[j] = used[i];
                ans++;
                break;
            }
        }
    }

    return ans;
}

    // Driver Code
    public static void main(String args[])
    {
        int[] a = {1, 2, 1, 2, 4};
        int k = 2;
        System.out.println(maxPairs(a, k));
    }
}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python Program for the above approach

# Function to find the maximum number
# of pairs.
def maxPairs(a, k):

    # Sort the array.
    a.sort()
    n = len(a)
    ans = 0

    # mark as used
    used = [False] * n

    # iterate over all elements
    for i in range(0, n):
        for j in range(i + 1, n):

            # if condition is satisfied,
            # pair the elements
            if (used[j] == False and a[j] == k * a[i] and used[i] == False):
                used[j] = used[j] = True
                ans += 1
                break

    return ans

# Driver Code
a = [1, 2, 1, 2, 4]
k = 2
print(maxPairs(a, k))

# This code is contributed by _saurabh_jaiswal
```

## C#

```
// C# program for the above approach.
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum number
// of pairs.
static int maxPairs(List<int> a, int k)
{

    // Sort the array.
    a.Sort();
    int n = a.Count, ans = 0;

    // mark as used
    int [] Ar = new int[n];
    List<int> used = new List<int>(Ar);

    // iterate over all elements
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // if condition is satisfied,
            // pair the elements
            if (used[j]==0
                && a[j] == k * a[i]
                && used[i]==0) {
                used[j] = used[i] = 1;
                ans++;
                break;
            }
        }
    }

    return ans;
}

// Driver Code
  public static void Main(){
    List<int> a = new List<int>(){ 1, 2, 1, 2, 4 };
    int k = 2;
    Console.Write(maxPairs(a, k));
  }
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        // Function to find the maximum number
        // of pairs.
        function maxPairs(a, k)
        {

            // Sort the array.
            a.sort(function (x, y) { return x - y });
            let n = a.length, ans = 0;

            // mark as used
            let used = new Array(n).fill(false);

            // iterate over all elements
            for (let i = 0; i < n; i++) {
                for (let j = i + 1; j < n; j++) {

                    // if condition is satisfied,
                    // pair the elements
                    if (used[j] == false && a[j] == k * a[i] && used[i] == false) {
                        used[j] = used[j] = true;
                        ans++;
                        break;
                    }
                }
            }

            return ans;
        }

        // Driver Code
        let a = [1, 2, 1, 2, 4];
        let k = 2;
        document.write(maxPairs(a, k));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
```

***时间复杂度:** O(N^2)*
***空间复杂度:** O(N)*