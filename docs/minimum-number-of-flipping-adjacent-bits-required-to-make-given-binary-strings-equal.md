# 使给定二进制字符串相等所需的翻转相邻位的最小数量

> 原文:[https://www . geeksforgeeks . org/最小翻转相邻位数-要求使给定二进制字符串相等/](https://www.geeksforgeeks.org/minimum-number-of-flipping-adjacent-bits-required-to-make-given-binary-strings-equal/)

给定两个相同长度的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **s1[]** 和**S2[]****N，**的任务是找到使它们相等的最小操作数。如果不可能打印 **-1** 。一个操作定义为选择一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)的两个相邻索引，并将这些位置的字符反转，即 **1** 到 **0** ，反之亦然。

**示例:**

> **输入:**S1[]=“0101”，S2[]=“1111”
> **输出:** 2
> **解释:**将第一个字符串中第 1 和第 2 个索引处以及第二个字符串中第 0 和第 1 个索引处的字符反转，使其等于 0011。还有其他方法也可以，比如转换到 1111 等。
> 
> **输入:** s1[] = "011 "，s2[] = "111"
> **输出:** -1

**方法:**思路是线性遍历两个[字符串](https://www.geeksforgeeks.org/tag/binary-string/)，如果在任何索引处字符不同，则反转**I<sup>th</sup>T7】和**(I+1)<sup>th</sup>T11】字符在[字符串](https://www.geeksforgeeks.org/tag/binary-string/)T14】S1[]。**按照以下步骤解决问题:**

*   初始化变量**计数**为 **0** 存储答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   如果 **s1[i]** 不等于 **s2[i]** ，则执行以下任务:
        *   如果**S1【I】**等于 **1，**则改为 **0** ，否则改为 **1。**
        *   同样，如果 **s1[i+1]** 等于 **1，**则改为 **0** ，否则改为 **1。**
        *   最后，将**计数**的值增加 **1。**
*   如果 **s1[]** 等于 **s2[]，**则返回**的值，将**算作答案，否则返回 **-1。**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of inversions required.
int find_Min_Inversion(int n, string s1, string s2)
{

    // Initializing the answer
    int count = 0;

    // Iterate over the range
    for (int i = 0; i < n - 1; i++) {
        if (s1[i] != s2[i]) {

            // If s1[i]!=s2[i], then inverse
            // the characters at i snd (i+1)
            // positions in s1.
            if (s1[i] == '1') {
                s1[i] = '0';
            }
            else {
                s1[i] = '1';
            }
            if (s1[i + 1] == '1') {
                s1[i + 1] = '0';
            }
            else {
                s1[i + 1] = '1';
            }

            // Adding 1 to counter
            // if characters are not same
            count++;
        }
    }
    if (s1 == s2) {
        return count;
    }
    return -1;
}

// Driver Code
int main()
{
    int n = 4;
    string s1 = "0101";
    string s2 = "1111";
    cout << find_Min_Inversion(n, s1, s2) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the minimum number
    // of inversions required.
    static int find_Min_Inversion(int n, char[] s1, char[] s2) {

        // Initializing the answer
        int count = 0;

        // Iterate over the range
        for (int i = 0; i < n - 1; i++) {
            if (s1[i] != s2[i]) {

                // If s1[i]!=s2[i], then inverse
                // the characters at i snd (i+1)
                // positions in s1.
                if (s1[i] == '1') {
                    s1[i] = '0';
                } else {
                    s1[i] = '1';
                }
                if (s1[i + 1] == '1') {
                    s1[i + 1] = '0';
                } else {
                    s1[i + 1] = '1';
                }

                // Adding 1 to counter
                // if characters are not same
                count++;
            }
        }

        if (String.copyValueOf(s1).equals(String.copyValueOf(s2))) {
            return count;
        }
        return -1;
    }

    // Driver Code
    public static void main(String[] args) {
        int n = 4;
        String s1 = "0101";
        String s2 = "1111";
        System.out.print(find_Min_Inversion(n, s1.toCharArray(), s2.toCharArray()) + "\n");
    }
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the minimum number
# of inversions required.
def find_Min_Inversion(n, s1, s2):

    # Initializing the answer
    count = 0

    # Iterate over the range
    s1 = list(s1)
    s2 = list(s2)
    for i in range(n - 1):
        if (s1[i] != s2[i]):

            # If s1[i]!=s2[i], then inverse
            # the characters at i snd (i+1)
            # positions in s1.
            if (s1[i] == '1'):
                s1[i] = '0'
            else:
                s1[i] = '1'
            if (s1[i + 1] == '1'):
                s1[i + 1] = '0'
            else:
                s1[i + 1] = '1'

            # Adding 1 to counter
            # if characters are not same
            count += 1
    s1 = ''.join(s1)
    s2 = ''.join(s2)
    if (s1 == s2):
        return count
    return -1

# Driver Code
if __name__ == '__main__':
    n = 4
    s1 = "0101"
    s2 = "1111"
    print(find_Min_Inversion(n, s1, s2))

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// Java program for the above approach
// Function to find the minimum number
// of inversions required.
function find_Min_Inversion(n, s1, s2)
{

    // Initializing the answer
    let count = 0;

    // Iterate over the range
    for (let i = 0; i < n - 1; i++) {
        if (s1[i] != s2[i]) {

            // If s1[i]!=s2[i], then inverse
            // the characters at i snd (i+1)
            // positions in s1.
            if (s1[i] = '1') {
                s1[i] = '0';
            }
            else {
                s1[i] = '1';
            }
            if (s1[i + 1] = '1') {
                s1[i + 1] = '0';
            }
            else {
                s1[i + 1] = '1';
            }

            // Adding 1 to counter
            // if characters are not same
            count++;
        }
    }
    if (s1 != s2) {
        return count;
    }
     return -1;
}

// Driver Code
    let n = 4;
    let s1 = "0101";
    let s2 = "1111";
    document.write(find_Min_Inversion(n, s1, s2));

// This code is contributed by shivanisinghss2110
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)