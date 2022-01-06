# 最小化将二进制字符串的所有字符转换为 0 的成本

> 原文:[https://www . geesforgeks . org/将二进制字符串的所有字符转换为 0 的最小成本/](https://www.geeksforgeeks.org/minimize-cost-to-convert-all-characters-of-a-binary-string-to-0s/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)、**字符串**，两个整数[数组](https://www.geeksforgeeks.org/array-data-structure/) **R[]** ，以及大小为 **N** 的 **C[]** 。将所有字符从索引 **i** 翻转到**R【I】**需要**C【I】**成本。任务是最小化将给定的二进制字符串仅转换为 **0s** 所需的成本。

**示例:**

> **输入:**str =“1010”，R[] = {1，2，2，3}，C[] = {3，1，2，3}
> **输出:** 4
> **解释:**
> 将所有字符从索引 1 翻转到 2，将 str 修改为“1100”。因此，成本= 1
> 将所有字符从索引 1 翻转到 2，将 str 修改为“0000”。因此，成本=成本+ 3 = 4
> 因此，所需的最小成本为 4。
> 
> **输入:** str = "01100 "，R[] = {1，2，3，4，5}，C[] = {1，5，5，2，3}
> **输出:** 10

**接近**:使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。想法是[从左到右遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并检查当前字符是否为非零字符。如果发现为真，则将所有字符从**当前索引(= i)** 翻转到**R【I】<sup>th</sup>**索引。按照以下步骤解决问题:

*   初始化一个变量，说**翻转**，存储当前字符可以翻转的次数。
*   创建一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)，比如 **pq** 来存储翻转值大于 0 的当前字符右侧的字符索引范围。
*   初始化一个变量，说**代价**存储最小代价得到需要的字符串。
*   [遍历给定字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)，检查当前字符是否为“ **1** ”。如果发现是真的，则将范围内的所有角色 **i** 翻转至**R【I】**并将成本值增加**C【I】**。
*   最后打印**成本**的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to get the minimum
// Cost to convert all characters
// of given string to 0s
int minCost(string str, int N, int R[], int C[])
{
    // Stores the range of indexes
    // of characters that need
    // to be flipped
    priority_queue<int, vector<int>, greater<int> > pq;

    // Stores the number of times
    // current character is flipped
    int flip = 0;

    // Stores minimum cost to get
    // the required string
    int cost = 0;

    // Traverse the given string
    for (int i = 0; i < N; i++)
    {
        // Remove all value from pq
        // whose value is less than i
        while (pq.size() > 0 and pq.top() < i)
        {
            pq.pop();

            // Update flip
            flip--;
        }

        // If current character
        // is flipped odd times
        if (flip % 2 == 1)
        {
            str[i] = '1' - str[i] + '0';
        }

        // If current character contains
        // non-zero value
        if (str[i] == '1')
        {
            // Update flip
            flip++;

            // Update cost
            cost += C[i];

            // Append R[i] into pq
            pq.push(R[i]);
        }
    }
    return cost;
}

// Driver Code
int main()
{
    string str = "1010";
    int R[] = { 1, 2, 2, 3 };
    int C[] = { 3, 1, 2, 3 };
    int N = str.length();

    // Function call
    cout << minCost(str, N, R, C);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG {

    // Function to get the minimum
    // Cost to convert all characters
    // of given string to 0s
    public static int minCost(String s,
                              int R[],
                              int C[],
                              int N)
    {
        char ch[] = s.toCharArray();

        // Stores the range of indexes
        // of characters that need
        // to be flipped
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        // Stores the number of times
        // current character is flipped
        int flip = 0;

        // Stores minimum cost to get
        // the required string
        int cost = 0;

        // Traverse the given string
        for (int i = 0; i < N; i++) {

            // Remove all value from pq
            // whose value is less than i

            while (pq.size() > 0 && pq.peek() < i)
            {
                pq.poll();

                // Update flip
                flip--;
            }

            // Get the current number
            int cn = ch[i] - '0';

            // If current character
            // is flipped odd times
            if (flip % 2 == 1)
                cn = 1 - cn;

            // If current character contains
            // non-zero value
            if (cn == 1)
            {
                // Update flip
                flip++;

                // Update cost
                cost += C[i];

                // Append R[i] into pq
                pq.add(R[i]);
            }
        }
        return cost;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 4;
        String s = "1010";
        int R[] = { 1, 2, 2, 3 };
        int C[] = { 3, 1, 2, 3 };

        // Function call
        System.out.println(minCost(s, R, C, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to get the minimum
# Cost to convert all characters
# of given string to 0s
def minCost(s, R, C, N) :
    ch = list(s)

    # Stores the range of indexes
    # of characters that need
    # to be flipped
    pq = []

    # Stores the number of times
    # current character is flipped
    flip = 0

    # Stores minimum cost to get
    # the required string
    cost = 0

    # Traverse the given string
    for i in range(N) :

        # Remove all value from pq
        # whose value is less than i
        while (len(pq) > 0 and pq[0] < i) :

            pq.pop(0);

            # Update flip
            flip -= 1

        # Get the current number
        cn = ord(ch[i]) - ord('0')

        # If current character
        # is flipped odd times
        if (flip % 2 == 1) :
            cn = 1 - cn

        # If current character contains
        # non-zero value
        if (cn == 1) :

            # Update flip
            flip += 1

            # Update cost
            cost += C[i]

            # Append R[i] into pq
            pq.append(R[i])

    return cost

  # Driver code
N = 4
s = "1010"
R = [ 1, 2, 2, 3 ]
C = [ 3, 1, 2, 3 ]

# Function call
print(minCost(s, R, C, N))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to get the minimum
// Cost to convert all characters
// of given string to 0s
public static int minCost(String s, int []R,
                           int []C, int N)
{
    char []ch = s.ToCharArray();

    // Stores the range of indexes
    // of characters that need
    // to be flipped
    Queue<int> pq = new Queue<int>();

    // Stores the number of times
    // current character is flipped
    int flip = 0;

    // Stores minimum cost to get
    // the required string
    int cost = 0;

    // Traverse the given string
    for(int i = 0; i < N; i++)
    {

        // Remove all value from pq
        // whose value is less than i
        while (pq.Count > 0 && pq.Peek() < i)
        {
            pq.Dequeue();

            // Update flip
            flip--;
        }

        // Get the current number
        int cn = ch[i] - '0';

        // If current character
        // is flipped odd times
        if (flip % 2 == 1)
            cn = 1 - cn;

        // If current character contains
        // non-zero value
        if (cn == 1)
        {

            // Update flip
            flip++;

            // Update cost
            cost += C[i];

            // Append R[i] into pq
            pq.Enqueue(R[i]);

        }
    }
    return cost;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4;
    String s = "1010";
    int []R = { 1, 2, 2, 3 };
    int []C = { 3, 1, 2, 3 };

    // Function call
    Console.WriteLine(minCost(s, R, C, N));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to get the minimum
// Cost to convert all characters
// of given string to 0s
function minCost(str, N, R, C)
{
    str = str.split('');

    // Stores the range of indexes
    // of characters that need
    // to be flipped
    var pq = [];

    // Stores the number of times
    // current character is flipped
    var flip = 0;

    // Stores minimum cost to get
    // the required string
    var cost = 0;

    // Traverse the given string
    for (var i = 0; i < N; i++)
    {
        // Remove all value from pq
        // whose value is less than i
        while (pq.length > 0 && pq[pq.length-1] < i)
        {
            pq.pop();

            // Update flip
            flip--;
        }

        // If current character
        // is flipped odd times
        if (flip % 2 == 1)
        {
            str[i] = String.fromCharCode('1'.charCodeAt(0) - str[i].charCodeAt(0) + '0'.charCodeAt(0));
        }

        // If current character contains
        // non-zero value
        if (str[i] == '1')
        {
            // Update flip
            flip++;

            // Update cost
            cost += C[i];

            // Append R[i] into pq
            pq.push(R[i]);
        }
        pq.sort((a,b)=>b-a);
    }
    return cost;
}

// Driver Code
var str = "1010";
var R = [1, 2, 2, 3 ];
var C = [3, 1, 2, 3 ];
var N = str.length;

// Function call
document.write(minCost(str, N, R, C));

// This code is contributed by noob2000.
</script>
```

**Output**

```
4
```

**时间复杂度:**O(N * log N)
T3】辅助空间: O(N)