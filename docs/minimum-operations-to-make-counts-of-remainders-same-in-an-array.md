# 使数组中余数相同的最小运算

> 原文:[https://www . geeksforgeeks . org/最小操作数-剩余数量-阵列中的相同数量/](https://www.geeksforgeeks.org/minimum-operations-to-make-counts-of-remainders-same-in-an-array/)

给定一个由 **N** 个整数和一个整数 **M** 组成的数组 **arr[]** ，其中 **N % M = 0** 。任务是找到需要在数组上执行的最小操作数，使 **c <sub>0</sub> = c <sub>1</sub> = …..= c<sub>M–1</sub>= N/M**，其中 **c <sub>r</sub>** 是给定数组**中元素**的**数量，当除以 **M** 时，剩余为 r** 。在每次操作中，任何数组元素都可以增加 **1** 。

**示例:**

> **输入:** arr[] = {1，2，3}，M = 3
> **输出:** 0
> 对给定数组进行模运算后，数组变为{0，1，2}
> ，c<sub>0</sub>= c<sub>1</sub>= c<sub>2</sub>= n/M = 1。
> 因此，不需要任何额外的操作。
> 
> **输入:** arr[] = {3，2，0，6，10，12}，M = 3
> **输出:** 3
> 对给定数组进行模运算后，数组变为{0，2，0，0，1，0}
> ，计数 c <sub>0</sub> = 4，c <sub>1</sub> = 1，c <sub>2</sub> = 1。使 c<sub>0</sub>= c<sub>1</sub>= c<sub>2</sub>= n/m = 2。
> 将 1 加 6，2 加 12，则数组变为{3，2，0，7，10，14}，c<sub>0</sub>= c<sub>1</sub>= c<sub>2</sub>= n/m = 2。

**方法:**对于从 **0** 到**m–1**的每个 **i** ，找到数组中与 **i 模 m** 一致的所有元素，并将它们的索引存储在列表中。另外，创建一个名为 extra 的向量，让 **k = n / m** 。

我们必须从 **0 到 m–1**循环两次。对于从 **0 到 m–1**的每个 **i** ，如果列表中的元素多于 **k** ，则从该列表中移除多余的元素并将其添加到 extra 中。如果有比 **k** 更少的元素，那么从额外的向量中移除最后几个元素。对于每个移除的索引 **idx** ，将**arr【idx】**增加**(I–arr【idx】)% m**。

很明显，在第一次 **m** 迭代之后，每个列表最多将具有大小 **k** ，而在 **m** 更多迭代之后，所有列表将具有相同的大小，即 **k** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// number of operations required
int minOperations(int n, int a[], int m)
{
    int k = n / m;

    // To store modulos values
    vector<vector<int> > val(m);
    for (int i = 0; i < n; ++i) {
        val[a[i] % m].push_back(i);
    }

    long long ans = 0;
    vector<pair<int, int> > extra;

    for (int i = 0; i < 2 * m; ++i) {
        int cur = i % m;

        // If it's size greater than k
        // it needed to be decreased
        while (int(val[cur].size()) > k) {
            int elem = val[cur].back();
            val[cur].pop_back();
            extra.push_back(make_pair(elem, i));
        }

        // If it's size is less than k
        // it needed to be increased
        while (int(val[cur].size()) < k && !extra.empty()) {
            int elem = extra.back().first;
            int mmod = extra.back().second;
            extra.pop_back();
            val[cur].push_back(elem);
            ans += i - mmod;
        }
    }

    return ans;
}

// Driver code
int main()
{
    int m = 3;

    int a[] = { 3, 2, 0, 6, 10, 12 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << minOperations(n, a, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

static class pair
{
    int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to return the minimum
// number of operations required
static int minOperations(int n, int a[], int m)
{
    int k = n / m;

    // To store modulos values
    @SuppressWarnings("unchecked")
    Vector<Integer> []val = new Vector[m];
    for(int i = 0; i < val.length; i++)
        val[i] = new Vector<Integer>();

    for(int i = 0; i < n; ++i)
    {
        val[a[i] % m].add(i);
    }

    long ans = 0;
    Vector<pair> extra = new Vector<>();

    for(int i = 0; i < 2 * m; ++i)
    {
        int cur = i % m;

        // If it's size greater than k
        // it needed to be decreased
        while ((val[cur].size()) > k)
        {
            int elem = val[cur].lastElement();
            val[cur].removeElementAt(val[cur].size() - 1);
            extra.add(new pair(elem, i));
        }

        // If it's size is less than k
        // it needed to be increased
        while (val[cur].size() < k && !extra.isEmpty())
        {
            int elem = extra.get(extra.size() - 1).first;
            int mmod = extra.get(extra.size() - 1).second;

            extra.remove(extra.size() - 1);
            val[cur].add(elem);
            ans += i - mmod;
        }
    }
    return (int)ans;
}

// Driver code
public static void main(String[] args)
{
    int m = 3;
    int a[] = { 3, 2, 0, 6, 10, 12 };
    int n = a.length;

    System.out.print(minOperations(n, a, m));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# number of operations required
def minOperations(n, a, m):

    k = n // m

    # To store modulos values
    val = [[] for i in range(m)]
    for i in range(0, n):
        val[a[i] % m].append(i)

    ans = 0
    extra = []

    for i in range(0, 2 * m):
        cur = i % m

        # If it's size greater than k
        # it needed to be decreased
        while len(val[cur]) > k:
            elem = val[cur].pop()
            extra.append((elem, i))

        # If it's size is less than k
        # it needed to be increased
        while (len(val[cur]) < k and
               len(extra) > 0):
            elem = extra[-1][0]
            mmod = extra[-1][1]
            extra.pop()
            val[cur].append(elem)
            ans += i - mmod

    return ans

# Driver code
if __name__ == "__main__":

    m = 3

    a = [3, 2, 0, 6, 10, 12]
    n = len(a)
    print(minOperations(n, a, m))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the
// above approach
using System;
using System.Collections.Generic;
class GFG{

public class pair
{
  public int first,
             second;

  public pair(int first,
              int second) 
  {
    this.first = first;
    this.second = second;
  }   
}

// Function to return the minimum
// number of operations required
static int minOperations(int n,
                         int []a,
                         int m)
{
  int k = n / m;

  // To store modulos values
  List<int> []val =
       new List<int>[m];

  for(int i = 0;
          i < val.Length; i++)
    val[i] = new List<int>();

  for(int i = 0; i < n; ++i)
  {
    val[a[i] % m].Add(i);
  }

  long ans = 0;
  List<pair> extra =
       new List<pair>();

  for(int i = 0;
          i < 2 * m; ++i)
  {
    int cur = i % m;

    // If it's size greater than k
    // it needed to be decreased
    while ((val[cur].Count) > k)
    {
      int elem = val[cur][val[cur].Count - 1];
      val[cur].RemoveAt(val[cur].Count - 1);
      extra.Add(new pair(elem, i));
    }

    // If it's size is less than k
    // it needed to be increased
    while (val[cur].Count < k &&
           extra.Count != 0)
    {
      int elem = extra[extra.Count - 1].first;
      int mmod = extra[extra.Count - 1].second;
      extra.RemoveAt(extra.Count - 1);
      val[cur].Add(elem);
      ans += i - mmod;
    }
  }
  return (int)ans;
}

// Driver code
public static void Main(String[] args)
{
  int m = 3;
  int []a = {3, 2, 0, 6, 10, 12};
  int n = a.Length;
  Console.Write(minOperations(n, a, m));
}
}

// This code is contributed by Princi Singh
```

**Output:** 

```
3

```