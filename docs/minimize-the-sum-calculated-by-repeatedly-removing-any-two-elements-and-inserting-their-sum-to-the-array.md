# 通过重复移除任意两个元素并将它们的和插入到数组中来最小化计算的和

> 原文:[https://www . geeksforgeeks . org/通过重复移除任意两个元素并将其总和插入数组来最小化总和/](https://www.geeksforgeeks.org/minimize-the-sum-calculated-by-repeatedly-removing-any-two-elements-and-inserting-their-sum-to-the-array/)

给定 **N** 个元素，可以从列表中移除任意两个元素，记下它们的总和，并将总和添加到列表中。当列表中有多个元素时，重复这些步骤。任务是最终最小化这些选择的总和。
**例:**

> **输入:** arr[] = {1，4，7，10}
> **输出:** 39
> 选择 1 和 4，Sum = 5，arr[] = {5，7，10}
> 选择 5 和 7，Sum = 17，arr[] = {12，10}
> 选择 12 和 10， **Sum = 39** ，arr[] = {22}
> **输入:**arr[]= { 0

**方法:**为了最小化和，每一步选择的元素必须是列表中最小的元素。为了高效地做到这一点，可以使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。在每一步，当列表中有不止一个元素时，选择最小值和第二个最小值，从列表中删除它们，在更新运行总和后将它们的总和添加到列表中。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return the minimized sum
int getMinSum(int arr[], int n)
{
    int i, sum = 0;

    // Priority queue to store the elements of the array
    // and retrieve the minimum element efficiently
    priority_queue<int, vector<int>, greater<int> > pq;

    // Add all the elements
    // to the priority queue
    for (i = 0; i < n; i++)
        pq.push(arr[i]);

    // While there are more than 1 elements
    // left in the queue
    while (pq.size() > 1)
    {

        // Remove and get the minimum
        // element from the queue
        int min = pq.top();

        pq.pop();

        // Remove and get the second minimum
        // element (currently minimum)
        int secondMin = pq.top();

        pq.pop();

        // Update the sum
        sum += (min + secondMin);

        // Add the sum of the minimum
        // elements to the queue
        pq.push(min + secondMin);
    }

    // Return the minimized sum
    return sum;
}

// Driver code
int main()
{

    int arr[] = { 1, 3, 7, 5, 6 };
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << (getMinSum(arr, n));
}

// This code is contributed by mohit
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.PriorityQueue;

class GFG
{

    // Function to return the minimized sum
    static int getMinSum(int arr[], int n)
    {
        int i, sum = 0;

        // Priority queue to store the elements of the array
        // and retrieve the minimum element efficiently
        PriorityQueue<Integer> pq = new PriorityQueue<>();

        // Add all the elements
        // to the prioriry queue
        for (i = 0; i < n; i++)
            pq.add(arr[i]);

        // While there are more than 1 elements
        // left in the queue
        while (pq.size() > 1)
        {

            // Remove and get the minimum
            // element from the queue
            int min = pq.poll();

            // Remove and get the second minimum
            // element (currently minimum)
            int secondMin = pq.poll();

            // Update the sum
            sum += (min + secondMin);

            // Add the sum of the minimum
            // elements to the queue
            pq.add(min + secondMin);
        }

        // Return the minimized sum
        return sum;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 3, 7, 5, 6 };
        int n = arr.length;
        System.out.print(getMinSum(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimized sum
def getMinSum(arr, n):

    sum = 0

    # Priority queue to store the elements of the array
    # and retrieve the minimum element efficiently
    pq = []

    # Add all the elements
    # to the priority queue
    for i in range( n ):
        pq.append(arr[i])

    # While there are more than 1 elements
    # left in the queue
    while (len(pq) > 1) :

        pq.sort(reverse=True)

        # Remove and get the minimum
        # element from the queue
        min = pq[-1];

        pq.pop();

        # Remove and get the second minimum
        # element (currently minimum)
        secondMin = pq[-1];

        pq.pop();

        # Update the sum
        sum += (min + secondMin);

        # Add the sum of the minimum
        # elements to the queue
        pq.append(min + secondMin)

    # Return the minimized sum
    return sum

# Driver code
if __name__ == "__main__":

    arr = [ 1, 3, 7, 5, 6 ]
    n = len(arr)
    print(getMinSum(arr, n))

# This code is contributed by chitranayal
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to return the minimized sum
  static int getMinSum(int[] arr, int n)
  {
    int i, sum = 0;

    // Priority queue to store the elements of the array
    // and retrieve the minimum element efficiently
    List<int> pq = new List<int>();

    // Add all the elements
    // to the priority queue
    for (i = 0; i < n; i++)
    {
      pq.Add(arr[i]);
    }

    // While there are more than 1 elements
    // left in the queue
    while(pq.Count > 1)
    {
      pq.Sort();

      // Remove and get the minimum
      // element from the queue
      int min = pq[0];
      pq.RemoveAt(0);

      // Remove and get the second minimum
      // element (currently minimum)
      int secondMin = pq[0];
      pq.RemoveAt(0);

      // Update the sum
      sum += (min + secondMin);

      // Add the sum of the minimum
      // elements to the queue
      pq.Add(min + secondMin);
    }

    // Return the minimized sum
    return sum;
  }

  // Driver code
  static public void Main ()
  {
    int[] arr = { 1, 3, 7, 5, 6 };
    int n = arr.Length;
    Console.WriteLine(getMinSum(arr, n));
  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to return the minimized sum
    function getMinSum(arr,n)
    {
        let i, sum = 0;

        // Priority queue to store the elements of the array
        // and retrieve the minimum element efficiently
        let pq = [];

        // Add all the elements
        // to the prioriry queue
        for (i = 0; i < n; i++)
            pq.push(arr[i]);

        // While there are more than 1 elements
        // left in the queue
        while (pq.length > 1)
        {

            // Remove and get the minimum
            // element from the queue
            let min = pq.shift();

            // Remove and get the second minimum
            // element (currently minimum)
            let secondMin = pq.shift();

            // Update the sum
            sum += (min + secondMin);

            // Add the sum of the minimum
            // elements to the queue
            pq.push(min + secondMin);
        }

        // Return the minimized sum
        return sum;
    }

    // Driver code
    let arr=[1, 3, 7, 5, 6];
    let n = arr.length;
    document.write(getMinSum(arr, n));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
48
```

**时间复杂度:** O(N * log(N))
**辅助空间:** O(N)