# 最大计数“010 ..”可以从给定二进制字符串中删除的子序列

> 原文:[https://www . geeksforgeeks . org/从给定二进制字符串中可移除的最大子序列数/](https://www.geeksforgeeks.org/maximum-count-of-010-subsequences-that-can-be-removed-from-given-binary-string/)

给定一个由大小为 **N** 组成的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是找到形式为**“010 ..”的二进制子序列的最大数量长度至少为 **2** 的**可以从给定的弦 **S** 上移除。

**示例:**

> **输入:**S =“110011010”
> **输出:** 3
> **解释:**
> 以下是删除的子序列:
> **操作 1:** 选择子序列作为索引{2，4}的“01”，删除它会修改字符串 S =“1101010”。
> **操作 2:** 选择索引{2，3}的子序列为“01”，删除会修改字符串 S =“11010”。
> **操作 3:** 选择索引{2，3}的子序列为“01”，删除会修改字符串 S =“110”。
> 从以上观察，去除子序列的最大次数为 3 次。
> 
> **输入:**S = " 00111110011 "
> T3】输出: 4

**方法:**给定的问题可以通过每次移除**“01”**类型的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)来解决，以最大化移除的子序列数量。因此，这可以通过保存存储字符数计数的变量 **0** 来保持。按照以下步骤解决问题:

*   初始化一个变量，将 **cnt** 设为 **0** 来存储字符串中出现的**0**的个数。
*   初始化变量，将**和**设为 **0** 来计算执行的移除操作的总数。
*   [使用变量 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)、 **S** ，并执行以下步骤:
    *   如果 **S[i]** 的值为 **X** ，则将 **cnt** 的值增加 **1** 。
    *   否则，如果 **cnt** 的值大于 **0** ，则 **cnt** 的值递减，而**和**的值递增 1。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to count the maximum number
// of operations performed on the string
void countOperations(string S)
{
    // Size of the string
    int n = S.length();

    // Stores the maximum number of
    // operations performed
    int ans = 0;

    // Stores the count of 'X' occurred
    // so far
    int cnt = 0;

    // Traverse the string
    for (int i = 0; i < n; i++) {

        // Check if current char
        // is 'X'
        if (S[i] == '0') {
            cnt++;
        }
        else {

            // Check if the value of
            // cnt is greater than 0
            if (cnt > 0) {

                // Decrement the value
                // of cnt
                cnt--;

                // Increment the value
                // of ans
                ans++;
            }
        }
    }

    // Print the value of ans
    cout << ans;
}

// Driver Code
int main()
{
    string S = "110011010";
    countOperations(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

    // Function to count the maximum number
    // of operations performed on the string
    public static void countOperations(String S)
    {

        // Size of the string
        int n = S.length();

        // Stores the maximum number of
        // operations performed
        int ans = 0;

        // Stores the count of 'X' occurred
        // so far
        int cnt = 0;

        // Traverse the string
        for (int i = 0; i < n; i++) {

            // Check if current char
            // is 'X'
            if (S.charAt(i) == '0') {
                cnt++;
            }
            else {

                // Check if the value of
                // cnt is greater than 0
                if (cnt > 0) {

                    // Decrement the value
                    // of cnt
                    cnt--;

                    // Increment the value
                    // of ans
                    ans++;
                }
            }
        }

        // Print the value of ans
        System.out.println(ans);
    }

    // Driver code
    public static void main (String[] args)
    {
        String S = "110011010";
        countOperations(S);
    }
}

// This code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to count the maximum number
# of operations performed on the string
def countOperations(S):
    # Size of the string
    n = len(S)

    # Stores the maximum number of
    # operations performed
    ans = 0

    # Stores the count of 'X' occurred
    # so far
    cnt = 0

    # Traverse the string
    for i in range(n):

        # Check if current char
        # is 'X'
        if (S[i] == '0'):
            cnt+=1
        else:
            # Check if the value of
            # cnt is greater than 0
            if (cnt > 0):

                # Decrement the value
                # of cnt
                cnt-=1

                # Increment the value
                # of ans
                ans+=1

    # Print value of ans
    print (ans)

# Driver Code
if __name__ == '__main__':
    S = "110011010"
    countOperations(S)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to count the maximum number
    // of operations performed on the string
    public static void countOperations(string S)
    {

        // Size of the string
        int n = S.Length;

        // Stores the maximum number of
        // operations performed
        int ans = 0;

        // Stores the count of 'X' occurred
        // so far
        int cnt = 0;

        // Traverse the string
        for (int i = 0; i < n; i++) {

            // Check if current char
            // is 'X'
            if (S[i] == '0') {
                cnt++;
            }
            else {

                // Check if the value of
                // cnt is greater than 0
                if (cnt > 0) {

                    // Decrement the value
                    // of cnt
                    cnt--;

                    // Increment the value
                    // of ans
                    ans++;
                }
            }
        }

        // Print the value of ans
        Console.Write(ans);
    }

    // Driver code
    public static void Main (string[] args)
    {
        string S = "110011010";
        countOperations(S);
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>

        // JavaScript Program for the above approach

        // Function to count the maximum number
        // of operations performed on the string
        function countOperations(S) {
            // Size of the string
            let n = S.length;

            // Stores the maximum number of
            // operations performed
            let ans = 0;

            // Stores the count of 'X' occurred
            // so far
            let cnt = 0;

            // Traverse the string
            for (let i = 0; i < n; i++) {

                // Check if current char
                // is 'X'
                if (S[i] == '0') {
                    cnt++;
                }
                else {

                    // Check if the value of
                    // cnt is greater than 0
                    if (cnt > 0) {

                        // Decrement the value
                        // of cnt
                        cnt--;

                        // Increment the value
                        // of ans
                        ans++;
                    }
                }
            }

            // Print the value of ans
            document.write(ans);
        }

        // Driver Code

        let S = "110011010";
        countOperations(S);

    // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)