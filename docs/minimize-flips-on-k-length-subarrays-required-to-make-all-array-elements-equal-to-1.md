# 最小化使所有阵列元素等于 1 所需的 K 长度子阵列上的翻转

> 原文:[https://www . geesforgeks . org/minimum-flips-on-k-length-subarrays-要求使所有数组元素等于 1/](https://www.geeksforgeeks.org/minimize-flips-on-k-length-subarrays-required-to-make-all-array-elements-equal-to-1/)

给定大小为 **N** 的二进制[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和正整数 **K** ，任务是从给定数组 **arr[]** 中找到大小为 **K** 的任何[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最小次数，以使所有数组元素等于 **1** 。如果不可能，则打印**-1”**。

**示例:**

> **输入:** arr[] = {0，1，0}，K = 1
> **输出:** 2
> **解释:**
> 按照以下顺序执行操作:
> **操作 1:** 翻转子阵列中存在的所有元素{arr[0]}。现在，数组修改为{1，1，0}。
> **操作 2:** 翻转子阵列{arr[2]}中存在的所有元素。现在数组修改为{1，1，1}。
> 因此，所需操作总数为 2。
> 
> **输入:** arr[] = {1，1，0}，K = 2
> **输出:** -1

**方法:**按照以下步骤解决问题:

*   初始化一个辅助[阵](https://www.geeksforgeeks.org/array-data-structure/)，说**是 **N.** 大小的**
*   初始化一个变量，比如说 **ans、**来存储所需的最小数量的**K**-长度子阵列翻转。
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   如果 **i** 的值大于 **0** ，则将**is lipped【I】**的值更新为**(is lipped【I】+is lipped【I–1】)% 2**。
    *   检查当前元素是否需要翻转，即如果 **A[i]的值为 0** 、**未设置**、[或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)、 **A[i]的值为 1** 、**未设置【I】则执行以下步骤:**
        *   如果这样的 K 长度子阵不可能，那么打印**-1”**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)，因为不可能让所有阵元都等于 **1** 。
        *   将 **ans** 和**增加 **1** 的【I】**，将**减少 **1** 的【I+K】**。
    *   否则[继续下一次迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。
*   完成以上步骤后，如果所有数组元素都可以做成 **1** ，则打印 **ans** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// K-length subarrays required to be
// flipped to make all array elements 1
void minimumOperations(vector<int>& A, int K)
{
    // Stores whether an element
    // can be flipped or not
    vector<int> isflipped(A.size(), 0);

    // Store the required number of flips
    int ans = 0;

    // Traverse the array, A[]
    for (int i = 0; i < A.size(); i++) {

        // Find the prefix sum
        // for the indices i > 0
        if (i > 0) {
            isflipped[i] += isflipped[i - 1];
            isflipped[i] %= 2;
        }

        // Check if the current element
        // is required to be flipped
        if (A[i] == 0 && !isflipped[i]) {

            // If subarray of size K
            // is not possible, then
            // print -1 and return
            if ((A.size() - i + 1) <= K) {
                cout << -1;
                return;
            }

            // Increment ans by 1
            ans++;

            // Change the current
            // state of the element
            isflipped[i]++;

            // Decrement isFlipped[i + K]
            isflipped[i + K]--;
        }
        else if (A[i] == 1 && isflipped[i]) {

            // If subarray of size K
            // is not possible, then
            // print -1 and return
            if ((A.size() - i + 1) <= K) {
                cout << -1;
                return;
            }

            // Increment ans by 1
            ans++;

            // Change the current
            // state of the element
            isflipped[i]++;

            // Decrement isFlipped[i+K]
            isflipped[i + K]--;
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 0, 1, 0 };
    int K = 1;
    minimumOperations(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{

  // Function to find the minimum number
  // K-length subarrays required to be
  // flipped to make all array elements 1 
  static void minimumOperations(int[] A, int K)
  {

    // Stores whether an element
    // can be flipped or not
    int[] isflipped = new int[A.length+1];

    // Store the required number of flips
    int ans = 0;

    // Traverse the array, A[]
    for (int i = 0; i < A.length; i++)
    {

      // Find the prefix sum
      // for the indices i > 0
      if (i > 0) {
        isflipped[i] += isflipped[i - 1];
        isflipped[i] %= 2;
      }

      // Check if the current element
      // is required to be flipped
      if (A[i] == 0 && isflipped[i] == 0)
      {

        // If subarray of size K
        // is not possible, then
        // print -1 and return
        if ((A.length - i + 1) <= K)
        {
          System.out.println(-1);
          return;
        }

        // Increment ans by 1
        ans++;

        // Change the current
        // state of the element
        isflipped[i]++;

        // Decrement isFlipped[i + K]
        isflipped[i + K]--;
      } else if (A[i] == 1 && isflipped[i] != 0)
      {

        // If subarray of size K
        // is not possible, then
        // print -1 and return
        if ((A.length - i + 1) <= K)
        {
          System.out.println(-1);
          return;
        }

        // Increment ans by 1
        ans++;

        // Change the current
        // state of the element
        isflipped[i]++;

        // Decrement isFlipped[i+K]
        isflipped[i + K]--;
      }
    }

    // Print the result
    System.out.println(ans);
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = {0, 1, 0};
    int K = 1;
    minimumOperations(arr, K);
  }
}

// This code is contributed by user_qa7r.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number
# K-length subarrays required to be
# flipped to make all array elements 1
def minimumOperations(A, K):

    # Stores whether an element
    # can be flipped or not
    isflipped = [0] * (len(A) + 1)

    # Store the required number of flips
    ans = 0

    # Traverse the array, A[]
    for i in range(len(A)):

        # Find the prefix sum
        # for the indices i > 0
        if (i > 0):
            isflipped[i] += isflipped[i - 1]
            isflipped[i] %= 2

        # Check if the current element
        # is required to be flipped
        if (A[i] == 0 and not isflipped[i]):

            # If subarray of size K
            # is not possible, then
            # print -1 and return
            if ((len(A) - i + 1) <= K):
                print(-1)
                return

            # Increment ans by 1
            ans += 1

            # Change the current
            # state of the element
            isflipped[i] += 1

            # Decrement isFlipped[i + K]
            isflipped[i + K] -= 1

        elif (A[i] == 1 and isflipped[i]):

            # If subarray of size K
            # is not possible, then
            # print -1 and return
            if ((len(A) - i + 1) <= K):
                print(-1)
                return

            # Increment ans by 1
            ans += 1

            # Change the current
            # state of the element
            isflipped[i] += 1

            # Decrement isFlipped[i+K]
            isflipped[i + K] -= 1

    # Print the result
    print(ans)

# Driver Code
if __name__ == "__main__":

    arr = [0, 1, 0]
    K = 1

    minimumOperations(arr, K)

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum number
// K-length subarrays required to be
// flipped to make all array elements 1
static void minimumOperations(List<int> A, int K)
{

    // Stores whether an element
    // can be flipped or not
    List<int> isflipped = new List<int>();
    for(int i = 0; i < A.Count + 1; i++)
        isflipped.Add(0);

    // Store the required number of flips
    int ans = 0;

    // Traverse the array, A[]
    for(int i = 0; i < A.Count; i++)
    {

        // Find the prefix sum
        // for the indices i > 0
        if (i > 0)
        {
            isflipped[i] += isflipped[i - 1];
            isflipped[i] %= 2;
        }

        // Check if the current element
        // is required to be flipped
        if (A[i] == 0 && isflipped[i] == 0)
        {

            // If subarray of size K
            // is not possible, then
            // print -1 and return
            if ((A.Count - i + 1) <= K)
            {
                Console.Write(-1);
                return;
            }

            // Increment ans by 1
            ans += 1;

            // Change the current
            // state of the element
            isflipped[i] += 1;

            // Decrement isFlipped[i + K]
            isflipped[i + K] -= 1;
        }
        else if (A[i] == 1 && isflipped[i] != 0)
        {

            // If subarray of size K
            // is not possible, then
            // print -1 and return
            if ((A.Count - i + 1) <= K)
            {
                Console.Write(-1);
                return;
            }

            // Increment ans by 1
            ans += 1;

            // Change the current
            // state of the element
            isflipped[i] += 1;

            // Decrement isFlipped[i+K]
            isflipped[i + K] -= 1;
        }
    }

    // Print the result
    Console.WriteLine(ans);
}

// Driver Code
public static void Main()
{
    List<int> arr = new List<int>(){ 0, 1, 0 };
    int K = 1;

    minimumOperations(arr, K);
}
}

// This code is contributed by bgangwar59
```

## java 描述语言

```
<script>

// Javascript program for the above approach

  // Function to find the minimum number
  // K-length subarrays required to be
  // flipped to make all array elements 1
  function minimumOperations(A, K)
  {

    // Stores whether an element
    // can be flipped or not
    let isflipped = [];
    for (let i = 0; i < A.length + 1; i++)
    {
        isflipped[i] =0;
    }

    // Store the required number of flips
    let ans = 0;

    // Traverse the array, A[]
    for (let i = 0; i < A.length; i++)
    {

      // Find the prefix sum
      // for the indices i > 0
      if (i > 0) {
        isflipped[i] += isflipped[i - 1];
        isflipped[i] %= 2;
      }

      // Check if the current element
      // is required to be flipped
      if (A[i] == 0 && isflipped[i] == 0)
      {

        // If subarray of size K
        // is not possible, then
        // print -1 and return
        if ((A.length - i + 1) <= K)
        {
          document.write(-1);
          return;
        }

        // Increment ans by 1
        ans++;

        // Change the current
        // state of the element
        isflipped[i]++;

        // Decrement isFlipped[i + K]
        isflipped[i + K]--;
      } else if (A[i] == 1 && isflipped[i] != 0)
      {

        // If subarray of size K
        // is not possible, then
        // print -1 and return
        if ((A.length - i + 1) <= K)
        {
          document.write(-1);
          return;
        }

        // Increment ans by 1
        ans++;

        // Change the current
        // state of the element
        isflipped[i]++;

        // Decrement isFlipped[i+K]
        isflipped[i + K]--;
      }
    }

    // Print the result
    document.write(ans);
  }

// Driver Code

    let arr = [ 0, 1, 0 ];
    let K = 1;
    minimumOperations(arr, K);

</script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**接近 2:-滑动窗口**

## C++

```
#include <bits/stdc++.h>
using namespace std;

int minKBitFlips(int A[], int K, int N)
{

    // store previous flip events
    queue<int> flip;
    int count = 0;
    for (int i = 0; i < N; i++)
    {

        // remove an item which is out range of window.
        if (flip.size() > 0 && (i - flip.front() >= K)) {
            flip.pop();
        }

        /*
         In a window,  if A[i] is a even number with
         even times flipped, it need to be flipped again.
         On other hand,if A[i] is a odd number with odd
         times flipped, it need to be flipped again.
        */
        if (A[i] % 2 == flip.size() % 2) {
            if (i + K - 1 >= N) {
                return -1;
            }
            flip.push(i); // insert
            count++;
        }
    }
    return count;
}

int main()
{
    int A[] = { 0, 1, 0 };
    int N = sizeof(A) / sizeof(A[0]);
    int K = 1;
    int ans = minKBitFlips(A, K, 3);
    cout << ans;

    return 0;
}

// This code is contributed by divyeshrabadiya07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;

class GFG {
    static int minKBitFlips(int[] A, int K)
    {
        // store previous flip events
        Queue<Integer> flip = new LinkedList<>();
        int count = 0;
        for (int i = 0; i < A.length; i++) {
            // remove an item which is out range of window.
            if (!flip.isEmpty() && (i - flip.peek() >= K)) {
                flip.poll();
            }
            /*
             In a window,  if A[i] is a even number with
             even times flipped, it need to be flipped again.
             On other hand,if A[i] is a odd number with odd
             times flipped, it need to be flipped again.
            */
            if (A[i] % 2 == flip.size() % 2) {
                if (i + K - 1 >= A.length) {
                    return -1;
                }
                flip.offer(i); // insert
                count++;
            }
        }
        return count;
    }
    public static void main(String[] args)
    {
        int[] A = { 0, 1, 0 };
        int K = 1;
        int ans = minKBitFlips(A, K);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
def minKBitFlips(A, K, N):

    # Store previous flip events
    flip = []
    count = 0

    for i in range(N):

        # Remove an item which is out range of window.
        if (len(flip) > 0 and (i - flip[0] >= K)):
            flip.pop(0)

        """
        In a window, if A[i] is a even number with
        even times flipped, it need to be flipped again.
        On other hand,if A[i] is a odd number with odd
        times flipped, it need to be flipped again.
        """
        if (A[i] % 2 == len(flip) % 2):
            if (i + K - 1 >= N):
                return -1

            # Insert
            flip.append(i)
            count += 1

    return count

# Driver code
A = [ 0, 1, 0 ]
N = len(A)
K = 1

ans = minKBitFlips(A, K, 3)

print(ans)

# This code is contributed by rameshtravel07
```

## C#

```
using System;
using System.Collections;
class GFG {

    static int minKBitFlips(int[] A, int K)
    {

        // store previous flip events
        Queue flip = new Queue();
        int count = 0;
        for (int i = 0; i < A.Length; i++)
        {

            // remove an item which is out range of window.
            if (flip.Count > 0 && (i - (int)flip.Peek() >= K)) {
                flip.Dequeue();
            }

            /*
             In a window,  if A[i] is a even number with
             even times flipped, it need to be flipped again.
             On other hand,if A[i] is a odd number with odd
             times flipped, it need to be flipped again.
            */
            if (A[i] % 2 == flip.Count % 2) {
                if (i + K - 1 >= A.Length) {
                    return -1;
                }
                flip.Enqueue(i); // insert
                count++;
            }
        }
        return count;
    }

  static void Main() {
    int[] A = { 0, 1, 0 };
    int K = 1;
    int ans = minKBitFlips(A, K);
    Console.WriteLine(ans);
  }
}

// This code is contributed by mukesh07.
```

## java 描述语言

```
<script>

function minKBitFlips(A,K)
{
    // store previous flip events
        let flip = [];
        let count = 0;
        for (let i = 0; i < A.length; i++) {
            // remove an item which is out range of window.
            if (flip.length!=0 && (i - flip[0] >= K)) {
                flip.shift();
            }
            /*
             In a window,  if A[i] is a even number with
             even times flipped, it need to be flipped again.
             On other hand,if A[i] is a odd number with odd
             times flipped, it need to be flipped again.
            */
            if (A[i] % 2 == flip.length % 2) {
                if (i + K - 1 >= A.length) {
                    return -1;
                }
                flip.push(i); // insert
                count++;
            }
        }
        return count;
}

let A=[0, 1, 0 ];
let K = 1;
let ans = minKBitFlips(A, K);
document.write(ans);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output**

```
2
```

***复杂度分析:-***

***时间复杂度:*** O(N)，其中 N 为数组长度。

***空间复杂度:*** O(N)。

**方法 3:-贪婪**

## C++

```
#include <bits/stdc++.h>
using namespace std;

int minKBitFlips(int A[], int K, int N)
{
    int temp[N];
    memset(temp, 0, N);
    int count = 0;
    int flip = 0;
    count++;
    for (int i = 0; i < N; ++i) {
        flip ^= temp[i];
        if (A[i] == flip) { // If we must flip the
                            // subarray starting here...
            count++; // We're flipping the subarray from
                     // A[i] to A[i+K-1]
            if (i + K > N) {
                return -1; // If we can't flip the
                           // entire subarray, its
                           // impossible
            }
            flip ^= 1;
            if (i + K < N) {
                temp[i + K] ^= 1;
            }
        }
    }

    return count;
}

int main()
{
    int A[] = { 0, 1, 0 };
    int N = sizeof(A) / sizeof(A[0]);
    int K = 1;
    int ans = minKBitFlips(A, K, N);
    cout << ans;

    return 0;
}

// This code is contributed by suresh07.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;
import java.util.*;

class GFG {
    static int minKBitFlips(int[] A, int K)
    {
        int[] temp = new int[A.length];
        int count = 0;
        int flip = 0;
        for (int i = 0; i < A.length; ++i) {
            flip ^= temp[i];
            if (A[i] == flip) { // If we must flip the
                                // subarray starting here...
                count++; // We're flipping the subarray from
                         // A[i] to A[i+K-1]
                if (i + K > A.length) {
                    return -1; // If we can't flip the
                               // entire subarray, its
                               // impossible
                }
                flip ^= 1;
                if (i + K < A.length) {
                    temp[i + K] ^= 1;
                }
            }
        }

        return count;
    }
    public static void main(String[] args)
    {
        int[] A = { 0, 1, 0 };
        int K = 1;
        int ans = minKBitFlips(A, K);
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
def minKBitFlips(A, K):

    temp = [0]*len(A)
    count = 0
    flip = 0
    for i in range(len(A)):
        flip ^= temp[i]
        if (A[i] == flip):

            # If we must flip the
            # subarray starting here...
            count += 1

            # We're flipping the subarray from
            # A[i] to A[i+K-1]
            if (i + K > len(A)) :
                return -1

                # If we can't flip the
                # entire subarray, its
                # impossible

            flip ^= 1
            if (i + K < len(A)):
                temp[i + K] ^= 1

    return count

A = [ 0, 1, 0 ]
K = 1
ans = minKBitFlips(A, K)
print(ans)

# This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    function minKBitFlips(A, K)
    {
        let temp = new Array(A.length);
        let count = 0;
        let flip = 0;
        for (let i = 0; i < A.length; ++i) {
            flip ^= temp[i];
            if (A[i] == flip) { // If we must flip the
                                // subarray starting here...
                count++; // We're flipping the subarray from
                         // A[i] to A[i+K-1]
                if (i + K > A.length) {
                    return -1; // If we can't flip the
                               // entire subarray, its
                               // impossible
                }
                flip ^= 1;
                if (i + K < A.length) {
                    temp[i + K] ^= 1;
                }
            }
        }

        return count;
    }

    let A = [ 0, 1, 0 ];
    let K = 1;
    let ans = minKBitFlips(A, K);
    document.write(ans);

 // This code is contributed by gfgking.
</script>
```

## C#

```
/*package whatever //do not write package name here */

using System;

class GFG {
    static int minKBitFlips(int[] A, int K)
    {
        int[] temp = new int[A.Length];
        int count = 0;
        int flip = 0;
        for (int i = 0; i < A.Length; ++i) {
            flip ^= temp[i];
            if (A[i] == flip) { // If we must flip the
                                // subarray starting here...
                count++; // We're flipping the subarray from
                         // A[i] to A[i+K-1]
                if (i + K > A.Length) {
                    return -1; // If we can't flip the
                               // entire subarray, its
                               // impossible
                }
                flip ^= 1;
                if (i + K < A.Length) {
                    temp[i + K] ^= 1;
                }
            }
        }

        return count;
    }
    public static void Main(String[] args)
    {
        int[] A = { 0, 1, 0 };
        int K = 1;
        int ans = minKBitFlips(A, K);
        Console.Write(ans);
    }
}

// This code is contributed by shivanisinghss2110
```

**Output**

```
2
```

***复杂度分析:-***

***时间复杂度:*** O(N)，其中 N 为数组长度。

***空间复杂度:*** O(N)。