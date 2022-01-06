# 给定二进制串中只包含 1 的 K 长度子阵的计数|集合 2

> 原文:[https://www . geesforgeks . org/count-of-k-length-subarrays-只包含给定二进制字符串中的-1s-set-2/](https://www.geeksforgeeks.org/count-of-k-length-subarrays-containing-only-1s-in-given-binary-string-set-2/)

给定二进制字符串 **str** ，任务是找到仅包含 **1** s 的 **K** 长度子阵的计数

**示例**

> **输入:** str = "0101000 "，K=1
> **输出:** 2
> **说明:** 0101000 - >有 2 个长度为 1 的子阵，只包含 1s。
> 
> **输入:** str = "11111001 "，K = 3
> T3】输出: 3

**方法:**给定的问题也可以使用[滑动窗口技术](http://www.geeksforgeeks.org/window-sliding-technique/)来解决。创建一个大小为 **K** 的窗口，初始计数为从范围 **0** 到 **K-1** 的 **1** s。然后从索引 **1** 到 **N-1** 遍历字符串，减去 **i-1** 的值，将 **i+K** 的值加到当前计数中。这里，如果当前计数等于 **K** ，则增加子阵列的可能计数。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of all possible
// k length subarrays
int get(string s, int k)
{
    int n = s.length();

    int cntOf1s = 0;

    for (int i = 0; i < k; i++)
        if (s[i] == '1')
            cntOf1s++;

    int ans = cntOf1s == k ? 1 : 0;

    for (int i = 1; i < n; i++) {
        cntOf1s = cntOf1s - (s[i - 1] - '0')
                  + (s[i + k - 1] - '0');
        if (cntOf1s == k)
            ans++;
    }
    return ans;
}

// Driver code
int main()
{
    string str = "0110101110";
    int K = 2;
    cout << get(str, K) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.*;
public class GFG {

  // Function to find the count of all possible
  // k length subarrays
  static int get(String s, int k)
  {
    int n = s.length();

    int cntOf1s = 0;

    for (int i = 0; i < k; i++) {
      if (s.charAt(i) == '1') {
        cntOf1s++;
      }
    }

    int ans = cntOf1s == k ? 1 : 0;

    for (int i = 1; i < n; i++) {
      if(i + k - 1 < n) {
        cntOf1s = cntOf1s - (s.charAt(i - 1) - '0')
          + (s.charAt(i + k - 1) - '0');
      }
      if (cntOf1s == k)
        ans++;
    }
    return ans;
  }

  // Driver code
  public static void main(String args[])
  {
    String str = "0110101110";
    int K = 2;
    System.out.println(get(str, K));

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python code to implement above approach

# Function to find the count of all possible
# k length subarrays
def get(s, k):
    n = len(s);

    cntOf1s = 0;

    for i in range(0,k):
        if (s[i] == '1'):
            cntOf1s += 1;

    ans = i if (cntOf1s == k) else 0;

    for i in range(1, n):
        if (i + k - 1 < n):
            cntOf1s = cntOf1s - (ord(s[i - 1]) - ord('0')) + (ord(s[i + k - 1]) - ord('0'));

        if (cntOf1s == k):
            ans += 1;

    return ans;

# Driver code
if __name__ == '__main__':
    str = "0110101110";
    K = 2;
    print(get(str, K));

# This code is contributed by 29AjayKumar
```

## C#

```
// C# code to implement above approach
using System;

public class GFG {

  // Function to find the count of all possible
  // k length subarrays
  static int get(string s, int k)
  {
    int n = s.Length;

    int cntOf1s = 0;

    for (int i = 0; i < k; i++) {
      if (s[i] == '1') {
        cntOf1s++;
      }
    }

    int ans = cntOf1s == k ? 1 : 0;

    for (int i = 1; i < n; i++) {
      if (i + k - 1 < n) {
        cntOf1s = cntOf1s - (s[i - 1] - '0')
          + (s[i + k - 1] - '0');
      }
      if (cntOf1s == k)
        ans++;
    }
    return ans;
  }

  // Driver code
  public static void Main()
  {
    string str = "0110101110";
    int K = 2;
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
     let n = s.length;
     let cntOf1s = 0;

     for (let i = 0; i < k; i++)
       if (s[i] == '1')
         cntOf1s++;

     let ans = cntOf1s == k ? 1 : 0;

     for (let i = 1; i < n; i++) 
     {
       cntOf1s = cntOf1s - (s[i - 1] - '0')
         + (s[i + k - 1] - '0');
       if (cntOf1s == k)
         ans++;
     }
     return ans;
   }

   // Driver code
   let str = "0110101110";
   let K = 2;
   document.write(get(str, K) + '<br>')

 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
3
```

**时间复杂度:** O(N)，其中 N 为字符串的长度。

**辅助空间:** O(1)。