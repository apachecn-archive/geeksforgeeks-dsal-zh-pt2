# 阵列中对(I，j)的计数，使得 arr[i]是 arr[j]

的因子

> 原文:[https://www . geeksforgeeks . org/数组中的对数 I-j-arri 是 arrj 的倍数/](https://www.geeksforgeeks.org/count-of-pairs-i-j-in-the-array-such-that-arri-is-a-factor-of-arrj/)

给定整数数组 **arr** ，任务是计算对的数量 **(i，j)** ，其中 **i < j** 使得**arr【j】% arr【I】= 0**。
**举例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 5
> **输入:** arr[] = {1，1，2，2，3，3}
> **输出:** 11

**方法 1:**
迭代数组的所有对，并不断增加满足所需条件的对的计数。
以下代码是上述方法的实现:

## C++

```
// C++ Program to find
// the number of pairs
// (i, j) such that arr[i]
// is a factor of arr[j]

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of Pairs
int numPairs(int arr[], int n)
{
    int ans = 0;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[j] % arr[i] == 0)
                ans++;
        }
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 1, 2, 2, 3, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << numPairs(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the number of pairs
// (i, j) such that arr[i] is a factor of arr[j]
import java.util.*;
import java.lang.*;
class GFG{

// Function to return the
// count of Pairs
static int numPairs(int arr[], int n)
{
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            if (arr[j] % arr[i] == 0)
                ans++;
        }
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 2, 2, 3, 3 };
    int n = arr.length;

    System.out.println(numPairs(arr, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the number
# of pairs (i, j) such that arr[i]
# is a factor of arr[j]

# Function to return the
# count of Pairs
def numPairs(arr, n):

    ans = 0
    for i in range(n):
        for j in range(i + 1, n):

            if arr[j] % arr[i] == 0:
                ans += 1

    return ans

# Driver code
arr = [ 1, 1, 2, 2, 3, 3 ]
n = len(arr)

print(numPairs(arr, n))

# This code is contributed by divyamohan123
```

## C#

```
// C# Program to find the number of pairs
// (i, j) such that arr[i] is a factor of arr[j]
using System;

class GFG{

// Function to return the
// count of Pairs
static int numPairs(int []arr, int n)
{
    int ans = 0;
    for(int i = 0; i < n; i++)
    {
       for(int j = i + 1; j < n; j++)
       {
          if (arr[j] % arr[i] == 0)
              ans++;
       }
    }
    return ans;
}

// Driver code
public static void Main()
{
    int []arr = { 1, 1, 2, 2, 3, 3 };
    int n = arr.Length;

    Console.Write(numPairs(arr, n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

    // Javascript Program to find
    // the number of pairs
    // (i, j) such that arr[i]
    // is a factor of arr[j]

    // Function to return the
    // count of Pairs
    function numPairs(arr, n)
    {
        let ans = 0;
        for (let i = 0; i < n; i++) {
            for (let j = i + 1; j < n; j++) {
                if (arr[j] % arr[i] == 0)
                    ans++;
            }
        }
        return ans;
    }

    let arr = [ 1, 1, 2, 2, 3, 3 ];
    let n = arr.length;

    document.write(numPairs(arr, n));

</script>
```

**Output:** 

```
11
```

**方法 2:** 将所有数组元素的索引存储在[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。遍历地图，每出现一个元素:

*   将相同元素的出现添加到当前出现之后。
*   使用[上限](https://www.geeksforgeeks.org/upper_bound-in-cpp/)将当前出现的所有倍数的出现相加

下面的代码是上述方法的实现:

## C++

```
// C++ Program to find
// the number of pairs
// (i, j) such that arr[i]
// is a factor of arr[j]

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of Pairs
int numPairs(int arr[], int n)
{
    map<int, vector<int> > mp;
    int mx = 0;
    for (int i = 0; i < n; i++) {

        // Update the maximum
        mx = max(mx, arr[i]);

        // Store the indices of
        // every element
        mp[arr[i]].push_back(i);
    }

    int ans = 0;
    for (auto i : mp) {

        int ctr = 1;

        // Access all indices of i
        for (int j : i.second) {

            // Add the number of
            // occurences of i
            // after j-th index
            ans += i.second.size() - ctr;

            // Traverse all multiples of i
            for (int k = 2 * i.first;
                 k <= mx;
                 k += i.first) {

                // Find their occurrences
                // after the j-th index
                int numGreater = 0;
                if (mp.find(k) != mp.end())
                    numGreater
                        = int(
                            mp[k]
                                .end()
                            - upper_bound(
                                  mp[k].begin(),
                                  mp[k].end(), j));
                // Add the count
                ans += numGreater;
            }
            ctr++;
        }
    }

    return ans;
}
// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << numPairs(arr, n) << endl;
    return 0;
}
```

**Output:** 

```
5
```