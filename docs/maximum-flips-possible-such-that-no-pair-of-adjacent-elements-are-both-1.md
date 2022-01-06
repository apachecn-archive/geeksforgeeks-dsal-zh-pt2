# 可能的最大翻转，使得没有一对相邻元素都是 1

> 原文:[https://www . geeksforgeeks . org/maximum-flips-可能-这样-没有相邻元素对-都是-1/](https://www.geeksforgeeks.org/maximum-flips-possible-such-that-no-pair-of-adjacent-elements-are-both-1/)

给定一个大小为 **N** 的[二进制数组](https://www.geeksforgeeks.org/sort-binary-array-using-one-traversal/)**arr【】**，任务是找到可转换为 **1** s 的 **0** s 的最大计数，使得没有一对相邻的数组元素是 **1** 。

**示例:**

> **输入:** arr[] = { 1，0，0，0，1 }
> **输出:** 1
> **解释:**
> 将 arr[2]更新为 1 会将 arr[]修改为{ 1，0，1，0，1 }
> 因此，所需的输出为 1
> 
> **输入:** arr[] = { 0，0，1，0，0，0，1，0，0 }
> **输出:** 3
> **解释:**
> 更新 arr[0]，arr[5]和 arr[9]将 arr[]修改为{ 1，0，1，0，0，1，0，1 }
> 因此，需要的输出为 3

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   [将 **0** 插在阵列](https://www.geeksforgeeks.org/c-program-to-insert-an-element-in-an-array/)的前端。
*   [遍历数组，arr[]](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) 。在每一次**的**迭代中，检查**arr【I】**、**arr【I+1】**和**arr【I+2】**是否为 **0** 。如果发现为真，则增加计数并更新 **arr[i + 1] = 1** 。
*   最后，打印获得的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum count of 0s
// required to be converted into 1s such
// no pair of adjacent elements are 1
void maxPositionsOccupied(vector<int>& arr)
{

    // Base Case
    if (arr.size() == 0) {
        cout << 0;
        return;
    }

    // Insert 0 at the end
    // of the array
    arr.push_back(0);

    // Insert 0 at the front
    // of the array
    arr.insert(arr.begin(), 0);

    // Stores the maximum count of of 0s
    // that can be converted into 1s
    int ans = 0;

    // Stores index of array elements
    int i = 0;

    // Traverse the array
    while ((i < arr.size() - 2)) {

        // If adjacent elements are 0s
        if ((arr[i] == 0) && (arr[i + 1] == 0)
            && (arr[i + 2] == 0)) {

            // Update ans
            ans++;

            // Update arr[i + 1]
            arr[i + 1] = 1;
        }

        // Update i
        i++;
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    // Given binary array
    vector<int> arr = { 1, 0, 0, 0, 1 };

    // Prints the maximum 0 to 1
    // conversions required
    maxPositionsOccupied(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

  // Function to find the maximum count of 0s
  // required to be converted into 1s such
  // no pair of adjacent elements are 1
  static void maxPositionsOccupied(int[] arr)
  {

    // Base Case
    if (arr.length == 0)
    {
      System.out.print(0);
      return;
    }

    // Stores the maximum count of of 0s
    // that can be converted into 1s
    int ans = 0;

    // Stores index of array elements
    int i = 0;

    // Traverse the array
    while ((i < arr.length - 2))
    {

      // If adjacent elements are 0s
      if ((arr[i] == 0) &&
          (arr[i + 1] == 0) &&
          (arr[i + 2] == 0))
      {

        // Update ans
        ans++;

        // Update arr[i + 1]
        arr[i + 1] = 1;
      }

      // Update i
      i++;
    }

    // Print the answer
    System.out.print(ans);
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given binary array
    int[] arr = { 1, 0, 0, 0, 1 };

    // Prints the maximum 0 to 1
    // conversions required
    maxPositionsOccupied(arr);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum count of 0s
# required to be converted into 1s such
# no pair of adjacent elements are 1
def maxPositionsOccupied(arr):

    # Base Case
    if (len(arr) == 0):
        print(0)

    # Insert 0 at the end
    # of the array
    arr.append(0)

    # Insert 0 at the front
    # of the array
    arr.insert(0, 0)

    # Stores the maximum count of of 0s
    # that can be converted into 1s
    ans = 0

    # Stores index of array elements
    i = 0

    # Traverse the array
    while((i < len(arr) - 2)):

        # If adjacent elements are 0s
        if ((arr[i] == 0) and
            (arr[i + 1] == 0) and
            (arr[i + 2] == 0)):

            # Update ans
            ans += 1

            # Update arr[i + 1]
            arr[i + 1] = 1

        # Update i
        i += 1

    # Print the answer
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given binary array
    arr =  [ 1, 0, 0, 0, 1 ]

    # Prints the maximum 0 to 1
    # conversions required
    maxPositionsOccupied(arr)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum count of 0s
// required to be converted into 1s such
// no pair of adjacent elements are 1
static void maxPositionsOccupied(int[] arr)
{

    // Base Case
    if (arr.Length == 0)
    {
        Console.Write(0);
        return;
    }

    // Stores the maximum count of of 0s
    // that can be converted into 1s
    int ans = 0;

    // Stores index of array elements
    int i = 0;

    // Traverse the array
    while ((i < arr.Length - 2))
    {

        // If adjacent elements are 0s
        if ((arr[i] == 0) &&
            (arr[i + 1] == 0) &&
            (arr[i + 2] == 0))
        {

            // Update ans
            ans++;

            // Update arr[i + 1]
            arr[i + 1] = 1;
        }

        // Update i
        i++;
    }

    // Print the answer
    Console.Write(ans);
}  

// Driver code
static void Main()
{

    // Given binary array
    int[] arr = { 1, 0, 0, 0, 1 };

    // Prints the maximum 0 to 1
    // conversions required
    maxPositionsOccupied(arr);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // Javascript program for the above approach

    // Function to find the maximum count of 0s
    // required to be converted into 1s such
    // no pair of adjacent elements are 1
    function maxPositionsOccupied(arr)
    {

        // Base Case
        if (arr.length == 0)
        {
            document.write(0);
            return;
        }

        // Stores the maximum count of of 0s
        // that can be converted into 1s
        let ans = 0;

        // Stores index of array elements
        let i = 0;

        // Traverse the array
        while ((i < arr.length - 2))
        {

            // If adjacent elements are 0s
            if ((arr[i] == 0) &&
                (arr[i + 1] == 0) &&
                (arr[i + 2] == 0))
            {

                // Update ans
                ans++;

                // Update arr[i + 1]
                arr[i + 1] = 1;
            }

            // Update i
            i++;
        }

        // Print the answer
        document.write(ans);
    }

    // Given binary array
    let arr = [ 1, 0, 0, 0, 1 ];

    // Prints the maximum 0 to 1
    // conversions required
    maxPositionsOccupied(arr);

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)