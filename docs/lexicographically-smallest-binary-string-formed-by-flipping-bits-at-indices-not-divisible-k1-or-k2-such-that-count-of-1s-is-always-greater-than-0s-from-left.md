# 字典上最小的二进制串，通过在不能被 K1 或 K2 整除的索引处翻转位形成，这样 1 的计数总是从左边大于 0

> 原文:[https://www . geeksforgeeks . org/按字典顺序最小二进制字符串-通过在索引处翻转位形成-不可分-k1-或-k2-这样-从左数 1 的计数总是大于 0/](https://www.geeksforgeeks.org/lexicographically-smallest-binary-string-formed-by-flipping-bits-at-indices-not-divisible-k1-or-k2-such-that-count-of-1s-is-always-greater-than-0s-from-left/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** (基于 1 的索引)和两个正整数 **K1** 和 **K2** ，任务是通过在不能被 **K1** 或 **K2** 整除的索引处翻转字符来找到字典上最小的字符串，使得 **1s** 的[计数一直大于如果不可能形成这样的字符串，打印**-1”**。](https://www.geeksforgeeks.org/count-1s-sorted-binary-array/)

**示例:**

> **输入:** K1 = 4，K2 = 6，S =【0000】
> **输出:** 1110
> **说明:**
> 既然指数 4 可以被 K1 整除(= 4)。因此，在不翻转索引的情况下，字符串会修改为“1110”，这在所有可能的翻转组合中是字典上最小的。
> 
> **输入:** K1 = 2，K2 = 4，S =【11000100】
> **输出:** 11100110

**方法:**对于每个解锁位置，从左到右修改字符串 **S** 即可解决，如果可以使 **0** 则转换为 **0** 否则转换为 **1** 。按照以下步骤解决问题:

*   初始化两个变量 **c1** 和 **c0** 分别存储 **1s** 和 **0s** 的计数。
*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)表示**位置[]** ，该向量存储所有不能被 **K1** 或 **K2** 整除的 **0s** 的位置。
*   [遍历给定的字符串**S**T3】并执行以下步骤:](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)
    *   如果字符为 **0** ，则增加 **c0** 的值。否则，增加 **c1** 的值。
    *   如果当前索引不能被 **K1** 或 **K2** 整除，则在向量**pos【】**中插入该索引。
    *   如果在任何索引 **i** 处， **0s** 的计数变得大于或等于 **1s** 则:
        *   如果[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)为空，则字符串不能修改为所需的组合。于是，打印 **-1** 。
        *   否则，弹出[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中的最后一个**位置，并将 **c0** 的值更新为**c0–1**和 **c1** 为 **c1 + 1** 和**S【pos】= ' 1 '**。**
*   完成上述步骤后，将字符串 **S** 打印为修改后的字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find lexicographically
// smallest string having number of 1s
// greater than number of 0s
void generateString(int k1, int k2, string s)
{
    // C1s And C0s stores the count of
    // 1s and 0s at every position
    int C1s = 0, C0s = 0;
    int flag = 0;
    vector<int> pos;

    // Traverse the string S
    for (int i = 0; i < s.length(); i++) {

        if (s[i] == '0') {
            C0s++;

            // If the position is not
            // divisible by k1 and k2
            if ((i + 1) % k1 != 0
                && (i + 1) % k2 != 0) {
                pos.push_back(i);
            }
        }

        else {
            C1s++;
        }

        if (C0s >= C1s) {

            // If C0s >= C1s and pos[] is
            // empty then the string can't
            // be formed
            if (pos.size() == 0) {
                cout << -1;
                flag = 1;
                break;
            }

            // If pos[] is not empty then
            // flip the bit of last position
            // present in pos[]
            else {
                int k = pos.back();
                s[k] = '1';
                C0s--;
                C1s++;
                pos.pop_back();
            }
        }
    }

    // Print the result
    if (flag == 0) {
        cout << s;
    }
}

// Driver Code
int main()
{
    int K1 = 2, K2 = 4;
    string S = "11000100";
    generateString(K1, K2, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Function to find lexicographically
// smallest String having number of 1s
// greater than number of 0s
static void generateString(int k1, int k2, char[] s)
{

    // C1s And C0s stores the count of
    // 1s and 0s at every position
    int C1s = 0, C0s = 0;
    int flag = 0;
    Vector<Integer> pos = new Vector<Integer>();

    // Traverse the String S
    for (int i = 0; i < s.length; i++) {

        if (s[i] == '0') {
            C0s++;

            // If the position is not
            // divisible by k1 and k2
            if ((i + 1) % k1 != 0
                && (i + 1) % k2 != 0) {
                pos.add(i);
            }
        }

        else {
            C1s++;
        }

        if (C0s >= C1s) {

            // If C0s >= C1s and pos[] is
            // empty then the String can't
            // be formed
            if (pos.size() == 0) {
                System.out.print(-1);
                flag = 1;
                break;
            }

            // If pos[] is not empty then
            // flip the bit of last position
            // present in pos[]
            else {
                int k = pos.get(pos.size()-1);
                s[k] = '1';
                C0s--;
                C1s++;
                pos.remove(pos.size() - 1);
            }
        }
    }

    // Print the result
    if (flag == 0) {
        System.out.print(s);
    }
}

// Driver Code
public static void main(String[] args)
{
    int K1 = 2, K2 = 4;
    String S = "11000100";
    generateString(K1, K2, S.toCharArray());

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find lexicographically
# smallest string having number of 1s
# greater than number of 0s
def generateString(k1, k2, s):

    # C1s And C0s stores the count of
    # 1s and 0s at every position
    s = list(s)
    C1s = 0
    C0s = 0
    flag = 0
    pos = []

    # Traverse the string S
    for i in range(len(s)):
        if (s[i] == '0'):
            C0s += 1

            # If the position is not
            # divisible by k1 and k2
            if ((i + 1) % k1 != 0 and (i + 1) % k2 != 0):
                pos.append(i)

        else:
            C1s += 1

        if (C0s >= C1s):
            # If C0s >= C1s and pos[] is
            # empty then the string can't
            # be formed
            if (len(pos) == 0):
                print(-1)
                flag = 1
                break

            # If pos[] is not empty then
            # flip the bit of last position
            # present in pos[]
            else:
                k = pos[len(pos)-1]
                s[k] = '1'
                C0s -= 1
                C1s += 1
                pos = pos[:-1]

    # Print the result
    s = ''.join(s)
    if (flag == 0):
        print(s)

# Driver Code
if __name__ == '__main__':
    K1 = 2
    K2 = 4
    S = "11000100"
    generateString(K1, K2, S)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

// Function to find lexicographically
// smallest String having number of 1s
// greater than number of 0s
static void generateString(int k1, int k2, char[] s)
{

    // C1s And C0s stores the count of
    // 1s and 0s at every position
    int C1s = 0, C0s = 0;
    int flag = 0;
    List<int> pos = new List<int>();

    // Traverse the String S
    for (int i = 0; i < s.Length; i++) {

        if (s[i] == '0') {
            C0s++;

            // If the position is not
            // divisible by k1 and k2
            if ((i + 1) % k1 != 0
                && (i + 1) % k2 != 0) {
                pos.Add(i);
            }
        }

        else {
            C1s++;
        }

        if (C0s >= C1s) {

            // If C0s >= C1s and pos[] is
            // empty then the String can't
            // be formed
            if (pos.Count == 0) {
                Console.WriteLine(-1);
                flag = 1;
                break;
            }

            // If pos[] is not empty then
            // flip the bit of last position
            // present in pos[]
            else {
                int k = pos[(pos.Count - 1)];
                s[k] = '1';
                C0s--;
                C1s++;
                pos.Remove(pos.Count - 1);
            }
        }
    }

    // Print the result
    if (flag == 0) {
        Console.WriteLine(s);
    }
}

    // Driver Code
    public static void Main()
    {
    int K1 = 2, K2 = 4;
    string S = "11000100";
    generateString(K1, K2, S.ToCharArray());
    }
}

// This code is contributed by avijitmondal1998.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find lexicographically
        // smallest string having number of 1s
        // greater than number of 0s
        function generateString(k1, k2, s)
        {

            // C1s And C0s stores the count of
            // 1s and 0s at every position
            let C1s = 0, C0s = 0;
            let flag = 0;
            let pos = [];

            // Traverse the string S
            for (let i = 0; i < s.length; i++) {

                if (s[i] == '0') {
                    C0s++;

                    // If the position is not
                    // divisible by k1 and k2
                    if ((i + 1) % k1 != 0
                        && (i + 1) % k2 != 0) {
                        pos.push(i);
                    }
                }

                else {
                    C1s++;
                }

                if (C0s >= C1s) {

                    // If C0s >= C1s and pos[] is
                    // empty then the string can't
                    // be formed
                    if (pos.length == 0) {
                        cout << -1;
                        flag = 1;
                        break;
                    }

                    // If pos[] is not empty then
                    // flip the bit of last position
                    // present in pos[]
                    else {
                        let k = pos[pos.length - 1];
                        var ns = s.replace(s[k], '1');
                        C0s--;
                        C1s++;
                        pos.pop();
                    }
                }
            }

            // Print the result
            if (flag == 0) {
                document.write(ns);
            }
        }

        // Driver Code
        let K1 = 2, K2 = 4;
        let S = "11000100";
        generateString(K1, K2, S);

// This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
11100110
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)