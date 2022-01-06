# 最小化由相同索引元素的乘积组成的所有子阵列的和

> 原文:[https://www . geeksforgeeks . org/最小化所有子阵列的总和-由相同索引元素的乘积组成/](https://www.geeksforgeeks.org/minimize-the-sum-of-all-the-subarrays-made-up-of-the-products-of-same-indexed-elements/)

给定两个长度为 **N** 的阵列 **arr[]** 和 **arr2[]** ，任务是在重新排列第二个阵列后，找到由两个阵列的相同索引元素的乘积组成的所有子阵列的**最小和**。

**注意:**由于答案可以很大，所以打印答案取模 **10 <sup>9</sup> + 7** 。

**示例:**

> **输入:** arr[] = {1，2}，arr2[] = {2，3}
> **输出:** 14
> **解释:**
> 将 arr2[]重新排列为{3，2}
> 因此，两个数组的相同索引元素的乘积变为{3，4}。
> 可能的子阵列有{3}、{4}、{3，4}
> 子阵列之和= 3 + 4 + 7 = 14。
> **输入:** arr[] = {1，2，3}，arr2[] = {2，3，2}
> **输出:** 43
> **解释:**
> 将 arr2[]重新排列为{3，2，2}
> 因此，两个数组的相同索引元素的乘积变为{3，4，6}。
> 因此，所有子阵列之和= 3 + 4 + 6 + 7 + 10 + 13 = 43

**进场:**
可以观察到， **i <sup>第</sup>元素**出现在**(I+1)*(n–I)**子阵中。因此，任务是最大化**(I+1)*(n–I)* a[I]* b[I]**的和。按照以下步骤解决问题:

*   由于 **arr2[]** 的元素只能重新排列，因此**(I+1)*(n–I)* a[I]**的值对于每一个 i <sup>第</sup>个元素都是不变的。
*   因此，计算所有指数的**(I+1)*(n–I)* a[I]**的值，然后**对**产品进行排序。
*   按**降序排列数组**arr 2[]****。
*   对于每个 i <sup>第</sup>个指数，按降序计算**(I+1)*(n–I)* a【I】**和按升序计算**arr 2【I】**的值的**乘积**之和。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
#define ll long long
using namespace std;

const int mod = (int)1e9 + 7;

// Returns the greater of
// the two values
bool comp(ll a, ll b)
{
    if (a > b)
        return true;
    else
        return false;
}

// Function to rearrange the second array such
// that the sum of its product of same indexed
// elements from both the arrays is minimized
ll findMinValue(vector<ll>& a, vector<ll>& b)
{

    int n = a.size();

    // Stores (i - 1) * (n - i) * a[i]
    // for every i-th element
    vector<ll> pro(n);

    for (int i = 0; i < n; ++i) {

        // Updating the value of pro
        // according to the function
        pro[i] = ((ll)(i + 1) * (ll)(n - i));
        pro[i] *= (1LL * a[i]);
        ;
    }

    // Sort the array in reverse order
    sort(b.begin(), b.end(), comp);

    // Sort the products
    sort(pro.begin(), pro.end());

    ll ans = 0;
    for (int i = 0; i < n; ++i) {

        // Updating the ans
        ans += (pro[i] % mod * b[i]) % mod;
        ans %= mod;
    }

    // Return the ans
    return ans;
}

// Driver code
int main()
{

    vector<ll> a = { 1, 2, 3 };
    vector<ll> b = { 2, 3, 2 };
    // Function call
    cout << findMinValue(a, b) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static int mod = (int)1e9 + 7;

// Function to rearrange the second array such
// that the sum of its product of same indexed
// elements from both the arrays is minimized
static int findMinValue(int [] a, int []b)
{
    int n = a.length;

    // Stores (i - 1) * (n - i) * a[i]
    // for every i-th element
    int [] pro = new int[n];

    for(int i = 0; i < n; ++i)
    {

        // Updating the value of pro
        // according to the function
        pro[i] = ((i + 1) * (n - i));
        pro[i] *= (1L * a[i]);
        ;
    }

    // Sort the array in reverse order
    Integer[] input = Arrays.stream(b).boxed(
                      ).toArray(Integer[]::new);

    Arrays.sort(input, (x, y) -> y - x);
    b = Arrays.stream(input).mapToInt(
        Integer::intValue).toArray();

    // Sort the products
    Arrays.sort(pro);

    int ans = 0;
    for(int i = 0; i < n; ++i)
    {

        // Updating the ans
        ans += (pro[i] % mod * b[i]) % mod;
        ans %= mod;
    }

    // Return the ans
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int []a = { 1, 2, 3 };
    int []b = { 2, 3, 2 };

    // Function call
    System.out.print(findMinValue(a, b) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
mod = 1e9 +7

# Function to rearrange
# the second array such
# that the sum of its
# product of same indexed
# elements from both
# the arrays is minimized
def findMinValue(a, b):

    n = len(a)

    # Stores (i - 1) * (n - i) * a[i]
    # for every i-th element
    pro = [0] * (n)

    for i in range (n):

        # Updating the value of pro
        # according to the function
        pro[i] = ((i + 1) * (n - i))
        pro[i] *= (a[i])

    # Sort the array in reverse order
    b.sort(reverse = True)

    # Sort the products
    pro.sort()

    ans = 0
    for i in range (n):

        # Updating the ans
        ans += (pro[i] % mod * b[i]) % mod
        ans %= mod

    # Return the ans
    return ans

# Driver code
if __name__ == "__main__":

    a = [1, 2, 3]
    b = [2, 3, 2]

    # Function call
    print (int(findMinValue(a, b)))

# This code is contributed by Chitranayal
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach
var mod = 1000000007;

// Function to rearrange the second array such
// that the sum of its product of same indexed
// elements from both the arrays is minimized
function findMinValue(a, b)
{
    var n = a.length;

    // Stores (i - 1) * (n - i) * a[i]
    // for every i-th element
    var pro = Array(n);

    for(var i = 0; i < n; ++i)
    {

        // Updating the value of pro
        // according to the function
        pro[i] = ((i + 1) * (n - i));
        pro[i] *= (1 * a[i]);
        ;
    }

    // Sort the array in reverse order
    b.sort((a, b) => b - a)

    // Sort the products
    pro.sort((a, b) => a - b)

    var ans = 0;
    for(var i = 0; i < n; ++i)
    {

        // Updating the ans
        ans += (pro[i] % mod * b[i]) % mod;
        ans %= mod;
    }

    // Return the ans
    return ans;
}

// Driver code
var a = [ 1, 2, 3 ];
var b = [ 2, 3, 2 ];

// Function call
document.write( findMinValue(a, b));

// This code is contributed by itsok

</script>
```

**Output:** 

```
43
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*