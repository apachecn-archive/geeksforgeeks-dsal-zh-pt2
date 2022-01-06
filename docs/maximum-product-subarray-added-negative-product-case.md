# 最大产品斯巴瑞|新增负产品案例

> 原文:[https://www . geesforgeks . org/max-product-subarray-add-negative-product-case/](https://www.geeksforgeeks.org/maximum-product-subarray-added-negative-product-case/)

给定一个包含正整数和负整数的数组，求最大乘积子数组的乘积。预期时间复杂度为 0(n)，只能使用 0(1)个额外空间。最大乘积可以是正、负或零。

**示例:**

```
Input : arr[] = {-2, -3, 0, -2, -40}
Output : 80
Subarray : arr[3..4] i.e.{-2, -40}

Input : arr[] = {0, -4, 0, -2}
Output : 0 
```

[Recommended : Please try your approach first on IDE and then look at the solution.](https://ide.geeksforgeeks.org/)

这个问题我们在[最大积子阵](https://www.geeksforgeeks.org/maximum-product-subarray/)中讨论过，但是有一个限制，结果只能是正的。为了使最大乘积为负或零，变量 maxval(当前元素前的最大乘积)和 minval(当前元素前的最小乘积)的值必须更新如下:

1.  **当 arr[i]为正时:**由于 maxval 是最大可能值，只需将 arr[i]与 maxval 相乘即可获得新的 maxval。minval 是最小可能负乘积。如果它的前一个值是负的，那么只需将其乘以 arr[i]。如果它的值是 1，保持它为 1。
2.  **当 arr[i]为 0 时:**考虑测试用例:arr[] = {0，-4，0，-2}。在这种情况下，最大乘积为 0。为了解释我们算法中的这种情况，每当 arr[i]为零时，用 0 而不是 1 更新 maxval。任何数与零的乘积为零。考虑另一个测试用例，arr[] = {0，1，2}。
    如果 maxval 在当前迭代后保持为零(根据上述步骤)，并且下一个元素为正，则结果将为零，而不是正元素。考虑到在每次迭代结束时检查 maxval 是否为零。
    如果为零，则设置为 1。用 1 作为子数组乘积更新 minval，其中零作为元素将为零，这将导致最小可能值的损失。因此，通过将 minval 设置为 1，即重新开始产品计算，将此零点从 subarray 中排除。
3.  **当 arr[i]为负时:**maxval 的新值为前一个 minval*arr[i]，minval 的新值为前一个 maxval*arr[i]。在更新 maxval 之前，将其先前的值存储在 prevMax 中，以用于更新 minval。

**实施:**

## C++

```
// C++ program to find maximum subarray product.
#include <bits/stdc++.h>

using namespace std;

// Function to find maximum subarray product.
int findMaxProduct(int arr[], int n)
{
    int i;

    // As maximum product can be negative, so
    // initialize ans with minimum integer value.
    int ans = INT_MIN;

    // Variable to store maximum product until
    // current value.
    int maxval = 1;

    // Variable to store minimum product until
    // current value.
    int minval = 1;

    // Variable used during updation of maximum
    // product and minimum product.
    int prevMax;

    for (i = 0; i < n; i++) {

        // If current element is positive, update
        // maxval. Update minval if it is
        // negative.
        if (arr[i] > 0) {
            maxval = maxval * arr[i];
            minval = min(1, minval * arr[i]);
        }

        // If current element is zero, maximum
        // product cannot end at current element.
        // Update minval with 1 and maxval with 0.
        // maxval is updated to 0 as in case all
        // other elements are negative, then maxval
        // is 0.
        else if (arr[i] == 0) {
            minval = 1;
            maxval = 0;
        }

        // If current element is negative, then new
        // value of maxval is previous minval*arr[i]
        // and new value of minval is previous
        // maxval*arr[i]. Before updating maxval,
        // store its previous value in prevMax to
        // be used to update minval.
        else if (arr[i] < 0) {
            prevMax = maxval;
            maxval = minval * arr[i];
            minval = prevMax * arr[i];
        }

        // Update ans if necessary.
        ans = max(ans, maxval);

        // If maxval is zero, then to calculate
        // product for next iteration, it should
        // be set to 1 as maximum product
        // subarray does not include 0.
        // The minimum possible value
        // to be considered in maximum product
        // subarray is already stored in minval,
        // so when maxval is negative it is set to 1.
        if (maxval <= 0) {
            maxval = 1;
        }
    }

    return ans;
}

int main()
{
    int arr[] = { 0, -4, 0, -2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findMaxProduct(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```

// Java program to find maximum subarray product.
 class GFG{
// Function to find maximum subarray product.
static int findMaxProduct(int arr[], int n)
{
    int i;

    // As maximum product can be negative, so
    // initialize ans with minimum integer value.
    int ans = Integer.MIN_VALUE;

    // Variable to store maximum product until
    // current value.
    int maxval = 1;

    // Variable to store minimum product until
    // current value.
    int minval = 1;

    // Variable used during updation of maximum
    // product and minimum product.
    int prevMax;

    for (i = 0; i < n; i++) {

        // If current element is positive, update
        // maxval. Update minval if it is
        // negative.
        if (arr[i] > 0) {
            maxval = maxval * arr[i];
            minval = Math.min(1, minval * arr[i]);
        }

        // If current element is zero, maximum
        // product cannot end at current element.
        // Update minval with 1 and maxval with 0.
        // maxval is updated to 0 as in case all
        // other elements are negative, then maxval
        // is 0.
        else if (arr[i] == 0) {
            minval = 1;
            maxval = 0;
        }

        // If current element is negative, then new
        // value of maxval is previous minval*arr[i]
        // and new value of minval is previous
        // maxval*arr[i]. Before updating maxval,
        // store its previous value in prevMax to
        // be used to update minval.
        else if (arr[i] < 0) {
            prevMax = maxval;
            maxval = minval * arr[i];
            minval = prevMax * arr[i];
        }

        // Update ans if necessary.
        ans = Math.max(ans, maxval);

        // If maxval is zero, then to calculate
        // product for next iteration, it should
        // be set to 1 as maximum product
        // subarray does not include 0.
        // The minimum possible value
        // to be considered in maximum product
        // subarray is already stored in minval,
        // so when maxval is negative it is set to 1.
        if (maxval <= 0) {
            maxval = 1;
        }
    }

    return ans;
}

     public static void main(String[] args) {

    int arr[] = { 0, -4, 0, -2 };
    int n = arr.length;
         System.out.println(findMaxProduct(arr, n));
     }
}
```

## 蟒蛇 3

```
# Python3 program to find maximum
# subarray product.

# Function to find maximum
# subarray product.
def findMaxProduct(arr, n):

    # As maximum product can be negative,
    # so initialize ans with minimum
    # integer value.
    ans = -float('inf')

    # Variable to store maximum product
    # until current value.
    maxval = 1

    # Variable to store minimum product
    # until current value.
    minval = 1

    for i in range(0, n):

        # If current element is positive,
        # update maxval. Update minval
        # if it is negative.
        if arr[i] > 0:
            maxval = maxval * arr[i]
            minval = min(1, minval * arr[i])

        # If current element is zero, maximum
        # product cannot end at current element.
        # Update minval with 1 and maxval with 0.
        # maxval is updated to 0 as in case all
        # other elements are negative, then
        # maxval is 0.
        elif arr[i] == 0:
            minval = 1
            maxval = 0

        # If current element is negative,
        # then new value of maxval is previous
        # minval*arr[i] and new value of minval
        # is previous maxval*arr[i]. Before
        # updating maxval, store its previous
        # value in prevMax to be used to
        # update minval.
        elif arr[i] < 0:
            prevMax = maxval
            maxval = minval * arr[i]
            minval = prevMax * arr[i]

        # Update ans if necessary.
        ans = max(ans, maxval)

        # If maxval is zero, then to calculate
        # product for next iteration, it should
        # be set to 1 as maximum product subarray
        # does not include 0\. The minimum possible
        # value to be considered in maximum product
        # subarray is already stored in minval,
        # so when maxval is negative it is set to 1.
        if maxval <= 0:
            maxval = 1

    return ans

# Driver Code
if __name__ == "__main__":

    arr = [ 0, -4, 0, -2 ]
    n = len(arr)
    print(findMaxProduct(arr, n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# program to find maximum subarray product.
using System;

class GFG
{
// Function to find maximum subarray product.
static int findMaxProduct(int[] arr, int n)
{
    int i;

    // As maximum product can be negative, so
    // initialize ans with minimum integer value.
    int ans = Int32.MinValue;

    // Variable to store maximum product until
    // current value.
    int maxval = 1;

    // Variable to store minimum product until
    // current value.
    int minval = 1;

    // Variable used during updation of maximum
    // product and minimum product.
    int prevMax;

    for (i = 0; i < n; i++)
    {

        // If current element is positive, update
        // maxval. Update minval if it is
        // negative.
        if (arr[i] > 0)
        {
            maxval = maxval * arr[i];
            minval = Math.Min(1, minval * arr[i]);
        }

        // If current element is zero, maximum
        // product cannot end at current element.
        // Update minval with 1 and maxval with 0.
        // maxval is updated to 0 as in case all
        // other elements are negative, then maxval
        // is 0.
        else if (arr[i] == 0)
        {
            minval = 1;
            maxval = 0;
        }

        // If current element is negative, then new
        // value of maxval is previous minval*arr[i]
        // and new value of minval is previous
        // maxval*arr[i]. Before updating maxval,
        // store its previous value in prevMax to
        // be used to update minval.
        else if (arr[i] < 0)
        {
            prevMax = maxval;
            maxval = minval * arr[i];
            minval = prevMax * arr[i];
        }

        // Update ans if necessary.
        ans = Math.Max(ans, maxval);

        // If maxval is zero, then to calculate
        // product for next iteration, it should
        // be set to 1 as maximum product
        // subarray does not include 0.
        // The minimum possible value
        // to be considered in maximum product
        // subarray is already stored in minval,
        // so when maxval is negative it is set to 1.
        if (maxval <= 0)
        {
            maxval = 1;
        }
    }

    return ans;
}

// Driver Code
public static void Main()
{
    int[] arr = { 0, -4, 0, -2 };
    int n = arr.Length;
    Console.WriteLine(findMaxProduct(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// subarray product.

// Function to find maximum
// subarray product.
function findMaxProduct(&$arr, $n)
{

    // As maximum product can be negative, so
    // initialize ans with minimum integer value.
    $ans = 0;

    // Variable to store maximum product
    // until current value.
    $maxval = 1;

    // Variable to store minimum product
    // until current value.
    $minval = 1;

    // Variable used during updation of
    // maximum product and minimum product.
    // is prevMax
    for ($i = 0; $i < $n; $i++)
    {

        // If current element is positive, update
        // maxval. Update minval if it is
        // negative.
        if ($arr[$i] > 0)
        {
            $maxval = $maxval * $arr[i];
            $minval = min(1, $minval * $arr[$i]);
        }

        // If current element is zero, maximum
        // product cannot end at current element.
        // Update minval with 1 and maxval with 0.
        // maxval is updated to 0 as in case all
        // other elements are negative, then maxval
        // is 0.
        else if ($arr[$i] == 0)
        {
            $minval = 1;
            $maxval = 0;
        }

        // If current element is negative, then new
        // value of maxval is previous minval*arr[i]
        // and new value of minval is previous
        // maxval*arr[i]. Before updating maxval,
        // store its previous value in prevMax to
        // be used to update minval.
        else if ($arr[$i] < 0)
        {
            $prevMax = $maxval;
            $maxval = $minval * $arr[$i];
            $minval = $prevMax * $arr[$i];
        }

        // Update ans if necessary.
        $ans = max($ans, $maxval);

        // If maxval is zero, then to calculate
        // product for next iteration, it should
        // be set to 1 as maximum product
        // subarray does not include 0.
        // The minimum possible value
        // to be considered in maximum product
        // subarray is already stored in minval,
        // so when maxval is negative it is set to 1.
        if ($maxval <= 0)
        {
            $maxval = 1;
        }
    }

    return $ans;
}

// Driver Code
$arr = array( 0, -4, 0, -2 );
$n = sizeof($arr);
echo findMaxProduct($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>

// JavaScript program to find maximum subarray product.

// Function to find maximum subarray product.
function findMaxProduct(arr, n)
{
    let i;

    // As maximum product can be negative, so
    // initialize ans with minimum integer value.
    let ans = -1;

    // Variable to store maximum product until
    // current value.
    let maxval = 1;

    // Variable to store minimum product until
    // current value.
    let minval = 1;

    // Variable used during updation of maximum
    // product and minimum product.
    let prevMax;

    for (i = 0; i < n; i++) {

        // If current element is positive, update
        // maxval. Update minval if it is
        // negative.
        if (arr[i] > 0) {
            maxval = maxval * arr[i];
            minval = Math.min(1, minval * arr[i]);
        }

        // If current element is zero, maximum
        // product cannot end at current element.
        // Update minval with 1 and maxval with 0.
        // maxval is updated to 0 as in case all
        // other elements are negative, then maxval
        // is 0.
        else if (arr[i] == 0) {
            minval = 1;
            maxval = 0;
        }

        // If current element is negative, then new
        // value of maxval is previous minval*arr[i]
        // and new value of minval is previous
        // maxval*arr[i]. Before updating maxval,
        // store its previous value in prevMax to
        // be used to update minval.
        else if (arr[i] < 0) {
            prevMax = maxval;
            maxval = minval * arr[i];
            minval = prevMax * arr[i];
        }

        // Update ans if necessary.
        ans = Math.max(ans, maxval);

        // If maxval is zero, then to calculate
        // product for next iteration, it should
        // be set to 1 as maximum product
        // subarray does not include 0.
        // The minimum possible value
        // to be considered in maximum product
        // subarray is already stored in minval,
        // so when maxval is negative it is set to 1.
        if (maxval <= 0) {
            maxval = 1;
        }
    }

    return ans;
}

// Driver code

        let arr = [ 0, -4, 0, -2 ];
        let n = arr.length;
        document.write(findMaxProduct(arr, n));

// This code is contributed by souravghosh0416.
</script>
```

**输出:**

```
 0
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)