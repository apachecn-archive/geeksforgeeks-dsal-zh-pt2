# 通过重复从一对中减去较小的元素将数组减少到 0 的最小操作

> 原文:[https://www . geeksforgeeks . org/通过从一对中减去较小的元素来将数组减少到 0 的最小操作-重复/](https://www.geeksforgeeks.org/minimum-operations-for-reducing-array-to-0-by-subtracting-smaller-element-from-a-pair-repeatedly/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，任务是找到使所有数组元素为零所需的最小操作数。在一个操作中，选择一对元素，并从数组中的两个元素中减去较小的元素。

**示例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:** 3
> **解释:**按以下顺序选取元素:
> 操作 1:在索引{3，2}处选取元素:arr[] = {1，2，0，1}
> 操作 2:在索引{1，3}处选取元素:arr[]={1，1，0，0}
> 操作 3:在索引{2，1}处选取元素:arr[]
> 
> **输入:** arr[] = {2，2，2，2 }
> T3】输出: 2

**方法:**这个问题可以使用[优先队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)来解决。要解决以下问题，请按照以下步骤操作:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并推送优先级队列中所有大于 0 的元素。
2.  创建一个变量 **op** ，存储操作次数，并用 0 初始化。
3.  现在，迭代优先级队列 **pq** 直到其大小在每次迭代中大于 1:
    *   增加变量**的值，操作**
    *   然后选择前两个元素，比如说 **p** 和 **q** 来应用给定的操作。
    *   应用操作后，一个元素肯定会变成 0。如果另一个大于零，则将它推回到优先级队列中。
4.  重复上述操作，直到优先级队列为空。
5.  打印 **op** ，作为这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of operations required to make all
// array elements zero
int setElementstoZero(int arr[], int N)
{

    // Create a priority queue
    priority_queue<int> pq;

    // Variable to store the number
    // of operations
    int op = 0;

    for (int i = 0; i < N; i++) {
        if (arr[i] > 0) {
            pq.push(arr[i]);
        }
    }

    // Iterate over the priority queue
    // till size is greater than 1
    while (pq.size() > 1) {
        // Increment op by 1
        op += 1;

        auto p = pq.top();
        pq.pop();
        auto q = pq.top();
        pq.pop();

        // If the element is still greater
        // than zero again push it again in pq
        if (p - q > 0) {
            pq.push(p);
        }
    }

    // Return op as the answer
    return op;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << setElementstoZero(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;
class CustomComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer number1, Integer number2)
    {
        int value = number1.compareTo(number2);

        // elements are sorted in reverse order
        if (value > 0) {
            return -1;
        }
        else if (value < 0) {
            return 1;
        }
        else {
            return 0;
        }
    }
}
class GFG
{

    // Function to find the minimum number
    // of operations required to make all
    // array elements zero
    static int setElementstoZero(int arr[], int N)
    {

        // Create a priority queue
        PriorityQueue<Integer> pq
            = new PriorityQueue<Integer>(
                new CustomComparator());

        // Variable to store the number
        // of operations
        int op = 0;
        for (int i = 0; i < N; i++) {
            if (arr[i] > 0) {
                pq.add(arr[i]);
            }
        }
        // Iterate over the priority queue
        // till size is greater than 1
        while (pq.size() > 1)
        {

            // Increment op by 1
            op = op + 1;
            Integer p = pq.poll();
            Integer q = pq.poll();

            // If the element is still greater
            // than zero again push it again in pq
            if (p - q > 0) {
                pq.add(p);
            }
        }

        // Return op as the answer
        return op;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4 };
        int N = arr.length;
        System.out.println(setElementstoZero(arr, N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum number
# of operations required to make all
# array elements zero
def setElementstoZero(arr, N):

    # Create a priority queue
    pq = []

    # Variable to store the number
    # of operations
    op = 0

    for i in range(N):
        if (arr[i] > 0):
            pq.append(arr[i])

    pq.sort()

    # Iterate over the priority queue
    # till size is greater than 1
    while (len(pq) > 1):
        # Increment op by 1
        op += 1

        p = pq[len(pq) - 1]
        pq.pop()
        q = pq[len(pq)-1]
        pq.pop()

        # If the element is still greater
        # than zero again push it again in pq
        if (p - q > 0):
            pq.append(p)
        pq.sort()

    # Return op as the answer
    return op

# Driver Code
arr = [1, 2, 3, 4]
N = len(arr)
print(setElementstoZero(arr, N))

# This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum number
// of operations required to make all
// array elements zero
function setElementstoZero(arr, N)
{

    // Create a priority queue
    var pq = [];

    // Variable to store the number
    // of operations
    var op = 0;

    for(var i = 0; i < N; i++) {
        if (arr[i] > 0) {
            pq.push(arr[i]);
        }
    }

    pq.sort((a,b) => a-b);

    // Iterate over the priority queue
    // till size is greater than 1
    while (pq.length > 1) {
        // Increment op by 1
        op += 1;

        var p = pq[pq.length-1];
        pq.pop();
        var q = pq[pq.length-1];
        pq.pop();

        // If the element is still greater
        // than zero again push it again in pq
        if (p - q > 0) {
            pq.push(p);
        }
        pq.sort((a,b) => a-b);
    }

    // Return op as the answer
    return op;
}

// Driver Code
var arr = [ 1, 2, 3, 4 ];
var N = arr.length;
document.write(setElementstoZero(arr, N));

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
3
```

**时间复杂度:**O(NlogN)
T3】辅助空间: O(N)