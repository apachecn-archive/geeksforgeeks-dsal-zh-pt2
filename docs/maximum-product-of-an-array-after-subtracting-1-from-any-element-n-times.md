# 任意元素 N 次减去 1 后的数组最大乘积

> 原文:[https://www . geeksforgeeks . org/任意元素 n 次减 1 后的最大数组乘积/](https://www.geeksforgeeks.org/maximum-product-of-an-array-after-subtracting-1-from-any-element-n-times/)

给定一个大小为 **M** 的正整数[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **N** ，任务是在从任意元素 **N** 中减去 **1** 的次数后，最大化数组的[乘积](https://www.geeksforgeeks.org/program-for-product-of-array/)

**示例**:

> **输入** : M = 5，arr[] = {5，1，7，8，3}，N = 2
> **输出** : 630
> **解释**:arr[3]2 次减 1 后，数组变成{5，1，7，6，3}积= 630
> **输入** : M = 2，arr[] = {2，2}，N = 4
> **输出** : 0

**逼近** ***:*** 借助 [max-heap](https://www.geeksforgeeks.org/max-heap-in-java/) 可以解决任务，按照以下步骤解决问题:

*   将所有元素插入最大堆
*   从最大堆中弹出最上面的元素，从中减去 1，也减去 N
*   将弹出的元素插入最大堆
*   继续此过程，直到 N > 0
*   最大乘积将是最大堆中所有元素的乘积

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// product of the array
int getMax(int m, int arr[], int n)
{

    // Max-heap
    priority_queue<int> q;

    // Store all the elements inside max-heap
    for (int i = 0; i < m; i++)
        q.push(arr[i]);

    // n operations
    while (n--) {
        int x = q.top();
        q.pop();

        // Decrement x
        --x;

        // Push back x inside the heap
        q.push(x);
    }

    // Store the max product possible
    int ans = 1;
    while (!q.empty()) {
        ans *= q.top();
        q.pop();
    }

    return ans;
}

// Driver Code
int main()
{
    int M = 5;
    int arr[5] = { 5, 1, 7, 8, 3 };
    int N = 2;

    cout << getMax(M, arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

    // Function to find the maximum
    // product of the array
    static Integer getMax(int m, Integer arr[], int n)
    {

        // Max-heap
        PriorityQueue<Integer> q
            = new PriorityQueue<Integer>(
                Collections.reverseOrder());

        // Store all the elements inside max-heap
        for (int i = 0; i < m; i++)
            q.add(arr[i]);

        // n operations
        while (n-- != 0) {
            Integer x = q.poll();

            // Decrement x
            --x;

            // Push back x inside the heap
            q.add(x);
        }

        // Store the max product possible
        Integer ans = 1;
        while (q.size() != 0) {
            ans *= q.poll();
        }

        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int M = 5;
        Integer arr[] = { 5, 1, 7, 8, 3 };
        int N = 2;

        System.out.println(getMax(M, arr, N));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# python program for the above approach
from queue import PriorityQueue

# Function to find the maximum
# product of the array
def getMax(m, arr, n):

        # Max-heap
    q = PriorityQueue()

    # Store all the elements inside max-heap
    for i in range(0, m):
        q.put(-arr[i])

        # n operations
    while (n):
        n -= 1
        x = -q.get()

        # Decrement x
        x -= 1

        # Push back x inside the heap
        q.put(-x)

        # Store the max product possible
    ans = 1
    while (not q.empty()):
        ans *= -q.get()

    return ans

# Driver Code
if __name__ == "__main__":

    M = 5
    arr = [5, 1, 7, 8, 3]
    N = 2

    print(getMax(M, arr, N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG
{

    // Function to find the maximum
    // product of the array
    static int getMax(int m, int []arr, int n)
    {

        // Max-heap
        List<int> q
            = new List<int>();

        // Store all the elements inside max-heap
        for (int i = 0; i < m; i++){
            q.Add(arr[i]);
        }
        q.Sort();
        q.Reverse();
        // n operations
        while (n-- != 0) {
            int x = q[0];
            q.RemoveAt(0);
            // Decrement x
            --x;

            // Push back x inside the heap
            q.Add(x);
            q.Sort();
            q.Reverse();
        }

        // Store the max product possible
        int ans = 1;
        while (q.Count != 0) {
            ans *= q[0];
            q.RemoveAt(0);
        }

        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int M = 5;
        int []arr = { 5, 1, 7, 8, 3 };
        int N = 2;

        Console.WriteLine(getMax(M, arr, N));
    }
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum
// product of the array
function getMax(m, arr, n)
{

    // Max-heap
    let q = [];

    // Store all the elements inside max-heap
    for (let i = 0; i < m; i++) {
        q.push(arr[i]);
    }
    q.sort();
    q.reverse();

    // n operations
    while (n-- != 0) {
        let x = q[0];
        q.splice(0, 1);

        // Decrement x
        --x;

        // Push back x inside the heap
        q.push(x);
        q.sort();
        q.reverse();
    }

    // Store the max product possible
    let ans = 1;
    while (q.length != 0) {
        ans *= q[0];
        q.splice(0, 1);
    }
    return ans;
}

// Driver Code
let M = 5;
let arr = [5, 1, 7, 8, 3];
let N = 2;

document.write(getMax(M, arr, N));

// This code is contributed by gfgking
</script>
```

**Output**

```
630
```

***时间复杂度*** : O(nlogm)
***辅助空间*** : O(m)