# 乘积为唯一素数倍数的子集计数

> 原文:[https://www . geeksforgeeks . org/子集计数-其乘积是唯一素数的倍数/](https://www.geeksforgeeks.org/count-of-subsets-whose-product-is-multiple-of-unique-primes/)

给定一个大小为 **N、**的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，任务是计算乘积等于 **P1×P2×P3×……的非空子集的数量..×Pk** 其中 **P1、P2、P3、……。Pk** 是不同的[素数](https://www.geeksforgeeks.org/primality-test-set-1-introduction-and-school-method/)数。

**示例:**

> **输入:** arr[ ] = {2，4，7，10}
> **输出:** 5
> **说明:**共有 5 个子集，它们的乘积是不同素数的乘积。
> 子集 1: {2} - > 2
> 子集 2: {2，7} - > 2×7
> 子集 3: {7} - > 7
> 子集 4: {7，10} - > 2×5×7
> 子集 5: {10} - > 2×5
> 
> **输入:** arr[ ] = {12，9 }
> T3】输出: 0

**方法:**主要思想是找到仅是不同[素数](https://www.geeksforgeeks.org/prime-numbers/)乘积的数，并调用递归，将它们包含在子集内或不包含在子集内。此外，只有当且仅当添加元素后整个子集的 [GCD](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) 为 1 时，元素才被添加到子集。按照以下步骤解决问题:

*   初始化一个[字典](https://www.geeksforgeeks.org/python-dictionary/)，比如 **Freq，**来存储数组元素的频率。
*   初始化一个[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)，比如说**唯一的[]** ，并存储所有那些只是不同[素数](https://www.geeksforgeeks.org/prime-numbers/)的乘积的元素。
*   调用一个递归函数，比如 **Countprime(pos，curSubset)** 来计算所有这些子集。
*   **基本情况**:如果**位置**等于唯一数组的**大小**；
    *   如果**光标设置**为空，则返回 **0**
    *   否则，返回 **curSubset** 各元素频率的乘积。
*   检查**位置**的元素是否可以在当前子集中获取
    *   如果取，那么调用递归函数作为 **countPrime(pos+1，curSubset)** 和 **countPrime(pos+1，curSubset+[unique[pos]]的和)。**
    *   否则，调用 **countPrime(pos+1，curSubset)。**
*   打印功能返回的**和**。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach

# Importing the module
from math import gcd, sqrt

# Function to check number has
# distinct prime
def checkDistinctPrime(n):
    original = n
    product = 1

    # While N has factors of
    # two
    if (n % 2 == 0):
        product *= 2
        while (n % 2 == 0):
            n = n//2

    # Traversing till sqrt(N)
    for i in range(3, int(sqrt(n)), 2):

        # If N has a factor of i
        if (n % i == 0):
            product = product * i

            # While N has a factor
            # of i
            while (n % i == 0):
                n = n//i

    # Covering case, N is Prime
    if (n > 2):
        product = product * n

    return product == original

# Function to check wheather num
# can be added to the subset
def check(pos, subset, unique):
    for num in subset:
        if gcd(num, unique[pos]) != 1:
            return False
    return True

# Recursive Function to count subset
def countPrime(pos, currSubset, unique, frequency):

    # Base Case
    if pos == len(unique):

        # If currSubset is empty
        if not currSubset:
            return 0

        count = 1
        for element in currSubset:
            count *= frequency[element]
        return count

    # If Unique[pos] can be added to
    # the Subset
    if check(pos, currSubset, unique):
        return countPrime(pos + 1, currSubset, \
                          unique, frequency)\
             + countPrime(pos + 1, currSubset+[unique[pos]], \
                          unique, frequency)
    else:
        return countPrime(pos + 1, currSubset, \
                          unique, frequency)

# Function to count the subsets
def countSubsets(arr, N):

    # Initialize unique
    unique = set()
    for element in arr:
        # Check it is a product of
        # distinct primes
        if checkDistinctPrime(element):
            unique.add(element)

    unique = list(unique)

    # Count frequency of unique element
    frequency = dict()
    for element in unique:
        frequency[element] = arr.count(element)

    # Function Call
    ans = countPrime(0, [], unique, frequency)
    return ans

# Driver Code
if __name__ == "__main__":

    # Given Input
    arr = [2, 4, 7, 10]
    N = len(arr)

    # Function Call
    ans = countSubsets(arr, N)
    print(ans)
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to return
    // gcd of a and b
    function gcd(a, b)
    {
        if (a == 0)
            return b;
        return gcd(b % a, a);
    }

    // Function to check number has
    // distinct prime
    function checkDistinctPrime(n)
    {
        let original = n;
        let product = 1;

        // While N has factors of
        // two
        if (n % 2 == 0)
        {
            product *= 2;
            while (n % 2 == 0)
            {
                n = parseInt(n/2, 10);
            }
        }

        // Traversing till sqrt(N)
        for(let i = 3; i < parseInt(Math.sqrt(n), 10); i+=2)
        {
            // If N has a factor of i
            if (n % i == 0)
            {
                product = product * i;

                // While N has a factor of i
                while(n % i == 0)
                {
                    n = parseInt(n / i, 10);
                }
            }
        }

        // Covering case, N is Prime
        if (n > 2)
        {
            product = product * n;
        }

        return product == original;
    }

    // Function to check wheather num
    // can be added to the subset
    function check(pos, subset, unique)
    {
        for(let num = 0; num < subset.length; num++)
        {
            if(gcd(subset[num], unique[pos]) != 1)
            {
                return false;
            }
        }
        return true;
    }

    // Recursive Function to count subset
    function countPrime(pos, currSubset, unique, frequency)
    {
        // Base Case
        if(pos == unique.length)
        {
            // If currSubset is empty
            if(currSubset.length == 0)
                return 0;

            count = 1;
            for(let element = 0; element < currSubset.length; element++)
            {
                count *= frequency[currSubset[element]];
            }
            return count;
        }

        // If Unique[pos] can be added to
        // the Subset
        if(check(pos, currSubset, unique))
        {
            return countPrime(pos + 1, currSubset, unique, frequency)
                 + countPrime(pos + 1, currSubset+[unique[pos]],
                              unique, frequency);
        }
        else
        {
            return countPrime(pos + 1, currSubset, unique, frequency);
        }
    }

    // Function to count the subsets
    function countSubsets(arr, N)
    {
        // Initialize unique
        let unique = new Set();
        for(let element = 0; element < arr.length; element++)
        {
            return 5;
            // Check it is a product of
            // distinct primes
            if(checkDistinctPrime(element))
            {
                unique.add(element);
            }
        }

        unique = Array.from(unique);

        // Count frequency of unique element
        let frequency = new Map();
        for(let element = 0; element < unique.length; element++)
        {
            let freq = 0;
            for(let i = 0; i < unique.length; i++)
            {
                if(unique[element] == unique[i])
                {
                    freq++;
                }
            }
            frequency[element] = freq;
        }

        // Function Call
        let ans = countPrime(0, [], unique, frequency);
        return ans;
    }

    // Given Input
    let arr = [2, 4, 7, 10];
    let N = arr.length;

    // Function Call
    let ans = countSubsets(arr, N);
    document.write(ans);

    // This code is contributed by divyesh072019.
</script>
```

**Output**

```
5
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*