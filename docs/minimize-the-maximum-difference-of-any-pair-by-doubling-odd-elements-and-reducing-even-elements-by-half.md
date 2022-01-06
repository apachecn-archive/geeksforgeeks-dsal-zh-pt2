# 将奇数元素加倍，偶数元素减半，使任意一对的最大差值最小

> 原文:[https://www . geeksforgeeks . org/通过将奇数元素加倍并将偶数元素减半来最小化任意对的最大差值/](https://www.geeksforgeeks.org/minimize-the-maximum-difference-of-any-pair-by-doubling-odd-elements-and-reducing-even-elements-by-half/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过将任意奇数数组元素乘以 **2** 并将任意偶数数组元素除以 **2** 来最小化任意一对数组元素之间的最大差异。

**示例:**

> **输入:** arr[] = {4，1，5，20，3}
> **输出:** 3
> **解释:**
> 操作 1:将 arr[1]乘以 2 将 arr[]修改为{4，2，5，20，3}。
> 操作 2:将 arr[3]除以 2 将 arr[]修改为{4，2，5，10，3}。
> 操作 3:将 arr[3]除以 2 将 arr[]修改为{4，2，5，5，3}。
> 因此，数组中任意一对的最大差值的最小值= 5–2 = 3。
> 
> **输入:** arr[] = {1，2，5，9}
> **输出:** 7
> **解释:**
> 运算 1:arr[0]乘以 2 将 arr[]修改为{2，2，5，9 }
> 运算 2:arr[2]乘以 2 将 arr[]修改为{ 2，2，10，9 }
> 因此，数组中任意对的最大差的最小值= 9–2 = 7。

**方法:**按照以下步骤解决给定问题:

*   首先，在一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/) **S** 中插入所有数组元素。[如果数组元素为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则按原样插入。否则，通过**乘以 2** 将其转换为偶数。
*   将集合中最后一个元素[和第一个元素**之间的差异存储在一个变量中，比如 **res** 。**](https://www.geeksforgeeks.org/setbegin-setend-c-stl)
*   [以相反的顺序](https://www.geeksforgeeks.org/how-to-traverse-a-c-set-in-reverse-direction/)遍历集合 **S** ，并执行以下操作:
    *   将 res 值更新为 **res** 的最大值以及集合的第一个元素和当前元素之间的差值。
    *   [从集合中移除当前元素。](https://www.geeksforgeeks.org/seterase-c-stl/)
    *   [将**(当前元素)/ 2** 插入集合。](https://www.geeksforgeeks.org/set-insert-function-in-c-stl/)
    *   如果当前元素的值是奇数，那么没有更多的数组元素可以使最大差值变小。因此[脱离循环](https://www.geeksforgeeks.org/break-statement-cc/)。
*   完成上述步骤后，打印 **res** 的值作为合成差值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to minimize the maximum
// difference between any pair of elements
// of the array by the given operations
int minimumMaxDiff(vector<int>& nums)
{
    set<int> s;

    // Traverse the array
    for (int i = 0; i < nums.size(); i++) {

        // If current element is even
        if (nums[i] % 2 == 0)

            // Insert it into even
            s.insert(nums[i]);

        // Otherwise
        else

            // Make it even by multiplying
            // by 2 and insert it into set
            s.insert(nums[i] * 2);
    }

    // Calculate difference between first
    // and the last element of the set
    int res = *s.rbegin() - *s.begin();

    // Iterate until difference is minimized
    while (*s.rbegin() % 2 == 0) {
        int x = *s.rbegin();

        // Erase the current element
        s.erase(x);

        // Reduce current element by half
        // and insert it into the Set
        s.insert(x / 2);

        // Update difference
        res = min(res, *s.rbegin()
                           - *s.begin());
    }

    // Return the resultant difference
    return res;
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 5, 9 };
    cout << minimumMaxDiff(arr);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG
{

  // Function to minimize the maximum
  // difference between any pair of elements
  // of the array by the given operations
  static int minimumMaxDiff(int[] nums)
  {
    TreeSet<Integer> s = new TreeSet<Integer>();

    // Traverse the array
    for (int i = 0; i < nums.length; i++)
    {

      // If current element is even
      if (nums[i] % 2 == 0)

        // Insert it into even
        s.add(nums[i]);

      // Otherwise
      else

        // Make it even by multiplying
        // by 2 and insert it into set
        s.add(nums[i] * 2);
    }

    // Calculate difference between first
    // and the last element of the set
    int res = s.last() - s.first();

    // Iterate until difference is minimized
    while (s.last() % 2 == 0)
    {
      int x = s.last();

      // Erase the current element
      s.remove(x);

      // Reduce current element by half
      // and insert it into the Set
      s.add(x / 2);

      // Update difference
      res = Math.min(res, s.last() - s.first());
    }

    // Return the resultant difference
    return res;
  }

  // Driver code
  public static void main(String[] args)
  {
    int[] arr = new int[] { 1, 2, 5, 9 };
    System.out.print(minimumMaxDiff(arr));
  }
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to minimize the maximum
# difference between any pair of elements
# of the array by the given operations
def minimumMaxDiff(nums):

    s = {}

    # Traverse the array
    for i in range(len(nums)):

        # If current element is even
        if (nums[i] % 2 == 0):

            # Insert it into even
            s[nums[i]] = 1

        # Otherwise
        else:

            # Make it even by multiplying
            # by 2 and insert it into set
            s[nums[i] * 2] = 1

    # Calculate difference between first
    # and the last element of the set
    sr = list(s.keys())
    res = sr[-1] - sr[0]

    # Iterate until difference is minimized
    while (list(s.keys())[-1] % 2 == 0):
        r = list(s.keys())
        x = r[-1]

        # Erase the current element
        del s[x]

        # Reduce current element by half
        # and insert it into the Set
        s[x // 2] = 1

        rr = list(s.keys())

        # Update difference
        res = min(res, rr[-1] - r[0])

    # Return the resultant difference
    return res

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 5, 9 ]

    print (minimumMaxDiff(arr))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
using System.Linq; 

class GFG
{

  // Function to minimize the maximum
  // difference between any pair of elements
  // of the array by the given operations
  static int minimumMaxDiff(int[] nums)
  {
    HashSet<int> s = new HashSet<int>();

    // Traverse the array
    for (int i = 0; i < nums.Length; i++) {

      // If current element is even
      if (nums[i] % 2 == 0)

        // Insert it into even
        s.Add(nums[i]);

      // Otherwise
      else

        // Make it even by multiplying
        // by 2 and insert it into set
        s.Add(nums[i] * 2);
    }

    // Calculate difference between first
    // and the last element of the set
    int res = s.Last() - s.First();

    // Iterate until difference is minimized
    while (s.Last() % 2 == 0) {
      int x = s.Last();

      // Erase the current element
      s.Remove(x);

      // Reduce current element by half
      // and insert it into the Set
      s.Add(x / 2);

      // Update difference
      res = Math.Min(res, s.Last() - s.First());
    }

    // Return the resultant difference
    return res;
  }

  // Driver code
  static public void Main()
  {
    int[] arr = new int[] { 1, 2, 5, 9 };
    Console.WriteLine(minimumMaxDiff(arr));
  }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to minimize the maximum
// difference between any pair of elements
// of the array by the given operations
function minimumMaxDiff( nums)
{
    var s = new Set();

    // Traverse the array
    for (var i = 0; i < nums.length; i++) {

        // If current element is even
        if (nums[i] % 2 == 0)

            // Insert it into even
            s.add(nums[i]);

        // Otherwise
        else

            // Make it even by multiplying
            // by 2 and insert it into set
            s.add(nums[i] * 2);
    }

    // Calculate difference between first
    // and the last element of the set
    var tmp = [...s].sort((a,b)=>a-b)
    var res = tmp[tmp.length-1] - tmp[0];

    // Iterate until difference is minimized
    while (tmp[tmp.length-1] % 2 == 0) {
        var x = tmp[tmp.length-1];

        // Erase the current element
        s.delete(x);

        // Reduce current element by half
        // and insert it into the Set
        s.add(parseInt(x / 2));
        tmp = [...s].sort((a,b)=>a-b)

        // Update difference
        res = Math.min(res,tmp[tmp.length-1]
                           - tmp[0]);
    }

    // Return the resultant difference
    return res;
}

// Driver Code
var arr = [1, 2, 5, 9];
document.write( minimumMaxDiff(arr));

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*