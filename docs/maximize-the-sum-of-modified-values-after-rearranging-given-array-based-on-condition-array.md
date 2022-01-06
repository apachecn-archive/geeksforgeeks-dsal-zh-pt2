# 根据条件数组

重新排列给定数组后，最大化修改值的总和

> 原文:[https://www . geeksforgeeks . org/最大化基于条件给定数组重新排列后的修改值总和数组/](https://www.geeksforgeeks.org/maximize-the-sum-of-modified-values-after-rearranging-given-array-based-on-condition-array/)

给定一个长度为 **N** 的*二进制数组* **arr1[]** 和一个*整数数组***arr 2[**，任务是重新排列数组 **arr2** 中的元素，使得生成的总**成本**最大化。生成的总成本通过 **arr2** 数组中的修改值的总和来计算。值的修改方式是 **arr1** 数组中值 0 对应的整数对其他元素没有影响，但是 **arr1** 数组中值 1 对应的整数可以是下一个整数的两倍。

**示例:**

> **输入:** N = 2，arr1 = [1，0]，arr2 = [3，4]
> **输出:** 11
> **说明:**元素 3 对应值 1，因此可以使下一个元素的值翻倍。在两种可能的排列方式中[3，4]和[4，3]，因此在第一种情况下产生的成本是 3+4*2 = 11，在第二种情况下产生的成本是 4+3=7
> 
> **输入:** N = 5，arr1 = [1，0，1，0，1]，arr2 = [3，7，2，12，5]
> **输出:** 53
> **说明:**在排列[3，7，2，5，12]中可以生成最大成本这里第 1，3，4 元素对应于值 1，因此它们的下一个元素成本可以翻倍，因此成本为 3+7*2+2+5*2+12*2=53

**方法:**给定的问题可以用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。这个想法是[按降序排列数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)，然后迭代它来计算生成的成本。可以遵循以下步骤:

*   初始化一个辅助[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr1** 并将数组 **arr2** 的所有元素复制到其中，这些元素在数组 **arr1** 中具有对应的值 1
*   在数组中找到最小值 **arr1，**从数组中移除并将其存储在变量中，比如 **val**
*   [按降序排列数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/) **数组 2**
*   初始化一个变量**和**来计算产生的最大成本
*   如果数组 **arr1** 中的所有元素都是 1，那么将除最小值**值**之外的所有元素的值加倍，并返回它们的总和
*   否则将 **arr1** 元素的值增加一倍到 **ans、**中，其余所有元素不做修改

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to compute maximum power
int max_pow(vector<int>& arr1, vector<int>& arr2)
{

    // Count of 1 in arr1
    int cnt = count(arr1.begin(), arr1.end(), 1);

    // Keep an array of integers corresponding
    // to value 1 in arr1 to eliminate the
    // integers contributing to minimum cost
    vector<int> cost1;

    for (int i = 0; i < arr1.size(); ++i) {
        if (arr1[i] == 1)
            cost1.push_back(arr2[i]);
    }

    int val = cost1[0];
    for (int i = 1; i < cost1.size(); ++i) {
        val = min(val, cost1[i]);
    }

    // Delete the minimum cost
    arr2.erase(find(arr2.begin(), arr2.end(), val));

    sort(arr2.rbegin(), arr2.rend());

    // Ans for storing max result
    int ans = 0;

    // Case when all are of type 1
    if (arr2.size() == cnt - 1) {
        int sum = 0;
        for (auto it : arr2) {
            sum += it;
        }
        ans = sum * 2 + val;
    }

    else {
        int sum = 0;
        for (auto it : arr2) {
            sum += it;
        }
        for (int i = 0; i < cnt; ++i) {
            sum += arr2[i];
        }
        ans = val + sum;
    }
    return ans;
}

// Driver code
int main()
{
    int N = 5;
    vector<int> arr_type = { 1, 0, 1, 0, 1 };
    vector<int> arr_power = { 3, 2, 7, 12, 5 };
    cout << max_pow(arr_type, arr_power);

    return 0;
}

    // This code is contributed by rakeshsahni
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Function to compute maximum power
def max_pow(arr1, arr2):

    # Count of 1 in arr1
    count = arr1.count(1)

    # Keep an array of integers corresponding
    # to value 1 in arr1 to eliminate the
    # integers contributing to minimum cost
    cost1 = []

    for i in range(len(arr1)):
        if(arr1[i] == 1):
            cost1.append(arr2[i])
    val = min(cost1)

    # Delete the minimum cost
    del arr2[arr2.index(val)]

    arr2.sort(reverse = True)

    # Ans for storing max result
    ans = 0

    # Case when all are of type 1
    if(len(arr2) == count-1):
        ans = sum(arr2)*2 + val

    else:
        ans = val + sum(arr2)+sum(arr2[:count])
    return ans

# Driver code
N = 5
arr_type = [1, 0, 1, 0, 1]
arr_power = [3, 2, 7, 12, 5]
print(max_pow(arr_type, arr_power))
```

## java 描述语言

```
<script>
// JavaScript implementation for the above approach

// Function to compute maximum power
function removeSmallest(arr1, arr2)
{
    var min = Math.min(...arr1);
    return arr2.filter(e => e != min);
}

function add(accumulator, a) {
    return accumulator + a;
}
function max_pow(arr1, arr2){

    // Count of 1 in arr1
    let count = 0
    arr1.forEach(e=>{if(e == 1)
                          count += 1
                          })

    // Keep an array of integers corresponding
    // to value 1 in arr1 to eliminate the
    // integers contributing to minimum cost
    let cost1 = []
    let i = 0
    arr1.forEach(e=>{if(e == 1){
                          cost1.push(arr2[i])
                          }
                          i += 1
                          })

    let val = Math.min(...cost1)

    // Delete the minimum cost
    arr2 = removeSmallest(cost1,arr2)

    arr2.sort(function(a, b){return a - b})
    arr2.reverse()

    // Ans for storing max result
    let ans = 0

    // Case when all are of type 1
    if(arr2.length == count-1)
        ans = (arr2.reduce(add,0))*2 + val
    else
        ans = val + arr2.reduce(add,0)+(arr2.slice(0,count)).reduce(add,0)

    return ans
}

// Driver code
let N = 5
let arr_type = [1, 0, 1, 0, 1]
let arr_power = [3, 2, 7, 12, 5]
document.write(max_pow(arr_type, arr_power))

// This code is contributed by rohitsingh07052.
</script>
```

**Output**

```
53
```

**时间复杂度:**O(N * log N)
T3】空间复杂度: O(N)