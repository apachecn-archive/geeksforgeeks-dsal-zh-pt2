# 没有给定前缀的 N 位数的计数

> 原文:[https://www . geesforgeks . org/n 位数字计数-没有给定前缀/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-not-having-given-prefixes/)

给定一个整数 **N** 和一个字符串的[向量](https://www.geeksforgeeks.org/array-strings-c-3-different-ways-create/) **前缀[]，**，任务是计算从字符**“0”**到**“9”**的总可能长度[字符串](https://www.geeksforgeeks.org/stringstream-c-applications/)。使得给定的前缀不能在任何字符串中使用。

**示例:**

> **输入:** N = 3，前缀= {“42”}
> **输出:** : 990
> **说明:**除{“420”、“421”、“422”、“423”、“424”、“425”、“426”、“427”、“428”、“429”}外的所有字符串均有效。
> 
> **输入:** N = 5，前缀[]**= {“0”、“1”、“911”}
> **输出:** 79900**

****方法:**可能的总长度字符串为 **(10^N)** 对于一个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/)中的每个位置，有 **10 个**字符选择。从总字符串中减去总坏字符串，而不是计算总好字符串。在迭代前缀之前，合并具有相同起始字符的前缀，因为较大长度的前缀可能会减少一些重复。按照以下步骤解决问题:**

*   **将变量**总计**初始化为**10<sup>N</sup>T5。****
*   **[初始化地图< int，向量<string>>](https://www.geeksforgeeks.org/map-of-vectors-in-c-stl-with-examples/)T2【MP】。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，M)** ，并执行以下任务:

    *   [在地图矢量 **mp【前缀[i]-'0 '】中推**前缀[i]** 的值**](https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/)。** 
*   **[初始化向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/) **新 _ 前缀[]** 。**
*   **使用变量 **x** 遍历地图 **mp[]** ，并执行以下任务:

    *   将变量 **mn** 初始化为 **N** 。
    *   使用变量 **p** 遍历向量 **x 秒**，并执行以下任务:
        *   将 **mn** 的值设置为 **mn** 或 **p.length()** 的最小值。
    *   使用变量 **p** 遍历向量 **x 秒**，并执行以下任务:
        *   如果 **p.length()** 小于或等于 **mn，**则将 **p** 推入[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **new_prefixes[]** 。** 
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，new_prefixes.size())** ，并执行以下任务:

    *   减去值 **int(幂(10，N–new _ prefixes[I])。长度())+ 0.5)** 来自变量**的总和。**** 
*   **执行上述步骤后，打印**合计**的值作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ Program to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Change int to long long in case of overflow!!
// Function to calculate total strings of length
// N without the given prefixes
int totalGoodStrings(int N, vector<string> prefixes)
{

    // Calculate total strings present
    int total = int(pow(10, N) + 0.5);

    // Make a map and insert the prefixes with same
    // character in a vector
    map<int, vector<string> > mp;
    for (int i = 0; i < prefixes.size(); i++) {
        mp[prefixes[i][0] - '0']
            .push_back(prefixes[i]);
    }

    // Make a new vector of prefixes strings
    vector<string> new_prefixes;

    // Iterate for each starting character
    for (auto x : mp) {

        int mn = N;

        // Iterate through the vector to calculate
        // minimum size prefix
        for (auto p : x.second) {
            mn = min(mn, int(p.length()));
        }

        // Take all the minimum prefixes in the new
        // vector of prefixes
        for (string p : x.second) {
            if (p.length() > mn) {
                continue;
            }
            new_prefixes.push_back(p);
        }
    }

    // Iterate through the new prefixes
    for (int i = 0; i < new_prefixes.size(); i++) {

        // Subtract bad strings
        total -= int(pow(10,
                         N - new_prefixes[i].length())
                     + 0.5);
    }
    return total;
}

// Driver Code
int main()
{
    int N = 5;

    vector<string> prefixes
        = { "1", "0", "911" };

    cout << totalGoodStrings(N, prefixes);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to implement the above approach
import java.util.ArrayList;
import java.util.HashMap;

class GFG
{

  // Change int to long long in case of overflow!!
  // Function to calculate total strings of length
  // N without the given prefixes
  public static int totalGoodStrings(int N, String[] prefixes) {

    // Calculate total strings present
    int total = (int) (Math.pow(10, N) + 0.5);

    // Make a map and insert the prefixes with same
    // character in a vector
    HashMap<Integer, ArrayList<String>> mp = new HashMap<Integer, ArrayList<String>>();

    for (int i = 0; i < prefixes.length; i++) {
      int key = (int) prefixes[i].charAt(0) - (int) '0';

      if (mp.containsKey(key)) {
        ArrayList<String> temp = mp.get(key);
        temp.add(prefixes[i]);
        mp.put(key, temp);
      } else {
        ArrayList<String> temp = new ArrayList<String>();
        temp.add(prefixes[i]);
        mp.put(key, temp);
      }
    }

    // Make a new vector of prefixes strings
    ArrayList<String> new_prefixes = new ArrayList<String>();

    // Iterate for each starting character
    for (Integer x : mp.keySet()) {

      int mn = N;

      // Iterate through the vector to calculate
      // minimum size prefix
      for (String p : mp.get(x)) {
        mn = Math.min(mn, p.length());
      }

      // Take all the minimum prefixes in the new
      // vector of prefixes
      for (String p : mp.get(x)) {
        if (p.length() > mn) {
          continue;
        }
        new_prefixes.add(p);
      }
    }

    // Iterate through the new prefixes
    for (int i = 0; i < new_prefixes.size(); i++) {

      // Subtract bad strings
      total -= (int) (Math.pow(10, N - new_prefixes.get(i).length()) + 0.5);
    }
    return total;
  }

  // Driver Code
  public static void main(String args[])
  {

    int N = 5;
    String[] prefixes = { "1", "0", "911" };
    System.out.println(totalGoodStrings(N, prefixes));
  }
}

// This code is contributed by gfgking.
```

## **蟒蛇 3**

```
# python Program to implement the above approach
import math

# Change int to long long in case of overflow!!
# Function to calculate total strings of length
# N without the given prefixes
def totalGoodStrings(N,  prefixes):

        # Calculate total strings present
    total = int(math.pow(10, N) + 0.5)

    # Make a map and insert the prefixes with same
    # character in a vector
    mp = {}
    for i in range(0, len(prefixes)):
        if (ord(prefixes[i][0]) - ord('0')) in mp:
            mp[ord(prefixes[i][0]) - ord('0')].append(prefixes[i])

        else:
            mp[ord(prefixes[i][0]) - ord('0')] = [prefixes[i]]

        # Make a new vector of prefixes strings
    new_prefixes = []

    # Iterate for each starting character
    for x in mp:

        mn = N

        # Iterate through the vector to calculate
        # minimum size prefix
        for p in mp[x]:
            mn = min(mn, len(p))

        # Take all the minimum prefixes in the new
        # vector of prefixes
        for p in mp[x]:
            if (len(p) > mn):
                continue

            new_prefixes.append(p)

        # Iterate through the new prefixes
    for i in range(0, len(new_prefixes)):

                # Subtract bad strings
        total -= int(pow(10, N - len(new_prefixes[i])) + 0.5)

    return total

# Driver Code
if __name__ == "__main__":

    N = 5
    prefixes = ["1", "0", "911"]
    print(totalGoodStrings(N, prefixes))

    # This code is contributed by rakeshsahni
```

## **C#**

```
// C# Program to implement the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Change int to long long in case of overflow!!
    // Function to calculate total strings of length
    // N without the given prefixes
    public static int totalGoodStrings(int N,
                                       string[] prefixes)
    {

        // Calculate total strings present
        int total = (int)(Math.Pow(10, N) + 0.5);

        // Make a map and insert the prefixes with same
        // character in a vector
        Dictionary<int, List<string> > mp
            = new Dictionary<int, List<string> >();

        for (int i = 0; i < prefixes.Length; i++) {
            int key = (int)prefixes[i][0] - (int)'0';

            if (mp.ContainsKey(key)) {
                List<string> temp = mp[key];
                temp.Add(prefixes[i]);
                mp[key] = temp;
            }
            else {
                List<string> temp = new List<string>();
                temp.Add(prefixes[i]);
                mp[key] = temp;
            }
        }

        // Make a new vector of prefixes strings
        List<string> new_prefixes = new List<string>();

        // Iterate for each starting character
        foreach(int x in mp.Keys)
        {

            int mn = N;

            // Iterate through the vector to calculate
            // minimum size prefix
            foreach(string p in mp[x])
            {
                mn = Math.Min(mn, p.Length);
            }

            // Take all the minimum prefixes in the new
            // vector of prefixes
            foreach(string p in mp[x])
            {
                if (p.Length > mn) {
                    continue;
                }
                new_prefixes.Add(p);
            }
        }

        // Iterate through the new prefixes
        for (int i = 0; i < new_prefixes.Count; i++) {

            // Subtract bad strings
            total
                -= (int)(Math.Pow(
                             10, N - new_prefixes[i].Length)
                         + 0.5);
        }
        return total;
    }

    // Driver Code
    public static void Main(string[] args)
    {

        int N = 5;
        string[] prefixes = { "1", "0", "911" };
        Console.WriteLine(totalGoodStrings(N, prefixes));
    }
}

// This code is contributed by ukasp.
```

## **java 描述语言**

```
// Javascript Program to implement the above approach

// Change int to long long in case of overflow!!
// Function to calculate total strings of length
// N without the given prefixes
function totalGoodStrings(N, prefixes) {

  // Calculate total strings present
  let total = Math.floor(Math.pow(10, N) + 0.5);

  // Make a map and insert the prefixes with same
  // character in a vector
  let mp = new Map();
  for (let i = 0; i < prefixes.length; i++) {
    let key = prefixes[i][0] - '0'.charCodeAt(0);

    if (mp.has(key)) {
      let temp = mp.get(key);
      temp.push(prefixes[i])
      mp.set(key, temp)
    } else {
      mp.set(key, [prefixes[i]])
    }
  }

  // Make a new vector of prefixes strings
  let new_prefixes = [];

  // Iterate for each starting character
  for (x of mp) {

    let mn = N;

    // Iterate through the vector to calculate
    // minimum size prefix
    for (p of x[1]) {
      mn = Math.min(mn, p.length);
    }

    // Take all the minimum prefixes in the new
    // vector of prefixes
    for (p of x[1]) {
      if (p.length > mn) {
        continue;
      }
      new_prefixes.push(p);
    }
  }

  // Iterate through the new prefixes
  for (let i = 0; i < new_prefixes.length; i++) {

    // Subtract bad strings
    total -= Math.floor(Math.pow(10, N - new_prefixes[i].length) + 0.5);
  }
  return total;
}

// Driver Code

let N = 5;

let prefixes = ["1", "0", "911"];

document.write(totalGoodStrings(N, prefixes))

// This code is contributed by saurabh_jaiswal.
```

****Output**

```
79900
```** 

*****时间复杂度:** O(M)，其中 M 是向量前缀的大小[]*
***辅助空间:** O(M*K)，*其中 K 是字符串的最大长度**