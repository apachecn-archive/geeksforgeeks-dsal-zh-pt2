# 通过增加和减少对来最小化移动以使数组元素相等

> 原文:[https://www . geeksforgeeks . org/最小化-移动-生成-数组-元素-等乘-递增-递减-对/](https://www.geeksforgeeks.org/minimize-moves-to-make-array-elements-equal-by-incrementing-and-decrementing-pairs/)

给定一个大小为 **N、**的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，任务是通过选择任意两个不同的索引来打印使所有数组元素相等所需的**最小**移动次数，然后在每个移动中将第一个选定索引处的元素递增，并将另一个选定索引处的元素递减 **1** 。如果不可能使所有数组元素相等，则打印“ **-1** ”。

**示例**:

> **输入:** arr[] = {5，4，1，10}
> **输出:** 5
> **解释:**
> 执行操作的一种可能方式是:
> **操作 1:** 选择索引 1 和 3，然后将 arr[1]递增 1，将 arr[3]递减 1。此后，数组修改为{5，5，1，9}。
> **操作 2:** 选择索引 2 和 3，然后将 arr[2]增加 1，将 arr[3]减少 1。此后，数组修改为{5，5，2，8}。
> **操作 3:** 选择索引 2 和 3，然后将 arr[2]增加 1，将 arr[3]减少 1。此后，数组修改为{5，5，3，7}。
> **操作 4:** 选择索引 2 和 3，然后将 arr[2]增加 1，将 arr[3]减少 1。此后，数组修改为{5，5，4，6}。
> **操作 5:** 选择索引 2 和 3，然后将 arr[2]增加 1，将 arr[3]减少 1。此后，数组修改为{5，5，5，5}。
> 因此，需要的移动总数是 5。此外，这是所需的最小可能的移动。
> 
> **输入:** arr[] = {1，4}
> **输出:** -1

**方法:**给定的问题可以基于以下观察来解决:

> *   It can be observed that the sum of [array](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/) remains unchanged in one movement. Therefore, if the sum of arrays cannot be evenly divided by **n** , it is impossible to make all array elements equal.
> *   Otherwise, each array element will be equal to the sum of arrays divided by **n** .
> *   Therefore, the idea is to use [double pointer technology](https://www.geeksforgeeks.org/two-pointers-technique/) to find the minimum number of moves required to make all array elements equal to **and/n** .

按照以下步骤解决问题:

*   初始化一个变量，将**和**设为 **0** ，以存储所需移动的计数。
*   [求数组的和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)并存储在一个变量中，比如**和**。
*   现在如果**之和**不能被 **N** 整除，那么打印“ **-1** ”。否则，将**和**更新为**和=和/否**
*   [按升序对数组进行排序。](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)
*   初始化变量，说 **i** 为 **0** 和 **j** 为**N–1**来迭代数组。
*   重复直到 **i** 小于 j，并执行以下步骤:
    *   **如果**将 **arr[i]** 增加到 **sum** 小于将 **arr[j]** 减少到 **sum** 那么将**sum–arr[I]**加到 **ans** 上，然后更新 **arr[i]** 和 **arr[j]** 然后将 **i** 增加 **1**
    *   否则，将**arr[j]–sum**加到 **ans** 上，更新 **arr[i]** 和 **arr[j]** ，然后将 **j** 减 **1。**
*   最后，完成上述步骤后，打印存储在**和**中的值。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach
#include <algorithm>
#include <iostream>
using namespace std;

// Function to find the minimum
// operations to make the array
// elements equal
int find(int arr[], int N)
{
  // Stores the sum of the
  // array
  int Sum = 0;
  for (int i = 0; i < N; i++) {
    Sum += arr[i];
  }
  if (Sum % N) {
    return -1;
  }

  // update sum
  Sum /= N;

  // sort array
  sort(arr, arr + N);

  // Store the minimum
  // needed moves
  int ans = 0;
  int i = 0, j = N - 1;

  // Iterate until i
  // is less than j
  while (i < j) {
    if (Sum - arr[i] < arr[j] - Sum) {

      // Increment ans by
      // Sum-arr[i]
      ans += (Sum - arr[i]);

      // update
      arr[i] += (Sum - arr[i]);
      arr[j] -= (Sum - arr[i]);

      // Increment i by 1
      i++;
    }
    else {

      // Increment ans by
      //arr[j]-Sum
      ans += (arr[j] - Sum);

      // Update
      arr[i] += (arr[j] - Sum);
      arr[j] -= (arr[j] - Sum);

      // Decrement j by 1
      j--;
    }
  }

  // Return the value in ans
  return ans;
}

// Driver code
int main()
{

  // Given input
  int arr[] = { 5, 4, 1, 10 };
  int N = sizeof(arr) / sizeof(int);

  // Function call
  cout << find(arr, N);
  return 0;
}

// This code is contributed by Parth Manchanda
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;

// Java Program for the above approach

class GFG {

    // Function to find the minimum
    // operations to make the array
    // elements equal
    public static int find(int arr[], int N)
    {

        // Stores the sum of the
        // array
        int Sum = 0;
        for (int i = 0; i < N; i++) {
            Sum += arr[i];
        }
        if (Sum % N > 0) {
            return -1;
        }

        // update sum
        Sum /= N;

        // sort array
        Arrays.sort(arr);

        // Store the minimum
        // needed moves
        int ans = 0;
        int i = 0, j = N - 1;

        // Iterate until i
        // is less than j
        while (i < j) {
            if (Sum - arr[i] < arr[j] - Sum) {

                // Increment ans by
                // Sum-arr[i]
                ans += (Sum - arr[i]);

                // update
                arr[i] += (Sum - arr[i]);
                arr[j] -= (Sum - arr[i]);

                // Increment i by 1
                i++;
            } else {

                // Increment ans by
                // arr[j]-Sum
                ans += (arr[j] - Sum);

                // Update
                arr[i] += (arr[j] - Sum);
                arr[j] -= (arr[j] - Sum);

                // Decrement j by 1
                j--;
            }
        }

        // Return the value in ans
        return ans;
    }

    // Driver code
    public static void main(String args[]) {

        // Given input
        int arr[] = { 5, 4, 1, 10 };
        int N = arr.length;

        // Function call
        System.out.println(find(arr, N));

    }
}

// This code is contributed by gfgking
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum
# operations to make the array
# elements equal
def find(arr, N):

    # Stores the sum of the
    # array
    Sum = sum(arr)

    # If sum is not divisible
    # by N
    if Sum % N:
        return -1
    else:

       # Update sum
        Sum //= N

        # Sort the array
        arr.sort()

        # Store the minimum
        # needed moves
        ans = 0

        i = 0
        j = N-1

        # Iterate until i
        # is less than j
        while i < j:

            # If the Sum-arr[i]
            # is less than the
            # arr[j]-sum
            if Sum-arr[i] < arr[j]-Sum:

                # Increment ans by
                # Sum-arr[i]
                ans += Sum-arr[i]

                # Update
                arr[i] += Sum-arr[i]
                arr[j] -= Sum-arr[i]

                # Increment i by 1
                i += 1

            # Otherwise,
            else:

                # Increment ans by
                # arr[j]-Sum
                ans += arr[j]-Sum

                # Update
                arr[i] += arr[j]-Sum
                arr[j] -= arr[j]-Sum

                # Decrement j by 1
                j -= 1

        # Return the value in ans
        return ans

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [5, 4, 1, 10]
    N = len(arr)

    # Function Call
    print(find(arr, N))
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum
// operations to make the array
// elements equal
public static int find(int[] arr, int N)
{

    // Stores the sum of the
    // array
    int Sum = 0;
    int i = 0;

    for(i = 0; i < N; i++)
    {
        Sum += arr[i];
    }
    if (Sum % N > 0)
    {
        return -1;
    }

    // update sum
    Sum /= N;

    // sort array
    Array.Sort(arr);

    // Store the minimum
    // needed moves
    int ans = 0;
    i = 0;
    int j = N - 1;

    // Iterate until i
    // is less than j
    while (i < j)
    {
        if (Sum - arr[i] < arr[j] - Sum)
        {

            // Increment ans by
            // Sum-arr[i]
            ans += (Sum - arr[i]);

            // update
            arr[i] += (Sum - arr[i]);
            arr[j] -= (Sum - arr[i]);

            // Increment i by 1
            i++;
        }
        else
        {

            // Increment ans by
            // arr[j]-Sum
            ans += (arr[j] - Sum);

            // Update
            arr[i] += (arr[j] - Sum);
            arr[j] -= (arr[j] - Sum);

            // Decrement j by 1
            j--;
        }
    }

    // Return the value in ans
    return ans;
}

// Driver code
static public void Main()
{

    // Given input
    int[] arr = { 5, 4, 1, 10 };
    int N = arr.Length;

    // Function call
    Console.WriteLine(find(arr, N));
}
}

// This code is contributed by target_2
```

## java 描述语言

```
<script>

        // JavaScript Program for the above approach

        // Function to find the minimum
        // operations to make the array
        // elements equal
        function find(arr, N) {

            // Stores the sum of the
            // array
            let Sum = 0;

            for (i = 0; i < arr.length; i++) {
                Sum = Sum + arr[i];
            }

            // If sum is not divisible
            // by N
            if (Sum % N)
                return -1;
            else {

                // Update sum
                Sum = Math.floor(Sum / N);

                // Sort the array
                arr.sort(function (a, b) { return a - b });

                // Store the minimum
                // needed moves
                ans = 0

                i = 0
                j = N - 1

                // Iterate until i
                // is less than j
                while (i < j) {

                    // If the Sum-arr[i]
                    // is less than the
                    // arr[j]-sum
                    if (Sum - arr[i] < arr[j] - Sum) {

                        // Increment ans by
                        // Sum-arr[i]
                        ans += Sum - arr[i]

                        // Update
                        arr[i] += Sum - arr[i]
                        arr[j] -= Sum - arr[i]

                        // Increment i by 1
                        i += 1
                    }
                    // Otherwise,
                    else {

                        // Increment ans by
                        // arr[j]-Sum
                        ans += arr[j] - Sum

                        // Update
                        arr[i] += arr[j] - Sum
                        arr[j] -= arr[j] - Sum

                        // Decrement j by 1
                        j -= 1
                    }

                }
            }
            // Return the value in ans
            return ans;

        }

        // Driver Code

        // Given Input
        let arr = [5, 4, 1, 10];
        let N = arr.length;

        // Function Call
        document.write(find(arr, N));

    // This code is contributed by Potta Lokesh

</script>
```

**Output**

```
5
```

***时间复杂度:*** O(N*log(N))
***辅助空间:*** O(1)