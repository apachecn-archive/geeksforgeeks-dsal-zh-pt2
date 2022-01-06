# 最大化可被 K 整除的和对数量

> 原文:[https://www . geeksforgeeks . org/最大化可被 k 整除的对和数/](https://www.geeksforgeeks.org/maximize-the-number-of-sum-pairs-which-are-divisible-by-k/)

给定一组 **N 个**整数和一个 **K 个**整数。任务是打印可被 k 整除的最大对数(A[I]+A[j])。
**注**:一个特定的索引号不能被考虑在多个对中。
**示例:**

> **输入:** a[] = {1，2，2，3，2，4，10}，k =2
> **输出:** 3
> 该对为:(1，2)、(4，5)、(0，3)
> **输入:** a[] = {1，2，2，3，2，4，5}，k = 3
> **输出:** 2

**天真方法**:天真方法是使用两个循环进行迭代，并计算总和可被 k 整除的对的总数。这种方法的时间复杂度是 O(N^2).
**有效方法**:一个有效的方法是使用哈希技术来解决问题。可以遵循以下步骤来解决上述问题。

*   最初，对于每个数组元素，将哈希[a[i]%k]增加 1。
*   迭代地图，获取所有可能的哈希值。
*   如果哈希值为 0，那么对的数量将是哈希[0]/2。
*   之后对于每个哈希值 x，我们可以使用 *(hash[x]，hash[k-x])* 的最小值，并使用它们来创建对。
*   相应地从哈希值中减去使用的对的数量。

下面是上述方法的实现。

## C++

```
// C++ program to implement the above
// approach
#include <bits/stdc++.h>
using namespace std;

// Function to maximize the number of pairs
int findMaximumPairs(int a[], int n, int k)
{

    // Hash-table
    unordered_map<int, int> hash;
    for (int i = 0; i < n; i++)
        hash[a[i] % k]++;

    int count = 0;

    // Iterate for all numbers less than hash values
    for (auto it : hash) {

        // If the number is 0
        if (it.first == 0) {

            // We take half since same number
            count += it.second / 2;
            if (it.first % 2 == 0)
                hash[it.first] = 0;
            else
                hash[it.first] = 1;
        }
        else {

            int first = it.first;
            int second = k - it.first;

            // Check for minimal occurrence
            if (hash[first] < hash[second]) {
                // Take the minimal
                count += hash[first];

                // Subtract the pairs used
                hash[second] -= hash[first];
                hash[first] = 0;
            }
            else if (hash[first] > hash[second]) {
                // Take the minimal
                count += hash[second];

                // Subtract the pairs used
                hash[first] -= hash[second];
                hash[second] = 0;
            }
            else {
                // Check if numbers are same
                if (first == second) {

                    // If same then number of pairs will be half
                    count += it.second / 2;

                    // Check for remaining
                    if (it.first % 2 == 0)
                        hash[it.first] = 0;
                    else
                        hash[it.first] = 1;
                }
                else {

                    // Store the number of pairs
                    count += hash[first];
                    hash[first] = 0;
                    hash[second] = 0;
                }
            }
        }
    }

    return count;
}

// Driver code
int main()
{
    int a[] = { 1, 2, 2, 3, 2, 4, 10 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 2;
    cout << findMaximumPairs(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the above
// approach
import java.util.*;

class GFG
{

// Function to maximize the number of pairs
static int findMaximumPairs(int a[], int n, int k)
{

    // Hash-table
    HashMap<Integer,Integer> hash = new HashMap<Integer,Integer>();
    for (int i = 0; i < n; i++)
        if(hash.containsKey(a[i] % k)){
            hash.put(a[i] % k, hash.get(a[i] % k)+1);
        }
        else{
            hash.put(a[i] % k, 1);
        }

    int count = 0;

    // Iterate for all numbers less than hash values
    for (Map.Entry<Integer,Integer> it : hash.entrySet()){

        // If the number is 0
        if (it.getKey() == 0) {

            // We take half since same number
            count += it.getValue() / 2;
            if (it.getKey() % 2 == 0)
                hash.put(it.getKey(), 0);
            else
                hash.put(it.getKey(), 1);
        }
        else {

            int first = it.getKey();
            int second = k - it.getKey();

            // Check for minimal occurrence
            if (hash.get(first) < hash.get(second))
            {

                // Take the minimal
                count += hash.get(first);

                // Subtract the pairs used
                hash.put(second, hash.get(second)-hash.get(first));
                hash.put(first, 0);
            }
            else if (hash.get(first) > hash.get(second))
            {

                // Take the minimal
                count += hash.get(second);

                // Subtract the pairs used
                hash.put(first, hash.get(first)-hash.get(second));
                hash.put(second, 0);
            }
            else
            {
                // Check if numbers are same
                if (first == second) {

                    // If same then number of pairs will be half
                    count += it.getValue() / 2;

                    // Check for remaining
                    if (it.getKey() % 2 == 0)
                        hash.put(it.getKey(), 0);
                    else
                        hash.put(it.getKey(), 1);
                }
                else {

                    // Store the number of pairs
                    count += hash.get(first);
                    hash.put(first, 0);
                    hash.put(second, 0);
                }
            }
        }
    }

    return count;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 1, 2, 2, 3, 2, 4, 10 };
    int n = a.length;
    int k = 2;
    System.out.print(findMaximumPairs(a, n, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to maximize the
# number of pairs
def findMaximumPairs(a, n, k) :

    # Hash-table
    hash = {};
    for i in range(n) :
        if a[i] % k not in hash :
            hash[a[i] % k] = 0

        hash[a[i] % k] += 1

    count = 0;

    # Iterate for all numbers less
    # than hash values
    for keys,values in hash.items() :

        # If the number is 0
        if (keys == 0) :

            # We take half since same number
            count += values // 2;
            if (keys % 2 == 0) :
                hash[keys] = 0;
            else :
                hash[keys] = 1;

        else :

            first = keys;
            second = k -keys;

            # Check for minimal occurrence
            if (hash[first] < hash[second]) :

                # Take the minimal
                count += hash[first];

                # Subtract the pairs used
                hash[second] -= hash[first];
                hash[first] = 0;

            elif (hash[first] > hash[second]) :

                # Take the minimal
                count += hash[second];

                # Subtract the pairs used
                hash[first] -= hash[second];
                hash[second] = 0;

            else :

                # Check if numbers are same
                if (first == second) :

                    # If same then number of pairs
                    # will be half
                    count += values // 2;

                    # Check for remaining
                    if (keys % 2 == 0) :
                        hash[keys] = 0;
                    else :
                        hash[keys] = 1;

                else :

                    # Store the number of pairs
                    count += hash[first];
                    hash[first] = 0;
                    hash[second] = 0;

    return count;

# Driver code
if __name__ == "__main__" :

    a = [ 1, 2, 2, 3, 2, 4, 10 ];
    n = len(a)
    k = 2;
    print(findMaximumPairs(a, n, k));

# This code is contributed by Ryuga
```

## java 描述语言

```
<script>
// Javascript program to implement the above
// approach

// Function to maximize the number of pairs
function findMaximumPairs(a, n, k) {

    // Hash-table
    let hash = new Map();
    for (let i = 0; i < n; i++) {
        if (hash.has(a[i] % k)) {
            hash.set(a[i] % k, hash.get(a[i] % k) + 1)
        } else {
            hash.set(a[i] % k, 1)
        }
    }

    let count = 0;

    // Iterate for all numbers less than hash values
    for (let it of hash) {

        // If the number is 0
        if (it[0] == 0) {

            // We take half since same number
            count += Math.floor(it[1] / 2);
            if (it[0] % 2 == 0)
                hash.set(it[0], 0);
            else
                hash.set(it[0], 1);
        }
        else {

            let first = it[0];
            let second = k - it[0];

            // Check for minimal occurrence
            if (hash.get(first) < hash.get(second)) {
                // Take the minimal
                count += hash.get(first);

                // Subtract the pairs used
                hash.set(second, hash.get(second) - hash.get(first));
                hash.set(first, 0);
            }
            else if (hash.get(first) > hash.get(second)) {
                // Take the minimal
                count += hash.get(second);

                // Subtract the pairs used
                hash.set(first, hash.get(first) - hash.get(second));
                hash.set(second, 0);
            }
            else {
                // Check if numbers are same
                if (first == second) {

                    // If same then number of pairs will be half
                    count += Math.floor(it[1] / 2);

                    // Check for remaining
                    if (it[0] % 2 == 0)
                        hash.set(it[0], 0);
                    else
                        hash.set(it[0], 1);
                }
                else {

                    // Store the number of pairs
                    count += hash.get(first);
                    hash.set(first, 0);
                    hash.set(second, 0);
                }
            }
        }
    }

    return count;
}

// Driver code
let a = [1, 2, 2, 3, 2, 4, 10];
let n = a.length;
let k = 2;
document.write(findMaximumPairs(a, n, k));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(最大(N，K))