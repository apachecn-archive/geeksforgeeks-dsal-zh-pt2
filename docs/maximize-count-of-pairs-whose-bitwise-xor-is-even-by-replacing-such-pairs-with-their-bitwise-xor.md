# 通过用按位异或

替换按位异或为偶数的对，最大化对的计数

> 原文:[https://www . geeksforgeeks . org/通过用它们的按位异或替换这样的对来最大化对的计数/](https://www.geeksforgeeks.org/maximize-count-of-pairs-whose-bitwise-xor-is-even-by-replacing-such-pairs-with-their-bitwise-xor/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是替换一对数组元素，它们的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于它们的**按位异或**。尽可能长时间地重复上述步骤。最后，打印在阵列上执行的此类操作的计数

**示例:**

> **输入:** arr[] = { 4，6，1，3 }
> **输出:** 3
> **解释:**
> 步骤 1:移除对(4，6)并用它们在数组中的异或值(= 2)替换它们。因此，数组 arr[]修改为{2，1，3}。
> 步骤 2:移除对(1，3)并用它们在数组中的异或值(= 2)替换它们，将数组修改为 arr[] = {2，2}。
> 最后选择对(2，2)，然后移除对，在数组中插入 2 和 2 的异或，将数组修改为 arr[] ={0}。
> 现在不能选择其他对，因此 3 是异或为偶数的对的最大数量。
> 
> **输入:** arr[ ] = { 1，2，3，4，5 }
> **输出:** 3

**天真方法:**解决这个问题最简单的方法是[找到数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中所有可能的对，并针对每一对，检查它们的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)是否为偶数。如果发现为真，则增加对的计数，从数组中移除两个元素，并将它们的异或加到数组中。重复以上步骤，直到无法选择更多对。打印已执行操作的计数。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法可以基于以下观察进行优化:

> *   *even even = even*
> *   *Odd odd = even*
> *   *The total number of pairs that can be formed only by odd numbers that meet the conditions is **odd/2\.***
> *   *The total number of pairs that can only be formed by even numbers that meet the conditions is **even numbers–1\.***

按照以下步骤解决问题:

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
2.  [统计奇数出现的频率](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)并存储在变量中，比如**奇数**。
3.  所有奇数阵列元素可以形成的偶[异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)对的总数为**层(奇数/ 2)** 。
4.  删除上一步形成的对，分别用它们的异或值替换，偶数元素的个数增加[**层(奇数/ 2)。**](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)
5.  最后，将偶数异或可以形成的对的个数打印为**(N–奇数+奇数/2 -1) +奇数/2。**

下面是上述方法的实现:

## C++

```
// C++ program to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to maximize the count
// of pairs with even XOR possible
// in an array by given operations
int countPairs(int arr[], int N)
{
    // Stores count of odd
    // array elements
    int odd = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If arr[i] is odd
        if (arr[i] & 1)
            odd++;
    }

    // Stores the total number
    // of even pairs
    int ans = (N - odd + odd / 2
               - 1)
              + odd / 2;

    return ans;
}

// Driver Code
int main()
{
    // Input
    int arr[] = { 4, 6, 1, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to count the number
    // of pairs whose XOR is even
    cout << countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above approach
public class GFG
{

  // Function to maximize the count
  // of pairs with even XOR possible
  // in an array by given operations
  static int countPairs(int []arr, int N)
  {

    // Stores count of odd
    // array elements
    int odd = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // If arr[i] is odd
      if ((arr[i] & 1)!=0)
        odd++;
    }

    // Stores the total number
    // of even pairs
    int ans = (N - odd + odd / 2
               - 1)
      + odd / 2;

    return ans;
  }

  // Driver Code
  public static void main(String args[])
  {

    // Input
    int []arr = { 4, 6, 1, 3 };
    int N = arr.length;

    // Function call to count the number
    // of pairs whose XOR is even
    System.out.println(countPairs(arr, N));
  }
}

// This code is contributed by AnkThon.
```

## 蟒蛇 3

```
# Python3 program to implement the above approach

# Function to maximize the count
# of pairs with even XOR possible
# in an array by given operations
def countPairs(arr, N):

    # Stores count of odd
    # array elements
    odd = 0

    # Traverse the array
    for i in range(N):

        # If arr[i] is odd
        if (arr[i] & 1):
            odd += 1

    # Stores the total number
    # of even pairs
    ans = (N - odd + odd // 2 - 1) + odd // 2

    return ans

# Driver Code
if __name__ == '__main__':

  # Input
    arr =[4, 6, 1, 3]
    N = len(arr)

    # Function call to count the number
    # of pairs whose XOR is even
    print (countPairs(arr, N))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement the above approach
using System;
class GFG
{

// Function to maximize the count
// of pairs with even XOR possible
// in an array by given operations
static int countPairs(int []arr, int N)
{

    // Stores count of odd
    // array elements
    int odd = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // If arr[i] is odd
        if ((arr[i] & 1)!=0)
            odd++;
    }

    // Stores the total number
    // of even pairs
    int ans = (N - odd + odd / 2
               - 1)
              + odd / 2;

    return ans;
}

// Driver Code
public static void Main()
{

    // Input
    int []arr = { 4, 6, 1, 3 };
    int N = arr.Length;

    // Function call to count the number
    // of pairs whose XOR is even
    Console.Write(countPairs(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>
// JavaScript program to implement the above approach

// Function to maximize the count
// of pairs with even XOR possible
// in an array by given operations
function countPairs(arr, N)
{
    // Stores count of odd
    // array elements
    let odd = 0;

    // Traverse the array
    for (let i = 0; i < N; i++) {

        // If arr[i] is odd
        if (arr[i] & 1)
            odd++;
    }

    // Stores the total number
    // of even pairs
    let ans = (N - odd + Math.floor(odd / 2) - 1) + Math.floor(odd / 2);

    return ans;
}

// Driver Code

    // Input
    let arr = [ 4, 6, 1, 3 ];
    let N = arr.length;

    // Function call to count the number
    // of pairs whose XOR is even
    document.write(countPairs(arr, N));

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)