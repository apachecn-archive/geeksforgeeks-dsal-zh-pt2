# 给定数值串中最小非素数子序列的长度

> 原文:[https://www . geesforgeks . org/给定数字字符串中最小非素数子序列的长度/](https://www.geeksforgeeks.org/length-of-smallest-non-prime-subsequence-in-given-numeric-string/)

给定一个由数字**【1，9】**组成的大小为 **N** 的[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** ，任务是找到字符串中最小[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，使其成为[而不是质数](https://www.geeksforgeeks.org/python-program-to-check-whether-a-number-is-prime-or-not/)。

**示例:**

> **输入:** S = "237"
> **输出:** 2
> **说明:**
> 有 7 个非空子序列{“2”、“3”、“7”、“23”、“27”、“37”、“237”}。在这些子序列中，有两个子序列不是素数，即 27 和 237。因此，as 27 的长度为 2。所以打印 2。
> 
> **输入:**S = " 44444 "
> T3】输出: 1

**方法:**解决这个问题的思路是基于这样的观察:如果在从字符串 **S** 中删除 **j** 或大于 **j** 的字符时，该字符串是一个[素数](https://www.geeksforgeeks.org/prime-numbers/)，那么答案应该大于 **j** 。基于这个事实，形成所有的字符串，这样从该字符串中删除元素就得到一个质数。以上直觉所有可能的字符串都是 **{2，3，5，7，23，37，53，73}** 因此子序列最大可能的大小是 **3** 。因此，想法是遍历大小为 **1** 和大小为 **2** 的所有子序列，如果发现子序列包含至少一个元素**，该元素在列表中不存在[，则大小可能是 **1** 或 **2** 。否则尺寸为 **3** 。按照以下步骤解决问题:](https://www.geeksforgeeks.org/check-if-element-exists-in-list-in-python/)**

*   **初始化布尔变量**标志**为**假。****
*   **初始化一个空字符串**哑元。****
*   **[使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，N)** ，并执行以下任务:

    *   如果 **j-th** 位置的字符不等于 **2** 或 **3** 或 **5** 或 **7、**，则将答案打印为 **1、**将**标志**的值设置为**真**并断开。** 
*   **如果**标志**为**真**，则返回否则执行以下任务。**
*   **[使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，N)** ，并执行以下任务:

    *   [使用变量 **j1** 迭代范围](https://www.geeksforgeeks.org/loops-in-java/)**【j+1，N)** ，并执行以下任务:
        *   在 **j** 和 **j1** 位置建立一个带字符的伪字符串。
        *   如果虚设串不等于 **2、3、5、7、23、37、53、**和 **73** ，则打印答案为 **2** ，并将**标志**的值设置为**真**[断](https://www.geeksforgeeks.org/break-statement-in-java/)。** 
*   **如果**标志**为**假**且字符串 **S** 长度大于等于 **3** ，则打印 **3** 作为答案否则打印 **-1** 。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest
// length of resultant subsequence
void findMinimumSubsequence(
    string S)
{
    bool flag = false;
    string dummy;

    // Check for a subsequence of size 1
    for (int j = 0; j < S.length(); j++)
    {
        if (S[j] != '2' && S[j] != '3' && S[j] != '5' && S[j] != '7')
        {
            cout << 1;
            flag = true;
            break;
        }
    }

    // Check for a subsequence of size 2

    if (!flag)
    {

        for (int j = 0;
             j < S.length() - 1; j++)
        {

            for (int j1 = j + 1;
                 j1 < S.length(); j1++)
            {

                dummy = S[j] + S[j1];

                if (dummy != "23" && dummy != "37" && dummy != "53" && dummy != "73")
                {
                    cout << 2;
                }
                if (flag = true)
                    break;
            }
            if (flag = true)
                break;
        }
    }

    // If none of the above check is
    // successful then subsequence
    // must be of size 3

    if (!flag)
    {
        if (S.length() >= 3)
        {

            // Never executed
            cout << 3;
        }
        else
        {
            cout << -1;
        }
    }
}

// Driver Code
int main()
{
    string S = "237";
    findMinimumSubsequence(S);
    return 0;
}

// This code is contributed by Potta Lokesh
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach

import java.io.*;

class GFG {

    // Function to find the smallest
    // length of resultant subsequence
    public static void findMinimumSubsequence(
        String S)
    {
        boolean flag = false;
        StringBuilder dummy = new StringBuilder();

        // Check for a subsequence of size 1
        for (int j = 0; j < S.length(); j++) {
            if (S.charAt(j) != '2' && S.charAt(j) != '3'
                && S.charAt(j) != '5'
                && S.charAt(j) != '7') {
                System.out.println(1);
                flag = true;
                break;
            }
        }

        // Check for a subsequence of size 2
        if (!flag) {
        loop:
            for (int j = 0;
                 j < S.length() - 1; j++) {

                for (int j1 = j + 1;
                     j1 < S.length(); j1++) {

                    dummy = new StringBuilder(
                        Character.toString(S.charAt(j)));
                    dummy.append(S.charAt(j1));

                    if (!dummy.toString().equals("23")
                        && !dummy.toString().equals("37")
                        && !dummy.toString().equals("53")
                        && !dummy.toString().equals("73")) {
                        System.out.println(2);
                        flag = true;
                        break loop;
                    }
                }
            }
        }

        // If none of the above check is
        // successful then subsequence
        // must be of size 3
        if (!flag) {
            if (S.length() >= 3) {

                // Never executed
                System.out.println(3);
            }
            else {
                System.out.println(-1);
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S = "237";
        findMinimumSubsequence(S);
    }
}
```

## **C#**

```
// C# program for the above approach
using System;
class GFG
{

    // Function to find the smallest
    // length of resultant subsequence
    static void findMinimumSubsequence(string S)
    {
        bool flag = false;
        string dummy = "";

        // Check for a subsequence of size 1
        for (int j = 0; j < S.Length; j++) {
            if (S[j] != '2' && S[j] != '3' && S[j] != '5'
                && S[j] != '7') {
                Console.WriteLine(1);
                flag = true;
                break;
            }
        }

        // Check for a subsequence of size 2
        if (!flag) {

            for (int j = 0; j < S.Length - 1; j++) {

                for (int j1 = j + 1; j1 < S.Length; j1++) {

                    dummy = S[j].ToString()
                            + S[j1].ToString();

                    if (dummy != "23" && dummy != "37"
                        && dummy != "53" && dummy != "73") {
                        Console.WriteLine(2);
                    }
                    if (flag == true)
                        break;
                    else
                        flag = true;
                }
                if (flag == true)
                    break;
            }
        }

        // If none of the above check is
        // successful then subsequence
        // must be of size 3

        if (flag == false) {
            if (S.Length >= 3) {

                // Never executed
                Console.WriteLine(3);
            }
            else {
                Console.WriteLine(-1);
            }
        }
    }

    // Driver Code
    public static void Main()
    {
        string S = "237";
        findMinimumSubsequence(S);
    }
}

// This code is contributed by ukasp.
```

## **蟒蛇 3**

```
# Python 3 program for the above approach

# Function to find the smallest
# length of resultant subsequence
def findMinimumSubsequence(S):
    flag = False
    dummy = ''

    # Check for a subsequence of size 1
    for j in range(len(S)):
        if (S[j] != '2' and S[j] != '3' and S[j] != '5' and S[j] != '7'):
            print(1)
            flag = True
            break

    # Check for a subsequence of size 2
    if (flag == False):
        for j in range(len(S)):
            for j1 in range(j + 1,len(S),1):
                dummy = S[j] + S[j1]

                if (dummy != "23" and dummy != "37" and dummy != "53" and dummy != "73"):
                    print(2)
                if (flag == True):
                    break
                else:
                    flag = True

            if (flag == True):
                break

    # If none of the above check is
    # successful then subsequence
    # must be of size 3
    if (flag == False):
        if (len(S) >= 3):
            # Never executed
            print(3)
        else:
            print(-1)

# Driver Code
if __name__ == '__main__':
    S = "237"
    findMinimumSubsequence(S)

    # This code is contributed by ipg2016107.
```

## **java 描述语言**

```
<script>   
// JavaScript program for the above approach

// Function to find the smallest
// length of resultant subsequence
function findMinimumSubsequence(S)
{
    let flag = false;

    // Check for a subsequence of size 1
    for (let j = 0; j < S.length; j++)
    {
        if (S[j] != '2' && S[j] != '3' && S[j] != '5' && S[j] != '7')
        {
            document.write(1);
            flag = true;
            break;
        }
    }

    // Check for a subsequence of size 2
    if (flag == false)
    {
        for (let j = 0; j < S.length; j++)
        {
            for (let j1 = j + 1; j1 < S.length; j1++)
            {
                let dummy = S[j] + S[j1];
                if (dummy != "23" && dummy != "37" && dummy != "53" && dummy != "73")
                {
                    document.write(2);
                }
                if (flag == true)
                    break;
                else
                    flag = true;
            }
            if (flag == true)
                break;
        }
    }

    // If none of the above check is
    // successful then subsequence
    // must be of size 3
    if (flag == false)
    {
        if (S.length >= 3)
        {

            // Never executed
           document.write(3);
        }
        else
        {
            document.write(-1);
        }
    }
}

// Driver Code
    let S = "237";
    findMinimumSubsequence(S);

// This code is contributed by AnkThon
</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)***