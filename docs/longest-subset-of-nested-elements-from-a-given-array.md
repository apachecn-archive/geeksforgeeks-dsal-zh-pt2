# 给定数组中嵌套元素的最长子集

> 原文:[https://www . geeksforgeeks . org/给定数组中嵌套元素的最长子集/](https://www.geeksforgeeks.org/longest-subset-of-nested-elements-from-a-given-array/)

给定一个由范围为**【0，N–1】**的数字排列组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是从数组中找到最长子集的长度，使得子集内的元素的形式为{ **arr[i]，arr[arr[i]]，arr[arr[arr[i]]，…}**

**示例:**

> **输入:** arr[] = {5，4，0，3，1，6，2}
> **输出:** 4
> **解释:**
> arr[arr[0]]等于 arr[5]
> arr[arr[arr[0]]等于 arr[6]
> arr[arr[arr[0]]等于 arr[2]
> 数组中可能的子集之一是{arr[0]，arr 因此，所需的输出为 4。
> 
> **输入:** arr[] ={3，1，4，0，2}
> **输出:** 2
> **解释:**
> arr[arr[0]]等于 arr[3]
> 数组中可能的子集之一是{arr[0]，arr[3]} = {3，0}
> 因此，需要的输出是 2。

**方法:**按照以下步骤解决问题:

*   初始化一个变量 **res = 0** 来存储满足条件的数组最长子集的长度。
*   [遍历阵列](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并执行以下操作:
    *   检查**arr【I】**是否等于 **i** 。如果发现为真，则更新 **res = max(res，1)** 。
    *   初始化一个变量，比如说**索引= i** ，来存储给定数组子集元素的索引。
    *   **arr[index]时迭代子集的元素！= index** ，将子集的当前元素更新为当前索引，同时更新**索引= arr【索引】**。
    *   最后，将 **res** 更新为 **res** 的最大值和当前子集中的元素数。
*   最后，打印 **res** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find length of longest subset
// such that subset { arr[i], arr[arr[i]], .. }
int arrayNesting(vector<int> arr)
{

  // Stores length of the longest subset
  // that satisfy the condition
  int res = 0;

  // Traverse in the array, arr[]
  for (int i = 0; i < arr.size(); i++)
  {

    // If arr[i] equals to i
    if (arr[i] == i)
    {

      // Update res
      res = max(res, 1);
    }
    else
    {

      // Count of elements in a subset
      int count = 0;

      // Stores index of elements in
      // the current subset
      int curr_index = i;

      // Calculate length of a subset that
      // satisfy the condition
      while (arr[curr_index] != curr_index)
      {
        int next_index = arr[curr_index];

        // Make visited the current index
        arr[curr_index] = curr_index;

        // Update curr_index
        curr_index = next_index;

        // Update count
        count++;
      }

      // Update res
      res = max(res, count);
    }
  }
  return res;
}

// Driver Code
int main()
{
  vector<int> arr = { 5, 4, 0, 3, 1, 6, 2 };
  int res = arrayNesting(arr);
  cout<<res;
}

// This code is contributed by mohit kumar 29.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;
import java.util.*;

class sol {

    // Function to find length of longest subset
    // such that subset { arr[i], arr[arr[i]], .. }
    public int arrayNesting(int[] arr)
    {

        // Stores length of the longest subset
        // that satisfy the condition
        int res = 0;

        // Traverse in the array, arr[]
        for (int i = 0; i < arr.length; i++) {

            // If arr[i] equals to i
            if (arr[i] == i) {

                // Update res
                res = Math.max(res, 1);
            }

            else {

                // Count of elements in a subset
                int count = 0;

                // Stores index of elements in
                // the current subset
                int curr_index = i;

                // Calculate length of a subset that
                // satisfy the condition
                while (arr[curr_index]
                       != curr_index) {

                    int next_index = arr[curr_index];

                    // Make visited the current index
                    arr[curr_index] = curr_index;

                    // Update curr_index
                    curr_index = next_index;

                    // Update count
                    count++;
                }

                // Update res
                res = Math.max(res, count);
            }
        }

        return res;
    }
}

// Driver Code
class GFG {
    public static void main(String[] args)
    {
        sol st = new sol();
        int[] arr = { 5, 4, 0, 3, 1, 6, 2 };
        int res = st.arrayNesting(arr);
        System.out.println(res);
    }
}
```

## C#

```
// C# program to implement
// the above approach
using System;
class sol {

  // Function to find length of longest subset
  // such that subset { arr[i], arr[arr[i]], .. }
  public int arrayNesting(int[] arr)
  {

    // Stores length of the longest subset
    // that satisfy the condition
    int res = 0;

    // Traverse in the array, arr[]
    for (int i = 0; i < arr.Length; i++) {

      // If arr[i] equals to i
      if (arr[i] == i) {

        // Update res
        res = Math.Max(res, 1);
      }

      else {

        // Count of elements in a subset
        int count = 0;

        // Stores index of elements in
        // the current subset
        int curr_index = i;

        // Calculate length of a subset that
        // satisfy the condition
        while (arr[curr_index] != curr_index) {

          int next_index = arr[curr_index];

          // Make visited the current index
          arr[curr_index] = curr_index;

          // Update curr_index
          curr_index = next_index;

          // Update count
          count++;
        }

        // Update res
        res = Math.Max(res, count);
      }
    }

    return res;
  }
}

// Driver Code
class GFG {
  static public void Main()
  {

    sol st = new sol();
    int[] arr = { 5, 4, 0, 3, 1, 6, 2 };
    int res = st.arrayNesting(arr);
    Console.WriteLine(res);
  }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find length of longest subset
# such that subset { arr[i], arr[arr[i]], .. }
def arrayNesting(arr) :

    # Stores length of the longest subset
    # that satisfy the condition
    res = 0

    # Traverse in the array, arr[]
    for i in range(len(arr)) :

        # If arr[i] equals to i
        if arr[i] == i :

            # Update res
            res = max(res, 1)

        else :

            # Count of elements in a subset
            count = 0

            # Stores index of elements in
            # the current subset
            curr_index = i

            # Calculate length of a subset that
            # satisfy the condition
            while arr[curr_index] != curr_index :

                next_index = arr[curr_index]

                # Make visited the current index
                arr[curr_index] = curr_index

                # Update curr_index
                curr_index = next_index

                # Update count
                count += 1

        # Update res
        res = max(res, count)
    return res

# Driver Code
if __name__ == "__main__" :

    arr = [ 5, 4, 0, 3, 1, 6, 2 ]
    res = arrayNesting(arr)
    print(res)

    # This code is contributed by jana_sayantam..
```

## java 描述语言

```
<script>
// javascript program of the above approach

    // Function to find length of longest subset
    // such that subset { arr[i], arr[arr[i]], .. }
    function arrayNesting(arr)
    {

        // Stores length of the longest subset
        // that satisfy the condition
        let res = 0;

        // Traverse in the array, arr[]
        for (let i = 0; i < arr.length; i++) {

            // If arr[i] equals to i
            if (arr[i] == i) {

                // Update res
                res = Math.max(res, 1);
            }

            else {

                // Count of elements in a subset
                let count = 0;

                // Stores index of elements in
                // the current subset
                let curr_index = i;

                // Calculate length of a subset that
                // satisfy the condition
                while (arr[curr_index]
                       != curr_index) {

                    let next_index = arr[curr_index];

                    // Make visited the current index
                    arr[curr_index] = curr_index;

                    // Update curr_index
                    curr_index = next_index;

                    // Update count
                    count++;
                }

                // Update res
                res = Math.max(res, count);
            }
        }

        return res;
    }

    // Driver Code

           let arr = [ 5, 4, 0, 3, 1, 6, 2 ];
        let res = arrayNesting(arr);
        document.write(res);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)