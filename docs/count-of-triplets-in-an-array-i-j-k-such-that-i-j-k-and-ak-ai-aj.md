# 一个数组(I，j，k)中三元组的计数，使得 i < j < k 和 a【k】<a【I】<a【j】

> 原文:[https://www . geeksforgeeks . org/数组中三元组的计数-I-j-k-so-I-j-k-and-AK-ai-aj/](https://www.geeksforgeeks.org/count-of-triplets-in-an-array-i-j-k-such-that-i-j-k-and-ak-ai-aj/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算数组中三元组 **(i，j，k)** 的数量，使得**a【k】<a【I】<a【j】**和 **i < j < k** 。
**示例:**

> **输入:** arr[] = {2，5，1，3，0}
> **输出:** 4
> **解释:**
> 下面是三元组(I，j，k)，这样 **i < j < k** 和**a【k】<a【I】<a【j】**:
> 1。(0，1，2)和 arr[2] < arr[0] 1 < 2 < 5。
> 2。(0，1，4)和 arr[4] < arr[0] 0 < 2 < 5。
> 3。(0，3，4)和 arr[4] < arr[0] 0 < 2 < 3。
> 4。(2，3，4)和 arr[4] < arr[2] 0 < 1 < 3。
> **输入:** arr[] = {2，5，1，2，0，3，10，1，5，0 }
> T21】输出: 25

**天真方法:**想法是迭代 3 个循环，检查每个三元组 **(i，j，k)** 是否满足给定条件。如果是，则递增该三元组，并在检查所有三元组后打印最终计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count triplets with the
// given conditions
int CountTriplets(int arr[], int n)
{
    int cnt = 0;

    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
            for (int k = j + 1; k < n; k++)

                // If it satisfy the
                // given conditions
                if (arr[k] < arr[i]
                    && arr[i] < arr[j]) {

                    cnt += 1;
                }

    // Return the final count
    return cnt;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 5, 1, 3, 0 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << CountTriplets(arr, n)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count triplets
// with the given conditions
static int CountTriplets(int arr[], int n)
{
    int cnt = 0;

    for(int i = 0; i < n; i++)
       for(int j = i + 1; j < n; j++)
          for(int k = j + 1; k < n; k++)

             // If it satisfy the
             // given conditions
             if (arr[k] < arr[i] &&
                 arr[i] < arr[j])
             {
                 cnt += 1;
             }

    // Return the final count
    return cnt;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = new int[]{ 2, 5, 1, 3, 0 };

    int n = arr.length;

    System.out.print(CountTriplets(arr, n));
}
}

// This code is contributed by Pratima Pandey
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count triplets with the
# given conditions
def CountTriplets(arr, n):

    cnt = 0;

    for i in range(0, n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):

                # If it satisfy the
                # given conditions
                if (arr[k] < arr[i] and arr[i] < arr[j]):
                    cnt += 1;

    # Return the final count
    return cnt;

# Driver Code

# Given array arr[]
arr = [ 2, 5, 1, 3, 0 ];

n = len(arr);

# Function Call
print(CountTriplets(arr, n))

# This code is contributed by Code_Mech
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count triplets
// with the given conditions
static int CountTriplets(int []arr, int n)
{
    int cnt = 0;

    for(int i = 0; i < n; i++)
       for(int j = i + 1; j < n; j++)
          for(int k = j + 1; k < n; k++)

             // If it satisfy the
             // given conditions
             if (arr[k] < arr[i] &&
                 arr[i] < arr[j])
             {
                 cnt += 1;
             }

    // Return the final count
    return cnt;
}

// Driver Code
public static void Main(string[] args)
{

    // Given array arr[]
    int []arr = new int[]{ 2, 5, 1, 3, 0 };

    int n = arr.Length;

    Console.Write(CountTriplets(arr, n));
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to count triplets with the
    // given conditions
    function CountTriplets(arr, n)
    {
        let cnt = 0;

        for (let i = 0; i < n; i++)
            for (let j = i + 1; j < n; j++)
                for (let k = j + 1; k < n; k++)

                    // If it satisfy the
                    // given conditions
                    if (arr[k] < arr[i]
                        && arr[i] < arr[j]) {

                        cnt += 1;
                    }

        // Return the final count
        return cnt;
    }

    // Given array arr[]
    let arr = [ 2, 5, 1, 3, 0 ];

    let n = arr.length;

    // Function Call
    document.write(CountTriplets(arr, n));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**我们可以使用以下步骤降低从 N^3 到 N^2 的复杂性:

1.  运行两个循环以找到对 **(i，j)** ，使得 **i < j** 和**arr【j】>arr【I】**并将这些对的计数保持为 **cnt** 。
2.  在上述循环中，如果存在任何元素如 **arr[j] < arr[i]** ，则通过 **cnt** 增加三胞胎的计数，因为当前元素是 **Kth 元素**，使得 **a[k] < a[i] < a[j]** 为三胞胎 **i < j < k** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count  triplets
int CountTriplets(int a[], int n)
{

    // To store count of total triplets
    int ans = 0;

    for (int i = 0; i < n; i++) {

        // Initialize count to zero
        int cnt = 0;

        for (int j = i + 1; j < n; j++) {

            // If a[j] > a[i] then,
            // increment cnt
            if (a[j] > a[i])
                cnt++;

            // If a[j] < a[i], then
            // it mean we have found a[k]
            // such that a[k] < a[i] < a[j]
            else
                ans += cnt;
        }
    }

    // Return the final count
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 2, 5, 1, 3, 0 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << CountTriplets(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to count triplets
static int CountTriplets(int a[], int n)
{

    // To store count of total triplets
    int ans = 0;

    for (int i = 0; i < n; i++)
    {

        // Initialize count to zero
        int cnt = 0;

        for (int j = i + 1; j < n; j++)
        {

            // If a[j] > a[i] then,
            // increment cnt
            if (a[j] > a[i])
                cnt++;

            // If a[j] < a[i], then
            // it mean we have found a[k]
            // such that a[k] < a[i] < a[j]
            else
                ans += cnt;
        }
    }

    // Return the final count
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 5, 1, 3, 0 };

    int n = arr.length;

    System.out.print(CountTriplets(arr, n));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program for
# the above approach

# Function to count  triplets
def CountTriplets(a, n):

    # To store count
    # of total triplets
    ans = 0

    for i in range (n):

        # Initialize count to zero
        cnt = 0

        for j in range (i + 1 , n):

            # If a[j] > a[i] then,
            # increment cnt
            if (a[j] > a[i]):
                cnt += 1

            # If a[j] < a[i], then
            # it mean we have found a[k]
            # such that a[k] < a[i] < a[j]
            else:
                ans += cnt

    # Return the final count
    return ans

# Driver code
if __name__ == "__main__": 
    arr = [2, 5, 1, 3, 0]
    n = len(arr)
    print (CountTriplets(arr, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to count triplets
static int CountTriplets(int []a, int n)
{

    // To store count of total triplets
    int ans = 0;

    for (int i = 0; i < n; i++)
    {

        // Initialize count to zero
        int cnt = 0;

        for (int j = i + 1; j < n; j++)
        {

            // If a[j] > a[i] then,
            // increment cnt
            if (a[j] > a[i])
                cnt++;

            // If a[j] < a[i], then
            // it mean we have found a[k]
            // such that a[k] < a[i] < a[j]
            else
                ans += cnt;
        }
    }

    // Return the final count
    return ans;
}

// Driver code
public static void Main()
{
    int []arr = { 2, 5, 1, 3, 0 };

    int n = arr.Length;

    Console.Write(CountTriplets(arr, n));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count  triplets
function CountTriplets(a, n)
{

    // To store count of total triplets
    let ans = 0;

    for(let i = 0; i < n; i++)
    {

        // Initialize count to zero
        let cnt = 0;

        for(let j = i + 1; j < n; j++)
        {

            // If a[j] > a[i] then,
            // increment cnt
            if (a[j] > a[i])
                cnt++;

            // If a[j] < a[i], then
            // it mean we have found a[k]
            // such that a[k] < a[i] < a[j]
            else
                ans += cnt;
        }
    }

    // Return the final count
    return ans;
}

// Driver code
let arr = [ 2, 5, 1, 3, 0 ];
let n = arr.length;

document.write(CountTriplets(arr, n));

// This code is contributed by rameshtravel07

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*