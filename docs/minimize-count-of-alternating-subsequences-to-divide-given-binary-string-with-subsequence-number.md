# 最小化交替子序列的计数，用子序列数来划分给定的二进制串

> 原文:[https://www . geeksforgeeks . org/最小化给定二进制字符串与子序列数的交替子序列数/](https://www.geeksforgeeks.org/minimize-count-of-alternating-subsequences-to-divide-given-binary-string-with-subsequence-number/)

给定一个长度为 **N** 的二进制字符串 **S** 。任务是找到以下内容:

*   子序列的最小数目，字符串 **S** 可以分成，这样子序列就不包含相邻的 0 或 1。
*   字符串 **S** 的每个字符所属的子序列编号。

如果答案很多，输出任意一个。

**示例:**

> ***输入:** S = "0011 "，N = 4*
> ***输出:***
> *2*
> *1 2 2 1*
> ***解释:***
> *至少可以有 2 个子序列，这样它们就没有任何相邻的 0 或 1。*
> *子序列 1:“01”*
> *子序列 2:“01”*
> *同样，S 的第一个字符(‘0’)属于子序列 1(“01”)*
> *S 的第二个字符(‘0’)属于子序列 2(“01”)*
> *S 的第三个字符(‘1’)属于子序列 2(“01”)*
> 
> ****输入:S =【1000110】，N = 7***
> ***输出:***
> *3*
> 1 1 2 3 2 2*

***方法:**需要注意的是,[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)是一个序列，可以通过删除零个或多个元素而不改变剩余元素的顺序，从给定的序列中导出。现在，按照以下步骤解决问题:*

1.  *创建一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **和**来存储字符串**的每个字符**所属的子序列。*
2.  *另外，创建两个向量 **endZero** 和 **endOne** 来存储分别以**“0”**和**“1”**结尾的子序列。*
3.  *因为子序列中不能有相邻的 0 或 1。因此，如果一个字符是**‘0’**，下一个要放入子序列的字符必须是**‘1’**，反之亦然。*
4.  *现在，使用循环遍历 **S** 的每个字符，检查它是**“0”**还是**“1”**。此外，声明一个变量 **newSeq** ，它表示如果遇到连续的 0 或 1 将形成的新子序列。*
5.  *如果一个字符是**‘0’**，检查向量 **endOne** 是否为空:

    *   如果是空的，那么将**新 eq** 推入 **endZero** 。
    *   否则，将 **endOne** 的最后一个子序列放入 **newSeq** 中。现在， **endOne** 的最后一个子序列不再以**“1”**结束，因为**“0”**已经被附加到它上面。因此，将其推入**端零**。* 
6.  *同样，如果 **S** 中的一个字符是**‘1’**，则按照上述步骤进行，即检查向量 **endZero** 是否为空:

    *   如果是空的，则将**新 eq** 推入**内**。
    *   否则，将 **endZero** 的最后一个子序列放入 **newSeq** 中。现在， **endZero** 的最后一个子序列不再以**“0”**结束，因为**“1”**已经被附加到它上面。这样，将其推入**内**。* 
7.  *然后，将**neweq**推入矢量 **ans** 。*
8.  *对 **S** 的每个字符重复上述步骤。*
9.  *子序列的最小数量将由 **endZero** 和 **endOne** 的大小之和给出。*
10.  *最后，输出最小数量的子序列和向量**和**。*

*下面是上述方法的实现:*

## *C++*

```
*// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// subsequences into which S has to divide
// and the subsequences to which each character
// of S belongs to.
void findSeq(string S, int N)
{
    // Stores the subsequences to which each
    // character of S belongs to.
    vector<int> ans(N);

    // Store the subsequences ending with zeroes
    // and ones respectively.
    vector<int> endZero, endOne;

    // Loop to traverse each character of S
    for (int i = 0; i < N; ++i) {

        // Stores the number of new
        // subsequence to be formed
        int newSeq = endZero.size()
                     + endOne.size();

        // If the character is '0'
        if (S[i] == '0') {

            // If there is no string
            // which ends with '1'
            if (endOne.empty()) {

                // Push newSeq into endZero
                endZero.push_back(newSeq);
            }
            else {

                // Put the last element
                // of endOne into newSeq
                newSeq = endOne.back();

                // Remove the last
                // element of endOne
                endOne.pop_back();

                // newSeq ends with '0'
                endZero.push_back(newSeq);
            }
        }
        else {

            // If there is no string
            // which ends with '0'
            if (endZero.empty()) {

                // Push newSeq into endOne
                endOne.push_back(newSeq);
            }
            else {

                // Put the last element
                // of endZero into newSeq
                newSeq = endZero.back();

                // Remove the last element of endOne
                endZero.pop_back();

                // newSeq ends with '1'
                endOne.push_back(newSeq);
            }
        }

        // Put newSeq into vector ans
        ans[i] = newSeq;
    }

    // Output the minimum
    // number of subsequences
    cout << endZero.size()
                + endOne.size()
         << endl;

    // Output the subsequences
    // to which each character
    // of S belongs to
    for (int i = 0; i < N; ++i) {

        // Add 1 as the index starts from 0
        cout << ans[i] + 1 << " ";
    }
}

// Driver Code
int main()
{

    // Given input
    string S = "1000110";
    int N = 7;

    // Function Call
    findSeq(S, N);

    return 0;
}*
```

## *Java 语言(一种计算机语言，尤用于创建网站)*

```
*// Java program for the above approach
import java.util.ArrayList;

class GFG {

    // Function to find the minimum number of
    // subsequences into which S has to divide
    // and the subsequences to which each character
    // of S belongs to.
    public static void findSeq(String S, int N)
    {

        // Stores the subsequences to which each
        // character of S belongs to.
        int[] ans = new int[N];

        // Store the subsequences ending with zeroes
        // and ones respectively.
        ArrayList<Integer> endZero = new ArrayList<Integer>();
        ArrayList<Integer> endOne = new ArrayList<Integer>();

        // Loop to traverse each character of S
        for (int i = 0; i < N; ++i) {

            // Stores the number of new
            // subsequence to be formed
            int newSeq = endZero.size() + endOne.size();

            // If the character is '0'
            if (S.charAt(i) == '0') {

                // If there is no string
                // which ends with '1'
                if (endOne.isEmpty()) {

                    // Push newSeq into endZero
                    endZero.add(newSeq);
                } else {

                    // Put the last element
                    // of endOne into newSeq
                    newSeq = endOne.get(endOne.size() - 1);

                    // Remove the last
                    // element of endOne
                    endOne.remove(endOne.size() - 1);

                    // newSeq ends with '0'
                    endZero.add(newSeq);
                }
            } else {

                // If there is no string
                // which ends with '0'
                if (endZero.isEmpty()) {

                    // Push newSeq into endOne
                    endOne.add(newSeq);
                } else {

                    // Put the last element
                    // of endZero into newSeq
                    newSeq = endZero.get(endZero.size() - 1);

                    // Remove the last element of endOne
                    endZero.remove(endZero.size() - 1);

                    // newSeq ends with '1'
                    endOne.add(newSeq);
                }
            }

            // Put newSeq into vector ans
            ans[i] = newSeq;
        }

        // Output the minimum
        // number of subsequences
        System.out.println(endZero.size() + endOne.size());

        // Output the subsequences
        // to which each character
        // of S belongs to
        for (int i = 0; i < N; ++i) {

            // Add 1 as the index starts from 0
            System.out.print(ans[i] + 1 + " ");
        }
    }

    // Driver Code
    public static void main(String args[]) {

        // Given input
        String S = "1000110";
        int N = 7;

        // Function Call
        findSeq(S, N);

    }
}

// This code is contributed by gfgking.*
```

## *蟒蛇 3*

```
*# python program for the above approach

# Function to find the minimum number of
# subsequences into which S has to divide
# and the subsequences to which each character
# of S belongs to.
def findSeq(S, N):

    # Stores the subsequences to which each
    # character of S belongs to.
    ans = [0 for _ in range(N)]

    # Store the subsequences ending with zeroes
    # and ones respectively.
    endZero = []
    endOne = []

    # Loop to traverse each character of S
    for i in range(0, N):

         # Stores the number of new
         # subsequence to be formed
        newSeq = len(endZero) + len(endOne)

        # If the character is '0'
        if (S[i] == '0'):

             # If there is no string
             # which ends with '1'
            if (len(endOne) == 0):

                # Push newSeq into endZero
                endZero.append(newSeq)

            else:

               # Put the last element
                # of endOne into newSeq
                newSeq = endOne[len(endOne) - 1]

                # Remove the last
                # element of endOne
                endOne.pop()

                # newSeq ends with '0'
                endZero.append(newSeq)

        else:

            # If there is no string
            # which ends with '0'
            if (len(endZero) == 0):

                # Push newSeq into endOne
                endOne.append(newSeq)

            else:

                 # Put the last element
                # of endZero into newSeq
                newSeq = endZero[len(endZero) - 1]

                # Remove the last element of endOne
                endZero.pop()

                # newSeq ends with '1'
                endOne.append(newSeq)

                # Put newSeq into vector ans
        ans[i] = newSeq

        # Output the minimum
        # number of subsequences
    print(len(endZero) + len(endOne))

    # Output the subsequences
    # to which each character
    # of S belongs to
    for i in range(0, N):

        # Add 1 as the index starts from 0
        print(ans[i] + 1, end=" ")

# Driver Code
if __name__ == "__main__":

        # Given input
    S = "1000110"
    N = 7

    # Function Call
    findSeq(S, N)

    # This code is contributed by rakeshsahni*
```

## *C#*

```
*// C# program for the above approach

using System;
using System.Collections.Generic;
class GFG
{

    // Function to find the minimum number of
    // subsequences into which S has to divide
    // and the subsequences to which each character
    // of S belongs to.
    public static void findSeq(String S, int N)
    {

        // Stores the subsequences to which each
        // character of S belongs to.
        int[] ans = new int[N];

        // Store the subsequences ending with zeroes
        // and ones respectively.
        List<int> endZero = new List<int>();
        List<int> endOne = new List<int>();

        // Loop to traverse each character of S
        for (int i = 0; i < N; ++i)
        {

            // Stores the number of new
            // subsequence to be formed
            int newSeq = endZero.Count + endOne.Count;

            // If the character is '0'
            if (S[i] == '0')
            {

                // If there is no string
                // which ends with '1'
                if (endOne.Count == 0)
                {

                    // Push newSeq into endZero
                    endZero.Add(newSeq);
                }
                else
                {

                    // Put the last element
                    // of endOne into newSeq
                    newSeq = endOne[endOne.Count - 1];

                    // Remove the last
                    // element of endOne
                    endOne.Remove(endOne.Count - 1);

                    // newSeq ends with '0'
                    endZero.Add(newSeq);
                }
            }
            else
            {

                // If there is no string
                // which ends with '0'
                if (endZero.Count == 0)
                {

                    // Push newSeq into endOne
                    endOne.Add(newSeq);
                }
                else
                {

                    // Put the last element
                    // of endZero into newSeq
                    newSeq = endZero[endZero.Count - 1];

                    // Remove the last element of endOne
                    endZero.Remove(endZero.Count - 1);

                    // newSeq ends with '1'
                    endOne.Add(newSeq);
                }
            }

            // Put newSeq into vector ans
            ans[i] = newSeq;
        }

        // Output the minimum
        // number of subsequences
        Console.WriteLine(endZero.Count + endOne.Count);

        // Output the subsequences
        // to which each character
        // of S belongs to
        for (int i = 0; i < N; ++i)
        {

            // Add 1 as the index starts from 0
            Console.Write(ans[i] + 1 + " ");
        }
    }

    // Driver Code
    public static void Main()
    {

        // Given input
        String S = "1000110";
        int N = 7;

        // Function Call
        findSeq(S, N);

    }
}

// This code is contributed by gfgking.*
```

## *java 描述语言*

```
*<script>

        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum number of
        // subsequences into which S has to divide
        // and the subsequences to which each character
        // of S belongs to.
        function findSeq(S, N)
        {

            // Stores the subsequences to which each
            // character of S belongs to.
            let ans = new Array(N);

            // Store the subsequences ending with zeroes
            // and ones respectively.
            let endZero = [], endOne = [];

            // Loop to traverse each character of S
            for (let i = 0; i < N; ++i) {

                // Stores the number of new
                // subsequence to be formed
                let newSeq = endZero.length
                    + endOne.length;

                // If the character is '0'
                if (S[i] == '0') {

                    // If there is no string
                    // which ends with '1'
                    if (endOne.length == 0) {

                        // Push newSeq into endZero
                        endZero.push(newSeq);
                    }
                    else {

                        // Put the last element
                        // of endOne into newSeq
                        newSeq = endOne[endOne.length - 1];

                        // Remove the last
                        // element of endOne
                        endOne.pop();

                        // newSeq ends with '0'
                        endZero.push(newSeq);
                    }
                }
                else {

                    // If there is no string
                    // which ends with '0'
                    if (endZero.length == 0) {

                        // Push newSeq into endOne
                        endOne.push(newSeq);
                    }
                    else {

                        // Put the last element
                        // of endZero into newSeq
                        newSeq = endZero[endZero.length - 1];

                        // Remove the last element of endOne
                        endZero.pop();

                        // newSeq ends with '1'
                        endOne.push(newSeq);
                    }
                }

                // Put newSeq into vector ans
                ans[i] = newSeq;
            }

            // Output the minimum
            // number of subsequences
            document.write(endZero.length
                + endOne.length
                + '<br>');

            // Output the subsequences
            // to which each character
            // of S belongs to
            for (let i = 0; i < N; ++i) {

                // Add 1 as the index starts from 0
                document.write(ans[i] + 1 + " ");
            }
        }

        // Driver Code

        // Given input
        let S = "1000110";
        let N = 7;

        // Function Call
        findSeq(S, N);

    // This code is contributed by Potta Lokesh
    </script>*
```

***Output**

```
3
1 1 2 3 3 2 2 
```* 

***时间复杂度:**O(N)
T3】辅助空间: O(N)*