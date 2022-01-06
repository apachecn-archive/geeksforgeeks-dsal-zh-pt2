# 反转每个数组元素的二进制表示后，计数剩余的数组元素

> 原文:[https://www . geesforgeks . org/count-returning-array-elements-反转后-每个数组元素的二进制表示/](https://www.geeksforgeeks.org/count-remaining-array-elements-after-reversing-binary-representation-of-each-array-element/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过反转它们来修改每个数组元素[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)，并计算修改后的数组中也存在于原始数组中的元素数量。

**示例:**

> **输入** : arr[] = {2，4，5，20， 16}
> **输出:** 2
> **解释:**
> 2->(10)<sub>2</sub>->(1)<sub>2</sub>->1 即不存在于原始数组中
> 4->(100)<sub>2</sub>->(1)<sub>2</sub>->1 <sub>2</sub> - > 5 即原阵中存在
> 20->(10100)<sub>2</sub>->(101)<sub>2</sub>->5 即原阵中存在
> 16->(10000)<sub>2</sub>->(1)<sub>2【T32</sub>
> 
> **输入:** arr[] = {1，30，3，8，12 }
> T3】输出: 4

**方法:**按照以下步骤解决问题:

*   初始化一个变量，说**计数**，存储需要的计数，一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，说 **V** ，存储每个数组元素的[反转位，一个](https://www.geeksforgeeks.org/reverse-actual-bits-given-number/)[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储原始数组中的数组元素。
*   [遍历给定数组 **arr[]**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，并执行以下步骤:
    *   将元素**arr【I】**的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)的每一位反转后形成的数字存储在向量 **V** 中。
    *   在**地图**中标记当前元素**的存在。**
*   [遍历向量 V](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) ，如果向量中存在的任何元素也存在于**地图**中，那么将**计数**增加 **1** 。
*   完成上述步骤后，打印计数值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to reverse the binary
// representation of a number
int findReverse(int N)
{
    int rev = 0;

    // Traverse bits of N
    // from the right
    while (N > 0) {

        // Bitwise left
        // shift 'rev' by 1
        rev <<= 1;

        // If current bit is '1'
        if (N & 1 == 1)
            rev ^= 1;

        // Bitwise right
        // shift N by 1
        N >>= 1;
    }

    // Required number
    return rev;
}

// Function to count elements from the
// original array that are also present
// in the array formed by reversing the
// binary representation of each element
void countElements(int arr[], int N)
{
    // Stores the reversed num
    vector<int> ans;

    // Iterate from [0, N]
    for (int i = 0; i < N; i++) {
        ans.push_back(findReverse(arr[i]));
    }

    // Stores the presence of integer
    unordered_map<int, int> cnt;
    for (int i = 0; i < N; i++) {
        cnt[arr[i]] = 1;
    }

    // Stores count of elements
    // present in original array
    int count = 0;

    // Traverse the array
    for (auto i : ans) {

        // If current number is present
        if (cnt[i])
            count++;
    }

    // Print the answer
    cout << count << endl;
}

// Driver Code
int main()
{
    int arr[] = { 1, 30, 3, 8, 12 };
    int N = sizeof(arr) / sizeof(arr[0]);

    countElements(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

  // Function to reverse the binary
  // representation of a number
  static int findReverse(int N)
  {
    int rev = 0;

    // Traverse bits of N
    // from the right
    while (N > 0)
    {

      // Bitwise left
      // shift 'rev' by 1
      rev <<= 1;

      // If current bit is '1'
      if ((N & 1) == 1)
        rev ^= 1;

      // Bitwise right
      // shift N by 1
      N >>= 1;
    }

    // Required number
    return rev;
  }

  // Function to count elements from the
  // original array that are also present
  // in the array formed by reversing the
  // binary representation of each element
  static void countElements(int arr[], int N)
  {
    // Stores the reversed num
    Vector<Integer> ans = new Vector<Integer>();

    // Iterate from [0, N]
    for (int i = 0; i < N; i++)
    {
      ans.add(findReverse(arr[i]));
    }

    // Stores the presence of integer
    HashMap<Integer, Integer> cnt = new HashMap<Integer, Integer>();
    for (int i = 0; i < N; i++)
    {
      cnt.put(arr[i], 1);
    }

    // Stores count of elements
    // present in original array
    int count = 0;

    // Traverse the array
    for(Integer i : ans) {

      // If current number is present
      if (cnt.containsKey(i))
        count++;
    }

    // Print the answer
    System.out.println(count);
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] arr = { 1, 30, 3, 8, 12 };
    int N = arr.length;

    countElements(arr, N);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to reverse the binary
# representation of a number
def findReverse(N):
    rev = 0

    # Traverse bits of N
    # from the right
    while (N > 0):

        # Bitwise left
        # shift 'rev' by 1
        rev <<= 1

        # If current bit is '1'
        if (N & 1 == 1):
            rev ^= 1

        # Bitwise right
        # shift N by 1
        N >>= 1

    # Required number
    return rev

# Function to count elements from the
# original array that are also present
# in the array formed by reversing the
# binary representation of each element
def countElements(arr, N):

    # Stores the reversed num
    ans = []

    # Iterate from [0, N]
    for i in range(N):
        ans.append(findReverse(arr[i]))

    # Stores the presence of integer
    cnt = {}
    for i in range(N):
        cnt[arr[i]] = 1

    # Stores count of elements
    # present in original array
    count = 0

    # Traverse the array
    for i in ans:

        # If current number is present
        if (i in cnt):
            count += 1

    # Print the answer
    print(count)

# Driver Code
if __name__ == '__main__':
    arr =  [1, 30, 3, 8, 12]
    N =  len(arr)

    countElements(arr, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function to reverse the binary
  // representation of a number
  static int findReverse(int N)
  {
    int rev = 0;

    // Traverse bits of N
    // from the right
    while (N > 0) {

      // Bitwise left
      // shift 'rev' by 1
      rev <<= 1;

      // If current bit is '1'
      if ((N & 1) == 1)
        rev ^= 1;

      // Bitwise right
      // shift N by 1
      N >>= 1;
    }

    // Required number
    return rev;
  }

  // Function to count elements from the
  // original array that are also present
  // in the array formed by reversing the
  // binary representation of each element
  static void countElements(int[] arr, int N)
  {
    // Stores the reversed num
    List<int> ans = new List<int>();

    // Iterate from [0, N]
    for (int i = 0; i < N; i++) {
      ans.Add(findReverse(arr[i]));
    }

    // Stores the presence of integer
    Dictionary<int, int> cnt
      = new Dictionary<int, int>();
    for (int i = 0; i < N; i++) {
      cnt[arr[i]] = 1;
    }

    // Stores count of elements
    // present in original array
    int count = 0;

    // Traverse the array
    foreach(int i in ans)
    {

      // If current number is present
      if (cnt.ContainsKey(i))
        count++;
    }

    // Print the answer
    Console.WriteLine(count);
  }

  // Driver Code
  public static void Main()
  {
    int[] arr = { 1, 30, 3, 8, 12 };
    int N = arr.Length;

    countElements(arr, N);
  }
}

// This code is contributed by chitranayal.
```

## java 描述语言

```
<script>
// Js program for the above approach

// Function to reverse the binary
// representation of a number
function findReverse(N) {

    let rev = 0;

    // Traverse bits of N
    // from the right
    while (N > 0) {

        // Bitwise left
        // shift 'rev' by 1
        rev <<= 1;

        // If current bit is '1'
        if (N & 1 == 1)
            rev ^= 1;

        // Bitwise right
        // shift N by 1
        N >>= 1;
    }

    // Required number
    return rev;
}

// Function to count elements from the
// original array that are also present
// in the array formed by reversing the
// binary representation of each element
function countElements( arr, N)
{
    // Stores the reversed num
    let ans=[];

    // Iterate from [0, N]
    for (let i = 0; i < N; i++) {
        ans.push(findReverse(arr[i]));
    }

    // Stores the presence of integer
    let cnt = new Map();
    for (let i = 0; i < N; i++) {
        cnt[arr[i]] = 1;
    }

    // Stores count of elements
    // present in original array
    let count = 0;

    // Traverse the array
    for (let i = 0;i<ans.length;i++) {

        // If current number is present
        if (cnt[ans[i]])
            count++;
    }

    // Print the answer
    document.write( count,'<br>');
}

// Driver Code
let arr = [ 1, 30, 3, 8, 12 ];
let N = arr.length;

countElements(arr, N);
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)