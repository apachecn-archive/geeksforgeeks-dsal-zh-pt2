# 给定偶数列中相邻对的计数

> 原文:[https://www . geesforgeks . org/给定偶和数组中相邻对的计数/](https://www.geeksforgeeks.org/count-of-adjacent-pairs-in-given-array-with-even-sum/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出相邻元素对的计数，这些元素的和是偶数，其中每个元素最多只能属于一对。

**示例:**

> **输入:** arr[] = {1，12，1，3，5}
> **输出:** 1
> **说明:**可以用 arr[3]和 arr[4]组成 1 对。
> 
> **输入:** arr[] = {1，2，3，4，5，6，8，9 }
> T3】输出: 0

**方法:**给定的问题可以用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。可以观察到，所需的对可以由仅具有相同奇偶性的元素形成，即(奇数、奇数)或(偶数、偶数)。同样，从 **X** 连续奇数或偶数可以形成的对的数量是地板 **(X / 2)** 。因此遍历给定的数组，计算所有可能的连续整数集合，并将每个集合的 **(X / 2)** 加到答案中。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {
    // Function to find maximum count of
    // pairs of adjacent elements with even
    // sum in the given array
    public static int findMaximumPairs(int[] arr)
    {

        // Total number of pairs is initially 0
        int totalPairs = 0;
        for (int i = 0; i < arr.length - 1; 
             i++) {

            // If current pair is even-even
            // or odd-odd
            if ((arr[i] + arr[i + 1]) % 2 == 0) {
                totalPairs++;
                i++;
            }
        }

        // Return Answer
        return totalPairs;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 12, 1, 3, 5 };
        System.out.println(
            findMaximumPairs(arr));
    }
}
```

**Output**

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)