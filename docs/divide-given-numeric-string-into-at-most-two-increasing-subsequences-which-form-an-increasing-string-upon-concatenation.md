# 将给定的数字串分成至多两个递增的子序列，通过连接形成递增的串

> 原文:[https://www . geeksforgeeks . org/将给定的数字串分成最多两个递增子序列，这些子序列在串联时形成递增串/](https://www.geeksforgeeks.org/divide-given-numeric-string-into-at-most-two-increasing-subsequences-which-form-an-increasing-string-upon-concatenation/)

给定由 **N** 个数字组成的[串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是将该串分成至多两个递增的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，使得它们的串联也形成递增的串。如果不可能，则打印**-1”**。

**示例:**

> **输入:**S =【040425524644】
> T3】输出: 0022444 44556
> **解释:**
> 分割给定字符串 S 的可能方式之一是{“0022444”、“44556”}。两者的顺序都是递增的，它们的串联也是递增的“0022444”+“4556”=“00224444556”。
> 因此，打印形成的两个子序列。
> 
> **输入:**S = " 123456789 "
> T3】输出: 123456789

**天真法:**解决问题最简单的方法是[生成所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，检查任意两个不重叠的子序列是否满足给定条件。如果发现**为真**，则打印两个子序列。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过将所有小于 **X** 的值放在第一个子序列中，所有大于 **X** 的元素放在第二个子序列中，所有等于 **X** 的元素根据它们在**【0，9】**范围内的所有 **X** 的位置来决定。按照以下步骤解决问题:

*   初始化一个变量，比如说， **pos** 存储第一个子序列中小于 **pos** 的位置，大于第二个子序列中的 **pos** 的位置，等于 **pos** 的元素将基于它们的位置在子序列中。
*   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **res[]** ，它将存储哪个元素属于哪个子序列。
*   [在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，9】**中迭代**位置**，并执行以下步骤:
    1.  将两个变量 **last1** 初始化为 **0** ，将 **last2** 初始化为 **pos** ，分别存储已经放入子序列 1 和 2 的最后一个元素。
    2.  初始化一个布尔变量**标志**为 **1** ，存储处理后的子序列是否有效。
    3.  [使用 **i** 作为变量，在](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**范围内迭代，并执行以下步骤:
        *   如果 **last2 ≤ S[i]** ，则将 **last2** 的值修改为 **S[i]** ，将 **res[i]** 修改为 **2** 。
        *   否则如果 **last1 ≤ S[i]** ，则将 **last1** 的值修改为 **S[i]** ，将 **res[i]** 修改为 **1** 。
        *   否则，将**标志**的值修改为 **0** 。
    4.  检查最后一个**的值是否大于**位置**，然后将**标志**的值修改为 **0** 。**
    5.  如果**标志**的值为 **1** ，则[打印数组](https://www.geeksforgeeks.org/how-to-print-an-array-in-java-without-using-loop/) **res** 作为答案，[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，如果没有找到可能的子序列，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check for valid subsequences
void findSubsequence(string str)
{
    int n = str.size();

    // Stores which element belongs to
    // which subsequence
    char res[n];
    for (int i = 0; i < n; i++)
        res[i] = 0;

    // Check for each pos if a possible
    // subsequence exist or not
    for (int pos = 0; pos <= 9; pos++) {

        // Last member of 1 subsequence
        char lst1 = '0';
        bool flag = 1;

        // Last Member of 2nd subsequence
        char lst2 = pos + '0';
        for (int i = 0; i < n; i++) {

            // Check if current element can
            // go to 2nd subsequence
            if (lst2 <= str[i]) {
                res[i] = '2';
                lst2 = str[i];
            }

            // Check if the current elements
            // belongs to first subsequence
            else if (lst1 <= str[i]) {
                res[i] = '1';
                lst1 = str[i];
            }

            // If the current element does
            // not belong to any subsequence
            else
                flag = 0;
        }

        // Check if last digit of first
        // subsequence is greater than pos
        if (lst1 > pos + '0')
            flag = 0;

        // If a subsequence is found,
        // find the subsequences
        if (flag) {

            // Stores the resulting
            // subsequences
            string S1 = "";
            string S2 = "";

            for (int i = 0; i < n; i++) {

                if (res[i] == '1') {
                    S1 += str[i];
                }
                else {
                    S2 += str[i];
                }
            }

            // Print the subsequence
            cout << S1 << ' ' << S2 << endl;
            return;
        }
    }

    // If no subsequence found, print -1
    cout << "-1";
}

// Driver Code
int main()
{
    string S = "040425524644";
    findSubsequence(S);

    S = "123456789";
    findSubsequence(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to check for valid subsequences
static void findSubsequence(String str)
{
    int n = str.length();

    // Stores which element belongs to
    // which subsequence
    char []res = new char[n];
    for (int i = 0; i < n; i++)
        res[i] = 0;

    // Check for each pos if a possible
    // subsequence exist or not
    for (int pos = 0; pos <= 9; pos++) {

        // Last member of 1 subsequence
        char lst1 = '0';
        boolean flag = true;

        // Last Member of 2nd subsequence
        char lst2 = (char) (pos + '0');
        for (int i = 0; i < n; i++) {

            // Check if current element can
            // go to 2nd subsequence
            if (lst2 <= str.charAt(i)) {
                res[i] = '2';
                lst2 = str.charAt(i);
            }

            // Check if the current elements
            // belongs to first subsequence
            else if (lst1 <= str.charAt(i)) {
                res[i] = '1';
                lst1 = str.charAt(i);
            }

            // If the current element does
            // not belong to any subsequence
            else
                flag = false;
        }

        // Check if last digit of first
        // subsequence is greater than pos
        if (lst1 > pos + '0')
            flag = false;

        // If a subsequence is found,
        // find the subsequences
        if (flag) {

            // Stores the resulting
            // subsequences
            String S1 = "";
            String S2 = "";

            for (int i = 0; i < n; i++) {

                if (res[i] == '1') {
                    S1 += str.charAt(i);
                }
                else {
                    S2 += str.charAt(i);
                }
            }

            // Print the subsequence
            System.out.print(S1 + " " + S2 +"\n");
            return;
        }
    }

    // If no subsequence found, print -1
    System.out.print("-1");
}

// Driver Code
public static void main(String[] args)
{
    String S = "040425524644";
    findSubsequence(S);

    S = "123456789";
    findSubsequence(S);

}
}

// This code is contributed by 29AjayKumar.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to check for valid subsequences
def findSubsequence(str):
    n = len(str)

    # Stores which element belongs to
    # which subsequence
    res = ['0' for i in range(n)]

    # Check for each pos if a possible
    # subsequence exist or not
    for pos in range(10):

        # Last member of 1 subsequence
        lst1 = '0'
        flag = 1

        # Last Member of 2nd subsequence
        lst2 = chr(pos + 48)
        for i in range(n):

            # Check if current element can
            # go to 2nd subsequence
            if (lst2 <= str[i]):
                res[i] = '2'
                lst2 = str[i]

            # Check if the current elements
            # belongs to first subsequence
            elif(lst1 <= str[i]):
                res[i] = '1'
                lst1 = str[i]

            # If the current element does
            # not belong to any subsequence
            else:
                flag = 0

        # Check if last digit of first
        # subsequence is greater than pos
        if (lst1 >  chr(pos + 48)):
            flag = 0

        # If a subsequence is found,
        # find the subsequences
        if (flag):

            # Stores the resulting
            # subsequences
            S1 = ""
            S2 = ""

            for i in range(n):
                if (res[i] == '1'):
                    S1 += str[i]
                else:
                    S2 += str[i]

            # Print the subsequence
            print(S1,S2)
            return

    # If no subsequence found, print -1
    print("-1")

# Driver Code
if __name__ == '__main__':
    S = "040425524644"
    findSubsequence(S)

    S = "123456789"
    findSubsequence(S)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the approach
using System;
using System.Collections.Generic;

class GFG {

// Function to check for valid subsequences
static void findSubsequence(string str)
{
    int n = str.Length;

    // Stores which element belongs to
    // which subsequence
    char[] res = new char[n];
    for (int i = 0; i < n; i++)
        res[i] = '0';

    // Check for each pos if a possible
    // subsequence exist or not
    for (int pos = 0; pos <= 9; pos++) {

        // Last member of 1 subsequence
        char lst1 = '0';
        bool flag = true;

        // Last Member of 2nd subsequence
        char lst2 = (char) (pos + '0');
        for (int i = 0; i < n; i++) {

            // Check if current element can
            // go to 2nd subsequence
            if (lst2 <= str[i]) {
                res[i] = '2';
                lst2 = str[i];
            }

            // Check if the current elements
            // belongs to first subsequence
            else if (lst1 <= str[i]) {
                res[i] = '1';
                lst1 = str[i];
            }

            // If the current element does
            // not belong to any subsequence
            else
                flag = false;
        }

        // Check if last digit of first
        // subsequence is greater than pos
        if (lst1 > pos + '0')
            flag = false;

        // If a subsequence is found,
        // find the subsequences
        if (flag) {

            // Stores the resulting
            // subsequences
            string S1 = "";
            string S2 = "";

            for (int i = 0; i < n; i++) {

                if (res[i] == '1') {
                    S1 += str[i];
                }
                else {
                    S2 += str[i];
                }
            }

            // Print the subsequence
            Console.WriteLine(S1 + ' ' + S2);
            return;
        }
    }

    // If no subsequence found, print -1
    Console.Write("-1");
}

    // Driver Code
    public static void Main()
    {
        string S = "040425524644";
        findSubsequence(S);

        S = "123456789";
        findSubsequence(S);
    }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to check for valid subsequences
        function findSubsequence(str) {
            let n = str.length;

            // Stores which element belongs to
            // which subsequence
            let res = new Array(n);
            for (let i = 0; i < n; i++)
                res[i] = 0;

            // Check for each pos if a possible
            // subsequence exist or not
            for (let pos = 0; pos <= 9; pos++) {

                // Last member of 1 subsequence
                let lst1 = '0';
                let flag = 1;

                // Last Member of 2nd subsequence
                let lst2 = String.fromCharCode(pos + '0'.charCodeAt(0));
                for (let i = 0; i < n; i++) {

                    // Check if current element can
                    // go to 2nd subsequence
                    if (lst2.charCodeAt(0) <= str[i].charCodeAt(0)) {
                        res[i] = '2';
                        lst2 = str[i];
                    }

                    // Check if the current elements
                    // belongs to first subsequence
                    else if (lst1.charCodeAt(0) <= str[i].charCodeAt(0)) {
                        res[i] = '1';
                        lst1 = str[i];
                    }

                    // If the current element does
                    // not belong to any subsequence
                    else
                        flag = 0;
                }

                // Check if last digit of first
                // subsequence is greater than pos
                if (lst1.charCodeAt(0) > pos + '0'.charCodeAt(0)) {
                    flag = 0;
                }

                // If a subsequence is found,
                // find the subsequences
                if (flag) {

                    // Stores the resulting
                    // subsequences
                    let S1 = "";
                    let S2 = "";

                    for (let i = 0; i < n; i++) {

                        if (res[i] == '1') {
                            S1 += str[i];
                        }
                        else {
                            S2 += str[i];
                        }
                    }

                    // Print the subsequence
                    document.write(S1 + ' ' + S2 + '<br>');
                    return;
                }
            }

            // If no subsequence found, print -1
            document.write("-1");
        }

        // Driver Code

        let S = "040425524644";
        findSubsequence(S);

        S = "123456789";
        findSubsequence(S);

// This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
0022444 44556 
123456789
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)