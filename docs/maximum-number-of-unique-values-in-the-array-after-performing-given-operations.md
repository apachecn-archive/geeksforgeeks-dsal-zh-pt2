# 执行给定操作后数组中唯一值的最大数量

> 原文:[https://www . geesforgeks . org/执行给定操作后数组中唯一值的最大数量/](https://www.geeksforgeeks.org/maximum-number-of-unique-values-in-the-array-after-performing-given-operations/)

给定一个大小为 **N** 的数组 **arr[]** ，数组 **arr[]** 中的每个元素都在**【1，N】**的范围内，数组可能包含重复的元素。任务是找到可以获得的唯一值的最大数量，使得任何索引 I 处的值可以是:

*   增加 1。
*   减少 1。
*   保持原样。

**注意:**对每个索引只能执行一次操作，并且必须对数组 arr[]中的所有索引执行。
**例:**

> **输入:** arr[] = {1，2，4，4}
> **输出:** 4
> **解释:**
> 一种方法是对索引执行以下操作:
> 1:保持第一个索引(1)的值不变。
> 2:保持第二个索引(2)的值不变。
> 3:保留第三个索引(4)的值不变。
> 4:将第四个索引(4)的值增加 1。
> 则数组变为{1，2，4，5}，有 4 个唯一值。
> **输入:** arr[]={3，3，3，3}
> **输出:** 3
> **解释:**
> 一种方法是对索引执行以下操作:
> 1:保持第一个索引(3)的值不变。
> 2:将第二个索引(3)处的值减 1。
> 3:保留第三个索引(3)的值不变。
> 4:将第四个索引(3)处的值增加 1。
> 则数组变为{3，2，3，4}，有 3 个唯一值。

**进场:**

*   对于索引为 **i** 的数组中的任意元素 **X** ，我们通过考虑以下因素来决定对其执行什么操作:
    1.  如果数组中不存在值(**X–1**)并且在不同的索引处数组中存在一个或多个其他 X，我们将**的值 **X** 减 1。**
    2.  如果值 **X** 在数组中只出现一次，我们**不改变**值 **X** 。
    3.  如果数组中不存在值( **X + 1** )并且在不同的索引处数组中存在一个或多个其他 X，我们将**的值 **X** 增加 1。**
*   通过对每个元素进行上述决策，我们可以确定我们得到的唯一元素的最终计数是最大的。
*   但是，要对每个索引执行上述步骤，计算元素 X 的出现次数并持续更新数组 arr[]，所用时间将是二次的，这对于大规模数组是不可行的。
*   降低时间复杂度的一个替代方法是首先[对数组](https://www.geeksforgeeks.org/sorting-algorithms/)进行排序。通过排序，数组中的所有元素被分组，所有重复的值聚集在一起。
*   在对数组进行排序后，由于数字的范围已经给出并且是固定的，因此可以使用[散列图](https://www.geeksforgeeks.org/hashing-data-structure/)，其中散列的关键字是范围**【1，N】**中的数字，并且每个关键字的值是布尔值，用于确定该关键字是否存在于数组中。
*   在这个问题中，由于索引本身是散列的关键字，所以使用大小为( **N + 2** )的数组 **freq[]** 来实现散列。

以下是上述方法的实现:

## C++

```
// C++ program to find the maximum number of
// unique values in the array

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number of
// unique values in the vector
int uniqueNumbers(vector<int> arr, int n)
{
    // Sorting the given vector
    sort(arr.begin(),arr.end());

    // This array will store the frequency
    // of each number in the array
    // after performing the given operation
      // initialise the array with 0
    vector<int> freq(n+2,0) ;

    // Loop to apply operation on
    // each element of the array
    for (int x = 0; x < n; x++) {

        // Incrementing the value at index x
        // if the value  arr[x] - 1 is
        // not present in the array
        if (freq[arr[x] - 1] == 0) {
            freq[arr[x] - 1]++;
        }

        // If arr[x] itself is not present, then it
        // is left as it is
        else if (freq[arr[x]] == 0) {
            freq[arr[x]]++;
        }

        // If both arr[x] - 1 and arr[x] are present
        // then the value is incremented by 1
        else {
            freq[arr[x] + 1]++;
        }
    }

    // Variable to store the number of unique values
    int unique = 0;

    // Finding the unique values
    for (int x = 0; x <= n + 1; x++) {
        if (freq[x]) {
            unique++;
        }
    }

    // Returning the number of unique values
    return unique;
}

// Driver Code
int main()
{
    vector<int> arr= { 3, 3, 3, 3 };

    // Size of the vector
    int n = arr.size();

    int ans = uniqueNumbers(arr, n);
    cout << ans;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum number of
// unique values in the array
import java.util.*;

class GFG {

    // Function to find the maximum number of
    // unique values in the array
    static int uniqueNumbers(int arr[], int n)
    {
        // Sorting the given array
        Arrays.sort(arr);

        // This array will store the frequency
        // of each number in the array
        // after performing the given operation
        int freq[] = new int[n + 2];

        // Initialising the array with all zeroes
        for(int i = 0; i < n + 2; i++)
            freq[i] = 0;

        // Loop to apply operation on
        // each element of the array
        for (int x = 0; x < n; x++) {

            // Incrementing the value at index x
            // if the value arr[x] - 1 is
            // not present in the array
            if (freq[arr[x] - 1] == 0) {
                freq[arr[x] - 1]++;
            }

            // If arr[x] itself is not present, then it
            // is left as it is
            else if (freq[arr[x]] == 0) {
                freq[arr[x]]++;
            }

            // If both arr[x] - 1 and arr[x] are present
            // then the value is incremented by 1
            else {
                freq[arr[x] + 1]++;
            }
        }

        // Variable to store the number of unique values
        int unique = 0;

        // Finding the unique values
        for (int x = 0; x <= n + 1; x++) {
            if (freq[x] != 0) {
                unique++;
            }
        }

        // Returning the number of unique values
        return unique;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int []arr = { 3, 3, 3, 3 };

        // Size of the array
        int n = 4;

        int ans = uniqueNumbers(arr, n);
        System.out.println(ans);
    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python program to find the maximum number of
# unique values in the array

# Function to find the maximum number of
# unique values in the array
def uniqueNumbers(arr, n):

    # Sorting the given array
    arr.sort()

    # This array will store the frequency
    # of each number in the array
    # after performing the given operation
    freq =[0]*(n + 2)

    # Loop to apply the operation on
    # each element of the array
    for val in arr:

        # Incrementing the value at index x
        # if the value  arr[x] - 1 is
        # not present in the array
        if(freq[val-1]== 0):
            freq[val-1]+= 1

        # If arr[x] itself is not present, then it
        # is left as it is
        elif(freq[val]== 0):
            freq[val]+= 1

        # If both arr[x] - 1 and arr[x] are present
        # then the value is incremented by 1
        else:
            freq[val + 1]+= 1

    # Variable to store the
    # number of unique values
    unique = 0

    # Finding the number of unique values
    for val in freq:
        if(val>0):
            unique+= 1

    return unique

# Driver code
if __name__ == "__main__":
    arr =[3, 3, 3, 3]
    n = 4
    print(uniqueNumbers(arr, n))
```

## C#

```
// C# program to find the maximum number of
// unique values in the array
using System;

class GFG {

    // Function to find the maximum number of
    // unique values in the array
    static int uniqueNumbers(int []arr, int n)
    {
        // Sorting the given array
        Array.Sort(arr);

        // This array will store the frequency
        // of each number in the array
        // after performing the given operation
        int []freq = new int[n + 2];

        // Initialising the array with all zeroes
        for(int i = 0; i < n + 2; i++)
            freq[i] = 0;

        // Loop to apply operation on
        // each element of the array
        for (int x = 0; x < n; x++) {

            // Incrementing the value at index x
            // if the value arr[x] - 1 is
            // not present in the array
            if (freq[arr[x] - 1] == 0) {
                freq[arr[x] - 1]++;
            }

            // If arr[x] itself is not present, then it
            // is left as it is
            else if (freq[arr[x]] == 0) {
                freq[arr[x]]++;
            }

            // If both arr[x] - 1 and arr[x] are present
            // then the value is incremented by 1
            else {
                freq[arr[x] + 1]++;
            }
        }

        // Variable to store the number of unique values
        int unique = 0;

        // Finding the unique values
        for (int x = 0; x <= n + 1; x++) {
            if (freq[x] != 0) {
                unique++;
            }
        }

        // Returning the number of unique values
        return unique;
    }

    // Driver Code
    public static void Main (string[] args)
    {
        int []arr = { 3, 3, 3, 3 };

        // Size of the array
        int n = 4;

        int ans = uniqueNumbers(arr, n);
        Console.WriteLine(ans);
    }
}

// This code is contributed by Yash_R
```

## java 描述语言

```
<script>
// javascript program to find the maximum number of
// unique values in the array

    // Function to find the maximum number of
    // unique values in the array
    function uniqueNumbers(arr , n) {
        // Sorting the given array
        arr.sort((a,b)=>a-b);

        // This array will store the frequency
        // of each number in the array
        // after performing the given operation
        var freq = Array(n + 2).fill(0);

        // Initialising the array with all zeroes
        for (i = 0; i < n + 2; i++)
            freq[i] = 0;

        // Loop to apply operation on
        // each element of the array
        for (x = 0; x < n; x++) {

            // Incrementing the value at index x
            // if the value arr[x] - 1 is
            // not present in the array
            if (freq[arr[x] - 1] == 0) {
                freq[arr[x] - 1]++;
            }

            // If arr[x] itself is not present, then it
            // is left as it is
            else if (freq[arr[x]] == 0) {
                freq[arr[x]]++;
            }

            // If both arr[x] - 1 and arr[x] are present
            // then the value is incremented by 1
            else {
                freq[arr[x] + 1]++;
            }
        }

        // Variable to store the number of unique values
        var unique = 0;

        // Finding the unique values
        for (x = 0; x <= n + 1; x++) {
            if (freq[x] != 0) {
                unique++;
            }
        }

        // Returning the number of unique values
        return unique;
    }

    // Driver Code

        var arr = [ 3, 3, 3, 3 ];

        // Size of the array
        var n = 4;

        var ans = uniqueNumbers(arr, n);
        document.write(ans);

// This code contributed by Rajput-Ji
</script>
```

**Output:** 

```
3
```

**时间复杂度分析:**

*   给定数组的排序时间为 **O(N * log(N))** ，其中 N 是数组的大小。
*   在排序后的数组上运行一个循环来执行操作所花费的时间是 **O(N)** 。
*   在散列上运行循环以计算唯一值所花费的时间是 **O(N)** 。
*   因此，整体时间复杂度为 **O(N * log(N)) + O(N) + O(N)** 。由于 N * log(N)更大，上述方法的最终时间复杂度为 **O(N * log(N))** 。

**辅助空间:O(N)**

*   **freq** 数组占用的额外空间为 0(N)。因此辅助空间为 O(N)。