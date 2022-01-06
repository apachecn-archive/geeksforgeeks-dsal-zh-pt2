# 从两个和等于 K 的数组中计数对

> 原文:[https://www . geesforgeks . org/count-pairs-from-two-array-have-sum-equal-k/](https://www.geeksforgeeks.org/count-pairs-from-two-arrays-having-sum-equal-to-k/)

给定一个整数 *K* 和两个数组 *A1* 和 *A2* ，任务是返回总对数(一个来自 *A1* 的元素和一个来自 *A2* 的元素)，总和等于 *K* 。
**注意:**数组可以有重复的元素。我们认为每一对都是不同的，唯一的限制是，(任何数组的)一个元素只能参与一对。例如，A1[] = {3，3}，A2[] = {4，4}和 K = 7，我们只考虑两对(3，4)和(3，4)
**示例:**

> **输入:** A1[] = {1，1，3，4，5，6，6}，A2[] = {1，4，4，5，7}，K = 10
> **输出:** 4
> 所有可能的对为{3，7}、{4，6}、{5，5}和{4，6}
> 
> **输入:** A1[] = {1，10，13，15}，A2[] = {3，3，12，4}，K = 13
> **输出:** 2

**进场:**

*   创建数组元素的映射 *A1* 。
*   对于数组 *A2* 中的每个元素，检查上一步创建的地图中是否存在*温度= K–A2[I]*。
*   如果*将【温度】映射为> 0* ，则将结果增加 *1* ，将*映射为【温度】T5，减少 *1* 。*
*   最后打印总计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach.

#include <bits/stdc++.h>
using namespace std;

// Function to return the count of pairs
// having sum equal to K
int countPairs(int A1[], int A2[]
                  , int n1, int n2, int K)
{
    // Initialize pairs to 0
    int res = 0;

    // create map of elements of array A1
    unordered_map<int, int> m;
    for (int i = 0; i < n1; ++i)
        m[A1[i]]++;

    // count total pairs
    for (int i = 0; i < n2; ++i) {
        int temp = K - A2[i];

        if (m[temp] != 0) {
            res++;

            // Every element can be part
            // of at most one pair.
            m[temp]--;
        }
    }

    // return total pairs
    return res;
}

// Driver program
int main()
{
    int A1[] = { 1, 1, 3, 4, 5, 6, 6 };
    int A2[] = { 1, 4, 4, 5, 7 }, K = 10;

    int n1 = sizeof(A1) / sizeof(A1[0]);
    int n2 = sizeof(A2) / sizeof(A2[0]);

    // function call to print required answer
    cout << countPairs(A1, A2, n1, n2, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach.
import java.util.*;
class GfG {

// Function to return the count of pairs
// having sum equal to K
static int countPairs(int A1[], int A2[] , int n1, int n2, int K)
{
    // Initialize pairs to 0
    int res = 0;

    // create map of elements of array A1
    Map<Integer, Integer> m = new HashMap<Integer, Integer> ();
    for (int i = 0; i < n1; ++i)
    {
        if(m.containsKey(A1[i]))
        m.put(A1[i], m.get(A1[i]) + 1);
        else
        m.put(A1[i], 1);
    }

    // count total pairs
    for (int i = 0; i < n2; ++i) {
        int temp = K - A2[i];

        if (m.containsKey(temp) && m.get(temp) != 0) {
            res++;

            // Every element can be part
            // of at most one pair.
            m.put(temp, m.get(A1[i]) - 1);
        }
    }

    // return total pairs
    return res;
}

// Driver program
public static void main(String[] args)
{
    int A1[] = { 1, 1, 3, 4, 5, 6, 6 };
    int A2[] = { 1, 4, 4, 5, 7 }, K = 10;

    int n1 = A1.length;
    int n2 = A2.length;

    // function call to print required answer
    System.out.println(countPairs(A1, A2, n1, n2, K));
}
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to return the count of
# pairs having sum equal to K
def countPairs(A1, A2, n1, n2, K):

    # Initialize pairs to 0
    res = 0

    # Create dictionary of elements
    # of array A1
    m = dict()
    for i in range(0, n1):
        if A1[i] not in m.keys():
            m[A1[i]] = 1
        else:
            m[A1[i]] = m[A1[i]] + 1

    # count total pairs
    for i in range(0, n2):
        temp = K - A2[i]
        if temp in m.keys():
            res = res + 1

            # Every element can be part
            # of at most one pair
            m[temp] = m[temp] - 1

    # return total pairs
    return res

# Driver Code
A1 = [1, 1, 3, 4, 5, 6 ,6]
A2 = [1, 4, 4, 5, 7]
K = 10

n1 = len(A1)
n2 = len(A2)

# function call to print required answer
print(countPairs(A1, A2, n1, n2, K))

# This code is contributed
# by Shashank_Sharma
```

## C#

```
// C# implementation of above approach.
using System;
using System.Collections.Generic;

class GfG
{

// Function to return the count of pairs
// having sum equal to K
static int countPairs(int []A1, int []A2 ,
                        int n1, int n2, int K)
{
    // Initialize pairs to 0
    int res = 0;

    // create map of elements of array A1
    Dictionary<int,int> m = new Dictionary<int,int> ();
    for (int i = 0; i < n1; ++i)
    {
        int a;
        if(m.ContainsKey(A1[i]))
        {
            a = m[A1[i]] + 1;
            m.Remove(A1[i]);
            m.Add(A1[i], a);
        }
        else
        m.Add(A1[i], 1);
    }

    // count total pairs
    for (int i = 0; i < n2; ++i)
    {
        int temp = K - A2[i];

        if (m.ContainsKey(temp) && m[temp] != 0)
        {
            res++;

            // Every element can be part
            // of at most one pair.
            m.Remove(temp);
            m.Add(temp, m[A1[i]] - 1);
        }
    }

    // return total pairs
    return res;
}

// Driver program
public static void Main()
{
    int []A1 = { 1, 1, 3, 4, 5, 6, 6 };
    int []A2 = { 1, 4, 4, 5, 7 };
    int K = 10;

    int n1 = A1.Length;
    int n2 = A2.Length;

    // function call to print required answer
    Console.WriteLine(countPairs(A1, A2, n1, n2, K));
}
}

/* This code contributed by PrinciRaj1992 */
```

**Output:** 

```
4
```

**时间复杂度:** O(N+M)

**辅助空间:** O(N+M)