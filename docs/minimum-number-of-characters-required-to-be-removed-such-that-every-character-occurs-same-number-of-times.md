# 需要删除的最少字符数，使得每个字符出现的次数相同

> 原文:[https://www . geeksforgeeks . org/需要删除的最小字符数-每个字符出现的次数相同/](https://www.geeksforgeeks.org/minimum-number-of-characters-required-to-be-removed-such-that-every-character-occurs-same-number-of-times/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是找到需要删除的最小字符数，以使字符串中每个不同的字符出现相同的次数。

**示例:**

> **输入:**S = " abbccdddd "
> **输出:** 4
> **解释:**去掉一个出现的字符‘a’、‘c’和两个出现的‘d’将字符串修改为“bbccdd”。因此，字符串中的每个字符出现的次数都相同。
> 
> **输入:**S = " geeks forgeeks "
> T3】输出: 5
> **解释:**去掉一个出现的‘r’、‘f’、‘o’，去掉两个出现的‘e’将 S 修饰为“geeks”。

**方法:**想法是使用[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)和[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。按照以下步骤解决问题:

*   初始化一个地图<char int="">说**计数地图**和一个多集< int >说**计数多集**来存储每个字符的[频率。](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)</char>
*   将变量**和**初始化为 INT_MAX，以存储要删除的最小字符数。
*   [遍历 **countMap 中的字符串**](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** 和**S【I】**的增量计数。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **countMap** 并在 **countMultiset 中插入字符的频率。**
*   找到多集的大小**计数多集**并将其存储在一个变量中，比如 **m.**
*   [遍历多集](https://www.geeksforgeeks.org/multiset-begin-and-end-function-in-c-stl/) **计数多集**并将 **ans** 更新为 **ans = min (ans，(N-(m-I)* *(it)))**并将 **i** 递增 **1** 。
*   最后，完成以上步骤后，将答案打印为 **ans。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of
// character removals required to make
// frequency of all distinct characters the same
int minimumDeletion(string s, int n)
{
    // Stores the frequency
    // of each character
    map<char, int> countMap;

    // Traverse the string
    for (int i = 0; i < n; i++) {
        countMap[s[i]]++;
    }

    // Stores the frequency of each
    // character in sorted order
    multiset<int> countMultiset;

    // Traverse the Map
    for (auto it : countMap) {

        // Insert the frequency in multiset
        countMultiset.insert(it.second);
    }

    // Stores the count of elements
    // required to be removed
    int ans = INT_MAX;

    int i = 0;

    // Stores the size of multiset
    int m = countMultiset.size();

    // Traverse the multiset
    for (auto j : countMultiset) {
        // Update the ans
        ans = min(ans, n - (m - i) * j);

        // Increment i by 1
        i++;
    }

    // Return
    return ans;
}

// Driver Code
int main()
{
    // Input
    string S = "geeksforgeeks";
    int N = S.length();

    cout << minimumDeletion(S, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find minimum number of
// character removals required to make
// frequency of all distinct characters the same
static int minimumDeletion(String s, int n)
{

    // Stores the frequency
    // of each character
    HashMap<Character, Integer> countMap = new HashMap<>();

    // Traverse the string
    for(int i = 0; i < n; i++)
    {
        char ch = s.charAt(i);
        countMap.put(ch,
                     countMap.getOrDefault(ch, 0) + 1);
    }

    // Stores the frequency of each
    // character in sorted order
    ArrayList<Integer> countMultiset = new ArrayList<>(
        countMap.values());
    Collections.sort(countMultiset);

    // Stores the count of elements
    // required to be removed
    int ans = Integer.MAX_VALUE;

    int i = 0;

    // Stores the size of multiset
    int m = countMultiset.size();

    // Traverse the multiset
    for(int j : countMultiset)
    {

        // Update the ans
        ans = Math.min(ans, n - (m - i) * j);

        // Increment i by 1
        i++;
    }

    // Return
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // Input
    String S = "geeksforgeeks";
    int N = S.length();

    System.out.println(minimumDeletion(S, N));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find minimum number of
# character removals required to make
# frequency of all distinct characters the same
def minimumDeletion(s, n):

    # Stores the frequency
    # of each character
    countMap = {}

    # Traverse the string
    for i in s:
        countMap[i] = countMap.get(i, 0) + 1

    # Stores the frequency of each
    # character in sorted order
    countMultiset = []

    # Traverse the Map
    for it in countMap:

        # Insert the frequency in multiset
        countMultiset.append(countMap[it])

    # Stores the count of elements
    # required to be removed
    ans = sys.maxsize + 1

    i = 0

    # Stores the size of multiset
    m = len(countMultiset)

    # Traverse the multiset
    for j in sorted(countMultiset):

        # Update the ans
        ans = min(ans, n - (m - i) * j)

        # Increment i by 1
        i += 1

    # Return
    return ans

# Driver Code
if __name__ == '__main__':

    # Input
    S = "geeksforgeeks"
    N = len(S)

    print (minimumDeletion(S, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System.Collections.Generic;
using System;

class GFG{

// Function to find minimum number of
// character removals required to make
// frequency of all distinct characters the same
static int minimumDeletion(string s, int n)
{

    // Stores the frequency
    // of each character
    Dictionary<char,
               int> countMap = new Dictionary<char,
                                              int>();

    // Traverse the string
    for(int i = 0; i < n; i++)
    {
        if (countMap.ContainsKey(s[i]) == true)
        {
            countMap[s[i]] += 1;
        }
        else
        {
            countMap[s[i]] = 1;
        }
    }

    // Stores the frequency of each
    // character in sorted order
    List<int> countMultiset = new List<int>();
    foreach(var values in countMap.Values)
    {
        countMultiset.Add(values);
    }
    countMultiset.Sort();

    // Stores the count of elements
    // required to be removed
    int ans = 100000000;
    int index = 0;

    // Stores the size of multiset
    int m = countMultiset.Count;

    // Traverse the multiset
    foreach(var j in countMultiset)
    {

        // Update the ans
        ans = Math.Min(ans, n - (m - index) * j);

        // Increment i by 1
        index++;
    }

    // Return
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Input
    string S = "geeksforgeeks";
    int N = S.Length;

    Console.WriteLine(minimumDeletion(S, N));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find minimum number of
// character removals required to make
// frequency of all distinct characters the same
function minimumDeletion(s, n)
{
    // Stores the frequency
    // of each character
    var countMap = new Map();

    // Traverse the string
    for (var i = 0; i < n; i++) {
        if(countMap.has(s[i]))
        {
            countMap.set(s[i], countMap.get(s[i])+1);
        }
        else
        {
            countMap.set(s[i], 1);
        }
    }

    // Stores the frequency of each
    // character in sorted order
    var countMultiset = [];

    // Traverse the Map
    countMap.forEach((value, key) => {
        // Insert the frequency in multiset
        countMultiset.push(value);
    });

    countMultiset.sort();
    // Stores the count of elements
    // required to be removed
    var ans = 1000000000;

    var i = 0;

    // Stores the size of multiset
    var m = countMultiset.length;

    // Traverse the multiset
    countMultiset.forEach(j => {
    // Update the ans
        ans = Math.min(ans, n - (m - i) * j);

        // Increment i by 1
        i++; 
    });

    // Return
    return ans;
}

// Driver Code
// Input
var S = "geeksforgeeks";
var N = S.length;
document.write( minimumDeletion(S, N));

</script>
```

**Output:** 

```
5
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(1)*