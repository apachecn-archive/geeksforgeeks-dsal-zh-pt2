# 找到一个数字 K，使得恰好 K 个数组元素大于或等于 K

> 原文:[https://www . geesforgeks . org/find-a-number-k-so-the-just-k-array-elements-大于或等于-k/](https://www.geeksforgeeks.org/find-a-number-k-such-that-exactly-k-array-elements-are-greater-than-or-equal-to-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**a【】**，其中只包含非负元素，任务是找到任意整数 **K** ，其中恰好有大于或等于 **K** 的 **K** 数组元素。如果不存在这样的 **K** ，则打印 **-1** 。

**示例:**

> **输入:** a[] = {7，8，9，0，0，1}
> **输出** : 3
> **说明:**
> 既然 3 小于等于 7，8，9，那么，3 就是答案。
> 
> **输入:** a[] = {0，0}
> **输出:** -1

**进场:**任务是找到 **K** 使阵元大于等于 **K** 。因此， **K** 不能超过数组**a【n】**中存在的[最大元素。按照以下步骤解决问题:](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

1.  [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)到[找到最大的数组元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)，存储在变量中，比如说 **m** 。
2.  初始化一个计数器变量 **cnt** 来计算大于或等于 **K** 的数组元素的数量。
3.  从 **0** 到 **m** 迭代 **K** 的可能值。[对每个值迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，[计算大于或等于该值的数组元素的数量](https://www.geeksforgeeks.org/queries-to-count-array-elements-greater-than-or-equal-to-a-given-number-with-updates/)。
4.  如果对于任何值，精确地 **K** 数组元素被发现大于或等于该值，打印该值。
5.  如果完成数组遍历后没有得到这样的值，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find K for which
// there are exactly K array
// elements greater than or equal to K
int zvalue(vector<int>& nums)
{

    // Finding the largest array element
    int m = *max_element(nums.begin(),
                         nums.end());
    int cnt = 0;

    // Possible values of K
    for (int i = 0; i <= m; i++) {
        cnt = 0;

        // Traverse the array
        for (int j = 0; j < nums.size(); j++) {

            // If current array element is
            // greater than or equal to i
            if (nums[j] >= i)
                cnt++;
        }

        // If i array elements are
        // greater than or equal to i
        if (cnt == i)
            return i;
    }

    // Otherwise
    return -1;
}

// Driver Code
int main()
{
    vector<int> nums = { 7, 8, 9, 0, 0, 1 };
    cout << zvalue(nums) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find K for which
// there are exactly K array
// elements greater than or equal to K
public static int zvalue(int[] nums)
{

    // Finding the largest array element
    int m = max_element(nums);
    int cnt = 0;

    // Possible values of K
    for(int i = 0; i <= m; i++)
    {
        cnt = 0;

        // Traverse the array
        for(int j = 0; j < nums.length; j++)
        {

            // If current array element is
            // greater than or equal to i
            if (nums[j] >= i)
                cnt++;
        }

        // If i array elements are
        // greater than or equal to i
        if (cnt == i)
            return i;
    }

    // Otherwise
    return -1;
}

// To find maximum Element
public static int max_element(int[] nums)
{
    int max = nums[0];
    for(int i = 1; i < nums.length; i++)
        max = Math.max(max, nums[i]);

    return max;
}

// Driver Code
public static void main(String args[])
{
    int[] nums = { 7, 8, 9, 0, 0, 1 };

    System.out.println(zvalue(nums));
}
}

// This code is contributed by hemanth gadarla
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find K for which
# there are exactly K array
# elements greater than or equal to K
def zvalue(nums):

    # Finding the largest array element
    m = max(nums)
    cnt = 0

    # Possible values of K
    for i in range(0, m + 1, 1):
        cnt = 0

        # Traverse the array
        for j in range(0, len(nums), 1):

            # If current array element is
            # greater than or equal to i
            if (nums[j] >= i):
                cnt += 1

        # If i array elements are
        # greater than or equal to i
        if (cnt == i):
            return i

    # Otherwise
    return -1

# Driver Code
if __name__ == '__main__':

    nums =  [ 7, 8, 9, 0, 0, 1 ]

    print(zvalue(nums))

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the
// above approach
using System;
class GFG{

// Function to find K for which
// there are exactly K array
// elements greater than or equal to K
public static int zvalue(int[] nums)
{
  // Finding the largest array element
  int m = max_element(nums);
  int cnt = 0;

  // Possible values of K
  for(int i = 0; i <= m; i++)
  {
    cnt = 0;

    // Traverse the array
    for(int j = 0;
            j < nums.Length; j++)
    {
      // If current array element is
      // greater than or equal to i
      if (nums[j] >= i)
        cnt++;
    }

    // If i array elements are
    // greater than or equal to i
    if (cnt == i)
      return i;
  }

  // Otherwise
  return -1;
}

// To find maximum Element
public static int max_element(int[] nums)
{
  int max = nums[0];

  for(int i = 1; i < nums.Length; i++)
    max = Math.Max(max, nums[i]);

  return max;
}

// Driver Code
public static void Main(String []args)
{
  int[] nums = {7, 8, 9, 0, 0, 1};
  Console.WriteLine(zvalue(nums));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to find K for which
// there are exactly K array
// elements greater than or equal to K
function zvalue(nums)
{

    // Finding the largest array element
    var m = max_element(nums);
    var cnt = 0;

    // Possible values of K
    for(i = 0; i <= m; i++)
    {
        cnt = 0;

        // Traverse the array
        for(j = 0; j < nums.length; j++)
        {

            // If current array element is
            // greater than or equal to i
            if (nums[j] >= i)
                cnt++;
        }

        // If i array elements are
        // greater than or equal to i
        if (cnt == i)
            return i;
    }

    // Otherwise
    return -1;
}

// To find maximum Element
function max_element(nums)
{
    var max = nums[0];
    for(i = 1; i < nums.length; i++)
        max = Math.max(max, nums[i]);

    return max;
}

// Driver Code
nums = [ 7, 8, 9, 0, 0, 1 ];

document.write(zvalue(nums));

// This code contributed by shikhasingrajput

</script>
```

**Output**

```
3

```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**

1.  找到数组中的最大元素并存储它。
2.  创建一个大小为(最大元素+1)的计数数组，并初始化为 0。
3.  遍历给定数组，并增加计数数组中相应索引的元素计数
    *   即，如果(nums[i] == j)，则计数[j]=计数[j]+1
4.  求计数数组的后缀和
    1.  从右向左遍历计数数组，并使用其右侧所有剩余数组元素计数的总和更新计数值
5.  再次遍历 count 数组，对于任何索引== count[index]，返回 index
6.  否则返回-1

## C++

```
#include <bits/stdc++.h>
using namespace std;
int solve(vector<int>& nums)
{
    // Finding the maximum element
    int max = *max_element(nums.begin(), nums.end());
    // initialising the count to 0 for all indices
    int count[max + 1] = { 0 };
    // incrementing count of corresponding element in the
    // count array
    for (int i = 0; i < nums.size(); i++) {
        count[nums[i]]++;
    }
    // corner case
    if (count[max] == max)
        return max;
    // finding suffix sum
    for (int j = max - 1; j >= 0; j--) {
        count[j] += count[j + 1];
        // Checking the index after updating the count
        if (j == count[j]) {
            return j;
        }
    }
    return -1;
}
// Driver Code
int main()
{
    vector<int> v = { 2, 0, 0 };
    cout << solve(v);
}

// This code is contributed by Maneesh Gupta NVSS
```

**Output**

```
1
```

**时间复杂度:** *O (N)* 其中 N 为最大值(nums.size()，max element)

**空间复杂度:** *O ( max 元素)*