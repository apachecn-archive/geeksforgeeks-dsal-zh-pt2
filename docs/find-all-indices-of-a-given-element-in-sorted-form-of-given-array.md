# 以给定数组的排序形式找到给定元素的所有索引

> 原文:[https://www . geeksforgeeks . org/find-给定数组排序形式的给定元素的所有索引/](https://www.geeksforgeeks.org/find-all-indices-of-a-given-element-in-sorted-form-of-given-array/)

给定大小为 **N** 的整数的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和目标值 **val** 。你的任务是在 [**排序**](https://www.geeksforgeeks.org/sorting-algorithms/) 数组**后，按照递增**的顺序找到数组中 val 的**索引**。

**注:**指数必须按递增顺序排列。

**示例:**

> **输入:** arr = [1，2，5，2，3]，val = 2
> **输出:** 1 2
> **说明:**排序后，arr[]变为[1，2，2，3，5]。arr[i] = 2 的指数是 1 和 2。因为指数应该是递增的，所以它们是(1，2)而不是(2，1)
> 
> **输入:**arr**=【1，2，5，2，3】**，** val = 6
> **输出:** []
> **说明:**排序后，nums 为【1，2，2，3，5】。值 6 不是**
> 
> ## **C++**
> 
> ```
> // C++ implementation of the above approach
>  
> #include <bits/stdc++.h>
> using namespace std;
>  
> // Function to find indices
> // of val in array after sorting
> vector<int> targetIndices(vector<int>& nums, int val)
> {
>     int count_less = 0;
>     int count_target = 0;
>  
>     // Loop to count smaller elements and val
>     for (auto& it : nums) {
>         if (it == val)
>             count_target++;
>         if (it < val)
>             count_less++;
>     }
>  
>     // List to store indices
>     vector<int> ans;
>     while (count_target--) {
>         ans.push_back(count_less++);
>     }
>     return ans;
> }
>  
> // Driver code
> int main()
> {
>     vector<int> nums{ 1, 2, 5, 2, 3 };
>     int val = 2;
>     vector<int> ans = targetIndices(nums, val);
>  
>     // Loop to print indices
>     for (int i = 0; i < ans.size(); i++) {
>         cout << ans[i] << " ";
>     }
>     return 0;
> }
> ```
> 
> ## **Java 语言(一种计算机语言，尤用于创建网站)**
> 
> ```
> // Java implementation of the above approach
> import java.util.*;
> public class GFG {
>  
>     // Function to find indices
>     // of val in array after sorting
>     static List<Integer> targetIndices(int[] nums, int val)
>     {
>         int count_less = 0;
>         int count_target = 0;
>  
>         // Loop to count smaller elements and val
>         for (int i = 0; i < nums.length; i++) {
>             if (nums[i] == val)
>                 count_target++;
>             if (nums[i] < val)
>                 count_less++;
>         }
>  
>         // List to store indices
>         List<Integer> ans = new ArrayList<Integer>();
>         while (count_target > 0) {
>             ans.add(count_less++);
>             count_target--;
>         }
>         return ans;
>     }
>  
>     // Driver code
>     public static void main(String args[])
>     {
>         int[] nums = { 1, 2, 5, 2, 3 };
>         int val = 2;
>         List<Integer> ans = targetIndices(nums, val);
>  
>         // Loop to print indices
>         for (int i = 0; i < ans.size(); i++) {
>             zz System.out.print(ans.get(i) + " ");
>         }
>     }
> }
>  
> // This code is contributed by Samim Hossain Mondal.
> ```
> 
> ## **蟒蛇 3**
> 
> ```
> # python implementation of the above approach
>  
> # Function to find indices
> # of val in array after sorting
> def targetIndices(nums, val):
>  
>     count_less = 0
>     count_target = 0
>  
>     # Loop to count smaller elements and val
>     for it in nums:
>         if (it == val):
>             count_target += 1
>         if (it < val):
>             count_less += 1
>  
>         # List to store indices
>     ans = []
>     while (count_target):
>         count_target -= 1
>         ans.append(count_less)
>         count_less += 1
>  
>     return ans
>  
> # Driver code
> if __name__ == "__main__":
>  
>     nums = [1, 2, 5, 2, 3]
>     val = 2
>     ans = targetIndices(nums, val)
>  
>     # Loop to print indices
>     for i in range(0, len(ans)):
>         print(ans[i], end=" ")
>  
>     # This code is contributed by rakeshsahni
> ```
> 
> ## **C#**
> 
> ```
> // C# implementation of the above approach
> using System;
> using System.Collections;
> using System.Collections.Generic;
>  
> class GFG {
>  
>     // Function to find indices
>     // of val in array after sorting
>     static ArrayList targetIndices(int[] nums, int val)
>     {
>         int count_less = 0;
>         int count_target = 0;
>  
>         // Loop to count smaller elements and val
>         for (int i = 0; i < nums.Length; i++) {
>             if (nums[i] == val)
>                 count_target++;
>             if (nums[i] < val)
>                 count_less++;
>         }
>  
>         // List to store indices
>         ArrayList ans = new ArrayList();
>         while (count_target > 0) {
>             ans.Add(count_less++);
>             count_target--;
>         }
>         return ans;
>     }
>  
>     // Driver code
>     public static void Main()
>     {
>         int[] nums = { 1, 2, 5, 2, 3 };
>         int val = 2;
>         ArrayList ans = targetIndices(nums, val);
>  
>         // Loop to print indices
>         for (int i = 0; i < ans.Count; i++) {
>             Console.Write(ans[i] + " ");
>         }
>     }
> }
>  
> // This code is contributed by Samim Hossain Mondal.
> ```
> 
> ## **java 描述语言**
> 
> ```
> <script>
> // Javascript implementation of the above approach
>  
> // Function to find indices
> // of val in array after sorting
> function targetIndices(nums, val)
> {
>     let count_less = 0;
>     let count_target = 0;
>  
>     // Loop to count smaller elements and val
>     for (let i = 0; i < nums.length; i++) {
>         if (nums[i] == val)
>             count_target++;
>         if (nums[i] < val)
>             count_less++;
>     }
>  
>     // List to store indices
>     let ans = [];
>     while (count_target--) {
>         ans.push(count_less++);
>     }
>     return ans;
> }
>  
> // Driver code
> let nums = [ 1, 2, 5, 2, 3 ];
> let val = 2;
> let ans = targetIndices(nums, val);
>  
>     // Loop to print indices
>     for (let i = 0; i < ans.length; i++) {
>         document.write(ans[i] + " ");
>     }
>      
> // This code is contributed by Samim Hossain Mondal.
> </script>
> ```
> 
> **出现在数组中。**

****幼稚法:**这种方法的概念是基于**排序**。数组按升序排序。然后遍历排序后的数组。遍历数组时，如果有任何值与目标匹配，则该索引会添加到答案列表中。迭代完成后，返回答案列表。
**时间复杂度:** O(N*logN)
**辅助空间:** O(1)**

****高效方法:**该方法基于对排序数组的**观察**。在以递增的顺序排列的**数组中，值**之前的所有元素**都小于值**。因此，为了得到排序数组中**值**的索引，我们可以简单地**比**值**少计算**元素**。如果**计数为 x** ，则**值**将从**第 x 个**索引开始(因为基于 0 的索引)。遵循以下步骤:********

*   遍历数组。使用变量存储小于值 ( **小计数**)的元素数**和具有与值**相同的值**的元素数(**相同的计数**)。**
*   如果一个元素的值小于值**，则将小计数**增加 1。
*   如果值**与值**相同，将**相同计数**增加 1。
*   遍历完成后，索引将从 smallCount 开始，到(smallCount+sameCount-1)结束

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find indices
// of val in array after sorting
vector<int> targetIndices(vector<int>& nums,
                          int val)
{
    int count_less = 0;
    int count_target = 0;

    // Loop to count smaller elements and val
    for (auto& it : nums) {
        if (it == val)
            count_target++;
        if (it < val)
            count_less++;
    }

    // List to store indices
    vector<int> ans;
    while (count_target--) {
        ans.push_back(count_less++);
    }
    return ans;
}

// Driver code
int main()
{
    vector<int> nums{ 1, 2, 5, 2, 3 };
    int val = 2;
    vector<int> ans = targetIndices(nums, val);

    // Loop to print indices
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;
public class GFG
{

// Function to find indices
// of val in array after sorting
static List<Integer> targetIndices(int []nums,
                          int val)
{
    int count_less = 0;
    int count_target = 0;

    // Loop to count smaller elements and val
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] == val)
            count_target++;
        if (nums[i] < val)
            count_less++;
    }

    // List to store indices
    List<Integer> ans = new ArrayList<Integer>();
    while (count_target > 0) {
        ans.add(count_less++);
        count_target--;
    }
    return ans;
}

// Driver code
public static void main(String args[])
{
    int []nums = { 1, 2, 5, 2, 3 };
    int val = 2;
    List<Integer> ans = targetIndices(nums, val);

    // Loop to print indices
    for (int i = 0; i < ans.size(); i++) {zz
        System.out.print(ans.get(i) + " ");
    }
}
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to find indices
# of val in array after sorting
def targetIndices(nums, val):
    count_less = 0
    count_target = 0

    # Loop to count smaller elements and val
    for i in range(len(nums)):
        if (nums[i] == val):
            count_target += 1
        if (nums[i] < val):
            count_less += 1

    # List to store indices
    ans = []
    while (count_target):
        ans.append(count_less)
        count_less += 1
        count_target -= 1
    return ans

# Driver code
nums = [1, 2, 5, 2, 3]
val = 2
ans = targetIndices(nums, val)

# Loop to print indices
for i in range(len(ans)):
    print(ans[i], end=" ")

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{

// Function to find indices
// of val in array after sorting
static ArrayList targetIndices(int []nums,
                          int val)
{
    int count_less = 0;
    int count_target = 0;

    // Loop to count smaller elements and val
    for (int i = 0; i < nums.Length; i++) {
        if (nums[i] == val)
            count_target++;
        if (nums[i] < val)
            count_less++;
    }

    // List to store indices
    ArrayList ans = new ArrayList();
    while (count_target > 0) {
        ans.Add(count_less++);
        count_target--;
    }
    return ans;
}

// Driver code
public static void Main()
{
    int []nums = { 1, 2, 5, 2, 3 };
    int val = 2;
    ArrayList ans = targetIndices(nums, val);

    // Loop to print indices
    for (int i = 0; i < ans.Count; i++) {
        Console.Write(ans[i] + " ");
    }
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to find indices
// of val in array after sorting
function targetIndices(nums, val)
{
    let count_less = 0;
    let count_target = 0;

    // Loop to count smaller elements and val
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] == val)
            count_target++;
        if (nums[i] < val)
            count_less++;
    }

    // List to store indices
    let ans = [];
    while (count_target--) {
        ans.push(count_less++);
    }
    return ans;
}

// Driver code
let nums = [ 1, 2, 5, 2, 3 ];
let val = 2;
let ans = targetIndices(nums, val);

    // Loop to print indices
    for (let i = 0; i < ans.length; i++) {
        document.write(ans[i] + " ");
    }

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
1 2 
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)