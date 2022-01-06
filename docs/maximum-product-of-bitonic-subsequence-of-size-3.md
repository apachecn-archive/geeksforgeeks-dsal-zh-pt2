# 大小为 3 的双离子子序列的最大乘积

> 原文:[https://www . geesforgeks . org/最大双音素子序列大小为 3/](https://www.geeksforgeeks.org/maximum-product-of-bitonic-subsequence-of-size-3/)

给定一个大小为 **N** 的正整数数组 **arr[]** ，任务是找到大小为 3 的双调和子序列的最大乘积。
**双音素子序列:**元素先递增后递减的子序列。子序列中的元素按照这个顺序排列，i < j < k，其中 I，j，k 是给定数组的索引。
**注意:**如果没有找到这样的元素，那么打印-1。

**示例:**

> **输入:** arr[] = {1，8，3，7，5，6，7}
> **输出:** 126
> **解释:**
> 大小为 3 的双音素子序列是
> {1，8，3}，{1，8，7}，{1，8，5}，{1，8，6}，{1，7，6}，{3，7，6}，{1，7，5}，{3，7，5}
> 因此，双音素子序列的最大乘积是 3*7*6 = 126
> 
> **输入:** arr[] = {1，8，3，7}
> **输出:** 56
> **解释:**
> 大小为 3 的双音素子序列为
> {1，8，3}，{1，8，7}，{1，7，3}。
> 因此双音素子序列的最大乘积是 1*8*7 = 56

**天真方法:**一个简单的解决方法是找到所有大小为 3 的双调和子序列的乘积，并取其中的最大值。

**算法:**

*   将**和**初始化为-1，这样如果没有这样的子序列，那么输出将为-1。
*   使用三个嵌套循环迭代数组，循环变量为 I、j 和 k，用于选择数组的三个元素。
*   检查 arr[j] > arr[i]和 arr[j] > arr[k]，然后用 **ans** 和 **arr[i] * arr[j] * arr[k]** 之间的最大值更新 **ans** 。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum product of the bitonic
// subsequence of size 3

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// product of bitonic subsequence
// of size 3
int maxProduct(int arr[], int n){

    // Initialize ans to -1 if no such
    // subsequence exist in the array
    int ans = -1;

    // Nested loops to choose the three
    // elements of the array
    for (int i = 0; i < n - 2; i++) {
        for (int j = i + 1; j < n - 1; j++) {
            for (int k = j + 1; k < n; k++) {

                // Condition to check if
                // they form a bitonic subsequence
                if (arr[i] < arr[j] &&
                      arr[j] > arr[k])
                    ans = max(
                       ans, arr[i] * arr[j] * arr[k]
                       );
            }
        }
    }
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 8, 3, 7 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << maxProduct(arr, n) << endl;   
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum product of the bitonic
// subsequence of size 3
import java.util.*;

class GFG{

// Function to find the maximum
// product of bitonic subsequence
// of size 3
static int maxProduct(int arr[], int n){

    // Initialize ans to -1 if no such
    // subsequence exist in the array
    int ans = -1;

    // Nested loops to choose the three
    // elements of the array
    for (int i = 0; i < n - 2; i++) {
        for (int j = i + 1; j < n - 1; j++) {
            for (int k = j + 1; k < n; k++) {

                // Condition to check if
                // they form a bitonic subsequence
                if (arr[i] < arr[j] &&
                      arr[j] > arr[k])
                    ans = Math.max(
                       ans, arr[i] * arr[j] * arr[k]
                       );
            }
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 8, 3, 7 };

    int n = arr.length;

    // Function call
    System.out.print(maxProduct(arr, n) +"\n");   
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum product of the bitonic
# subsequence of size 3

# Function to find the maximum
# product of bitonic subsequence
# of size 3
def maxProduct(arr, n):

    # Initialize ans to -1 if no such
    # subsequence exist in the array
    ans = -1

    # Nested loops to choose the three
    # elements of the array
    for i in range(n - 2):
        for j in range(i + 1, n - 1):
            for k in range(j + 1, n):

                # Condition to check if
                # they form a bitonic subsequence
                if (arr[i] < arr[j] and arr[j] > arr[k]):
                    ans = max(ans, arr[i] * arr[j] * arr[k])

    return ans

# Driver Code
if __name__ == '__main__':
    arr= [ 1, 8, 3, 7]

    n = len(arr)

    # Function call
    print(maxProduct(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// maximum product of the bitonic
// subsequence of size 3
using System;

class GFG {

     // Function to find the maximum
     // product of bitonic subsequence
    // of size 3
    static int maxProduct(int[] arr, int n)
    {
        // Initialize ans to -1 if no such
        // subsequence exist in the array
        int ans = -1;

        // Nested loops to choose the three
        // elements of the array
        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {

                    // Condition to check if
                    // they form a bitonic subsequence
                    if (arr[i] < arr[j] &&
                          arr[j] > arr[k])
                        ans = Math.Max(ans, arr[i] * arr[j] * arr[k]
                           );
                }
            }
        }
        return ans;
    }

    // Driver code
    static void Main()
    {
        int[] arr = new int[] { 1, 8, 3, 7 };
        int n = arr.Length;

        // Function call to find product
        Console.Write(maxProduct(arr, n));
    }
}

// This code is contributed by shubhamsingh
```

## java 描述语言

```
<script>
// Java  script implementation to find the
// maximum product of the bitonic
// subsequence of size 3

// Function to find the maximum
// product of bitonic subsequence
// of size 3
function maxProduct(arr,n){

    // Initialize ans to -1 if no such
    // subsequence exist in the array
    let ans = -1;

    // Nested loops to choose the three
    // elements of the array
    for (let i = 0; i < n - 2; i++) {
        for (let j = i + 1; j < n - 1; j++) {
            for (let k = j + 1; k < n; k++) {

                // Condition to check if
                // they form a bitonic subsequence
                if (arr[i] < arr[j] &&
                    arr[j] > arr[k])
                    ans = Math.max(
                    ans, arr[i] * arr[j] * arr[k]
                    );
            }
        }
    }
    return ans;
}

// Driver Code

    let arr = [ 1, 8, 3, 7 ];

    let n = arr.length;

    // Function call
    document.write(maxProduct(arr, n) +"<br>");   

// This code is contributed by Bobby
</script>
```

**Output:** 

```
56
```

**性能分析:**

*   **时间复杂度:**和上面的方法一样，有三个嵌套循环来寻找大小为 3 的双音素子序列的最大乘积，因此时间复杂度为 **O(N <sup>3</sup> )** 。
*   **辅助空间:**和上面的方法一样，没有使用额外的空间，因此辅助空间将是 **O(1)** 。

**高效的方法:**想法是在每个指数的左侧和右侧找到最大值，该值小于当前指数中存在的元素，要做到这一点，使用[自平衡 BST](https://www.geeksforgeeks.org/tag/self-balancing-bst/) 然后为每个元素找到可以形成的最大乘积，并从这些乘积中获取最大值。
自平衡 BST 实现为 C++中的[集和 Java 中的](https://www.geeksforgeeks.org/set-in-cpp-stl/)[树集](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)。

**算法:**

*   声明一个自平衡 BST(说 **s** )。
*   声明两个新数组**左[]** 和**右[]** 来存储左[i]中该元素左边 arr[i]的下界和右[i]中该元素右边 arr[i]的下界。
*   运行一个从 0 到长度–1 的循环，以找到 arr[i]在该元素左边的下限，并将其存储在左边的[i]中。
*   运行一个从长度-1 到 0 的循环，在该元素的右边找到 arr[i]的下限，并将其存储在右边的[i]中。
*   运行一个从 0 到 length–1 的循环，以找到可以使用该元素形成的双调和子序列，从而使用 left[]和 right[]数组获得最大乘积。也就是说，对于每个元素，可以形成的最大乘积双调和子序列是**左[i] *右[i] * arr[i]** 。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum product of the bitonic
// subsequence of size 3

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// product of bitonic subsequence
// of size 3
int maxProduct(int arr[], int n){

    // Self Balancing BST
    set<int> s;
    set<int>::iterator it;

    // Left array to store the
    // maximum smallest value for
    // every element in left of it
    int Left[n];

    // Right array to store the
    // maximum smallest value for
    // every element in right of it
    int Right[n];

    // Loop to find the maximum
    // smallest element in left of
    // every element in array
    for (int i = 0; i < n; i++) {
        s.insert(arr[i]);
        it = s.lower_bound(arr[i]);

        // Condition to check if there
        // is a maximum smallest element
        if (it != s.begin()) {
            it--;
            Left[i] = *it;
        }
        else {
            Left[i] = -1;
        }
    }
    // Clear Set
    s.clear();

    // Loop to find the maximum
    // smallest element in right of
    // every element in array
    for (int i = n - 1; i >= 0; i--) {
        s.insert(arr[i]);
        it = s.lower_bound(arr[i]);

        // Condition to check if there
        // is such element exists
        if (it != s.begin()) {
            it--;
            Right[i] = *it;
        }

        // If no such element exists.
        else {
            Right[i] = -1;
        }
    }
    int ans = -1;

    // Loop to find the maximum product
    // bitonic subsequence of size 3
    for (int i = 0; i < n; i++) {
        if (Left[i] > 0 and Right[i] > 0)
            ans = max(ans, arr[i] * Left[i] * Right[i]);
    }

    if (ans < 0) {
        return -1;
    }
    else {
        return ans;
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 8, 3, 7, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << maxProduct(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum product of the bitonic
// subsequence of size 3
import java.util.*;
import java.lang.System;

class GFG{

 public static int maxProduct(int arr[],int n)
 {
    // Self Balancing BST
    TreeSet<Integer> ts = new TreeSet<Integer>();

    // Left array to store the
    // maximum smallest value for
    // every element in left of it
    int Left[] = new int[n];

    // Right array to store the
    // maximum smallest value for
    // every element in right of it
    int Right[] = new int[n];

    // Loop to find the maximum
    // smallest element in left of
    // every element in array
    for(int i = 0; i < n; i++)
    {
        ts.add(arr[i]);

        if(ts.lower(arr[i]) == null)
            Left[i] = -1;
        else
            Left[i] = ts.lower(arr[i]);
    }

    ts.clear();

    // Loop to find the maximum
    // smallest element in right of
    // every element in array
    for (int i = n-1; i >= 0; i--)
    {
        ts.add(arr[i]);

        if(ts.lower(arr[i]) == null)
            Right[i] = -1;
        else
            Right[i] = ts.lower(arr[i]);
    }

    // Loop to find the maximum product
    // bitonic subsequence of size 3
    int ans = 0;

    for(int i = 0; i < n; i++)
    {
        //Condition to check whether a sequence is bitonic or not
        if(Left[i] != -1 && Right[i] != -1)
            ans = Math.max(ans, Left[i] * arr[i] * Right[i]);
    }

    return ans;
 }

 // Driver Code
 public static void main(String args[])
{
    int arr[] = {1, 8, 3, 7, 5, 6, 7 };

    int n = arr.length;

    int maximum_product = maxProduct(arr,n);

    System.out.println(maximum_product);
}
}

// This code is contributed by Siddhi.
```

**Output:** 

```
126
```

**性能分析:**

*   **时间复杂度:** O(NlogN)。
*   **辅助空间:** O(N)。