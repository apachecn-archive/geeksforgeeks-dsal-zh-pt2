# 用数组元素的和替换任意一对数组元素使所有数组元素均匀

> 原文:[https://www . geeksforgeeks . org/通过用它们的和替换任意一对数组元素来制造所有数组元素偶数/](https://www.geeksforgeeks.org/make-all-array-elements-even-by-replacing-any-pair-of-array-elements-with-their-sum/)

给定一个由正整数 **N** 组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是通过用它们的和替换任意一对数组元素来使所有数组元素均匀。

**示例:**

> **输入:** arr[] = {5，6，3，7，20}
> **输出:** 3
> **解释:**
> **操作 1:** 用 arr[0]和 arr[2]的和来替换它们(= 5 + 3 = 8)将 arr[]修改为{8，6，8，7，20}。
> **操作 2:** 将 arr[2]和 arr[3]替换为它们的和(= 7 + 8 = 15)将 arr[]修改为{8，6，15，15，20}。
> **操作 3:** 将 arr[2]和 arr[3]替换为它们的和(= 15 + 15 = 30)将 arr[]修改为{8，6，30，30，20}。
> 
> **输入:** arr[] = {2，4，16，8，7，9，3，1}
> **输出:** 2

**方法:**思路是不断用两个奇数数组元素的和替换它们，直到所有数组元素都是偶数。按照以下步骤解决问题:

*   初始化一个变量，比如**移动**，以存储所需的最小替换次数。
*   [计算给定数组中奇数元素的总数](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)并将其存储在一个变量中，比如 **cnt** 。
*   [如果 **cnt** 的值为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则打印 **(cnt / 2 + 2)** 作为结果。否则，打印 **cnt / 2** 作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of replacements required to make
// all array elements even
void minMoves(int arr[], int N)
{
    // Stores the count of odd elements
    int odd_element_cnt = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Increase count of odd elements
        if (arr[i] % 2 != 0) {
            odd_element_cnt++;
        }
    }

    // Store number of replacements required
    int moves = (odd_element_cnt) / 2;

    // Two extra moves will be required
    // to make the last odd element even
    if (odd_element_cnt % 2 != 0)
        moves += 2;

    // Print the minimum replacements
    cout << moves;
}

// Driver Code
int main()
{
    int arr[] = { 5, 6, 3, 7, 20 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    minMoves(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to find the minimum number
// of replacements required to make
// all array elements even
static void minMoves(int arr[], int N)
{

    // Stores the count of odd elements
    int odd_element_cnt = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // Increase count of odd elements
        if (arr[i] % 2 != 0)
        {
            odd_element_cnt++;
        }
    }

    // Store number of replacements required
    int moves = (odd_element_cnt) / 2;

    // Two extra moves will be required
    // to make the last odd element even
    if (odd_element_cnt % 2 != 0)
        moves += 2;

    // Print the minimum replacements
    System.out.print(moves);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 6, 3, 7, 20 };
    int N = arr.length;

    // Function call
    minMoves(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
public class GFG
{

  // Function to find the minimum number
  // of replacements required to make
  // all array elements even
  static void minMoves(int []arr, int N)
  {

    // Stores the count of odd elements
    int odd_element_cnt = 0;

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // Increase count of odd elements
      if (arr[i] % 2 != 0)
      {
        odd_element_cnt++;
      }
    }

    // Store number of replacements required
    int moves = (odd_element_cnt) / 2;

    // Two extra moves will be required
    // to make the last odd element even
    if (odd_element_cnt % 2 != 0)
      moves += 2;

    // Print the minimum replacements
    Console.Write(moves);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = { 5, 6, 3, 7, 20 };
    int N = arr.Length;

    // Function call
    minMoves(arr, N);
  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum number
# of replacements required to make
# all array elements even
def minMoves(arr, N):

    # Stores the count of odd elements
    odd_element_cnt = 0;

    # Traverse the array
    for i in range(N):

        # Increase count of odd elements
        if (arr[i] % 2 != 0):
            odd_element_cnt += 1;

    # Store number of replacements required
    moves = (odd_element_cnt) // 2;

    # Two extra moves will be required
    # to make the last odd element even
    if (odd_element_cnt % 2 != 0):
        moves += 2;

    # Prthe minimum replacements
    print(moves);

# Driver Code
if __name__ == '__main__':
    arr = [5, 6, 3, 7, 20];
    N = len(arr);

    # Function call
    minMoves(arr, N);

    # This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Function to find the minimum number
// of replacements required to make
// all array elements even
function minMoves(arr, N)
{
    // Stores the count of odd elements
    var odd_element_cnt = 0;

    var i;
    // Traverse the array
    for(i = 0; i < N; i++) {

        // Increase count of odd elements
        if (arr[i] % 2 != 0) {
            odd_element_cnt++;
        }
    }

    // Store number of replacements required
    var moves = Math.floor((odd_element_cnt)/2);

    // Two extra moves will be required
    // to make the last odd element even
    if (odd_element_cnt % 2 != 0)
        moves += 2;

    // Print the minimum replacements
    document.write(moves);
}

// Driver Code
    var arr = [5, 6, 3, 7, 20];
    N =  arr.length;

    // Function call
    minMoves(arr, N);

</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)