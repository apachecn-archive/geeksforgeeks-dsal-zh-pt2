# 在给定阵列中要进行的最小删除，使得每对总和为 2 的幂

> 原文:[https://www . geesforgeks . org/给定阵列中要执行的最小删除数，这样每对总和就是 2 的幂/](https://www.geeksforgeeks.org/minimum-deletions-to-be-done-in-given-array-such-that-every-pair-sum-is-a-power-of-2/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找到应该移除的元素的最小数量，这样对于每个剩余的元素**arr【I】**，就存在另一个元素**arr【j】，(I！=j)** 使得 **arr[i]** 和 **arr[j]** 的和是 **2** 的幂。如果在多次删除后，没有这样的配对，打印-1。

**示例:**

> **输入:** arr[] ={1，2，3，4，5，6}，N = 6
> **输出:** 1
> **解释:**
> 去掉 4 就足够了，因为对于剩余的元素存在一个元素，使得它们的和是 2 的幂:
> 
> 1.  对于 1，存在 3，因此(1+3=4)是 2 的幂。
> 2.  对于 2，存在 6，因此(2+6=8)是 2 的幂。
> 3.  对于 3，存在 1，因此(3+1=4)是 2 的幂。
> 4.  对于 5，存在 3，因此(5+3=8)是 2 的幂。
> 5.  对于 6，存在 2，因此(6+2=8)是 2 的幂。
> 
> **输入:** A={1，5，10，25，50}，N = 5
> T3】输出: -1

**方法:**想法是使用[逐位运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)来跟踪每个元素的频率。按照以下步骤解决问题:

*   将变量**和**初始化为 **0** ，以存储要移除的元素数量。
*   [计算**arr【】**中所有元素](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)的频率，并将其存储在一张[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中，上面写着 **mp** 。
*   从 **0 迭代到 N-1** ，对于每个当前索引 **i，**执行以下操作:
    *   初始化一个变量说[T1 标志](https://www.geeksforgeeks.org/use-of-flag-in-programming/)到 **0** 。
    *   从 **0** **迭代到 30** ，对于每个当前指标 **j** ，执行以下操作:
        *   如果**2<sup>j</sup>T3**arr【I】**之差等于**arr【I】、**且**arr【I】**的频率大于 **1** ，则递增**标志**并断开。**
        *   否则，如果 **2 <sup>j</sup>** 和**arr【I】**的差频大于 **0** ，则增加**标志**并断开。
    *   如果**标志**仍然是 **0** ，则增加 **ans，**作为当前需要移除的元素。
*   最后，完成上述步骤后，如果小于或等于 n，将删除元素的计数打印为在**和**中获得的值。否则打印-1。

下面是上述方法的一个实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// number of elements to be removed
// satisfying the conditions
int minimumDeletions(int arr[], int N)
{
    // Stores the final answer
    int ans = 0;

    // Map to store frequency
    // of each element
    map<int, int> mp;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
        mp[arr[i]]++;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        // Stores whether current
        // element needs to be
        // removed or not
        int flag = 0;

        // Iterate over the range
        // [0, 30]
        for (int j = 0; j < 31; j++) {

            // Stores 2^j
            int pw = (1 << j);

            // If 2^j -arr[i] equals
            // to the arr[i]
            if (pw - arr[i] == arr[i]) {

                // If count of arr[i]
                // is greater than 1
                if (mp[arr[i]] > 1) {
                    flag = 1;
                    break;
                }
            }
            // Else if count of 2^j-arr[i]
            // is greater than 0
            else if (mp[pw - arr[i]] > 0) {
                flag = 1;
                break;
            }
        }
        // If flag is 0
        if (flag == 0)
            ans++;
    }
    // Return ans
    return ans == N ? -1 : ans;
}
// Driver Code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minimumDeletions(arr, N) << endl;

    int arr1[] = { 1, 5, 10, 25, 50 };
    N = sizeof(arr) / sizeof(arr[0]);
    cout << minimumDeletions(arr1, N) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

    // Function to calculate the minimum
    // number of elements to be removed
    // satisfying the conditions
    static int minimumDeletions(int []arr, int N)
    {

        // Stores the final answer
        int ans = 0;

        // Map to store frequency
        // of each element
        Map<Integer, Integer> mp = new HashMap<Integer, Integer>();

        // Traverse the array arr[]
        for (int i = 0; i < N; i++){
            if(mp.containsKey(arr[i]))
              mp.put(arr[i],mp.get(arr[i]) + 1);
            else
              mp.put(arr[i],1);
        }

        // Traverse the array arr[]
        for (int i = 0; i < N; i++)
        {

            // Stores whether current
            // element needs to be
            // removed or not
            int flag = 0;

            // Iterate over the range
            // [0, 30]
            for (int j = 0; j < 31; j++) {

                // Stores 2^j
                int pw = (1 << j);

                // If 2^j -arr[i] equals
                // to the arr[i]
                if (pw - arr[i] == arr[i]) {

                    // If count of arr[i]
                    // is greater than 1
                    if (mp.containsKey(arr[i]) && mp.get(arr[i]) > 1) {
                        flag = 1;
                        break;
                    }
                }

                // Else if count of 2^j-arr[i]
                // is greater than 0
                else if (mp.containsKey(pw - arr[i]) && mp.get(pw - arr[i]) > 0) {
                    flag = 1;
                    break;
                }
            }

            // If flag is 0
            if (flag == 0)
                ans++;
        }

        // Return ans
        if(ans == N)
         return -1;
        else
         return ans;

    }

    // Driver Code
    public static void main(String[] args)
    {

        int arr[] = { 1, 2, 3, 4, 5, 6 };
        int N = arr.length;

        System.out.println(minimumDeletions(arr, N));

        int arr1[] = { 1, 5, 10, 25, 50 };
        N = arr1.length;
        System.out.print(minimumDeletions(arr1, N));

    }
}

// This code is contributed by ShubhamSingh10
```

## 蟒蛇 3

```
# Py program for the above approach

# Function to calculate the minimum
# number of elements to be removed
# satisfying the conditions
def minimumDeletions(arr, N):
    # Stores the final answer
    ans = 0

    # Map to store frequency
    # of each element
    mp = {}

    # Traverse the array arr[]
    for i in arr:
        mp[i] =  mp.get(i,0)+1

    # Traverse the array arr[]
    for i in range(N):
        # Stores whether current
        # element needs to be
        # removed or not
        flag = 0

        # Iterate over the range
        # [0, 30]
        for j in range(31):
            # Stores 2^j
            pw = (1 << j)

            # If 2^j -arr[i] equals
            # to the arr[i]
            if i >= len(arr):
                break

            if (pw - arr[i] == arr[i]):

                # If count of arr[i]
                # is greater than 1
                if (mp[arr[i]] > 1):
                    flag = 1
                    break
            # Else if count of 2^j-arr[i]
            # is greater than 0
            elif (((pw - arr[i]) in mp) and mp[pw - arr[i]] > 0):
                flag = 1
                break

        # If flag is 0
        if (flag == 0):
            ans += 1
    # Return ans
    return -1 if ans == N else ans

# Driver Code
if __name__ == '__main__':

    arr= [1, 2, 3, 4, 5, 6]
    N = len(arr)

    print (minimumDeletions(arr, N))

    arr1= [1, 5, 10, 25, 50]
    N = len(arr)
    print (minimumDeletions(arr1, N))

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate the minimum
// number of elements to be removed
// satisfying the conditions
static int minimumDeletions(int []arr, int N)
{

    // Stores the final answer
    int ans = 0;

    // Map to store frequency
    // of each element
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Traverse the array arr[]
    for (int i = 0; i < N; i++){
        if(mp.ContainsKey(arr[i]))
          mp[arr[i]] += 1;
        else
          mp.Add(arr[i],1);
    }

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // Stores whether current
        // element needs to be
        // removed or not
        int flag = 0;

        // Iterate over the range
        // [0, 30]
        for (int j = 0; j < 31; j++) {

            // Stores 2^j
            int pw = (1 << j);

            // If 2^j -arr[i] equals
            // to the arr[i]
            if (pw - arr[i] == arr[i]) {

                // If count of arr[i]
                // is greater than 1
                if (mp.ContainsKey(arr[i]) && mp[arr[i]] > 1) {
                    flag = 1;
                    break;
                }
            }

            // Else if count of 2^j-arr[i]
            // is greater than 0
            else if (mp.ContainsKey(pw - arr[i]) && mp[pw - arr[i]] > 0) {
                flag = 1;
                break;
            }
        }

        // If flag is 0
        if (flag == 0)
            ans++;
    }

    // Return ans
    if(ans == N)
     return -1;
    else
     return ans;

}

// Driver Code
public static void Main()
{

    int []arr = { 1, 2, 3, 4, 5, 6 };
    int N = arr.Length;

    Console.WriteLine(minimumDeletions(arr, N));

    int []arr1 = { 1, 5, 10, 25, 50 };
    N = arr1.Length;
    Console.Write(minimumDeletions(arr1, N));

}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the minimum
// number of elements to be removed
// satisfying the conditions
function minimumDeletions(arr, N) {
    // Stores the final answer
    let ans = 0;

    // Map to store frequency
    // of each element
    let mp = new Map();

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {
        if (mp.has(arr[i])) {
            mp.set(arr[i], mp.get(arr[i]) + 1)
        } else {
            mp.set(arr[i], 1)
        }
    }

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {
        // Stores whether current
        // element needs to be
        // removed or not
        let flag = 0;

        // Iterate over the range
        // [0, 30]
        for (let j = 0; j < 31; j++) {

            // Stores 2^j
            let pw = (1 << j);

            // If 2^j -arr[i] equals
            // to the arr[i]
            if (pw - arr[i] == arr[i]) {

                // If count of arr[i]
                // is greater than 1
                if (mp.get(arr[i]) > 1) {
                    flag = 1;
                    break;
                }
            }
            // Else if count of 2^j-arr[i]
            // is greater than 0
            else if (mp.get(pw - arr[i]) > 0) {
                flag = 1;
                break;
            }
        }
        // If flag is 0
        if (flag == 0)
            ans++;
    }
    // Return ans
    return ans == N ? -1 : ans;
}
// Driver Code

let arr = [1, 2, 3, 4, 5, 6];
let N = arr.length;

document.write(minimumDeletions(arr, N) + "<br>");

let arr1 = [1, 5, 10, 25, 50];
N = arr.length;
document.write(minimumDeletions(arr1, N) + "<br>");

</script>
```

**Output:** 

```
1
-1
```

***时间复杂度:** O(30*N)*
***辅助空间:** O(1)*