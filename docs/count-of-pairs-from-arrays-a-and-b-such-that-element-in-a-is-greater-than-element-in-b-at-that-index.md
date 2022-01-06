# 对数组 A 和 B 中的元素对进行计数，使得在该索引处 A 中的元素大于 B 中的元素

> 原文:[https://www . geeksforgeeks . org/数组 a 和 b 中的对计数-a 中的元素大于 b 中的元素-at-index/](https://www.geeksforgeeks.org/count-of-pairs-from-arrays-a-and-b-such-that-element-in-a-is-greater-than-element-in-b-at-that-index/)

给定两个大小为 **N** 的数组 **A[]** 和 **B[]** ，任务是计算最大对数，其中每对包含每个数组中的一个，这样 **A[i] > B[i]** 。此外，数组 A 可以被重新排列任意次。

**示例:**

> **输入:** A[] = {20，30，50}，B[]= {60，40，25}
> **输出:** 2
> **解释:**
> 最初:
> A[0]= 20<B[0]= 60
> A[1]= 30<B[1]= 40
> A[2]= 50>B[2]= 20
> 此数组 A[]在重新排列为{20，50，30}时:
> A[0]= 20<B[0]= 60
> A[1]= 50>B[1]= 40
> A[2]= 30>B[2]= 25
> 2 值遵循条件 A[i] > B[i]，这是这组数组的最大值。
> 
> **输入:** A[] = {10，3，7，5，8}，B[] = {8，6，2，5，9}
> **输出:** 4
> **解释:**
> 最初:
> A[0]= 10>B[0]= 8
> A[1]= 3<B[1]= 6
> A[2]= 7>B[2]= 2【2
> 此数组 A[]重新排列为{10，8，5，7，3}时:
> A[0]= 10>B[0]= 8
> A[1]= 8>B[1]= 6
> A[2]= 5>B[2]= 2
> A[3]= 7>B[3]= 5
> A[4]= 3<B[4]= 9

**进场:**思路是用[堆](https://www.geeksforgeeks.org/heap-data-structure/)的概念。既然问题中 B[]的排列无关紧要，我们可以在两个数组上执行 [max heap](https://www.geeksforgeeks.org/max-heap-in-java/) 。在执行最大堆并将值存储在两个不同的堆中之后，遍历对应于 A[]和 B[]的堆，以计数满足给定条件 **A[i] > B[i]** 的索引的数量。

下面是上述方法的实现:

## C++14

```
// C++ program to find the maximum count of
// values that follow the given condition
#include<bits/stdc++.h>
using namespace std;

// Function to find the maximum count of
// values that follow the given condition
int check(int A[], int B[], int N)
{

    // Initializing the max-heap for the array A[]
    priority_queue <int> pq1,pq2;

    // Adding the values of A[] into max heap
    for (int i = 0; i < N; i++) {
        pq1.push(A[i]);
    }

    // Adding the values of B[] into max heap
    for (int i = 0; i < N; i++) {
        pq2.push(B[i]);
    }

    // Counter variable
    int c = 0;

    // Loop to iterate through the heap
    for (int i = 0; i < N; i++) {

        // Comparing the values at the top.
        // If the value of heap A[] is greater,
        // then counter is incremented
        if (pq1.top()>pq2.top()) {
            c++;
            pq1.pop();
            pq2.pop();
        }
        else {
            if (pq2.size() == 0) {
                break;
            }
            pq2.pop();
        }
    }
    return (c);
}

// Driver code
int main()
{
    int A[] = { 10, 3, 7, 5, 8 };
    int B[] = { 8, 6, 2, 5, 9 };
    int N = sizeof(A)/sizeof(A[0]);

    cout<<(check(A, B, N));
}

// This code is contributed by mohit kumar 29   
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum count of
// values that follow the given condition

import java.util.*;
public class GFG {

    // Function to find the maximum count of
    // values that follow the given condition
    static int check(int A[], int B[], int N)
    {

        // Initializing the max-heap for the array A[]
        PriorityQueue<Integer> pq1
            = new PriorityQueue<Integer>(
Collections.reverseOrder());

        // Initializing the max-heap for the array B[]
        PriorityQueue<Integer> pq2
            = new PriorityQueue<Integer>(
Collections.reverseOrder());

        // Adding the values of A[] into max heap
        for (int i = 0; i < N; i++) {
            pq1.add(A[i]);
        }

        // Adding the values of B[] into max heap
        for (int i = 0; i < N; i++) {
            pq2.add(B[i]);
        }

        // Counter variable
        int c = 0;

        // Loop to iterate through the heap
        for (int i = 0; i < N; i++) {

            // Comparing the values at the top.
            // If the value of heap A[] is greater,
            // then counter is incremented
            if (pq1.peek().compareTo(pq2.peek()) == 1) {
                c++;
                pq1.poll();
                pq2.poll();
            }
            else {
                if (pq2.size() == 0) {
                    break;
                }
                pq2.poll();
            }
        }
        return (c);
    }

    // Driver code
    public static void main(String args[])
    {
        int A[] = { 10, 3, 7, 5, 8 };
        int B[] = { 8, 6, 2, 5, 9 };
        int N = A.length;

        System.out.println(check(A, B, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the maximum count of
# values that follow the given condition
import heapq

# Function to find the maximum count of
# values that follow the given condition
def check(A, B,N):

    # Initializing the max-heap for the array A[]
    pq1 = []
    pq2 = []

    # Adding the values of A[] into max heap
    for i in range(N):
        heapq.heappush(pq1,-A[i])

    # Adding the values of B[] into max heap
    for i in range(N):
        heapq.heappush(pq2,-B[i])

    # Counter variable
    c = 0

    # Loop to iterate through the heap
    for i in range(N):

        # Comparing the values at the top.
        # If the value of heap A[] is greater,
        # then counter is incremented
        if -pq1[0] > -pq2[0]:
            c += 1
            heapq.heappop(pq1)
            heapq.heappop(pq2)

        else:
            if len(pq2) == 0:
                break
            heapq.heappop(pq2)
    return (c)

# Driver code
A = [ 10, 3, 7, 5, 8 ]
B = [ 8, 6, 2, 5, 9 ]
N = len(A)

print(check(A, B, N))

# This code is contributed by apurva raj
```

## C#

```
// C# program to find the maximum count of
// values that follow the given condition
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum count of
// values that follow the given condition
static int check(int[] A, int[] B, int N)
{

    // Initializing the max-heap for the array A[]
    List<int> pq1 = new List<int>();

    // Initializing the max-heap for the array B[]
    List<int> pq2 = new List<int>();

    // Adding the values of A[] into max heap
    for(int i = 0; i < N; i++)
    {
        pq1.Add(A[i]);
    }

    // Adding the values of B[] into max heap
    for(int i = 0; i < N; i++)
    {
        pq2.Add(B[i]);
    }
    pq1.Sort();
    pq1.Reverse();
    pq2.Sort();
    pq2.Reverse();

    // Counter variable
    int c = 0;

    // Loop to iterate through the heap
    for(int i = 0; i < N; i++)
    {

        // Comparing the values at the top.
        // If the value of heap A[] is greater,
        // then counter is incremented
        if (pq1[0] > pq2[0])
        {
            c++;
            pq1.RemoveAt(0);
            pq2.RemoveAt(0);
        }
        else
        {
            if (pq2.Count == 0)
            {
                break;
            }
            pq2.RemoveAt(0);
        }
    }
    return c;
}

// Driver code
static public void Main()
{
    int[] A = { 10, 3, 7, 5, 8 };
    int[] B = { 8, 6, 2, 5, 9 };
    int N = A.Length;

    Console.WriteLine(check(A, B, N));
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript program to find the maximum count of
// values that follow the given condition

// Function to find the maximum count of
// values that follow the given condition
function check(A,B,N)
{
    let pq1=[];
    let pq2=[];

    // Adding the values of A[] into max heap
    for (let i = 0; i < N; i++) {
        pq1.push(A[i]);
    }

    // Adding the values of B[] into max heap
    for (let i = 0; i < N; i++) {
        pq2.push(B[i]);
    }

    pq1.sort(function(a,b){return a-b;});
    pq1.reverse();
    pq2.sort(function(a,b){return a-b;});
    pq2.reverse();

     // Counter variable
     let c = 0;

     // Loop to iterate through the heap
     for (let i = 0; i < N; i++) {

          // Comparing the values at the top.
        // If the value of heap A[] is greater,
        // then counter is incremented
        if (pq1[0] > pq2[0]) {
            c++;
            pq1.shift();
            pq2.shift();
        }
        else {
            if (pq2.length == 0) {
                break;
            }
            pq2.shift();
        }
      }
      return (c);
}

// Driver code
let A=[ 10, 3, 7, 5, 8];
let B=[8, 6, 2, 5, 9 ];
let N = A.length;
document.write(check(A, B, N));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N * log(N))