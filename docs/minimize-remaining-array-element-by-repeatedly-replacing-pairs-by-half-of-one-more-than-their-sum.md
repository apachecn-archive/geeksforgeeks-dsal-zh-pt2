# 通过将数组重复替换成比其总和多一半的数组来最小化剩余的数组元素

> 原文:[https://www . geeksforgeeks . org/最小化剩余数组元素重复替换大于其和的一半的对/](https://www.geeksforgeeks.org/minimize-remaining-array-element-by-repeatedly-replacing-pairs-by-half-of-one-more-than-their-sum/)

给定一个包含第一个 **N 个**自然数的[排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 。一次操作，从[阵列](https://www.geeksforgeeks.org/arrays-in-c-cpp/)中取出一对 **(X，Y)** ，将 **(X + Y + 1) / 2** 插入[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)。任务是通过精确执行给定的操作**N–1**次和**N–1**对，找到数组中剩余的最小数组元素。如果存在多个解决方案，则打印其中任何一个。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** {2}、{ (2，4)、(3，3)、(1，3) }
> **解释:**
> 选择一对(arr[1]，arr[3])会修改数组 arr[] = {1，3，3}
> 选择一对(arr[1]，arr[2])会修改数组 arr[] = {1，3}
> 选择一对(arr[1，3]
> 
> **输入:** arr[] = {3，2，1}
> **输出:** {2}、{ (3，2)、(3，1) }

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化一个数组，比如**pairsar[]**来存储通过执行给定操作可以选择的所有对。
*   创建一个[](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)**优先级队列，说 **pq** 来存储优先级队列中的所有数组元素。**
*   **遍历 **pq** 当 **pq** 中剩余的计数元素大于 **1** 时，在每个操作[中弹出 **pq** 的前两个元素](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/) **(X，Y)** ，将 **(X，Y)** 存储在**pairsar【】**和[中，插入一个值为 **(X + Y + 1) / 2 的元素**](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)**
*   **最后，打印 **pq** 和**pairsar【】**中剩余元素的值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print the smallest element left
// in the array and the pairs by given operation
void smallestNumberLeftInPQ(int arr[], int N)
{

    // Stores array elements and return
    // the minimum element of arr[] in O(1)
    priority_queue<int> pq;

    // Stores all the pairs that can be
    // selected by the given operations
    vector<pair<int, int> > pairsArr;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        pq.push(arr[i]);
    }

    // Traverse pq while count of elements
    // left in pq greater than 1
    while (pq.size() > 1) {

        // Stores top element of pq
        int X = pq.top();

        // Pop top element of pq
        pq.pop();

        // Stores top element of pq
        int Y = pq.top();

        // Pop top element of pq
        pq.pop();

        // Insert (X + Y + 1) / 2 in pq
        pq.push((X + Y + 1) / 2);

        // Insert the pair  (X, Y)
        // in pairsArr[]
        pairsArr.push_back({ X, Y });
    }

    // Print the element left in pq
    // by performing the given operations
    cout << "{" << pq.top() << "}, ";

    // Stores count of elements
    // in pairsArr[]
    int sz = pairsArr.size();

    // Print all the pairs that can
    // be selected in given operations
    for (int i = 0; i < sz; i++) {

        // If i is the first
        // index of pairsArr[]
        if (i == 0) {
            cout << "{ ";
        }

        // Print current pairs of pairsArr[]
        cout << "(" << pairsArr[i].first
             << ", " << pairsArr[i].second << ")";

        // If i is not the last index
        // of pairsArr[]
        if (i != sz - 1) {
            cout << ", ";
        }

        // If i is the last index
        // of pairsArr[]
        if (i == sz - 1) {
            cout << " }";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 1 };

    int N = sizeof(arr) / sizeof(arr[0]);

    smallestNumberLeftInPQ(arr, N);
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
import java.util.*;

class GFG
{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }

// Function to print the smallest element left
// in the array and the pairs by given operation
static void smallestNumberLeftInPQ(int arr[], int N)
{

    // Stores array elements and return
    // the minimum element of arr[] in O(1)
    PriorityQueue<Integer> pq = new PriorityQueue<>((x, y) ->
                                    Integer.compare(y, x));

    // Stores all the pairs that can be
    // selected by the given operations
    Vector<pair > pairsArr = new Vector<>();

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {
        pq.add(arr[i]);
    }

    // Traverse pq while count of elements
    // left in pq greater than 1
    while (pq.size() > 1) {

        // Stores top element of pq
        int X = pq.peek();

        // Pop top element of pq
        pq.remove();

        // Stores top element of pq
        int Y = pq.peek();

        // Pop top element of pq
        pq.remove();

        // Insert (X + Y + 1) / 2 in pq
        pq.add((X + Y + 1) / 2);

        // Insert the pair  (X, Y)
        // in pairsArr[]
        pairsArr.add(new pair( X, Y ));
    }

    // Print the element left in pq
    // by performing the given operations
    System.out.print("{" +  pq.peek()+ "}, ");

    // Stores count of elements
    // in pairsArr[]
    int sz = pairsArr.size();

    // Print all the pairs that can
    // be selected in given operations
    for (int i = 0; i < sz; i++) {

        // If i is the first
        // index of pairsArr[]
        if (i == 0) {
            System.out.print("{ ");
        }

        // Print current pairs of pairsArr[]
        System.out.print("(" +  pairsArr.get(i).first
            + ", " +  pairsArr.get(i).second+ ")");

        // If i is not the last index
        // of pairsArr[]
        if (i != sz - 1) {
            System.out.print(", ");
        }

        // If i is the last index
        // of pairsArr[]
        if (i == sz - 1) {
            System.out.print(" }");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 2, 1 };
    int N = arr.length;
    smallestNumberLeftInPQ(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Function to print smallest
# element left in the array
# and the pairs by given operation
def smallestNumberLeftInPQ(arr, N):

    # Stores array elements and
    # return the minimum element
    # of arr[] in O(1)
    pq = []

    # Stores all the pairs that can
    # be selected by the given operations
    pairsArr = []

    # Traverse the array arr[]
    for i in range(N):
        pq.append(arr[i])
    pq = sorted(pq)

    # Traverse pq while count of
    # elements left in pq greater
    # than 1
    while (len(pq) > 1):

        # Stores top element of pq
        X = pq[-1]

        del pq[-1]

        # Stores top element of pq
        Y = pq[-1]

        # Pop top element of pq
        del pq[-1]

        # Insert (X + Y + 1) / 2
        # in pq
        pq.append((X + Y + 1) // 2)

        # Insert the pair  (X, Y)
        # in pairsArr[]
        pairsArr.append([X, Y])

        pq = sorted(pq)

    # Print element left in pq
    # by performing the given
    # operations
    print("{", pq[-1], "}, ",
          end = "")

    # Stores count of elements
    # in pairsArr[]
    sz = len(pairsArr)

    # Print the pairs that can
    # be selected in given operations
    for i in range(sz):

        # If i is the first
        # index of pairsArr[]
        if (i == 0):
            print("{ ", end = "")

        # Print pairs of pairsArr[]
        print("(", pairsArr[i][0], ",",
              pairsArr[i][1], ")", end = "")

        # If i is not the last index
        # of pairsArr[]
        if (i != sz - 1):
            print(end = ", ")

        # If i is the last index
        # of pairsArr[]
        if (i == sz - 1):
            print(end = " }")

# Driver Code
if __name__ == '__main__':

    arr = [3, 2, 1]
    N = len(arr)
    smallestNumberLeftInPQ(arr, N)

# This code is contributed by Mohit Kumar 29
```

## **C#**

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

public class pair
{
    public int first, second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to print the smallest element left
// in the array and the pairs by given operation
static void smallestNumberLeftInPQ(int[] arr,
                                   int N)
{

    // Stores array elements and return
    // the minimum element of []arr in O(1)
    List<int> pq = new List<int>();

    // Stores all the pairs that can be
    // selected by the given operations
    List<pair> pairsArr = new List<pair>();

    // Traverse the array []arr
    for(int i = 0; i < N; i++)
    {
        pq.Add(arr[i]);
    }
    pq.Sort();
    pq.Reverse();

    // Traverse pq while count of elements
    // left in pq greater than 1
    while (pq.Count > 1)
    {

        // Stores top element of pq
        int X = pq[0];

        // Pop top element of pq
        pq.RemoveAt(0);

        // Stores top element of pq
        int Y = pq[0];

        // Pop top element of pq
        pq.RemoveAt(0);

        // Insert (X + Y + 1) / 2 in pq
        pq.Add((X + Y + 1) / 2);
        pq.Sort();
        pq.Reverse();

        // Insert the pair  (X, Y)
        // in pairsArr[]
        pairsArr.Add(new pair(X, Y));
    }

    // Print the element left in pq
    // by performing the given operations
    Console.Write("{" + pq[0] + "}, ");

    // Stores count of elements
    // in pairsArr[]
    int sz = pairsArr.Count;

    // Print all the pairs that can
    // be selected in given operations
    for(int i = 0; i < sz; i++)
    {

        // If i is the first
        // index of pairsArr[]
        if (i == 0)
        {
            Console.Write("{ ");
        }

        // Print current pairs of pairsArr[]
        Console.Write("(" + pairsArr[i].first + ", " +
                            pairsArr[i].second + ")");

        // If i is not the last index
        // of pairsArr[]
        if (i != sz - 1)
        {
            Console.Write(", ");
        }

        // If i is the last index
        // of pairsArr[]
        if (i == sz - 1)
        {
            Console.Write(" }");
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int[] arr = { 3, 2, 1 };
    int N = arr.Length;

    smallestNumberLeftInPQ(arr, N);
}
}

// This code is contributed by aashish1995
```

## **java 描述语言**

```
<script>

// JavaScript program to implement
// the above approach

class pair
{
    constructor(first,second)
    {
            this.first = first;
            this.second = second;
    }

}
// Function to print the smallest element left
// in the array and the pairs by given operation
function smallestNumberLeftInPQ(arr,N)
{
    // Stores array elements and return
    // the minimum element of arr[] in O(1)
    let pq = [];

    // Stores all the pairs that can be
    // selected by the given operations
    let pairsArr = [];

    // Traverse the array arr[]
    for (let i = 0; i < N; i++)
    {
        pq.push(arr[i]);
    }

    pq.sort(function(a,b){return b-a;});

    // Traverse pq while count of elements
    // left in pq greater than 1
    while (pq.length > 1) {

        // Stores top element of pq
        let X = pq[0];

        // Pop top element of pq
        pq.shift();

        // Stores top element of pq
        let Y = pq[0];

        // Pop top element of pq
        pq.shift();

        // Insert (X + Y + 1) / 2 in pq
        pq.push(Math.floor((X + Y + 1) / 2));

        pq.sort(function(a,b){return b-a;});
        // Insert the pair  (X, Y)
        // in pairsArr[]
        pairsArr.push(new pair( X, Y ));
    }

    // Print the element left in pq
    // by performing the given operations
    document.write("{" +  pq[0]+ "}, ");

    // Stores count of elements
    // in pairsArr[]
    let sz = pairsArr.length;

    // Print all the pairs that can
    // be selected in given operations
    for (let i = 0; i < sz; i++) {

        // If i is the first
        // index of pairsArr[]
        if (i == 0) {
            document.write("{ ");
        }

        // Print current pairs of pairsArr[]
        document.write("(" +  pairsArr[i].first
            + ", " +  pairsArr[i].second+ ")");

        // If i is not the last index
        // of pairsArr[]
        if (i != sz - 1) {
            document.write(", ");
        }

        // If i is the last index
        // of pairsArr[]
        if (i == sz - 1) {
            document.write(" }");
        }
    }
}

// Driver Code
let arr=[3, 2, 1 ];
let N = arr.length;
smallestNumberLeftInPQ(arr, N);

// This code is contributed by patel2127

</script>
```

****Output:** 

```
{2}, { (3, 2), (3, 1) }
```** 

*****时间复杂度:** O(N * log(N))***

*****辅助空间:** O(N)***