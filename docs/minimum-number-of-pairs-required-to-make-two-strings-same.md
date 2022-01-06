# 使两根弦相同所需的最小对数

> 原文:[https://www . geesforgeks . org/最小配对数-需要制作两个相同的字符串/](https://www.geeksforgeeks.org/minimum-number-of-pairs-required-to-make-two-strings-same/)

给定两个长度相同的字符串 **s1** 和 **s2** ，任务是计算字符对 **(c1，c2)** 的最小数量，从而通过将任意字符串中的 **c1 转换为 c2** 或 **c2 转换为 c1** 的任意次数，使两个字符串相同。

**示例:**

> **输入:**s1 =“abb”，S2 =“dad”
> **输出:** 2
> 变换 S1 中的‘a’->‘d’、‘b’->‘a’和‘b’->‘a’->‘d’。
> 我们不能把(a，d)、(b，a)、(b，d)当成对，因为
> (b，d)可以通过遵循变换‘b’->‘a’->‘d’来实现
> 
> **输入:**S1 =“drpepper”，S2 =“cocacola”
> T3】输出: 7

**方法:**这个问题可以用图或不相交集来解决。构建一个空图 G，并遍历字符串。仅当满足以下条件之一时，才在图 G 中添加边:

*   **S1【I】**和**S2【I】**都不在 g
*   **s1[i]** 在 G，但 **s2[i]** 不在 G
*   **s2[i]** 在 G，但 **s1[i]** 不在 G
*   从**S1【I】**到**S2【I】**没有路径。

最小对数将是最终图形 g 中的边数

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function which will check if there is
// a path between a and b by using BFS
bool checkPath(char a, char b, 
           map<char, vector<char>> &G)
{
    map<char, bool> visited;
    deque<char> queue;
    queue.push_back(a);
    visited[a] = true;

    while (!queue.empty()) 
    {
        int n = queue.front();
        queue.pop_front();

        if (n == b) return true;
        for (auto i : G[n]) 
        {
            if (visited[i] == false)
            {
                queue.push_back(i);
                visited[i] = true;
            }
        }
    }
    return false;
}

// Function to return the 
// minimum number of pairs
int countPairs(string s1, string s2,
         map<char, vector<char>> &G, int x) 
{

    // To store the count of pairs
    int count = 0;

    // Iterating through the strings
    for (int i = 0; i < x; i++) 
    {
        char a = s1[i];
        char b = s2[i];

        // Check if we can add an edge in the graph
        if (G.find(a) != G.end() and 
            G.find(b) == G.end() and a != b)
        {
            G[a].push_back(b);
            G[b].push_back(a);
            count++;
        }
        else if (G.find(b) != G.end() and
                 G.find(a) == G.end() and a != b) 
        {
            G[b].push_back(a);
            G[a].push_back(b);
            count++;
        } 
        else if (G.find(a) == G.end() and 
                 G.find(b) == G.end() and a != b) 
        {
            G[a].push_back(b);
            G[b].push_back(a);
            count++;
        } 
        else
        {
            if (!checkPath(a, b, G) and a != b)
            {
                G[a].push_back(b);
                G[b].push_back(a);
                count++;
            }
        }
    }

    // Return the count of pairs
    return count;
}

// Driver Code
int main() 
{
    string s1 = "abb", s2 = "dad";
    int x = s1.length();
    map<char, vector<char>> G;
    cout << countPairs(s1, s2, G, x) << endl;

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import defaultdict, deque   

# Function which will check if there is 
# a path between a and b by using BFS
def Check_Path(a, b, G):
    visited = defaultdict(bool)
    queue = deque()
    queue.append(a)
    visited[a]= True
    while queue:
        n = queue.popleft()
        if n == b:
            return True
        for i in list(G[n]):
            if visited[i]== False:
                queue.append(i)
                visited[i]= True
    return False

# Function to return the minimum number of pairs
def countPairs(s1, s2, G):
    name = defaultdict(bool)

    # To store the count of pairs
    count = 0

    # Iterating through the strings
    for i in range(x):
        a = s1[i]
        b = s2[i]

        # Check if we can add an edge in the graph
        if a in G and b not in G and a != b:
            G[a].append(b)
            G[b].append(a)
            count+= 1
        elif b in G and a not in G and a != b:
            G[b].append(a)
            G[a].append(b)
            count+= 1
        elif a not in G and b not in G and a != b:
            G[a].append(b)
            G[b].append(a)
            count+= 1
        else:
            if not Check_Path(a, b, G) and a != b:
                G[a].append(b)
                G[b].append(a)
                count+= 1

    # Return the count of pairs
    return count

# Driver code
if __name__=="__main__":
    s1 ="abb"
    s2 ="dad"
    x = len(s1)
    G = defaultdict(list)
    print(countPairs(s1, s2, G))
```

**Output:**

```
2

```