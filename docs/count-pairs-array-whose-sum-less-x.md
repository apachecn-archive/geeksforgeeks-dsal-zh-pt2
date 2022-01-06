# 计数排序数组中总和小于 x 的对

> 原文:[https://www . geesforgeks . org/count-pairs-array-what-sum-less-x/](https://www.geeksforgeeks.org/count-pairs-array-whose-sum-less-x/)

给定一个排序的整数数组和数字 x，任务是对数组中总和小于 x 的对进行计数。
示例:

```
Input  : arr[] = {1, 3, 7, 9, 10, 11}
         x = 7
Output : 1
There is only one pair (1, 3)

Input  : arr[] = {1, 2, 3, 4, 5, 6, 7, 8}
         x = 7
Output : 6
Pairs are (1, 2), (1, 3), (1, 4), (1, 5)
          (2, 3) and (2, 4)  
```

这个问题的一个**简单解决方案**运行两个循环，一个接一个地生成所有对，并检查当前对的和是否小于 x。
这个问题的一个**有效解决方案**是在 l 和 r 变量中取指数的初值和终值。

```
1) Initialize two variables l and r to find the candidate 
   elements in the sorted array.
       (a) l = 0
       (b) r = n - 1
2) Initialize : result = 0
2) Loop while l < r.

    // If current left and current
    // right have sum smaller than x,
    // the all elements from l+1 to r
    // form a pair with current
    (a) If (arr[l] + arr[r] < x)  
          result = result + (r - l)      

    (b) Else
            r--;

3) Return result
```

下面是以上步骤的实现。

## C++

```
// C++ program to count pairs in an array
// whose sum is less than given number x
#include<bits/stdc++.h>
using namespace std;

// Function to count pairs in array
// with sum less than x.
int findPairs(int arr[],int n,int x)
{
    int l = 0, r = n-1;
    int result = 0;

    while (l < r)
    {
        // If current left and current
        // right have sum smaller than x,
        // the all elements from l+1 to r
        // form a pair with current l.
        if (arr[l] + arr[r] < x)
        {
            result += (r - l);
            l++;
        }

        // Move to smaller value
        else
            r--;
    }

    return result;
}

// Driven code
int main()
{
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8};
    int n = sizeof(arr)/sizeof(int);
    int x = 7;
    cout << findPairs(arr, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs in an array
// whose sum is less than given number x
class GFG {

    // Function to count pairs in array
    // with sum less than x.
    static int findPairs(int arr[], int n, int x)
    {

        int l = 0, r = n - 1;
        int result = 0;

        while (l < r)
        {

            // If current left and current
            // right have sum smaller than x,
            // the all elements from l+1 to r
            // form a pair with current l.
            if (arr[l] + arr[r] < x)
            {
                result += (r - l);
                l++;
            }

            // Move to smaller value
            else
                r--;
        }

        return result;
    }

    // Driver method
    public static void main(String[] args)
    {

        int arr[] = {1, 2, 3, 4, 5, 6, 7, 8};
        int n = arr.length;
        int x = 7;

        System.out.print(findPairs(arr, n, x));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to count pairs
# in an array whose sum is less
# than given number x

# Function to count pairs in array
# with sum less than x.
def findPairs(arr, n, x):

    l = 0; r = n-1
    result = 0

    while (l < r):

        # If current left and current
        # right have sum smaller than x,
        # the all elements from l+1 to r
        # form a pair with current l.
        if (arr[l] + arr[r] < x):

            result += (r - l)
            l += 1

        # Move to smaller value
        else:
            r -= 1

    return result

# Driver Code
arr = [1, 2, 3, 4, 5, 6, 7, 8]
n = len(arr)
x = 7
print(findPairs(arr, n, x))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# program to count pairs in
// an array whose sum is less
// than given number x
using System;

class GFG {

    // Function to count pairs in array
    // with sum less than x.
    static int findPairs(int []arr, int n,
                         int x)
    {

        int l = 0, r = n - 1;
        int result = 0;

        while (l < r)
        {

            // If current left and current
            // right have sum smaller than x,
            // the all elements from l+1 to r
            // form a pair with current l.
            if (arr[l] + arr[r] < x)
            {
                result += (r - l);
                l++;
            }

            // Move to smaller value
            else
                r--;
        }

        return result;
    }

    // Driver code
    public static void Main(String[] args)
    {

        int []arr = {1, 2, 3, 4, 5, 6, 7, 8};
        int n = arr.Length;
        int x = 7;

        Console.Write(findPairs(arr, n, x));
    }
}

// This code is contributed by parashar...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pairs in an array
// whose sum is less than given number x

// Function to count pairs in array
// with sum less than x.
function findPairs($arr,$n,$x)
{
    $l = 0;
    $r = $n - 1;
    $result = 0;

    while ($l < $r)
    {

        // If current left and current
        // right have sum smaller than x,
        // the all elements from l+1 to r
        // form a pair with current l.
        if ($arr[$l] + $arr[$r] < $x)
        {
            $result += ($r - $l);
            $l++;
        }

        // Move to smaller value
        else
            $r--;
    }

    return $result;
}

    // Driver Code
    $arr = array(1, 2, 3, 4, 5, 6, 7, 8);
    $n = sizeof($arr) / sizeof($arr[0]);
    $x = 7;
    echo findPairs($arr, $n, $x);
    return 0;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
//javascript program to count pairs in an array
// whose sum is less than given number x
// Function to count pairs in array
// with sum less than x.
function findPairs(arr,n,x)
{
    let l = 0, r = n-1;
    let result = 0;

    while (l < r)
    {
        // If current left and current
        // right have sum smaller than x,
        // the all elements from l+1 to r
        // form a pair with current l.
        if (arr[l] + arr[r] < x)
        {
            result += (r - l);
            l++;
        }

        // Move to smaller value
        else
            r--;
    }

    return result;
}

    let arr = [1, 2, 3, 4, 5, 6, 7, 8];
    let n = arr.length;
    let x = 7;
    document.write(findPairs(arr,n,x));

// This code is contributed by vaibhavrabadiya117.
</script>
```

**Output**

```
6
```

时间复杂度:O(n)
空间复杂度:O(1)

**使用基于策略的数据结构:**

它也适用于未排序的数组

## C++

```
#include <iostream>
using namespace std;
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
using namespace __gnu_pbds;
#define ordered_set                                        \
    tree<pair<int, int>, null_type, less<pair<int, int> >, \
         rb_tree_tag, tree_order_statistics_node_update>

int countPair(vector<int> v, int sum)
{
    int ans = 0;

    ordered_set st;
    int y = 0;
    for (auto i = v.rbegin(); i != v.rend(); i++) {
        int num = *i;
        if (st.empty())
            st.insert({ num, y });

        else {
            int left = sum - num;
            ans += st.order_of_key({ left, -1 });
            st.insert({ num, y });
        }
        y++;
    }

    return ans;
}
int main()
{

    int n;
    cin >> n;

    vector<int> v{ 1, 2, 3, 4, 5, 6, 7, 8 };

    int sum = 7;

    cout << countPair(v, sum);

    return 0;
}
```

**Output**

```
6
```

**扩展:**
如果数组没有排序，那么我们可以先对数组进行排序，然后应用上面的方法在 O(n Log n)时间内求解。
**相关文章:**
[统计所有差异等于 k 的不同对](https://www.geeksforgeeks.org/count-pairs-difference-equal-k/)
[统计给定和的对](https://www.geeksforgeeks.org/count-pairs-with-given-sum/)
**参考:**[https://www . quora . com/Given-a-sorted-integer-array-and-number-z-Count-all-pairs-x-y-in-array-so-x-+-y-z-Can-it-in-O-n 如果你喜欢 GeeksforGeeks 并想投稿，你也可以用](https://www.quora.com/Given-a-sorted-integer-array-and-number-z-count-all-pairs-x-y-in-the-array-so-that-x-+-y-z-Can-it-be-done-in-O-n)[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。