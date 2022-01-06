# 给定范围内 M 次循环运算后出现的最大整数

> 原文:[https://www . geesforgeks . org/m 后最大发生整数-循环-给定范围内的操作/](https://www.geeksforgeeks.org/maximum-occurred-integers-after-m-circular-operations-in-given-range/)

给定一个整数 **N** 和一个由范围**【1，N】**中的 **M** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 。**(M–1)**需要进行操作。在每次 **i <sup>th</sup>** 操作中，循环遍历从**arr【I】**到**arr【I+1】**范围内的每一个连续元素。任务是完成 **M** 操作后，按排序顺序打印访问次数最多的元素。

**示例:**

> **输入:** N = 4，arr[] = {1，2，1，2}
> **输出:** 1 2
> **解释:**
> 运算 1:1–>2。
> 操作 2:2–>3–>4–>1。
> 操作 3:1–>2。
> 完成三次运算后，最大出现整数为{1，2}。
> 因此，打印{1，2}
> 
> **输入:** N = 6，arr[] = {1，2，1，2，3 }
> T3】输出: 1 2 3

**方法:**按照以下步骤解决问题:

*   创建一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来计算一个元素被访问的次数，变量**最大访问次数**来存储任何元素的最大访问次数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下操作:
    *   从 **A[i]** 中的当前元素开始，访问循环( **mod N** 中的所有连续元素，直到 **A[i+1]** 。
    *   在每次迭代中，将其访问次数**增加 1** ，并在**最大访问次数**变量中记录最高访问次数。
    *   完成每一轮后，将最后访问的元素的**计数增加 1** 。
*   [查找地图](https://www.geeksforgeeks.org/program-to-find-frequency-of-each-element-in-a-vector-using-map-in-c/)中存储的最大频率(比如 **maxFreq** )。
*   完成上述步骤后，[迭代地图](https://www.geeksforgeeks.org/iterate-map-java/)并打印具有频率的元素 **maxFreq** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// occurred integer after completing
// all circular operations
void mostvisitedsector(int N, vector<int>& A)
{
    // Stores the highest visit count
    // for any element
    int maxVisited = 0;

    // Stores the number of times an
    // element is visited
    map<int, int> mp;

    // Iterate over the array
    for (int i = 0; i < A.size() - 1; i++) {

        int start = A[i] % N;
        int end = A[i + 1] % N;

        // Iterate over the range
        // circularly form start to end
        while (start != end) {

            // Count number of times an
            // element is visited
            if (start == 0) {

                // Increment frequency
                // of N
                mp[N]++;

                // Update maxVisited
                if (mp[N] > maxVisited) {
                    maxVisited = mp[N];
                }
            }
            else {

                // Increment frequency
                // of start
                mp[start]++;

                // Update maxVisited
                if (mp[start] > maxVisited) {
                    maxVisited = mp[start];
                }
            }

            // Increment the start
            start = (start + 1) % N;
        }
    }

    // Increment the count for the last
    // visited element
    mp[A.back()]++;
    if (mp[A.back()] > maxVisited) {
        maxVisited = mp[A.back()];
    }

    // Print most visited elements
    for (auto x : mp) {
        if (x.second == maxVisited) {
            cout << x.first << " ";
        }
    }
}

// Driver Code
int main()
{
    int N = 4;
    vector<int> arr = { 1, 2, 1, 2 };

    // Function Call
    mostvisitedsector(N, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find the maximum
// occurred integer after completing
// all circular operations
static void mostvisitedsector(int N,
                              ArrayList<Integer> A)
{

    // Stores the highest visit count
    // for any element
    int maxVisited = 0;

    // Stors the number of times an
    // element is visited
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // Iterate over the array
    for(int i = 0; i < A.size() - 1; i++)
    {
        int start = A.get(i) % N;
        int end = A.get(i + 1) % N;

        // Iterate over the range
        // circularly form start to end
        while (start != end)
        {

            // Count number of times an
            // element is visited
            if (start == 0)
            {

                // Increment frequency
                // of N
                if (mp.containsKey(N))
                    mp.put(N, mp.get(N) + 1);
                else
                    mp.put(N, 1);

                // Update maxVisited
                if (mp.get(N) > maxVisited)
                {
                    maxVisited = mp.get(N);
                }
            }
            else
            {

                // Increment frequency
                // of start
                if (mp.containsKey(start))
                    mp.put(start, mp.get(start) + 1);
                else
                    mp.put(start, 1);

                // Update maxVisited
                if (mp.get(start) > maxVisited)
                {
                    maxVisited = mp.get(start);
                }
            }

            // Increment the start
            start = (start + 1) % N;
        }
    }

    // Increment the count for the last
    // visited element
    int last = A.get(A.size() - 1);
    if (mp.containsKey(last))
        mp.put(last, mp.get(last) + 1);
    else
        mp.put(last, 1);
    if (mp.get(last) > maxVisited)
    {
        maxVisited = mp.get(last);
    }

    // Print most visited elements
    for(Map.Entry x : mp.entrySet())
    {
        if ((int)x.getValue() == maxVisited)
        {
            System.out.print(x.getKey() + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;

    ArrayList<Integer> arr = new ArrayList<Integer>(
        Arrays.asList(1, 2, 1, 2));

    // Function Call
    mostvisitedsector(N, arr);
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum
# occurred integer after completing
# all circular operations
def mostvisitedsector(N, A):

    # Stores the highest visit count
    # for any element
    maxVisited = 0

    # Stors the number of times an
    # element is visited
    mp = {}

    # Iterate over the array
    for i in range(0, len(A) - 1):
        start = A[i] % N
        end = A[i + 1] % N

        # Iterate over the range
        # circularly form start to end
        while (start != end):

            # Count number of times an
            # element is visited
            if (start == 0):

                # Increment frequency
                # of N
                if N in mp:
                    mp[N] = mp[N] + 1
                else:
                    mp[N] = 1

                # Update maxVisited
                if (mp[N] > maxVisited):
                    maxVisited = mp[N]

            else:

                # Increment frequency
                # of start
                if start in mp:
                    mp[start] = mp[start] + 1
                else:
                    mp[start] = 1

                # Update maxVisited
                if (mp[start] > maxVisited):
                    maxVisited = mp[start]

            # Increment the start
            start = (start + 1) % N

    # Increment the count for the last
    # visited element
    if A[-1] in mp:
        mp[A[-1]] = mp[A[-1]] + 1

    if (mp[A[-1]] > maxVisited):
        maxVisited = mp[A[-1]]

    # Print most visited elements
    for x in mp:
        if (mp[x] == maxVisited):
            print(x, end = ' ')

# Driver Code
if __name__ == '__main__':

    N = 4
    arr = [ 1, 2, 1, 2 ]

    # Function Call
    mostvisitedsector(N, arr)

# This code is contributed by akhilsaini
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to find the maximum
// occurred integer after completing
// all circular operations
static void mostvisitedsector(int N, ArrayList A)
{

    // Stores the highest visit count
    // for any element
    int maxVisited = 0;

    // Stors the number of times an
    // element is visited
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Iterate over the array
    for(int i = 0; i < A.Count - 1; i++)
    {
        int start = (int)A[i] % N;
        int end = (int)A[i + 1] % N;

        // Iterate over the range
        // circularly form start to end
        while (start != end)
        {

            // Count number of times an
            // element is visited
            if (start == 0)
            {

                // Increment frequency
                // of N
                if (mp.ContainsKey(N))
                    mp[N] = mp[N] + 1;
                else
                    mp[N] = 1;

                // Update maxVisited
                if (mp[N] > maxVisited)
                {
                    maxVisited = mp[N];
                }
            }
            else
            {

                // Increment frequency
                // of start
                if (mp.ContainsKey(start))
                    mp[start] = mp[start] + 1;
                else
                    mp[start] = 1;

                // Update maxVisited
                if (mp[start] > maxVisited)
                {
                    maxVisited = mp[start];
                }
            }

            // Increment the start
            start = (start + 1) % N;
        }
    }

    // Increment the count for the last
    // visited element
    int last_element = (int)A[A.Count - 1];

    if (mp.ContainsKey(last_element))
        mp[last_element] = mp[last_element] + 1;
    else
        mp[last_element] = 1;

    if (mp[last_element] > maxVisited)
    {
        maxVisited = mp[last_element];
    }

    // Print most visited elements
    foreach(var x in mp)
    {
        if ((int)x.Value == maxVisited)
        {
            Console.Write(x.Key + " ");
        }
    }
}

// Driver Code
public static void Main()
{
    int N = 4;
    ArrayList arr = new ArrayList(){ 1, 2, 1, 2 };

    // Function Call
    mostvisitedsector(N, arr);
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum
// occurred integer after completing
// all circular operations
function mostvisitedsector(N, A)
{

    // Stores the highest visit count
    // for any element
    var maxVisited = 0;

    // Stors the number of times an
    // element is visited
    var mp = new Map();

    // Iterate over the array
    for (var i = 0; i < A.length - 1; i++) {

        var start = A[i] % N;
        var end = A[i + 1] % N;

        // Iterate over the range
        // circularly form start to end
        while (start != end) {

            // Count number of times an
            // element is visited
            if (start == 0) {

                // Increment frequency
                // of N
                if(mp.has(N))
                    mp.set(N, mp.get(N)+1);
                else
                    mp.set(N, 1);

                // Update maxVisited
                if (mp.get(N) > maxVisited) {
                    maxVisited = mp.get(N);
                }
            }
            else {

                // Increment frequency
                // of start
                if(mp.has(start))
                    mp.set(start, mp.get(start)+1)
                else
                    mp.set(start, 1);

                // Update maxVisited
                if (mp.get(start) > maxVisited) {
                    maxVisited = mp.get(start);
                }
            }

            // Increment the start
            start = (start + 1) % N;
        }
    }

    // Increment the count for the last
    // visited element
    var back = A[A.length-1];
    if(mp.has(back))
        mp.set(back, mp.get(back)+1)
    else
        mp.set(back, 1);

    if (mp.get(back) > maxVisited) {
        maxVisited = mp.get(back);
    }

    // Print most visited elements
    mp.forEach((value, key) => {

        if (value == maxVisited) {
            document.write(key+" ");
        }
    });
}

// Driver Code
var N = 4;
var arr = [1, 2, 1, 2];

// Function Call
mostvisitedsector(N, arr);

// This code is contributed by importantly.
</script>
```

**Output:** 

```
1 2
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N)*