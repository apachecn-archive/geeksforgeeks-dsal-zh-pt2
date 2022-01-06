# 在不改变给定数组平均值的情况下可以删除的三元组的计数

> 原文:[https://www . geeksforgeeks . org/不改变给定数组平均值即可移除的三元组计数/](https://www.geeksforgeeks.org/count-of-triplets-that-can-be-removed-without-changing-mean-of-given-array/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算可能的三元组的数量，以便它们可以从数组中移除，而不改变数组的[算术平均值](https://www.geeksforgeeks.org/arithmetic-mean/)。

**示例:**

> **输入:** arr[] = {8，7，4，6，3，0，7}
> **输出:** 3
> **解释:**给定数组有 3 个可能的三元组，去掉它们不会影响数组的算术平均值。有{7，3，0}、{4，6，0}和{3，0，7}。
> 
> **输入:** arr[] = {5，5，5，5 }
> T3】输出: 4

**方法:**给定的问题可以通过以下观察来解决:对于剩余的[数组](https://www.geeksforgeeks.org/array-data-structure/)的[平均值](https://www.geeksforgeeks.org/arithmetic-mean/)为常数，移除的三元组的平均值必须等于初始数组的平均值。因此，给定的问题被简化为[寻找具有给定总和的三元组的计数](https://www.geeksforgeeks.org/print-all-triplets-with-given-sum/)，这可以通过以下步骤使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)来解决:

*   迭代给定数组 **arr[]** 以获得所有可能的值对 **(a，b)** ，并将它们的和插入到[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
*   迭代数组时，检查映射中是否已经存在(**TargetSum –( a+b)**)。如果是，则将所需计数的值增加其频率。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// triplets with the given sum
int countTriplets(int arr[], int n, int sum)
{
    // Stores the final count
    int cnt = 0;

    // Map to store occured elements
    unordered_map<int, int> m;

    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {

            // Check if Sum - (a + b)
            // is present in map
            int k = sum - (arr[i] + arr[j]);
            if (m.find(k) != m.end())

                // Increment count
                cnt += m[k];
        }

        // Store the occurences
        m[arr[i]]++;
    }

    // Return Answer
    return cnt;
}

// Function to C=find count of triplets
// that can be removed without changing
// arithmetic mean of the given array
int count_triplets(int arr[], int n)
{
    // Stores sum of all elements
    // of the given array
    int sum = 0;

    // Calculate the sum of the array
    for (int i = 0; i < n; i++) {
        sum = sum + arr[i];
    }
    // Store the arithmetic mean
    int mean = sum / n;
    int reqSum = 3 * mean;

    if ((3 * sum) % n != 0)
        return 0;

    // Return count
    return countTriplets(arr, n, reqSum);
}

// Driver Code
int main()
{
    int arr[] = { 5, 5, 5, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << count_triplets(arr, N);

    return 0;
}
```

## 蟒蛇 3

```
# python code for the above approach

# Function to count the number of
# triplets with the given sum
def countTriplets(arr, n, sum):

    # Stores the final count
    cnt = 0

    # Map to store occured elements
    m = {}

    for i in range(0, n-1):
        for j in range(i+1, n):

            # Check if Sum - (a + b)
            # is present in map
            k = sum - (arr[i] + arr[j])
            if (k in m):

                # Increment count
                cnt += m[k]

        # Store the occurences
        if arr[i] in m:
            m[arr[i]] += 1
        else:
            m[arr[i]] = 1

    # Return Answer
    return cnt

# Function to C=find count of triplets
# that can be removed without changing
# arithmetic mean of the given array
def count_triplets(arr, n):

    # Stores sum of all elements
    # of the given array
    sum = 0

    # Calculate the sum of the array
    for i in range(0, n):
        sum = sum + arr[i]

    # Store the arithmetic mean
    mean = sum // n
    reqSum = 3 * mean

    if ((3 * sum) % n != 0):
        return 0

    # Return count
    return countTriplets(arr, n, reqSum)

# Driver Code
if __name__ == "__main__":

    arr = [5, 5, 5, 5]
    N = len(arr)
    print(count_triplets(arr, N))

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach

    // Function to count the number of
    // triplets with the given sum
    const countTriplets = (arr, n, sum) => {

        // Stores the final count
        let cnt = 0;

        // Map to store occured elements
        let m = {};

        for (let i = 0; i < n - 1; i++) {
            for (let j = i + 1; j < n; j++) {

                // Check if Sum - (a + b)
                // is present in map
                let k = sum - (arr[i] + arr[j]);
                if (k in m)

                    // Increment count
                    cnt += m[k];
            }

            // Store the occurences
            if (arr[i] in m) m[arr[i]]++;
            else m[arr[i]] = 1;
        }

        // Return Answer
        return cnt;
    }

    // Function to C=find count of triplets
    // that can be removed without changing
    // arithmetic mean of the given array
    const count_triplets = (arr, n) => {

        // Stores sum of all elements
        // of the given array
        let sum = 0;

        // Calculate the sum of the array
        for (let i = 0; i < n; i++) {
            sum = sum + arr[i];
        }

        // Store the arithmetic mean
        let mean = parseInt(sum / n);
        let reqSum = 3 * mean;

        if ((3 * sum) % n != 0)
            return 0;

        // Return count
        return countTriplets(arr, n, reqSum);
    }

    // Driver Code
    let arr = [5, 5, 5, 5];
    let N = arr.length;
    document.write(count_triplets(arr, N));

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*