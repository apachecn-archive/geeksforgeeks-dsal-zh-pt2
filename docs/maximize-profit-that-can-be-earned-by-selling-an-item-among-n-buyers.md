# 在 N 个买家中销售一件商品可以获得的利润最大化

> 原文:[https://www . geeksforgeeks . org/通过在 n 个买家中销售一件物品来获得最大利润/](https://www.geeksforgeeks.org/maximize-profit-that-can-be-earned-by-selling-an-item-among-n-buyers/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到物品的价格，使得在 **N** 个买家中销售物品所获得的利润最大可能由 **N** 个买家的预算组成。如果买方的**预算大于或等于**至**物品价格**，物品可以出售给任何买方。

**示例:**

> **输入:** arr[] = {34，78，90，15，67}
> **输出:** 67
> **说明:**对于价格为 67 的物品，可以购买该物品的买家数量为 3 个。所以赚到的利润是 67 * 3 = 201，是最大的。
> 
> **输入:** arr[] = {300，50，32，43，42 }
> T3】输出: 300

**天真方法:**按照以下步骤解决问题:

*   初始化两个变量，将**价格**和**利润**设为 **0** ，分别存储一个物品的销售利润和该物品的可能价格。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   将项目价格设置为**arr【I】**。
    *   通过遍历给定的数组，找出预算至少为**arr【I】**的买家数量。让值为**计数**。
    *   如果 **count*arr[i]** 的值大于**利润**，则将**利润**更新为 **count*arr[i]** ，将**价格**更新为 **arr[i]** 。
*   完成上述步骤后，打印**价格**的值作为合成价格。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
#include <climits>
#include <algorithm>
using namespace std;

// Function to find the maximum profit
// earned by selling an item among
// N buyers
int maximumProfit(int arr[],int N)
{

  // Stores the maximum profit
  int ans = INT_MIN;

  // Stores the price of the item
  int price = 0;

  // Sort the array
  sort(arr, arr + N);

  // Traverse the array
  for (int i = 0; i < N; i++)
  {

    // Count of buyers with
    // budget >= arr[i]
    int count = (N - i);

    // Update the maximum profit
    if (ans < count * arr[i])
    {
      price = arr[i];
      ans = count * arr[i];
    }
  }

  // Return the maximum possible
  // price
  return price;
}

// Driver code
int main()
{
  int arr[] = { 22, 87, 9, 50, 56, 43 };
  cout << maximumProfit(arr,6);
  return 0;
}

// This code is contributed by le0.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the maximum profit
    // earned by selling an item among
    // N buyers
    public static int maximumProfit(int arr[])
    {
        // Stores the maximum profit
        int ans = Integer.MIN_VALUE;

        // Stores the price of the item
        int price = 0;

        int n = arr.length;

        // Traverse the array
        for (int i = 0; i < n; i++) {

            // Count of buyers with
            // budget >= arr[i]
            int count = 0;

            for (int j = 0; j < n; j++) {

                if (arr[i] <= arr[j]) {

                    // Increment count
                    count++;
                }
            }

            // Update the maximum profit
            if (ans < count * arr[i]) {
                price = arr[i];
                ans = count * arr[i];
            }
        }

        // Return the maximum possible
        // price
        return price;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 22, 87, 9, 50, 56, 43 };
        System.out.print(
            maximumProfit(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the maximum profit
# earned by selling an item among
# N buyers
def maximumProfit(arr, N):

    # Stores the maximum profit
    ans = -sys.maxsize - 1

    # Stores the price of the item
    price = 0

    # Sort the array
    arr.sort()

    # Traverse the array
    for i in range(N):

        # Count of buyers with
        # budget >= arr[i]
        count = (N - i)

        # Update the maximum profit
        if (ans < count * arr[i]):

            price = arr[i]
            ans = count * arr[i]

    # Return the maximum possible
    # price
    return price

# Driver code
if __name__ == "__main__":

    arr = [22, 87, 9, 50, 56, 43]

    print(maximumProfit(arr, 6))

# This code is contributed by ukasp
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to find the maximum profit
  // earned by selling an item among
  // N buyers
  public static int maximumProfit(int[] arr)
  {

    // Stores the maximum profit
    int ans = Int32.MinValue;

    // Stores the price of the item
    int price = 0;

    int n = arr.Length;

    // Traverse the array
    for (int i = 0; i < n; i++) {

      // Count of buyers with
      // budget >= arr[i]
      int count = 0;

      for (int j = 0; j < n; j++) {

        if (arr[i] <= arr[j]) {

          // Increment count
          count++;
        }
      }

      // Update the maximum profit
      if (ans < count * arr[i]) {
        price = arr[i];
        ans = count * arr[i];
      }
    }

    // Return the maximum possible
    // price
    return price;
  }

  // Driver Code
  public static void Main(string[] args)
  {
    int[] arr = { 22, 87, 9, 50, 56, 43 };
    Console.Write(
      maximumProfit(arr));
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the maximum profit
// earned by selling an item among
// N buyers
function maximumProfit( arr, N)
{

  // Stores the maximum profit
  let ans = Number.MIN_VALUE;

  // Stores the price of the item
  let price = 0;

  // Sort the array
  arr.sort(function(a,b){return a-b});

  // Traverse the array
  for (let i = 0; i < N; i++)
  {

    // Count of buyers with
    // budget >= arr[i]
    let count = (N - i);

    // Update the maximum profit
    if (ans < count * arr[i])
    {
      price = arr[i];
      ans = count * arr[i];
    }
  }

  // Return the maximum possible
  // price
  return price;
}

// Driver code
let arr = [ 22, 87, 9, 50, 56, 43 ];
document.write( maximumProfit(arr,6));

</script>
```

**Output**

```
43
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方式:**上述方式可以通过[对数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序进行优化，使得大于当前元素的元素个数可以在*T5【O(1)*时间进行计算。按照以下步骤解决问题:

*   初始化两个变量，将**价格**和**利润**设为 **0** ，分别存储一个物品的销售利润和该物品的可能价格。
*   [按升序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   [遍历给定数组**arr【I】**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并执行以下步骤:
    *   将项目价格设置为**arr【I】**。
    *   现在，预算至少为**arr【I】**的买家数量由**(N–I)**给出。让值为**计数**。
    *   如果 **count*arr[i]** 的值大于**利润**，则将**利润**更新为 **count*arr[i]** ，将**价格**更新为 **arr[i]** 。
*   完成上述步骤后，打印**价格**的值作为合成价格。

下面是上述方法的实现:

## C++

```
#include <iostream>
#include <climits>
#include <algorithm>
using namespace std;
// Function to find the maximum profit
// earned by selling an item among
// N buyers
int maximumProfit(int arr[],int n)
{
  // Stores the maximum profit
  int ans = INT_MIN;

  // Stores the price of the item
  int price = 0;

  // Traverse the array
  for (int i = 0; i < n; i++) {

    // Count of buyers with
    // budget >= arr[i]
    int count = 0;

    for (int j = 0; j < n; j++) {

      if (arr[i] <= arr[j]) {

        // Increment count
        count++;
      }
    }

    // Update the maximum profit
    if (ans < count * arr[i]) {
      price = arr[i];
      ans = count * arr[i];
    }
  }

  // Return the maximum possible
  // price
  return price;
}

// Driver code
int main()
{

  int arr[] = { 22, 87, 9, 50, 56, 43 };

  cout<<maximumProfit(arr,6);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the maximum profit
    // earned by selling an item among
    // N buyers
    public static int maximumProfit(int arr[])
    {
        // Stores the maximum profit
        int ans = Integer.MIN_VALUE;

        // Stores the price of the item
        int price = 0;

        // Sort the array
        Arrays.sort(arr);

        int N = arr.length;

        // Traverse the array
        for (int i = 0; i < N; i++) {

            // Count of buyers with
            // budget >= arr[i]
            int count = (N - i);

            // Update the maximum profit
            if (ans < count * arr[i]) {
                price = arr[i];
                ans = count * arr[i];
            }
        }

        // Return the maximum possible
        // price
        return price;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 22, 87, 9, 50, 56, 43 };

        System.out.print(
            maximumProfit(arr));
    }
}
```

## C#

```
// C# Program to implement
// the above approach
using System;
class GFG
{

  // Function to find the maximum profit
  // earned by selling an item among
  // N buyers
  public static int maximumProfit(int[] arr)
  {

    // Stores the maximum profit
    int ans = Int32.MinValue;

    // Stores the price of the item
    int price = 0;

    // Sort the array
    Array.Sort(arr);

    int N = arr.Length;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Count of buyers with
      // budget >= arr[i]
      int count = (N - i);

      // Update the maximum profit
      if (ans < count * arr[i]) {
        price = arr[i];
        ans = count * arr[i];
      }
    }

    // Return the maximum possible
    // price
    return price;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int[] arr = { 22, 87, 9, 50, 56, 43 };

    Console.WriteLine(
      maximumProfit(arr));
  }
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
import sys

# Function to find the maximum profit
# earned by selling an item among
# N buyers
def maximumProfit(arr, n):

    # Stores the maximum profit
    ans = -sys.maxsize - 1

    # Stores the price of the item
    price = 0

    # Traverse the array
    for i in range(n):

        # Count of buyers with
        # budget >= arr[i]
        count = 0

        for j in range(n):
            if (arr[i] <= arr[j]):

                # Increment count
                count += 1

        # Update the maximum profit
        if (ans < count * arr[i]):
            price = arr[i]
            ans = count * arr[i]

    # Return the maximum possible
    # price
    return price;

# Driver code
if __name__ == '__main__':
    arr =  [22, 87, 9, 50, 56, 43]
    print(maximumProfit(arr,6))

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Function to find the maximum profit
// earned by selling an item among
// N buyers
function maximumProfit(arr, n)
{
// Stores the maximum profit
var ans = -100000;;

// Stores the price of the item
var price = 0;

// Traverse the array
for (var i = 0; i < n; i++) {

    // Count of buyers with
    // budget >= arr[i]
    var count = 0;

    for (var j = 0; j < n; j++) {

    if (arr[i] <= arr[j]) {

        // Increment count
        count++;
    }
    }

    // Update the maximum profit
    if (ans < count * arr[i]) {
    price = arr[i];
    ans = count * arr[i];
    }
}

// Return the maximum possible
// price
return price;
}

 arr = [ 22, 87, 9, 50, 56, 43 ];

document.write(maximumProfit(arr,6));

</script>
```

**Output**

```
43
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(1)*