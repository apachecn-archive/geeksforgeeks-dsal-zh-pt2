# 合并数组的前两个最小元素，直到所有元素都大于 K

> 原文:[https://www . geesforgeks . org/merge-数组的前两个最小元素-直到所有元素都大于-k/](https://www.geeksforgeeks.org/merge-first-two-minimum-elements-of-the-array-until-all-the-elements-are-greater-than-k/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是找到所需的合并操作数，使得数组的所有元素都大于或等于 **K** 。

元素的合并过程–

```
New Element = 
   1 * (First Minimum element) + 
   2 * (Second Minimum element)
```

**示例:**

> **输入:** arr[] = {1，2，3，9，10，12}，K = 7
> **输出:** 2
> **解释:**
> 在第一个合并操作元素 1 和 2 被移除后，
> 和元素(1*1 + 2*2 = 5)被插入数组
> {3，5，9，10，12}
> 在第二个合并操作元素 3 和 5 被移除后，
> 
> **输入:** arr[] = {52，96，13，37}，K = 10
> **输出:** 0
> **说明:**
> 数组的所有元素都已经大于 K 了。
> 因此，不需要合并操作。

**方法:**思路是用 [Min-Heap](https://www.geeksforgeeks.org/min-heap-in-java/) 存储元素，然后合并数组的两个最小元素，直到数组的最小元素大于等于 k

下面是上述方法的实现:

## C++

```
// C++ implementation to merge the
// elements of the array until all
// the array element of the array
// greater than or equal to K

#include <bits/stdc++.h>

using namespace std;

// Function to find the minimum
// operation required to merge
// elements of the array
int minOperations(int arr[], int K,
                          int size)
{
    int least, second_least,
       min_operations = 0,
       new_ele = 0, flag = 0;

    // Heap to store the elements
    // of the array and to extract
    // minimum elements of O(logN)
    priority_queue<int, vector<int>,
                 greater<int> > heap;

    // Loop to push all the elements
    // of the array into heap
    for (int i = 0; i < size; i++) {
        heap.push(arr[i]);
    }

    // Loop to merge the minimum
    // elements until there is only
    // all the elements greater than K
    while (heap.size() != 1) {

        // Condition to check minimum
        // element of the array is
        // greater than the K
        if (heap.top() >= K) {
            flag = 1;
            break;
        }

        // Merge the two minimum
        // elements of the heap
        least = heap.top();
        heap.pop();
        second_least = heap.top();
        heap.pop();
        new_ele = (1 * least) +
            (2 * second_least);
        min_operations++;
        heap.push(new_ele);
    }
    if (heap.top() >= K) {
        flag = 1;
    }
    if (flag == 1) {
        return min_operations;
    }
    return -1;
}

// Driver Code
int main()
{
    int N = 6, K = 7;
    int arr[] = { 1, 2, 3, 9, 10, 12 };
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << minOperations(arr, K, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to merge the
// elements of the array until all
// the array element of the array
// greater than or equal to K
import java.util.Collections;
import java.util.PriorityQueue;

class GFG{

// Function to find the minimum
// operation required to merge
// elements of the array
static int minOperations(int arr[], int K,
                         int size)
{
    int least, second_least,
        min_operations = 0,
        new_ele = 0, flag = 0;

    // Heap to store the elements
    // of the array and to extract
    // minimum elements of O(logN)
    PriorityQueue<Integer> heap = new PriorityQueue<>();

    // priority_queue<int, vector<int>,
    // greater<int> > heap;

    // Loop to push all the elements
    // of the array into heap
    for(int i = 0; i < size; i++)
    {
        heap.add(arr[i]);
    }

    // Loop to merge the minimum
    // elements until there is only
    // all the elements greater than K
    while (heap.size() != 1)
    {

        // Condition to check minimum
        // element of the array is
        // greater than the K
        if (heap.peek() >= K)
        {
            flag = 1;
            break;
        }

        // Merge the two minimum
        // elements of the heap
        least = heap.poll();
        second_least = heap.poll();
        new_ele = (1 * least) +
                  (2 * second_least);
        min_operations++;
        heap.add(new_ele);
    }
    if (heap.peek() >= K)
    {
        flag = 1;
    }
    if (flag == 1)
    {
        return min_operations;
    }
    return -1;
}

// Driver Code
public static void main(String[] args)
{
    int N = 6, K = 7;
    int arr[] = { 1, 2, 3, 9, 10, 12 };
    int size = arr.length;

    System.out.println(minOperations(arr, K, size));
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation to merge the
# elements of the array until all
# the array element of the array
# greater than or equal to K

# Function to find the minimum
# operation required to merge
# elements of the array
def minOperations(arr, K, size):
    least, second_least = 0, 0
    min_operations = 0
    new_ele, flag = 0, 0

    # Heap to store the elements
    # of the array and to extract
    # minimum elements of O(logN)
    heap = []

    # Loop to append all the elements
    # of the array into heap
    for i in range(size):
        heap.append(arr[i])

    heap  = sorted(heap)[::-1]

    # Loop to merge the minimum
    # elements until there is only
    # all the elements greater than K
    while (len(heap) > 0):

        # Condition to check minimum
        # element of the array is
        # greater than the K
        if (heap[-1] >= K):
            flag = 1
            break

        # Merge the two minimum
        # elements of the heap
        least = heap[-1]
        del heap[-1]
        second_least = heap[-1]
        del heap[-1]
        new_ele = (1 * least) + (2 * second_least)
        min_operations += 1
        heap.append(new_ele)

        heap = sorted(heap)[::-1]

    if (heap[-1] >= K):
        flag = 1

    if (flag == 1):
        return min_operations
    return -1

# Driver Code
if __name__ == '__main__':
    N, K = 6, 7
    arr = [1, 2, 3, 9, 10, 12]
    size = len(arr)
    print(minOperations(arr, K, size))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to merge the
// elements of the array until all
// the array element of the array
// greater than or equal to K
using System;
using System.Collections.Generic;
class GFG
{

  // Function to find the minimum
  // operation required to merge
  // elements of the array
  static int minOperations(int[] arr, int K, int size)
  {
    int least, second_least, min_operations = 0,
    new_ele = 0, flag = 0;

    // Heap to store the elements
    // of the array and to extract
    // minimum elements of O(logN)
    List<int> heap = new List<int>();

    // priority_queue<int, vector<int>,
    // greater<int> > heap;

    // Loop to push all the elements
    // of the array into heap
    for(int i = 0; i < size; i++)
    {
      heap.Add(arr[i]);
    }
    heap.Sort();
    heap.Reverse();

    // Loop to merge the minimum
    // elements until there is only
    // all the elements greater than K
    while(heap.Count != 1)
    {

      // Condition to check minimum
      // element of the array is
      // greater than the K
      if(heap[heap.Count - 1] >= K)
      {
        flag = 1;
        break;
      }

      // Merge the two minimum
      // elements of the heap
      least = heap[heap.Count - 1];
      heap.RemoveAt(heap.Count - 1);
      second_least = heap[heap.Count - 1];
      heap.RemoveAt(heap.Count - 1);
      new_ele = (1 * least) +(2 * second_least);
      min_operations++;
      heap.Add(new_ele);
      heap.Sort();
      heap.Reverse();          
    }
    if(heap[heap.Count - 1] >= K)
    {
      flag = 1;
    }
    if(flag == 1)
    {
      return min_operations;
    }
    return -1;       
  }

  // Driver Code
  static public void Main ()
  {
    int K = 7;
    int[] arr = { 1, 2, 3, 9, 10, 12 };
    int size = arr.Length;
    Console.WriteLine(minOperations(arr, K, size));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>
// Javascript implementation to merge the
// elements of the array until all
// the array element of the array
// greater than or equal to K

// Function to find the minimum
// operation required to merge
// elements of the array
function  minOperations(arr,K,size)
{
    let least, second_least,
        min_operations = 0,
        new_ele = 0, flag = 0;

    // Heap to store the elements
    // of the array and to extract
    // minimum elements of O(logN)
    let heap = [];

    // priority_queue<int, vector<int>,
    // greater<int> > heap;

    // Loop to push all the elements
    // of the array into heap
    for(let i = 0; i < size; i++)
    {
        heap.push(arr[i]);
    }

    // Loop to merge the minimum
    // elements until there is only
    // all the elements greater than K
    while (heap.length != 1)
    {

        // Condition to check minimum
        // element of the array is
        // greater than the K
        if (heap[0] >= K)
        {
            flag = 1;
            break;
        }

        // Merge the two minimum
        // elements of the heap
        least = heap.shift();
        second_least = heap.shift();
        new_ele = (1 * least) +
                  (2 * second_least);
        min_operations++;
        heap.push(new_ele);
    }
    if (heap[0] >= K)
    {
        flag = 1;
    }
    if (flag == 1)
    {
        return min_operations;
    }
    return -1;
}

// Driver Code
let N = 6, K = 7;
let arr=[1, 2, 3, 9, 10, 12];
let size = arr.length;
document.write(minOperations(arr, K, size));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2
```