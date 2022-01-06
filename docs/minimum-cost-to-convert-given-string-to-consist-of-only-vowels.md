# 将给定字符串转换为仅包含元音的最小成本

> 原文:[https://www . geesforgeks . org/将给定字符串转换为仅由元音组成的最小成本/](https://www.geeksforgeeks.org/minimum-cost-to-convert-given-string-to-consist-of-only-vowels/)

给定小写字母的字符串 **str** ，任务是找到在只包含元音的字符串中更改输入字符串的最小成本。每个辅音都变成了最接近的元音。成本定义为辅音和元音的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)之间的绝对差异。

**示例:**

> **输入:** str = "abcde"
> **输出:** 4
> **解释:**
> 这里 a 和 e 已经是元音了，但是 b、c 和 d 是辅音。所以 b、c、d 变成最接近的元音为:
> 1。b–>a = | 98–97 | = 1，
> 2。c–>a = | 99–97 | = 2 或 c–>e = | 99–101 | = 2(以最小成本计算)，
> 3。d–>e = | 100–101 | = 1。
> 因此，最小成本为 1 + 2 + 1 = 4。
> 
> **输入:** str = "aaa"
> **输出:** 0
> **说明:**
> 字符串中没有辅音。

**方法:**思路是遍历字符串，将每个辅音替换为它们最近的元音，并将成本加为辅音和变化元音之间的差异。打印所有操作后的成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
int min_cost(string st)
{

    // Store vowels
    string vow = "aeiou";
    int cost = 0;

    // Loop for iteration of string
    for(int i = 0; i < st.size(); i++)
    {
        vector<int> costs;

        // Loop to calculate the cost
        for(int j = 0; j < 5; j++)
            costs.push_back(abs(st[i] - vow[j]));

        // Add minimum cost
        cost += *min_element(costs.begin(),
                            costs.end());
    }
    return cost;
}

// Driver Code
int main()
{

    // Given String
    string str = "abcde";

    // Function Call
    cout << (min_cost(str));
}

// This code is contributed by grand_master
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the minimum cost
static int min_cost(String st)
{

    // Store vowels
    String vow = "aeiou";
    int cost = 0;

    // Loop for iteration of string
    for(int i = 0; i < st.length(); i++)
    {
        ArrayList<Integer> costs = new ArrayList<>();

        // Loop to calculate the cost
        for(int j = 0; j < 5; j++)
            costs.add(Math.abs(st.charAt(i) -
                              vow.charAt(j)));

        // Add minimum cost
        int minx = Integer.MAX_VALUE;
        for(int x : costs)
        {
            if(x < minx)
            {
                minx = x;
            }
        }
        cost += minx;
    }
    return cost;
}

// Driver Code
public static void main(String[] args)
{

    // Given string
    String str = "abcde";

    // Function call
    System.out.println(min_cost(str));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find the minimum cost
def min_cost(st):

    # Store vowels
    vow = "aeiou"
    cost = 0

    # Loop for iteration of string
    for i in range(len(st)):
        costs = []

        # Loop to calculate the cost
        for j in range(5):
            costs.append(abs(ord(st[i])-ord(vow[j])))

        # Add minimum cost
        cost += min(costs)
    return cost

# Driver Code

# Given String
str = "abcde"

# Function Call
print(min_cost(str))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum cost
static int min_cost(string st)
{

    // Store vowels
    string vow = "aeiou";
    int cost = 0;

    // Loop for iteration of string
    for(int i = 0; i < st.Length; i++)
    {
        List<int> costs = new List<int>();

        // Loop to calculate the cost
        for(int j = 0; j < 5; j++)
            costs.Add(Math.Abs(st[i] -
                              vow[j]));

        // Add minimum cost
        int minx = Int32.MaxValue;
        foreach(int x in costs)
        {
            if(x < minx)
            {
                minx = x;
            }
        }
        cost += minx;
    }
    return cost;
}

// Driver Code
public static void Main()
{

    // Given string
    string str = "abcde";

    // Function call
    Console.WriteLine(min_cost(str));
}
}

// This code is contributed by code_hunt
```

**Output:**

```
4

```

**时间复杂度:** *O(N)，其中 N 是字符串的长度。*
**辅助空间:** *O(1)*