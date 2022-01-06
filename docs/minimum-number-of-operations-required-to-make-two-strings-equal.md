# 使两个字符串相等所需的最小操作次数

> 原文:[https://www . geesforgeks . org/最小操作数-要求使两个字符串相等/](https://www.geeksforgeeks.org/minimum-number-of-operations-required-to-make-two-strings-equal/)

给定两个字符串 **s1** 和 **s2** ，它们只包含相同长度的小写字母。任务是通过使用最少的操作次数使这些字符串相等。在一次操作中，你可以把任何一个字母和其他任何一个字母等同起来。

**示例:**

> **输入:**S1 =“abb”，S2 =“dad”
> **输出:**2
> a->d
> b->a
> **说明:**
> 第一次操作后的字符串–
> S1 =“dbb”，S2 =“DDD”
> 第二次操作后的字符串–
> S1 =“DDD”，S2 =“DDD”
> 
> **输入:**S1 =“Bab”，S2 =“aab”
> **输出:** 1
> b - > a
> **解释:**
> 第一次操作后的字符串–
> S1 =“AAA”，S2 =“AAA”

**方法:**思路是使用[不相交集并集数据结构](https://www.geeksforgeeks.org/disjoint-set-data-structures/)。下面是步骤的图示:

*   将每个字母表的父字母初始化为它自己。
*   在索引的帮助下同时遍历两个字符串，检查对应的字符是否有不同的父字符，然后合并字符串中排名较低的字符串。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of operations to
// make two strings equal

#include <bits/stdc++.h>

#define MAX 500001
using namespace std;

int parent[MAX];
int Rank[MAX];

// Function to find out
// parent of an alphabet
int find(int x)
{
    return parent[x] =
       parent[x] == x ? x :
            find(parent[x]);
}

// Function to merge two
// different alphabets
void merge(int r1, int r2)
{
    // Merge a and b using
    // rank compression
    if (r1 != r2) {
        if (Rank[r1] > Rank[r2]) {
            parent[r2] = r1;
            Rank[r1] += Rank[r2];
        }
        else {
            parent[r1] = r2;
            Rank[r2] += Rank[r1];
        }
    }
}

// Function to find the minimum
// number of operations required
void minimumOperations(string s1,
                       string s2){

    // Initializing parent to i
    // and rank(size) to 1
    for (int i = 1; i <= 26; i++) {
        parent[i] = i;
        Rank[i] = 1;
    }

    // We will store our
    // answerin this vector
    vector<pair<char, char> > ans;

    // Traversing strings
    for (int i = 0; i < s1.length(); i++) {
        if (s1[i] != s2[i]) {

            // If they have different parents
            if (find(s1[i] - 96) !=
                find(s2[i] - 96)) {

                // Find their respective
                // parents and merge them
                int x = find(s1[i] - 96);
                int y = find(s2[i] - 96);
                merge(x, y);

                // Store this in
                // our Answer vector
                ans.push_back({ s1[i], s2[i] });
            }
        }
    }

    // Number of operations
    cout << ans.size() << endl;
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i].first << "->"
             <<ans[i].second << endl;

}

// Driver Code
int main()
{
    // Two strings
    // S1 and S2
    string s1, s2;
    s1 = "abb";
    s2 = "dad";

    // Function Call
    minimumOperations(s1, s2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of operations to
// make two Strings equal
import java.util.*;

class GFG{

static final int MAX = 500001;
static int []parent = new int[MAX];
static int []Rank = new int[MAX];

static class pair
{
    char first, second;

    public pair(char first, char second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find out
// parent of an alphabet
static int find(int x)
{
    return parent[x] = parent[x] == x ? x :
                  find(parent[x]);
}

// Function to merge two
// different alphabets
static void merge(int r1, int r2)
{

    // Merge a and b using
    // rank compression
    if (r1 != r2)
    {
        if (Rank[r1] > Rank[r2])
        {
            parent[r2] = r1;
            Rank[r1] += Rank[r2];
        }
        else
        {
            parent[r1] = r2;
            Rank[r2] += Rank[r1];
        }
    }
}

// Function to find the minimum
// number of operations required
static void minimumOperations(String s1,
                              String s2)
{

    // Initializing parent to i
    // and rank(size) to 1
    for(int i = 1; i <= 26; i++)
    {
        parent[i] = i;
        Rank[i] = 1;
    }

    // We will store our
    // answer in this vector
    Vector<pair> ans = new Vector<pair>();

    // Traversing Strings
    for(int i = 0; i < s1.length(); i++)
    {
        if (s1.charAt(i) != s2.charAt(i))
        {

            // If they have different parents
            if (find(s1.charAt(i) - 96) !=
                find(s2.charAt(i) - 96))
            {

                // Find their respective
                // parents and merge them
                int x = find(s1.charAt(i) - 96);
                int y = find(s2.charAt(i) - 96);
                merge(x, y);

                // Store this in
                // our Answer vector
                ans.add(new pair(s1.charAt(i),
                                 s2.charAt(i)));
            }
        }
    }

    // Number of operations
    System.out.print(ans.size() + "\n");
    for(int i = 0; i < ans.size(); i++)
        System.out.print(ans.get(i).first + "->" +
                         ans.get(i).second +"\n");
}

// Driver Code
public static void main(String[] args)
{

    // Two Strings
    // S1 and S2
    String s1, s2;
    s1 = "abb";
    s2 = "dad";

    // Function call
    minimumOperations(s1, s2);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of operations to
# make two strings equal

MAX = 500001
parent = [0] * MAX
Rank = [0] * MAX

# Function to find out
# parent of an alphabet
def find(x):

    if parent[x] == x:
        return x
    else:
        return find(parent[x])

# Function to merge two
# different alphabets
def merge(r1, r2):

    # Merge a and b using
    # rank compression
    if(r1 != r2):
        if(Rank[r1] > Rank[r2]):
            parent[r2] = r1
            Rank[r1] += Rank[r2]

        else:
            parent[r1] = r2
            Rank[r2] += Rank[r1]

# Function to find the minimum
# number of operations required
def minimumOperations(s1, s2):

    # Initializing parent to i
    # and rank(size) to 1
    for i in range(1, 26 + 1):
        parent[i] = i
        Rank[i] = 1

    # We will store our
    # answerin this list
    ans = []

    # Traversing strings
    for i in range(len(s1)):
        if(s1[i] != s2[i]):

            # If they have different parents
            if(find(ord(s1[i]) - 96) !=
               find(ord(s2[i]) - 96)):

                # Find their respective
                # parents and merge them
                x = find(ord(s1[i]) - 96)
                y = find(ord(s2[i]) - 96)
                merge(x, y)

                # Store this in
                # our Answer list
                ans.append([s1[i], s2[i]])

    # Number of operations
    print(len(ans))
    for i in ans:
        print(i[0], "->", i[1])

# Driver code
if __name__ == '__main__':

    # Two strings
    # S1 and S2
    s1 = "abb"
    s2 = "dad"

    # Function Call
    minimumOperations(s1, s2)

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation to find the
// minimum number of operations to
// make two Strings equal
using System;
using System.Collections.Generic;
class GFG{

static readonly int MAX = 500001;
static int []parent = new int[MAX];
static int []Rank = new int[MAX];
class pair
{
  public char first, second;
  public pair(char first, char second)
  {
    this.first = first;
    this.second = second;
  }
}

// Function to find out
// parent of an alphabet
static int find(int x)
{
  return parent[x] = parent[x] ==
         x ? x : find(parent[x]);
}

// Function to merge two
// different alphabets
static void merge(int r1, int r2)
{
  // Merge a and b using
  // rank compression
  if (r1 != r2)
  {
    if (Rank[r1] > Rank[r2])
    {
      parent[r2] = r1;
      Rank[r1] += Rank[r2];
    }
    else
    {
      parent[r1] = r2;
      Rank[r2] += Rank[r1];
    }
  }
}

// Function to find the minimum
// number of operations required
static void minimumOperations(String s1,
                              String s2)
{
  // Initializing parent to i
  // and rank(size) to 1
  for(int i = 1; i <= 26; i++)
  {
    parent[i] = i;
    Rank[i] = 1;
  }

  // We will store our
  // answer in this vector
  List<pair> ans = new List<pair>();

  // Traversing Strings
  for(int i = 0; i < s1.Length; i++)
  {
    if (s1[i] != s2[i])
    {
      // If they have different parents
      if (find(s1[i] - 96) !=
          find(s2[i] - 96))
      {
        // Find their respective
        // parents and merge them
        int x = find(s1[i] - 96);
        int y = find(s2[i] - 96);
        merge(x, y);

        // Store this in
        // our Answer vector
        ans.Add(new pair(s1[i],
                         s2[i]));
      }
    }
  }

  // Number of operations
  Console.Write(ans.Count + "\n");
  for(int i = 0; i < ans.Count; i++)
    Console.Write(ans[i].first + "->" +
                  ans[i].second + "\n");
}

// Driver Code
public static void Main(String[] args)
{   
  // Two Strings
  // S1 and S2
  String s1, s2;
  s1 = "abb";
  s2 = "dad";

  // Function call
  minimumOperations(s1, s2);
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
2
a->d
b->a
```

**时间复杂度:** O(N)，其中 N 为给定字符串的长度。
**辅助空间:** O(N)。