# 总和 N 在 0 到 N 范围内的斐波那契对的计数

> 原文:[https://www . geeksforgeeks . org/Fibonacci-count-of-of-Fibonacci-pairs-with-sum-n-in-range-0-n/](https://www.geeksforgeeks.org/count-of-fibonacci-pairs-with-sum-n-in-range-0-to-n/)

给定一个数字 **N** ，任务是在范围 **0 到 N** 内找到[斐波那契对](https://www.geeksforgeeks.org/tag/fibonacci/)的计数，其和为 **N** 。

**示例:**

> **输入:** N = 90
> **输出:** 1
> **解释:**
> 只有和等于 90 的范围【0，90】内的斐波那契对才是{1，89}
> 
> **输入:** N = 3
> **输出:** 2
> **解释:**
> 范围【0，3】内的斐波那契对，其和等于 3 的是{0，3}，{1，2}

**进场:**

1.  想法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)来预先计算并存储小于等于 **N** 的[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)到散列中
2.  将计数器变量初始化为 0
3.  然后，对于该散列中的每个元素 **K** ，检查散列中是否也存在**N–K**。
4.  如果 K 和 N–K 都在哈希中，则递增计数器变量

下面是上述方法的实现:

## C++

```
// C++ program to find count of
// Fibonacci pairs whose
// sum can be represented as N

#include <bits/stdc++.h>
using namespace std;

// Function to create hash table
// to check Fibonacci numbers
void createHash(set<int>& hash, int maxElement)
{
    // Storing the first two numbers
    // in the hash
    int prev = 0, curr = 1;
    hash.insert(prev);
    hash.insert(curr);

    // Finding Fibonacci numbers up to N
    // and storing them in the hash
    while (curr < maxElement) {

        int temp = curr + prev;
        hash.insert(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find count of Fibonacci
// pair with the given sum
int findFibonacciPairCount(int N)
{
    // creating a set containing
    // all fibonacci numbers
    set<int> hash;
    createHash(hash, N);

    // Initialize count with 0
    int count = 0;

    // traverse the hash to find
    // pairs with sum as N
    set<int>::iterator itr;
    for (itr = hash.begin();
 *itr <= (N / 2);
 itr++) {

        // If both *itr and
//(N - *itr) are Fibonacci
        // increment the count
        if (hash.find(N - *itr)
 != hash.end()) {

            // Increase the count
            count++;
        }
    }

    // Return the count
    return count;
}

// Driven code
int main()
{
    int N = 90;
    cout << findFibonacciPairCount(N)
<< endl;

    N = 3;
    cout << findFibonacciPairCount(N)
 << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find count of
// Fibonacci pairs whose
// sum can be represented as N
import java.util.*;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<Integer> hash, int maxElement)
{
    // Storing the first two numbers
    // in the hash
    int prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    // Finding Fibonacci numbers up to N
    // and storing them in the hash
    while (curr < maxElement) {

        int temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find count of Fibonacci
// pair with the given sum
static int findFibonacciPairCount(int N)
{
    // creating a set containing
    // all fibonacci numbers
    HashSet<Integer> hash = new HashSet<Integer>();
    createHash(hash, N);

    // Initialize count with 0
    int count = 0;
    int i = 0;

    // traverse the hash to find
    // pairs with sum as N
    for (int itr : hash) {
        i++;

        // If both *itr and
        //(N - *itr) are Fibonacci
        // increment the count
        if (hash.contains(N - itr)) {

            // Increase the count
            count++;
        }
        if(i == hash.size()/2)
            break;
    }

    // Return the count
    return count;
}

// Driven code
public static void main(String[] args)
{
    int N = 90;
    System.out.print(findFibonacciPairCount(N)
+"\n");

    N = 3;
    System.out.print(findFibonacciPairCount(N)
 +"\n");

}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find count of
# Fibonacci pairs whose sum can be
# represented as N

# Function to create hash table
# to check Fibonacci numbers
def createHash(Hash, maxElement):

    # Storing the first two numbers
    # in the hash
    prev, curr = 0, 1
    Hash.add(prev)
    Hash.add(curr)

    # Finding Fibonacci numbers up to N
    # and storing them in the hash
    while (curr < maxElement):
        temp = curr + prev
        Hash.add(temp)
        prev = curr
        curr = temp

# Function to find count of Fibonacci
# pair with the given sum
def findFibonacciPairCount(N):

    # Creating a set containing
    # all fibonacci numbers
    Hash = set()
    createHash(Hash, N)

    # Initialize count with 0
    count = 0
    i = 0

    # Traverse the hash to find
    # pairs with sum as N
    for itr in Hash:
        i += 1

        # If both *itr and 
        #(N - *itr) are Fibonacci
        # increment the count
        if ((N - itr) in Hash):

            # Increase the count
            count += 1

        if (i == (len(Hash) // 2)):
            break

    # Return the count
    return count

# Driver Code
N = 90
print(findFibonacciPairCount(N))

N = 3
print(findFibonacciPairCount(N))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find count of
// Fibonacci pairs whose
// sum can be represented as N
using System;
using System.Collections.Generic;

class GFG{

// Function to create hash table
// to check Fibonacci numbers
static void createHash(HashSet<int> hash, int maxElement)
{
    // Storing the first two numbers
    // in the hash
    int prev = 0, curr = 1;
    hash.Add(prev);
    hash.Add(curr);

    // Finding Fibonacci numbers up to N
    // and storing them in the hash
    while (curr < maxElement) {

        int temp = curr + prev;
        hash.Add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find count of Fibonacci
// pair with the given sum
static int findFibonacciPairCount(int N)
{
    // creating a set containing
    // all fibonacci numbers
    HashSet<int> hash = new HashSet<int>();
    createHash(hash, N);

    // Initialize count with 0
    int count = 0;
    int i = 0;

    // traverse the hash to find
    // pairs with sum as N
    foreach (int itr in hash) {
        i++;

        // If both *itr and
        //(N - *itr) are Fibonacci
        // increment the count
        if (hash.Contains(N - itr)) {

            // Increase the count
            count++;
        }
        if(i == hash.Count/2)
            break;
    }

    // Return the count
    return count;
}

// Driven code
public static void Main(String[] args)
{
    int N = 90;
    Console.Write(findFibonacciPairCount(N)
                    +"\n");

    N = 3;
    Console.Write(findFibonacciPairCount(N)
                     +"\n");

}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find count of
// Fibonacci pairs whose
// sum can be represented as N

// Function to create hash table
// to check Fibonacci numbers
function createHash(hash, maxElement)
{
    // Storing the first two numbers
    // in the hash
    var prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    // Finding Fibonacci numbers up to N
    // and storing them in the hash
    while (curr < maxElement) {

        var temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find count of Fibonacci
// pair with the given sum
function findFibonacciPairCount(N)
{
    // creating a set containing
    // all fibonacci numbers
    var hash = new Set();
    createHash(hash, N);

    // Initialize count with 0
    var count = 0, i =0;

    // traverse the hash to find
    // pairs with sum as N
    hash.forEach(element => {
        i++;

        if(hash.size >= parseInt(i*2))
        {

        // If both *itr and
        //(N - *itr) are Fibonacci
        // increment the count
        if (hash.has(N-element))
        {

            // Increase the count
            count++;
        }
        }

    });

    // Return the count
    return count;
}

// Driven code
var N = 90;
document.write( findFibonacciPairCount(N) + "<br>")
N = 3;
document.write( findFibonacciPairCount(N) + "<br>")

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
1
2
```

**性能分析:**

*   **时间复杂度:**在上面的方法中，构建斐波那契数小于 **N** 的 hashmap 将是 **O(N)** 运算。然后，对于 hashmap 中的每个元素，我们搜索另一个元素，使得搜索时间复杂度为 **O(N * log N)** 。所以整体时间复杂度为 ***O(N * log N)***
*   **辅助空间复杂度:**在上面的方法中，我们使用额外的空间来存储 hashmap 值。所以辅助空间的复杂度是*T3【O(N)T5】*