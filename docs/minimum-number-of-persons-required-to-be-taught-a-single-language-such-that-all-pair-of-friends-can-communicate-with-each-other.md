# 需要被教授一种语言的最小人数，以便所有的朋友能够相互交流

> 原文:[https://www . geesforgeks . org/需要教授单一语言的最小人数，这样所有的朋友对都可以相互交流/](https://www.geeksforgeeks.org/minimum-number-of-persons-required-to-be-taught-a-single-language-such-that-all-pair-of-friends-can-communicate-with-each-other/)

给定一个整数 **N** 和两个[数组](https://www.geeksforgeeks.org/array-data-structure/) **A[][]** ，代表一个人知道的一组语言，以及 **B[][]** ，由 **M** 对友谊组成，任务是找到被教授单一语言的最小人数，以便每对朋友能够相互交流。

**示例:**

> **输入:** N = 2，A[][] = {{1}，{2}，{1，2}}，B[][] = {{1，2}，{1，3}，{2，3}}
> **输出:** 1
> **解释:**
> 一种可能的方法是教 1 <sup>st</sup> 人语言 2。
> 另一种可能的方法是教第二个<sup>人语言 1。
> 因此，要求教授的语言最少为 1 种。</sup>
> 
> **输入:** N = 4，A[][] = {{2}，{1，4}，{1，2}，{3，4}}，B[][] = {{1，4}，{1，2}，{3，4}，{2，3}}
> **输出:** 2
> **解释:**
> 其中一种可能的方法是教 1 <sup>st</sup> 人语言 3 或 4 和 3 <sup>rd
> 因此，要求教授的语言最少为 2 种。</sup>

**方法:**给定的问题可以使用[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)和[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)数据结构来解决给定的问题。
按照以下步骤解决问题:

*   定义一个函数，比如**检查(A[]，B[])** ，检查两个排序的数组中是否存在任何[公共元素](https://www.geeksforgeeks.org/union-and-intersection-of-two-sorted-arrays-2/):
    *   定义两个变量，比如说 **P1** 和 **P2** 来存储指针。
    *   一边迭代一边 **P1 < M** 和 **P2 < N** 。如果**A【P1】**等于**B【P2】**，则返回真。否则，如果**A【P1】<B【P2】**，将 **P1** 递增 1。否则，如果**A【P1】>B【P2】**，将 **P2** 增加 **1** 。
    *   如果以上情况都不满足，则返回 false。
*   初始化一个[集合< int >](https://www.geeksforgeeks.org/set-in-cpp-stl/) ，说 **S** ，和一个[地图< int，int >](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) ，说 **mp** ，存储所有不能和朋友交流的人，并统计懂某一种语言的人。
*   初始化一个变量，比如说**结果**，来存储被教人数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **B[][]** 调用函数 **Check(B[i][0]，B[i][1])插入这一对没有共同语言的人。**
*   [遍历一个人知道的语言集合](https://www.geeksforgeeks.org/how-to-traverse-a-c-set-in-reverse-direction/) **S** ，并在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **mp** 中增加该语言的计数。
*   [遍历地图< int，int >](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **mp** 并将**结果**更新为**结果= min(s . size()–it . second，result)。**
*   最后，完成上述步骤后，打印**结果。**

下面是上述方法的实现:

## C++

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if there
// exists any common language
bool check(vector<int>& a, vector<int>& b)
{
    // Stores the size of array a[]
    int M = a.size();

    // Stores the size of array b[]
    int N = b.size();

    // Pointers
    int p1 = 0, p2 = 0;

    // Iterate while p1 < M and p2 < N
    while (p1 < M && p2 < N) {

        if (a[p1] < b[p2])
            p1++;
        else if (a[p1] > b[p2])
            p2++;
        else
            return true;
    }
    return false;
}

// Function to count the minimum number
// of people required to be teached
int minimumTeachings(
    int N, vector<vector<int> >& languages,
    vector<vector<int> > friendships)
{
    // Stores the size of array A[][]
    int m = languages.size();

    // Stores the size of array B[][]
    int t = friendships.size();

    // Stores all the persons with no
    // common languages with their friends
    unordered_set<int> total;

    // Stores count of languages
    unordered_map<int, int> overall;

    // Sort all the languages of
    // a person in ascending order
    for (int i = 0; i < m; i++)
        sort(languages[i].begin(),
             languages[i].end());

    // Traverse the array B[][]
    for (int i = 0; i < t; i++) {
        // Check if there is no common
        // language between two friends
        if (!check(languages[friendships[i][0] - 1],
                   languages[friendships[i][1] - 1])) {

            // Insert the persons in the Set
            total.insert(friendships[i][0]);
            total.insert(friendships[i][1]);
        }
    }

    // Stores the size of the Set
    int s = total.size();

    // Stores the count of
    // minimum persons to teach
    int result = s;

    // Traverse the set total
    for (auto p : total) {

        // Traverse A[p - 1]
        for (int i = 0;
             i < languages[p - 1].size(); i++)

            // Increment count of languages by one
            overall[languages[p - 1][i]]++;
    }

    // Traverse the map
    for (auto c : overall)

        // Update result
        result = min(result, s - c.second);

    // Return the result
    return result;
}

// Driver Code
int main()
{
    int N = 3;

    vector<vector<int> > A
        = { { 1 }, { 1, 3 }, { 1, 2 }, { 3 } };

    vector<vector<int> > B
        = { { 1, 4 }, { 1, 2 }, { 3, 4 }, { 2, 3 } };

    cout << minimumTeachings(N, A, B) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to check if there
// exists any common language
static boolean check(int a[], int b[])
{

    // Stores the size of array a[]
    int M = a.length;

    // Stores the size of array b[]
    int N = b.length;

    // Pointers
    int p1 = 0, p2 = 0;

    // Iterate while p1 < M and p2 < N
    while (p1 < M && p2 < N)
    {
        if (a[p1] < b[p2])
            p1++;
        else if (a[p1] > b[p2])
            p2++;
        else
            return true;
    }
    return false;
}

// Function to count the minimum number
// of people required to be teached
static int minimumTeachings(int N, int languages[][],
                            int friendships[][])
{

    // Stores the size of array A[][]
    int m = languages.length;

    // Stores the size of array B[][]
    int t = friendships.length;

    // Stores all the persons with no
    // common languages with their friends
    HashSet<Integer> total = new HashSet<>();

    // Stores count of languages
    HashMap<Integer, Integer> overall = new HashMap<>();

    // Sort all the languages of
    // a person in ascending order
    for(int i = 0; i < m; i++)
        Arrays.sort(languages[i]);

    // Traverse the array B[][]
    for(int i = 0; i < t; i++)
    {

        // Check if there is no common
        // language between two friends
        if (!check(languages[friendships[i][0] - 1],
                   languages[friendships[i][1] - 1]))
        {

            // Insert the persons in the Set
            total.add(friendships[i][0]);
            total.add(friendships[i][1]);
        }
    }

    // Stores the size of the Set
    int s = total.size();

    // Stores the count of
    // minimum persons to teach
    int result = s;

    // Traverse the set total
    for(int p : total)
    {

        // Traverse A[p - 1]
        for(int i = 0; i < languages[p - 1].length; i++)

            // Increment count of languages by one
            overall.put(languages[p - 1][i],
                        overall.getOrDefault(
                            languages[p - 1][i], 0) + 1);
    }

    // Traverse the map
    for(int k : overall.keySet())

        // Update result
        result = Math.min(result, s - overall.get(k));

    // Return the result
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int N = 3;

    int A[][] = { { 1 }, { 1, 3 },
                  { 1, 2 }, { 3 } };

    int B[][] = { { 1, 4 }, { 1, 2 },
                  { 3, 4 }, { 2, 3 } };

    System.out.println(minimumTeachings(N, A, B));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to check if there
# exists any common language
def check(a, b):
    # Stores the size of array a[]
    M = len(a)

    # Stores the size of array b[]
    N = len(b)

    # Pointers
    p1 = 0
    p2 = 0

    # Iterate while p1 < M and p2 < N
    while(p1 < M and p2 < N):
        if (a[p1] < b[p2]):
            p1 += 1
        elif(a[p1] > b[p2]):
            p2 += 1
        else:
            return True
    return False

# Function to count the minimum number
# of people required to be teached
def minimumTeachings(N, languages, friendships):
    # Stores the size of array A[][]
    m = len(languages)

    # Stores the size of array B[][]
    t = len(friendships)

    # Stores all the persons with no
    # common languages with their friends
    total = set()

    # Stores count of languages
    overall = {}

    # Sort all the languages of
    # a person in ascending order
    for i in range(m):
        languages[i].sort(reverse=False)

    # Traverse the array B[][]
    for i in range(t):
        # Check if there is no common
        # language between two friends
        if(check(languages[friendships[i][0] - 1], languages[friendships[i][1] - 1])==False):
            # Insert the persons in the Set
            total.add(friendships[i][0])
            total.add(friendships[i][1])

    # Stores the size of the Set
    s = len(total)

    # Stores the count of
    # minimum persons to teach
    result = s

    # Traverse the set total
    for p in total:
        # Traverse A[p - 1]
        for i in range(len(languages[p - 1])):
            # Increment count of languages by one
            if languages[p - 1][i] in overall:
              overall[languages[p - 1][i]] += 1
            else:
              overall[languages[p - 1][i]] = 1

    # Traverse the map
    for keys,value in overall.items():
        # Update result
        result = min(result, s - value)

    # Return the result
    return result

# Driver Code
if __name__ == '__main__':
    N = 3

    A =   [[1],[1, 3],[1, 2],[3]]
    B =  [[1, 4],[1, 2],[3, 4],[2, 3]]
    print(minimumTeachings(N, A, B))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to check if there
    // exists any common language
    static bool check(int[] a, int[] b)
    {

        // Stores the size of array a[]
        int M = a.Length;

        // Stores the size of array b[]
        int N = b.Length;

        // Pointers
        int p1 = 0, p2 = 0;

        // Iterate while p1 < M and p2 < N
        while (p1 < M && p2 < N)
        {
            if (a[p1] < b[p2])
                p1++;
            else if (a[p1] > b[p2])
                p2++;
            else
                return true;
        }
        return false;
    }

    // Function to count the minimum number
    // of people required to be teached
    static int minimumTeachings(int N, int[,] languages,
                                int[,] friendships)
    {
        // Stores the size of array A[][]
        int m = languages.Length;
        int[] arr1 = {1,2,3};

        // Stores the size of array B[][]
        int t = friendships.Length;
        int[] arr2 = {1,2,3};

        // Stores all the persons with no
        // common languages with their friends
        HashSet<int> total = new HashSet<int>();

        // Stores count of languages
        Dictionary<int, int> overall = new Dictionary<int, int>();

        // Sort all the languages of
        // a person in ascending order
        for(int i = 0; i < m; i++)
            Array.Sort(arr1);

        // Traverse the array B[][]
        for(int i = 0; i < t; i++)
        {

            // Check if there is no common
            // language between two friends
            if (!check(arr1,arr2))
            {

                // Insert the persons in the Set
                total.Add(friendships[i,0]);
                total.Add(friendships[i,1]);
            }
        }

        // Stores the size of the Set
        int s = total.Count;

        // Stores the count of
        // minimum persons to teach
        int result = s+1;

        // Traverse the set total
        foreach(int p in total)
        {

            // Traverse A[p - 1]
            for(int i = 0; i < languages.GetLength(1); i++)

                // Increment count of languages by one
                overall[languages[p - 1,i]]+=1;
        }

        // Traverse the map
        foreach(KeyValuePair<int, int> k in overall)
        {
            result = Math.Min(result, s - k.Value);
        }

        // Return the result
        return result;
    }

  static void Main() {
    int N = 3;

    int[,] A = { { 1, 0 }, { 1, 3 },
                  { 1, 2 }, { 3, 0 } };

    int[,] B = { { 1, 4 }, { 1, 2 },
                  { 3, 4 }, { 2, 3 } };

    Console.Write(minimumTeachings(N, A, B));
  }
}
```

## java 描述语言

```
<script>

// Javascript implementation of
// the above approach

// Function to check if there
// exists any common language
function check(a, b)
{

    // Stores the size of array a[]
    let M = a.length;

    // Stores the size of array b[]
    let N = b.length;

    // Pointers
    let p1 = 0, p2 = 0;

    // Iterate while p1 < M and p2 < N
    while (p1 < M && p2 < N)
    {
        if (a[p1] < b[p2])
            p1++;
        else if (a[p1] > b[p2])
            p2++;
        else
            return true;
    }
    return false;
}

// Function to count the minimum number
// of people required to be teached
function minimumTeachings(N, languages, friendships)
{

    // Stores the size of array A[][]
    let m = languages.length;

    // Stores the size of array B[][]
    let t = friendships.length;

    // Stores all the persons with no
    // common languages with their friends
    let total = new Set();

    // Stores count of languages
    let overall = new Map();

    // Sort all the languages of
    // a person in ascending order
    for(let i = 0; i < m; i++)
        languages[i].sort((a, b) => a - b);

    // Traverse the array B[][]
    for(let i = 0; i < t; i++)
    {

        // Check if there is no common
        // language between two friends
        if (!check(languages[friendships[i][0] - 1],
                   languages[friendships[i][1] - 1]))
        {

            // Insert the persons in the Set
            total.add(friendships[i][0]);
            total.add(friendships[i][1]);
        }
    }

    // Stores the size of the Set
    let s = total.size;

    // Stores the count of
    // minimum persons to teach
    let result = s;

    // Traverse the set total
    for(let p of total)
    {

        // Traverse A[p - 1]
        for(let i = 0; i < languages[p - 1].length; i++)
        {

            // Increment count of languages by one
            if (overall.has(languages[p - 1][i]))
            {
                overall.set(languages[p - 1][i],
                overall.get(languages[p - 1][i]) + 1)
            }
            else
            {
                overall.set(languages[p - 1][i], 1)
            }
        }
    }

    // Traverse the map
    for(let c of overall)

        // Update result
        result = Math.min(result, s - c[1]);

    // Return the result
    return result;
}

// Driver Code
let N = 3;
let A = [ [ 1 ], [ 1, 3 ],
          [ 1, 2 ], [ 3 ] ];

let B = [ [ 1, 4 ], [ 1, 2 ],
          [ 3, 4 ], [ 2, 3 ] ];

document.write(minimumTeachings(N, A, B) + "<br>");

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*