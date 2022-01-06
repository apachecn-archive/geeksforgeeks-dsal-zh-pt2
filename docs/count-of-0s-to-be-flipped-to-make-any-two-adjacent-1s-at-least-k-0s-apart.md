# 翻转 0 的计数，使任意两个相邻的 1 至少相隔 K 个 0

> 原文:[https://www . geeksforgeeks . org/要翻转的 0s 计数以使任意两个相邻的 1s 至少 k-0s 分开/](https://www.geeksforgeeks.org/count-of-0s-to-be-flipped-to-make-any-two-adjacent-1s-at-least-k-0s-apart/)

给定一个二进制字符串 **s** 和一个数字 **K，**的任务是找到可以被 **1s** 替换的 **0s** 的最大数量，使得两个相邻的 **1s** 之间至少相隔 **K** **0s** 。
**示例:**

> **输入:** K = 2，s = "000000"
> **输出:** 2
> **说明:**
> 在 0、3 位置改变 0s。那么最后的字符串将是“100100”，这样每一个 **1** 至少被 2 个 **0s** 隔开。
> 
> **输入:** K = 1，s =“01001000100000”
> **输出:** 3
> **说明:**
> 在位置 6、10、12 改变 0s。那么最后的字符串将是“01001010101010”，这样每 1 个字符串之间至少会有 1 个 **0s** 。

**进场:**

1.  将给定字符串的所有字符插入一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)(比如说 **arr[])** 。
2.  遍历数组 **arr[]** ，将所有 **0s** 转换为 **-1** ，其位于 **< = K** 处，靠近已存在的 **1** 。该操作给出了可插入 **1** 的所有可能位置。
3.  将**计数**变量初始化为 0。
4.  从左到右遍历数组 **arr[]** 。一旦遇到第一个 0，就用 1 替换它，并增加计数值。
5.  将所有位于新转换 1 附近 **< = K** 处的 **0s** 转换为 **-1** 。
6.  继续遍历数组直到结束，每次遇到 0，重复步骤**4–5**。

下面是上述方法的实现:

## C++

```
// C++ program for the above problem
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// count of 0s to be flipped
int count(int k, string s)
{
    int ar[s.length()];
    int end = 0;

    // Loop traversal to mark K
    // adjacent positions to the right
    // of already existing 1s.
    for(int i = 0; i < s.length(); i++)
    {
       if (s[i] == '1')
       {
           for(int j = i;
                   j < s.length() &&
                   j <= i + k; j++)
           {
              ar[j] = -1;
              end = j;
           }
           i = end;
       }
    }
    end = 0;

    // Loop traversal to mark K
    // adjacent positions to the left
    // of already existing 1s.
    for(int i = s.length() - 1;
            i >= 0; i--)
    {
       if (s[i] == '1')
       {
           for(int j = i;
                   j >= 0 &&
                   j >= i - k; j--)
           {
              ar[j] = -1;
              end = j;
           }
           i = end;
       }
    }

    int ans = 0;
    end = 0;

    // Loop to count the maximum
    // number of 0s that will be
    // replaced by 1s
    for(int j = 0;
            j < s.length(); j++)
    {
       if (ar[j] == 0)
       {
           ans++;
           for(int g = j;
                   g <= j + k &&
                   g < s.length(); g++)
           {
              ar[g] = -1;
              end = g;
           }
           j = end - 1;
       }
    }
    return ans;
}

// Driver code
int main()
{
    int K = 2;
    string s = "000000";

    cout << count(K, s) << endl;

    return 0;
}

// This code is contributed by divyeshrabadiya07
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above problem
import java.util.Scanner;

// Driver Code
public class Check {

    // Function to find the
    // count of 0s to be flipped
    public static int count(int k, String s)
    {

        int ar[] = new int[s.length()];
        int end = 0;

        // Loop traversal to mark K
        // adjacent positions to the right
        // of already existing 1s.
        for (int i = 0;
             i < s.length(); i++) {

            if (s.charAt(i) == '1') {

                for (int j = i;
                     j < s.length()
                     && j <= i + k;
                     j++) {

                    ar[j] = -1;
                    end = j;
                }
                i = end;
            }
        }

        end = 0;

        // Loop traversal to mark K
        // adjacent positions to the left
        // of already existing 1s.
        for (int i = s.length() - 1;
             i >= 0; i--) {

            if (s.charAt(i) == '1') {
                for (int j = i;
                     j >= 0 && j >= i - k;
                     j--) {

                    ar[j] = -1;
                    end = j;
                }

                i = end;
            }
        }

        int ans = 0;
        end = 0;

        // Loop to count the maximum
        // number of 0s that will be
        // replaced by 1s
        for (int j = 0;
             j < s.length(); j++) {

            if (ar[j] == 0) {

                ans++;
                for (int g = j;
                     g <= j + k
                     && g < s.length();
                     g++) {

                    ar[g] = -1;
                    end = g;
                }

                j = end - 1;
            }
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {

        int K = 2;
        String s = "000000";

        System.out.println(count(K, s));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above problem

# Function to find the 
# count of 0s to be flipped
def count(k, s):

    ar = [0] * len(s)
    end = 0

    # Loop traversal to mark K 
    # adjacent positions to the right 
    # of already existing 1s.
    for i in range(len(s)):
        if s[i] == '1':

            for j in range(i, len(s)):
                if (j <= i + k):
                    ar[j] = -1
                    end = j

            i = end

    end = 0

    # Loop traversal to mark K 
    # adjacent positions to the left 
    # of already existing 1s.
    for i in range(len(s) - 1, -1, -1):
        if (s[i] == '1'):

            for j in range(i, -1, -1):
                if (j >= i - k):
                    ar[j] = -1
                    end = j

            i = end

    ans = 0
    end = 0

    # Loop to count the maximum 
    # number of 0s that will be 
    # replaced by 1s
    for j in range(len(s)):
        if (ar[j] == 0):
            ans += 1

            for g in range(j, len(s)):
                if (g <= j + k):
                    ar[g] = -1
                    end = g

            j = end - 1

    return ans

# Driver code
K = 2
s = "000000"

print(count(K, s))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program for the above problem
using System;

class GFG{

// Function to find the
// count of 0s to be flipped
public static int count(int k, String s)
{

    int []ar = new int[s.Length];
    int end = 0;

    // Loop traversal to mark K
    // adjacent positions to the right
    // of already existing 1s.
    for(int i = 0; i < s.Length; i++)
    {
       if (s[i] == '1')
       {
           for(int j = i;
                   j < s.Length &&
                   j <= i + k; j++)
           {
              ar[j] = -1;
              end = j;
           }
           i = end;
       }
    }
    end = 0;

    // Loop traversal to mark K
    // adjacent positions to the left
    // of already existing 1s.
    for(int i = s.Length - 1; i >= 0; i--)
    {
       if (s[i] == '1')
       {
           for(int j = i;
                   j >= 0 &&
                   j >= i - k; j--)
           {
              ar[j] = -1;
              end = j;
           }
           i = end;
       }
    }

    int ans = 0;
    end = 0;

    // Loop to count the maximum
    // number of 0s that will be
    // replaced by 1s
    for(int j = 0; j < s.Length; j++)
    {
       if (ar[j] == 0)
       {
           ans++;
           for(int g = j;
                   g <= j + k &&
                   g < s.Length; g++)
           {
              ar[g] = -1;
              end = g;
           }
           j = end - 1;
       }
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int K = 2;
    String s = "000000";

    Console.WriteLine(count(K, s));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript program for the above problem

// Function to find the
// count of 0s to be flipped
function count(k, s)
{
    var ar = Array(s.length).fill(0);
    var end = 0;

    var i,j;
    // Loop traversal to mark K
    // adjacent positions to the right
    // of already existing 1s.
    for(i = 0; i < s.length; i++)
    {
       if (s[i] == '1')
       {
           for(j = i; j < s.length &&
               j <= i + k; j++)
           {
              ar[j] = -1;
              end = j;
           }
           i = end;
       }
    }
    end = 0;

    // Loop traversal to mark K
    // adjacent positions to the left
    // of already existing 1s.
    for(i = s.length - 1; i >= 0; i--)
    {
       if (s[i] == '1')
       {
           for(j = i; j >= 0 &&
               j >= i - k; j--)
           {
              ar[j] = -1;
              end = j;
           }
           i = end;
       }
    }

    var ans = 0;
    end = 0;

    // Loop to count the maximum
    // number of 0s that will be
    // replaced by 1s
    var g;
    for(j = 0;j < s.length; j++)
    {
       if (ar[j] == 0)
       {
           ans++;
           for(g = j; g <= j + k &&
               g < s.length; g++)
           {
              ar[g] = -1;
              end = g;
           }
           j = end - 1;
       }
    }
    return ans;
}

// Driver code
    var K = 2;
    var s = "000000";

    document.write(count(K, s));

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * K)*
***辅助空间:** O(1)*