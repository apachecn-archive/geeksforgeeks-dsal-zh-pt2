# 通过将按位“与”替换为按位“与”

，最大化按位“与”超过按位“异或”的对的计数

> 原文:[https://www . geeksforgeeks . org/通过用它们的按位“与”替换这样的对来最大化其按位“与”超过按位“异或”的对的计数/](https://www.geeksforgeeks.org/maximize-count-of-pairs-whose-bitwise-and-exceeds-bitwise-xor-by-replacing-such-pairs-with-their-bitwise-and/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，用它们的按位“与”值替换其[按位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)超过[按位“异或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值的数组元素对。最后，计算可以从数组中生成的这种对的最大数量。

**示例:**

> **输入:** arr[] = {12，9，15，7}
> **输出:** 2
> **解释:**
> 第一步:选择配对{12，15}并用它们的位运算 AND (= 12)替换该配对。数组 arr[]修改为{12，9，7}。
> 步骤 2:用它们的按位“与”(= 8)替换对{12，9}。因此，数组 arr[]修改为{8，7}。
> 因此，此类对的最大数量为 2。
> 
> **输入:** arr[] = {2，6，12，18，9 }
> T3】输出: 1

**天真方法:**解决这个问题最简单的方法是[生成所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，并选择一个比它们的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)大的对[。更换成对并插入它们的**位“与”**。重复上述过程，直到没有找到这样的配对。打印获得的此类配对的数量。
**时间复杂度:** O(N <sup>3</sup> )
**辅助空间:** O(1)](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)

**高效方法:**上述方法可以基于以下观察进行优化:

*   位于 **i <sup>第</sup>T5】位置的[最高有效位](https://www.geeksforgeeks.org/find-significant-set-bit-number/)的数字只能与位于 **i <sup>第</sup>T11】位置的 **MSB** 的其他数字形成一对。****
*   如果选择了这些对中的一个，其 **MSB** 位于 **i <sup>第</sup>T5】位置的数字总数将减少 1。**
*   因此，可以在第 **i <sup>第</sup>T3】位置形成的总对是在第 **i <sup>第</sup>T9】位置具有第 **MB** 的总数减少了第 **1** 。****

按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如 **freq** ，以存储在各个比特位置具有 MSB 的数字的计数。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组元素**arr【I】**，[找到**arr【I】**的 MSB](https://www.geeksforgeeks.org/find-significant-set-bit-number/) ，并将 **freq** 中的 MSB 计数增加 **1** 。
*   初始化一个变量，比如**对**，来存储总对的计数。
*   [遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)并将对更新为**对+=(freq[I]–1)**。
*   完成以上步骤后，打印**对**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// pairs whose Bitwise AND is
// greater than the Bitwise XOR
int countPairs(int arr[], int N)
{
    // Stores the frequency of
    // MSB of array elements
    unordered_map<int, int> freq;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Increment count of numbers
        // having MSB at log(arr[i])
        freq[log2(arr[i])]++;
    }

    // Stores total number of pairs
    int pairs = 0;

    // Traverse the Map
    for (auto i : freq) {
        pairs += i.second - 1;
    }

    // Return total count of pairs
    return pairs;
}

// Driver Code
int main()
{
    int arr[] = { 12, 9, 15, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// C# program for the above approach
import java.util.*;
class GFG {

  // Function to count the number of
  // pairs whose Bitwise AND is
  // greater than the Bitwise XOR
  static int countPairs(int[] arr, int N)
  {

    // Stores the frequency of
    // MSB of array elements
    HashMap<Integer, Integer> freq
      = new HashMap<Integer, Integer>();

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Increment count of numbers
      // having MSB at log(arr[i])
      if (freq.containsKey((int)(Math.log(arr[i]))))
        freq.put((int)(Math.log(arr[i])),
                 (int)(Math.log(arr[i])) + 1);
      else
        freq.put((int)(Math.log(arr[i])), 1);
    }

    // Stores total number of pairs
    int pairs = 0;

    // Traverse the Map
    for (Map.Entry<Integer, Integer> item :
         freq.entrySet())

    {
      pairs += item.getValue() - 1;
    }

    // Return total count of pairs
    return pairs;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int[] arr = { 12, 9, 15, 7 };
    int N = arr.length;
    System.out.println(countPairs(arr, N));
  }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log2

# Function to count the number of
# pairs whose Bitwise AND is
# greater than the Bitwise XOR
def countPairs(arr, N):

    # Stores the frequency of
    # MSB of array elements
    freq = {}

    # Traverse the array
    for i in range(N):

        # Increment count of numbers
        # having MSB at log(arr[i])
        x = int(log2(arr[i]))
        freq[x] = freq.get(x, 0) + 1

    # Stores total number of pairs
    pairs = 0

    # Traverse the Map
    for i in freq:
        pairs += freq[i] - 1

    # Return total count of pairs
    return pairs

# Driver Code
if __name__ == '__main__':
    arr = [12, 9, 15, 7]
    N = len(arr)
    print(countPairs(arr, N))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Function to count the number of
// pairs whose Bitwise AND is
// greater than the Bitwise XOR
static int countPairs(int []arr, int N)
{

    // Stores the frequency of
    // MSB of array elements
    Dictionary<int,int> freq = new Dictionary<int,int>();

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Increment count of numbers
        // having MSB at log(arr[i])
        if(freq.ContainsKey((int)(Math.Log(Convert.ToDouble(arr[i]),2.0))))
         freq[(int)(Math.Log(Convert.ToDouble(arr[i]),2.0))]++;
        else
          freq[(int)(Math.Log(Convert.ToDouble(arr[i]),2.0))] = 1;
    }

    // Stores total number of pairs
    int pairs = 0;

    // Traverse the Map
    foreach(var item in freq)
    {
        pairs += item.Value - 1;
    }

    // Return total count of pairs
    return pairs;
}

// Driver Code
public static void Main()
{
    int []arr = { 12, 9, 15, 7 };
    int N =  arr.Length;
    Console.WriteLine(countPairs(arr, N));
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of
// pairs whose Bitwise AND is
// greater than the Bitwise XOR
function countPairs(arr, N)
{
    // Stores the frequency of
    // MSB of array elements
    var freq = new Map();

    // Traverse the array
    for (var i = 0; i < N; i++) {

        // Increment count of numbers
        // having MSB at log(arr[i])
        if(freq.has(parseInt(Math.log2(arr[i]))))
        {
            freq.set(parseInt(Math.log2(arr[i])), freq.get(parseInt(Math.log2(arr[i])))+1);
        }
        else
        {
            freq.set(parseInt(Math.log2(arr[i])), 1);
        }
    }

    // Stores total number of pairs
    var pairs = 0;

    // Traverse the Map
    freq.forEach((value,key) => {
        pairs += value - 1;
    });

    // Return total count of pairs
    return pairs;
}

// Driver Code
var arr = [12, 9, 15, 7 ];
var N = arr.length;
document.write( countPairs(arr, N));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(32)