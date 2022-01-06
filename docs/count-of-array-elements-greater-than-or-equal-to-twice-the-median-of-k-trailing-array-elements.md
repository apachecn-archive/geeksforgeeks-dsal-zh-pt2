# 大于或等于 K 个尾随数组元素中值两倍的数组元素计数

> 原文:[https://www . geesforgeks . org/数组元素计数-大于或等于 k 个尾随数组元素中值的两倍/](https://www.geeksforgeeks.org/count-of-array-elements-greater-than-or-equal-to-twice-the-median-of-k-trailing-array-elements/)

给定一个大小大于整数 K 的数组**A[]**，任务是从数组中找出大于或等于给定数组中的**K 个尾随元素**的中值的两倍的元素总数。

**示例:**

> **输入:** A[] = {10，20，30，40，50}，K = 3
> **输出:** 1
> **说明:**
> 由于 K = 3，所以只需要检查两个元素{40，50}。
> 对于 40，3 个尾随数字{10，20，30}的中位数为 20。
> 因为 40 = 2 * 20，所以算 40。
> 对于元素 50，3 个尾随数字{20，30，40}的中间值为 30。
> 既然 50 < 2 * 30，那么 50 不算。
> 所以，答案是 1。
> 
> **输入:** A[] = {1，2，2，4，5}，K = 3
> **输出:** 2
> **解释:**
> 由于 K = 3，所以只考虑了{4，5}两个元素。
> 对于 4，3 个尾随数字{1，2，2}的中间值为 2。
> 因为 4 = 2 * 2，所以，4 也算。
> 对于 5，3 个尾随数字{2，2，4}的中间值为 2。
> 5 > 2 * 2，所以算 5。
> 所以，答案是 2。

**天真方法:**
按照以下步骤解决问题:

*   迭代给定的数组，从 **K + 1** 到数组的大小，对于每个元素，添加数组中先前的 **K** 元素。
*   然后，找到中间值，并检查当前元素是否等于或超过中间值的两倍。如果发现为真，增加**计数**。
*   终于。打印**计数**。

***时间复杂度:**O(N * K * log K)*
T5**辅助空间:** O(1)

**高效进场:**
对上述进场进行优化，思路是采用 [**计频**](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)[**滑动窗口**](https://www.geeksforgeeks.org/window-sliding-technique/) 手法。按照以下步骤解决问题:

*   存储出现在第一个 **K** 索引中的元素的频率。
*   迭代数组从 **(k + 1) <sup>第</sup>** 个索引到**第<sup>个</sup>** 个索引，对于每次迭代，降低**I–K<sup>第</sup>个元素**的频率，其中 **i** 是前一个 **K** 个尾随元素的当前索引，并增加当前元素的频率计数。
*   对于每次迭代，获取低中值和高中值的值，如果 **K** 为偶数，则低中值和高中值将不同。否则就一样了。
*   初始化一个**计数**变量，该变量将对频率进行计数。每当到达**楼层((k+1)/2)** 时，计数给出**低中值**，同样，当计数达到**天花板((k+1)/2)** 时，计数给出**高中值**。
*   然后**将低、高中值相加**，检查当前值是否大于或等于或，并相应更新答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

const int N = 2e5;
const int V = 500;

// Function to find the count of array
// elements >= twice the median of K
// trailing array elements
void solve(int n, int d, int input[])
{
    int a[N];

    // Stores frequencies
    int cnt[V + 1];

    // Stores the array elements
    for (int i = 0; i < n; ++i)
        a[i] = input[i];

    int answer = 0;

    // Count the frequencies of the
    // array elements
    for (int i = 0; i < d; ++i)
        cnt[a[i]]++;

    // Iterating from d to n-1 index
    // means (d+1)th element to nth element
    for (int i = d; i <= n - 1; ++i) {

        // To check the median
        int acc = 0;

        int low_median = -1, high_median = -1;

        // Iterate over the frequencies
        // of the elements
        for (int v = 0; v <= V; ++v) {

            // Add the frequencies
            acc += cnt[v];

            // Check if the low_median value is
            // obtained or not, if yes then do
            // not change as it will be minimum
            if (low_median == -1
                && acc >= int(floor((d + 1) / 2.0)))
                low_median = v;

            // Check if the high_median value is
            // obtained or not, if yes then do not
            // change it as it will be maximum
            if (high_median == -1
                && acc >= int(ceil((d + 1) / 2.0)))
                high_median = v;
        }

        // Store 2 * median of K trailing elements
        int double_median = low_median + high_median;

        // If the current >= 2 * median
        if (a[i] >= double_median)
            answer++;

        // Decrease the frequency for (k-1)-th element
        cnt[a[i - d]]--;

        // Increase the frequency of the
        // current element
        cnt[a[i]]++;
    }

    // Print the count
    cout << answer << endl;
}

// Driver Code
int main()
{
    int input[] = { 1, 2, 2, 4, 5 };
    int n = sizeof input / sizeof input[0];
    int k = 3;

    solve(n, k, input);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG{

static int N = (int) 2e5;
static int V = 500;

// Function to find the count of array
// elements >= twice the median of K
// trailing array elements
static void solve(int n, int d, int input[])
{
    int []a = new int[N];

    // Stores frequencies
    int []cnt = new int[V + 1];

    // Stores the array elements
    for (int i = 0; i < n; ++i)
        a[i] = input[i];

    int answer = 0;

    // Count the frequencies of the
    // array elements
    for (int i = 0; i < d; ++i)
        cnt[a[i]]++;

    // Iterating from d to n-1 index
    // means (d+1)th element to nth element
    for (int i = d; i <= n - 1; ++i)
    {

        // To check the median
        int acc = 0;

        int low_median = -1, high_median = -1;

        // Iterate over the frequencies
        // of the elements
        for (int v = 0; v <= V; ++v)
        {

            // Add the frequencies
            acc += cnt[v];

            // Check if the low_median value is
            // obtained or not, if yes then do
            // not change as it will be minimum
            if (low_median == -1
                && acc >= (int)(Math.floor((d + 1) / 2.0)))
                low_median = v;

            // Check if the high_median value is
            // obtained or not, if yes then do not
            // change it as it will be maximum
            if (high_median == -1
                && acc >= (int)(Math.ceil((d + 1) / 2.0)))
                high_median = v;
        }

        // Store 2 * median of K trailing elements
        int double_median = low_median + high_median;

        // If the current >= 2 * median
        if (a[i] >= double_median)
            answer++;

        // Decrease the frequency for (k-1)-th element
        cnt[a[i - d]]--;

        // Increase the frequency of the
        // current element
        cnt[a[i]]++;
    }

    // Print the count
    System.out.print(answer +"\n");
}

// Driver Code
public static void main(String[] args)
{
    int input[] = { 1, 2, 2, 4, 5 };
    int n = input.length;
    int k = 3;

    solve(n, k, input);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

N = 200000
V = 500

# Function to find the count of array
# elements >= twice the median of K
# trailing array elements
def solve(n, d, input1):

    a = [0] * N

    # Stores frequencies
    cnt = [0] * (V + 1)

    # Stores the array elements
    for i in range(n):
        a[i] = input1[i]

    answer = 0

    # Count the frequencies of the
    # array elements
    for i in range(d):
        cnt[a[i]] += 1

    # Iterating from d to n-1 index
    # means (d+1)th element to nth element
    for i in range(d, n):

        # To check the median
        acc = 0

        low_median = -1
        high_median = -1

        # Iterate over the frequencies
        # of the elements
        for v in range(V + 1):

            # Add the frequencies
            acc += cnt[v]

            # Check if the low_median value is
            # obtained or not, if yes then do
            # not change as it will be minimum
            if (low_median == -1 and
                acc >= int(math.floor((d + 1) / 2.0))):
                low_median = v

            # Check if the high_median value is
            # obtained or not, if yes then do not
            # change it as it will be maximum
            if (high_median == -1 and
                acc >= int(math.ceil((d + 1) / 2.0))):
                high_median = v

        # Store 2 * median of K trailing elements
        double_median = low_median + high_median

        # If the current >= 2 * median
        if (a[i] >= double_median):
            answer += 1

        # Decrease the frequency for (k-1)-th element
        cnt[a[i - d]] -= 1

        # Increase the frequency of the
        # current element
        cnt[a[i]] += 1

    # Print the count
    print(answer)

# Driver Code
if __name__ == "__main__":

    input1 = [ 1, 2, 2, 4, 5 ]
    n = len(input1)
    k = 3

    solve(n, k, input1)

# This code is contributed by chitranayal
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

static int N = (int) 2e5;
static int V = 500;

// Function to find the count of array
// elements >= twice the median of K
// trailing array elements
static void solve(int n, int d, int []input)
{
    int []a = new int[N];

    // Stores frequencies
    int []cnt = new int[V + 1];

    // Stores the array elements
    for (int i = 0; i < n; ++i)
        a[i] = input[i];

    int answer = 0;

    // Count the frequencies of the
    // array elements
    for (int i = 0; i < d; ++i)
        cnt[a[i]]++;

    // Iterating from d to n-1 index
    // means (d+1)th element to nth element
    for (int i = d; i <= n - 1; ++i)
    {

        // To check the median
        int acc = 0;

        int low_median = -1, high_median = -1;

        // Iterate over the frequencies
        // of the elements
        for (int v = 0; v <= V; ++v)
        {

            // Add the frequencies
            acc += cnt[v];

            // Check if the low_median value is
            // obtained or not, if yes then do
            // not change as it will be minimum
            if (low_median == -1 &&
                acc >= (int)(Math.Floor((d + 1) / 2.0)))
                low_median = v;

            // Check if the high_median value is
            // obtained or not, if yes then do not
            // change it as it will be maximum
            if (high_median == -1 &&
                acc >= (int)(Math.Ceiling((d + 1) / 2.0)))
                high_median = v;
        }

        // Store 2 * median of K trailing elements
        int double_median = low_median + high_median;

        // If the current >= 2 * median
        if (a[i] >= double_median)
            answer++;

        // Decrease the frequency for (k-1)-th element
        cnt[a[i - d]]--;

        // Increase the frequency of the
        // current element
        cnt[a[i]]++;
    }

    // Print the count
    Console.Write(answer + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []input = { 1, 2, 2, 4, 5 };
    int n = input.Length;
    int k = 3;

    solve(n, k, input);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach
const N = 2e5;
const V = 500;

// Function to find the count of array
// elements >= twice the median of K
// trailing array elements
function solve(n, d, input)
{
    let a = new Array(N);

    // Stores frequencies
    let cnt = new Array(V + 1);

    // Stores the array elements
    for(let i = 0; i < n; ++i)
        a[i] = input[i];

    let answer = 0;

    // Count the frequencies of the
    // array elements
    for(let i = 0; i < d; ++i)
        cnt[a[i]]++;

    // Iterating from d to n-1 index
    // means (d+1)th element to nth element
    for(let i = d; i <= n - 1; ++i)
    {

        // To check the median
        let acc = 0;

        let low_median = -1, high_median = -1;

        // Iterate over the frequencies
        // of the elements
        for(let v = 0; v <= V; ++v)
        {

            // Add the frequencies
            acc += cnt[v];

            // Check if the low_median value is
            // obtained or not, if yes then do
            // not change as it will be minimum
            if (low_median == -1 &&
                acc >= parseInt(Math.floor((d + 1) / 2.0)))
                low_median = v;

            // Check if the high_median value is
            // obtained or not, if yes then do not
            // change it as it will be maximum
            if (high_median == -1 &&
                acc >= parseInt(Math.ceil((d + 1) / 2.0)))
                high_median = v;
        }

        // Store 2 * median of K trailing elements
        let double_median = low_median + high_median;

        // If the current >= 2 * median
        if (a[i] >= double_median)
            answer++;

        // Decrease the frequency for (k-1)-th element
        cnt[a[i - d]]--;

        // Increase the frequency of the
        // current element
        cnt[a[i]]++;
    }

    // Print the count
    document.write(answer);
}

// Driver Code
let input = [ 1, 2, 2, 4, 5 ];
let n = input.length;
let k = 3;

solve(n, k, input);

// This code is contributed by subham348

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*