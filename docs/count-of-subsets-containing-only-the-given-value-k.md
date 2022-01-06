# 仅包含给定值 K 的子集计数

> 原文:[https://www . geesforgeks . org/子集计数-仅包含给定值-k/](https://www.geeksforgeeks.org/count-of-subsets-containing-only-the-given-value-k/)

给定一个数组 **arr[]** 和数组中至少出现一次的数字 **K** ，任务是找出数组中子集的数量，使得每个子集只包含给定值 **K** 。
**举例:**

> **输入:** arr[] = {1，0，0，1，0，1，2，5，2，1}，K = 0
> **输出:** 4
> **解释:**
> 从索引 2 和 3 处数组中出现的两个 0，可以形成 3 个子序列:{0}、{0}、{0，0}
> 从索引 5 处数组中出现的 0，可以形成 1 个子序列:{0}
> 因此
> **输入:** arr[] = {1，0，0，1，1，0，0，2，3，5}，K = 1
> **输出:** 4

**方法:**为了[找到子集](https://www.geeksforgeeks.org/finding-all-subsets-of-a-given-set-in-java/)的数量，需要对给定集合中不同数量的元素形成的子集的数量进行一次观察。
那么，让 N 是我们需要找到子集的元素数。
然后，如果:

```
N = 1: Only one subset can be formed.
N = 2: Three subsets can be formed.
N = 3: Six subsets can be formed.
N = 4: Ten subsets can be formed.
.
.
.
N = K: (K * (K + 1))/2 subsets can be formed.
```

由于我们正在计算由值 K 的连续出现所形成的子集的数量，所以想法是找到给定数组中存在的连续 K 的计数，并使用给定的公式来找到计数。
以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// number of subsets formed by
// the given value K
#include <iostream>
using namespace std;

// Function to find the number
// of subsets formed by the
// given value K
int count(int arr[], int N, int K)
{
    // Count is used to maintain the
    // number of continuous K's
    int count = 0, ans = 0;

    // Iterating through the array
    for (int i = 0; i < N; i++) {

        // If the element in the array
        // is equal to K
        if (arr[i] == K) {
            count = count + 1;
        }
        else {

            // count*(count+1)/2 is the
            // total number of subsets
            // with only K as their element
            ans += (count * (count + 1)) / 2;

            // Change count to 0 because
            // other element apart from
            // K has been found
            count = 0;
        }
    }

    // To handle the last set of K's
    ans = ans + (count * (count + 1)) / 2;
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 1, 0, 0, 1, 1, 0, 0 };
    int N = sizeof(arr) / sizeof(int);
    int K = 0;

    cout << count(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// number of subsets formed by
// the given value K
class GFG{

// Function to find the number
// of subsets formed by the
// given value K
static int count(int arr[], int N, int K)
{
    // Count is used to maintain the
    // number of continuous K's
    int count = 0, ans = 0;

    // Iterating through the array
    for (int i = 0; i < N; i++) {

        // If the element in the array
        // is equal to K
        if (arr[i] == K) {
            count = count + 1;
        }
        else {

            // count*(count+1)/2 is the
            // total number of subsets
            // with only K as their element
            ans += (count * (count + 1)) / 2;

            // Change count to 0 because
            // other element apart from
            // K has been found
            count = 0;
        }
    }

    // To handle the last set of K's
    ans = ans + (count * (count + 1)) / 2;
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 0, 0, 1, 1, 0, 0 };
    int N = arr.length;
    int K = 0;

    System.out.print(count(arr, N, K));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 implementation to find the
# number of subsets formed by
# the given value K

# Function to find the number
# of subsets formed by the
# given value K
def count(arr, N, K):
    # Count is used to maintain the
    # number of continuous K's
    count = 0
    ans = 0

    # Iterating through the array
    for i in range(N):
        # If the element in the array
        # is equal to K
        if (arr[i] == K):
            count = count + 1

        else:
            # count*(count+1)/2 is the
            # total number of subsets
            # with only K as their element
            ans += (count * (count + 1)) // 2

            # Change count to 0 because
            # other element apart from
            # K has been found
            count = 0

    # To handle the last set of K's
    ans = ans + (count * (count + 1)) // 2
    return ans

# Driver code
if __name__ == '__main__':
    arr =  [1, 0, 0, 1, 1, 0, 0]
    N = len(arr)
    K = 0

    print(count(arr, N, K))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation to find the
// number of subsets formed by
// the given value K
using System;

class GFG{

// Function to find the number
// of subsets formed by the
// given value K
static int count(int []arr, int N, int K)
{
    // Count is used to maintain the
    // number of continuous K's
    int count = 0, ans = 0;

    // Iterating through the array
    for(int i = 0; i < N; i++)
    {

       // If the element in the array
       // is equal to K
       if (arr[i] == K)
       {
           count = count + 1;

       }
       else
       {
           // count*(count+1)/2 is the
           // total number of subsets
           // with only K as their element
           ans += (count * (count + 1)) / 2;

           // Change count to 0 because
           // other element apart from
           // K has been found
           count = 0;

       }
    }

    // To handle the last set of K's
    ans = ans + (count * (count + 1)) / 2;
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 0, 0, 1, 1, 0, 0 };
    int N = arr.Length;
    int K = 0;

    Console.Write(count(arr, N, K));
}
}

//This is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
    // Javascript implementation to find the
    // number of subsets formed by
    // the given value K

    // Function to find the number
    // of subsets formed by the
    // given value K
    function count(arr, N, K)
    {

        // Count is used to maintain the
        // number of continuous K's
        let count = 0, ans = 0;

        // Iterating through the array
        for (let i = 0; i < N; i++)
        {

            // If the element in the array
            // is equal to K
            if (arr[i] == K) {
                count = count + 1;
            }
            else {

                // count*(count+1)/2 is the
                // total number of subsets
                // with only K as their element
                ans += (count * (count + 1)) / 2;

                // Change count to 0 because
                // other element apart from
                // K has been found
                count = 0;
            }
        }

        // To handle the last set of K's
        ans = ans + (count * (count + 1)) / 2;
        return ans;
    }

    let arr = [ 1, 0, 0, 1, 1, 0, 0 ];
    let N = arr.length;
    let K = 0;

    document.write(count(arr, N, K));

    //his code is contributed by divyeshrabadiya
</script>
```

**Output:** 

```
6
```

**时间复杂度:** *O(N)* ，其中 N 是数组的大小。