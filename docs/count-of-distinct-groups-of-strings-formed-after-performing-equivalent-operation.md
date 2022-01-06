# 执行等效操作后形成的不同字符串组的计数

> 原文:[https://www . geeksforgeeks . org/执行等效操作后形成的不同字符串组的计数/](https://www.geeksforgeeks.org/count-of-distinct-groups-of-strings-formed-after-performing-equivalent-operation/)

给定一个由小写字母组成的 **N** 字符串的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出在执行等价操作后形成的不同字符串组的数量。

> 如果两个字符串中存在相同的**字符，并且如果存在与等价字符串组中的一个字符串等价的另一个字符串，则这两个字符串被称为等价的**。****

******示例:******

> ******输入:**arr[]= {“a”、“b”、“ab”、“d”}
> **输出:** 2
> **解释:**
> 由于字符串“b”和“ab”有‘b’作为同一个字符，它们也等价于“ab”，字符串“a”有‘a’作为同一个字符，所以字符串“a”、“b”、“ab”是等价的，“d”是另一个字符串。****
> 
>  ****因此，形成的不同字符串组的计数是 2。
> 
> **输入:**arr[]= {“ab”、“bc”、“ABC”}
> **输出:** 1****

******方法:**给定的问题可以使用[不相交集合并集](https://www.geeksforgeeks.org/disjoint-set-data-structures/)来解决，思路是遍历字符串，将当前字符串的所有**字符**标记为**真**，对当前字符串的第一个字符进行**并集**操作，字符为**‘a’**，统计**父**向量中**不同**的父数并存储。按照以下步骤解决问题:****

*   ****初始化[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **父(27)，秩(27，0)，总计(26，假)**，和**当前(26，假)**。****
*   ****初始化一个变量，比如说 **distCount** 为 **0** ，它存储不同字符串的计数。****
*   ****使用变量 **i** 迭代范围**【0，27)** ，并将**父级【I】**的值设置为 **i** 。****
*   ****使用变量 **i** 迭代范围**【0，N)** ，并执行以下步骤:

    *   [使用变量 **j** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，26)** ，并将**电流【j】**设置为**假**。
    *   使用变量 **ch** 迭代字符串**arr【I】**的字符，并将**当前的【ch –' a '】**设置为 **true** 。
    *   使用变量 **j** 迭代范围**【0，26】**，如果**当前【j】**为真，则将**总计【j】**设置为**真**，并调用函数 **Union(父，rank，arr[I][0]–‘a’，j)** 。**** 
*   ****使用变量 **i** 迭代范围**【0，26)** ，检查**总计【I】**是否为**真**和**查找(父，i)** 是否为 **I** 如果为真，则将 **distCount** 的值增加 **1** 。****
*   ****最后，打印 **distCount** 的值。****

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to perform the find operation
// to find the parent of a disjoint set
int Find(vector<int>& parent, int a)
{
    return parent[a]
           = (parent[a] == a ? a : Find(parent, parent[a]));
}

// Function to perform union operation
// of disjoint set union
void Union(vector<int>& parent,
           vector<int>& rank, int a,
           int b)
{

    // Find the parent of node a and b
    a = Find(parent, a);
    b = Find(parent, b);

    // Update the rank
    if (rank[a] == rank[b])
        rank[a]++;
    if (rank[a] > rank[b])
        parent[b] = a;
    else
        parent[a] = b;
}

// Function to find the number of distinct
// strings after performing the
// given operations
void numOfDistinctStrings(string arr[],
                          int N)
{
    // Stores the parent elements
    // of the sets
    vector<int> parent(27);

    // Stores the rank of the sets
    vector<int> rank(27, 0);

    for (int j = 0; j < 27; j++) {
        // Update parent[i] to i
        parent[j] = j;
    }

    // Stores the total characters
    // traversed through the strings
    vector<bool> total(26, false);

    // Stores the current characters
    // traversed through a string
    vector<bool> current(26, false);

    for (int i = 0; i < N; i++) {

        for (int j = 0; j < 26; j++) {

            // Update current[i] to false
            current[j] = false;
        }

        for (char ch : arr[i]) {

            // Update current[ch - 'a'] to true
            current[ch - 'a'] = true;
        }

        for (int j = 0; j < 26; j++) {

            // Check if current[j] is true
            if (current[j]) {

                // Update total[j] to true
                total[j] = true;

                // Add arr[i][0] - 'a' and
                // j elements to same set
                Union(parent, rank,
                      arr[i][0] - 'a', j);
            }
        }
    }

    // Stores the count of distinct strings
    int distCount = 0;
    for (int i = 0; i < 26; i++) {

        // Check total[i] is true and
        // parent of i is i only
        if (total[i] && Find(parent, i) == i) {

            // Increment the value of
            // distCount by 1
            distCount++;
        }
    }

    // Print the value of distCount
    cout << distCount << endl;
}

// Driver Code
int main()
{
    string arr[] = { "a", "ab", "b", "d" };
    int N = sizeof(arr) / sizeof(arr[0]);
    numOfDistinctStrings(arr, N);

    return 0;
}**
```

## ****蟒蛇 3****

```
**# python program for the above approach

# Function to perform the find operation
# to find the parent of a disjoint set
def Find(parent, a):
    if parent[a] == a:
        parent[a] = a
        return parent[a]
    else:
        parent[a] = Find(parent, parent[a])
        return parent[a]

# Function to perform union operation
# of disjoint set union
def Union(parent, rank, a, b):

        # Find the parent of node a and b
    a = Find(parent, a)
    b = Find(parent, b)

    # Update the rank
    if (rank[a] == rank[b]):
        rank[a] += 1
    if (rank[a] > rank[b]):
        parent[b] = a
    else:
        parent[a] = b

# Function to find the number of distinct
# strings after performing the
# given operations
def numOfDistinctStrings(arr, N):

    # Stores the parent elements
    # of the sets
    parent = [0 for _ in range(27)]

    # Stores the rank of the sets
    rank = [0 for _ in range(27)]

    for j in range(0, 27):
        # Update parent[i] to i
        parent[j] = j

    # Stores the total characters
    # traversed through the strings
    total = [False for _ in range(26)]

    # Stores the current characters
    # traversed through a string
    current = [False for _ in range(26)]

    for i in range(0, N):

        for j in range(0, 26):

            # Update current[i] to false
            current[j] = False

        for ch in arr[i]:

            # Update current[ch - 'a'] to true
            current[ord(ch) - ord('a')] = True

        for j in range(0, 26):

            # Check if current[j] is true
            if (current[j]):

                # Update total[j] to true
                total[j] = True

                # Add arr[i][0] - 'a' and
                # j elements to same set
                Union(parent, rank, ord(arr[i][0]) - ord('a'), j)

    # Stores the count of distinct strings
    distCount = 0
    for i in range(0, 26):

        # Check total[i] is true and
        # parent of i is i only
        if (total[i] and Find(parent, i) == i):

            # Increment the value of
            # distCount by 1
            distCount += 1

    # Print the value of distCount
    print(distCount)

# Driver Code
if __name__ == "__main__":

    arr = ["a", "ab", "b", "d"]
    N = len(arr)
    numOfDistinctStrings(arr, N)

    # This code is contributed by rakeshsahni**
```

## ****C#****

```
**// C# program for the above approach
using System;
class GFG {

    // Function to perform the find operation
    // to find the parent of a disjoint set
    static int Find(int[] parent, int a)
    {
        return parent[a]
            = (parent[a] == a ? a
                              : Find(parent, parent[a]));
    }

    // Function to perform union operation
    // of disjoint set union
    static void Union(int[] parent, int[] rank, int a,
                      int b)
    {

        // Find the parent of node a and b
        a = Find(parent, a);
        b = Find(parent, b);

        // Update the rank
        if (rank[a] == rank[b])
            rank[a]++;
        if (rank[a] > rank[b])
            parent[b] = a;
        else
            parent[a] = b;
    }

    // Function to find the number of distinct
    // strings after performing the
    // given operations
    static void numOfDistinctStrings(string[] arr, int N)
    {
        // Stores the parent elements
        // of the sets
        int[] parent = new int[(27)];

        // Stores the rank of the sets
        int[] rank = new int[(27)];

        for (int j = 0; j < 27; j++) {
            // Update parent[i] to i
            parent[j] = j;
        }

        // Stores the total characters
        // traversed through the strings
        bool[] total = new bool[26];

        // Stores the current characters
        // traversed through a string
        bool[] current = new bool[26];

        for (int i = 0; i < N; i++) {

            for (int j = 0; j < 26; j++) {

                // Update current[i] to false
                current[j] = false;
            }

            foreach(char ch in arr[i])
            {

                // Update current[ch - 'a'] to true
                current[ch - 'a'] = true;
            }

            for (int j = 0; j < 26; j++) {

                // Check if current[j] is true
                if (current[j]) {

                    // Update total[j] to true
                    total[j] = true;

                    // Add arr[i][0] - 'a' and
                    // j elements to same set
                    Union(parent, rank, arr[i][0] - 'a', j);
                }
            }
        }

        // Stores the count of distinct strings
        int distCount = 0;
        for (int i = 0; i < 26; i++) {

            // Check total[i] is true and
            // parent of i is i only
            if (total[i] && Find(parent, i) == i) {

                // Increment the value of
                // distCount by 1
                distCount++;
            }
        }

        // Print the value of distCount
        Console.WriteLine(distCount);
    }

    // Driver Code
    public static void Main()
    {
        string[] arr = { "a", "ab", "b", "d" };
        int N = arr.Length;
        numOfDistinctStrings(arr, N);
    }
}

// This code is contributed by ukasp.**
```

******Output:** 

```
2
```**** 

*******时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*****