# 最小化按字符频率递增顺序对字符串进行排序的成本

> 原文:[https://www . geeksforgeeks . org/最小化按频率递增顺序排序字符串的成本/](https://www.geeksforgeeks.org/minimize-cost-to-sort-a-string-in-increasing-order-of-frequencies/)

给定一个字符串 **S** ，任务是通过将一个重复字符块与另一个不同重复字符块进行交换，计算按频率递增顺序对字符串进行排序的最小成本。每次操作的成本是两个区块的绝对差值。
**例:**

> **输入:**S = " aabbcccdefffgghhii "
> T3】输出:5
> T6】解释:
> 
> *   用“aa”替换“d”。此操作的成本为 1
> *   用“bb”替换“e”。此操作的成本为 1
> *   用“ccc”替换“ii”。此操作的成本是成本是 1
> *   用“ffff”替换“ccc”。此操作的成本为 1
> *   用“hhhhh”替换“ffff”。此操作的成本为 1
> 
> **输入:**S = " AAAA "
> T3】输出: 0

**方法:**
按照以下步骤解决问题:

*   存储字符串中出现的每个字符的[频率。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)
*   对频率进行排序。
*   计算**排序后的**和**原始**序列中各频率之间的差值。
*   所有差异总和的一半是必需的答案。这是因为，对于每个交换，在上面的步骤中会计算两次差值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// above approach
#include <bits/stdc++.h>
using namespace std;

int sortString(string S)
{
    vector<int> sorted, original;
    bool insert = false;

    // For a single character
    if (S.length() == 1)
    {
        cout << 0 << endl;
    }

    // Stores count of repetitions
    // of a character
    int curr = 1;

    for(int i = 0; i < (S.length() - 1); i++)
    {

        // If repeating character
        if (S[i] == S[i + 1])
        {
            curr += 1;
            insert = false;
        }

        // Otherwise
        else
        {

            // Store frequency
            sorted.push_back(curr);
            original.push_back(curr);

            // Reset count
            curr = 1;
            insert = true;
        }
    }

    // Insert the last character block
    if ((S[(S.length() - 1)] !=
         S[(S.length() - 2)]) || insert == false)
    {
        sorted.push_back(curr);
        original.push_back(curr);
    }

    // Sort the frequencies
    sort(sorted.begin(), sorted.end());

    // Stores the minimum cost of all operations
    int t_cost = 0;

    for(int i = 0; i < sorted.size(); i++)
    {

        // Store the absolute difference of
        // i-th frequencies of ordered and
        // unordered sequences
        t_cost += abs(sorted[i] -
                      original[i]);
    }

    // Return the minimum cost
    return (t_cost / 2);
}

// Driver Code
int main()
{
    string S = "aabbcccdeffffggghhhhhii";

    cout << sortString(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// above approach
import java.util.*;

class GFG{

public static int sortString(String S)
{
    Vector<Integer> sorted = new Vector<Integer>();
    Vector<Integer> original = new Vector<Integer>();
    boolean insert = false;

    // For a single character
    if (S.length() == 1)
    {
        System.out.println(0);
    }

    // Stores count of repetitions
    // of a character
    int curr = 1;
    for(int i = 0; i < (S.length() - 1); i++)
    {

        // If repeating character
        if (S.charAt(i) == S.charAt(i + 1))
        {
            curr += 1;
            insert = false;
        }

        // Otherwise
        else
        {

            // Store frequency
            sorted.add(curr);
            original.add(curr);

            // Reset count
            curr = 1;
            insert = true;
        }
    }

    // Insert the last character block
    if ((S.charAt(S.length() - 1) !=
         S.charAt(S.length() - 2)) ||
         insert == false)
    {
        sorted.add(curr);
        original.add(curr);
    }

    // Sort the frequencies
    Collections.sort(sorted);

    // Stores the minimum cost of all operations
    int t_cost = 0;
    for(int i = 0; i < sorted.size(); i++)
    {

        // Store the absolute difference of
        // i-th frequencies of ordered and
        // unordered sequences
        t_cost += Math.abs(sorted.get(i) -
                           original.get(i));
    }

    // Return the minimum cost
    return (t_cost / 2);
}

// Driver code
public static void main(String[] args)
{
    String S = "aabbcccdeffffggghhhhhii";
    System.out.print(sortString(S));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
def sortString(S):

    sorted1 = []
    original = []
    insert = False

    # For a single character
    if (len(S) == 1):
        print(0)

    # Stores count of repetitions
    # of a character
    curr = 1

    for i in range(len(S) - 1):
        # If repeating character
        if (S[i] == S[i + 1]):
            curr += 1
            insert = False

        # Otherwise
        else:
            # Store frequency
            sorted1.append(curr)
            original.append(curr)

            # Reset count
            curr = 1
            insert = True

    # Insert the last character block
    if ((S[(len(S) - 1)] != S[(len(S) - 2)]) or
         insert == False):
        sorted1.append(curr)
        original.append(curr)

    # Sort the frequencies
    sorted1.sort()

    # Stores the minimum cost of all operations
    t_cost = 0

    for i in range(len(sorted1)):

        # Store the absolute difference of
        # i-th frequencies of ordered and
        # unordered sequences
        t_cost += abs(sorted1[i] - original[i])

    # Return the minimum cost
    return (t_cost // 2)

# Driver Code
if __name__ == "__main__":
    S = "aabbcccdeffffggghhhhhii"
    print(sortString(S))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// above approach
using System;
using System.Collections.Generic;

class GFG{

public static int sortString(string S)
{
    List<int> sorted = new List<int>();
    List<int> original = new List<int>();

    bool insert = false;

    // For a single character
    if (S.Length == 1)
    {
        Console.WriteLine(0);
    }

    // Stores count of repetitions
    // of a character
    int curr = 1;

    for(int i = 0; i < (S.Length - 1); i++)
    {

        // If repeating character
        if (S[i] == S[i + 1])
        {
            curr += 1;
            insert = false;
        }

        // Otherwise
        else
        {

            // Store frequency
            sorted.Add(curr);
            original.Add(curr);

            // Reset count
            curr = 1;
            insert = true;
        }
    }

    // Insert the last character block
    if ((S[S.Length - 1] !=
         S[S.Length - 2]) || insert == false)
    {
        sorted.Add(curr);
        original.Add(curr);
    }

    // Sort the frequencies
    sorted.Sort();

    // Stores the minimum cost of all operations
    int t_cost = 0;

    for(int i = 0; i < sorted.Count; i++)
    {

        // Store the absolute difference of
        // i-th frequencies of ordered and
        // unordered sequences
        t_cost += Math.Abs(sorted[i] -
                         original[i]);
    }

    // Return the minimum cost
    return (t_cost / 2);
}

// Driver Code   
static void Main()
{
    string S = "aabbcccdeffffggghhhhhii";

    Console.Write(sortString(S));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // Javascript program to implement above approach

    function sortString(S)
    {
        let sorted = [];
        let original = [];

        let insert = false;

        // For a single character
        if (S.length == 1)
        {
            document.write(0 + "</br>");
        }

        // Stores count of repetitions
        // of a character
        let curr = 1;

        for(let i = 0; i < (S.length - 1); i++)
        {

            // If repeating character
            if (S[i] == S[i + 1])
            {
                curr += 1;
                insert = false;
            }

            // Otherwise
            else
            {

                // Store frequency
                sorted.push(curr);
                original.push(curr);

                // Reset count
                curr = 1;
                insert = true;
            }
        }

        // Insert the last character block
        if ((S[S.length - 1] !=
             S[S.length - 2]) || insert == false)
        {
            sorted.push(curr);
            original.push(curr);
        }

        // Sort the frequencies
        sorted.sort(function(a, b){return a - b});

        // Stores the minimum cost of all operations
        let t_cost = 0;

        for(let i = 0; i < sorted.length; i++)
        {

            // Store the absolute difference of
            // i-th frequencies of ordered and
            // unordered sequences
            t_cost += Math.abs(sorted[i] - original[i]);
        }

        // Return the minimum cost
        return parseInt(t_cost / 2, 10);
    }

    let S = "aabbcccdeffffggghhhhhii";

    document.write(sortString(S));

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*