# 给定矩阵中唯一行的计数

> 原文:[https://www . geesforgeks . org/给定矩阵中唯一行数/](https://www.geeksforgeeks.org/count-of-unique-rows-in-a-given-matrix/)

给定一个包含小写英文字母的大小为 **N*M** 的 **2D** 矩阵 arr，任务是找到给定矩阵中唯一行数。

**示例:**

> **输入:** arr[][]= { {'a '，' b '，' c '，' d'}，
> {'a '，' e '，' f '，' r'}，
> {'a '，' b '，' c '，' d'}，
> {'z '，' c '，' e '，' f'} }
> **输出:** 2
> **说明:**第二排和第四排是唯一的。
> 
> **输入:** arr[][]={{'a '，' c'}，
> {'b '，' d'}，
> {'e '，' f'}}
> **输出:** 3

**简单方法:**逐个遍历所有行，并通过与所有其他行进行比较来检查每行是否唯一。

**时间复杂度:**O(N<sup>2</sup>X M)
T5】辅助空间: O(1)

**高效方法:**使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)，我们可以将密钥存储为包含该行中所有字符的字符串，并将其频率作为值。遍历地图中的所有行，如果其频率为 1，则将其视为唯一。

下面是上述方法的实现:

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find number of unique rows
int uniqueRows(vector<vector<char> > arr)
{

    // Map to store the frequency of
    // each row as string
    unordered_map<string, int> mp;
    string t;

    for (auto x : arr) {
        t = "";
        for (auto y : x) {
            t += y;
        }

        mp[t] += 1;
    }

    int cnt = 0;

    // Counting unique rows
    for (auto x : mp) {
        if (x.second == 1) {
            cnt += 1;
        }
    }

    return cnt;
}

// Driver Code
int main()
{
    vector<vector<char> > arr = {
        { 'a', 'b', 'c', 'd' },
        { 'a', 'e', 'f', 'r' },
        { 'a', 'b', 'c', 'd' },
        { 'z', 'c', 'e', 'f' },
    };

    cout << uniqueRows(arr);
    return 0;
}
```

## 蟒蛇 3

```
# Python 3 code to implement the above approach
from collections import defaultdict

# Function to find number of unique rows
def uniqueRows(arr):

    # Map to store the frequency of
    # each row as string
    mp = defaultdict(int)
    t = ""

    for x in arr:
        t = ""
        for y in x:
            t += y

        mp[t] += 1

    cnt = 0

    # Counting unique rows
    for x in mp:
        if (mp[x] == 1):
            cnt += 1

    return cnt

# Driver Code
if __name__ == "__main__":

    arr = [
        ['a', 'b', 'c', 'd'],
        ['a', 'e', 'f', 'r'],
        ['a', 'b', 'c', 'd'],
        ['z', 'c', 'e', 'f'],
    ]

    print(uniqueRows(arr))

    # This code is contributed by ukasp.
```

## C#

```
// C# code to implement the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to find number of unique rows
static int uniqueRows(char [,]arr)
{

    // Map to store the frequency of
    // each row as string
    Dictionary<string,
               int> mp = new Dictionary<string,
                                        int>();

    string t;

    for(int i = 0; i < arr.GetLength(0); i++)
    {
        t = "";
        for(int j = 0; j < arr.GetLength(1); j++)
        {
            t += arr[i, j];
        }
        if (mp.ContainsKey(t))
        {
            mp[t] = mp[t] + 1;
        }
        else
        {
            mp.Add(t, 1);
        }
    }

    int cnt = 0;

    // Counting unique rows
    foreach(var x in mp.Keys)
    {
        if (mp[x] == 1)
        {
            cnt += 1;
        }
    }
    return cnt;
}

// Driver Code
public static void Main()
{
    char [,]arr = { { 'a', 'b', 'c', 'd' },
                    { 'a', 'e', 'f', 'r' },
                    { 'a', 'b', 'c', 'd' },
                    { 'z', 'c', 'e', 'f' }, };

    Console.Write(uniqueRows(arr));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to find number of unique rows
      function uniqueRows(arr) {

          // Map to store the frequency of
          // each row as string
          let mp = new Map();
          let t;

          for (let x of arr) {
              t = "";
              for (let y of x) {
                  t += y;
              }
              if (!mp.has(t))
                  mp.set(t, 1);
              else
                  mp.set(t, mp.get(t) + 1);
          }

          let cnt = 0;

          // Counting unique rows
          for (let [key, val] of mp) {
              if (val == 1) {
                  cnt += 1;
              }
          }
          return cnt;
      }

      // Driver Code
      let arr = [
          ['a', 'b', 'c', 'd'],
          ['a', 'e', 'f', 'r'],
          ['a', 'b', 'c', 'd'],
          ['z', 'c', 'e', 'f'],
      ];

      document.write(uniqueRows(arr));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(N*M)