# 给定二进制串中只包含 1 的 K 长度子阵的计数

> 原文:[https://www . geesforgeks . org/count-of-k-length-subarrays-只包含给定二进制字符串中的-1s/](https://www.geeksforgeeks.org/count-of-k-length-subarrays-containing-only-1s-in-given-binary-string/)

给定一个二进制字符串 **str** ，任务是找到 **K** 长度**子阵**中仅包含 **1s 的**计数**。**

**示例:**

> **输入:** str = "0101000 "，K=1
> **输出:** 2
> **说明:**0**1**0**1**000->有 2 个子阵 1 个
> 
> **输入:** str = "11111001 "，K = 3
> T3】输出: 3

**接近**:跟踪**连续**的**组大小**即可解决任务。一旦得到**组大小**，我们就可以推导出长度为 **k** 的可能子阵列的数量，所有 **1s** 都是**组大小–k+1**。

按照以下步骤解决问题:

*   从**开始**迭代二进制字符串
*   **如果遇到 **1** ，并且在 **0** 到来时，增加**计数。
*   **存储**当前计数**以获得**连续 1s、**和**的组大小，并将**计数重新初始化为 **0。****
*   使用关系**组大小–k+1**将该**组大小**中大小为 k 的可能子阵列的数量相加
*   返回计数的最终总和。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of all possible
// k length subarrays
int get(string s, int k)
{
    // Add dummy character at last to handle
    // edge cases, where string ends with '1'
    s += '0';
    int n = s.length();

    int cnt = 0, ans = 0;
    for (int i = 0; i < n; i++) {
        if (s[i] == '1')
            cnt++;
        else {
            if (cnt >= k) {
                ans += (cnt - k + 1);
            }
            cnt = 0;
        }
    }
    return ans;
}

// Driver code
int main()
{
    string str = "0101000";
    int K = 1;
    cout << get(str, K) << endl;
    return 0;
}
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the count of all possible
# k length subarrays
def get(s, k):

    # Add dummy character at last to handle
    # edge cases, where string ends with '1'
    s += '0'
    n = len(s)

    cnt = 0
    ans = 0
    for i in range(n):
        if (s[i] == '1'):
            cnt += 1
        else:
            if (cnt >= k):
                ans += (cnt - k + 1)
            cnt = 0
    return ans

# Driver code
str = "0101000"
K = 1
print(get(str, K))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the count of all possible
    // k length subarrays
    static int get(string s, int k)
    {

        // Add dummy character at last to handle
        // edge cases, where string ends with '1'
        s += '0';
        int n = s.Length;

        int cnt = 0, ans = 0;
        for (int i = 0; i < n; i++) {
            if (s[i] == '1')
                cnt++;
            else {
                if (cnt >= k) {
                    ans += (cnt - k + 1);
                }
                cnt = 0;
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        string str = "0101000";
        int K = 1;
        Console.WriteLine(get(str, K));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach

    // Function to find the count of all possible
    // k length subarrays
    function get(s, k) 
    {

      // Add dummy character at last to handle
      // edge cases, where string ends with '1'
      s += '0';
      let n = s.length;

      let cnt = 0, ans = 0;
      for (let i = 0; i < n; i++) {
        if (s[i] == '1')
          cnt++;
        else {
          if (cnt >= k) {
            ans += (cnt - k + 1);
          }
          cnt = 0;
        }
      }
      return ans;
    }

    // Driver code
    let str = "0101000";
    let K = 1;
    document.write(get(str, K) + '<br>');

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
```

***时间复杂度*****:**O(N)
***辅助空间*** **:** O(1)