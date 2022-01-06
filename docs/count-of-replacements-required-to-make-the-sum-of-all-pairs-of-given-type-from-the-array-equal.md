# 使数组中给定类型的所有对的总和相等所需的替换计数

> 原文:[https://www . geeksforgeeks . org/需要替换次数才能使数组中所有给定类型对的总和相等/](https://www.geeksforgeeks.org/count-of-replacements-required-to-make-the-sum-of-all-pairs-of-given-type-from-the-array-equal/)

给定一个长度为 **N** 的整数数组 **arr** 和一个整数 **K** ，任务是从范围**【1，K】**中找到要被一个值替换的数组元素的数量，使得每对 **(arr[i]、arr[N–1–I]**具有相等的和。

**示例:**

> **输入:** arr[] = {1，2，2，1}，K = 3
> **输出:** 1
> **解释:**
> 用 3 替换 arr[0]，使数组变成{3，2，2，1}。
> 现在可以看到 arr[0] + arr[3] = arr[1] + arr[2] = 4。
> 
> **输入:** arr[] = {1，2，1，2，1，2}
> **输出:** 0
> **解释:**
> 无需做任何更改，因为 arr[0]+arr[5]= arr[1]+arr[4]= arr[2]+arr[3]= 3

**天真方法:**
解决这个问题最简单的方法可能是像迭代 **X** 的所有可能值，该值可以是 **1** 到 **2*K** 范围内的任何数字，并找到实现等于 **X** 的对和所需的运算次数。最后从所有操作中返回最小数量的替换。

***时间复杂度:** O (N * K)*
***辅助空间:** O (1)*

**有效方法:**上述方法可以通过以下观察进行优化:

*   **X** 可以清晰取值在**【2，2 * K】**范围内。
*   考虑对**arr【I】**和**arr【N–I–1】**，可以观察到，在 0、1 或 2 次替换中，任何对的和都可以等于 **X** 。
*   让这两个数字的最大值为 **mx** ，最小值为 **mn** 。在一次替换中，该对的总和将在**【Mn+1，MX+K】**的范围内。
*   **mx** 小于**(X–K)**和 **mn** 大于或等于 **X** 的配对需要更换 2 次。
*   只需在两个不同的向量中为所有对插入 **mx** 和 **mn** ，对它们进行排序并应用二分搜索法查找需要 **2** 替换的对的数量。
*   通过存储每个和的频率，使用[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)找到不需要任何替换的对。
*   最后，需要一次更换的线对数量可以通过公式**(N/2 –(需要 2 次更换的线对+不需要更换的线对))**来计算。

按照以下步骤找到解决问题的方法:

1.  找出所有对 **arr [ i ]** 、**arr[N–I–1]**的最大值和最小值，并将它们分别存储在 **max_values** 和 **min_values** 向量中。还要将所有这些对的频率和存储在一个映射中。
2.  对向量**最大值**和**最小值进行排序。**
3.  从 **X = 2** 迭代到 **X = 2 * K** ，对于 **X** 的每个值，按照上面的方法找到替换的总数。将答案更新为:

> 答案= min(答案，2 *(我们需要进行两次替换的对的数量)+(我们需要进行一次替换的对的数量))。

> **图解:**
> arr[] = { 1，2，2，1}，K = 3
> max_values = {1，2}
> min_values = {1，2}
> map = {{2，1 }，{4，1}}
> 在 X = 4 时，需要最小替换，即只需要 1 次替换，要么将 arr[0]转换为 3，要么将 arr[3]转换为 3，才能使所有对之和等于 4。

下面是上述方法的实现:

## C++

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
#define int long long int
using namespace std;

const int inf = 1e18;

// Function to find the minimum
// replacements required
int minimumReplacement(int* arr, int N,
                    int K)
{
    int ans = inf;

    // Stores the maximum and minimum
    // values for every pair of
    // the form arr[i], arr[n-i-1]
    vector<int> max_values;
    vector<int> min_values;

    // Map for storing frequencies
    // of every sum formed by pairs
    map<int, int> sum_equal_to_x;

    for (int i = 0; i < N / 2; i++) {

        // Minimum element in the pair
        int mn = min(arr[i], arr[N - i - 1]);

        // Maximum element in the pair
        int mx = max(arr[i], arr[N - i - 1]);

        // Incrementing the frequency of
        // sum encountered
        sum_equal_to_x[arr[i]
                    + arr[N - i - 1]]++;

        // Insert minimum and maximum values
        min_values.push_back(mn);
        max_values.push_back(mx);
    }

    // Sorting the vectors
    sort(max_values.begin(),
        max_values.end());

    sort(min_values.begin(),
        min_values.end());

    // Iterate over all possible values of x
    for (int x = 2; x <= 2 * K; x++) {

        // Count of pairs for which x > x + k
        int mp1
            = lower_bound(max_values.begin(),
                        max_values.end(), x - K)
            - max_values.begin();

        // Count of pairs for which x < mn + 1
        int mp2
            = lower_bound(min_values.begin(),
                        min_values.end(), x)
            - min_values.begin();

        // Count of pairs requiring 2 replacements
        int rep2 = mp1 + (N / 2 - mp2);

        // Count of pairs requiring no replacements
        int rep0 = sum_equal_to_x[x];

        // Count of pairs requiring 1 replacement
        int rep1 = (N / 2 - rep2 - rep0);

        // Update the answer
        ans = min(ans, rep2 * 2 + rep1);
    }

    // Return the answer
    return ans;
}

// Driver Code
int32_t main()
{
    int N = 4;
    int K = 3;
    int arr[] = { 1, 2, 2, 1 };

    cout << minimumReplacement(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program implement
// the above approach
import java.util.*;
import java.io.*;

class GFG{

static int inf = (int)1e18;

// Function to find the minimum
// replacements required
static int minimumReplacement(int[] arr, int N,
                                        int K)
{
    int ans = inf;

    // Stores the maximum and minimum
    // values for every pair of
    // the form arr[i], arr[n-i-1]
    ArrayList<Integer> max_values = new ArrayList<>();
    ArrayList<Integer> min_values = new ArrayList<>();

    // Map for storing frequencies
    // of every sum formed by pairs
    Map<Integer,
        Integer> sum_equal_to_x = new HashMap<>();

    for(int i = 0; i < N / 2; i++)
    {

        // Minimum element in the pair
        int mn = Math.min(arr[i], arr[N - i - 1]);

        // Maximum element in the pair
        int mx = Math.max(arr[i], arr[N - i - 1]);

        // Incrementing the frequency of
        // sum encountered
        sum_equal_to_x.put(arr[i] +
                        arr[N - i - 1],
        sum_equal_to_x.getOrDefault(arr[i] +
                                    arr[N - i - 1],
                                    0) + 1);

        // Insert minimum and maximum values
        min_values.add(mn);
        max_values.add(mx);
    }

    // Sorting the vectors
    Collections.sort(max_values);

    Collections.sort(min_values);

    // Iterate over all possible values of x
    for(int x = 2; x <= 2 * K; x++)
    {

        // Count of pairs for which x > x + k
        int mp1 = max_values.indexOf(x - K);

        // Count of pairs for which x < mn + 1
        int mp2 = min_values.indexOf(x);

        // Count of pairs requiring 2 replacements
        int rep2 = mp1 + (N / 2 - mp2);

        // Count of pairs requiring no replacements
        int rep0 = sum_equal_to_x.getOrDefault(x, -1);

        // Count of pairs requiring 1 replacement
        int rep1 = (N / 2 - rep2 - rep0);

        // Update the answer
        ans = Math.min(ans, rep2 * 2 + rep1);
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main (String[] args)
{
    int N = 4;
    int K = 3;
    int arr[] = { 1, 2, 2, 1 };

    System.out.print(minimumReplacement(arr, N, K));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement the
# above approach
inf = 10**18

def firstOccurance(numbers, length,
                   searchnum):

    answer = -1 
    start = 0   
    end = length - 1

    while start <= end:
        middle = (start + end) // 2

        if numbers[middle] == searchnum:
            answer = middle
            end = middle - 1
        elif numbers[middle] > searchnum:
            end = middle - 1   
        else:
            start = middle + 1

    return answer

# Function to find the minimum
# replacements required
def minimumReplacement(arr, N,  K):

    ans = inf

    # Stores the maximum and minimum
    # values for every pair of
    # the form arr[i], arr[n-i-1]
    max_values = []
    min_values = []

    # Map for storing frequencies
    # of every sum formed by pairs
    sum_equal_to_x = dict()

    for i in range(N // 2):

        # Minimum element in the pair
        mn = min(arr[i], arr[N - i - 1])

        # Maximum element in the pair
        mx = max(arr[i], arr[N - i - 1])

        # Incrementing the frequency of
        # sum encountered
        if(arr[i] + arr[N - i - 1] not in sum_equal_to_x):
            sum_equal_to_x[arr[i] + arr[N - i - 1]] = 0

        sum_equal_to_x[arr[i] + arr[N - i - 1]] += 1

        # Insert minimum and maximum values
        min_values.append(mn)
        max_values.append(mx)

    max_values.sort()
    min_values.sort()

    # Iterate over all possible values of x
    for x in range(2, 2 * K + 1):

        # Count of pairs for which x > x + k
        mp1 = firstOccurance(
            max_values, len(max_values), x - K)

        # Count of pairs for which x < mn + 1
        mp2 = firstOccurance(
            min_values, len(min_values), x)

        # Count of pairs requiring 2 replacements
        rep2 = mp1 + (N // 2 - mp2)

        # Count of pairs requiring no replacements
        if x in sum_equal_to_x:
            rep0 = sum_equal_to_x[x]
        else:
            rep0 = 0

        # Count of pairs requiring 1 replacement
        rep1 = (N // 2 - rep2 - rep0)

        # Update the answer
        ans = min(ans, rep2 * 2 + rep1)

    # Return the answer
    return ans

# Driver Code
if __name__=='__main__':

    N = 4
    K = 3
    arr = [ 1, 2, 2, 1 ]

    print(minimumReplacement(arr, N, K))

# This code is contributed by pratham76
```

## C#

```
// C# program implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to find the minimum
// replacements required
static int minimumReplacement(int[] arr, int N,
                                         int K)
{
    int ans = int.MaxValue;

    // Stores the maximum and minimum
    // values for every pair of
    // the form arr[i], arr[n-i-1]
    ArrayList max_values = new ArrayList();
    ArrayList min_values = new ArrayList();

    // Map for storing frequencies
    // of every sum formed by pairs
    Dictionary<int,
               int> sum_equal_to_x = new Dictionary<int,
                                                    int>();

    for(int i = 0; i < N / 2; i++)
    {

        // Minimum element in the pair
        int mn = Math.Min(arr[i], arr[N - i - 1]);

        // Maximum element in the pair
        int mx = Math.Max(arr[i], arr[N - i - 1]);

        // Incrementing the frequency of
        // sum encountered
        sum_equal_to_x[arr[i] + arr[N - i - 1]] =
        sum_equal_to_x.GetValueOrDefault(arr[i] +
                             arr[N - i - 1], 0) + 1;

        // Insert minimum and maximum values
        min_values.Add(mn);
        max_values.Add(mx);
    }

    // Sorting the vectors
    max_values.Sort();

    min_values.Sort();

    // Iterate over all possible values of x
    for(int x = 2; x <= 2 * K; x++)
    {

        // Count of pairs for which x > x + k
        int mp1 = max_values.IndexOf(x - K);

        // Count of pairs for which x < mn + 1
        int mp2 = min_values.IndexOf(x);

        // Count of pairs requiring 2 replacements
        int rep2 = mp1 + (N / 2 - mp2);

        // Count of pairs requiring no replacements
        int rep0 = sum_equal_to_x.GetValueOrDefault(
                   x, -1);

        // Count of pairs requiring 1 replacement
        int rep1 = (N / 2 - rep2 - rep0);

        // Update the answer
        ans = Math.Min(ans, rep2 * 2 + rep1);
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main(string[] args)
{
    int N = 4;
    int K = 3;
    int []arr = { 1, 2, 2, 1 };

    Console.Write(minimumReplacement(arr, N, K));
}
}

// This code is contributed by rutvik_56
```

**Output**

```
1
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*