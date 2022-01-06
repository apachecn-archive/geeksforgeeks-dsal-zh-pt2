# 初始化优先级队列的有效方法

> 原文:[https://www . geesforgeks . org/高效初始化优先级队列的方法/](https://www.geeksforgeeks.org/efficient-way-to-initialize-a-priority-queue/)

[STL 优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)是[堆数据结构](https://www.geeksforgeeks.org/heap-data-structure/)的实现。默认情况下，这是一个最大堆，可以很容易地用于[原始数据类型](https://www.geeksforgeeks.org/c-data-types/)。它有一些重要的应用可以在[这篇文章](https://www.geeksforgeeks.org/applications-priority-queue/)中找到。

优先级队列可以通过两种方式初始化，一种是逐个推送所有元素，另一种是使用它们的[构造函数](https://www.geeksforgeeks.org/constructors-c/)初始化。在本文中，我们将讨论这两种方法，并检查它们的[时间复杂性](https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/)。

**方法 1:** 最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并在优先级队列中逐个推送每个元素。在该方法中，优先级队列中的[推送方法花费 ***O(log N)*** 时间。其中 **N** 是数组中的元素个数。](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)

下面是上述方法的实现:

## C++

```
// C++ program to initialize the
// priority queue
#include <bits/stdc++.h>
using namespace std;

// Driver Code
int main()
{
    int arr[] = { 15, 25, 6, 54, 45, 26, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Initialize priority_queue
    priority_queue<int> pq;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Push the element arr[i]
        pq.push(arr[i]);
    }

    cout << "The elements in priority"
         << " Queue are: ";

    // Traverse until pq is non-empty
    while (!pq.empty()) {

        // Print the element in pq
        cout << pq.top() << " ";

        // Pop the top element
        pq.pop();
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to initialize the
// priority queue
import java.util.*;
public class GFG
{
    public static void main(String[] args)
    {
        int[] arr = { 15, 25, 6, 54, 45, 26, 12 };
        int N = arr.length;

        // Initialize priority_queue
        Vector<Integer> pq = new Vector<Integer>();

        // Traverse the array arr[]
        for (int i = 0; i < N; i++)
        {

          // Push the element arr[i]
          pq.add(arr[i]);
        }
        Collections.sort(pq);
        Collections.reverse(pq);
        System.out.print("The elements in priority" + " Queue are: ");

        // Traverse until pq is non-empty
        while (pq.size() > 0)
        {

          // Print the element in pq
          System.out.print(pq.get(0) + " ");

          // Pop the top element
          pq.remove(0);
        }
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 program to initialize the
# priority queue

# Driver Code
if __name__ == '__main__':
    arr = [15, 25, 6, 54, 45, 26, 12]
    N = len(arr)

    # Initialize priority_queue
    pq = []

    # Traverse the array arr[]
    for i in range(N):

        # Push the element arr[i]
        pq.append(arr[i])
    print("The elements in priority Queue are: ", end = "")
    pq = sorted(pq)

    # Traverse until pq is non-empty
    while (len(pq) > 0):

        # Print the element in pq
        print(pq[-1], end = " ")

        # Pop the top element
        del pq[-1]

        # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to initialize the
// priority queue
using System;
using System.Collections.Generic;
class GfG
{
  public static void Main()
  {
    int[] arr = { 15, 25, 6, 54, 45, 26, 12 };
    int N = arr.Length;

    // Initialize priority_queue
    List<int> pq = new List<int>();

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

      // Push the element arr[i]
      pq.Add(arr[i]);
    }

    pq.Sort();
    pq.Reverse();

    Console.Write("The elements in priority" + " Queue are: ");

    // Traverse until pq is non-empty
    while (pq.Count > 0) {

      // Print the element in pq
      Console.Write(pq[0] + " ");

      // Pop the top element
      pq.RemoveAt(0);
    }
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program to initialize the priority queue

    let arr = [ 15, 25, 6, 54, 45, 26, 12 ];
    let N = arr.length;

    // Initialize priority_queue
    let pq = [];

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {

      // Push the element arr[i]
      pq.push(arr[i]);
    }

    pq.sort(function(a, b){return a - b});
    pq.reverse();

    document.write("The elements in priority" + " Queue are: ");

    // Traverse until pq is non-empty
    while (pq.length > 0) {

      // Print the element in pq
      document.write(pq[0] + " ");

      // Pop the top element
      pq.shift();
    }

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
The elements in priority Queue are: 54 45 26 25 15 12 6
```

***时间复杂度:** O(N*log N)，其中 N 是数组中元素的总数。*
***辅助空间:** O(N)*

**方法 2:** 在该方法中，在初始化优先级队列时，将所有数组元素复制到优先级队列中(这种复制将使用 priority_queue 的[复制构造函数](https://www.geeksforgeeks.org/copy-constructor-in-cpp/)进行)。在这个方法中， **priority_queue** 将在内部使用构建堆方法。所以建堆法是取 **O(N)** 时间。

**语法:**

> priority_queue <int>pq(第一个元素的地址，最后一个元素的下一个的地址)；</int>

**语法为** [**阵**](https://www.geeksforgeeks.org/introduction-to-arrays/) **:**

> priority_queue <int>pq (arr，arr + N)
> 其中 arr 为数组，N 为数组的大小。</int>

**语法为** [**矢量**](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **:**

> priority_queue <int>pq(v.begin()、v . end())；
> 其中 v 为矢量。</int>

下面是上述方法的实现:

## C++

```
// C++ program to initialize the
// priority queue
#include <iostream>
#include <queue>
using namespace std;

// Driver Code
int main()
{
    int arr[] = { 15, 25, 6, 54, 45, 26, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // By this type of initialization
    // the priority_queue is using
    // build heap to make the max heap
    cout << "The elements in priority"
         << " Queue are: ";

    // Initialize priority_queue
    priority_queue<int> pq(arr, arr + N);

    // Iterate until pq is non empty
    while (!pq.empty()) {

        // Print the element
        cout << pq.top() << " ";
        pq.pop();
    }

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to initialize the
# priority queue

# Driver Code
if __name__=='__main__':

    arr = [ 15, 25, 6, 54, 45, 26, 12 ]
    N = len(arr)

    # By this type of initialization
    # the priority_queue is using
    # build heap to make the max heap
    print("The elements in priority Queue are: ", end = '')

    # Initialize priority_queue
    pq = arr
    pq.sort()

    # Iterate until pq is non empty
    while (len(pq) != 0):

        # Print the element
        print(pq[-1], end = ' ')
        pq.pop()

    # This code is contributed by rutvik_56.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Driver Code
public static void Main(string[] args)
{
    int []arr= { 15, 25, 6, 54, 45, 26, 12 };
    int N = arr.Length;

    // By this type of initialization
    // the priority_queue is using
    // build heap to make the max heap
    Console.Write("The elements in priority"
         + " Queue are: ");

    // Initialize priority_queue
    List<int> l = new List<int>(arr);
    l.Sort();

    // Iterate until pq is non empty
    while (l.Count!=0) {

        // Print the element
        Console.Write(l[l.Count-1]+ " ");
        l.RemoveAt(l.Count-1);
    }
}
}

// This code is contributed by noob2000.
```

## java 描述语言

```
<script>
// JAvaScript program to initialize the
// priority queue
let arr = [ 15, 25, 6, 54, 45, 26, 12 ];
let N = arr.length;

// By this type of initialization
// the priority_queue is using
// build heap to make the max heap
document.write("The elements in priority Queue are: ")

// Initialize priority_queue
let pq = arr;
pq.sort(function(a, b){return a - b;});

// Iterate until pq is non empty
while(pq.length != 0)

    // Print the element
    document.write(pq.pop()+" ");

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
The elements in priority Queue are: 54 45 26 25 15 12 6
```

***时间复杂度:** O(N)，其中 N 是数组中元素的总数。*
***辅助空间:** O(N)*