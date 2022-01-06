# 数组中每个元素等于另一个元素的索引的对的计数

> 原文:[https://www . geesforgeks . org/每元素等于数组中其他元素的索引的对计数/](https://www.geeksforgeeks.org/count-of-pairs-having-each-element-equal-to-index-of-the-other-from-an-array/)

给定一个整数 **N** 和一个包含范围**【1，N】**中的元素的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到所有对的计数 **(arr[i]，arr[j])** ，使得 **i < j** 和 **i == arr[j]和 j == arr[i]** 。
**示例:**

> **输入:** N = 4，arr[] = {2，1，4，3}
> **输出:** 2
> **解释:**
> 所有可能的对都是{1，2}和{3，4}
> **输入:** N = 5，arr[] = {5，5，5，5，1}
> **输出:** 1
> **解释:**
> 只有可能

**天真方法:**
最简单的方法是[生成给定数组的所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，如果任何对满足给定条件，则增加**计数**。最后，打印**计数**的值。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*
**高效进场:**
按照以下步骤解决以上进场:

*   遍历给定的数组并保持其索引等于**arr[arr[index]–1]–1**的元素(比如 **cnt** )的计数。这将计算具有给定标准的有效对。
*   遍历后，总计数由 **cnt/2** 给出，因为我们在上面的遍历中每对计数两次。

以下是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to print the count of pair
void countPairs(int N, int arr[])
{
    int count = 0;

    // Iterate over all the
    // elements of the array
    for(int i = 0; i < N; i++)
    {
        if (i == arr[arr[i] - 1] - 1)
        {

            // Increment the count
            count++;
        }
    }

    // Print the result
    cout << (count / 2) << endl;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 4, 3 };
    int N = sizeof(arr)/sizeof(arr[0]);

    countPairs(N, arr);
}

// This code is contributed by Amit Katiyar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
import java.util.*;

class GFG {

    // Function to print the count of pair
    static void countPairs(int N, int[] arr)
    {
        int count = 0;

        // Iterate over all the
        // elements of the array
        for (int i = 0; i < N; i++) {

            if (i == arr[arr[i] - 1] - 1) {

                // Increment the count
                count++;
            }
        }

        // Print the result
        System.out.println(count / 2);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 2, 1, 4, 3 };
        int N = arr.length;

        countPairs(N, arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
# Function to print the count of pair
def countPairs(N, arr):

    count = 0

    # Iterate over all the
    # elements of the array
    for i in range(N):
        if (i == arr[arr[i] - 1] - 1):

            # Increment the count
            count += 1

    # Print the result
    print(count // 2)

# Driver Code
if __name__ == "__main__":

    arr = [2, 1, 4, 3]
    N = len(arr)
    countPairs(N, arr)

# This code is contributed by Chitranayal
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG{

  // Function to print the count of pair
  static void countPairs(int N, int[] arr)
  {
    int count = 0;

    // Iterate over all the
    // elements of the array
    for (int i = 0; i < N; i++)
    {
      if (i == arr[arr[i] - 1] - 1)
      {

        // Increment the count
        count++;
      }
    }

    // Print the result
    Console.Write(count / 2);
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] arr = { 2, 1, 4, 3 };
    int N = arr.Length;

    countPairs(N, arr);
  }
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Function to print the count of pair
    function countPairs(N, arr)
    {
        let count = 0;

        // Iterate over all the
        // elements of the array
        for(let i = 0; i < N; i++)
        {
            if (i == arr[arr[i] - 1] - 1)
            {

                // Increment the count
                count++;
            }
        }

        // Print the result
        document.write(count / 2);
    }

    let arr = [ 2, 1, 4, 3 ];
    let N = arr.length;

    countPairs(N, arr);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)