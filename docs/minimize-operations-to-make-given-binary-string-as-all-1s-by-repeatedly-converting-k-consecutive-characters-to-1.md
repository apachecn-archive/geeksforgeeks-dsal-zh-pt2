# 通过重复将 K 个连续字符转换为 1 来最小化操作，使给定的二进制字符串全部为 1

> 原文:[https://www . geesforgeks . org/minimum-operations-to-make-给定-二进制-string-as-all-1s-by-repeat-k-continuous-characters-to-1/](https://www.geeksforgeeks.org/minimize-operations-to-make-given-binary-string-as-all-1s-by-repeatedly-converting-k-consecutive-characters-to-1/)

给定一个由 N 个字符组成的二进制字符串 **str** 和一个整数 **K** ，任务是找到将该字符串的所有字符转换为 **1 的**所需的最小移动量，其中在每次移动时，可以将 **K** 个连续字符转换为 **1** 。

**示例:**

> **输入:** str="0010 "，K=3
> **输出:** 2
> **说明:**
> 移动 1:从 0 到 2 选择子串，全部替换为 1。
> 移动 2:从 1 到 3 选择子串，全部替换为 1。
> 
> **输入:** str="0000010 "，K = 1
> T3】输出: 6

**方法:**这个问题可以用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。要解决此问题，请遵循以下步骤:

1.  创建变量 **cnt** ，以存储所需的最小移动次数。用 **0** 初始化。
2.  [使用变量 **i** 和 **str[i] = '0'** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，然后将 **i** 更新为 **i + K** ，并将 **cnt** 增加 **1** ，因为无论这些字符是什么，总是需要一个移动来将字符 **str[i]** 转换为**“1”**。
3.  循环结束后，返回 **cnt** ，这将是所需的答案。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// operations required to convert
// the binary string str to all 1s
int minMoves(string str, int K)
{
    int N = str.size();

    // Variable to store number
    // of minimum moves required
    int cnt = 0;

    int i = 0;

    // Loop to traverse str
    while (i < N) {

        // If element is '0'
        if (str[i] == '0') {
            i += K;
            cnt += 1;
        }

        // If element is '1'
        else {
            i++;
        }
    }

    return cnt;
}

// Driver Code
int main()
{
    string str = "0010";
    int K = 3;
    cout << minMoves(str, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
class GFG {

    // Function to find the minimum
    // operations required to convert
    // the binary String str to all 1s
    static int minMoves(String str, int K) {
        int N = str.length();

        // Variable to store number
        // of minimum moves required
        int cnt = 0;

        int i = 0;

        // Loop to traverse str
        while (i < N) {

            // If element is '0'
            if (str.charAt(i) == '0') {
                i += K;
                cnt += 1;
            }

            // If element is '1'
            else {
                i++;
            }
        }

        return cnt;
    }

    // Driver Code
    public static void main(String args[]) {
        String str = "0010";
        int K = 3;
        System.out.println(minMoves(str, K));
    }
}

// This code is contributed by Saurabh Jaiswal
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to find the minimum
# operations required to convert
# the binary string str to all 1s
def minMoves(str, K):
    N = len(str)

    # Variable to store number
    # of minimum moves required
    cnt = 0

    i = 0

    # Loop to traverse str
    while (i < N):

        # If element is '0'
        if (str[i] == '0'):
            i += K
            cnt += 1
        # If element is '1'
        else:
            i += 1

    return cnt

# Driver Code
str = "0010"
K = 3
print(minMoves(str, K))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# code for the above approach
using System;

class GFG
{

// Function to find the minimum
// operations required to convert
// the binary string str to all 1s
static int minMoves(string str, int K)
{
    int N = str.Length;

    // Variable to store number
    // of minimum moves required
    int cnt = 0;

    int i = 0;

    // Loop to traverse str
    while (i < N) {

        // If element is '0'
        if (str[i] == '0') {
            i += K;
            cnt += 1;
        }

        // If element is '1'
        else {
            i++;
        }
    }

    return cnt;
}

// Driver Code
public static void Main()
{
    string str = "0010";
    int K = 3;
    Console.Write(minMoves(str, K));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to find the minimum
       // operations required to convert
       // the binary string str to all 1s
       function minMoves(str, K) {
           let N = str.length;

           // Variable to store number
           // of minimum moves required
           let cnt = 0;

           let i = 0;

           // Loop to traverse str
           while (i < N) {

               // If element is '0'
               if (str[i] == '0') {
                   i += K;
                   cnt += 1;
               }

               // If element is '1'
               else {
                   i++;
               }
           }

           return cnt;
       }

       // Driver Code

       let str = "0010";
       let K = 3;
       document.write(minMoves(str, K));

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)