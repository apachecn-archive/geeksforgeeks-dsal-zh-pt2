# 通过反复翻转大小为 K 的子串中的字符，最小化翻转，使二进制字符串全部为 1

> 原文:[https://www . geeksforgeeks . org/通过反复翻转大小为 k 的子串中的字符将二进制字符串最小化为全 1/](https://www.geeksforgeeks.org/minimize-flips-to-make-binary-string-as-all-1s-by-flipping-characters-in-substring-of-size-k-repeatedly/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和一个整数 **K** ，任务是通过[翻转大小为**K**的子字符串](https://www.geeksforgeeks.org/number-flips-make-binary-string-alternate/)中的字符，找到使所有字符成为二进制字符串中的 **1s** 所需的最小操作数。如果不可能，则打印**-1”**。

**示例:**

> **输入:** S = "00010110 "，K = 3
> **输出:** 3
> **说明:**
> 下面是执行的操作:
> 
> 1.  考虑大小为 K(= 3)的子字符串 S[0，2]，翻转这些字符会将字符串修改为“11110110”。
> 2.  考虑大小为 K(= 3)的子字符串 S[4，6]，翻转这些字符会将字符串修改为“11111000”。
> 3.  考虑大小为 K(= 3)的子字符串 S[5，7]，翻转这些字符会将字符串修改为“111111111”。
> 
> 上述运算后，所有的 0 都转换为 1，所需的最小运算次数为 3。
> 
> **输入:** S = "01010 "，K = 4
> **输出:** -1

**方法:**给定的问题可以使用 [**贪婪方法**](https://www.geeksforgeeks.org/greedy-algorithms/) 来解决。按照以下步骤解决问题:

*   初始化一个变量，将**次操作**设为 **0** ，存储所需最小操作次数的计数。
*   [使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，如果字符**S【I】**为**‘0’**， **(i + K)** 的值最多为**K**，则翻转子字符串**S【I，I+K】**的所有字符，并将 **minOperations** 的值增加
*   **完成上述操作后，遍历字符串 **S** ，如有字符**‘0’**则打印**-1”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。**
*   **如果字符串 **S** 的所有字符都是 **1s** ，则打印**最小操作数**作为最小操作数。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations required to convert all
// the characters to 1 by flipping the
// substrings of size K
void minOperation(string S, int K, int N)
{

    // Stores the minimum number of
    // operations required
    int min = 0;

    int i;

    // Traverse the string S
    for (i = 0; i < N; i++) {

        // If the character is 0
        if (S[i] == '0' && i + K <= N) {

            // Flip the substrings of
            // size K starting from i
            for (int j = i; j < i + K; j++) {
                if (S[j] == '1')
                    S[j] = '0';
                else
                    S[j] = '1';
            }

            // Increment the minimum count
            // of operations required
            min++;
        }
    }

    // After performing the operations
    // check if string S contains any 0s
    for (i = 0; i < N; i++) {
        if (S[i] == '0')
            break;
    }

    // If S contains only 1's
    if (i == N)
        cout << min;
    else
        cout << -1;
}

// Driver Code
int main()
{

    string S = "00010110";
    int K = 3;
    int N = S.length();
    minOperation(S, K, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
public class GFG
{

// Function to find the minimum number
// of operations required to convert all
// the characters to 1 by flipping the
// substrings of size K
static void minOperation(String S, int K, int N)
{

    // Stores the minimum number of
    // operations required
    int min = 0;

    int i;

    // Traverse the string S
    for (i = 0; i < N; i++) {

        // If the character is 0
        if (S.charAt(i) == '0' && i + K <= N) {

            // Flip the substrings of
            // size K starting from i
            for (int j = i; j < i + K; j++) {
                if (S.charAt(j) == '1')
                    S = S.substring(0, j) + '0' + S.substring(j + 1);
                else
                   S = S.substring(0, j) + '1' + S.substring(j + 1);
            }

            // Increment the minimum count
            // of operations required
            min++;
        }
    }

    // After performing the operations
    // check if string S contains any 0s
    for (i = 0; i < N; i++) {
        if (S.charAt(i) == '0')
            break;
    }

    // If S contains only 1's
    if (i == N)
      System.out.println(min);
    else
      System.out.println(-1);
}

// Driver Code
public static void main(String []args)
{

    String S = "00010110";
    int K = 3;
    int N = S.length();
    minOperation(S, K, N);
}
}

// This code is contributed by AnkThon
```

## **蟒蛇 3**

```
# Function to find the minimum number
# of operations required to convert all
# the characters to 1 by flipping the
# substrings of size K
def minOperation(St, K, N):
    S = list(St)

    # Stores the minimum number of
    # operations required
    min = 0

    i = 0

    # Traverse the string S
    for i in range(0, N):

        # If the character is 0
        if (S[i] == '0' and i + K <= N):

            # Flip the substrings of
            # size K starting from i
            j = i
            while(j < i + K):
                if (S[j] == '1'):
                    S[j] = '0'
                else:
                    S[j] = '1'
                j += 1

            # Increment the minimum count
            # of operations required
            min += 1

    # After performing the operations
    # check if string S contains any 0s
    temp = 0

    for i in range(0, N):
        temp += 1
        if (S[i] == '0'):
            break

    # If S contains only 1's
    if (temp == N):
        print(min)
    else:
        print(-1)

# Driver Code
S = "00010110"
K = 3
N = len(S)
minOperation(S, K, N)

# This code is contributed by gfgking
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum number
// of operations required to convert all
// the characters to 1 by flipping the
// substrings of size K
static void minOperation(string S, int K, int N)
{

    // Stores the minimum number of
    // operations required
    int min = 0;

    int i;

    // Traverse the string S
    for (i = 0; i < N; i++) {

        // If the character is 0
        if (S[i] == '0' && i + K <= N) {

            // Flip the substrings of
            // size K starting from i
            for (int j = i; j < i + K; j++) {
                if (S[j] == '1')
                    S = S.Substring(0, j) + '0' + S.Substring(j + 1);
                else
                   S = S.Substring(0, j) + '1' + S.Substring(j + 1);
            }

            // Increment the minimum count
            // of operations required
            min++;
        }
    }

    // After performing the operations
    // check if string S contains any 0s
    for (i = 0; i < N; i++) {
        if (S[i] == '0')
            break;
    }

    // If S contains only 1's
    if (i == N)
      Console.Write(min);
    else
      Console.Write(-1);
}

// Driver Code
public static void Main()
{

    string S = "00010110";
    int K = 3;
    int N = S.Length;
    minOperation(S, K, N);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## **java 描述语言**

```
<script>

// Function to find the minimum number
// of operations required to convert all
// the characters to 1 by flipping the
// substrings of size K
function minOperation(St, K, N)
{
    S = St.split('');

    // Stores the minimum number of
    // operations required
    let min = 0;

    let i;

    // Traverse the string S
    for (i = 0; i < N; i++) {

        // If the character is 0
        if (S[i] == '0' && i + K <= N) {

            // Flip the substrings of
            // size K starting from i
            for (let j = i; j < i + K; j++) {
                if (S[j] == '1')
                    S[j] = '0';
                else
                    S[j] = '1';
            }

            // Increment the minimum count
            // of operations required
            min++;
        }
    }

    // After performing the operations
    // check if string S contains any 0s
    for (i = 0; i < N; i++) {
        if (S[i] == '0')
            break;
    }

    // If S contains only 1's
    if (i == N)
        document.write(min);
    else
        document.write(-1);
}

// Driver Code
        let S = "00010110";
    let K = 3;
    let N = S.length;
    minOperation(S, K, N);

// This code is contributed by sanjoy_62.   
</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:** O(N*K)*
***辅助空间:** O(1)***