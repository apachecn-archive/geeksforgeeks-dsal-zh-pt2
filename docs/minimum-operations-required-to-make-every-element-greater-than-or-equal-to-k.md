# 使每个元素大于或等于 K 所需的最小操作数

> 原文:[https://www . geesforgeks . org/minimum-operations-required-to-make-even-element-大于或等于-k/](https://www.geeksforgeeks.org/minimum-operations-required-to-make-every-element-greater-than-or-equal-to-k/)

给定一组长度 **N** 。任务是将其转换为所有元素都大于或等于 **K** 的序列。唯一允许的操作是获取序列中的两个最小元素，并用它们的 LCM 替换它们。找到所需的最小操作数。
如果不可能得到这样的阵列，打印-1。
**例:**

> **输入:** N = 4，K = 3，arr=[1 4 5 5]
> **输出:**1
> 1 和 4 的 LCM 为 4，因此用 4 替换(1，4)。
> 现在数组变成[4，4，5]。
> 此数组中的每个元素都大于或等于 k。
> 所需的操作数等于 1。
> **输入:** N = 5，K = 8，arr=[4，4，4，4]，4]
> **输出:** -1
> 无法转换给定数组。

**进场:**

*   其思想是使用优先级队列(最小堆)，它可以在日志(N)时间内处理删除和插入操作。
*   当优先级队列中的元素数量小于 2 时，将出现不可能的情况。在这种情况下，答案等于-1。
*   否则，从队列顶部取出两个元素，并用它们的 LCM 替换它。
*   这样做，直到队列顶部的最小数字小于 k

以下是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// C++ function to get
// minimum operation needed
int FindMinOperation(int a[], int n, int k)
{

    // The priority queue holds a minimum
    // element in the top position
    priority_queue<int, vector<int>,
                              greater<int> > Q;

    for (int i = 0; i < n; i++)

        // push value one by one
        // from the given array
        Q.push(a[i]);

    // store count of minimum operation needed
    int ans = 0;

    while (1) {

        // All elements are now >= k
        if (Q.top() >= k)
            break;

        // It is impossible to make as there are
        // no sufficient elements available
        if (Q.size() < 2)
            return -1;

        // Take two smallest elements and
        // replace them by their LCM
        // first smallest element
        int x = Q.top();
        Q.pop();

        // Second smallest element
        int y = Q.top();
        Q.pop();

        int z = (x * y) / __gcd(x, y);
        Q.push(z);

        // Increment the count
        ans++;
    }

    return ans;
}

// Driver Code
int main()
{

    int a[] = { 3, 5, 7, 6, 8 };
    int k = 8;
    int n = sizeof(a) / sizeof(a[0]);

    cout << FindMinOperation(a, n, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
import java.util.PriorityQueue;

class GFG
{

    // Function to calculate gcd of two numbers
    static int gcd(int a, int b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Java function to get
    // minimum operation needed
    static int FindMinOperation(int[] a, int n, int k)
    {

        // The priority queue holds a minimum
        // element in the top position
        PriorityQueue<Integer> Q = new PriorityQueue<>();

        for (int i = 0; i < n; i++)

            // push value one by one
            // from the given array
            Q.add(a[i]);

        // store count of minimum operation needed
        int ans = 0;

        while (true)
        {

            // All elements are now >= k
            if (Q.peek() >= k)
                break;

            // It is impossible to make as there are
            // no sufficient elements available
            if (Q.size() < 2)
                return -1;

            // Take two smallest elements and
            // replace them by their LCM
            // first smallest element
            int x = Q.peek();
            Q.poll();

            // Second smallest element
            int y = Q.peek();
            Q.poll();

            int z = (x * y) / gcd(x, y);
            Q.add(z);

            // Increment the count
            ans++;
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] a = { 3, 5, 7, 6, 8 };
        int k = 8;
        int n = a.length;
        System.out.println(FindMinOperation(a, n, k));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to calculate gcd of two numbers
def gcd(a, b) :

    if (a == 0) :
      return b
    return gcd(b % a, a)

# function to get 
# minimum operation needed
def FindMinOperation(a, n, k) :

    # The priority queue holds a minimum
    # element in the top position
    Q = []
    for i in range(0, n) :

      # push value one by one
      # from the given array
      Q.append(a[i])
    Q.sort()

    # store count of minimum operation needed
    ans = 0
    while (True) :

      # All elements are now >= k
      if (Q[0] >= k) :
        break

      # It is impossible to make as there are
      # no sufficient elements available
      if (len(Q) < 2) :
        return -1

      # Take two smallest elements and 
      # replace them by their LCM
      # first smallest element
      x = Q[0] 
      Q.pop(0)

      # Second smallest element
      y = Q[0] 
      Q.pop(0)
      z = (x * y) // gcd(x, y)
      Q.append(z)
      Q.sort()

      # Increment the count
      ans += 1 

    return ans

  # Driver code
a = [ 3, 5, 7, 6, 8 ]
k = 8
n = len(a)

print(FindMinOperation(a, n, k))

# This code is contributed by divyesh0720219.
```

## C#

```
// C# implementation of above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to calculate gcd of two numbers
  static int gcd(int a, int b)
  {
    if (a == 0)
      return b;
    return gcd(b % a, a);
  }

  // C# function to get 
  // minimum operation needed
  static int FindMinOperation(int[] a, int n, int k)
  {

    // The priority queue holds a minimum
    // element in the top position
    List<int> Q = new List<int>();
    for (int i = 0; i < n; i++)

      // push value one by one
      // from the given array
      Q.Add(a[i]);
    Q.Sort();

    // store count of minimum operation needed
    int ans = 0; 
    while (true)
    {

      // All elements are now >= k
      if (Q[0] >= k)
        break;

      // It is impossible to make as there are
      // no sufficient elements available
      if (Q.Count < 2)
        return -1;

      // Take two smallest elements and 
      // replace them by their LCM
      // first smallest element
      int x = Q[0]; 
      Q.RemoveAt(0);

      // Second smallest element
      int y = Q[0]; 
      Q.RemoveAt(0);
      int z = (x * y) / gcd(x, y);
      Q.Add(z);
      Q.Sort();

      // Increment the count
      ans++; 
    }
    return ans;
  }

  // Driver code
  static void Main()
  {
    int[] a = { 3, 5, 7, 6, 8 };
    int k = 8;
    int n = a.Length;

    Console.WriteLine(FindMinOperation(a, n, k));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript implementation of above approach

    // Function to calculate gcd of two numbers
    function gcd(a, b)
    {
      if (a == 0)
        return b;
      return gcd(b % a, a);
    }

    // function to get
    // minimum operation needed
    function FindMinOperation(a, n, k)
    {

      // The priority queue holds a minimum
      // element in the top position
      let Q = [];
      for (let i = 0; i < n; i++)

        // push value one by one
        // from the given array
        Q.push(a[i]);
      Q.sort(function(a, b){return a - b});

      // store count of minimum operation needed
      let ans = 0;
      while (true)
      {

        // All elements are now >= k
        if (Q[0] >= k)
          break;

        // It is impossible to make as there are
        // no sufficient elements available
        if (Q.length < 2)
          return -1;

        // Take two smallest elements and
        // replace them by their LCM
        // first smallest element
        let x = Q[0];
        Q.shift();

        // Second smallest element
        let y = Q[0];
        Q.shift();
        let z = parseInt((x * y) / gcd(x, y), 10);
        Q.push(z);
        Q.sort(function(a, b){return a - b});

        // Increment the count
        ans++;
      }
      return ans;
    }

    let a = [ 3, 5, 7, 6, 8 ];
    let k = 8;
    let n = a.length;

    document.write(FindMinOperation(a, n, k));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(NlogN)