# 对连续元素严格递减的子阵列进行计数

> 原文:[https://www . geeksforgeeks . org/count-带有严格递减连续元素的子数组/](https://www.geeksforgeeks.org/count-subarrays-with-strictly-decreasing-consecutive-elements/)

给定一个包含整数的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 。任务是找出相差 **1** 的递减子阵个数。

**示例:**

> **输入:** arr[] = {3，2，1，4}
> **输出:** 7
> **说明:**以下是可能的递减子阵列，差异为 1。
> 【3】、【2】、【1】、【4】、【3，2】、【2，1】、【3，2，1】
> 所以，答案是 7。
> 
> **输入:** arr[] = {5，4，3，2，1，6 }
> T3】输出: 16

**天真法:**这个问题可以用[动态规划](http://www.geeksforgeeks.org/dynamic-programming/)解决。按照以下步骤解决给定的问题。

1.  对于每个索引 I，任务是计算以 **i** 结束的子阵列数量，其遵循以下模式 **arr[i-2]==arr[i-1]+1** ， **arr[i-1]==arr[i]+1** 。
2.  初始化一个变量，比如说 **ans = 0** ，以存储递减子阵列的数量，其差值为 **1** 。
3.  我们可以制作一个 **dp[]** 数组，存储每个索引的这些连续元素的计数。
4.  dp[i]是以 **i** 结束的子阵列的数量，它遵循这个模式。
5.  遍历 **dp[]** 并将 ans 中的每个值相加。
6.  返回**和**作为最终结果。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count number of
// decreasing subarrays with difference 1
long long getcount(vector<int>& p)
{
    int size = p.size(), cnt = 0;
    long long ans = 0;
    vector<int> dp(size, cnt);
    for (int i = 0; i < size; i++) {
        if (i == 0)
            cnt = 1;
        else if (p[i] + 1 == p[i - 1])
            cnt++;
        else
            cnt = 1;
        dp[i] = cnt;
    }
    for (int i = 0; i < size; i++)
        ans += dp[i];
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr{ 5, 4, 3, 2, 1, 6 };

    // Function Call
    cout << getcount(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement the above approach
import java.util.*;
public class GFG
{

  // Function to count number of
  // decreasing subarrays with difference 1
  static long getcount(int p[])
  {
    int size = p.length, cnt = 0;
    long ans = 0;

    int dp[] = new int[size];
    for(int i = 0; i < size; i++) {
      dp[i] = cnt;
    }

    for (int i = 0; i < size; i++) {
      if (i == 0)
        cnt = 1;
      else if (p[i] + 1 == p[i - 1])
        cnt++;
      else
        cnt = 1;
      dp[i] = cnt;
    }
    for (int i = 0; i < size; i++)
      ans += dp[i];
    return ans;
  }

  // Driver code
  public static void main(String args[])
  {
    int arr[] = { 5, 4, 3, 2, 1, 6 };

    // Function Call
    System.out.println(getcount(arr));
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>

// JavaScript program for above approach

// Function to count number of decreasing
// subarrays with difference 1
function getcount(p)
{
    let size = p.length, cnt = 0;
    let ans = 0;
    let dp = new Array(size).fill(cnt);

    for(let i = 0; i < size; i++)
    {
        if (i == 0)
            cnt = 1;
        else if (p[i] + 1 == p[i - 1])
            cnt++;
        else
            cnt = 1;

        dp[i] = cnt;
    }
    for(let i = 0; i < size; i++)
        ans += dp[i];

    return ans;
}

// Driver Code
let arr = [ 5, 4, 3, 2, 1, 6 ];

// Function Call
document.write(getcount(arr));

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
16
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)

**高效方法:**在上述方法中，通过用变量替换 **dp[]** 阵列来跟踪当前子阵列数量，可以将辅助空间复杂度进一步优化为恒定空间。按照以下步骤解决给定的问题。

*   初始化一个变量，比如**计数= 0** 。
*   当 **arr[i]-arr[i-1 ]==1** 时开始遍历数组，形成一个由 **1** 递减的数字链，然后**计数++** 。
*   把总数加到 ans 上。
*   当链条断裂时，这意味着， **arr[i]-arr[i-1]！=1** 然后重置计数。
*   返回**和**作为最终结果。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// decreasing subarrays wit difference 1
long long getcount(vector<int>& arr)
{
    long long int ans = arr.size();
    long long int count = 0;
    for (int i = 1; i < arr.size(); i++) {
        if (arr[i - 1] - arr[i] == 1)
            count++;
        else
            count = 0;
        ans = ans + count;
    }
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr{ 5, 4, 3, 2, 1, 6 };

    // Function Call
    cout << getcount(arr);

    return 0;
}
```

**Output**

```
16
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)